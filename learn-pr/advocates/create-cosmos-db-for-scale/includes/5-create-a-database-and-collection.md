<span data-ttu-id="e1d22-101">现在, 您已经了解了如何使用请求单元来确定数据库吞吐量, 以及分区键如何为数据库创建扩展策略, 您已准备好创建数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="e1d22-101">Now that you understand how request units are used to determine database throughput, and how the partition key creates the scale-out strategy for your database, you're ready to create your database and collection.</span></span> <span data-ttu-id="e1d22-102">您将在创建集合时设置分区键和吞吐量值, 因此, 建议您在创建数据库之前了解这些概念。</span><span class="sxs-lookup"><span data-stu-id="e1d22-102">You'll set your partition key and throughput values when you create your collection, so it's recommended that you understand those concepts before you create a database.</span></span>

## <a name="creating-your-database-and-collection"></a><span data-ttu-id="e1d22-103">创建数据库和集合</span><span class="sxs-lookup"><span data-stu-id="e1d22-103">Creating your database and collection</span></span>

1. <span data-ttu-id="e1d22-104">在 Azure 门户中, 从 Cosmos DB 资源中选择 "**数据资源管理器**", 然后单击工具栏中的 "**新建集合**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="e1d22-104">In the Azure portal, select **Data Explorer** from your Cosmos DB resource and then click the **New Collection** button in the toolbar.</span></span>
    
    <span data-ttu-id="e1d22-105">"**添加集合**" 区域显示在最右侧。</span><span class="sxs-lookup"><span data-stu-id="e1d22-105">The **Add Collection** area is displayed on the far right.</span></span> <span data-ttu-id="e1d22-106">您可能需要向右滚动才能看到它。</span><span class="sxs-lookup"><span data-stu-id="e1d22-106">You may need to scroll right to see it.</span></span>

    ![Azure 门户数据浏览器, 添加集合边栏](../media/5-azure-cosmosdb-data-explorer.png)

1. <span data-ttu-id="e1d22-108">在 "**添加集合**" 页中, 输入新集合的设置。</span><span class="sxs-lookup"><span data-stu-id="e1d22-108">In the **Add collection** page, enter the settings for the new collection.</span></span>

    <span data-ttu-id="e1d22-109">设置</span><span class="sxs-lookup"><span data-stu-id="e1d22-109">Setting</span></span> | <span data-ttu-id="e1d22-110">建议值</span><span class="sxs-lookup"><span data-stu-id="e1d22-110">Suggested value</span></span> | <span data-ttu-id="e1d22-111">说明</span><span class="sxs-lookup"><span data-stu-id="e1d22-111">Description</span></span>
    --------|-----------------|-------------
    <span data-ttu-id="e1d22-112">数据库 id</span><span class="sxs-lookup"><span data-stu-id="e1d22-112">Database id</span></span>    | <span data-ttu-id="e1d22-113">物料</span><span class="sxs-lookup"><span data-stu-id="e1d22-113">Products</span></span>   | <span data-ttu-id="e1d22-114">输入 "*产品*" 作为新数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="e1d22-114">Enter *Products* as the name for the new database.</span></span> <span data-ttu-id="e1d22-115">数据库名称的长度必须为1到255个字符, 并且不得包含/、 \\、#、? 或尾部空格。</span><span class="sxs-lookup"><span data-stu-id="e1d22-115">Database names must be 1 to 255 characters in length, and must not contain /, \\, #, ?, or a trailing space.</span></span>
    <span data-ttu-id="e1d22-116">集合 id</span><span class="sxs-lookup"><span data-stu-id="e1d22-116">Collection id</span></span>  | <span data-ttu-id="e1d22-117">衣物</span><span class="sxs-lookup"><span data-stu-id="e1d22-117">Clothing</span></span>   | <span data-ttu-id="e1d22-118">输入*衣服*作为新收藏的名称。</span><span class="sxs-lookup"><span data-stu-id="e1d22-118">Enter *Clothing* as the name for your new collection.</span></span> <span data-ttu-id="e1d22-119">集合 id 与数据库名称具有相同的字符要求。</span><span class="sxs-lookup"><span data-stu-id="e1d22-119">Collection ids have the same character requirements as database names.</span></span>
    <span data-ttu-id="e1d22-120">分区键</span><span class="sxs-lookup"><span data-stu-id="e1d22-120">Partition key</span></span>  | <span data-ttu-id="e1d22-121">id</span><span class="sxs-lookup"><span data-stu-id="e1d22-121">productId</span></span>  | <span data-ttu-id="e1d22-122">productId 是在线零售方案的一个很棒的分区键, 因为这很多查询都基于产品 ID。</span><span class="sxs-lookup"><span data-stu-id="e1d22-122">productId is a good partition key for an online retail scenario, as so many queries are based around the product ID.</span></span>
    <span data-ttu-id="e1d22-123">提高</span><span class="sxs-lookup"><span data-stu-id="e1d22-123">Throughput</span></span>     | <span data-ttu-id="e1d22-124">1000 RU</span><span class="sxs-lookup"><span data-stu-id="e1d22-124">1000 RU</span></span>    | <span data-ttu-id="e1d22-125">将吞吐量更改为每秒1000个请求单元 (RU/秒)。</span><span class="sxs-lookup"><span data-stu-id="e1d22-125">Change the throughput to 1000 request units per second (RU/s).</span></span> <span data-ttu-id="e1d22-126">1000是可设置为启用自动缩放的最小 RU/秒值。</span><span class="sxs-lookup"><span data-stu-id="e1d22-126">1000 is the minimum RU/s value you can set to enable automatic scaling.</span></span>
    
    <span data-ttu-id="e1d22-127">目前, 请勿检查 "**设置数据库吞吐量**" 选项, 也不要将任何唯一键添加到集合中。</span><span class="sxs-lookup"><span data-stu-id="e1d22-127">For now, don't check the **Provision database throughput** option, and don't add any unique keys to the collection.</span></span>
    
1. <span data-ttu-id="e1d22-128">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="e1d22-128">Click **OK**.</span></span> <span data-ttu-id="e1d22-129">数据资源管理器显示新的数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="e1d22-129">The Data Explorer displays the new database and collection.</span></span>

    ![显示新数据库和集合的 Azure 门户数据浏览器](../media/5-azure-cosmos-db-new-collection.png)

## <a name="summary"></a><span data-ttu-id="e1d22-131">摘要</span><span class="sxs-lookup"><span data-stu-id="e1d22-131">Summary</span></span>

<span data-ttu-id="e1d22-132">在此单元中, 你使用了分区密钥和请求单元的知识, 以创建符合你的业务需求的吞吐量和扩展设置的数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="e1d22-132">In this unit, you used your knowledge of partition keys and request units to create a database and collection with throughput and scaling settings appropriate for your business needs.</span></span>