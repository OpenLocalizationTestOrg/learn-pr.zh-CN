用户将连接到应用程序服务器, 以输入订单、更新其帐户并执行类似活动, 这将使用这些更改来更新数据库。 由于我们在数据库中存储了个人数据, 因此确保仅允许来自受信任的和必要的资源的访问至关重要。 让我们来看一看通过网络控制对 SQL 数据库的访问的多种方法。

## <a name="firewall-rules"></a>防火墙规则

Azure SQL 数据库具有内置防火墙, 用于允许和拒绝对数据库服务器本身以及各个数据库的网络访问。 防火墙规则是在服务器和/或数据库级别配置的, 将明确声明允许哪些网络资源建立与数据库的连接。 根据级别的不同, 您可以应用的规则如下所示:

- **服务器级别的防火墙规则**
  - 允许访问 Azure 服务
  - IP 地址规则
  - 虚拟网络规则
- **数据库级别的防火墙规则**
  - IP 地址规则

让我们进一步了解这些规则的工作原理。

### <a name="server-level-firewall-rules"></a>服务器级别的防火墙规则

这些规则使客户端可以访问您的整个 Azure SQL server, 即同一逻辑服务器中的所有数据库。 可以在服务器级别应用以下三种类型的规则。

"**允许访问 azure 服务**" 规则允许 azure 中的服务连接到 azure SQL 数据库。 如果启用此设置, 则允许来自所有 Azure 公用 IP 地址的通信。 这包括所有 azure 平台作为服务 (PaaS) 服务 (如 azure 应用服务和 azure 容器服务) 以及具有出站 internet 访问权限的 azure vm。 可以通过门户的 "防火墙" 窗格中的 "**开/关**" 选项或将0.0.0.0 作为开始和结束 ip 地址的 IP 规则配置此规则。

![允许访问 Azure 服务网络图](../media/2-allow-azure-services.png)

当您的应用程序在 azure 中的 PaaS 服务 (如 azure 逻辑应用或 azure 函数) 中运行时, 需要访问 azure SQL 数据库, 则使用此规则。 其中许多服务没有静态 IP 地址, 因此需要此规则以确保它们能够连接到数据库。

> [!IMPORTANT]
> 此选项将防火墙配置为允许来自 Azure 的所有连接, 包括来自其他客户的订阅的连接。 选择此选项时, 请确保您的登录和用户权限仅限制授权用户访问。

**IP 地址规则**是基于特定公用 IP 地址范围的规则。 将允许从允许的公共 IP 范围连接的 IP 地址连接到数据库。

![IP 地址规则网络图](../media/2-server-ip-rule-1.png)

当您有需要访问您的数据库的静态公共 IP 地址时, 可以使用这些规则。

**虚拟网络规则**允许你显式允许一个或多个 Azure 虚拟网络 (vnet) 内的指定子网中的连接。 虚拟网络规则可以对数据库提供更大的访问控制, 并且可以是首选选项, 具体取决于您的应用场景。 由于 Azure VNet 地址空间是专用的, 因此您可以有效消除对公用 IP 地址的暴露和与您控制的那些地址的安全连接。

![VNet 规则网络图](../media/2-vnet-rule.png)

当您的 Azure vm 需要访问您的数据库时, 将使用虚拟网络规则。

对于服务器级别的规则, 可以通过门户、PowerShell、CLI 和 transact-sql (t-sql) 来创建和操作上述所有项。

### <a name="database-level-firewall-rules"></a>数据库级别的防火墙规则

这些规则允许访问逻辑服务器上的单个数据库, 并存储在数据库本身中。 对于数据库级别的规则, 只能配置**IP 地址规则**。 它们的工作方式与在服务器级别应用时相同, 但范围仅限于数据库。

![数据库 IP 地址规则网络图](../media/2-db-ip-rule-1.png)

数据库级规则的优势在于它们的可移植性。 将数据库复制到另一台服务器时, 数据库级别的规则将被复制, 因为它们存储在数据库本身中。

数据库级规则的缺点是, 只能使用 IP 地址规则。 这可能会限制你拥有的灵活性, 并可能会增加管理开销。

最后, 只能通过 t-sql 创建和处理数据库级别的防火墙规则。

## <a name="restricting-network-access-in-practice"></a>在实践中限制网络访问

我们来看看这些工作在实践中的工作方式, 以及如何确保网络访问只允许必要。 请记住, 我们创建了一个 Azure SQL 数据库逻辑服务器、一个数据库和一个作为应用程序服务器的_appServer_ Linux 虚拟机。 当数据库迁移到 Azure SQL 数据库, 并且虚拟网络内部的资源需要访问它时, 通常会出现此情况。 Azure SQL Database 的防火墙功能可在许多方案中使用, 但这是一个具有实用适用性的示例, 并说明了每个规则的工作方式。

我们来看一下防火墙设置, 并查看它们的工作方式。 我们将使用云命令行管理程序和门户来实现这些练习。

我们创建的数据库当前不允许从任何连接进行访问。 这是根据我们为创建逻辑服务器和数据库而运行的命令设计的。 让我们对此进行确认。

1. 如果尚未连接, 则在云命令行管理程序中, SSH 加入你的 Linux VM。

    ```bash
    ssh <X.X.X.X>
    ```

1. 撤回我们`sqlcmd`之前检索的命令。 继续执行并运行它以尝试连接到数据库。 请确保将和`<username>` `<password>`替换为您`ADMINUSER`在上一个设备中指定的凭据。 请务必在用户名和密码周围保留单引号, 以便命令行管理程序不会错误地误解任何特殊字符。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    尝试连接时, 应会收到错误。 这是预期的原因, 因为我们不允许对数据库进行任何访问。

    ```output
    Sqlcmd: Error: Microsoft ODBC Driver 17 for SQL Server : Cannot open server 'securedb' requested by the login. Client with IP address '40.112.128.214' is not allowed to access the server.  To enable access, use the Windows Azure Management Portal or run sp_set_firewall_rule on the master database to create a firewall rule for this IP address or address range.  It may take up to five minutes for this change to take effect..
    ```

让我们授予访问权限, 以便我们可以连接。

### <a name="use-the-server-level-allow-access-to-azure-services-rule"></a>使用服务器级别的允许访问 Azure 服务规则

由于我们的 VM 具有出站 internet 访问权限, 因此我们可以使用 "**允许访问 Azure 服务**" 规则来允许从我们的虚拟机访问。

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 在顶部的 "**搜索资源、服务和文档**" 框中, 搜索您的数据库服务器名称`server<12345>`。 选择 SQL server。

1. 在 "SQL server" 面板中, 在左侧菜单的 "**安全性**" 部分, 选择 "**防火墙和虚拟网络**"。

1. 将 "**允许访问 Azure 服务**" 设置为 **"打开"** , 然后单击 "**保存**"。

1. 回到 SSH 会话中, 让我们再次尝试连接到您的数据库。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    此时, 您应能够连接。 如果成功, 您应该会看到 sqlcmd 提示。

    ```sql
    1>
    ```

因此, 我们打开了连接, 但此设置当前允许从_任何_Azure 资源 (包括我们的订阅之外的资源) 访问。 让我们进一步限制此限制, 将网络访问限制为仅限控制范围内的资源。

### <a name="use-a-database-level-ip-address-rule"></a>使用数据库级别的 IP 地址规则

回想一下, 数据库级别的 IP 地址规则仅允许对逻辑服务器上的单个数据库的访问。 我们将在此处使用一个, 以向我们的_appServer_ VM 的静态 IP 授予访问权限。

若要创建数据库级 IP 规则, 我们需要运行一些 t-sql 命令。 您将使用以下约定创建数据库规则, 在该规则中传递规则名称、起始 ip 地址和结束 ip 地址。 通过将起始和结束 IP 指定为相同, 我们将限制对单个 ip 的访问, 但如果我们有更大的地址块需要访问, 我们可以扩展该范围。

```sql
EXECUTE sp_set_database_firewall_rule N'My Firewall Rule', '40.112.128.214', '40.112.128.214'
```

1. 仍在 sqlcmd 提示符处, 运行以下命令, 在下面的两个位置替换您的_appServer_ VM 的公共 IP 地址。

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Allow appServer database level rule', '<From IP Address>', '<To IP Address>';
    GO
    ```

    命令完成后, 键入`exit` exit sqlcmd。 通过 SSH 保持连接。

1. 在门户中, 在您的 SQL server 的 "**防火墙和虚拟网络**" 面板上, 将 "**允许访问 Azure 服务**" 设置为 "**关闭**", 然后单击 "**保存**"。 这将禁用来自所有 Azure 服务的访问, 但我们仍可以连接, 因为我们为我们的服务器提供了数据库级 IP 规则。

1. 在云命令行管理程序中, 在通过 SSH 连接到的 VM 中, 尝试再次连接到数据库。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    此时, 您应能够连接。 如果成功, 您应该会看到 sqlcmd 提示。

    ```sql
    1>
    ```

通过使用数据库级别的规则, 可以将访问特定于数据库进行隔离。 如果你想要为每个数据库配置网络访问, 这会非常有用。 如果多个数据库具有相同级别的网络访问权限, 则可以使用服务器级别的规则对服务器上的所有数据库应用相同的访问权限, 从而简化管理。

#### <a name="use-a-server-level-ip-address-rule"></a>使用服务器级别的 IP 地址规则

数据库级规则是一个很好的选择, 但如果我们在_appServer_ VM 需要连接到的同一台服务器上有多个数据库, 该怎么办？ 我们可以向每个数据库添加数据库级别的规则, 这会在我们添加更多数据库时执行更多的工作。 它会降低管理工作, 以允许访问服务器级别的规则, 这些规则将应用于服务器上的所有数据库。

现在, 我们使用服务器级别的 IP 规则来限制可以连接的系统。

1. 仍在 sqlcmd 提示符处, 运行以下命令以删除数据库级别的 IP 地址规则。

    ```sql
    EXECUTE sp_delete_database_firewall_rule N'Allow appServer database level rule';
    GO
    ```

    命令完成后, 键入`exit` exit sqlcmd。 通过 SSH 保持连接。

1. 返回到门户, 在您的 SQL server 的 "**防火墙和虚拟网络**" 面板中, 添加一个新规则, 其中包含**规则名称**"**允许 appServer** ", 并将 "**起始 ip** " 和 "**结束 ip** " 设置为 "appServer" 的公用 IP 地址。 __ VM。

    单击 "**保存**"

    ![显示已添加的带有所述 IP 限制配置的服务器防火墙规则创建的 Azure 门户屏幕截图。](../media/2-ip-address-rule.png)

1. 在云命令行管理程序中的_appServer_虚拟机上, 尝试再次连接到数据库。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    此时, 您应该能够进行连接, 因为服务器级别规则允许基于_appServer_ VM 的公共 IP 地址进行访问。 如果成功, 您应该会看到 sqlcmd 提示。

    ```sql
    1>
    ```

    要`exit`退出 sqlcmd 的类型。 通过 SSH 保持连接。

因此, 我们已将连接隔离到在规则中指定的 IP 地址。 这非常有用, 但在添加需要连接的更多系统时仍可能会遇到管理难题。 它还需要来自定义的 ip 地址范围的静态 ip 或 ip。如果 IP 是动态的且发生了更改, 则必须更新规则以确保连接。 _appServer_ VM 当前已配置了动态 IP 地址, 因此此 IP 地址可能在某个时刻发生变化, 并在出现这种情况时中断我们的访问。 现在, 我们来看看虚拟网络规则在我们的配置中是如何有益的。

#### <a name="use-a-server-level-virtual-network-rule"></a>使用服务器级别的虚拟网络规则

在这种情况下, 由于我们的 VM 在 Azure 中运行, 因此我们可以使用服务器级别的虚拟网络规则来隔离访问权限, 并使将来的服务能够轻松地获取对数据库的访问权限。

1. 在 "**虚拟网络**" 部分的 "门户" 和 "仍在**防火墙和虚拟网络**" 面板中, 单击 " **+ 添加现有虚拟网络**" 选项。

1. 将显示 "创建/更新虚拟网络规则" 对话框。 设置以下值:

    | _設定_                        | _値_                                  |
    | -------------------------------- | ---------------------------------------- |
    | **名称**                         | 保留默认值                  |
    | **订购**                 | Concierge 订阅                   |
    | **虚拟网络**              | appServerVNET                            |
    | **子网名称/地址前缀** | appServerSubnet/10.0.0.0/24            |

    单击 "**启用**" 以启用子网上的服务终结点, 然后在启用终结点以创建规则后单击 **"确定"** 。

1. 现在, 让我们删除 IP 地址规则。 单击 "**允许 appServer** " 规则旁边的 " **...** ", 然后单击 "**删除**", 然后单击 "**保存**"。

1. 在云命令行管理程序中的_appServer_虚拟机上, 尝试再次连接到数据库。

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    此时, 您应能够连接。 如果成功, 您应该会看到 sqlcmd 提示。

    ```sql
    1>
    ```

我们在此处执行的操作将有效地删除对 SQL server 的任何公开访问, 并且仅允许来自我们定义的 Azure VNet 中的特定子网的访问权限。 如果要在该子网中添加其他应用程序服务器, 则不需要进行其他配置, 因为该子网中的任何服务器都将能够连接到 SQL server。 这将限制我们对控制范围之外的服务的暴露, 并在我们添加其他服务器时简化管理。 这是保护对 Azure SQL 数据库的网络访问的有效方法。