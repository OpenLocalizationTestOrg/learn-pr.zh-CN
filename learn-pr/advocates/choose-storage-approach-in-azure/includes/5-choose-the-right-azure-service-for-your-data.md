<span data-ttu-id="e4764-101">选择正确的存储解决方案可带来更好的性能、成本节约和改进的可管理性。</span><span class="sxs-lookup"><span data-stu-id="e4764-101">Choosing the correct storage solution can lead to better performance, cost savings, and improved manageability.</span></span> <span data-ttu-id="e4764-102">在这里, 你将应用你在在线零售方案中了解的数据, 并为每个数据集查找最佳的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="e4764-102">Here, you'll apply what you've learned about the data in your online retail scenario, and find the best Azure service for each data set.</span></span> 

## <a name="product-catalog-data"></a><span data-ttu-id="e4764-103">产品目录数据</span><span class="sxs-lookup"><span data-stu-id="e4764-103">Product catalog data</span></span>

<span data-ttu-id="e4764-104">**数据分类:** 由于需要为新产品扩展或修改架构而进行半结构化</span><span class="sxs-lookup"><span data-stu-id="e4764-104">**Data classification:** Semi-structured because of the need to extend or modify the schema for new products</span></span>

<span data-ttu-id="e4764-105">**运算**</span><span class="sxs-lookup"><span data-stu-id="e4764-105">**Operations:**</span></span>

- <span data-ttu-id="e4764-106">客户需要大量的读取操作, 并且能够在数据库中的多个字段上进行查询。</span><span class="sxs-lookup"><span data-stu-id="e4764-106">Customers require a high number of read operations, with the ability to query on many fields within the database.</span></span>
- <span data-ttu-id="e4764-107">业务需要大量的写入操作来跟踪不断变化的清单。</span><span class="sxs-lookup"><span data-stu-id="e4764-107">The business requires a high number of write operations to track the constantly changing inventory.</span></span>

<span data-ttu-id="e4764-108">**延迟 & 吞吐量:** 高吞吐量和低延迟</span><span class="sxs-lookup"><span data-stu-id="e4764-108">**Latency & throughput:** High throughput and low latency</span></span>

<span data-ttu-id="e4764-109">**事务性支持:** 必填</span><span class="sxs-lookup"><span data-stu-id="e4764-109">**Transactional support:** Required</span></span>

### <a name="recommended-service-azure-cosmos-db"></a><span data-ttu-id="e4764-110">推荐的服务: Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4764-110">Recommended service: Azure Cosmos DB</span></span>

<span data-ttu-id="e4764-111">Azure Cosmos DB 支持半结构化数据或受设计的 NoSQL 数据。</span><span class="sxs-lookup"><span data-stu-id="e4764-111">Azure Cosmos DB supports semi-structured data, or NoSQL data, by design.</span></span> <span data-ttu-id="e4764-112">因此, 支持新字段 (如 "启用了 Bluetooth 的" 字段或将来需要的任何新字段) 是 Azure Cosmos DB 的提供。</span><span class="sxs-lookup"><span data-stu-id="e4764-112">So, supporting new fields, such as the "Bluetooth-enabled" field or any new fields you need in the future, is a given with Azure Cosmos DB.</span></span>

<span data-ttu-id="e4764-113">Azure Cosmos DB 支持查询的 SQL, 默认情况下, 每个属性都编制索引。</span><span class="sxs-lookup"><span data-stu-id="e4764-113">Azure Cosmos DB supports SQL for queries and every property is indexed by default.</span></span> <span data-ttu-id="e4764-114">您可以创建查询, 以便客户可以对目录中的任何属性进行筛选。</span><span class="sxs-lookup"><span data-stu-id="e4764-114">You can create queries so that your customers can filter on any property in the catalog.</span></span>

<span data-ttu-id="e4764-115">Azure Cosmos DB 也是符合 ACID 的, 因此您可以确信您的事务是按照这些严格要求完成的。</span><span class="sxs-lookup"><span data-stu-id="e4764-115">Azure Cosmos DB is also ACID-compliant, so you can be assured that your transactions are completed according to those strict requirements.</span></span>

<span data-ttu-id="e4764-116">作为附加的 plus, 使用 Azure Cosmos DB 还可以在单击按钮的情况下将数据复制到世界上任何位置。</span><span class="sxs-lookup"><span data-stu-id="e4764-116">As an added plus, Azure Cosmos DB also enables you to replicate your data anywhere in the world with the click of a button.</span></span> <span data-ttu-id="e4764-117">因此, 如果您的电子商务网站在美国、法国和英国集中了用户, 则可以将您的数据复制到这些数据中心, 以减少延迟, 因为您已将数据移动到距离较近的用户。</span><span class="sxs-lookup"><span data-stu-id="e4764-117">So, if your e-commerce site has users concentrated in the US, France, and England, you can replicate your data to those data centers to reduce latency, as you've physically moved the data closer to your users.</span></span> 

<span data-ttu-id="e4764-118">即使在世界各地复制数据, 你也可以从五个一致性级别中选择一个。</span><span class="sxs-lookup"><span data-stu-id="e4764-118">Even with data replicated around the world, you can choose from one of five consistency levels.</span></span> <span data-ttu-id="e4764-119">通过选择正确的一致性级别, 可以确定在一致性、可用性、延迟和吞吐量之间做出的权衡。</span><span class="sxs-lookup"><span data-stu-id="e4764-119">By choosing the right consistency level, you can determine the tradeoffs to make between consistency, availability, latency, and throughput.</span></span> <span data-ttu-id="e4764-120">您可以进行扩展以在高峰期内满足更高的客户需求, 或在较慢的时间内向下扩展以节省成本。</span><span class="sxs-lookup"><span data-stu-id="e4764-120">You can scale up to handle higher customer demand during peak shopping times, or scale down during slower times to conserve cost.</span></span>

### <a name="why-not-other-azure-services"></a><span data-ttu-id="e4764-121">为什么不是其他 Azure 服务？</span><span class="sxs-lookup"><span data-stu-id="e4764-121">Why not other Azure services?</span></span>

<span data-ttu-id="e4764-122">Azure SQL 数据库是此数据集的理想选择, 不是为了让新产品的临时架构扩展。</span><span class="sxs-lookup"><span data-stu-id="e4764-122">Azure SQL Database would be an excellent choice for this data set, were it not for the need to extend the schema ad-hoc for new products.</span></span> <span data-ttu-id="e4764-123">在 Azure SQL 数据库中, 所有数据都需要遵循架构。</span><span class="sxs-lookup"><span data-stu-id="e4764-123">In Azure SQL Database, all data needs to adhere to a schema.</span></span> <span data-ttu-id="e4764-124">azure SQL 数据库可以提供 azure Cosmos DB 的许多相同优点, 但不能处理异类数据。</span><span class="sxs-lookup"><span data-stu-id="e4764-124">Azure SQL Database can provide many of the same benefits of Azure Cosmos DB, but it cannot handle heterogeneous data.</span></span> 

<span data-ttu-id="e4764-125">其他 azure 服务 (如 azure 表存储、azure HBase 作为 HDInsight 的一部分) 和适用于 Redis 的 azure 缓存也可以存储 NoSQL 数据。</span><span class="sxs-lookup"><span data-stu-id="e4764-125">Other Azure services, such as Azure Table storage, Azure HBase as a part of HDInsight, and Azure Cache for Redis, can also store NoSQL data.</span></span> <span data-ttu-id="e4764-126">在这种情况下, 用户将需要查询多个字段, 因此 Azure Cosmos DB 更合适。</span><span class="sxs-lookup"><span data-stu-id="e4764-126">In this scenario, users will want to query on multiple fields, so Azure Cosmos DB is a better fit.</span></span> <span data-ttu-id="e4764-127">默认情况下, Azure Cosmos DB 会为每个字段编制索引, 而其他服务则在其索引的数据中受到限制, 而对未编制索引的字段进行查询将导致性能下降。</span><span class="sxs-lookup"><span data-stu-id="e4764-127">Azure Cosmos DB indexes every field by default, whereas the other services are limited in the data they index, and querying on non-indexed fields results in reduced performance.</span></span>

## <a name="photos-and-videos"></a><span data-ttu-id="e4764-128">照片和视频</span><span class="sxs-lookup"><span data-stu-id="e4764-128">Photos and videos</span></span>

<span data-ttu-id="e4764-129">**数据分类:** 化</span><span class="sxs-lookup"><span data-stu-id="e4764-129">**Data classification:** Unstructured</span></span>

<span data-ttu-id="e4764-130">**运算**</span><span class="sxs-lookup"><span data-stu-id="e4764-130">**Operations:**</span></span>

- <span data-ttu-id="e4764-131">仅需要按 ID 检索。</span><span class="sxs-lookup"><span data-stu-id="e4764-131">Only need to be retrieved by ID.</span></span>
- <span data-ttu-id="e4764-132">客户需要大量具有低延迟的读取操作。</span><span class="sxs-lookup"><span data-stu-id="e4764-132">Customers require a high number of read operations with low latency.</span></span>
- <span data-ttu-id="e4764-133">创建和更新将稍有不同, 并且延迟可能会高于读取操作。</span><span class="sxs-lookup"><span data-stu-id="e4764-133">Creates and updates will be somewhat infrequent and can have higher latency than read operations.</span></span>

<span data-ttu-id="e4764-134">**延迟 & 吞吐量:** 按 ID 检索需要支持低延迟和高吞吐量。</span><span class="sxs-lookup"><span data-stu-id="e4764-134">**Latency & throughput:** Retrievals by ID need to support low latency and high throughput.</span></span> <span data-ttu-id="e4764-135">创建和更新的延迟可能比读取操作的延迟更长。</span><span class="sxs-lookup"><span data-stu-id="e4764-135">Creates and updates can have higher latency than read operations.</span></span>

<span data-ttu-id="e4764-136">**事务性支持:** 不需要</span><span class="sxs-lookup"><span data-stu-id="e4764-136">**Transactional support:** Not required</span></span>

### <a name="recommended-service-azure-blob-storage"></a><span data-ttu-id="e4764-137">推荐的服务: Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="e4764-137">Recommended service: Azure Blob storage</span></span>

<span data-ttu-id="e4764-138">Azure Blob 存储支持存储照片和视频等文件。</span><span class="sxs-lookup"><span data-stu-id="e4764-138">Azure Blob storage supports storing files such as photos and videos.</span></span> <span data-ttu-id="e4764-139">它还通过缓存最常用的内容并将其存储在边缘服务器上来处理 Azure 内容传送网络 (CDN)。</span><span class="sxs-lookup"><span data-stu-id="e4764-139">It also works with Azure Content Delivery Network (CDN) by caching the most frequently used content and storing it on edge servers.</span></span> <span data-ttu-id="e4764-140">Azure CDN 降低了为用户提供这些图像的延迟。</span><span class="sxs-lookup"><span data-stu-id="e4764-140">Azure CDN reduces latency in serving up those images to your users.</span></span>

<span data-ttu-id="e4764-141">通过使用 Azure Blob 存储, 您还可以将图像从热存储层移动到酷或存档存储层, 以降低成本并重点提高最频繁查看的图像和视频的吞吐量。</span><span class="sxs-lookup"><span data-stu-id="e4764-141">By using Azure Blob storage, you can also move images from the hot storage tier to the cool or archive storage tier, to reduce costs and focus throughput on the most frequently viewed images and videos.</span></span>

### <a name="why-not-other-azure-services"></a><span data-ttu-id="e4764-142">为什么不是其他 Azure 服务？</span><span class="sxs-lookup"><span data-stu-id="e4764-142">Why not other Azure services?</span></span>

<span data-ttu-id="e4764-143">你可以将图像上传到 Azure 应用服务, 以便运行你的应用程序的同一台服务器正在为你的映像提供服务。</span><span class="sxs-lookup"><span data-stu-id="e4764-143">You could upload your images to Azure App Service, so that the same server that is running your app is serving up your images.</span></span> <span data-ttu-id="e4764-144">如果你没有很多文件, 此解决方案将正常运行。</span><span class="sxs-lookup"><span data-stu-id="e4764-144">This solution would work if you didn't have many files.</span></span> <span data-ttu-id="e4764-145">但是, 如果你有大量文件和全局访问群体, 你将通过使用 azure Blob 存储和 azure CDN 获得更具性能的结果。</span><span class="sxs-lookup"><span data-stu-id="e4764-145">But if you have lots of files, and a global audience, you'll get more performant results by using Azure Blob storage with Azure CDN.</span></span>

## <a name="business-data"></a><span data-ttu-id="e4764-146">业务数据</span><span class="sxs-lookup"><span data-stu-id="e4764-146">Business data</span></span>

<span data-ttu-id="e4764-147">**数据分类:** 方式</span><span class="sxs-lookup"><span data-stu-id="e4764-147">**Data classification:** Structured</span></span>

<span data-ttu-id="e4764-148">**操作:** 跨多个数据库的只读、复杂的分析查询</span><span class="sxs-lookup"><span data-stu-id="e4764-148">**Operations:** Read-only, complex analytical queries across multiple databases</span></span>

<span data-ttu-id="e4764-149">**延迟 & 吞吐量:** 结果中的某些延迟根据查询的复杂性质而预计。</span><span class="sxs-lookup"><span data-stu-id="e4764-149">**Latency & throughput:** Some latency in the results is expected based on the complex nature of the queries.</span></span>

<span data-ttu-id="e4764-150">**事务性支持:** 必填</span><span class="sxs-lookup"><span data-stu-id="e4764-150">**Transactional support:** Required</span></span>

### <a name="recommended-service-azure-sql-database"></a><span data-ttu-id="e4764-151">推荐的服务: Azure SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="e4764-151">Recommended service: Azure SQL Database</span></span>

<span data-ttu-id="e4764-152">业务分析人员最有可能会查询业务数据, 而不太可能知道 SQL 其他任何查询语言。</span><span class="sxs-lookup"><span data-stu-id="e4764-152">Business data will most likely be queried by business analysts, who are more likely to know SQL than any other query language.</span></span> <span data-ttu-id="e4764-153">azure SQL 数据库本身可用作解决方案, 但将其与 Azure Analysis Services 配对使数据分析师能够创建 SQL 数据库中的数据的语义模型。</span><span class="sxs-lookup"><span data-stu-id="e4764-153">Azure SQL Database could be used as the solution by itself, but pairing it with Azure Analysis Services enables data analysts to create a semantic model over the data in SQL Database.</span></span> <span data-ttu-id="e4764-154">然后, 数据分析师可以与业务用户共享它, 以便他们只需从任何商业智能 (BI) 工具连接到模型即可立即浏览数据并获得见解。</span><span class="sxs-lookup"><span data-stu-id="e4764-154">The data analysts can then share it with business users, so that they only need to connect to the model from any business intelligence (BI) tool to immediately explore the data and gain insights.</span></span> 

### <a name="why-not-other-azure-services"></a><span data-ttu-id="e4764-155">为什么不是其他 Azure 服务？</span><span class="sxs-lookup"><span data-stu-id="e4764-155">Why not other Azure services?</span></span>

<span data-ttu-id="e4764-156">Azure SQL 数据仓库支持 OLAP 解决方案和 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="e4764-156">Azure SQL Data Warehouse supports OLAP solutions and SQL queries.</span></span> <span data-ttu-id="e4764-157">但您的业务分析师将需要执行跨数据库查询, 而 SQL 数据仓库不支持这些查询。</span><span class="sxs-lookup"><span data-stu-id="e4764-157">But your business analysts will need to perform cross-database queries, which SQL Data Warehouse does not support.</span></span>

<span data-ttu-id="e4764-158">除了 azure SQL Database 之外, 还可以使用 azure Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="e4764-158">Azure Analysis Services could be used in addition to Azure SQL Database.</span></span> <span data-ttu-id="e4764-159">但在 SQL 中, 您的业务分析师比使用 Power BI 更精通。</span><span class="sxs-lookup"><span data-stu-id="e4764-159">But your business analysts are more well-versed in SQL than in working with Power BI.</span></span> <span data-ttu-id="e4764-160">因此, 他们需要一个支持 SQL 查询的数据库, 而 Azure Analysis Services 不会这样。</span><span class="sxs-lookup"><span data-stu-id="e4764-160">So they'd like a database that supports SQL queries, which Azure Analysis Services does not.</span></span> <span data-ttu-id="e4764-161">此外, 您在业务数据集中存储的财务数据在本质上是关系和多维的。</span><span class="sxs-lookup"><span data-stu-id="e4764-161">In addition, the financial data you're storing in your business data set is relational and multidimensional in nature.</span></span> <span data-ttu-id="e4764-162">Azure Analysis Services 支持存储在服务本身 (但不是多维数据) 上的表格数据。</span><span class="sxs-lookup"><span data-stu-id="e4764-162">Azure Analysis Services supports tabular data stored on the service itself, but not multidimensional data.</span></span> <span data-ttu-id="e4764-163">若要使用 Azure Analysis Services 分析多维数据, 可以使用 SQL 数据库的直接查询。</span><span class="sxs-lookup"><span data-stu-id="e4764-163">To analyze multidimensional data with Azure Analysis Services, you can use a direct query to the SQL Database.</span></span>

<span data-ttu-id="e4764-164">Azure Stream Analytics 是分析数据并将其转换为可操作的见解的一种极好的方法, 但其重点是流入的实时数据。</span><span class="sxs-lookup"><span data-stu-id="e4764-164">Azure Stream Analytics is a great way to analyze data and transform it into actionable insights, but its focus is on real-time data that is streaming in.</span></span> <span data-ttu-id="e4764-165">在这种情况下, 业务分析师仅查看历史数据。</span><span class="sxs-lookup"><span data-stu-id="e4764-165">In this scenario, the business analysts are looking at historical data only.</span></span>

## <a name="summary"></a><span data-ttu-id="e4764-166">摘要</span><span class="sxs-lookup"><span data-stu-id="e4764-166">Summary</span></span>

<span data-ttu-id="e4764-167">每种类型的数据都有不同的存储要求, 而您的工作就是要确定哪个解决方案是最佳的。</span><span class="sxs-lookup"><span data-stu-id="e4764-167">Each type of data has different storage requirements, and it's your job to figure out which solution is best.</span></span> <span data-ttu-id="e4764-168">始终考虑数据类型、所需的操作、预期的延迟和事务性支持的需求。</span><span class="sxs-lookup"><span data-stu-id="e4764-168">Always consider the type of data, the operations required, expected latency, and the need for transactional support.</span></span>