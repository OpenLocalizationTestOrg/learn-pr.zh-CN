<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)-->
<span data-ttu-id="042dd-101">现在, 你已在应用程序中创建文档, 让我们从你的应用程序中查询它们。</span><span class="sxs-lookup"><span data-stu-id="042dd-101">Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="042dd-102">Azure Cosmos DB 使用 SQL 查询和 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="042dd-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="042dd-103">此单元重点介绍如何从应用程序 (而不是门户) 运行 SQL 查询和 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="042dd-103">This unit focuses on running SQL queries and LINQ queries from your application, as opposed to the portal.</span></span>

<span data-ttu-id="042dd-104">我们将使用你为在线零售商应用程序创建的用户文档来测试这些查询。</span><span class="sxs-lookup"><span data-stu-id="042dd-104">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="042dd-105">LINQ 查询基础知识</span><span class="sxs-lookup"><span data-stu-id="042dd-105">LINQ query basics</span></span>

<span data-ttu-id="042dd-106">LINQ 是一种 .net 编程模型, 用于将计算表示为对象流上的查询。</span><span class="sxs-lookup"><span data-stu-id="042dd-106">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="042dd-107">您可以创建一个将 LINQ 查询转换为 Cosmos db 查询的**IQueryable**对象, 该对象将直接查询 Azure Cosmos db。</span><span class="sxs-lookup"><span data-stu-id="042dd-107">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="042dd-108">然后, 将该查询传递到 Azure Cosmos DB 服务器以检索 JSON 格式的结果集。</span><span class="sxs-lookup"><span data-stu-id="042dd-108">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="042dd-109">返回的结果将被反序列化为客户端上的 .net 对象流。</span><span class="sxs-lookup"><span data-stu-id="042dd-109">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="042dd-110">许多开发人员喜欢 LINQ 查询, 因为它们提供了在应用程序代码中处理对象的方式以及它们如何表示在数据库中运行的查询逻辑的单一一致编程模型。</span><span class="sxs-lookup"><span data-stu-id="042dd-110">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="042dd-111">下表显示了如何将 LINQ 查询转换为 SQL。</span><span class="sxs-lookup"><span data-stu-id="042dd-111">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="042dd-112">LINQ 表达式</span><span class="sxs-lookup"><span data-stu-id="042dd-112">LINQ expression</span></span> | <span data-ttu-id="042dd-113">SQL 转换</span><span class="sxs-lookup"><span data-stu-id="042dd-113">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="042dd-114">运行 SQL 和 LINQ 查询</span><span class="sxs-lookup"><span data-stu-id="042dd-114">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="042dd-115">下面的示例演示如何在 .net 代码中执行 SQL、linq 或 linq lambda 中的查询。</span><span class="sxs-lookup"><span data-stu-id="042dd-115">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="042dd-116">复制代码并将其添加到 Program.cs 文件的末尾。</span><span class="sxs-lookup"><span data-stu-id="042dd-116">Copy the code and add it to the end of the Program.cs file.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1, EnableCrossPartitionQuery = true };

        // Here we find nelapin via their LastName
        IQueryable<User> userQuery = this.client.CreateDocumentQuery<User>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(u => u.LastName == "Pindakova");

        // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (User user in userQuery)
        {
            Console.WriteLine("\tRead {0}", user);
        }

        // Now execute the same query via direct SQL
        IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM User WHERE User.lastName = 'Pindakova'", queryOptions );

        Console.WriteLine("Running direct SQL query...");
        foreach (User user in userQueryInSql)
        {
                Console.WriteLine("\tRead {0}", user);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. <span data-ttu-id="042dd-117">将以下代码复制并粘贴到您\*\*\*\* 的`await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` BasicOperations 方法中, 在该行之前。</span><span class="sxs-lookup"><span data-stu-id="042dd-117">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. <span data-ttu-id="042dd-118">在集成终端中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="042dd-118">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="042dd-119">控制台显示 LINQ 和 SQL 查询的输出。</span><span class="sxs-lookup"><span data-stu-id="042dd-119">The console displays the output of the LINQ and SQL queries.</span></span>

<span data-ttu-id="042dd-120">在此单位中, 您了解了 linq 查询, 然后向应用程序添加了 linq 和 SQL 查询以检索用户记录。</span><span class="sxs-lookup"><span data-stu-id="042dd-120">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>
