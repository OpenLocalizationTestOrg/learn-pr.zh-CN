<!--TODO: explain Etag in knowledge needed-->

建立与 Azure Cosmos DB 的连接后, 下一步是创建、读取、替换和删除存储在数据库中的文档。 在此单元中, 您将在`WebCustomer`集合中创建用户文档。 然后, 通过 ID 检索这些文件, 将其替换, 并将其删除。

## <a name="working-with-documents-programmatically"></a>以编程方式使用文档

数据存储在 Azure Cosmos DB 的 JSON 文档中。 可以在门户中创建、检索、替换或删除[文档](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents), 如前面的模块中所示, 或以编程方式进行, 如本模块中所述。 Azure Cosmos DB 为 .net、.net Core、Java、node.js 和 Python 提供了客户端 sdk, 每个提供程序都支持这些操作。 在本模块中, 我们将使用 .net Core SDK 对存储在 Azure Cosmos DB 中的 NoSQL 数据执行 CRUD (创建、检索、更新和删除) 操作。

Azure Cosmos DB 文档的主要操作是[DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)类的一部分:
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet)
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Upsert 执行创建或替换操作, 具体取决于文档是否已存在。

若要执行这些操作, 您需要创建一个表示存储在数据库中的对象的类。 由于我们使用的是用户数据库, 因此您需要创建一个**用户**类来存储主要数据, 如其名、姓和用户 id (这是必需的用于启用水平缩放的分区键) 和用于发货的类首选项和订单历史记录。

创建用于表示用户的这些类之后, 您将为每个实例创建新的用户文档, 然后将对这些文档执行一些基本的 CRUD 操作。

## <a name="create-documents"></a>创建文档

1. 首先, 创建一个代表要存储在 Azure Cosmos DB 中的对象的**用户**类。 我们还将创建在**用户**中使用的**OrderHistory**和**ShippingPreference**类。 请注意, 文档必须将**Id**属性序列化为 JSON 中的**id** 。

    若要创建这些类, 请在**BasicOperations**方法下复制并粘贴以下**用户**、 **OrderHistory**和**ShippingPreference**类。

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

1. 在集成终端中, 键入以下命令以运行程序以确保其运行。

    ```bash
    dotnet run
    ```

1. 现在, 将**CreateUserDocumentIfNotExists**任务复制并粘贴到 Program.cs 文件末尾的**WriteToConsoleAndPromptToContinue**方法下。

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

1. 然后, 返回到**BasicOperations**方法, 并将以下项添加到该方法的末尾。

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

1. 在集成终端中, 键入以下命令以运行该程序。

    ```bash
    dotnet run
    ```

    当应用程序创建每个新的用户文档时, 终端将显示输出。 按任意键完成该程序。

    ```output
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>阅读文档

1. 若要从数据库读取文档, 请复制以下代码, 并将其放在 Program.cs 文件中的**WriteToConsoleAndPromptToContinue**方法后面。

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

1. 将以下代码复制并粘贴到**BasicOperations**方法的末尾, 在`await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`该行后面。

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中, 键入以下命令以运行该程序。

    ```bash
    dotnet run
    ```

    终端显示以下输出, 其中输出 "读取用户 1" 表示已检索文档。

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

## <a name="replace-documents"></a>替换文档

Azure Cosmos DB 支持替换 JSON 文档。 在这种情况下, 我们将更新用户记录以考虑其姓氏的更改。

1. 将**ReplaceUserDocument**方法复制并粘贴到 Program.cs 文件中的**ReadUserDocument**方法之后。

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

1. 将以下代码复制并粘贴到**BasicOperations**方法的末尾, 在`await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`该行后面。

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中, 运行以下命令。

    ```bash
    dotnet run
    ```
    终端显示以下输出, 其中输出 "替换了 Suh 的姓" 表示文档已被替换。

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

## <a name="delete-documents"></a>删除文档

1. 将**DeleteUserDocument**方法复制并粘贴到**ReplaceUserDocument**方法的下面。

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

1. 将以下代码复制并粘贴到**BasicOperations**方法的末尾。

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中, 运行以下命令。

    ```bash
    dotnet run
    ```

    终端显示以下输出, 其中输出 "Deleted user 1" 表示文档已被删除。

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

在此单位中, 您在 Azure Cosmos DB 数据库中创建、替换和删除了文档。
