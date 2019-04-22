尽管我们可以通过网络连接到数据库, 但这并不意味着我们实际上可以获取对数据本身的访问权限。 按照分层方法, 我们需要确保只有需要访问数据的用户才能实际访问它。 在这种情况下, 身份验证和授权会发挥作用。

## <a name="authentication"></a>Authentication

身份验证是验证标识的过程。 此标识可以是用户、系统上运行的服务或系统本身 (如虚拟机)。 通过身份验证过程, 我们确保用户或系统是其声称的身份。 sql 数据库支持两种类型的身份验证: SQL 身份验证和 Azure Active Directory 身份验证。

### <a name="sql-authentication"></a>SQL 身份验证

SQL 身份验证方法使用用户名和密码。 可以在 master 数据库中创建用户帐户, 并且可以在服务器上的所有数据库中授予权限, 也可以在数据库本身 (称为包含的用户) 中创建用户帐户, 并授予仅对该数据库的访问权限。 为数据库创建逻辑服务器时, 使用用户名和密码指定了 "服务器管理员" 登录名。 使用这些凭据, 可以对该服务器上的任何数据库作为数据库所有者或 "dbo" 进行身份验证。

### <a name="azure-active-directory-authentication"></a>Azure Active Directory 身份验证

此身份验证方法使用 Azure Active Directory (AD) 管理的标识, 并且受管理域和集成域支持。 尽可能使用 Azure AD 身份验证 (集成安全性)。 使用 Azure AD 身份验证, 可以在一个中央位置集中管理数据库用户和其他 Microsoft 服务的标识。 中央 ID 管理提供了一个用于管理数据库用户并简化权限管理的位置。 如果要使用 Azure ad 身份验证, 则必须创建另一个名为 "azure ad 管理员" 的服务器管理员, 这是允许管理 Azure ad 用户和组的。 此管理员还可以执行常规服务器管理员可以执行的所有操作。

## <a name="authorization"></a>批准

授权是指标识可以在 Azure SQL 数据库中执行的操作。 这是由直接授予用户帐户和/或数据库角色成员身份的权限控制的。 数据库角色用于将权限组合在一起, 以简化管理, 并将用户添加到角色以向其授予角色拥有的权限。 这些权限可以授予诸如登录到数据库的功能、读取表的能力以及在数据库中添加和删除列的功能。 作为一种最佳做法, 您应向用户授予所需的最少权限。 向 SQL 和 Azure AD 用户授予授权的过程是相同的。

在本示例中, 您要连接的服务器管理员帐户是 db_owner 角色的成员, 它具有在数据库中执行任何操作的权限。

## <a name="authentication-and-authorization-in-practice"></a>实践中的身份验证和授权

现在, 我们来看看如何设置用户并向其授予对数据库的访问权限。 在这种情况下, 我们将为用户使用 SQL 身份验证, 但如果我们使用的是 Azure AD 身份验证, 则该过程基本上是相同的。

### <a name="create-a-database-user"></a>创建数据库用户

接下来, 创建一个新用户, 我们可以使用它授予对的访问权限。

1. 在云命令行管理程序中, 在您的_appServer_ VM 上, 再次`ADMINUSER`连接到您的数据库。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

1. 运行以下命令以创建新用户。 这将是_包含的用户_, 并且只允许访问_marketplace_数据库。 你可以根据需要随意调整密码, 但请务必在将来的步骤中需要它时对其进行说明。

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    GO
    ```

使用这些凭据, 用户将能够对数据库进行身份验证, 但无权访问任何数据。 让我们授予此用户访问权限。

### <a name="grant-permissions-to-a-user"></a>向用户授予权限

让该用户成为`db_datareader`和`db_datawriter`角色的成员, 分别授予对数据库的读取和写入权限。 我们还希望阻止此用户访问具有地址的表格。

1. 尽管仍连接到`sqlcmd` _appServer_, 请运行以下 t-sql, 向刚刚创建的用户`db_datareader`授予`db_datawriter`和角色。

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    GO
    ```

1. 我们可以进一步缩小访问范围。 我们可以使用 deny 运算符拒绝用户对数据库中其他元素的访问。 运行以下 t-sql 以拒绝用户_ApplicationUser_从`SalesLT.Address`表中选择数据的功能。

    ```sql
    DENY SELECT ON SalesLT.Address TO ApplicationUser;
    GO
    ```

现在, 让我们以该用户的形式登录, 并查看此操作。

1. 仍在 t-sql 提示符处, 键入`exit`退出会话。

1. 现在, 让我们重新登录到数据库, 但作为刚创建的用户。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U 'ApplicationUser' -P '<password>' -N -l 30
    ```

1. 运行以下查询。 这将从用户向其授予访问权限的表中提取数据。

    ```sql
    SELECT FirstName, LastName, EmailAddress, Phone FROM SalesLT.Customer;
    GO
    ```

    你应获取客户列表。

    ```output
    FirstName      LastName       EmailAddress                    Phone
    -------------- -------------- ------------------------------- ------------
    Orlando        Gee            orlando0@adventure-works.com    245-555-0173
    Keith          Harris         keith0@adventure-works.com      170-555-0127
    Donna          Carreras       donna0@adventure-works.com      279-555-0130
    Janet          Gates          janet1@adventure-works.com      710-555-0173
    ...
    ```

1. 现在, 我们来看看当我们尝试查询我们无法访问的表时, 会发生什么情况。

    ```sql
    SELECT * FROM SalesLT.Address;
    GO
    ```

    您应该会收到一条消息, 指出您无权访问此表。

    ```output
    Msg 229, Level 14, State 5, Server server-22942, Line 1
    The SELECT permission was denied on the object 'Address', database 'marketplace', schema 'SalesLT'.
    ```

正如您在此处看到的, 即使我们已授予对数据库的读/写访问权限, 我们也可以通过明确拒绝对表的访问来加强对数据的访问。 如果有多个共享类似访问权限的用户, 您可以创建具有适当权限的自定义角色, 并简化管理。

正确保护数据库和仅在必要的地方授予访问权限是非常重要的。 Azure SQL Database 提供了内置功能, 可以完全控制身份验证和授权身份的能力, 以访问数据库中的数据。