假设您当前正在使用灵活的数据类型和地理空间支持的本地 PostgreSQL 关系数据库。 您的公司正在寻找扩展, 这需要数据库进行扩展。 作为额外硬件投资的替代方案, 您需要找到最佳的云托管数据库服务。 您已决定对 PostgreSQL 服务器使用 Azure 数据库。

## <a name="what-is-an-azure-database-for-postgresql-server"></a>什么是 PostgreSQL 服务器的 Azure 数据库？

PostgreSQL 服务器是一个或多个数据库的中心管理点。 Azure 中的 PostgreSQL 服务是一种可提供性能保证的托管资源, 它提供了服务器级别的访问和功能。

PostgreSQL server 的**Azure 数据库**是数据库的父_资源_。 _资源_是通过 Azure 提供的可管理项。 通过创建此资源, 您可以配置服务器实例。

### <a name="what-is-an-azure-database-for-postgresql-server-resource"></a>什么是 PostgreSQL 服务器资源的 Azure 数据库？

PostgreSQL server 资源的 Azure 数据库是对服务器和数据库具有极高生存期影响的容器。 如果删除了服务器资源, 则还会删除所有数据库。 请注意, 属于父代的所有资源都托管在同一个区域中。

服务器资源名称用于定义服务器终结点名称。 例如, 如果资源名称为**mypgsqlserver**, 则服务器名称将变为**mypgsqlserver.postgres.database.azure.com**。

服务器资源还为应用到其数据库的管理策略提供__连接作用域__。 例如: 登录、防火墙、用户、角色和配置。

就像 PostgreSQL 的开放源代码版本一样, 服务器可在多个版本中使用, 并允许安装扩展。 你将选择要安装的服务器版本。

> [!NOTE]
> 扩展允许将多个 SQL 对象捆绑在一起, 在可以使用单个命令加载或删除的单个包中。 扩展的一个示例是`chkpass`, 它提供自动加密密码的数据类型。

## <a name="pricing-tiers"></a>定价层

PostgreSQL 的 Azure 数据库提供了根据参数 (如计算功率和存储) 选择定价层的选项。 有关更多详细信息, 请参阅[Azure Database for PostgreSQL 定价层](https://docs.microsoft.com/azure/postgresql/concepts-pricing-tiers?azure-portal=true)。

## <a name="steps-to-create-an-azure-database-for-postgresql-server"></a>为 PostgreSQL 服务器创建 Azure 数据库的步骤

通常, 您将使用 azure 门户为 PostgreSQL 服务器创建 azure 数据库。 我们来看看您需要执行的步骤。 这不是一个练习, 但如果选择使用 Azure 门户, 则可以熟悉这些步骤。

首先, 你将登录到 Azure 门户, 然后单击 "**创建资源**"。

您将选择 PostgreSQL 的**数据库**和**Azure 数据库**。 您还可以使用**搜索**功能查找此类别。

门户将显示 "PostgreSQL 服务器配置" 屏幕 (也称为 "边栏"), 并进行选择。

您需要为刀片中的所有项目提供值, 因此, 让我们看一下每个项目。

### <a name="server-name"></a>服务器名称

之前我们提到过, 您将创建服务器资源。 服务器名称是指定该资源的项。 因此, 您必须为服务器选择唯一的名称。 服务器名称必须全部为小写字母, 并且可以包含数字和连字符。

假设您要为服务器_艾德公司的工作跟踪_命名。 然后, 将 "名称" 设置为`adventure-works-tracking`。 如果尝试使用已经存在的名称创建服务器, 则会对此产生错误。

### <a name="subscription"></a>订购

"订阅" 字段用于帐单。 如果你有多个订阅, 你将选择特定订阅。

### <a name="resource-group"></a>资源组

您将使用资源组来管理与服务器相关的所有资源。 您可以创建新的资源组或重用现有的资源组。

### <a name="source"></a>源

您可以通过选择_空白_默认选项或现有备份来从头开始创建服务器。 **备份**选项将为您提供恢复 PostgreSQL 服务器现有 Azure 数据库的地域备份的机会。

### <a name="server-admin-login-name"></a>服务器管理员登录名

创建服务器管理员用户。 选择要用作新服务器的管理员登录名的登录名。 管理员登录名不能为 azure_superuser、azure_pg_admin、admin、administrator、root、guest 或 public。 它不能以 pg_ 开头。 请记住或记下此名称以供将来使用。

### <a name="password"></a>Password

选择与上述管理员登录名一起使用的密码。 您的密码必须包含以下三种类别中的字符:

- 英文大写字母
- 英文小写字母
- 数字 (0 到 9)
- 非字母数字字符 (!、$、#、% 等)

请记住或记下此密码以供将来使用。

### <a name="confirm-password"></a>确认密码

重新键入密码进行确认。

### <a name="location"></a>位置

"位置" 选项允许您指定在物理上创建服务器的位置。 选择离你最近的地理位置。 在实际方案中, 该位置应是最接近用户大部分的位置。

### <a name="version"></a>Version

您可以指定要使用的 PostgreSQL 版本。 Microsoft 旨在支持当前版本和两个早期版本的 PostgreSQL。 你将选择与你的生产环境相匹配的版本。

> [!NOTE]
> 有关详细信息, 请参阅以下资源:
> - [支持的 PostgreSQL 数据库版本](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions?azure-portal=true)
> - [版本控制策略](https://www.postgresql.org/support/versioning/?azure-portal=true)

### <a name="pricing-tier"></a>定价层

你将选择支持你的服务器工作负载的定价层。 请记住, 您有不同的层可供选择。 如前文所述, 这些层中的每一层都允许您配置计算和存储选项。 

现在, 剩下的只是查看您输入的值, 以后您可能需要的任何说明, 然后单击 "**创建**" 以创建服务器。

部署服务器需要几分钟时间。 部署完成后, 你将收到通知。 从通知中, 您可以导航到新创建的服务器。

