<span data-ttu-id="fb12b-101">让我们创建一个客户端应用程序以使用队列。</span><span class="sxs-lookup"><span data-stu-id="fb12b-101">Let's create a client application to work with a queue.</span></span> <span data-ttu-id="fb12b-102">然后, 将我们的连接字符串添加到代码中。</span><span class="sxs-lookup"><span data-stu-id="fb12b-102">Then we'll add our connection string to the code.</span></span>

> [!NOTE]
> <span data-ttu-id="fb12b-103">如果已安装 .net Core, 或者直接在云命令行管理器环境中, 则可以在本地计算机上创建客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="fb12b-103">You can create the client application on your local computer if you have .NET Core installed, or directly in the Cloud Shell environment.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="fb12b-104">创建应用程序</span><span class="sxs-lookup"><span data-stu-id="fb12b-104">Create the application</span></span>

<span data-ttu-id="fb12b-105">我们将创建可在 Linux、macOS 或 Windows 上运行的 .net Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fb12b-105">We'll create a .NET Core application that you can run on Linux, macOS, or Windows.</span></span> <span data-ttu-id="fb12b-106">让我们将其命名为**QueueApp**。</span><span class="sxs-lookup"><span data-stu-id="fb12b-106">Let's name it **QueueApp**.</span></span> <span data-ttu-id="fb12b-107">为简单起见, 我们将使用单个应用程序, 该应用将通过我们的队列发送和接收邮件。</span><span class="sxs-lookup"><span data-stu-id="fb12b-107">For simplicity, we'll use a single app that will both send and receive messages through our queue.</span></span>

1. <span data-ttu-id="fb12b-108">使用`dotnet new`命令创建名称为 " **QueueApp**" 的新控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="fb12b-108">Use the `dotnet new` command to create a new console app with the name **QueueApp**.</span></span> <span data-ttu-id="fb12b-109">您可以将命令键入到右侧的云命令行管理程序中, 或者如果您正在本地运行, 请在终端/控制台窗口中键入命令。</span><span class="sxs-lookup"><span data-stu-id="fb12b-109">You can type commands into the Cloud Shell on the right, or if you are working locally, in a terminal/console window.</span></span> <span data-ttu-id="fb12b-110">此命令将创建一个包含单个源文件的简单应用程序`Program.cs`:。</span><span class="sxs-lookup"><span data-stu-id="fb12b-110">This command creates a simple app with a single source file: `Program.cs`.</span></span>

    ```azurecli
    dotnet new console -n QueueApp
    ```

1. <span data-ttu-id="fb12b-111">切换到新创建`QueueApp`的文件夹, 并生成应用程序以验证是否一切正常。</span><span class="sxs-lookup"><span data-stu-id="fb12b-111">Switch to the newly created `QueueApp` folder and build the app to verify that all is well.</span></span>

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a><span data-ttu-id="fb12b-112">获取您的连接字符串</span><span class="sxs-lookup"><span data-stu-id="fb12b-112">Get your connection string</span></span>

<span data-ttu-id="fb12b-113">请记住, 您的连接字符串在您的存储帐户的 "Azure 门户**设置 > 访问密钥**" 部分中可用。</span><span class="sxs-lookup"><span data-stu-id="fb12b-113">Recall that your connection string is available in the Azure portal **Settings > Access keys** section of your storage account.</span></span>

<span data-ttu-id="fb12b-114">您还可以通过 Azure CLI 或 PowerShell 工具进行检索。</span><span class="sxs-lookup"><span data-stu-id="fb12b-114">You can also retrieve it through the Azure CLI or PowerShell tools.</span></span> <span data-ttu-id="fb12b-115">让我们使用 Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="fb12b-115">Let's use the Azure CLI command.</span></span> <span data-ttu-id="fb12b-116">请记住, 将`<name>`替换为您创建的存储帐户的特定名称。</span><span class="sxs-lookup"><span data-stu-id="fb12b-116">Remember to replace the `<name>` with the specific name of the storage account you created.</span></span> <span data-ttu-id="fb12b-117">如果需要提醒`az storage account list` , 可以使用。</span><span class="sxs-lookup"><span data-stu-id="fb12b-117">You can use `az storage account list` if you need a reminder.</span></span>

```azurecli
az storage account show-connection-string --name <name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="fb12b-118">此命令将使用您的连接字符串返回一个 JSON 块。</span><span class="sxs-lookup"><span data-stu-id="fb12b-118">This command will return a JSON block with your connection string.</span></span> <span data-ttu-id="fb12b-119">它将包括存储帐户名称和帐户密钥:</span><span class="sxs-lookup"><span data-stu-id="fb12b-119">It will include the storage account name and the account key:</span></span>

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a><span data-ttu-id="fb12b-120">将连接字符串添加到应用程序</span><span class="sxs-lookup"><span data-stu-id="fb12b-120">Add the connection string to the application</span></span>

<span data-ttu-id="fb12b-121">最后, 让我们将连接字符串添加到我们的应用程序中, 以便它可以访问存储帐户。</span><span class="sxs-lookup"><span data-stu-id="fb12b-121">Finally, let's add the connection string into our app so it can access the storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="fb12b-122">为简单起见, 您将在**Program.cs**文件中放置连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fb12b-122">For simplicity, you will place the connection string in the **Program.cs** file.</span></span> <span data-ttu-id="fb12b-123">在生产应用程序中, 应将其存储在安全位置。</span><span class="sxs-lookup"><span data-stu-id="fb12b-123">In a production application, you should store it in a secure location.</span></span> <span data-ttu-id="fb12b-124">对于服务器端使用, 我们建议使用 Azure Key Vault。</span><span class="sxs-lookup"><span data-stu-id="fb12b-124">For server side use, we recommend using Azure Key Vault.</span></span>

1. <span data-ttu-id="fb12b-125">在`code .` "终端" 中键入以打开 "联机代码编辑器"。</span><span class="sxs-lookup"><span data-stu-id="fb12b-125">Type `code .` in the terminal to open the online code editor.</span></span> <span data-ttu-id="fb12b-126">或者, 如果您自己处理自己的工作, 则可以使用您选择的 IDE。</span><span class="sxs-lookup"><span data-stu-id="fb12b-126">Alternatively, if you are working on your own you can use the IDE of your choice.</span></span> <span data-ttu-id="fb12b-127">建议使用 Visual Studio Code, 这是一种优秀的跨平台 IDE。</span><span class="sxs-lookup"><span data-stu-id="fb12b-127">We recommend Visual Studio Code, which is an excellent cross-platform IDE.</span></span>

1. <span data-ttu-id="fb12b-128">打开项目`Program.cs`中的源文件。</span><span class="sxs-lookup"><span data-stu-id="fb12b-128">Open the `Program.cs` source file in the project.</span></span>

1. <span data-ttu-id="fb12b-129">在`Program`类中, 添加一个`const string`值以保存连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fb12b-129">In the `Program` class, add a `const string` value to hold the connection string.</span></span> <span data-ttu-id="fb12b-130">您只需要此值 (它以文本**DefaultEndpointsProtocol**开头)。</span><span class="sxs-lookup"><span data-stu-id="fb12b-130">You only need the value (it starts with the text **DefaultEndpointsProtocol**).</span></span>

1. <span data-ttu-id="fb12b-131">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="fb12b-131">Save the file.</span></span> <span data-ttu-id="fb12b-132">您可以单击椭圆 "..."在云编辑器的右下角, 或使用加速器键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> , macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="fb12b-132">You can click the ellipse "..." in the right corner of the cloud editor, or use the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

<span data-ttu-id="fb12b-133">代码应类似于以下内容 (字符串值对您的帐户是唯一的)。</span><span class="sxs-lookup"><span data-stu-id="fb12b-133">Your code should look something like this (the string value will be unique to your account).</span></span>

```csharp
...
namespace QueueApp
{
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https; ...";
        
        ...
    }
}
```

<span data-ttu-id="fb12b-134">至此, 我们已提供了此初学者项目设置, 我们来看看如何在代码中使用队列。</span><span class="sxs-lookup"><span data-stu-id="fb12b-134">Now that we have this starter project setup, let's look at how to work with a queue in code.</span></span> <span data-ttu-id="fb12b-135">所有这些都是从_邮件_开始。</span><span class="sxs-lookup"><span data-stu-id="fb12b-135">It all starts with _messages_.</span></span>