现在, 已准备好所有要求, 您可以编写代码来创建新的存储队列并添加邮件。 我们通常会将此代码放在生成数据的前端应用中。

## <a name="add-the-client-library-for-azure-storage"></a>为 Azure 存储添加客户端库

首先, 我们将**Azure 存储客户端库**添加到我们的应用中的 .net。 可以使用 NuGet (.net 程序包管理器) 来安装它。 

1. 使用`dotnet add package`命令`WindowsAzure.Storage`将包安装到项目中。 您可以在 "终端" 窗口中的云命令行管理程序_下_执行此操作, 如果您正在本地计算机上运行, 则可以在项目所在的同一个文件夹中的终端/控制台窗口中执行此操作。

```azurecli
dotnet add package WindowsAzure.Storage
```

## <a name="add-a-method-to-send-a-news-alert"></a>添加用于发送新闻通知的方法

接下来, 创建一个新方法, 将新闻报道发送到队列中。

1. 在代码`Program.cs`编辑器中打开该文件。

1. 在文件顶部, 添加以下命名空间。 我们将使用这两个类型的类型连接到 Azure 存储, 然后使用队列。

    - `System.Threading.Tasks`
    - `Microsoft.WindowsAzure.Storage`
    - `Microsoft.WindowsAzure.Storage.Queue`

1. 在`Program`名为`SendArticleAsync`的类中创建一个静态方法, `string`该方法采用`Task`a 并返回。 我们将使用此方法向我们的服务发送新闻文章。 将输入参数`newsMessage`命名为如下所示。

    ```csharp
    ...
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Queue; 
    
    class Program
    {
        ...
    
        static async Task SendArticleAsync(string newsMessage)
        {
        }
    }
    ```
    
1. 在您的新方法中, 使用`CloudStorageAccount.Parse`静态方法分析连接字符串 (回想我们将其放入常量字符串中)。 此方法返回一个`CloudStorageAccount`需要存储在变量中的对象。

1. 对存储`CreateCloudQueueClient()`帐户对象调用方法, 以获取客户端对象并将其存储在变量中。

1. 接下来, `GetQueueReference`对客户端对象调用方法, 并为队列名称传递字符串 "newsqueue"。 这将`CloudQueue`返回可用于处理队列的对象。 如果队列尚不存在, 则它是正常的。

1. 对`CreateIfNotExistsAsync()` `CloudQueue`对象的调用, 以确保队列已准备好使用。 这将创建队列 (如有必要)。
    - 由于这是一种异步方法, 因此请`await`使用 c # 关键字以确保我们能与它一起正常工作。 这也意味着需要使用`async`关键字修饰_方法_。 
    - `CreateIfNotExistsAsync`返回一个`bool`值, 如果队列`true`已创建且已存在, `false`则为。 如果创建了队列, 则将消息输出到控制台。
    - 下面是一个示例, 如果你需要一些帮助。

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        // Not Shown here - code from prior steps
        ...
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    }
    ```

1. 创建的`CloudQueueMessage`实例。 
    - 它采用`string`参数, 并在方法参数 (`newsMessage`) 中传递。 这将是邮件的_正文_。 还有一个名为的静态方法, 可以创建二进制邮件有效负载。

1. 对`AddMessageAsync`要将`CloudQueue`邮件添加到队列中的对象的调用。 这也是一种异步方法, 您需要使用`await`关键字来确保我们能与它进行正确的交互。

1. 保存文件, 并通过在命令窗口`dotnet build`中键入内容生成它。 修复所有错误, 可以使用以下代码检查工作。

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    
        CloudQueue queue = queueClient.GetQueueReference("newsqueue");
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    
        CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
        await queue.AddMessageAsync(articleMessage);
    }
    ```

## <a name="add-code-to-send-a-message"></a>添加代码以发送邮件

让我们修改`Main`方法以将接收到的任何参数传递到新方法, 以便我们可以测试新的 send 方法。

1. 查找`Main`方法。

1. 检查传递`args`的参数以查看是否有任何数据传递到了命令行。 如果是这样, `String.Join`请使用空格作为分隔符, 以创建单个字符串中的所有单词。

1. 将其传递给新`SendArticleAsync`方法。 

1. 返回后, 使用`Console.WriteLine`它输出我们发送的消息。

1. 保存文件并生成程序 (`dotnet build`), 可以使用下面的代码检查您的工作。

    > [!NOTE]
    > 由于我们的方法在技术上是异步的, 因此我们`await`需要使用关键字, 但是, 除非您使用`Main`的是 c # 7.1 或更高版本, 否则该功能在方法中不可用。 只需`Wait()`调用方法以实际阻止正在等待的方法返回, 我们将在一分钟内修复。

    ```csharp
    static void Main(string[] args)
    {
        if (args.Length > 0)
        {
            string value = String.Join(" ", args);
            SendArticleAsync(value).Wait();
            Console.WriteLine($"Sent: {value}");
        }
    }
    ```

## <a name="execute-the-application"></a>执行应用程序

应用程序现在可以发送邮件。 若要对其进行测试, 可以使用`dotnet run`命令从命令行运行它。 任何其他字符串都作为参数传递给应用程序。 

> [!WARNING]
> 在生成和运行程序之前, 请确保已将所有文件保存在联机编辑器中。

例如, 您可以键入:

```azurecli
dotnet run Send this message
```

这应将字符串`"Send this message"`添加到队列中。

## <a name="check-your-results"></a>检查结果

您可以使用**存储资源管理器**检查 Azure 门户中的队列, 如果您打开该产品, 它将允许您浏览每个存储帐户中的数据。

或者, 也可以使用 Azure CLI 或 PowerShell。 在命令行管理程序中尝试此命令`<connection-string>` , 将值替换为您的特定连接字符串:

```azurecli
az storage message peek --queue-name newsqueue --connection-string <connection-string> 
```

这将转储邮件的信息, 如下所示:

```json
[
  {
    "content": "U2VuZCB0aGlzIG1lc3NhZ2U=",
    "dequeueCount": 0,
    "expirationTime": "2018-09-05T02:43:40+00:00",
    "id": "b47cbe9f-a246-4a81-86ae-fa02ea8d98bc",
    "insertionTime": "2018-09-24T02:43:40+00:00",
    "popReceipt": null,
    "timeNextVisible": null
  }
]
```

还可以使用其他几个命令来尝试使用工具-同时`az storage queue --help`签出和`az storage message --help`浏览这些命令。

> [!TIP]
> 将您的连接字符串值放在名`AZURE_STORAGE_CONNECTION_STRING`为的环境变量中, 让您不必`--connection-string`每次都键入参数!

## <a name="optional---use-the-async-versions-of-the-methods"></a>可选-使用方法的异步版本

我们在`Wait()`上面的 send 方法中使用, 但这并不是我们的计算资源的有效使用。 相反, 我们需要使用 c # `async`和`await`方法。 但是, 我们需要_至少_使用 c # 7.1, 才能将这些关键字应用到**主**方法。

### <a name="switch-to-c-71"></a>切换到 c # 7。1

在 c `async` # `await` 7.1 之前, c # 和关键字在**Main**方法中不是有效的关键字。 我们可以通过 **.csproj**文件中的标志轻松切换到该编译器。

1. 在编辑器中打开**QueueApp**文件。

1. 在`<LangVersion>7.1</LangVersion>`生成文件中`PropertyGroup`添加到第一个中。 完成后, 其外观应如下所示。
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a>应用 async 关键字

接下来, 将`async`关键字应用于**Main**方法。 我们将需要执行三项操作。

1. 将`async`关键字添加到**Main**方法签名中。
1. 将返回类型从`void`更改为`Task`。
1. 删除呼叫`Wait()`上的呼叫`SendArticleAsync` , 并将其替换为。 `await`

请尝试再次运行应用程序-它仍应完全像以前一样正常运行, 但现在代码能够将线程释放回 .net threadpool, 同时我们等待邮件排队。

现在我们已发送了一封邮件, 最后一步是添加支持以_接收_邮件。