<span data-ttu-id="8bafc-101">使用 Visual Studio Code, 可以通过使用集成终端和几个短命令来创建控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="8bafc-101">Visual Studio Code enables you to create a console application by using the integrated terminal and a few short commands.</span></span>

<span data-ttu-id="8bafc-102">在此单元中, 将使用集成终端创建一个基本控制台应用程序, 从扩展检索 Azure Cosmos DB 连接字符串, 然后配置从应用程序到 Azure Cosmos DB 的连接。</span><span class="sxs-lookup"><span data-stu-id="8bafc-102">In this unit, you will create a basic console app using the integrated terminal, retrieve your Azure Cosmos DB connection string from the extension, and then configure the connection from your application to Azure Cosmos DB.</span></span>

## <a name="create-a-console-app"></a><span data-ttu-id="8bafc-103">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="8bafc-103">Create a console app</span></span>

1. <span data-ttu-id="8bafc-104">在 Visual Studio Code 中, 选择 "**文件** > **打开文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="8bafc-104">In Visual Studio Code, select **File** > **Open Folder**.</span></span>

1. <span data-ttu-id="8bafc-105">在所选位置创建`learning-module`一个名为的新文件夹, 然后单击 "**选择文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="8bafc-105">Create a new folder named `learning-module` in the location of your choice, and then click **Select Folder**.</span></span>

1. <span data-ttu-id="8bafc-106">通过单击 "文件" 菜单并选中 "**自动保存**" (如果为空), 确保已启用文件自动保存。</span><span class="sxs-lookup"><span data-stu-id="8bafc-106">Ensure that file auto-save is enabled by clicking on the File menu and checking **Auto Save** if it is blank.</span></span> <span data-ttu-id="8bafc-107">您将在几个代码块中进行复制, 这将确保您始终对文件的最新编辑进行操作。</span><span class="sxs-lookup"><span data-stu-id="8bafc-107">You will be copying in several blocks of code, and this will ensure you are always operating against the latest edits of your files.</span></span>

1. <span data-ttu-id="8bafc-108">从 "主" 菜单中选择 "**查看** > **终端**", 从 Visual Studio Code 中打开集成的终端。</span><span class="sxs-lookup"><span data-stu-id="8bafc-108">Open the integrated terminal from Visual Studio Code by selecting **View** > **Terminal** from the main menu.</span></span>

1. <span data-ttu-id="8bafc-109">在终端窗口中, 复制并粘贴以下命令。</span><span class="sxs-lookup"><span data-stu-id="8bafc-109">In the terminal window, copy and paste the following command.</span></span>

    ```bash
    dotnet new console
    ```

    <span data-ttu-id="8bafc-110">此命令将在文件夹中创建一个已写入基本 "Hello World" 程序的**Program.cs**文件, 以及一个名为**learning-module**的 c # 项目文件。</span><span class="sxs-lookup"><span data-stu-id="8bafc-110">This command creates a **Program.cs** file in your folder with a basic "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

1. <span data-ttu-id="8bafc-111">在终端窗口中, 复制并粘贴以下命令, 以运行 "Hello World" 程序。</span><span class="sxs-lookup"><span data-stu-id="8bafc-111">In the terminal window, copy and paste the following command to run the "Hello World" program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="8bafc-112">终端窗口显示 "Hello world!"</span><span class="sxs-lookup"><span data-stu-id="8bafc-112">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="8bafc-113">作为输出。</span><span class="sxs-lookup"><span data-stu-id="8bafc-113">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="8bafc-114">将应用连接到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8bafc-114">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="8bafc-115">在终端提示符处, 复制并粘贴以下命令块以安装所需的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="8bafc-115">At the terminal prompt, copy and paste the following command block to install the required NuGet packages.</span></span>

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

1. <span data-ttu-id="8bafc-116">在资源管理器窗格顶部, 单击 " **Program.cs** " 以打开该文件。</span><span class="sxs-lookup"><span data-stu-id="8bafc-116">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

1. <span data-ttu-id="8bafc-117">在后面`using System;`添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="8bafc-117">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

    <span data-ttu-id="8bafc-118">如果您收到有关添加所需缺少资产的消息, 请单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="8bafc-118">If you get a message about adding required missing assets, click **Yes**.</span></span>

1. <span data-ttu-id="8bafc-119">在`learning-module`文件夹中创建一个名为 app.config 的新文件, 并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="8bafc-119">Create a new file named App.config in the `learning-module` folder, and add the following code.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. <span data-ttu-id="8bafc-120">若要复制连接字符串, 请![单击左侧](../media/2-setup/visual-studio-code-explorer-icon.png)的 azure 图标 azure 图标, 展开您的 Concierge 订阅, 右键单击新的 Azure Cosmos DB 帐户, 然后单击 "**复制连接字符串**"。</span><span class="sxs-lookup"><span data-stu-id="8bafc-120">Copy your connection string by clicking the ![Azure icon](../media/2-setup/visual-studio-code-explorer-icon.png) Azure icon on the left, expanding your Concierge Subscription, right-clicking your new Azure Cosmos DB account, and then clicking **Copy Connection String**.</span></span>

1. <span data-ttu-id="8bafc-121">将连接字符串粘贴到 app.config 文件的末尾, 然后将**AccountEndpoint**部分从连接字符串复制到 app.config 中的**AccountEndpoint**值中。</span><span class="sxs-lookup"><span data-stu-id="8bafc-121">Paste the connection string into the end of the App.config file, and then copy the **AccountEndpoint** portion from the connection string into the **accountEndpoint** value in App.config.</span></span>

    <span data-ttu-id="8bafc-122">**accountEndpoint**应类似于以下内容:</span><span class="sxs-lookup"><span data-stu-id="8bafc-122">The **accountEndpoint** should look like the following:</span></span>

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. <span data-ttu-id="8bafc-123">现在, 将**AccountKey**值从连接字符串复制到**AccountKey**值中, 然后删除您在中复制的原始连接字符串。</span><span class="sxs-lookup"><span data-stu-id="8bafc-123">Now copy the **AccountKey** value from the connection string into the **accountKey** value, and then delete the original connection string you copied in.</span></span>

    <span data-ttu-id="8bafc-124">最终的 app.config 文件看起来类似于这样。</span><span class="sxs-lookup"><span data-stu-id="8bafc-124">Your final App.config file looks similar to this.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="https://my-account.documents.azure.com:443/" />
            <add key="accountKey" value="6e7sRxunccGEeO7IVlMdeFt5BdsllfSGLYc28KyjzkESiCu7tfWbTaZXAErt2v88gOcMbOYgwp1q4NYDifD7ew==" />
          </appSettings>
    </configuration>
    ```

1. <span data-ttu-id="8bafc-125">在终端提示符处, 复制并粘贴以下命令以运行该程序。</span><span class="sxs-lookup"><span data-stu-id="8bafc-125">At the terminal prompt, copy and paste the following command to run the program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="8bafc-126">该程序显示 Hello World!</span><span class="sxs-lookup"><span data-stu-id="8bafc-126">The program displays Hello World!</span></span> <span data-ttu-id="8bafc-127">在终端中。</span><span class="sxs-lookup"><span data-stu-id="8bafc-127">in the terminal.</span></span>

## <a name="create-the-documentclient"></a><span data-ttu-id="8bafc-128">创建 DocumentClient</span><span class="sxs-lookup"><span data-stu-id="8bafc-128">Create the DocumentClient</span></span>

<span data-ttu-id="8bafc-129">现在是时候创建的`DocumentClient`实例, 即 Azure Cosmos DB 服务的客户端表示形式。</span><span class="sxs-lookup"><span data-stu-id="8bafc-129">Now it's time to create an instance of the `DocumentClient`, which is the client-side representation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="8bafc-130">此客户端用于配置和执行对服务的请求。</span><span class="sxs-lookup"><span data-stu-id="8bafc-130">This client is used to configure and execute requests against the service.</span></span>

1. <span data-ttu-id="8bafc-131">在 Program.cs 中, 将以下项添加到`Program`类的开头。</span><span class="sxs-lookup"><span data-stu-id="8bafc-131">In Program.cs, add the following to the beginning of the `Program` class.</span></span>

    ```csharp
    private DocumentClient client;
    ```

1. <span data-ttu-id="8bafc-132">添加新的异步任务以创建新的客户端, 并通过在\*\*\*\* `Main`方法后面添加以下方法来检查用户数据库是否存在。</span><span class="sxs-lookup"><span data-stu-id="8bafc-132">Add a new asynchronous task to create a new client, and check whether the **Users** database exists by adding the following method after the `Main` method.</span></span>

    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. <span data-ttu-id="8bafc-133">在集成终端中, 复制并粘贴以下命令, 以运行程序以确保其运行。</span><span class="sxs-lookup"><span data-stu-id="8bafc-133">In the integrated terminal, again, copy and paste the following command to run the program to ensure it runs.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="8bafc-134">将以下代码复制并粘贴到**Main**方法中, 并覆盖当前`Console.WriteLine("Hello World!");`行。</span><span class="sxs-lookup"><span data-stu-id="8bafc-134">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

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

1. <span data-ttu-id="8bafc-135">在集成终端中, 键入以下命令以运行程序以确保其运行。</span><span class="sxs-lookup"><span data-stu-id="8bafc-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="8bafc-136">控制台显示以下输出。</span><span class="sxs-lookup"><span data-stu-id="8bafc-136">The console displays the following output.</span></span>

    ```output
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

<span data-ttu-id="8bafc-137">在此单元中, 您为 Azure Cosmos DB 应用程序设置了基础。</span><span class="sxs-lookup"><span data-stu-id="8bafc-137">In this unit, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="8bafc-138">您在 Visual Studio Code 中设置开发环境, 创建了一个基本的 "Hello World" 项目, 将项目连接到 Azure Cosmos DB 终结点, 并确保存在您的数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="8bafc-138">You set up your development environment in Visual Studio Code, created a basic "Hello World" project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>
