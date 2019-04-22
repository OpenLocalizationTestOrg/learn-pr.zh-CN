现在, 你的 Azure SQL 数据库已启动并在运行, 你可以将其连接到你最喜欢的 SQL Server 管理工具, 以使用实际数据填充它。

最初考虑是在本地还是在云中运行数据库。 使用 Azure SQL database, 可以配置几个基本选项, 并且您拥有一个可连接到应用程序的功能齐全的 SQL 数据库。

没有要维护的基础结构或软件修补程序。 现在, 你可以自由地重点了解如何在启动和运行的运输物流应用原型上, 并在数据库管理上执行更少的工作。 您的原型也不会成为 "扔掉" 演示。 Azure SQL Database 提供了生产级的安全性和性能功能。

请记住, 每个 Azure SQL 逻辑服务器包含一个或多个数据库。 Azure SQL Database 提供了两种定价模型, 即 DTU 和 vCore, 可帮助您跨所有数据库平衡成本与性能。

如果只是开始使用, 或者需要一个简单的预配置的购买选项, 请选择 "DTU"。 如果您希望更好地控制您为其创建和支付的计算和存储资源, 请选择 "vCore"。

使用 Azure 云命令行管理程序, 可以轻松地开始使用数据库。 从云命令行管理程序中, 您可以访问 azure CLI, 这使您可以获取有关 azure 资源的信息。 云命令行管理程序还提供了许多其他常见`sqlcmd`的实用程序, 例如, 可帮助您立即开始使用新数据库。

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>其他资源

该文档提供了更多的信息, 包括教程和示例。 下面是一些指向我们介绍的内容的链接:

- [Azure SQL 数据库文档](https://docs.microsoft.com/azure/sql-database/)
- [Azure SQL 数据库购买模型和资源](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)
- [Azure SQL 数据库逻辑服务器及其管理](https://docs.microsoft.com/azure/sql-database/sql-database-logical-servers)
- [Azure SQL 数据库和 SQL 数据仓库防火墙规则](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)

若要了解云命令行管理程序的详细信息, 请参阅[Azure 云命令行](https://docs.microsoft.com/azure/cloud-shell/overview)管理程序概述。

如果你有兴趣了解有关该实用工具的`sqlcmd`详细信息, 请参阅[sqlcmd 实用工具](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-2017)。
