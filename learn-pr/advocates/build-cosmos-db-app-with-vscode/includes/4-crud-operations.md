<!--TODO: explain Etag in knowledge needed-->

<span data-ttu-id="2507a-101">建立与 Azure Cosmos DB 的连接后, 下一步是创建、读取、替换和删除存储在数据库中的文档。</span><span class="sxs-lookup"><span data-stu-id="2507a-101">Once the connection to Azure Cosmos DB has been made, the next step is to create, read, replace, and delete the documents that are stored in the database.</span></span> <span data-ttu-id="2507a-102">在此单元中, 您将在`WebCustomer`集合中创建用户文档。</span><span class="sxs-lookup"><span data-stu-id="2507a-102">In this unit, you will create User documents in your `WebCustomer` collection.</span></span> <span data-ttu-id="2507a-103">然后, 通过 ID 检索这些文件, 将其替换, 并将其删除。</span><span class="sxs-lookup"><span data-stu-id="2507a-103">Then, you'll retrieve them by ID, replace them, and delete them.</span></span>

## <a name="working-with-documents-programmatically"></a><span data-ttu-id="2507a-104">以编程方式使用文档</span><span class="sxs-lookup"><span data-stu-id="2507a-104">Working with documents programmatically</span></span>

<span data-ttu-id="2507a-105">数据存储在 Azure Cosmos DB 的 JSON 文档中。</span><span class="sxs-lookup"><span data-stu-id="2507a-105">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="2507a-106">可以在门户中创建、检索、替换或删除[文档](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents), 如前面的模块中所示, 或以编程方式进行, 如本模块中所述。</span><span class="sxs-lookup"><span data-stu-id="2507a-106">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="2507a-107">Azure Cosmos DB 为 .net、.net Core、Java、node.js 和 Python 提供了客户端 sdk, 每个提供程序都支持这些操作。</span><span class="sxs-lookup"><span data-stu-id="2507a-107">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="2507a-108">在本模块中, 我们将使用 .net Core SDK 对存储在 Azure Cosmos DB 中的 NoSQL 数据执行 CRUD (创建、检索、更新和删除) 操作。</span><span class="sxs-lookup"><span data-stu-id="2507a-108">In this module, we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations on the NoSQL data stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="2507a-109">Azure Cosmos DB 文档的主要操作是[DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)类的一部分:</span><span class="sxs-lookup"><span data-stu-id="2507a-109">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="2507a-110">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="2507a-110">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="2507a-111">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="2507a-111">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="2507a-112">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="2507a-112">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [<span data-ttu-id="2507a-113">UpsertDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="2507a-113">UpsertDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="2507a-114">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="2507a-114">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="2507a-115">Upsert 执行创建或替换操作, 具体取决于文档是否已存在。</span><span class="sxs-lookup"><span data-stu-id="2507a-115">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>

<span data-ttu-id="2507a-116">若要执行这些操作, 您需要创建一个表示存储在数据库中的对象的类。</span><span class="sxs-lookup"><span data-stu-id="2507a-116">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="2507a-117">由于我们使用的是用户数据库, 因此您需要创建一个**用户**类来存储主要数据, 如其名、姓和用户 id (这是必需的用于启用水平缩放的分区键) 和用于发货的类首选项和订单历史记录。</span><span class="sxs-lookup"><span data-stu-id="2507a-117">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their first name, last name, and user id (which is required, as that's the partition key to enable horizontal scaling) and classes for shipping preferences and order history.</span></span>

<span data-ttu-id="2507a-118">创建用于表示用户的这些类之后, 您将为每个实例创建新的用户文档, 然后将对这些文档执行一些基本的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="2507a-118">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some basic CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="2507a-119">创建文档</span><span class="sxs-lookup"><span data-stu-id="2507a-119">Create documents</span></span>

1. <span data-ttu-id="2507a-120">首先, 创建一个代表要存储在 Azure Cosmos DB 中的对象的**用户**类。</span><span class="sxs-lookup"><span data-stu-id="2507a-120">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="2507a-121">我们还将创建在**用户**中使用的**OrderHistory**和**ShippingPreference**类。</span><span class="sxs-lookup"><span data-stu-id="2507a-121">We will also create **OrderHistory** and **ShippingPreference** classes that are used within **User**.</span></span> <span data-ttu-id="2507a-122">请注意, 文档必须将**Id**属性序列化为 JSON 中的**id** 。</span><span class="sxs-lookup"><span data-stu-id="2507a-122">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span>

    <span data-ttu-id="2507a-123">若要创建这些类, 请在**BasicOperations**方法下复制并粘贴以下**用户**、 **OrderHistory**和**ShippingPreference**类。</span><span class="sxs-lookup"><span data-stu-id="2507a-123">To create these classes, copy and paste the following **User**, **OrderHistory**, and **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

    ```csharp
    public class User
    {
        [JsonProperty("id")]
        public string Id { get; set; }
        [JsonProperty("userId")]
        public string UserId { get; set; }
        [JsonProperty("lastName")]
        public string LastName { get; set; }
        [JsonProperty("firstName")]
        public string FirstName { get; set; }
        [JsonProperty("email")]
        public string Email { get; set; }
        [JsonProperty("dividend")]
        public string Dividend { get; set; }
        [JsonProperty("OrderHistory")]
        public OrderHistory[] OrderHistory { get; set; }
        [JsonProperty("ShippingPreference")]
        public ShippingPreference[] ShippingPreference { get; set; }
        [JsonProperty("CouponsUsed")]
        public CouponsUsed[] Coupons { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class OrderHistory
    {
        public string OrderId { get; set; }
        public string DateShipped { get; set; }
        public string Total { get; set; }
    }

    public class ShippingPreference
    {
        public int Priority { get; set; }
        public string AddressLine1 { get; set; }
        public string AddressLine2 { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string ZipCode { get; set; }
        public string Country { get; set; }
    }

    public class CouponsUsed
    {
        public string CouponCode { get; set; }

    }

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. <span data-ttu-id="2507a-124">在集成终端中, 键入以下命令以运行程序以确保其运行。</span><span class="sxs-lookup"><span data-stu-id="2507a-124">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="2507a-125">现在, 将**CreateUserDocumentIfNotExists**任务复制并粘贴到 Program.cs 文件末尾的**WriteToConsoleAndPromptToContinue**方法下。</span><span class="sxs-lookup"><span data-stu-id="2507a-125">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **WriteToConsoleAndPromptToContinue** method at the end of the Program.cs file.</span></span>

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("User {0} already exists in the database", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="2507a-126">然后, 返回到**BasicOperations**方法, 并将以下项添加到该方法的末尾。</span><span class="sxs-lookup"><span data-stu-id="2507a-126">Then, return to the **BasicOperations** method and add the following to the end of that method.</span></span>

    ```csharp
    User yanhe = new User
    {
        Id = "1",
        UserId = "yanhe",
        LastName = "He",
        FirstName = "Yan",
        Email = "yanhe@contoso.com",
        OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
            ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);

    User nelapin = new User
    {
        Id = "2",
        UserId = "nelapin",
        LastName = "Pindakova",
        FirstName = "Nela",
        Email = "nelapin@contoso.com",
        Dividend = "8.50",
        OrderHistory = new OrderHistory[]
        {
            new OrderHistory {
                OrderId = "1001",
                DateShipped = "08/17/2018",
                Total = "105.89"
            }
        },
         ShippingPreference = new ShippingPreference[]
        {
            new ShippingPreference {
                    Priority = 1,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            },
            new ShippingPreference {
                    Priority = 2,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            }
        },
        Coupons = new CouponsUsed[]
        {
            new CouponsUsed{
                CouponCode = "Fall2018"
            }
        }
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

1. <span data-ttu-id="2507a-127">在集成终端中, 键入以下命令以运行该程序。</span><span class="sxs-lookup"><span data-stu-id="2507a-127">In the integrated terminal, again, type the following command to run the program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="2507a-128">当应用程序创建每个新的用户文档时, 终端将显示输出。</span><span class="sxs-lookup"><span data-stu-id="2507a-128">The terminal will display output as the application creates each new user document.</span></span> <span data-ttu-id="2507a-129">按任意键完成该程序。</span><span class="sxs-lookup"><span data-stu-id="2507a-129">Press any key to complete the program.</span></span>

    ```output
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="2507a-130">阅读文档</span><span class="sxs-lookup"><span data-stu-id="2507a-130">Read documents</span></span>

1. <span data-ttu-id="2507a-131">若要从数据库读取文档, 请复制以下代码, 并将其放在 Program.cs 文件中的**WriteToConsoleAndPromptToContinue**方法后面。</span><span class="sxs-lookup"><span data-stu-id="2507a-131">To read documents from the database, copy in the following code and place after the **WriteToConsoleAndPromptToContinue** method in the Program.cs file.</span></span>

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("Read user {0}", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not read", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="2507a-132">将以下代码复制并粘贴到**BasicOperations**方法的末尾, 在`await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`该行后面。</span><span class="sxs-lookup"><span data-stu-id="2507a-132">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="2507a-133">在集成终端中, 键入以下命令以运行该程序。</span><span class="sxs-lookup"><span data-stu-id="2507a-133">In the integrated terminal, type the following command to run the program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="2507a-134">终端显示以下输出, 其中输出 "读取用户 1" 表示已检索文档。</span><span class="sxs-lookup"><span data-stu-id="2507a-134">The terminal displays the following output, where the output "Read user 1" indicates the document was retrieved.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a><span data-ttu-id="2507a-135">替换文档</span><span class="sxs-lookup"><span data-stu-id="2507a-135">Replace documents</span></span>

<span data-ttu-id="2507a-136">Azure Cosmos DB 支持替换 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="2507a-136">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="2507a-137">在这种情况下, 我们将更新用户记录以考虑其姓氏的更改。</span><span class="sxs-lookup"><span data-stu-id="2507a-137">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="2507a-138">将**ReplaceUserDocument**方法复制并粘贴到 Program.cs 文件中的**ReadUserDocument**方法之后。</span><span class="sxs-lookup"><span data-stu-id="2507a-138">Copy and paste the **ReplaceUserDocument** method after the **ReadUserDocument** method in the Program.cs file.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) });
            this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser.LastName);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for replacement", updatedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="2507a-139">将以下代码复制并粘贴到**BasicOperations**方法的末尾, 在`await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`该行后面。</span><span class="sxs-lookup"><span data-stu-id="2507a-139">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="2507a-140">在集成终端中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="2507a-140">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```
    <span data-ttu-id="2507a-141">终端显示以下输出, 其中输出 "替换了 Suh 的姓" 表示文档已被替换。</span><span class="sxs-lookup"><span data-stu-id="2507a-141">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a><span data-ttu-id="2507a-142">删除文档</span><span class="sxs-lookup"><span data-stu-id="2507a-142">Delete documents</span></span>

1. <span data-ttu-id="2507a-143">将**DeleteUserDocument**方法复制并粘贴到**ReplaceUserDocument**方法的下面。</span><span class="sxs-lookup"><span data-stu-id="2507a-143">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>

    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, User deletedUser)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, deletedUser.Id), new RequestOptions { PartitionKey = new PartitionKey(deletedUser.UserId) });
            Console.WriteLine("Deleted user {0}", deletedUser.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for deletion", deletedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="2507a-144">将以下代码复制并粘贴到**BasicOperations**方法的末尾。</span><span class="sxs-lookup"><span data-stu-id="2507a-144">Copy and paste the following code in the end of the **BasicOperations** method.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="2507a-145">在集成终端中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="2507a-145">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="2507a-146">终端显示以下输出, 其中输出 "Deleted user 1" 表示文档已被删除。</span><span class="sxs-lookup"><span data-stu-id="2507a-146">The terminal displays the following output, where the output "Deleted user 1" indicates the document was deleted.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    Deleted user 1
    End of demo, press any key to exit.
    ```

<span data-ttu-id="2507a-147">在此单位中, 您在 Azure Cosmos DB 数据库中创建、替换和删除了文档。</span><span class="sxs-lookup"><span data-stu-id="2507a-147">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>
