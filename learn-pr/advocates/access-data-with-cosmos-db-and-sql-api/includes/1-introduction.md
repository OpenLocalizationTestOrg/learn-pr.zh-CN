<span data-ttu-id="bcd38-101">在数据库中添加数据和查询数据应简单明了。</span><span class="sxs-lookup"><span data-stu-id="bcd38-101">Adding data and querying data in your database should be straightforward.</span></span> 

<span data-ttu-id="bcd38-102">假设您为在线衣服零售商工作, 您需要在 Azure Cosmos DB 中向电子商务数据库添加库存数据。</span><span class="sxs-lookup"><span data-stu-id="bcd38-102">Imagine you work for an online clothing retailer and you need to add inventory data to your e-commerce database in Azure Cosmos DB.</span></span> <span data-ttu-id="bcd38-103">一旦数据在数据库中, 就可以使用熟悉的 sql 查询 (是, 就像 sql Server 中使用的查询一样), 并使用存储过程和用户定义的函数 (udf) 执行复杂的操作, 从而查询数据。</span><span class="sxs-lookup"><span data-stu-id="bcd38-103">Once the data is in the database, you can query it by using familiar SQL queries (yes, just like the ones you use in SQL Server) and perform complex operations by using stored procedures and user-defined functions (UDFs).</span></span>

<span data-ttu-id="bcd38-104">azure Cosmos DB 在 azure 门户中提供了一个数据资源管理器, 可用于执行所有这些操作: 添加数据、修改数据以及创建和运行存储过程。</span><span class="sxs-lookup"><span data-stu-id="bcd38-104">Azure Cosmos DB provides a Data Explorer in the Azure portal that you can use to perform all these operations: adding data, modifying data, and creating and running stored procedures.</span></span> <span data-ttu-id="bcd38-105">数据浏览器可在 Azure 门户中使用, 也可在独立 web 浏览器中使用, 从而提供额外的空间来处理数据。</span><span class="sxs-lookup"><span data-stu-id="bcd38-105">The Data Explorer can be used in the Azure portal or it can be undocked and used in a standalone web browser, providing additional space to work with your data.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="bcd38-106">学习目标</span><span class="sxs-lookup"><span data-stu-id="bcd38-106">Learning objectives</span></span>

<span data-ttu-id="bcd38-107">在本模块中, 您将:</span><span class="sxs-lookup"><span data-stu-id="bcd38-107">In this module, you will:</span></span>

- <span data-ttu-id="bcd38-108">在数据资源管理器中创建产品目录文档</span><span class="sxs-lookup"><span data-stu-id="bcd38-108">Create product catalog documents in the Data Explorer</span></span>
- <span data-ttu-id="bcd38-109">执行 Azure Cosmos DB 查询</span><span class="sxs-lookup"><span data-stu-id="bcd38-109">Perform Azure Cosmos DB queries</span></span>
- <span data-ttu-id="bcd38-110">使用存储过程创建和运行文档上的操作</span><span class="sxs-lookup"><span data-stu-id="bcd38-110">Create and run operations on your documents by using stored procedures</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcd38-111">先决条件</span><span class="sxs-lookup"><span data-stu-id="bcd38-111">Prerequisites</span></span>

- <span data-ttu-id="bcd38-112">了解数据库和查询</span><span class="sxs-lookup"><span data-stu-id="bcd38-112">Have an understanding of databases and queries</span></span>
