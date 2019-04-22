<span data-ttu-id="036cf-101">向您的客户提供对在线衣物网站上产品的最快访问权限对您的客户和您的企业成功至关重要。</span><span class="sxs-lookup"><span data-stu-id="036cf-101">Providing your customers the fastest access to the products on your online clothing site is paramount to your customers, and your businesses success.</span></span> <span data-ttu-id="036cf-102">通过减少数据与用户之间的距离, 可以更快地传递更多的内容。</span><span class="sxs-lookup"><span data-stu-id="036cf-102">By decreasing the distance data has to travel to your users, you can deliver more content faster.</span></span> <span data-ttu-id="036cf-103">如果数据存储在 Azure Cosmos DB 中, 则将网站的数据复制到世界各地的多个区域是一个点, 然后单击 "操作"。</span><span class="sxs-lookup"><span data-stu-id="036cf-103">If your data is stored in Azure Cosmos DB, replicating your site's data to multiple regions around the world is a point and click operation.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="036cf-104">在此单元中, 你将了解全局分发和本机多核数据库服务的优势, 然后将你的帐户复制到三个其他区域。</span><span class="sxs-lookup"><span data-stu-id="036cf-104">In this unit you'll learn the benefits of global distribution and a natively multi-mastered database service, and then replicate your account into three additional regions.</span></span>

## <a name="global-distribution-basics"></a><span data-ttu-id="036cf-105">全球分布基础知识</span><span class="sxs-lookup"><span data-stu-id="036cf-105">Global distribution basics</span></span>

<span data-ttu-id="036cf-106">通过全局分发, 可以将数据从一个区域复制到多个 Azure 区域。</span><span class="sxs-lookup"><span data-stu-id="036cf-106">Global distribution enables you to replicate data from one region into multiple Azure regions.</span></span> <span data-ttu-id="036cf-107">您可以在任何时候添加或删除数据库复制到的区域, Azure Cosmos DB 可确保在您添加其他区域时, 数据在30分钟内可用于操作, 假定您的数据为 100 tb 或更低。</span><span class="sxs-lookup"><span data-stu-id="036cf-107">You can add or remove regions in which your database is replicated at any time, and Azure Cosmos DB ensures that when you add an additional region, your data is available for operations within 30 minutes, assuming your data is 100 TBs or less.</span></span>

<span data-ttu-id="036cf-108">在两个或更多区域中复制数据的常见方案有两个:</span><span class="sxs-lookup"><span data-stu-id="036cf-108">There are two common scenarios for replicating data in two or more regions:</span></span>

1. <span data-ttu-id="036cf-109">将低延迟数据访问传递给最终用户, 无论它们位于全球的何处</span><span class="sxs-lookup"><span data-stu-id="036cf-109">Delivering low-latency data access to end users no matter where they are located around the globe</span></span>
2. <span data-ttu-id="036cf-110">为业务连续性和灾难恢复添加区域弹性 (BCDR)</span><span class="sxs-lookup"><span data-stu-id="036cf-110">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="036cf-111">若要向客户提供低延迟访问, 建议您将数据复制到离用户最接近的地区。</span><span class="sxs-lookup"><span data-stu-id="036cf-111">To deliver low-latency access to customers, it is recommended that you replicate the data to regions closest to where your users are.</span></span> <span data-ttu-id="036cf-112">对于您的在线服装公司, 您的洛杉矶、纽约和东京的客户。</span><span class="sxs-lookup"><span data-stu-id="036cf-112">For your online clothing company, you have customers in Los Angeles, New York, and Tokyo.</span></span> <span data-ttu-id="036cf-113">查看 " [Azure 区域](https://azure.microsoft.com/global-infrastructure/regions/)" 页面, 并确定与这些客户组最接近的地区, 因为这些是您将向其复制用户的位置。</span><span class="sxs-lookup"><span data-stu-id="036cf-113">Take a look at the [Azure regions](https://azure.microsoft.com/global-infrastructure/regions/) page, and determine the closest regions to those sets of customers, as those are the locations you'll replicate users to.</span></span>

<span data-ttu-id="036cf-114">若要提供 BCDR 解决方案, 建议根据[业务连续性和灾难恢复 (BCDR)](https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/)中描述的区域对添加区域: Azure 配对区域文章。</span><span class="sxs-lookup"><span data-stu-id="036cf-114">To provide a BCDR solution, it is recommended to add regions based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions](https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/) article.</span></span>

<span data-ttu-id="036cf-115">当复制数据库时, 吞吐量和存储也同样进行复制。</span><span class="sxs-lookup"><span data-stu-id="036cf-115">When a database is replicated, the throughput and storage are replicated equally as well.</span></span> <span data-ttu-id="036cf-116">因此, 如果您的原始数据库的存储空间为 10gb, 并且吞吐量为 1000 RU/秒, 并且如果您将其复制到三个其他区域, 则每个区域的吞吐量都是 10gb, 1000 RU/秒。</span><span class="sxs-lookup"><span data-stu-id="036cf-116">So if your original database had 10GB of storage, and throughput of 1,000 RU/s, and if you replicated that to three additional regions, each region would have 10GB of data and 1,000 RU/s of throughput.</span></span> <span data-ttu-id="036cf-117">由于存储和吞吐量是在每个区域中复制的, 因此复制到区域的成本与原始区域相同, 因此复制到3个其他区域的成本大约是原始非复制数据库的四倍。</span><span class="sxs-lookup"><span data-stu-id="036cf-117">Because the storage and throughput is replicated in each region, the cost of replicating to a region is the same as the original region, so replicating to 3 additional regions, would cost approximately four times the original non-replicated database.</span></span>

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a><span data-ttu-id="036cf-118">在门户中创建 Azure Cosmos DB 帐户</span><span class="sxs-lookup"><span data-stu-id="036cf-118">Creating an Azure Cosmos DB account in the portal</span></span>

1. <span data-ttu-id="036cf-119">使用用于激活沙盒的相同帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="036cf-119">Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you used to activate the sandbox.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="036cf-120">使用相同的帐户登录到 Azure 门户和沙盒。</span><span class="sxs-lookup"><span data-stu-id="036cf-120">Login to the Azure portal and the sandbox with the same account.</span></span>
    >
    > <span data-ttu-id="036cf-121">使用上面的链接登录到 Azure 门户, 以确保您已连接到沙盒, 该沙箱提供对 Concierge 订阅的访问权限。</span><span class="sxs-lookup"><span data-stu-id="036cf-121">Login to the Azure portal using the link above to ensure you are connected to the sandbox, which provides access to a Concierge Subscription.</span></span>

1. <span data-ttu-id="036cf-122">单击 "**创建资源** > **数据库** > " "**Azure Cosmos DB**"。</span><span class="sxs-lookup"><span data-stu-id="036cf-122">Click **Create a resource** > **Databases** > **Azure Cosmos DB**.</span></span>

   ![Azure portal 数据库窗格](../media/2-global-distribution/2-create-nosql-db-databases-json-tutorial.png)

1. <span data-ttu-id="036cf-124">在 "**创建 Azure Cosmos db 帐户**" 页上, 输入新的 Azure Cosmos DB 帐户的设置, 包括位置。</span><span class="sxs-lookup"><span data-stu-id="036cf-124">On the **Create Azure Cosmos DB Account** page, enter the settings for the new Azure Cosmos DB account, including the location.</span></span>

    <!-- Resource selection -->  
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    <span data-ttu-id="036cf-125">设置</span><span class="sxs-lookup"><span data-stu-id="036cf-125">Setting</span></span>|<span data-ttu-id="036cf-126">值</span><span class="sxs-lookup"><span data-stu-id="036cf-126">Value</span></span>|<span data-ttu-id="036cf-127">说明</span><span class="sxs-lookup"><span data-stu-id="036cf-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="036cf-128">订购</span><span class="sxs-lookup"><span data-stu-id="036cf-128">Subscription</span></span>|<span data-ttu-id="036cf-129">*Concierge 订阅*</span><span class="sxs-lookup"><span data-stu-id="036cf-129">*Concierge Subscription*</span></span>|<span data-ttu-id="036cf-130">选择您的 Concierge 订阅。</span><span class="sxs-lookup"><span data-stu-id="036cf-130">Select your Concierge Subscription.</span></span> <span data-ttu-id="036cf-131">如果您没有看到列出的 Concierge 订阅, 则您的订阅上启用了多个租户, 您需要更改租户。</span><span class="sxs-lookup"><span data-stu-id="036cf-131">If you do not see the Concierge Subscription listed, you have multiple tenants enabled on your subscription, and you need to change tenants.</span></span> <span data-ttu-id="036cf-132">为此, 请使用以下门户链接再次登录:[用于沙盒的 Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="036cf-132">To do so, login again using the following portal link: [Azure portal for sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).</span></span>
    <span data-ttu-id="036cf-133">资源组</span><span class="sxs-lookup"><span data-stu-id="036cf-133">Resource Group</span></span>|<span data-ttu-id="036cf-134">使用现有</span><span class="sxs-lookup"><span data-stu-id="036cf-134">Use existing</span></span><br><br><span data-ttu-id="036cf-135"><rgn>[沙盒资源组名称]</rgn></span><span class="sxs-lookup"><span data-stu-id="036cf-135"><rgn>[sandbox resource group name]</rgn></span></span>|<span data-ttu-id="036cf-136">选择 "**使用现有**", 然后输入<rgn>[沙盒资源组名称]</rgn>。</span><span class="sxs-lookup"><span data-stu-id="036cf-136">Select **Use existing**, and then enter <rgn>[sandbox resource group name]</rgn>.</span></span>
    <span data-ttu-id="036cf-137">帐户名称</span><span class="sxs-lookup"><span data-stu-id="036cf-137">Account Name</span></span>|<span data-ttu-id="036cf-138">*输入一个唯一的名称*</span><span class="sxs-lookup"><span data-stu-id="036cf-138">*Enter a unique name*</span></span>|<span data-ttu-id="036cf-139">输入唯一名称以标识此 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="036cf-139">Enter a unique name to identify this Azure Cosmos DB account.</span></span> <span data-ttu-id="036cf-140">由于将*documents.azure.com*追加到您提供的用于创建 URI 的 ID, 因此请使用唯一但可识别的 id。</span><span class="sxs-lookup"><span data-stu-id="036cf-140">Because *documents.azure.com* is appended to the ID that you provide to create your URI, use a unique but identifiable ID.</span></span><br><br><span data-ttu-id="036cf-141">ID 只能包含小写字母、数字和连字符 (-) 字符, 并且必须包含3到31个字符。</span><span class="sxs-lookup"><span data-stu-id="036cf-141">The ID can contain only lowercase letters, numbers, and the hyphen (-) character, and it must contain 3 to 31 characters.</span></span>
    <span data-ttu-id="036cf-142">API</span><span class="sxs-lookup"><span data-stu-id="036cf-142">API</span></span>|<span data-ttu-id="036cf-143">SQL</span><span class="sxs-lookup"><span data-stu-id="036cf-143">SQL</span></span>|<span data-ttu-id="036cf-144">API 确定要创建的帐户类型。</span><span class="sxs-lookup"><span data-stu-id="036cf-144">The API determines the type of account to create.</span></span> <span data-ttu-id="036cf-145">Azure Cosmos DB 提供了五个 api 来满足您的应用程序需求: SQL (document database)、Gremlin (graph 数据库)、MongoDB (文档数据库)、Azure 表和 Cassandra, 每个用户都需要一个单独的帐户。</span><span class="sxs-lookup"><span data-stu-id="036cf-145">Azure Cosmos DB provides five APIs to suit the needs of your application: SQL (document database), Gremlin (graph database), MongoDB (document database), Azure Table, and Cassandra, each of which currently requires a separate account.</span></span> <br><br><span data-ttu-id="036cf-146">选择**SQL** , 因为在此模块中, 您要创建可使用 sql 语法查询且可通过 sql API 访问的文档数据库。</span><span class="sxs-lookup"><span data-stu-id="036cf-146">Select **SQL** because in this module you are creating a document database that is queryable using SQL syntax and accessible with the SQL API.</span></span>|
    <span data-ttu-id="036cf-147">位置</span><span class="sxs-lookup"><span data-stu-id="036cf-147">Location</span></span>|<span data-ttu-id="036cf-148">*选择最接近你的区域*</span><span class="sxs-lookup"><span data-stu-id="036cf-148">*Select the region closest to you*</span></span>|<span data-ttu-id="036cf-149">从上述区域列表中选择离你最近的地区。</span><span class="sxs-lookup"><span data-stu-id="036cf-149">Select the region closest to you from the list of regions above.</span></span>
    <span data-ttu-id="036cf-150">地域冗余</span><span class="sxs-lookup"><span data-stu-id="036cf-150">Geo-Redundancy</span></span>| <span data-ttu-id="036cf-151">启用</span><span class="sxs-lookup"><span data-stu-id="036cf-151">Disable</span></span> | <span data-ttu-id="036cf-152">此设置在第二个 (成对的) 区域中创建数据库的复制版本。</span><span class="sxs-lookup"><span data-stu-id="036cf-152">This setting creates a replicated version of your database in a second (paired) region.</span></span> <span data-ttu-id="036cf-153">将此设置保留为 "现在禁用", 因为稍后将对数据库进行复制。</span><span class="sxs-lookup"><span data-stu-id="036cf-153">Leave this set to disabled for now, as you will replicate the database later.</span></span>
    <span data-ttu-id="036cf-154">多区域写入</span><span class="sxs-lookup"><span data-stu-id="036cf-154">Multi-region Writes</span></span> | <span data-ttu-id="036cf-155">启用</span><span class="sxs-lookup"><span data-stu-id="036cf-155">Enable</span></span> | <span data-ttu-id="036cf-156">通过此设置, 您可以同时写入多个区域。</span><span class="sxs-lookup"><span data-stu-id="036cf-156">This setting enables you to write to multiple regions at the same time.</span></span> <span data-ttu-id="036cf-157">仅可在创建帐户过程中配置此设置。</span><span class="sxs-lookup"><span data-stu-id="036cf-157">This setting can only be configured during account creation.</span></span>

1. <span data-ttu-id="036cf-158">单击 "**审阅 + 创建**"。</span><span class="sxs-lookup"><span data-stu-id="036cf-158">Click **Review + Create**.</span></span>

    ![Azure Cosmos DB 的 "新建帐户" 页](../media/2-global-distribution/2-azure-cosmos-db-create-new-account.png)

1. <span data-ttu-id="036cf-160">验证设置后, 单击 "**创建**" 以创建帐户。</span><span class="sxs-lookup"><span data-stu-id="036cf-160">After the settings are validated, click **Create** to create the account.</span></span>

1. <span data-ttu-id="036cf-161">帐户创建需要几分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="036cf-161">The account creation takes a few minutes.</span></span> <span data-ttu-id="036cf-162">等待门户显示部署成功的通知并单击通知。</span><span class="sxs-lookup"><span data-stu-id="036cf-162">Wait for the portal to display the notification that the deployment succeeded and click the notification.</span></span>

    ![通知警报](../media/2-global-distribution/2-azure-cosmos-db-notification.png)

1. <span data-ttu-id="036cf-164">在通知窗口中, 单击 "**转到资源**"。</span><span class="sxs-lookup"><span data-stu-id="036cf-164">In the notification window, click **Go to resource**.</span></span>

    ![转到资源](../media/2-global-distribution/2-azure-cosmos-db-go-to-resource.png)

    <span data-ttu-id="036cf-166">门户将显示**恭喜!已创建 Azure Cosmos DB 帐户**页面。</span><span class="sxs-lookup"><span data-stu-id="036cf-166">The portal displays the **Congratulations! Your Azure Cosmos DB account was created** page.</span></span>

    ![Azure 门户通知窗格](../media/2-global-distribution/2-azure-cosmos-db-account-created.png)

## <a name="replicate-data-in-multiple-regions"></a><span data-ttu-id="036cf-168">复制多个区域中的数据</span><span class="sxs-lookup"><span data-stu-id="036cf-168">Replicate data in multiple regions</span></span>

<span data-ttu-id="036cf-169">现在, 让我们在洛杉矶、纽约和东京中复制离您最近的全局用户的数据库。</span><span class="sxs-lookup"><span data-stu-id="036cf-169">Let's now replicate your database closest to your global users in Los Angeles, New York, and Tokyo.</span></span>

1. <span data-ttu-id="036cf-170">在 "帐户" 页中, 单击菜单中的 "从**全局处复制数据**"。</span><span class="sxs-lookup"><span data-stu-id="036cf-170">In the account page, click **Replicate data globally** from the menu.</span></span>
1. <span data-ttu-id="036cf-171">在 "在**全局复制数据**" 页中, 选择 "美国西部 2"、"东 us" 和 "日本东部地区", 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="036cf-171">In the **Replicate data globally** page, select the West US 2, East US, and Japan East regions, and then click **Save**.</span></span>

    <span data-ttu-id="036cf-172">如果在 Azure 门户中看不到地图, 请将屏幕左侧的菜单最小化以显示它。</span><span class="sxs-lookup"><span data-stu-id="036cf-172">If you don't see the map in the Azure portal, minimize the menus of the left side of the screen to display it.</span></span>

    <span data-ttu-id="036cf-173">页面将在向新区域写入数据时显示**更新**消息。</span><span class="sxs-lookup"><span data-stu-id="036cf-173">The page will display an **Updating** message while the data is written to the new regions.</span></span> <span data-ttu-id="036cf-174">新区域中的数据将在30分钟内可用。</span><span class="sxs-lookup"><span data-stu-id="036cf-174">Data in the new regions will be available within 30 minutes.</span></span>

    ![单击地图中的区域以将其添加](../media/2-global-distribution/2-global-replication.gif)

## <a name="summary"></a><span data-ttu-id="036cf-176">摘要</span><span class="sxs-lookup"><span data-stu-id="036cf-176">Summary</span></span>

<span data-ttu-id="036cf-177">在此单元中, 您将数据库复制到您的用户最集中的世界区域, 从而为其提供对网站上数据的低延迟访问。</span><span class="sxs-lookup"><span data-stu-id="036cf-177">In this unit, you replicated your database to the regions of the world in which your users are most concentrated, providing them lower-latency access to the data on your site.</span></span>