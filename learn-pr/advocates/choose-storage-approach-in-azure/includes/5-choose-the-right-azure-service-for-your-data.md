选择正确的存储解决方案可带来更好的性能、成本节约和改进的可管理性。 在这里, 你将应用你在在线零售方案中了解的数据, 并为每个数据集查找最佳的 Azure 服务。 

## <a name="product-catalog-data"></a>产品目录数据

**数据分类:** 由于需要为新产品扩展或修改架构而进行半结构化

**运算**

- 客户需要大量的读取操作, 并且能够在数据库中的多个字段上进行查询。
- 业务需要大量的写入操作来跟踪不断变化的清单。

**延迟 & 吞吐量:** 高吞吐量和低延迟

**事务性支持:** 必填

### <a name="recommended-service-azure-cosmos-db"></a>推荐的服务: Azure Cosmos DB

Azure Cosmos DB 支持半结构化数据或受设计的 NoSQL 数据。 因此, 支持新字段 (如 "启用了 Bluetooth 的" 字段或将来需要的任何新字段) 是 Azure Cosmos DB 的提供。

Azure Cosmos DB 支持查询的 SQL, 默认情况下, 每个属性都编制索引。 您可以创建查询, 以便客户可以对目录中的任何属性进行筛选。

Azure Cosmos DB 也是符合 ACID 的, 因此您可以确信您的事务是按照这些严格要求完成的。

作为附加的 plus, 使用 Azure Cosmos DB 还可以在单击按钮的情况下将数据复制到世界上任何位置。 因此, 如果您的电子商务网站在美国、法国和英国集中了用户, 则可以将您的数据复制到这些数据中心, 以减少延迟, 因为您已将数据移动到距离较近的用户。 

即使在世界各地复制数据, 你也可以从五个一致性级别中选择一个。 通过选择正确的一致性级别, 可以确定在一致性、可用性、延迟和吞吐量之间做出的权衡。 您可以进行扩展以在高峰期内满足更高的客户需求, 或在较慢的时间内向下扩展以节省成本。

### <a name="why-not-other-azure-services"></a>为什么不是其他 Azure 服务？

Azure SQL 数据库是此数据集的理想选择, 不是为了让新产品的临时架构扩展。 在 Azure SQL 数据库中, 所有数据都需要遵循架构。 azure SQL 数据库可以提供 azure Cosmos DB 的许多相同优点, 但不能处理异类数据。 

其他 azure 服务 (如 azure 表存储、azure HBase 作为 HDInsight 的一部分) 和适用于 Redis 的 azure 缓存也可以存储 NoSQL 数据。 在这种情况下, 用户将需要查询多个字段, 因此 Azure Cosmos DB 更合适。 默认情况下, Azure Cosmos DB 会为每个字段编制索引, 而其他服务则在其索引的数据中受到限制, 而对未编制索引的字段进行查询将导致性能下降。

## <a name="photos-and-videos"></a>照片和视频

**数据分类:** 化

**运算**

- 仅需要按 ID 检索。
- 客户需要大量具有低延迟的读取操作。
- 创建和更新将稍有不同, 并且延迟可能会高于读取操作。

**延迟 & 吞吐量:** 按 ID 检索需要支持低延迟和高吞吐量。 创建和更新的延迟可能比读取操作的延迟更长。

**事务性支持:** 不需要

### <a name="recommended-service-azure-blob-storage"></a>推荐的服务: Azure Blob 存储

Azure Blob 存储支持存储照片和视频等文件。 它还通过缓存最常用的内容并将其存储在边缘服务器上来处理 Azure 内容传送网络 (CDN)。 Azure CDN 降低了为用户提供这些图像的延迟。

通过使用 Azure Blob 存储, 您还可以将图像从热存储层移动到酷或存档存储层, 以降低成本并重点提高最频繁查看的图像和视频的吞吐量。

### <a name="why-not-other-azure-services"></a>为什么不是其他 Azure 服务？

你可以将图像上传到 Azure 应用服务, 以便运行你的应用程序的同一台服务器正在为你的映像提供服务。 如果你没有很多文件, 此解决方案将正常运行。 但是, 如果你有大量文件和全局访问群体, 你将通过使用 azure Blob 存储和 azure CDN 获得更具性能的结果。

## <a name="business-data"></a>业务数据

**数据分类:** 方式

**操作:** 跨多个数据库的只读、复杂的分析查询

**延迟 & 吞吐量:** 结果中的某些延迟根据查询的复杂性质而预计。

**事务性支持:** 必填

### <a name="recommended-service-azure-sql-database"></a>推荐的服务: Azure SQL 数据库

业务分析人员最有可能会查询业务数据, 而不太可能知道 SQL 其他任何查询语言。 azure SQL 数据库本身可用作解决方案, 但将其与 Azure Analysis Services 配对使数据分析师能够创建 SQL 数据库中的数据的语义模型。 然后, 数据分析师可以与业务用户共享它, 以便他们只需从任何商业智能 (BI) 工具连接到模型即可立即浏览数据并获得见解。 

### <a name="why-not-other-azure-services"></a>为什么不是其他 Azure 服务？

Azure SQL 数据仓库支持 OLAP 解决方案和 SQL 查询。 但您的业务分析师将需要执行跨数据库查询, 而 SQL 数据仓库不支持这些查询。

除了 azure SQL Database 之外, 还可以使用 azure Analysis Services。 但在 SQL 中, 您的业务分析师比使用 Power BI 更精通。 因此, 他们需要一个支持 SQL 查询的数据库, 而 Azure Analysis Services 不会这样。 此外, 您在业务数据集中存储的财务数据在本质上是关系和多维的。 Azure Analysis Services 支持存储在服务本身 (但不是多维数据) 上的表格数据。 若要使用 Azure Analysis Services 分析多维数据, 可以使用 SQL 数据库的直接查询。

Azure Stream Analytics 是分析数据并将其转换为可操作的见解的一种极好的方法, 但其重点是流入的实时数据。 在这种情况下, 业务分析师仅查看历史数据。

## <a name="summary"></a>摘要

每种类型的数据都有不同的存储要求, 而您的工作就是要确定哪个解决方案是最佳的。 始终考虑数据类型、所需的操作、预期的延迟和事务性支持的需求。