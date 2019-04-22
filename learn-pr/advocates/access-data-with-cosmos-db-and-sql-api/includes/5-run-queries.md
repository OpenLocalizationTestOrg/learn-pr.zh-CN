<span data-ttu-id="a21ce-101">现在, 您已经了解了可以创建哪些类型的查询, 我们将使用 Azure 门户中的数据浏览器检索和筛选您的产品数据。</span><span class="sxs-lookup"><span data-stu-id="a21ce-101">Now that you've learned about what kinds of queries you can create, let's use the Data Explorer in the Azure portal to retrieve and filter your product data.</span></span>

<span data-ttu-id="a21ce-102">在 "数据浏览器" 窗口中, 请注意, 默认情况下, "**文档**" 选项`SELECT * FROM c`卡上的查询设置为, 如下图所示。</span><span class="sxs-lookup"><span data-stu-id="a21ce-102">In your Data Explorer window, note that by default, the query on the **Document** tab is set to `SELECT * FROM c` as shown in the following image.</span></span> <span data-ttu-id="a21ce-103">此默认查询检索并显示集合中的所有文档。</span><span class="sxs-lookup"><span data-stu-id="a21ce-103">This default query retrieves and displays all documents in the collection.</span></span>

![数据资源管理器中的默认查询是从 c 中选择 \*](../media/5-azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a><span data-ttu-id="a21ce-105">创建新查询</span><span class="sxs-lookup"><span data-stu-id="a21ce-105">Create a new query</span></span>

1. <span data-ttu-id="a21ce-106">在数据资源管理器中, 单击 "**新建 SQL 查询**"。</span><span class="sxs-lookup"><span data-stu-id="a21ce-106">In Data Explorer, click **New SQL Query**.</span></span> <span data-ttu-id="a21ce-107">请注意, "新建**查询 1** " 选项卡上的默认`SELECT * from c`查询再次返回, 这将返回集合中的所有文档。</span><span class="sxs-lookup"><span data-stu-id="a21ce-107">Note that the default query on the new  **Query 1** tab is again `SELECT * from c`, which will return all documents in the collection.</span></span> 

1. <span data-ttu-id="a21ce-108">单击 "**执行查询**"。</span><span class="sxs-lookup"><span data-stu-id="a21ce-108">Click **Execute Query**.</span></span> <span data-ttu-id="a21ce-109">此查询将返回数据库中的所有结果。</span><span class="sxs-lookup"><span data-stu-id="a21ce-109">This query returns all results in the database.</span></span>

    ![通过添加 ORDER by _ts DESC 并单击 "应用筛选器" 来更改默认查询](../media/5-azure-cosmosdb-data-explorer-edit-query.png)

2. <span data-ttu-id="a21ce-111">现在, 让我们运行在上一个设备中讨论的一些查询。</span><span class="sxs-lookup"><span data-stu-id="a21ce-111">Now, let's run some of the queries discussed in the previous unit.</span></span> <span data-ttu-id="a21ce-112">在 "查询" 选项卡`SELECT * from c`上, 删除、复制并粘贴以下查询, 然后单击 "**执行查询**":</span><span class="sxs-lookup"><span data-stu-id="a21ce-112">On the query tab, delete `SELECT * from c`, copy and paste the following query, and then click **Execute Query**:</span></span>

    ```sql
    SELECT * 
    FROM Products p 
    WHERE p.id ="1"
    ```

    <span data-ttu-id="a21ce-113">结果返回的产品的`productId`为1。</span><span class="sxs-lookup"><span data-stu-id="a21ce-113">The results return the product whose `productId` is 1.</span></span>

    ![id 为1的查询](../media/5-azure-cosmosdb-data-explorer-query-by-id.png)

3. <span data-ttu-id="a21ce-115">删除以前的查询, 复制并粘贴以下查询, 然后单击 "**执行查询**"。</span><span class="sxs-lookup"><span data-stu-id="a21ce-115">Delete the previous query, copy and paste the following query, and click **Execute Query**.</span></span> <span data-ttu-id="a21ce-116">此查询返回按价格以升序排序的所有产品的价格、说明和产品 ID。</span><span class="sxs-lookup"><span data-stu-id="a21ce-116">This query returns the price, description, and product ID for all products, ordered by price, in ascending order.</span></span>
 
    ```sql
    SELECT p.price, p.description, p.productId 
    FROM Products p 
    ORDER BY p.price ASC
    ```

## <a name="summary"></a><span data-ttu-id="a21ce-117">摘要</span><span class="sxs-lookup"><span data-stu-id="a21ce-117">Summary</span></span>

<span data-ttu-id="a21ce-118">现在, 您已对 Azure Cosmos DB 中的数据完成了一些基本查询。</span><span class="sxs-lookup"><span data-stu-id="a21ce-118">You have now completed some basic queries on your data in Azure Cosmos DB.</span></span> 