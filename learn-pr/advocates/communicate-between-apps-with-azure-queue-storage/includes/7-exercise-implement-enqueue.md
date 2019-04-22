<span data-ttu-id="01e9e-101">现在, 已准备好所有要求, 您可以编写代码来创建新的存储队列并添加邮件。</span><span class="sxs-lookup"><span data-stu-id="01e9e-101">Now that all the requirements are in place, you can write code that creates a new storage queue and adds a message.</span></span> <span data-ttu-id="01e9e-102">我们通常会将此代码放在生成数据的前端应用中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-102">We would typically place this code in our front-end apps that generate the data.</span></span>

## <a name="add-the-client-library-for-azure-storage"></a><span data-ttu-id="01e9e-103">为 Azure 存储添加客户端库</span><span class="sxs-lookup"><span data-stu-id="01e9e-103">Add the client library for Azure Storage</span></span>

<span data-ttu-id="01e9e-104">首先, 我们将**Azure 存储客户端库**添加到我们的应用中的 .net。</span><span class="sxs-lookup"><span data-stu-id="01e9e-104">Let's start by adding the **Azure Storage Client Library for .NET** to our app.</span></span> <span data-ttu-id="01e9e-105">可以使用 NuGet (.net 程序包管理器) 来安装它。</span><span class="sxs-lookup"><span data-stu-id="01e9e-105">It can be installed with NuGet (a .NET package manager).</span></span> 

1. <span data-ttu-id="01e9e-106">使用`dotnet add package`命令`WindowsAzure.Storage`将包安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-106">Install the `WindowsAzure.Storage` package to the project with the `dotnet add package` command.</span></span> <span data-ttu-id="01e9e-107">您可以在 "终端" 窗口中的云命令行管理程序_下_执行此操作, 如果您正在本地计算机上运行, 则可以在项目所在的同一个文件夹中的终端/控制台窗口中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="01e9e-107">You can do this in the terminal window _below_ the Cloud Shell, or if you are working on your local computer, in a terminal/console window in the same folder as the project.</span></span>

```azurecli
dotnet add package WindowsAzure.Storage
```

## <a name="add-a-method-to-send-a-news-alert"></a><span data-ttu-id="01e9e-108">添加用于发送新闻通知的方法</span><span class="sxs-lookup"><span data-stu-id="01e9e-108">Add a method to send a news alert</span></span>

<span data-ttu-id="01e9e-109">接下来, 创建一个新方法, 将新闻报道发送到队列中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-109">Next, let's create a new method to send a news story into a queue.</span></span>

1. <span data-ttu-id="01e9e-110">在代码`Program.cs`编辑器中打开该文件。</span><span class="sxs-lookup"><span data-stu-id="01e9e-110">Open the `Program.cs` file in your code editor.</span></span>

1. <span data-ttu-id="01e9e-111">在文件顶部, 添加以下命名空间。</span><span class="sxs-lookup"><span data-stu-id="01e9e-111">At the top of the file, add the following namespaces.</span></span> <span data-ttu-id="01e9e-112">我们将使用这两个类型的类型连接到 Azure 存储, 然后使用队列。</span><span class="sxs-lookup"><span data-stu-id="01e9e-112">We'll be using types from both of these to connect to Azure Storage and then to work with queues.</span></span>

    - `System.Threading.Tasks`
    - `Microsoft.WindowsAzure.Storage`
    - `Microsoft.WindowsAzure.Storage.Queue`

1. <span data-ttu-id="01e9e-113">在`Program`名为`SendArticleAsync`的类中创建一个静态方法, `string`该方法采用`Task`a 并返回。</span><span class="sxs-lookup"><span data-stu-id="01e9e-113">Create a static method in the `Program` class named `SendArticleAsync` that takes a `string` and returns a `Task`.</span></span> <span data-ttu-id="01e9e-114">我们将使用此方法向我们的服务发送新闻文章。</span><span class="sxs-lookup"><span data-stu-id="01e9e-114">We'll use this method to send a news article in to our service.</span></span> <span data-ttu-id="01e9e-115">将输入参数`newsMessage`命名为如下所示。</span><span class="sxs-lookup"><span data-stu-id="01e9e-115">Name the input parameter `newsMessage` as shown below.</span></span>

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
    
1. <span data-ttu-id="01e9e-116">在您的新方法中, 使用`CloudStorageAccount.Parse`静态方法分析连接字符串 (回想我们将其放入常量字符串中)。</span><span class="sxs-lookup"><span data-stu-id="01e9e-116">In your new method, use the static `CloudStorageAccount.Parse` method to parse your connection string (recall we placed it into a constant string).</span></span> <span data-ttu-id="01e9e-117">此方法返回一个`CloudStorageAccount`需要存储在变量中的对象。</span><span class="sxs-lookup"><span data-stu-id="01e9e-117">This method returns a `CloudStorageAccount` object that needs to be stored in a variable.</span></span>

1. <span data-ttu-id="01e9e-118">对存储`CreateCloudQueueClient()`帐户对象调用方法, 以获取客户端对象并将其存储在变量中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-118">Call the `CreateCloudQueueClient()` method on the storage account object to get a client object and store that in a variable.</span></span>

1. <span data-ttu-id="01e9e-119">接下来, `GetQueueReference`对客户端对象调用方法, 并为队列名称传递字符串 "newsqueue"。</span><span class="sxs-lookup"><span data-stu-id="01e9e-119">Next, call `GetQueueReference` method on the client object and pass the string "newsqueue" for the queue name.</span></span> <span data-ttu-id="01e9e-120">这将`CloudQueue`返回可用于处理队列的对象。</span><span class="sxs-lookup"><span data-stu-id="01e9e-120">This returns a `CloudQueue` object that we can use to work with the queue.</span></span> <span data-ttu-id="01e9e-121">如果队列尚不存在, 则它是正常的。</span><span class="sxs-lookup"><span data-stu-id="01e9e-121">It's OK if the queue does not exist yet.</span></span>

1. <span data-ttu-id="01e9e-122">对`CreateIfNotExistsAsync()` `CloudQueue`对象的调用, 以确保队列已准备好使用。</span><span class="sxs-lookup"><span data-stu-id="01e9e-122">Call `CreateIfNotExistsAsync()` on the `CloudQueue` object to ensure the queue is ready for use.</span></span> <span data-ttu-id="01e9e-123">这将创建队列 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="01e9e-123">This will create the queue if necessary.</span></span>
    - <span data-ttu-id="01e9e-124">由于这是一种异步方法, 因此请`await`使用 c # 关键字以确保我们能与它一起正常工作。</span><span class="sxs-lookup"><span data-stu-id="01e9e-124">Since this is an asynchronous method, use the C# `await` keyword to ensure we work properly with it.</span></span> <span data-ttu-id="01e9e-125">这也意味着需要使用`async`关键字修饰_方法_。</span><span class="sxs-lookup"><span data-stu-id="01e9e-125">That also means you need to decorate the _method_ with the `async` keyword.</span></span> 
    - <span data-ttu-id="01e9e-126">`CreateIfNotExistsAsync`返回一个`bool`值, 如果队列`true`已创建且已存在, `false`则为。</span><span class="sxs-lookup"><span data-stu-id="01e9e-126">`CreateIfNotExistsAsync` returns a `bool` value that will be `true` if the queue was created and `false` if it already exists.</span></span> <span data-ttu-id="01e9e-127">如果创建了队列, 则将消息输出到控制台。</span><span class="sxs-lookup"><span data-stu-id="01e9e-127">Output a message to the console if we created the queue.</span></span>
    - <span data-ttu-id="01e9e-128">下面是一个示例, 如果你需要一些帮助。</span><span class="sxs-lookup"><span data-stu-id="01e9e-128">Here's an example if you need some help.</span></span>

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

1. <span data-ttu-id="01e9e-129">创建的`CloudQueueMessage`实例。</span><span class="sxs-lookup"><span data-stu-id="01e9e-129">Create an instance of a `CloudQueueMessage`.</span></span> 
    - <span data-ttu-id="01e9e-130">它采用`string`参数, 并在方法参数 (`newsMessage`) 中传递。</span><span class="sxs-lookup"><span data-stu-id="01e9e-130">It takes a `string` parameter, pass in the method parameter (`newsMessage`).</span></span> <span data-ttu-id="01e9e-131">这将是邮件的_正文_。</span><span class="sxs-lookup"><span data-stu-id="01e9e-131">This will be the _body_ of the message.</span></span> <span data-ttu-id="01e9e-132">还有一个名为的静态方法, 可以创建二进制邮件有效负载。</span><span class="sxs-lookup"><span data-stu-id="01e9e-132">There is also a static method named  that can create a binary message payload.</span></span>

1. <span data-ttu-id="01e9e-133">对`AddMessageAsync`要将`CloudQueue`邮件添加到队列中的对象的调用。</span><span class="sxs-lookup"><span data-stu-id="01e9e-133">Call `AddMessageAsync` on the `CloudQueue` object to add the message to the queue.</span></span> <span data-ttu-id="01e9e-134">这也是一种异步方法, 您需要使用`await`关键字来确保我们能与它进行正确的交互。</span><span class="sxs-lookup"><span data-stu-id="01e9e-134">This is also an asynchronous method and you will need to use the `await` keyword to ensure we properly interact with it.</span></span>

1. <span data-ttu-id="01e9e-135">保存文件, 并通过在命令窗口`dotnet build`中键入内容生成它。</span><span class="sxs-lookup"><span data-stu-id="01e9e-135">Save the file and build it by typing `dotnet build` into the command window.</span></span> <span data-ttu-id="01e9e-136">修复所有错误, 可以使用以下代码检查工作。</span><span class="sxs-lookup"><span data-stu-id="01e9e-136">Fix any errors, you can use the following code to check your work.</span></span>

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

## <a name="add-code-to-send-a-message"></a><span data-ttu-id="01e9e-137">添加代码以发送邮件</span><span class="sxs-lookup"><span data-stu-id="01e9e-137">Add code to send a message</span></span>

<span data-ttu-id="01e9e-138">让我们修改`Main`方法以将接收到的任何参数传递到新方法, 以便我们可以测试新的 send 方法。</span><span class="sxs-lookup"><span data-stu-id="01e9e-138">Let's modify the `Main` method to pass any parameters received into our new method so we can test our new send method.</span></span>

1. <span data-ttu-id="01e9e-139">查找`Main`方法。</span><span class="sxs-lookup"><span data-stu-id="01e9e-139">Locate the `Main` method.</span></span>

1. <span data-ttu-id="01e9e-140">检查传递`args`的参数以查看是否有任何数据传递到了命令行。</span><span class="sxs-lookup"><span data-stu-id="01e9e-140">Check the passed `args` parameter to see if any data was passed to the command line.</span></span> <span data-ttu-id="01e9e-141">如果是这样, `String.Join`请使用空格作为分隔符, 以创建单个字符串中的所有单词。</span><span class="sxs-lookup"><span data-stu-id="01e9e-141">If so, use `String.Join` to create a single string from all the words using a space as the separator.</span></span>

1. <span data-ttu-id="01e9e-142">将其传递给新`SendArticleAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="01e9e-142">Pass that to the new `SendArticleAsync` method.</span></span> 

1. <span data-ttu-id="01e9e-143">返回后, 使用`Console.WriteLine`它输出我们发送的消息。</span><span class="sxs-lookup"><span data-stu-id="01e9e-143">Once it returns, use `Console.WriteLine` to output the message we sent.</span></span>

1. <span data-ttu-id="01e9e-144">保存文件并生成程序 (`dotnet build`), 可以使用下面的代码检查您的工作。</span><span class="sxs-lookup"><span data-stu-id="01e9e-144">Save the file and build the program (`dotnet build`), you can use the code below to check your work.</span></span>

    > [!NOTE]
    > <span data-ttu-id="01e9e-145">由于我们的方法在技术上是异步的, 因此我们`await`需要使用关键字, 但是, 除非您使用`Main`的是 c # 7.1 或更高版本, 否则该功能在方法中不可用。</span><span class="sxs-lookup"><span data-stu-id="01e9e-145">Since our method is technically asynchronous, we will want to use the `await` keyword, however that feature isn't available on your `Main` method unless you are using C# 7.1 or later.</span></span> <span data-ttu-id="01e9e-146">只需`Wait()`调用方法以实际阻止正在等待的方法返回, 我们将在一分钟内修复。</span><span class="sxs-lookup"><span data-stu-id="01e9e-146">Just call `Wait()` on the method to actually block waiting for the method to return, we'll fix that in a minute.</span></span>

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

## <a name="execute-the-application"></a><span data-ttu-id="01e9e-147">执行应用程序</span><span class="sxs-lookup"><span data-stu-id="01e9e-147">Execute the application</span></span>

<span data-ttu-id="01e9e-148">应用程序现在可以发送邮件。</span><span class="sxs-lookup"><span data-stu-id="01e9e-148">The application can now send messages.</span></span> <span data-ttu-id="01e9e-149">若要对其进行测试, 可以使用`dotnet run`命令从命令行运行它。</span><span class="sxs-lookup"><span data-stu-id="01e9e-149">To test it, you can run it from the command line with the `dotnet run` command.</span></span> <span data-ttu-id="01e9e-150">任何其他字符串都作为参数传递给应用程序。</span><span class="sxs-lookup"><span data-stu-id="01e9e-150">Any additional strings are passed as parameters to the application.</span></span> 

> [!WARNING]
> <span data-ttu-id="01e9e-151">在生成和运行程序之前, 请确保已将所有文件保存在联机编辑器中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-151">Make sure you have saved all the files in the online editor before you build and run the program.</span></span>

<span data-ttu-id="01e9e-152">例如, 您可以键入:</span><span class="sxs-lookup"><span data-stu-id="01e9e-152">As an example, you can type:</span></span>

```azurecli
dotnet run Send this message
```

<span data-ttu-id="01e9e-153">这应将字符串`"Send this message"`添加到队列中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-153">This should add the string `"Send this message"` into the queue.</span></span>

## <a name="check-your-results"></a><span data-ttu-id="01e9e-154">检查结果</span><span class="sxs-lookup"><span data-stu-id="01e9e-154">Check your results</span></span>

<span data-ttu-id="01e9e-155">您可以使用**存储资源管理器**检查 Azure 门户中的队列, 如果您打开该产品, 它将允许您浏览每个存储帐户中的数据。</span><span class="sxs-lookup"><span data-stu-id="01e9e-155">You can check queues in the Azure portal using the **Storage Explorer**, if you open that product it will let you explore the data in each storage account you own.</span></span>

<span data-ttu-id="01e9e-156">或者, 也可以使用 Azure CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="01e9e-156">Alternatively, you can use the Azure CLI or PowerShell.</span></span> <span data-ttu-id="01e9e-157">在命令行管理程序中尝试此命令`<connection-string>` , 将值替换为您的特定连接字符串:</span><span class="sxs-lookup"><span data-stu-id="01e9e-157">Try this command in the shell, replacing the `<connection-string>` value with your specific connection string:</span></span>

```azurecli
az storage message peek --queue-name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="01e9e-158">这将转储邮件的信息, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="01e9e-158">This should dump the information for your message, which will look something like this:</span></span>

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

<span data-ttu-id="01e9e-159">还可以使用其他几个命令来尝试使用工具-同时`az storage queue --help`签出和`az storage message --help`浏览这些命令。</span><span class="sxs-lookup"><span data-stu-id="01e9e-159">There are several other commands available that you can try with the tools - check out both `az storage queue --help` and `az storage message --help` to explore them.</span></span>

> [!TIP]
> <span data-ttu-id="01e9e-160">将您的连接字符串值放在名`AZURE_STORAGE_CONNECTION_STRING`为的环境变量中, 让您不必`--connection-string`每次都键入参数!</span><span class="sxs-lookup"><span data-stu-id="01e9e-160">Put your connection string value into an environment variable named `AZURE_STORAGE_CONNECTION_STRING` to save yourself from having to type the `--connection-string` parameter every time!</span></span>

## <a name="optional---use-the-async-versions-of-the-methods"></a><span data-ttu-id="01e9e-161">可选-使用方法的异步版本</span><span class="sxs-lookup"><span data-stu-id="01e9e-161">Optional - Use the async versions of the methods</span></span>

<span data-ttu-id="01e9e-162">我们在`Wait()`上面的 send 方法中使用, 但这并不是我们的计算资源的有效使用。</span><span class="sxs-lookup"><span data-stu-id="01e9e-162">We used `Wait()` on the send method above but that's not an efficient use of our computing resources.</span></span> <span data-ttu-id="01e9e-163">相反, 我们需要使用 c # `async`和`await`方法。</span><span class="sxs-lookup"><span data-stu-id="01e9e-163">Instead, we want to use the C# `async` and `await` methods.</span></span> <span data-ttu-id="01e9e-164">但是, 我们需要_至少_使用 c # 7.1, 才能将这些关键字应用到**主**方法。</span><span class="sxs-lookup"><span data-stu-id="01e9e-164">However, we will need to be using _at least_ C# 7.1 to be able to apply these keywords to our **Main** method.</span></span>

### <a name="switch-to-c-71"></a><span data-ttu-id="01e9e-165">切换到 c # 7。1</span><span class="sxs-lookup"><span data-stu-id="01e9e-165">Switch to C# 7.1</span></span>

<span data-ttu-id="01e9e-166">在 c `async` # `await` 7.1 之前, c # 和关键字在**Main**方法中不是有效的关键字。</span><span class="sxs-lookup"><span data-stu-id="01e9e-166">C#'s `async` and `await` keywords were not valid keywords in **Main** methods until C# 7.1.</span></span> <span data-ttu-id="01e9e-167">我们可以通过 **.csproj**文件中的标志轻松切换到该编译器。</span><span class="sxs-lookup"><span data-stu-id="01e9e-167">We can easily switch to that compiler through a flag in the **.csproj** file.</span></span>

1. <span data-ttu-id="01e9e-168">在编辑器中打开**QueueApp**文件。</span><span class="sxs-lookup"><span data-stu-id="01e9e-168">Open the **QueueApp.csproj** file in the editor.</span></span>

1. <span data-ttu-id="01e9e-169">在`<LangVersion>7.1</LangVersion>`生成文件中`PropertyGroup`添加到第一个中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-169">Add `<LangVersion>7.1</LangVersion>` into the first `PropertyGroup` in the build file.</span></span> <span data-ttu-id="01e9e-170">完成后, 其外观应如下所示。</span><span class="sxs-lookup"><span data-stu-id="01e9e-170">It should look like the following when you are finished.</span></span>
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a><span data-ttu-id="01e9e-171">应用 async 关键字</span><span class="sxs-lookup"><span data-stu-id="01e9e-171">Apply the async keyword</span></span>

<span data-ttu-id="01e9e-172">接下来, 将`async`关键字应用于**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="01e9e-172">Next, apply the `async` keyword to the **Main** method.</span></span> <span data-ttu-id="01e9e-173">我们将需要执行三项操作。</span><span class="sxs-lookup"><span data-stu-id="01e9e-173">We will have to do three things.</span></span>

1. <span data-ttu-id="01e9e-174">将`async`关键字添加到**Main**方法签名中。</span><span class="sxs-lookup"><span data-stu-id="01e9e-174">Add the `async` keyword onto the **Main** method signature.</span></span>
1. <span data-ttu-id="01e9e-175">将返回类型从`void`更改为`Task`。</span><span class="sxs-lookup"><span data-stu-id="01e9e-175">Change the return type from `void` to `Task`.</span></span>
1. <span data-ttu-id="01e9e-176">删除呼叫`Wait()`上的呼叫`SendArticleAsync` , 并将其替换为。 `await`</span><span class="sxs-lookup"><span data-stu-id="01e9e-176">Remove the call to `Wait()` on the call to `SendArticleAsync` and replace it with `await`.</span></span>

<span data-ttu-id="01e9e-177">请尝试再次运行应用程序-它仍应完全像以前一样正常运行, 但现在代码能够将线程释放回 .net threadpool, 同时我们等待邮件排队。</span><span class="sxs-lookup"><span data-stu-id="01e9e-177">Try running the app again - it should still work exactly as before, but now the code is able to release the thread back to the .NET threadpool while we wait for the message to be queued.</span></span>

<span data-ttu-id="01e9e-178">现在我们已发送了一封邮件, 最后一步是添加支持以_接收_邮件。</span><span class="sxs-lookup"><span data-stu-id="01e9e-178">Now that we have sent a message, the last step is to add support to _receive_ the message.</span></span>