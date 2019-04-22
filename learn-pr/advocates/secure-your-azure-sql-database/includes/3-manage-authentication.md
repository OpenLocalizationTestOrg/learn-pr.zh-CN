<span data-ttu-id="37e1e-101">尽管我们可以通过网络连接到数据库, 但这并不意味着我们实际上可以获取对数据本身的访问权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-101">Even though we may be able to connect to the database over the network, that doesn't mean we can actually gain access to the data itself.</span></span> <span data-ttu-id="37e1e-102">按照分层方法, 我们需要确保只有需要访问数据的用户才能实际访问它。</span><span class="sxs-lookup"><span data-stu-id="37e1e-102">Following a layered approach, we'll want to ensure that only users who need access to the data can actually access it.</span></span> <span data-ttu-id="37e1e-103">在这种情况下, 身份验证和授权会发挥作用。</span><span class="sxs-lookup"><span data-stu-id="37e1e-103">This is where authentication and authorization come in to play.</span></span>

## <a name="authentication"></a><span data-ttu-id="37e1e-104">Authentication</span><span class="sxs-lookup"><span data-stu-id="37e1e-104">Authentication</span></span>

<span data-ttu-id="37e1e-105">身份验证是验证标识的过程。</span><span class="sxs-lookup"><span data-stu-id="37e1e-105">Authentication is the process of verifying an identity.</span></span> <span data-ttu-id="37e1e-106">此标识可以是用户、系统上运行的服务或系统本身 (如虚拟机)。</span><span class="sxs-lookup"><span data-stu-id="37e1e-106">This identity could be a user, a service running on a system, or a system itself (such as a virtual machine).</span></span> <span data-ttu-id="37e1e-107">通过身份验证过程, 我们确保用户或系统是其声称的身份。</span><span class="sxs-lookup"><span data-stu-id="37e1e-107">Through the process of authentication, we ensure that the person or system is who they claim to be.</span></span> <span data-ttu-id="37e1e-108">sql 数据库支持两种类型的身份验证: SQL 身份验证和 Azure Active Directory 身份验证。</span><span class="sxs-lookup"><span data-stu-id="37e1e-108">SQL Database supports two types of authentication: SQL authentication and Azure Active Directory authentication.</span></span>

### <a name="sql-authentication"></a><span data-ttu-id="37e1e-109">SQL 身份验证</span><span class="sxs-lookup"><span data-stu-id="37e1e-109">SQL authentication</span></span>

<span data-ttu-id="37e1e-110">SQL 身份验证方法使用用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="37e1e-110">SQL authentication method uses a username and password.</span></span> <span data-ttu-id="37e1e-111">可以在 master 数据库中创建用户帐户, 并且可以在服务器上的所有数据库中授予权限, 也可以在数据库本身 (称为包含的用户) 中创建用户帐户, 并授予仅对该数据库的访问权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-111">User accounts can be created in the master database and can be granted permissions in all databases on the server, or they can be created in the database itself (called contained users) and given access to only that database.</span></span> <span data-ttu-id="37e1e-112">为数据库创建逻辑服务器时, 使用用户名和密码指定了 "服务器管理员" 登录名。</span><span class="sxs-lookup"><span data-stu-id="37e1e-112">When you created the logical server for your database, you specified a "server admin" login with a username and password.</span></span> <span data-ttu-id="37e1e-113">使用这些凭据, 可以对该服务器上的任何数据库作为数据库所有者或 "dbo" 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="37e1e-113">Using these credentials, you can authenticate to any database on that server as the database owner, or "dbo".</span></span>

### <a name="azure-active-directory-authentication"></a><span data-ttu-id="37e1e-114">Azure Active Directory 身份验证</span><span class="sxs-lookup"><span data-stu-id="37e1e-114">Azure Active Directory authentication</span></span>

<span data-ttu-id="37e1e-115">此身份验证方法使用 Azure Active Directory (AD) 管理的标识, 并且受管理域和集成域支持。</span><span class="sxs-lookup"><span data-stu-id="37e1e-115">This authentication method uses identities managed by Azure Active Directory (AD) and is supported for managed and integrated domains.</span></span> <span data-ttu-id="37e1e-116">尽可能使用 Azure AD 身份验证 (集成安全性)。</span><span class="sxs-lookup"><span data-stu-id="37e1e-116">Use Azure AD authentication (integrated security) whenever possible.</span></span> <span data-ttu-id="37e1e-117">使用 Azure AD 身份验证, 可以在一个中央位置集中管理数据库用户和其他 Microsoft 服务的标识。</span><span class="sxs-lookup"><span data-stu-id="37e1e-117">With Azure AD authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="37e1e-118">中央 ID 管理提供了一个用于管理数据库用户并简化权限管理的位置。</span><span class="sxs-lookup"><span data-stu-id="37e1e-118">Central ID management provides a single place to manage database users and simplifies permission management.</span></span> <span data-ttu-id="37e1e-119">如果要使用 Azure ad 身份验证, 则必须创建另一个名为 "azure ad 管理员" 的服务器管理员, 这是允许管理 Azure ad 用户和组的。</span><span class="sxs-lookup"><span data-stu-id="37e1e-119">If you want to use Azure AD authentication, you must create another server admin called the "Azure AD admin," which is allowed to administer Azure AD users and groups.</span></span> <span data-ttu-id="37e1e-120">此管理员还可以执行常规服务器管理员可以执行的所有操作。</span><span class="sxs-lookup"><span data-stu-id="37e1e-120">This admin can also perform all operations that a regular server admin can.</span></span>

## <a name="authorization"></a><span data-ttu-id="37e1e-121">批准</span><span class="sxs-lookup"><span data-stu-id="37e1e-121">Authorization</span></span>

<span data-ttu-id="37e1e-122">授权是指标识可以在 Azure SQL 数据库中执行的操作。</span><span class="sxs-lookup"><span data-stu-id="37e1e-122">Authorization refers to what an identity can do within an Azure SQL Database.</span></span> <span data-ttu-id="37e1e-123">这是由直接授予用户帐户和/或数据库角色成员身份的权限控制的。</span><span class="sxs-lookup"><span data-stu-id="37e1e-123">This is controlled by permissions granted directly to the user account and/or database role memberships.</span></span> <span data-ttu-id="37e1e-124">数据库角色用于将权限组合在一起, 以简化管理, 并将用户添加到角色以向其授予角色拥有的权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-124">A database role is used to group permissions together to ease administration, and a user is added to a role to be granted the permissions the role has.</span></span> <span data-ttu-id="37e1e-125">这些权限可以授予诸如登录到数据库的功能、读取表的能力以及在数据库中添加和删除列的功能。</span><span class="sxs-lookup"><span data-stu-id="37e1e-125">These permissions can grant things such as the ability to log in to the database, the ability to read a table, and the ability to add and remove columns from a database.</span></span> <span data-ttu-id="37e1e-126">作为一种最佳做法, 您应向用户授予所需的最少权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-126">As a best practice, you should grant users the least privileges necessary.</span></span> <span data-ttu-id="37e1e-127">向 SQL 和 Azure AD 用户授予授权的过程是相同的。</span><span class="sxs-lookup"><span data-stu-id="37e1e-127">The process of granting authorization to both SQL and Azure AD users is the same.</span></span>

<span data-ttu-id="37e1e-128">在本示例中, 您要连接的服务器管理员帐户是 db_owner 角色的成员, 它具有在数据库中执行任何操作的权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-128">In our example here, the server admin account you are connecting with is a member of the db_owner role, which has authority to do anything within the database.</span></span>

## <a name="authentication-and-authorization-in-practice"></a><span data-ttu-id="37e1e-129">实践中的身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="37e1e-129">Authentication and authorization in practice</span></span>

<span data-ttu-id="37e1e-130">现在, 我们来看看如何设置用户并向其授予对数据库的访问权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-130">Let's now take a look at how to set up a user and grant them access to a database.</span></span> <span data-ttu-id="37e1e-131">在这种情况下, 我们将为用户使用 SQL 身份验证, 但如果我们使用的是 Azure AD 身份验证, 则该过程基本上是相同的。</span><span class="sxs-lookup"><span data-stu-id="37e1e-131">In this case we'll use SQL authentication for our user, but the process would be essentially the same if we were using Azure AD authentication.</span></span>

### <a name="create-a-database-user"></a><span data-ttu-id="37e1e-132">创建数据库用户</span><span class="sxs-lookup"><span data-stu-id="37e1e-132">Create a database user</span></span>

<span data-ttu-id="37e1e-133">接下来, 创建一个新用户, 我们可以使用它授予对的访问权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-133">Let's go ahead and create a new user that we can use to grant access to.</span></span>

1. <span data-ttu-id="37e1e-134">在云命令行管理程序中, 在您的_appServer_ VM 上, 再次`ADMINUSER`连接到您的数据库。</span><span class="sxs-lookup"><span data-stu-id="37e1e-134">In cloud shell, on your _appServer_ VM, connect to your database again as your `ADMINUSER`.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

1. <span data-ttu-id="37e1e-135">运行以下命令以创建新用户。</span><span class="sxs-lookup"><span data-stu-id="37e1e-135">Run the following command to create a new user.</span></span> <span data-ttu-id="37e1e-136">这将是_包含的用户_, 并且只允许访问_marketplace_数据库。</span><span class="sxs-lookup"><span data-stu-id="37e1e-136">This will be a _contained user_ and will only allow access to the _marketplace_ database.</span></span> <span data-ttu-id="37e1e-137">你可以根据需要随意调整密码, 但请务必在将来的步骤中需要它时对其进行说明。</span><span class="sxs-lookup"><span data-stu-id="37e1e-137">Feel free to adjust the password as necessary, but be sure and note it as we'll need it for a future step.</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    GO
    ```

<span data-ttu-id="37e1e-138">使用这些凭据, 用户将能够对数据库进行身份验证, 但无权访问任何数据。</span><span class="sxs-lookup"><span data-stu-id="37e1e-138">With these credentials, the user will be able to authenticate to the database, but they aren't authorized to access any data.</span></span> <span data-ttu-id="37e1e-139">让我们授予此用户访问权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-139">Let's grant this user access.</span></span>

### <a name="grant-permissions-to-a-user"></a><span data-ttu-id="37e1e-140">向用户授予权限</span><span class="sxs-lookup"><span data-stu-id="37e1e-140">Grant permissions to a user</span></span>

<span data-ttu-id="37e1e-141">让该用户成为`db_datareader`和`db_datawriter`角色的成员, 分别授予对数据库的读取和写入权限。</span><span class="sxs-lookup"><span data-stu-id="37e1e-141">Let's make the user a member of the `db_datareader` and `db_datawriter` roles, granting access to read and write to the database, respectively.</span></span> <span data-ttu-id="37e1e-142">我们还希望阻止此用户访问具有地址的表格。</span><span class="sxs-lookup"><span data-stu-id="37e1e-142">We also want to prevent this user from accessing a table with addresses.</span></span>

1. <span data-ttu-id="37e1e-143">尽管仍连接到`sqlcmd` _appServer_, 请运行以下 t-sql, 向刚刚创建的用户`db_datareader`授予`db_datawriter`和角色。</span><span class="sxs-lookup"><span data-stu-id="37e1e-143">While still connected to `sqlcmd` on _appServer_, run the following T-SQL to grant the `db_datareader` and `db_datawriter` roles to the user we just created.</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    GO
    ```

1. <span data-ttu-id="37e1e-144">我们可以进一步缩小访问范围。</span><span class="sxs-lookup"><span data-stu-id="37e1e-144">We can narrow the scope of access further.</span></span> <span data-ttu-id="37e1e-145">我们可以使用 deny 运算符拒绝用户对数据库中其他元素的访问。</span><span class="sxs-lookup"><span data-stu-id="37e1e-145">We could deny a user's access to other elements within the database using the DENY operator.</span></span> <span data-ttu-id="37e1e-146">运行以下 t-sql 以拒绝用户_ApplicationUser_从`SalesLT.Address`表中选择数据的功能。</span><span class="sxs-lookup"><span data-stu-id="37e1e-146">Run the following T-SQL to deny the user _ApplicationUser_ the ability to select data from the `SalesLT.Address` table.</span></span>

    ```sql
    DENY SELECT ON SalesLT.Address TO ApplicationUser;
    GO
    ```

<span data-ttu-id="37e1e-147">现在, 让我们以该用户的形式登录, 并查看此操作。</span><span class="sxs-lookup"><span data-stu-id="37e1e-147">Let's now log in as that user and take a look at this in action.</span></span>

1. <span data-ttu-id="37e1e-148">仍在 t-sql 提示符处, 键入`exit`退出会话。</span><span class="sxs-lookup"><span data-stu-id="37e1e-148">While still at the T-SQL prompt, type `exit` to exit your session.</span></span>

1. <span data-ttu-id="37e1e-149">现在, 让我们重新登录到数据库, 但作为刚创建的用户。</span><span class="sxs-lookup"><span data-stu-id="37e1e-149">Now let's log back in to the database, but as the user we just created.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U 'ApplicationUser' -P '<password>' -N -l 30
    ```

1. <span data-ttu-id="37e1e-150">运行以下查询。</span><span class="sxs-lookup"><span data-stu-id="37e1e-150">Run the following query.</span></span> <span data-ttu-id="37e1e-151">这将从用户向其授予访问权限的表中提取数据。</span><span class="sxs-lookup"><span data-stu-id="37e1e-151">This is pulling data from a table that the user is authorized to access.</span></span>

    ```sql
    SELECT FirstName, LastName, EmailAddress, Phone FROM SalesLT.Customer;
    GO
    ```

    <span data-ttu-id="37e1e-152">你应获取客户列表。</span><span class="sxs-lookup"><span data-stu-id="37e1e-152">You should get back a listing of customers.</span></span>

    ```output
    FirstName      LastName       EmailAddress                    Phone
    -------------- -------------- ------------------------------- ------------
    Orlando        Gee            orlando0@adventure-works.com    245-555-0173
    Keith          Harris         keith0@adventure-works.com      170-555-0127
    Donna          Carreras       donna0@adventure-works.com      279-555-0130
    Janet          Gates          janet1@adventure-works.com      710-555-0173
    ...
    ```

1. <span data-ttu-id="37e1e-153">现在, 我们来看看当我们尝试查询我们无法访问的表时, 会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="37e1e-153">Now let's see what happens when we try to query a table that we don't have access to.</span></span>

    ```sql
    SELECT * FROM SalesLT.Address;
    GO
    ```

    <span data-ttu-id="37e1e-154">您应该会收到一条消息, 指出您无权访问此表。</span><span class="sxs-lookup"><span data-stu-id="37e1e-154">You should get a message that you don't have access to this table.</span></span>

    ```output
    Msg 229, Level 14, State 5, Server server-22942, Line 1
    The SELECT permission was denied on the object 'Address', database 'marketplace', schema 'SalesLT'.
    ```

<span data-ttu-id="37e1e-155">正如您在此处看到的, 即使我们已授予对数据库的读/写访问权限, 我们也可以通过明确拒绝对表的访问来加强对数据的访问。</span><span class="sxs-lookup"><span data-stu-id="37e1e-155">As you can see here, even though we've granted read/write access to the database, we can further secure access to data by explicitly denying access to tables.</span></span> <span data-ttu-id="37e1e-156">如果有多个共享类似访问权限的用户, 您可以创建具有适当权限的自定义角色, 并简化管理。</span><span class="sxs-lookup"><span data-stu-id="37e1e-156">If you had multiple users who shared similar access, you could create custom roles with the proper permissions and simplify your administration.</span></span>

<span data-ttu-id="37e1e-157">正确保护数据库和仅在必要的地方授予访问权限是非常重要的。</span><span class="sxs-lookup"><span data-stu-id="37e1e-157">It's important to properly secure your database, and only grant access where necessary.</span></span> <span data-ttu-id="37e1e-158">Azure SQL Database 提供了内置功能, 可以完全控制身份验证和授权身份的能力, 以访问数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="37e1e-158">Azure SQL Database provides the built-in ability to fully control the ability to authenticate and authorize identities to access the data in your database.</span></span>