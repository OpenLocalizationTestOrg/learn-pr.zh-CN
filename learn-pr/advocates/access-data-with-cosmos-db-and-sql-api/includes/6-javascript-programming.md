<span data-ttu-id="0dcff-101">数据库中的多个文档经常需要同时更新。</span><span class="sxs-lookup"><span data-stu-id="0dcff-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> 

<span data-ttu-id="0dcff-102">对于您的在线零售版应用程序, 当用户下订单并想要使用优惠券代码、信用卡或被除数 (或同时是这三个) 时, 您需要为这些选项查询其帐户, 并对其帐户进行更新以表明他们使用了这些选项。、更新订单总计和处理订单。</span><span class="sxs-lookup"><span data-stu-id="0dcff-102">For your online retail application, when a user places an order and wants to use a coupon code, a credit, or a dividend (or all three at once), you need to query their account for those options, make updates to their account indicating they used them, update the order total, and process the order.</span></span>

<span data-ttu-id="0dcff-103">所有这些操作都需要在一个事务中同时发生。</span><span class="sxs-lookup"><span data-stu-id="0dcff-103">All of these actions need to happen at the same time, within a single transaction.</span></span> <span data-ttu-id="0dcff-104">如果用户选择取消订单, 您希望回滚更改而不修改其帐户信息, 以便他们的优惠券代码、片尾和红利可用于下一次购买。</span><span class="sxs-lookup"><span data-stu-id="0dcff-104">If the user chooses to cancel the order, you want to roll back the changes and not modify their account information, so that their coupon codes, credits, and dividends are available for their next purchase.</span></span>

<span data-ttu-id="0dcff-105">在 Azure Cosmos DB 中执行这些事务的方法是使用存储过程和用户定义的函数 (udf)。</span><span class="sxs-lookup"><span data-stu-id="0dcff-105">The way to perform these transactions in Azure Cosmos DB is by using stored procedures and user-defined functions (UDFs).</span></span> <span data-ttu-id="0dcff-106">存储过程是确保 ACID (原子性、一致性、隔离、持久性) 事务的唯一方法, 因为它们在服务器上运行, 因而称为服务器端编程。</span><span class="sxs-lookup"><span data-stu-id="0dcff-106">Stored procedures are the only way to ensure ACID (Atomicity, Consistency, Isolation, Durability) transactions because they are run on the server, and are thus referred to as server-side programming.</span></span> <span data-ttu-id="0dcff-107">udf 也存储在服务器上, 并在查询过程中用于对值或文档中的文档执行计算逻辑。</span><span class="sxs-lookup"><span data-stu-id="0dcff-107">UDFs are also stored on the server and are used during queries to perform computational logic on values or documents within the query.</span></span> 

<span data-ttu-id="0dcff-108">在本模块中, 你将了解存储过程和 udf, 然后在门户中运行一些。</span><span class="sxs-lookup"><span data-stu-id="0dcff-108">In this module, you'll learn about stored procedures and UDFs, and then run some in the portal.</span></span>

## <a name="stored-procedure-basics"></a><span data-ttu-id="0dcff-109">存储过程基础知识</span><span class="sxs-lookup"><span data-stu-id="0dcff-109">Stored procedure basics</span></span>

<span data-ttu-id="0dcff-110">存储过程对文档和属性执行复杂的事务。</span><span class="sxs-lookup"><span data-stu-id="0dcff-110">Stored procedures perform complex transactions on documents and properties.</span></span> <span data-ttu-id="0dcff-111">存储过程是在 JavaScript 中编写的, 并存储在 Azure Cosmos DB 上的集合中。</span><span class="sxs-lookup"><span data-stu-id="0dcff-111">Stored procedures are written in JavaScript and are stored in a collection on Azure Cosmos DB.</span></span> <span data-ttu-id="0dcff-112">通过对数据库引擎执行存储过程并接近数据, 可以提高客户端编程的性能。</span><span class="sxs-lookup"><span data-stu-id="0dcff-112">By performing the stored procedures on the database engine and close to the data, you can improve performance over client-side programming.</span></span>

<span data-ttu-id="0dcff-113">存储过程是在 Azure Cosmos DB 中实现原子事务的唯一方法;客户端 sdk 不支持事务。</span><span class="sxs-lookup"><span data-stu-id="0dcff-113">Stored procedures are the only way to achieve atomic transactions within Azure Cosmos DB; the client-side SDKs do not support transactions.</span></span>

<span data-ttu-id="0dcff-114">此外, 建议在存储过程中执行批处理操作, 因为减少了创建单独的事务的必要性。</span><span class="sxs-lookup"><span data-stu-id="0dcff-114">Performing batch operations in stored procedures is also recommended because of the reduced need to create separate transactions.</span></span>

## <a name="stored-procedure-example"></a><span data-ttu-id="0dcff-115">存储过程示例</span><span class="sxs-lookup"><span data-stu-id="0dcff-115">Stored procedure example</span></span>

<span data-ttu-id="0dcff-116">下面的示例是一个简单的 HelloWorld 存储过程, 它可获取当前上下文并发送显示 "Hello, World" 的响应。</span><span class="sxs-lookup"><span data-stu-id="0dcff-116">The following sample is a simple HelloWorld stored procedure that gets the current context and sends a response that displays "Hello, World".</span></span>

```javascript
function helloWorld() {
    var context = getContext();
    var response = context.getResponse();

    response.setBody("Hello, World");
}
```

## <a name="user-defined-function-basics"></a><span data-ttu-id="0dcff-117">用户定义的函数基础知识</span><span class="sxs-lookup"><span data-stu-id="0dcff-117">User-defined function basics</span></span>

<span data-ttu-id="0dcff-118">udf 用于扩展 Azure Cosmos DB SQL 查询语言语法, 并实现自定义业务逻辑, 例如对属性和文档的计算。</span><span class="sxs-lookup"><span data-stu-id="0dcff-118">UDFs are used to extend the Azure Cosmos DB SQL query language grammar and implement custom business logic, such as calculations on properties and documents.</span></span> <span data-ttu-id="0dcff-119">udf 只能在内部查询中调用, 与存储过程不同, 它们不具有对 context 对象的访问权限, 因此它们无法读取或写入文档。</span><span class="sxs-lookup"><span data-stu-id="0dcff-119">UDFs can be called only from inside queries and, unlike stored procedures, they do not have access to the context object, so they cannot read or write documents.</span></span>

<span data-ttu-id="0dcff-120">在在线商务方案中, UDF 可用于确定要应用于订单总计或应用于产品或订单的折扣百分比的增值税。</span><span class="sxs-lookup"><span data-stu-id="0dcff-120">In an online commerce scenario, a UDF could be used to determine the sales tax to apply to an order total or a percentage discount to apply to products or orders.</span></span>

## <a name="user-defined-function-example"></a><span data-ttu-id="0dcff-121">用户定义的函数示例</span><span class="sxs-lookup"><span data-stu-id="0dcff-121">User-defined function example</span></span>

<span data-ttu-id="0dcff-122">下面的示例创建 UDF 以根据产品成本计算虚构公司产品中的税:</span><span class="sxs-lookup"><span data-stu-id="0dcff-122">The following sample creates a UDF to calculate tax on a product in a fictitious company based the product cost:</span></span>

```javascript
function producttax(price) {
    if (price == undefined) 
        throw 'no input';

    var amount = parseFloat(price);

    if (amount < 1000) 
        return amount * 0.1;
    else if (amount < 10000) 
        return amount * 0.2;
    else
        return amount * 0.4;
}
```

## <a name="create-a-stored-procedure-in-the-portal"></a><span data-ttu-id="0dcff-123">在门户中创建存储过程</span><span class="sxs-lookup"><span data-stu-id="0dcff-123">Create a stored procedure in the portal</span></span>

<span data-ttu-id="0dcff-124">让我们在门户中创建一个新的存储过程。</span><span class="sxs-lookup"><span data-stu-id="0dcff-124">Let's create a new stored procedure in the portal.</span></span> <span data-ttu-id="0dcff-125">门户将自动填充一个简单的存储过程, 用于检索集合中的第一个项目, 因此我们首先运行此存储过程。</span><span class="sxs-lookup"><span data-stu-id="0dcff-125">The portal automatically populates a simple stored procedure that retrieves the first item in the collection, so we'll run this stored procedure first.</span></span>

1. <span data-ttu-id="0dcff-126">在 "数据浏览器" 中, 单击 "**新建存储过程**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-126">In the Data Explorer, click **New Stored Procedure**.</span></span>

    <span data-ttu-id="0dcff-127">数据资源管理器显示带有示例存储过程的新选项卡。</span><span class="sxs-lookup"><span data-stu-id="0dcff-127">Data Explorer displays a new tab with a sample stored procedure.</span></span>

2. <span data-ttu-id="0dcff-128">在 "**存储过程 Id** " 框中, 输入名称*示例*, 单击 "**保存**", 然后单击 "**执行**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-128">In the **Stored Procedure Id** box, enter the name *sample*, click **Save**, and then click **Execute**.</span></span>


3. <span data-ttu-id="0dcff-129">在 "**输入参数**" 框中, 键入分区键的名称*33218896*, 然后单击 "**执行**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-129">In the **Input parameters** box, type the name of a partition key, *33218896*, and then click **Execute**.</span></span> <span data-ttu-id="0dcff-130">请注意, 存储过程在单个分区中工作。</span><span class="sxs-lookup"><span data-stu-id="0dcff-130">Note that stored procedures work within a single partition.</span></span>

    ![在门户中运行存储过程](../media/6-stored-procedure.gif)

    <span data-ttu-id="0dcff-132">**结果**窗格将显示集合中第一个文档的源。</span><span class="sxs-lookup"><span data-stu-id="0dcff-132">The **Result** pane displays the feed from the first document in the collection.</span></span>

## <a name="create-a-stored-procedure-that-creates-documents"></a><span data-ttu-id="0dcff-133">创建创建文档的存储过程</span><span class="sxs-lookup"><span data-stu-id="0dcff-133">Create a stored procedure that creates documents</span></span>

<span data-ttu-id="0dcff-134">现在, 让我们创建一个创建文档的存储过程。</span><span class="sxs-lookup"><span data-stu-id="0dcff-134">Now, let's create a stored procedure that creates documents.</span></span>

1. <span data-ttu-id="0dcff-135">在 "数据浏览器" 中, 单击 "**新建存储过程**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-135">In the Data Explorer, click **New Stored Procedure**.</span></span> <span data-ttu-id="0dcff-136">将此存储过程命名为*createMyDocument*, 将以下代码复制并粘贴到**存储过程正文**框中, 单击 "**保存**", 然后单击 "**执行**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-136">Name this stored procedure *createMyDocument*, copy and paste the following code into the **Stored Procedure Body** box, click **Save**, and then click **Execute**.</span></span>

    ```javascript
    function createMyDocument() {
        var context = getContext();
        var collection = context.getCollection();

        var doc = {
            "id": "3",
            "productId": "33218898",
            "description": "Contoso microfleece zip-up jacket",
            "price": "44.99"
        };

        var accepted = collection.createDocument(collection.getSelfLink(),
            doc,
            function (err, documentCreated) {
                if (err) throw new Error('Error' + err.message);
                context.getResponse().setBody(documentCreated)
            });
        if (!accepted) return;
    }
    ```

2. <span data-ttu-id="0dcff-137">在 "输入参数" 框中, 输入分区项值*33218898*, 然后单击 "**执行**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-137">In the Input parameters box, enter a Partition Key Value of *33218898*, and then click **Execute**.</span></span>

    <span data-ttu-id="0dcff-138">数据资源管理器将在结果区域中显示新创建的文档。</span><span class="sxs-lookup"><span data-stu-id="0dcff-138">Data Explorer displays the newly created document in the Result area.</span></span>

    <span data-ttu-id="0dcff-139">您可以返回到 "文档" 选项卡, 单击 "**刷新**" 按钮, 然后查看新文档。</span><span class="sxs-lookup"><span data-stu-id="0dcff-139">You can go back to the Documents tab, click the **Refresh** button and see the new document.</span></span> 

## <a name="create-a-user-defined-function"></a><span data-ttu-id="0dcff-140">创建用户定义函数</span><span class="sxs-lookup"><span data-stu-id="0dcff-140">Create a user-defined function</span></span>

<span data-ttu-id="0dcff-141">现在, 让我们在数据资源管理器中创建一个 UDF。</span><span class="sxs-lookup"><span data-stu-id="0dcff-141">Now, let's create a UDF in Data Explorer.</span></span>

<span data-ttu-id="0dcff-142">在 "数据浏览器" 中, 单击 "**新建 UDF**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-142">In the Data Explorer, click **New UDF**.</span></span> <span data-ttu-id="0dcff-143">您可能需要单击 "**新建存储 Prodedure** " 旁边的向下箭头以查看**新的 UDF**。</span><span class="sxs-lookup"><span data-stu-id="0dcff-143">You may need to click the down arrow next to **New Stored Prodedure** to see **New UDF**.</span></span> <span data-ttu-id="0dcff-144">将下面的代码复制到窗口中, 命名 UDF *producttax*, 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="0dcff-144">Copy the following code into the window, name the UDF *producttax*, and then click **Save**.</span></span>

```javascript
function producttax(price) {
    if (price == undefined) 
        throw 'no input';

    var amount = parseFloat(price);

    if (amount < 1000) 
        return amount * 0.1;
    else if (amount < 10000) 
        return amount * 0.2;
    else
        return amount * 0.4;
}
```

<span data-ttu-id="0dcff-145">定义 UDF 后, 转到 "**查询 1** " 选项卡, 并将以下查询复制并粘贴到查询区域中, 以运行 UDF。</span><span class="sxs-lookup"><span data-stu-id="0dcff-145">Once you have defined the UDF, go to the **Query 1** tab and copy and paste the following query into the query area to run the UDF.</span></span>

```sql
SELECT c.id, c.productId, c.price, udf.producttax(c.price) AS producttax FROM c
```
