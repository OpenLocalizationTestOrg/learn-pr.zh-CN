假设你使用的是本地 PostgreSQL 数据库。 您正在管理所有安全方面, 并且已通过标准 PostgreSQL 服务器级别的防火墙规则锁定了对您的服务器的所有访问。 现在, 您需要确保您可以在 Azure 中配置相同的服务器级别防火墙规则。

## <a name="server-security-considerations-and-connection-methods"></a>服务器安全注意事项和连接方法

您可以使用多种方法来限制对 PostgreSQL 服务器和数据库的 Azure 数据库的访问。 可以在网络、服务器或数据库级别限制网络访问。 您可以使用以下任一选项:

- 限制数据库访问的用户帐户
- 用于限制网络访问的虚拟网络
- 限制服务器访问的防火墙规则

### <a name="authentication-and-authorization"></a>身份验证和授权

适用于 PostgreSQL 服务器的 Azure 数据库支持本机 PostgreSQL 身份验证。 您可以通过服务器的管理员登录与服务器进行连接和身份验证。 您还将创建用户以连接到特定数据库来限制访问。

### <a name="what-is-a-virtual-network"></a>什么是虚拟网络？

虚拟网络是在 Azure 网络中创建的逻辑隔离网络。 您可以使用虚拟网络控制哪些 Azure 资源可以连接到其他资源。

假设您正在运行连接到数据库的 web 应用程序。 你将使用子网隔离网络的不同部分。 子网是基于 IP 地址范围的网络的一部分。

若要配置这些子网, 您将创建一个虚拟网络, 然后将该网络细分为子网。 web 应用程序将在一个子网和另一个子网上的数据库上运行。 每个子网都有自己的规则, 用于与其他网络进行通信。 这些规则使您能够限制从数据库到 web 应用程序的访问。

### <a name="what-is-a-firewall"></a>什么是防火墙？

防火墙是一项服务, 它基于每个请求的原始 IP 地址授予服务器访问权限。 创建用于指定 IP 地址范围的防火墙规则。 仅允许来自这些已授予 IP 地址的客户端访问服务器。 通常情况下, 防火墙规则还包括特定网络协议和端口信息。 例如, 默认情况下, PostgreSQL 服务器侦听端口5432上的 TCP 请求。

### <a name="azure-database-for-postgresql-server-firewall"></a>用于 PostgreSQL 服务器防火墙的 Azure 数据库

PostgreSQL server 防火墙的 Azure 数据库将阻止对数据库服务器的所有访问, 直到您指定哪些计算机具有权限。 防火墙配置允许您指定允许连接到服务器的 IP 地址范围。 服务器始终使用默认的 PostgreSQL 连接信息。

![显示用于 PostgreSQL 服务器防火墙的 Azure 数据库扫描所有传入请求的 IP 地址的插图。 仅来自一系列预定义的有效 IP 地址的请求将被转发到数据库](../media/6-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a>用于 PostgreSQL server SSL 连接的 Azure 数据库

适用于 PostgreSQL 的 Azure 数据库首选客户端应用程序使用安全套接字层 (SSL) 连接到 PostgreSQL 服务。 在数据库服务器和客户端应用程序之间实施 SSL 连接有助于通过加密服务器和客户端之间的数据来防止 "中间人" 和类似的攻击。 启用 SSL 需要在客户端和服务器之间交换密钥和严格的身份验证, 以便连接能够正常工作。 有关使用 SSL 的详细信息不在本学习模块的范围之内。

## <a name="configure-connection-security"></a>配置连接安全性

让我们来看一下为 PostgreSQL server 防火墙配置 Azure 数据库时所做的决策和步骤。 此外, 您还将了解如何连接到之前创建的服务器。

使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。 导航到您要为其创建防火墙规则的服务器资源。

然后, 选择 "**连接安全**" 选项以打开右侧的 "连接安全" 边栏。

![显示 PostgreSQL 数据库资源边栏的 "连接安全" 部分的 Azure 门户屏幕截图](../media/6-db-security-settings.png)

在此屏幕上, 您有多个选项。 您可以：

- 通过单击 "**添加客户端 IP** " 按钮, 添加用于将门户访问为防火墙条目的 IP 地址。
- 允许访问 Azure 服务。 默认情况下, 所有 Azure 服务都**无法**访问 PostgreSQL 服务器。
- 通过输入 IP 地址的范围来添加防火墙规则。
- 强制实施 SSL 连接。 此选项将强制客户端使用 SSL 证书连接到服务器。

始终记得单击 "保存" 图标上方的 "**保存**" 图标, 以在进行更改后保存已更新的配置。

### <a name="allow-access-to-azure-services"></a>允许访问 Azure 服务

若要使用 Azure 云命令行管理程序访问或配置您的服务器, 请确保启用 "**允许访问 Azure 服务**"。 此步骤将向服务器配置添加防火墙规则, 以允许从云命令行管理程序访问。 此规则不会显示为你添加的自定义规则之一。

此外, 还需要禁用**强制 SSL 连接**。 如果客户端连接需要 SSL, PowerShell 将无法连接到服务器。

如果配置不正确, 这两个选项都将导致在命令行中显示错误消息。

例如, 如果不允许访问 Azure 服务并强制实施 SSL 连接, 则当防火墙阻止访问时, 您会看到类似于此错误的内容:

```output
psql: FATAL: no pg_hba.conf entry for host "123.45.67.89", user "adminuser", database "postgres", SSL on FATAL:  SSL connection is required. Please specify SSL options and retry.
```

### <a name="create-a-firewall-rule-using-the-portal"></a>使用门户创建防火墙规则

假设您要创建提供来自任何 IP 地址的访问权限的防火墙规则。

> [!WARNING]
> 创建此防火墙规则将允许 Internet 上的任何 IP 地址尝试连接到您的服务器。 即使客户端无法在不使用用户名和密码的情况下访问服务器, 也应谨慎启用此规则, 并确保了解安全含义。

您可以通过在标记的字段中输入以下数据来创建新的防火墙规则:

- 规则名称:`AllowAll`
- 起始 IP:`0.0.0.0`
- 结束 IP:`255.255.255.255`

若要删除防火墙规则, 请单击要删除的规则末尾的省略号 (...)。 单击 "**删除**" 按钮以删除规则。

单击 "**保存**" 图标上方的 "输入" 字段以提交规则的删除。

### <a name="create-a-firewall-rule-using-the-azure-cli"></a>使用 Azure CLI 创建防火墙规则

您可以使用 Azure CLI 将防火墙规则添加到您的服务器中的`az postgres server firewall-rule create`命令。 下面的示例将根据上面的内容创建规则。

```azurecli
az postgres server firewall-rule create \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --server <server-name> \
  --name AllowAll \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 255.255.255.255
```

使用命令`az postgres server firewall-rule delete`删除服务器中的防火墙规则。 下面是一个示例:

```azurecli
az postgres server firewall-rule delete \
  --name AllowAll \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --server-name <server-name>
```

## <a name="connecting-to-your-server"></a>连接到服务器

与任何新式数据库一样, PostgreSQL 需要进行定期服务器管理以实现最佳性能。 有许多选项可用于连接和管理 PostgreSQL 服务器的 Azure 数据库。 我们将使用`psql`连接到服务器。

### <a name="what-is-psql"></a>什么是 psql？

调用`psql`的命令行工具是用于使用 PostgreSQL 服务器和数据库的 PostgreSQL 分布式交互终端。 `psql`适用于 PostgreSQL 的 azure 数据库, 与任何其他 PostgreSQL 实现相同, 并且包含在 Azure 云命令行管理程序中。 该`psql`工具允许您管理数据库以及对这些数据库执行结构查询。

使用`psql`需要成功连接到 PostgreSQL 服务器。 使用时, 有许多命令行参数可供使用`psql`。

- `--host`-要连接到的主机。
- `--username`-连接所用的用户名/ID。
- `--dbname`-要连接到的数据库的名称。

> [!TIP]
> 在管理服务器访问和数据库`postgres`配置时, 通常会连接到管理数据库。

下面是完整的命令:

```bash
psql --host=<server-name>.postgres.database.azure.com \
  --username=<admin-user>@<server-name> \
  --dbname=<database>
```

连接后, 将显示命令提示符, 并可对服务器和数据库执行命令。

现在, 您已看到为 PostgreSQL 安全设置配置 Azure 数据库所需的步骤。 在下一个设备中, 您将为 PostgreSQL 安全设置配置 Azure 数据库。 您还将使用云命令行管理程序连接到服务器。
