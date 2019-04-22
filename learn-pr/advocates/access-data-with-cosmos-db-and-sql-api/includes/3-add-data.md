<span data-ttu-id="de34a-101">将数据添加到你的 Azure Cosmos DB 数据库非常简单。</span><span class="sxs-lookup"><span data-stu-id="de34a-101">Adding data to your Azure Cosmos DB database is simple.</span></span> <span data-ttu-id="de34a-102">您打开 Azure 门户, 导航到您的数据库, 并使用数据资源管理器将 JSON 文档添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="de34a-102">You open the Azure portal, navigate to your database, and use the Data Explorer to add JSON documents to the database.</span></span> <span data-ttu-id="de34a-103">有更高级的添加数据的方法, 但我们将从这里开始, 因为数据浏览器是一个很好的工具, 可让你熟悉 Azure Cosmos DB 提供的内部工作原理和功能。</span><span class="sxs-lookup"><span data-stu-id="de34a-103">There are more advanced ways to add data, but we'll start here because the Data Explorer is a great tool to get you acquainted with the inner workings and functionality provided by Azure Cosmos DB.</span></span>

## <a name="what-is-the-data-explorer"></a><span data-ttu-id="de34a-104">数据浏览器是什么？</span><span class="sxs-lookup"><span data-stu-id="de34a-104">What is the Data Explorer?</span></span>
<span data-ttu-id="de34a-105">azure Cosmos DB 数据浏览器是 azure 门户中包含的一个工具, 用于管理 azure Cosmos DB 中存储的数据。</span><span class="sxs-lookup"><span data-stu-id="de34a-105">The Azure Cosmos DB Data Explorer is a tool included in the Azure portal that is used to manage data stored in an Azure Cosmos DB.</span></span> <span data-ttu-id="de34a-106">它提供了用于查看和导航数据集合的 UI, 以及用于编辑数据库中的文档、查询数据以及创建和运行存储过程的 UI。</span><span class="sxs-lookup"><span data-stu-id="de34a-106">It provides a UI for viewing and navigating data collections, as well as for editing documents within the database, querying data, and creating and running stored procedures.</span></span>

## <a name="add-data-using-the-data-explorer"></a><span data-ttu-id="de34a-107">使用数据资源管理器添加数据</span><span class="sxs-lookup"><span data-stu-id="de34a-107">Add data using the Data Explorer</span></span>

1. <span data-ttu-id="de34a-108">使用与激活沙盒时相同的帐户登录到[沙盒的 Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="de34a-108">Sign into the [Azure portal for sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="de34a-109">使用相同的帐户登录到 Azure 门户和沙盒。</span><span class="sxs-lookup"><span data-stu-id="de34a-109">Login to the Azure portal and the sandbox with the same account.</span></span>
    >
    > <span data-ttu-id="de34a-110">使用上面的链接登录到 Azure 门户, 以确保您已连接到沙盒, 该沙箱提供对 Concierge 订阅的访问权限。</span><span class="sxs-lookup"><span data-stu-id="de34a-110">Login to the Azure portal using the link above to ensure you are connected to the sandbox, which provides access to a Concierge Subscription.</span></span>

1. <span data-ttu-id="de34a-111">单击 "**所有服务** > **数据库** > " "**Azure Cosmos DB**"。</span><span class="sxs-lookup"><span data-stu-id="de34a-111">Click **All services** > **Databases** > **Azure Cosmos DB**.</span></span> <span data-ttu-id="de34a-112">然后选择您的帐户, 单击 "**数据资源管理器**", 然后单击 "以**全屏打开**"。</span><span class="sxs-lookup"><span data-stu-id="de34a-112">Then select your account, click **Data Explorer**, and then click **Open Full Screen**.</span></span>

   ![在 Azure 门户中的数据资源管理器中创建新文档](../media/3-azure-cosmosdb-data-explorer-full-screen.png)

2. <span data-ttu-id="de34a-114">在 "**打开**全屏显示" 框中, 单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="de34a-114">In the **Open Full Screen** box, click **Open**.</span></span>

    <span data-ttu-id="de34a-115">web 浏览器将显示新的全屏数据浏览器, 这将为您提供更多空间和用于处理数据库的专用环境。</span><span class="sxs-lookup"><span data-stu-id="de34a-115">The web browser displays the new full-screen Data Explorer, which gives you more space and a dedicated environment for working with your database.</span></span>

3. <span data-ttu-id="de34a-116">若要创建新的 JSON 文档, 请在 "SQL API" 窗格中, 展开 "**衣服**", 单击 "**文档**", 然后单击 "**新建文档**"。</span><span class="sxs-lookup"><span data-stu-id="de34a-116">To create a new JSON document, in the SQL API pane, expand **Clothing**, click **Documents**, then click **New Document**.</span></span>

   ![在 Azure 门户中的数据资源管理器中创建新文档](../media/3-azure-cosmosdb-data-explorer-new-document.png)

4. <span data-ttu-id="de34a-118">现在, 使用以下结构将文档添加到集合中。</span><span class="sxs-lookup"><span data-stu-id="de34a-118">Now, add a document to the collection with the following structure.</span></span> <span data-ttu-id="de34a-119">只需将以下代码复制并粘贴到 "**文档**" 选项卡中, 即可覆盖当前内容:</span><span class="sxs-lookup"><span data-stu-id="de34a-119">Just copy and paste the following code into the **Documents** tab, overwriting the current content:</span></span>

     ```json
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
    }
     ```

5. <span data-ttu-id="de34a-120">将 JSON 添加到 "**文档**" 选项卡后, 单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="de34a-120">Once you've added the JSON to the **Documents** tab, click **Save**.</span></span>

    ![在 Azure 门户中复制 JSON 数据并单击 "在数据资源管理器中保存"](../media/3-azure-cosmosdb-data-explorer-save-document.png)

6. <span data-ttu-id="de34a-122">再次创建并保存一个文档, 再次单击 "**新建文档**", 并将以下 JSON 对象复制到 "数据资源管理器" 中, 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="de34a-122">Create and save one more document clicking **New Document** again, and copying the following JSON object into Data Explorer and clicking **Save**.</span></span>

     ```json
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "price": "49.99",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
           }
        }
    }
     ```

7. <span data-ttu-id="de34a-123">单击左侧菜单上的 "**文档**", 确认已保存文档。</span><span class="sxs-lookup"><span data-stu-id="de34a-123">Confirm the documents have been saved by clicking **Documents** on the left-hand menu.</span></span>

    <span data-ttu-id="de34a-124">"数据资源管理器" 在 "**文档**" 选项卡中显示两个文档。</span><span class="sxs-lookup"><span data-stu-id="de34a-124">Data Explorer displays the two documents in the **Documents** tab.</span></span>

<span data-ttu-id="de34a-125">在此单位中, 您将使用数据浏览器将两个文档 (每个文档都表示产品目录中的产品) 添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="de34a-125">In this unit, you added two documents, each representing a product in your product catalog, to your database by using the Data Explorer.</span></span> <span data-ttu-id="de34a-126">数据浏览器是创建文档、修改文档以及开始使用 Azure Cosmos DB 的好方法。</span><span class="sxs-lookup"><span data-stu-id="de34a-126">The Data Explorer is a good way to create documents, modify documents, and get started with Azure Cosmos DB.</span></span>
