使用 Visual Studio Code, 可以通过使用集成终端和几个短命令来创建控制台应用程序。

在此单元中, 将使用集成终端创建一个基本控制台应用程序, 从扩展检索 Azure Cosmos DB 连接字符串, 然后配置从应用程序到 Azure Cosmos DB 的连接。

## <a name="create-a-console-app"></a>创建控制台应用程序

1. 在 Visual Studio Code 中, 选择 "**文件** > **打开文件夹**"。

1. 在所选位置创建`learning-module`一个名为的新文件夹, 然后单击 "**选择文件夹**"。

1. 通过单击 "文件" 菜单并选中 "**自动保存**" (如果为空), 确保已启用文件自动保存。 您将在几个代码块中进行复制, 这将确保您始终对文件的最新编辑进行操作。

1. 从 "主" 菜单中选择 "**查看** > **终端**", 从 Visual Studio Code 中打开集成的终端。

1. 在终端窗口中, 复制并粘贴以下命令。

    ```bash
    dotnet new console
    ```

    此命令将在文件夹中创建一个已写入基本 "Hello World" 程序的**Program.cs**文件, 以及一个名为**learning-module**的 c # 项目文件。

1. 在终端窗口中, 复制并粘贴以下命令, 以运行 "Hello World" 程序。

    ```bash
    dotnet run
    ```

    终端窗口显示 "Hello world!" 作为输出。

## <a name="connect-the-app-to-azure-cosmos-db"></a>将应用连接到 Azure Cosmos DB

1. 在终端提示符处, 复制并粘贴以下命令块以安装所需的 NuGet 包。

    ```bash
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package System.Configuration.ConfigurationManager
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet restore
    ```

1. 在资源管理器窗格顶部, 单击 " **Program.cs** " 以打开该文件。

1. 在后面`using System;`添加以下 using 语句。

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

    如果您收到有关添加所需缺少资产的消息, 请单击 **"是"**。

1. 在`learning-module`文件夹中创建一个名为 app.config 的新文件, 并添加以下代码。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. 若要复制连接字符串, 请![单击左侧](../media/2-setup/visual-studio-code-explorer-icon.png)的 azure 图标 azure 图标, 展开您的 Concierge 订阅, 右键单击新的 Azure Cosmos DB 帐户, 然后单击 "**复制连接字符串**"。

1. 将连接字符串粘贴到 app.config 文件的末尾, 然后将**AccountEndpoint**部分从连接字符串复制到 app.config 中的**AccountEndpoint**值中。

    **accountEndpoint**应类似于以下内容:

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. 现在, 将**AccountKey**值从连接字符串复制到**AccountKey**值中, 然后删除您在中复制的原始连接字符串。

    最终的 app.config 文件看起来类似于这样。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="https://my-account.documents.azure.com:443/" />
            <add key="accountKey" value="6e7sRxunccGEeO7IVlMdeFt5BdsllfSGLYc28KyjzkESiCu7tfWbTaZXAErt2v88gOcMbOYgwp1q4NYDifD7ew==" />
          </appSettings>
    </configuration>
    ```

1. 在终端提示符处, 复制并粘贴以下命令以运行该程序。

    ```bash
    dotnet run
    ```

    该程序显示 Hello World! 在终端中。

## <a name="create-the-documentclient"></a>创建 DocumentClient

现在是时候创建的`DocumentClient`实例, 即 Azure Cosmos DB 服务的客户端表示形式。 此客户端用于配置和执行对服务的请求。

1. 在 Program.cs 中, 将以下项添加到`Program`类的开头。

    ```csharp
    private DocumentClient client;
    ```

1. 添加新的异步任务以创建新的客户端, 并通过在**** `Main`方法后面添加以下方法来检查用户数据库是否存在。

    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. 在集成终端中, 复制并粘贴以下命令, 以运行程序以确保其运行。

    ```bash
    dotnet run
    ```

1. 将以下代码复制并粘贴到**Main**方法中, 并覆盖当前`Console.WriteLine("Hello World!");`行。

    ```csharp
    try
    {
        Program p = new Program();
        p.BasicOperations().Wait();
    }
    catch (DocumentClientException de)
    {
        Exception baseException = de.GetBaseException();
        Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
    }
    catch (Exception e)
    {
        Exception baseException = e.GetBaseException();
        Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
    }
    finally
    {
        Console.WriteLine("End of demo, press any key to exit.");
        Console.ReadKey();
    }
    ```

1. 在集成终端中, 键入以下命令以运行程序以确保其运行。

    ```bash
    dotnet run
    ```

    控制台显示以下输出。

    ```output
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

在此单元中, 您为 Azure Cosmos DB 应用程序设置了基础。 您在 Visual Studio Code 中设置开发环境, 创建了一个基本的 "Hello World" 项目, 将项目连接到 Azure Cosmos DB 终结点, 并确保存在您的数据库和集合。
