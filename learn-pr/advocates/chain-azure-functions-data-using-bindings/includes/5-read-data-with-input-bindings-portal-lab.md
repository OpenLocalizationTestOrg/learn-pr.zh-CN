<span data-ttu-id="651ad-101">假设您想要创建一个简单的书签查找服务。</span><span class="sxs-lookup"><span data-stu-id="651ad-101">Imagine that you want to create a simple bookmark lookup service.</span></span> <span data-ttu-id="651ad-102">您的服务最初是只读的。</span><span class="sxs-lookup"><span data-stu-id="651ad-102">Your service is read-only initially.</span></span> <span data-ttu-id="651ad-103">如果用户想要查找条目, 则会向其发送 ID 为的请求, 并返回该 URL。</span><span class="sxs-lookup"><span data-stu-id="651ad-103">If users want to find an entry, they send a request with the ID of the entry and you return the URL.</span></span> <span data-ttu-id="651ad-104">下面的流程图对流进行了说明:</span><span class="sxs-lookup"><span data-stu-id="651ad-104">The following flowchart explains the flow:</span></span>

![显示在我们的 Cosmos DB 后端中查找书签的过程的流程图。](../media/5-find-bookmark-flow-small.png)

<span data-ttu-id="651ad-109">当用户向你发送带有一些文本的请求时, 请尝试在后端数据库中查找包含此文本的条目作为密钥或 ID。</span><span class="sxs-lookup"><span data-stu-id="651ad-109">When users send you a request with some text, you try to find an entry in your back-end database that contains this text as a key or ID.</span></span> <span data-ttu-id="651ad-110">您将返回一个结果, 指示是否找到了该条目。</span><span class="sxs-lookup"><span data-stu-id="651ad-110">You return a result that indicates whether you found the entry.</span></span>

<span data-ttu-id="651ad-111">您需要将数据存储在某个位置。</span><span class="sxs-lookup"><span data-stu-id="651ad-111">You need to store the data somewhere.</span></span> <span data-ttu-id="651ad-112">在此流程图中, 数据存储是一个 Azure Cosmos DB 实例。</span><span class="sxs-lookup"><span data-stu-id="651ad-112">In this flowchart, the data store is an Azure Cosmos DB instance.</span></span> <span data-ttu-id="651ad-113">但如何从函数连接到数据库并读取数据？</span><span class="sxs-lookup"><span data-stu-id="651ad-113">But how do you connect to a database from a function and read data?</span></span> <span data-ttu-id="651ad-114">在函数世界中, 可以为该作业配置*输入绑定*。</span><span class="sxs-lookup"><span data-stu-id="651ad-114">In the world of functions, you configure an *input binding* for that job.</span></span>  <span data-ttu-id="651ad-115">通过 Azure 门户配置绑定非常简单。</span><span class="sxs-lookup"><span data-stu-id="651ad-115">Configuring a binding through the Azure portal is straightforward.</span></span> <span data-ttu-id="651ad-116">正如您很快就会看到的, 您不必为打开存储连接这样的任务编写代码。</span><span class="sxs-lookup"><span data-stu-id="651ad-116">As you'll see shortly, you don't have to write code for such tasks as opening a storage connection.</span></span> <span data-ttu-id="651ad-117">Azure 函数运行时和绑定会为你处理这些任务。</span><span class="sxs-lookup"><span data-stu-id="651ad-117">The Azure Functions runtime and bindings take care of those tasks for you.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="651ad-118">创建 Azure Cosmos DB 帐户</span><span class="sxs-lookup"><span data-stu-id="651ad-118">Create an Azure Cosmos DB account</span></span>

> [!NOTE]
> <span data-ttu-id="651ad-119">本单元不是 Azure Cosmos DB 上的教程。</span><span class="sxs-lookup"><span data-stu-id="651ad-119">This unit is not intended to be a tutorial on Azure Cosmos DB.</span></span> <span data-ttu-id="651ad-120">如果您有兴趣在完成本模块后了解详细信息, 请在 Cosmos DB 上提供完整的学习路径。</span><span class="sxs-lookup"><span data-stu-id="651ad-120">There is a complete learning path on Cosmos DB if you are interested in learning more after finishing this module.</span></span>

### <a name="create-a-database-account"></a><span data-ttu-id="651ad-121">创建数据库帐户</span><span class="sxs-lookup"><span data-stu-id="651ad-121">Create a database account</span></span>

<span data-ttu-id="651ad-122">数据库帐户是用于管理一个或多个数据库的容器。</span><span class="sxs-lookup"><span data-stu-id="651ad-122">A database account is a container for managing one or more databases.</span></span> <span data-ttu-id="651ad-123">在可以创建数据库之前, 我们需要创建一个数据库帐户。</span><span class="sxs-lookup"><span data-stu-id="651ad-123">Before we can create a database, we need to create a database account.</span></span>

1. <span data-ttu-id="651ad-124">请确保使用随激活沙盒的相同帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="651ad-124">Make sure you are signed into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="651ad-125">选择 "**创建资源**" 按钮 (位于 Azure 门户的左上角), 然后选择 "**数据库** > **azure Cosmos DB**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-125">Select the **Create a resource** button found on the upper left-hand corner of the Azure portal, then select **Databases** > **Azure Cosmos DB**.</span></span>

1. <span data-ttu-id="651ad-126">在 "**创建 azure Cosmos db 帐户**" 页中, 输入新的 Azure Cosmos DB 帐户的设置。</span><span class="sxs-lookup"><span data-stu-id="651ad-126">In the **Create Azure Cosmos DB Account** page, enter the settings for the new Azure Cosmos DB account.</span></span>

    |<span data-ttu-id="651ad-127">设置</span><span class="sxs-lookup"><span data-stu-id="651ad-127">Setting</span></span>  |<span data-ttu-id="651ad-128">值</span><span class="sxs-lookup"><span data-stu-id="651ad-128">Value</span></span>  |<span data-ttu-id="651ad-129">说明</span><span class="sxs-lookup"><span data-stu-id="651ad-129">Description</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="651ad-130">订购</span><span class="sxs-lookup"><span data-stu-id="651ad-130">Subscription</span></span>     |  <span data-ttu-id="651ad-131">Concierge 订阅</span><span class="sxs-lookup"><span data-stu-id="651ad-131">Concierge subscription</span></span>       |  <span data-ttu-id="651ad-132">要用于此 Azure Cosmos DB 帐户的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="651ad-132">The Azure subscription that you want to use for this Azure Cosmos DB account.</span></span>       |
    |<span data-ttu-id="651ad-133">资源组</span><span class="sxs-lookup"><span data-stu-id="651ad-133">Resource Group</span></span>     |   <span data-ttu-id="651ad-134"><rgn>[沙盒资源组名称]</rgn></span><span class="sxs-lookup"><span data-stu-id="651ad-134"><rgn>[sandbox resource group name]</rgn></span></span>      |  <span data-ttu-id="651ad-135">将使用沙盒中的资源组预填充此字段。</span><span class="sxs-lookup"><span data-stu-id="651ad-135">This field is pre-populated with the resource group from your sandbox.</span></span>       |
    |<span data-ttu-id="651ad-136">帐户名称</span><span class="sxs-lookup"><span data-stu-id="651ad-136">Account Name</span></span>     | <span data-ttu-id="651ad-137">*输入一个唯一的名称*</span><span class="sxs-lookup"><span data-stu-id="651ad-137">*Enter a unique name*</span></span>        |  <span data-ttu-id="651ad-138">输入唯一名称以标识此 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="651ad-138">Enter a unique name to identify this Azure Cosmos DB account.</span></span> <span data-ttu-id="651ad-139">由于`documents.azure.com`将追加到您为创建 URI 而提供的名称, 因此请使用唯一但可识别的名称。</span><span class="sxs-lookup"><span data-stu-id="651ad-139">Because `documents.azure.com` is appended to the name that you provide to create your URI, use a unique but identifiable name.</span></span><br><br><span data-ttu-id="651ad-140">帐户名称只能包含小写字母、数字和连字符 (-) 字符, 并且必须包含3到50个字符。</span><span class="sxs-lookup"><span data-stu-id="651ad-140">The account name can contain only lowercase letters, numbers, and the hyphen (-) character, and it must contain 3 to 50 characters.</span></span>       |
    |<span data-ttu-id="651ad-141">API</span><span class="sxs-lookup"><span data-stu-id="651ad-141">API</span></span>     | <span data-ttu-id="651ad-142">Core (SQL)</span><span class="sxs-lookup"><span data-stu-id="651ad-142">Core (SQL)</span></span>        |  <span data-ttu-id="651ad-143">API 确定要创建的帐户类型。</span><span class="sxs-lookup"><span data-stu-id="651ad-143">The API determines the type of account to create.</span></span> <span data-ttu-id="651ad-144">Azure Cosmos DB 提供了五个 api 来满足您的应用程序的需求: SQL (document database)、Gremlin (graph 数据库)、MongoDB (文档数据库)、Azure 表和 Cassandra, 每个当前需要一个单独的帐户。</span><span class="sxs-lookup"><span data-stu-id="651ad-144">Azure Cosmos DB provides five APIs to suit the needs of your application: SQL (document database), Gremlin (graph database), MongoDB (document database), Azure Table, and Cassandra, each of which currently require a separate account.</span></span> <br><br><span data-ttu-id="651ad-145">选择 " **Core (SQL)**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-145">Select **Core (SQL)**.</span></span> <span data-ttu-id="651ad-146">目前, Azure Cosmos DB trigger、input 绑定和输出绑定仅适用于 SQL API 和 Graph API 帐户。</span><span class="sxs-lookup"><span data-stu-id="651ad-146">At this time, the Azure Cosmos DB trigger, input bindings, and output bindings only work with SQL API and Graph API accounts.</span></span>        |
    |<span data-ttu-id="651ad-147">位置</span><span class="sxs-lookup"><span data-stu-id="651ad-147">Location</span></span>     | <span data-ttu-id="651ad-148">从列表中选择</span><span class="sxs-lookup"><span data-stu-id="651ad-148">Select from the list</span></span>        | <span data-ttu-id="651ad-149">选择最接近的一个, 也可以是下面列出的允许的*沙盒区域*之一。</span><span class="sxs-lookup"><span data-stu-id="651ad-149">Choose the nearest one to you that is also one of the allowed *Sandbox regions* listed below.</span></span>        |

     <span data-ttu-id="651ad-150">将**新帐户**边栏中的所有其他字段保留为其默认值。</span><span class="sxs-lookup"><span data-stu-id="651ad-150">Leave all other fields in the **New account** blade at their default values.</span></span>

    ### <a name="sandbox-regions"></a><span data-ttu-id="651ad-151">沙盒区域</span><span class="sxs-lookup"><span data-stu-id="651ad-151">Sandbox regions</span></span>
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]


1. <span data-ttu-id="651ad-152">选择 "**审阅 + 创建**" 以查看和验证配置。</span><span class="sxs-lookup"><span data-stu-id="651ad-152">Select **Review + create** to review and validate the configuration.</span></span> 

1. <span data-ttu-id="651ad-153">在下一个屏幕上, 选择 "**创建**" 设置和部署数据库帐户。</span><span class="sxs-lookup"><span data-stu-id="651ad-153">On the next screen, select **Create** to provision and deploy the database account.</span></span>

1. <span data-ttu-id="651ad-154">部署可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="651ad-154">Deployment can take some time.</span></span> <span data-ttu-id="651ad-155">因此, 在继续之前, 请等待通知中心中的 "**部署已成功**" 消息。</span><span class="sxs-lookup"><span data-stu-id="651ad-155">So, wait for a **Deployment succeeded** message in the Notification Hub before proceeding.</span></span>

    ![已完成数据库帐户部署的通知](../media/5-db-deploy-success.PNG)

1. <span data-ttu-id="651ad-157">选择 "**转到资源**" 以导航到门户中的数据库帐户。</span><span class="sxs-lookup"><span data-stu-id="651ad-157">Select **Go to resource** to navigate to the database account in the portal.</span></span> <span data-ttu-id="651ad-158">接下来, 我们将向数据库中添加一个集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-158">We'll add a collection to the database next.</span></span>

### <a name="add-a-collection"></a><span data-ttu-id="651ad-159">添加集合</span><span class="sxs-lookup"><span data-stu-id="651ad-159">Add a collection</span></span>

<span data-ttu-id="651ad-160">在 Cosmos DB 中,*容器*包含用户生成的任意实体。</span><span class="sxs-lookup"><span data-stu-id="651ad-160">In Cosmos DB, a *container* holds arbitrary user-generated entities.</span></span> <span data-ttu-id="651ad-161">对于 SQL 和 MongoDB API 帐户, 容器映射到*集合*。</span><span class="sxs-lookup"><span data-stu-id="651ad-161">For SQL and MongoDB API accounts, a container maps to a *collection*.</span></span> <span data-ttu-id="651ad-162">在集合中, 我们存储文档。</span><span class="sxs-lookup"><span data-stu-id="651ad-162">Inside a collection, we store documents.</span></span>

<span data-ttu-id="651ad-163">我们来使用 Azure 门户中的数据资源管理器工具来创建数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-163">Let's use the Data Explorer tool in the Azure portal to create a database and collection.</span></span>

1. <span data-ttu-id="651ad-164">选择 "**数据资源管理器** > **新集合**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-164">Select **Data Explorer** > **New Collection**.</span></span>

2. <span data-ttu-id="651ad-165">在 "**添加集合**" 下, 输入新集合的设置。</span><span class="sxs-lookup"><span data-stu-id="651ad-165">Under **Add collection**, enter the settings for the new collection.</span></span>

    >[!TIP]
    ><span data-ttu-id="651ad-166">"**添加集合**" 区域显示在最右侧。</span><span class="sxs-lookup"><span data-stu-id="651ad-166">The **Add Collection** area is displayed on the far right.</span></span> <span data-ttu-id="651ad-167">您可能需要向右滚动才能看到它。</span><span class="sxs-lookup"><span data-stu-id="651ad-167">You may need to scroll right to see it.</span></span>

    |<span data-ttu-id="651ad-168">设置</span><span class="sxs-lookup"><span data-stu-id="651ad-168">Setting</span></span>|<span data-ttu-id="651ad-169">建议值</span><span class="sxs-lookup"><span data-stu-id="651ad-169">Suggested value</span></span>|<span data-ttu-id="651ad-170">说明</span><span class="sxs-lookup"><span data-stu-id="651ad-170">Description</span></span>
    |---|---|---|
    |<span data-ttu-id="651ad-171">数据库 ID</span><span class="sxs-lookup"><span data-stu-id="651ad-171">Database ID</span></span>|[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]| <span data-ttu-id="651ad-172">数据库名称必须包含1到255个字符, 并且不能包含/、 \\、#、? 或尾部空格。</span><span class="sxs-lookup"><span data-stu-id="651ad-172">Database names must contain from 1 through 255 characters, and they cannot contain /, \\, #, ?, or a trailing space.</span></span><br><br><span data-ttu-id="651ad-173">您可以随意在此处输入所需的内容, 但我们[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]建议将其作为新数据库的名称, 这就是我们在此单位中要参考的内容。</span><span class="sxs-lookup"><span data-stu-id="651ad-173">You are free to enter whatever you want here, but we suggest [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)] as the name for the new database, and that's what we'll refer to in this unit.</span></span> |
    |<span data-ttu-id="651ad-174">集合 ID</span><span class="sxs-lookup"><span data-stu-id="651ad-174">Collection ID</span></span>|[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]|<span data-ttu-id="651ad-175">输入[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]作为新集合的名称。</span><span class="sxs-lookup"><span data-stu-id="651ad-175">Enter [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] as the name for our new collection.</span></span> <span data-ttu-id="651ad-176">集合 id 与数据库名称具有相同的字符要求。</span><span class="sxs-lookup"><span data-stu-id="651ad-176">Collection IDs have the same character requirements as database names.</span></span>|
    |<span data-ttu-id="651ad-177">分区键</span><span class="sxs-lookup"><span data-stu-id="651ad-177">Partition key</span></span>|<span data-ttu-id="651ad-178">**/id**</span><span class="sxs-lookup"><span data-stu-id="651ad-178">**/id**</span></span>| <span data-ttu-id="651ad-179">partition 键指定 Cosmos DB 集合中的文档分布在逻辑数据分区中的方式。</span><span class="sxs-lookup"><span data-stu-id="651ad-179">The partition key specifies how the documents in Cosmos DB collections are distributed across logical data partitions.</span></span> <span data-ttu-id="651ad-180">为了方便起见, `id`我们将使用字段, 因为我们不关注此模块中的数据库性能。</span><span class="sxs-lookup"><span data-stu-id="651ad-180">We will use the `id` field as a convenience, as we are not concerned with database performance in this module.</span></span> <span data-ttu-id="651ad-181">若要了解有关 Cosmos 数据库分区键策略的详细信息, 请浏览 Microsoft 学习 Cosmos DB 模块。</span><span class="sxs-lookup"><span data-stu-id="651ad-181">If you would like to learn more about Cosmos DB partition key strategies, please explore the Microsoft Learn Cosmos DB modules.</span></span>|
    |<span data-ttu-id="651ad-182">提高</span><span class="sxs-lookup"><span data-stu-id="651ad-182">Throughput</span></span>|<span data-ttu-id="651ad-183">1000 RU</span><span class="sxs-lookup"><span data-stu-id="651ad-183">1000 RU</span></span>|<span data-ttu-id="651ad-184">将吞吐量更改为每秒1000个请求单元 (RU/秒)。</span><span class="sxs-lookup"><span data-stu-id="651ad-184">Change the throughput to 1000 request units per second (RU/s).</span></span> <span data-ttu-id="651ad-185">如果要减少延迟, 可以在以后扩展性能。</span><span class="sxs-lookup"><span data-stu-id="651ad-185">If you want to reduce latency, you can scale up the performance later.</span></span>|

3. <span data-ttu-id="651ad-186">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="651ad-186">Click **OK**.</span></span> <span data-ttu-id="651ad-187">数据资源管理器显示新的数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-187">The Data Explorer displays the new database and collection.</span></span> <span data-ttu-id="651ad-188">现在, 我们有一个数据库。</span><span class="sxs-lookup"><span data-stu-id="651ad-188">So, now we have a database.</span></span> <span data-ttu-id="651ad-189">在数据库中, 我们定义了一个集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-189">Inside the database, we've defined a collection.</span></span> <span data-ttu-id="651ad-190">接下来, 我们将添加一些数据 (也称为 "文档")。</span><span class="sxs-lookup"><span data-stu-id="651ad-190">Next, we'll add some data, also known as documents.</span></span>

### <a name="add-test-data"></a><span data-ttu-id="651ad-191">添加测试数据</span><span class="sxs-lookup"><span data-stu-id="651ad-191">Add test data</span></span>

<span data-ttu-id="651ad-192">我们在名[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]为的数据库中定义了一个集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-192">We've defined a collection in our database called [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)].</span></span> <span data-ttu-id="651ad-193">我们想要在每个文档中存储 URL 和 ID, 如网页书签列表。</span><span class="sxs-lookup"><span data-stu-id="651ad-193">We want to store a URL and ID in each document, like a list of web page bookmarks.</span></span>

<span data-ttu-id="651ad-194">您将使用数据浏览器将数据添加到新集合中。</span><span class="sxs-lookup"><span data-stu-id="651ad-194">You'll add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="651ad-195">在数据资源管理器中, 新数据库将显示在 "集合" 窗格中。</span><span class="sxs-lookup"><span data-stu-id="651ad-195">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="651ad-196">展开[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]数据库, 展开[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]集合, 选择 "**文档**", 然后选择 "**新建文档**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-196">Expand the [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)] database, expand the [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] collection, select **Documents**, and then select **New Document**.</span></span>

2. <span data-ttu-id="651ad-197">将新文档的默认内容替换为以下 JSON。</span><span class="sxs-lookup"><span data-stu-id="651ad-197">Replace the default content of the new document with the following JSON.</span></span>

     ```json
     {
         "id": "docs",
         "URL": "https://docs.microsoft.com/azure"
     }
     ```

3. <span data-ttu-id="651ad-198">将 JSON 添加到 "**文档**" 选项卡后, 选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-198">After you've added the JSON to the **Documents** tab, select **Save**.</span></span>

    <span data-ttu-id="651ad-199">请注意, 有些属性比我们添加的属性多。</span><span class="sxs-lookup"><span data-stu-id="651ad-199">Notice that there are more properties than the ones we added.</span></span> <span data-ttu-id="651ad-200">它们都以下划线 (_rid、_self、_etag、_attachments、_ts) 开头。</span><span class="sxs-lookup"><span data-stu-id="651ad-200">They all begin with an underline (_rid, _self, _etag, _attachments, _ts).</span></span> <span data-ttu-id="651ad-201">这些是由系统生成的用于帮助管理文档的属性。</span><span class="sxs-lookup"><span data-stu-id="651ad-201">These are properties generated by the system to help manage the document.</span></span>

    |<span data-ttu-id="651ad-202">属性</span><span class="sxs-lookup"><span data-stu-id="651ad-202">Property</span></span>  |<span data-ttu-id="651ad-203">说明</span><span class="sxs-lookup"><span data-stu-id="651ad-203">Description</span></span>  |
    |---------|---------|
    | `_rid`     |     <span data-ttu-id="651ad-204">资源 ID 是一个唯一的标识符, 它在资源模型上也按资源堆栈为层次结构。</span><span class="sxs-lookup"><span data-stu-id="651ad-204">The resource ID is a unique identifier that is also hierarchical per the resource stack on the resource model.</span></span> <span data-ttu-id="651ad-205">它在内部用于放置和导航文档资源。</span><span class="sxs-lookup"><span data-stu-id="651ad-205">It is used internally for placement and navigation of the document resource.</span></span>    |
    | `_self`     |   <span data-ttu-id="651ad-206">资源的唯一可寻址 URI。</span><span class="sxs-lookup"><span data-stu-id="651ad-206">The unique addressable URI for the resource.</span></span>      |
    | `_etag`     |   <span data-ttu-id="651ad-207">对于开放式并发控制是必需的。</span><span class="sxs-lookup"><span data-stu-id="651ad-207">Required for optimistic concurrency control.</span></span>     |
    | `_attachments`     |  <span data-ttu-id="651ad-208">附件资源的可寻址路径。</span><span class="sxs-lookup"><span data-stu-id="651ad-208">The addressable path for the attachments resource.</span></span>       |
    | `_ts`     |    <span data-ttu-id="651ad-209">此资源的上次更新时间戳。</span><span class="sxs-lookup"><span data-stu-id="651ad-209">The time stamp of the last update of this resource.</span></span>    |

4. <span data-ttu-id="651ad-210">让我们向集合中添加更多文档。</span><span class="sxs-lookup"><span data-stu-id="651ad-210">Let's add a few more documents into the collection.</span></span> <span data-ttu-id="651ad-211">使用以下内容创建另外四个文档。</span><span class="sxs-lookup"><span data-stu-id="651ad-211">Create four more documents with the following content.</span></span> <span data-ttu-id="651ad-212">请记住保存您的工作。</span><span class="sxs-lookup"><span data-stu-id="651ad-212">Remember to save your work.</span></span>

    ```json
    {
        "id": "portal",
        "URL": "https://portal.azure.com"
    }
    ```

    ```json
    {
        "id": "learn",
        "URL": "https://docs.microsoft.com/learn"
    }
    ```

    ```json
    {
        "id": "marketplace",
        "URL": "https://azuremarketplace.microsoft.com/marketplace/apps"
    }
    ```

    ```json
    {
        "id": "blog",
        "URL": "https://azure.microsoft.com/blog"
    }
    ```

1. <span data-ttu-id="651ad-213">完成后, 您的集合应如下所示:</span><span class="sxs-lookup"><span data-stu-id="651ad-213">When you've finished, your collection should look like the following:</span></span>

    ![门户中的 SQL API UI, 显示添加到书签集合中的项的列表。](../media/5-db-bookmark-coll.PNG)

<span data-ttu-id="651ad-215">您现在在书签集合中有几个条目。</span><span class="sxs-lookup"><span data-stu-id="651ad-215">You now have a few entries in your bookmark collection.</span></span> <span data-ttu-id="651ad-216">我们的方案将按如下方式工作。</span><span class="sxs-lookup"><span data-stu-id="651ad-216">Our scenario will work as follows.</span></span> <span data-ttu-id="651ad-217">如果请求收到 (例如, "id = 文档"), 您将在书签集合中查找该 id 并返回 URL `https://docs.microsoft.com/azure`。</span><span class="sxs-lookup"><span data-stu-id="651ad-217">If a request arrives with, for example, "id=docs", you'll look up that ID in your bookmarks collection and return the URL `https://docs.microsoft.com/azure`.</span></span> <span data-ttu-id="651ad-218">让我们创建一个用于查找此集合中的值的 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="651ad-218">Let's make an Azure function that looks up values in this collection.</span></span>

## <a name="create-your-function"></a><span data-ttu-id="651ad-219">创建函数</span><span class="sxs-lookup"><span data-stu-id="651ad-219">Create your function</span></span>

1. <span data-ttu-id="651ad-220">导航到在前面的单元中创建的函数应用程序。</span><span class="sxs-lookup"><span data-stu-id="651ad-220">Navigate to the function app that you created in the preceding unit.</span></span>

1. <span data-ttu-id="651ad-221">选择 "**函数**"**+** 旁边的 "**添加**" () 按钮以启动函数创建过程。</span><span class="sxs-lookup"><span data-stu-id="651ad-221">Select the **Add** (**+**) button next to **Functions** to start the function creation process.</span></span> 
   <span data-ttu-id="651ad-222">页面显示一组完整的受支持的触发器。</span><span class="sxs-lookup"><span data-stu-id="651ad-222">The page displays the complete set of supported triggers.</span></span>

1. <span data-ttu-id="651ad-223">选择**HTTP 触发器**</span><span class="sxs-lookup"><span data-stu-id="651ad-223">Select **HTTP trigger**</span></span>

1. <span data-ttu-id="651ad-224">使用以下值填写显示在右侧的 "**新建函数**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="651ad-224">Fill out the **New Function** dialog that appears to the right using the following values.</span></span>

    | <span data-ttu-id="651ad-225">Field</span><span class="sxs-lookup"><span data-stu-id="651ad-225">Field</span></span> | <span data-ttu-id="651ad-226">值</span><span class="sxs-lookup"><span data-stu-id="651ad-226">Value</span></span> |
    |----------|--------|
    | <span data-ttu-id="651ad-227">名称</span><span class="sxs-lookup"><span data-stu-id="651ad-227">Name</span></span>     | [!INCLUDE [func-name-find](./func-name-find.md)] |
    | <span data-ttu-id="651ad-228">授权级别</span><span class="sxs-lookup"><span data-stu-id="651ad-228">Authorization level</span></span> | <span data-ttu-id="651ad-229">**函数**</span><span class="sxs-lookup"><span data-stu-id="651ad-229">**Function**</span></span> |

1. <span data-ttu-id="651ad-230">选择 "**创建**" 以创建函数。</span><span class="sxs-lookup"><span data-stu-id="651ad-230">Select **Create** to create your function.</span></span>
    <span data-ttu-id="651ad-231">此操作将在代码编辑器中打开该 *.js*文件, 并显示 HTTP 触发的函数的默认实现。</span><span class="sxs-lookup"><span data-stu-id="651ad-231">This action opens the *index.js* file in the code editor and displays a default implementation of the HTTP-triggered function.</span></span>

### <a name="verify-the-function"></a><span data-ttu-id="651ad-232">验证函数</span><span class="sxs-lookup"><span data-stu-id="651ad-232">Verify the function</span></span>

<span data-ttu-id="651ad-233">您可以通过测试新函数来验证我们已完成的操作, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="651ad-233">You can verify what we have done so far by testing our new function as follows:</span></span>

1. <span data-ttu-id="651ad-234">在新函数中, 单击右上角的 "**获取函数 URL** ", 选择 "**默认 (功能键)**", 然后单击 "**复制**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-234">In your new function, click **Get function URL** at the top right, select **default (Function key)**, and then click **Copy**.</span></span>

1. <span data-ttu-id="651ad-235">将复制的函数 URL 粘贴到浏览器的地址栏中。</span><span class="sxs-lookup"><span data-stu-id="651ad-235">Paste the function URL you copied into your browser's address bar.</span></span> <span data-ttu-id="651ad-236">将查询字符串值`&name=<yourname>`添加到 URL 的末尾, 然后按**enter**以执行请求。</span><span class="sxs-lookup"><span data-stu-id="651ad-236">Add the query string value `&name=<yourname>` to the end of the URL and press **Enter** to execute the request.</span></span> <span data-ttu-id="651ad-237">应在浏览器中获取 Azure 函数权限的响应。</span><span class="sxs-lookup"><span data-stu-id="651ad-237">You should get a response from the Azure Function right in the browser.</span></span>

<span data-ttu-id="651ad-238">现在我们已开始使用我们的基本功能, 我们将重点介绍如何从 Azure Cosmos DB 或我们的方案 (我们[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]的集合) 中读取数据。</span><span class="sxs-lookup"><span data-stu-id="651ad-238">Now that we have our bare-bones function working, let's turn our attention to reading data from our Azure Cosmos DB, or in our scenario, our [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] collection.</span></span>

## <a name="add-an-azure-cosmos-db-input-binding"></a><span data-ttu-id="651ad-239">添加 Azure Cosmos DB 输入绑定</span><span class="sxs-lookup"><span data-stu-id="651ad-239">Add an Azure Cosmos DB input binding</span></span>

<span data-ttu-id="651ad-240">若要从数据库中读取数据, 需要定义输入绑定。</span><span class="sxs-lookup"><span data-stu-id="651ad-240">To read data from the database, you need to define an input binding.</span></span> <span data-ttu-id="651ad-241">正如您所看到的, 可以配置一个绑定, 只需几个步骤即可与您的数据库进行对话。</span><span class="sxs-lookup"><span data-stu-id="651ad-241">As you'll see, you can configure a binding that can talk to your database in just a few steps.</span></span>

1. <span data-ttu-id="651ad-242">在左窗格中选择 "**集成**" 以打开 "集成" 选项卡。您使用的模板创建了一个 http 触发器和一个 http 输出绑定。</span><span class="sxs-lookup"><span data-stu-id="651ad-242">Select **Integrate** in the left pane to open the integration tab. The template you used created an HTTP trigger and an HTTP output binding.</span></span> <span data-ttu-id="651ad-243">现在, 添加新的 Azure Cosmos DB 输入绑定。</span><span class="sxs-lookup"><span data-stu-id="651ad-243">Now add your new Azure Cosmos DB input binding.</span></span>

1. <span data-ttu-id="651ad-244">在 "**输入**" 列中选择 "**新建输入**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-244">Select **New Input** in the **Inputs** column.</span></span>
   <span data-ttu-id="651ad-245">将显示所有可能的输入绑定类型的列表。</span><span class="sxs-lookup"><span data-stu-id="651ad-245">A list of all possible input binding types is displayed.</span></span>

1. <span data-ttu-id="651ad-246">在列表中, 选择 " **Azure Cosmos DB**", 然后选择 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-246">In the list, select **Azure Cosmos DB**, and then select **Select**.</span></span>
   <span data-ttu-id="651ad-247">此操作将打开 "Azure Cosmos DB 输入配置" 页。</span><span class="sxs-lookup"><span data-stu-id="651ad-247">This action opens the Azure Cosmos DB input configuration page.</span></span> <span data-ttu-id="651ad-248">接下来, 您将设置与您的数据库的连接。</span><span class="sxs-lookup"><span data-stu-id="651ad-248">Next, you'll set up a connection to your database.</span></span>

1. <span data-ttu-id="651ad-249">如果在**Azure Cosmos DB 输入**配置 UI 中出现以下消息, 告诉您必须安装扩展, 请选择 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-249">If the following message appears in the **Azure Cosmos DB input** configuration UI telling you that you must install an extension, select **Install**.</span></span> 

    ![HTTP 触发 Azure 函数的默认 JavaScript 实现](../media/extension-not-installed.png)

    > [!NOTE]
    > <span data-ttu-id="651ad-251">安装扩展可能需要一段时间, 因此请等待安装完成, 然后再继续执行下一步。</span><span class="sxs-lookup"><span data-stu-id="651ad-251">It can take a while to install an extension, so please wait for installation to complete before proceeding to the next step.</span></span>

1. <span data-ttu-id="651ad-252">在 " **Azure Cosmos DB 帐户连接**" 框旁边, 选择 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-252">Next to the **Azure Cosmos DB account connection** box, select **new**.</span></span>
   <span data-ttu-id="651ad-253">此操作将打开 "**连接**" 窗口, 该窗口已选择 " **azure Cosmos DB 帐户**" 和 "azure 订阅"。</span><span class="sxs-lookup"><span data-stu-id="651ad-253">This action opens the **Connection** window, which already has **Azure Cosmos DB account** and your Azure subscription selected.</span></span> <span data-ttu-id="651ad-254">剩下的唯一事情是选择数据库帐户 ID。</span><span class="sxs-lookup"><span data-stu-id="651ad-254">The only thing left to do is to select a database account ID.</span></span>

1. <span data-ttu-id="651ad-255">在 "创建数据库帐户" 部分中, 必须提供 ID 值。</span><span class="sxs-lookup"><span data-stu-id="651ad-255">In the "Create a database account" section, you had to supply an ID value.</span></span> <span data-ttu-id="651ad-256">在 "**数据库帐户**" 下拉列表中找到该值, 然后单击 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-256">Find that value in the **Database Account** drop-down list, and then click **Select**.</span></span>

1. <span data-ttu-id="651ad-257">已配置与数据库的新连接, 并显示在 " **Azure Cosmos DB 帐户连接**" 字段中。</span><span class="sxs-lookup"><span data-stu-id="651ad-257">A new connection to the database is configured and is shown in the **Azure Cosmos DB account connection** field.</span></span> <span data-ttu-id="651ad-258">如果您想了解此抽象名称的实际背后的内容, 请单击 "*显示值*" 以显示连接字符串。</span><span class="sxs-lookup"><span data-stu-id="651ad-258">If you're curious about what is actually behind this abstract name, click *show value* to reveal the connection string.</span></span>

<span data-ttu-id="651ad-259">您想要查找具有特定 ID 的书签, 让我们将接收到的 id 与绑定的 id 关联起来。</span><span class="sxs-lookup"><span data-stu-id="651ad-259">You want to look up a bookmark with a specific ID, so let's tie the ID we receive to the binding.</span></span>

1. <span data-ttu-id="651ad-260">在 "**文档 ID (可选)** " 字段中`{id}`, 输入。</span><span class="sxs-lookup"><span data-stu-id="651ad-260">In the **Document ID (optional)** field, enter `{id}`.</span></span> <span data-ttu-id="651ad-261">此语法称为*绑定表达式*。</span><span class="sxs-lookup"><span data-stu-id="651ad-261">This syntax is known as a *binding expression*.</span></span> <span data-ttu-id="651ad-262">此函数由 HTTP 请求触发, 该请求使用查询字符串指定要查找的 ID。</span><span class="sxs-lookup"><span data-stu-id="651ad-262">The function is triggered by an HTTP request that uses a query string to specify the ID to look up.</span></span> <span data-ttu-id="651ad-263">由于 id 在集合中是唯一的, 因此绑定将返回0个 (未找到) 或1个 (找到的) 文档。</span><span class="sxs-lookup"><span data-stu-id="651ad-263">Since IDs are unique in our collection, the binding will return either 0 (not found) or 1 (found) documents.</span></span>

1. <span data-ttu-id="651ad-264">使用下表中的值仔细填写本页上的其余字段。</span><span class="sxs-lookup"><span data-stu-id="651ad-264">Carefully fill out the remaining fields on this page using the values in the following table.</span></span> <span data-ttu-id="651ad-265">您可以随时单击每个字段名称右侧的信息图标, 以了解有关每个字段的用途的详细信息。</span><span class="sxs-lookup"><span data-stu-id="651ad-265">At any time, you can click on the information icon to the right of each field name to learn more about the purpose of each field.</span></span>

    |<span data-ttu-id="651ad-266">设置</span><span class="sxs-lookup"><span data-stu-id="651ad-266">Setting</span></span>  |<span data-ttu-id="651ad-267">值</span><span class="sxs-lookup"><span data-stu-id="651ad-267">Value</span></span>  |<span data-ttu-id="651ad-268">说明</span><span class="sxs-lookup"><span data-stu-id="651ad-268">Description</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="651ad-269">文档参数名称</span><span class="sxs-lookup"><span data-stu-id="651ad-269">Document parameter name</span></span>     |  <span data-ttu-id="651ad-270">**书签**</span><span class="sxs-lookup"><span data-stu-id="651ad-270">**bookmark**</span></span>       |  <span data-ttu-id="651ad-271">用于标识代码中的此绑定的名称。</span><span class="sxs-lookup"><span data-stu-id="651ad-271">The name used to identify this binding in your code.</span></span>      |
    |<span data-ttu-id="651ad-272">数据库名称</span><span class="sxs-lookup"><span data-stu-id="651ad-272">Database name</span></span>     |  [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]       | <span data-ttu-id="651ad-273">要使用的数据库。</span><span class="sxs-lookup"><span data-stu-id="651ad-273">The database to work with.</span></span> <span data-ttu-id="651ad-274">此值是我们在本课前面设置的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="651ad-274">This value is the database name we set earlier in this lesson.</span></span>        |
    |<span data-ttu-id="651ad-275">集合名称</span><span class="sxs-lookup"><span data-stu-id="651ad-275">Collection Name</span></span>     |  [!INCLUDE [cosmos-db-name](./cosmos-coll-name.md)]        | <span data-ttu-id="651ad-276">将从中读取数据的集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-276">The collection from which we'll read data.</span></span> <span data-ttu-id="651ad-277">此设置是在本课前面的部分定义的。</span><span class="sxs-lookup"><span data-stu-id="651ad-277">This setting was defined earlier in the lesson.</span></span> |
    |<span data-ttu-id="651ad-278">SQL 查询 (可选)</span><span class="sxs-lookup"><span data-stu-id="651ad-278">SQL Query (optional)</span></span>    |   <span data-ttu-id="651ad-279">保留为空</span><span class="sxs-lookup"><span data-stu-id="651ad-279">leave blank</span></span>       |   <span data-ttu-id="651ad-280">我们仅基于 ID 在一次检索一个文档。</span><span class="sxs-lookup"><span data-stu-id="651ad-280">We are only retrieving one document at a time based on the ID.</span></span> <span data-ttu-id="651ad-281">因此, 使用 "文档 ID" 字段进行筛选比在此实例中使用 SQL 查询更好。</span><span class="sxs-lookup"><span data-stu-id="651ad-281">So, filtering with the Document ID field is a better than using a SQL Query in this instance.</span></span> <span data-ttu-id="651ad-282">我们可以手工创建一个 SQL 查询, 以返回一个`SELECT * from b where b.ID = {id}`条目 ()。</span><span class="sxs-lookup"><span data-stu-id="651ad-282">We could craft a SQL Query to return one entry (`SELECT * from b where b.ID = {id}`).</span></span> <span data-ttu-id="651ad-283">该查询确实会返回一个文档, 但会将其返回到文档集合中。</span><span class="sxs-lookup"><span data-stu-id="651ad-283">That query would indeed return a document, but it would return it in a document collection.</span></span> <span data-ttu-id="651ad-284">我们的代码必须不必要地处理集合。</span><span class="sxs-lookup"><span data-stu-id="651ad-284">Our code would have to manipulate a collection unnecessarily.</span></span> <span data-ttu-id="651ad-285">当您想要获取多个文档时, 请使用 SQL 查询方法。</span><span class="sxs-lookup"><span data-stu-id="651ad-285">Use the SQL Query approach when you want to get multiple documents.</span></span>   |
    |<span data-ttu-id="651ad-286">分区键 (可选)</span><span class="sxs-lookup"><span data-stu-id="651ad-286">Partition key (optional)</span></span> | <span data-ttu-id="651ad-287">**号**</span><span class="sxs-lookup"><span data-stu-id="651ad-287">**{id}**</span></span> |  <span data-ttu-id="651ad-288">在前面创建[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] Cosmos DB 集合时, 添加已定义的分区键。</span><span class="sxs-lookup"><span data-stu-id="651ad-288">Add the partition key that we defined when we created the [!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] Cosmos DB collection earlier.</span></span>  <span data-ttu-id="651ad-289">此处输入的项 (在输入绑定格式`{<key>}`中指定) 必须与集合中的键相匹配。</span><span class="sxs-lookup"><span data-stu-id="651ad-289">The key entered here (specified in input binding format `{<key>}`) must match the one in the collection.</span></span>|

9. <span data-ttu-id="651ad-290">选择 "**保存**" 以保存对此绑定配置所做的所有更改。</span><span class="sxs-lookup"><span data-stu-id="651ad-290">Select **Save** to save all changes to this binding configuration.</span></span>

<span data-ttu-id="651ad-291">现在, 您已定义绑定, 现在可以在您的函数中使用它了。</span><span class="sxs-lookup"><span data-stu-id="651ad-291">Now that you have your binding defined, it's time to use it in your function.</span></span>

## <a name="update-function-implementation"></a><span data-ttu-id="651ad-292">更新函数实现</span><span class="sxs-lookup"><span data-stu-id="651ad-292">Update function implementation</span></span>

1. <span data-ttu-id="651ad-293">选择您[!INCLUDE [func-name-find](./func-name-find.md)]的函数, 在代码编辑器中打开*node.js* 。</span><span class="sxs-lookup"><span data-stu-id="651ad-293">Select your function, [!INCLUDE [func-name-find](./func-name-find.md)], to open *index.js* in the code editor.</span></span> <span data-ttu-id="651ad-294">您已添加了要从数据库读取的输入绑定, 因此请更新逻辑以使用此绑定。</span><span class="sxs-lookup"><span data-stu-id="651ad-294">You've added an input binding to read from your database, so update the logic to use this binding.</span></span>

2. <span data-ttu-id="651ad-295">将*index .js*中的所有代码替换为以下代码段中的代码, 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="651ad-295">Replace all code in *index.js* with the code from the following snippet and hit **Save**.</span></span>

   [!code-javascript[](../code/find-bookmark-single.js)]

<span data-ttu-id="651ad-296">传入的 HTTP 请求将触发函数, 并将`id`查询参数传递给 Cosmos DB 输入绑定。</span><span class="sxs-lookup"><span data-stu-id="651ad-296">An incoming HTTP request triggers the function, and an `id` query parameter is passed to the Cosmos DB input binding.</span></span> <span data-ttu-id="651ad-297">如果数据库找到与此 ID 匹配的文档, 则会将`bookmark`该参数设置为找到的文档。</span><span class="sxs-lookup"><span data-stu-id="651ad-297">If the database finds a document that matches this ID, then the `bookmark` parameter will be set to the located document.</span></span> <span data-ttu-id="651ad-298">在这种情况下, 我们将构建一个响应, 其中包含在书签标记的文档中找到的 URL 值。</span><span class="sxs-lookup"><span data-stu-id="651ad-298">In that case, we construct a response that contains the URL value found in the bookmarked document.</span></span> <span data-ttu-id="651ad-299">如果找不到与此键匹配的文档, 我们将使用有效负载和状态代码进行响应, 告知用户出现坏消息。</span><span class="sxs-lookup"><span data-stu-id="651ad-299">If no document is found matching this key, we would respond with a payload and status code that tells the user the bad news.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="651ad-300">试用</span><span class="sxs-lookup"><span data-stu-id="651ad-300">Try it out</span></span>

1. <span data-ttu-id="651ad-301">选择右上角的 "**获取函数 URL** ", 选择 "**默认 (功能键)**", 然后选择 "**复制**" 以复制函数的 URL。</span><span class="sxs-lookup"><span data-stu-id="651ad-301">Select **Get function URL** at the top right, select **default (Function key)**, and then select **Copy** to copy the function's URL.</span></span>

2. <span data-ttu-id="651ad-302">将复制的函数 URL 粘贴到浏览器的地址栏中。</span><span class="sxs-lookup"><span data-stu-id="651ad-302">Paste the function URL you copied into your browser's address bar.</span></span> <span data-ttu-id="651ad-303">将查询字符串值`&id=docs`添加到此 URL 的末尾, 然后按键盘`Enter`上的键以执行请求。</span><span class="sxs-lookup"><span data-stu-id="651ad-303">Add the query string value `&id=docs` to the end of this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="651ad-304">您应该会看到一个包含指向该资源的 URL 的响应。</span><span class="sxs-lookup"><span data-stu-id="651ad-304">You should see a response that includes a URL to that resource.</span></span>

3. <span data-ttu-id="651ad-305">将`&id=docs`替换`&id=missing`为, 并观察响应。</span><span class="sxs-lookup"><span data-stu-id="651ad-305">Replace `&id=docs` with `&id=missing`, and observe the response.</span></span>

    >[!TIP]
    ><span data-ttu-id="651ad-306">您还可以使用 function portal UI 中的 "**测试**" 选项卡来测试函数。</span><span class="sxs-lookup"><span data-stu-id="651ad-306">You can also test the function using the **Test** tab in the function portal UI.</span></span> <span data-ttu-id="651ad-307">您可以添加查询参数或提供请求正文, 以获取与前面步骤中所述相同的结果。</span><span class="sxs-lookup"><span data-stu-id="651ad-307">You can add a query parameter or supply a request body to get the same results as described in the preceding steps.</span></span>

<span data-ttu-id="651ad-308">在此单位中, 我们已手动创建了第一个输入绑定, 以从 Azure Cosmos DB 数据库进行读取。</span><span class="sxs-lookup"><span data-stu-id="651ad-308">In this unit, we created our first input binding manually to read from an Azure Cosmos DB database.</span></span> <span data-ttu-id="651ad-309">我们为搜索数据库和读取数据而编写的代码量最小, 这归功于绑定。</span><span class="sxs-lookup"><span data-stu-id="651ad-309">The amount of code we wrote to search our database and read data was minimal, thanks to bindings.</span></span> <span data-ttu-id="651ad-310">我们做的大部分工作都以声明方式配置绑定, 而平台负责处理 rest。</span><span class="sxs-lookup"><span data-stu-id="651ad-310">We did most of our work configuring the binding declaratively, and the platform took care of the rest.</span></span>

<span data-ttu-id="651ad-311">在下一个单元中, 我们将通过 Azure Cosmos DB 输出绑定向书签集合中添加更多数据。</span><span class="sxs-lookup"><span data-stu-id="651ad-311">In the next unit, we'll add more data to our bookmark collection through an Azure Cosmos DB output binding.</span></span>