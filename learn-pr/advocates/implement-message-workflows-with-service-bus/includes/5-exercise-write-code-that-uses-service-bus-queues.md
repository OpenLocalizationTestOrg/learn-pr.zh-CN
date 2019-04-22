<span data-ttu-id="f49ff-101">您已选择使用服务总线队列来交换有关销售人员使用的移动应用程序与托管在 azure 中的 web 服务之间的单个销售的消息, 这些邮件将存储 azure SQL 数据库实例中每个销售的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f49ff-101">You've chosen to use a Service Bus queue to exchange messages about individual sales between the mobile app that your sales personnel use and the web service, hosted in Azure, that will store details about each sale in an Azure SQL Database instance.</span></span>

<span data-ttu-id="f49ff-102">你已在 Azure 订阅中实现必要的对象。</span><span class="sxs-lookup"><span data-stu-id="f49ff-102">You've already implemented the necessary objects in your Azure subscription.</span></span> <span data-ttu-id="f49ff-103">现在, 您想要编写将邮件发送到该队列并检索邮件的代码。</span><span class="sxs-lookup"><span data-stu-id="f49ff-103">Now, you want to write code that sends messages to that queue and retrieves messages.</span></span>

## <a name="clone-and-open-the-starter-application"></a><span data-ttu-id="f49ff-104">克隆并打开起始应用程序</span><span class="sxs-lookup"><span data-stu-id="f49ff-104">Clone and open the starter application</span></span>

<span data-ttu-id="f49ff-105">在此单元中, 将生成两个控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="f49ff-105">In this unit, you'll build two console applications.</span></span> <span data-ttu-id="f49ff-106">第一个应用程序将邮件放入服务总线队列, 第二个应用程序将其检索。</span><span class="sxs-lookup"><span data-stu-id="f49ff-106">The first application places messages into a Service Bus queue and the second retrieves them.</span></span> <span data-ttu-id="f49ff-107">应用程序是单个 .net Core 解决方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="f49ff-107">The applications are part of a single .NET Core solution.</span></span>

1. <span data-ttu-id="f49ff-108">通过克隆解决方案开始: 在云命令行管理程序中运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="f49ff-108">Start by cloning the solution: run the following commands in the Cloud Shell:</span></span>

```bash
cd ~
git clone https://github.com/MicrosoftDocs/mslearn-connect-services-together.git
```

2. <span data-ttu-id="f49ff-109">接下来, 将目录更改为起始文件夹, 然后打开云命令行管理程序编辑器。</span><span class="sxs-lookup"><span data-stu-id="f49ff-109">Next, change directories into the starter folder and open the Cloud Shell editor.</span></span>

```bash
cd mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
code .
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="f49ff-110">配置到服务总线命名空间的连接字符串</span><span class="sxs-lookup"><span data-stu-id="f49ff-110">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="f49ff-111">为了访问服务总线命名空间并使用队列, 您必须在控制台应用程序中配置两条信息:</span><span class="sxs-lookup"><span data-stu-id="f49ff-111">In order to access a Service Bus namespace and use a queue, you must configure two pieces of information in your console apps:</span></span>

* <span data-ttu-id="f49ff-112">命名空间的终结点</span><span class="sxs-lookup"><span data-stu-id="f49ff-112">The endpoint for your namespace</span></span>
* <span data-ttu-id="f49ff-113">用于身份验证的共享访问密钥</span><span class="sxs-lookup"><span data-stu-id="f49ff-113">The shared access key for authentication</span></span>

<span data-ttu-id="f49ff-114">这两个值都可以从 Azure 门户获取, 形式为完整的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f49ff-114">Both of these values can be obtained from the Azure portal in the form of a complete connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="f49ff-115">为简单起见, 您将在两个控制台应用程序的**Program.cs**文件中对连接字符串进行硬编码。</span><span class="sxs-lookup"><span data-stu-id="f49ff-115">For simplicity, you will hard-code the connection string in the **Program.cs** file of both console applications.</span></span> <span data-ttu-id="f49ff-116">在生产应用程序中, 您可以使用配置文件甚至 Azure 密钥存储库来存储连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f49ff-116">In a production application, you might use a configuration file or even Azure Key Vault to store the connection string.</span></span>

1. <span data-ttu-id="f49ff-117">在 CloudShell 中运行以下命令, 以显示服务总线命名空间的主连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f49ff-117">Run the following command in the CloudShell to display the primary connection string for your Service Bus namespace.</span></span> <span data-ttu-id="f49ff-118">将`<namespace-name>`替换为服务总线命名空间的名称。</span><span class="sxs-lookup"><span data-stu-id="f49ff-118">Replace `<namespace-name>` with the name of your Service Bus namespace.</span></span>

    ```azurecli
    az servicebus namespace authorization-rule keys list \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name RootManageSharedAccessKey \
        --query primaryConnectionString \
        --output tsv \
        --namespace-name <namespace-name>
    ```

    <span data-ttu-id="f49ff-119">此模块中将多次需要此连接字符串, 因此您可能需要将其粘贴到某个位置。</span><span class="sxs-lookup"><span data-stu-id="f49ff-119">You'll need this connection string multiple times throughout this module, so you might want to paste it somewhere handy.</span></span>

1. <span data-ttu-id="f49ff-120">从云命令行管理程序复制密钥。</span><span class="sxs-lookup"><span data-stu-id="f49ff-120">Copy the key from Cloud Shell.</span></span> <span data-ttu-id="f49ff-121">在编辑器中, 打开**privatemessagesender/程序 .cs**并找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="f49ff-121">In the editor, open **privatemessagesender/Program.cs** and locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    <span data-ttu-id="f49ff-122">在引号之间粘贴连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f49ff-122">Paste the connection string between the quotation marks.</span></span> <span data-ttu-id="f49ff-123">使用<kbd>Ctrl + S</kbd>键保存文件。</span><span class="sxs-lookup"><span data-stu-id="f49ff-123">Save the file using the <kbd>Ctrl+S</kbd> keys.</span></span>

1. <span data-ttu-id="f49ff-124">在 " **privatemessagereceiver/Program**" 中重复上述步骤, 在相同的 "连接字符串" 值中粘贴。</span><span class="sxs-lookup"><span data-stu-id="f49ff-124">Repeat the previous step in **privatemessagereceiver/Program.cs**, pasting in the same connection string value.</span></span> <span data-ttu-id="f49ff-125">通过 "..." 保存文件菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="f49ff-125">Save the file either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

## <a name="write-code-that-sends-a-message-to-the-queue"></a><span data-ttu-id="f49ff-126">编写用于将邮件发送到队列的代码</span><span class="sxs-lookup"><span data-stu-id="f49ff-126">Write code that sends a message to the queue</span></span>

<span data-ttu-id="f49ff-127">若要完成发送有关销售的邮件的组件, 请按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="f49ff-127">To complete the component that sends messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="f49ff-128">在编辑器中打开**privatemessagesender/程序 .cs。**</span><span class="sxs-lookup"><span data-stu-id="f49ff-128">Open **privatemessagesender/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="f49ff-129">查找`SendSalesMessageAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="f49ff-129">Locate the `SendSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="f49ff-130">在该方法中, 找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="f49ff-130">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="f49ff-131">若要创建队列客户端, 请将该行代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-131">To create a queue client, replace that line of code with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="f49ff-132">在`try...catch`块中, 找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="f49ff-132">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="f49ff-133">若要为队列创建和设置邮件格式, 请将该行代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-133">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="f49ff-134">若要在控制台中显示邮件, 请在下一行中添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-134">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="f49ff-135">若要将邮件发送到队列, 请在下一行中添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-135">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.SendAsync(message);
    ```

1. <span data-ttu-id="f49ff-136">找到以下代码行： </span><span class="sxs-lookup"><span data-stu-id="f49ff-136">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the queue here
    ```

1. <span data-ttu-id="f49ff-137">若要关闭与服务总线的连接, 请将该行代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-137">To close the connection to the Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="f49ff-138">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="f49ff-138">Save the file.</span></span>

## <a name="send-a-message-to-the-queue"></a><span data-ttu-id="f49ff-139">将邮件发送到队列</span><span class="sxs-lookup"><span data-stu-id="f49ff-139">Send a message to the queue</span></span>

<span data-ttu-id="f49ff-140">若要运行发送有关销售的消息的组件, 请在云命令行管理程序中运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="f49ff-140">To run the component that sends a message about a sale, run the following command in the Cloud Shell:</span></span>

```bash
dotnet run -p privatemessagesender
```

> [!NOTE]
> <span data-ttu-id="f49ff-141">您在此练习中运行的应用程序可能需要一段时间才能启动`dotnet` , 就像从远程源还原包并在首次运行应用程序时生成这些应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="f49ff-141">The apps you run during this exercise may take a moment to start up, as `dotnet` has to restore packages from remote sources and build the apps the first time they are run.</span></span>

<span data-ttu-id="f49ff-142">在程序执行时, 您将看到已打印的邮件, 表明它发送了一封邮件。</span><span class="sxs-lookup"><span data-stu-id="f49ff-142">As the program executes, you'll see messages printed indicating that it's sending a message.</span></span> <span data-ttu-id="f49ff-143">每次运行应用程序时, 都会向队列中添加一封其他消息。</span><span class="sxs-lookup"><span data-stu-id="f49ff-143">Each time you run the app, one additional message will be added to the queue.</span></span>

<span data-ttu-id="f49ff-144">完成后, 运行以下命令以查看队列中的邮件数:</span><span class="sxs-lookup"><span data-stu-id="f49ff-144">Once it's finished, run the following command to see how many messages are in the queue:</span></span>

```azurecli
az servicebus queue show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name salesmessages \
    --query messageCount \
    --namespace-name <namespace-name>
```

## <a name="write-code-that-receives-a-message-from-the-queue"></a><span data-ttu-id="f49ff-145">编写从队列中接收邮件的代码</span><span class="sxs-lookup"><span data-stu-id="f49ff-145">Write code that receives a message from the queue</span></span>

1. <span data-ttu-id="f49ff-146">在编辑器中打开**privatemessagereceiver/程序 .cs**</span><span class="sxs-lookup"><span data-stu-id="f49ff-146">Open **privatemessagereceiver/Program.cs** in the editor</span></span>

1. <span data-ttu-id="f49ff-147">查找`ReceiveSalesMessageAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="f49ff-147">Locate the `ReceiveSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="f49ff-148">在该方法中, 找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="f49ff-148">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="f49ff-149">若要创建队列客户端, 请将该行替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-149">To create a queue client, replace that line with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="f49ff-150">查找`RegisterMessageHandler()`方法。</span><span class="sxs-lookup"><span data-stu-id="f49ff-150">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="f49ff-151">若要配置邮件处理选项, 请将该方法中的所有代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-151">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="f49ff-152">若要注册邮件处理程序, 在下一行中, 添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-152">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="f49ff-153">查找`ProcessMessagesAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="f49ff-153">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="f49ff-154">您已将此方法注册为处理传入邮件的方法。</span><span class="sxs-lookup"><span data-stu-id="f49ff-154">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="f49ff-155">若要在控制台中显示传入的邮件, 请将该方法中的所有代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-155">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="f49ff-156">若要从队列中删除收到的邮件, 请在下一行中添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-156">To remove the received message from the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="f49ff-157">返回到`ReceiveSalesMessageAsync()`方法并找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="f49ff-157">Return to the `ReceiveSalesMessageAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the queue here
    ```

1. <span data-ttu-id="f49ff-158">若要关闭与服务总线的连接, 请将该行替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="f49ff-158">To close the connection to Service Bus, replace that line with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="f49ff-159">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="f49ff-159">Save the file.</span></span>

## <a name="retrieve-a-message-from-the-queue"></a><span data-ttu-id="f49ff-160">从队列中检索邮件</span><span class="sxs-lookup"><span data-stu-id="f49ff-160">Retrieve a message from the queue</span></span>

<span data-ttu-id="f49ff-161">若要运行发送有关销售的消息的组件, 请在云命令行管理程序中运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="f49ff-161">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p privatemessagereceiver
```

<span data-ttu-id="f49ff-162">当您看到邮件已接收并显示在控制台中时, 按键`Enter`停止应用。</span><span class="sxs-lookup"><span data-stu-id="f49ff-162">When you see that the message has been received and displayed in the console, press `Enter` to stop the app.</span></span> <span data-ttu-id="f49ff-163">然后, 运行与之前相同的命令, 以确认已从队列中删除了所有邮件:</span><span class="sxs-lookup"><span data-stu-id="f49ff-163">Then, run the same command as before to confirm that all of the messages have been removed from the queue:</span></span>

```azurecli
az servicebus queue show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name salesmessages \
    --query messageCount \
    --namespace-name <namespace-name>
```

<span data-ttu-id="f49ff-164">这将显示`0`是否已删除所有邮件。</span><span class="sxs-lookup"><span data-stu-id="f49ff-164">This will show `0` if all the messages have been removed.</span></span>

<span data-ttu-id="f49ff-165">您编写的代码将有关单个销售的消息发送到服务总线队列。</span><span class="sxs-lookup"><span data-stu-id="f49ff-165">You have written code that sends a message about individual sales to a Service Bus queue.</span></span> <span data-ttu-id="f49ff-166">在销售团队分布式应用程序中, 应在销售人员在设备上使用的移动应用中编写此代码。</span><span class="sxs-lookup"><span data-stu-id="f49ff-166">In the sales force distributed application, you should write this code in the mobile app that sales personnel use on devices.</span></span>

<span data-ttu-id="f49ff-167">您还编写了从服务总线队列中接收邮件的代码。</span><span class="sxs-lookup"><span data-stu-id="f49ff-167">You have also written code that receives a message from the Service Bus queue.</span></span> <span data-ttu-id="f49ff-168">在销售团队分布式应用程序中, 应在运行在 Azure 中的 web 服务中编写此代码并处理收到的邮件。</span><span class="sxs-lookup"><span data-stu-id="f49ff-168">In the sales force distributed application, you should write this code in the web service that runs in Azure and processes received messages.</span></span>
