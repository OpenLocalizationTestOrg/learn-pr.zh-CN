<span data-ttu-id="10724-101">您已选择使用 Azure 服务总线主题在销售团队分布式应用程序中分发有关销售业绩的邮件。</span><span class="sxs-lookup"><span data-stu-id="10724-101">You have chosen to use an Azure Service Bus topic to distribute messages about sales performance in your sales force distributed application.</span></span> <span data-ttu-id="10724-102">由销售人员在其移动设备上使用的应用程序将发送汇总每个区域和时间段的销售数据的邮件。</span><span class="sxs-lookup"><span data-stu-id="10724-102">The app used by sales personnel on their mobile devices will send messages that summarize sales figures for each area and time period.</span></span> <span data-ttu-id="10724-103">这些邮件将分发到位于公司运营区域 (包括美洲和欧洲) 的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="10724-103">Those messages will be distributed to web services located in the company's operational regions, including the Americas and Europe.</span></span>

<span data-ttu-id="10724-104">你已在 Azure 订阅中实施了必要的基础结构, 包括主题和订阅。</span><span class="sxs-lookup"><span data-stu-id="10724-104">You have already implemented the necessary infrastructure in your Azure subscription, including the topic and subscriptions.</span></span> <span data-ttu-id="10724-105">现在, 您需要编写向主题发送邮件并从订阅中检索邮件的代码。</span><span class="sxs-lookup"><span data-stu-id="10724-105">Now, you want to write the code that sends messages to the topic and retrieves messages from a subscription.</span></span> <span data-ttu-id="10724-106">在开始之前, 您需要通过在云命令行管理程序中执行以下命令来确保您在正确的目录中工作:</span><span class="sxs-lookup"><span data-stu-id="10724-106">Before you begin, you'll need to make sure you are working in the correct directory by executing the following command in the Cloud Shell:</span></span>

```bash
cd ~/mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="10724-107">配置到服务总线命名空间的连接字符串</span><span class="sxs-lookup"><span data-stu-id="10724-107">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="10724-108">首先在 "发送" 和 "接收" 组件中配置连接字符串:</span><span class="sxs-lookup"><span data-stu-id="10724-108">Start by configuring connection strings both in the sending and receiving components:</span></span>

1. <span data-ttu-id="10724-109">在编辑器中, 打开**performancemessagesender/程序 .cs**并找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="10724-109">In the editor, open **performancemessagesender/Program.cs** and locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    <span data-ttu-id="10724-110">在引号之间粘贴连接字符串, 并通过 "..." 保存文件。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="10724-110">Paste the connection string between the quotation marks and save the file either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="10724-111">在 " **performancemessagereceiver/Program**" 中重复上述步骤, 在相同的 "连接字符串" 值中粘贴并保存文件。</span><span class="sxs-lookup"><span data-stu-id="10724-111">Repeat the previous step in **performancemessagereceiver/Program.cs**, pasting in the same connection string value and save the file.</span></span>

## <a name="write-code-that-sends-a-message-to-the-topic"></a><span data-ttu-id="10724-112">编写向主题发送邮件的代码</span><span class="sxs-lookup"><span data-stu-id="10724-112">Write code that sends a message to the topic</span></span>

<span data-ttu-id="10724-113">若要完成发送有关销售业绩的邮件的组件, 请按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="10724-113">To complete the component that sends messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="10724-114">在编辑器中打开**performancemessagesender/程序 .cs。**</span><span class="sxs-lookup"><span data-stu-id="10724-114">Open **performancemessagesender/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="10724-115">查找`SendPerformanceMessageAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="10724-115">Locate the `SendPerformanceMessageAsync()` method.</span></span>

1. <span data-ttu-id="10724-116">在该方法中, 找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="10724-116">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Topic Client here
    ```

1. <span data-ttu-id="10724-117">若要创建主题客户端, 请将该行代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-117">To create a topic client, replace that line of code with the following code:</span></span>

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. <span data-ttu-id="10724-118">在`try...catch`块中, 找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="10724-118">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="10724-119">若要为队列创建和设置邮件格式, 请将该行代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-119">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="10724-120">若要在控制台中显示邮件, 请在下一行中添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-120">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="10724-121">若要将邮件发送到队列, 请在下一行中添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-121">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await topicClient.SendAsync(message);
    ```

1. <span data-ttu-id="10724-122">找到以下代码行： </span><span class="sxs-lookup"><span data-stu-id="10724-122">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the topic here
    ```

1. <span data-ttu-id="10724-123">若要关闭与服务总线的连接, 请将该行代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-123">To close the connection to Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await topicClient.CloseAsync();
    ```

1. <span data-ttu-id="10724-124">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="10724-124">Save the file.</span></span>

## <a name="send-a-message-to-the-topic"></a><span data-ttu-id="10724-125">向主题发送邮件</span><span class="sxs-lookup"><span data-stu-id="10724-125">Send a message to the topic</span></span>

<span data-ttu-id="10724-126">若要运行发送有关销售的消息的组件, 请在云命令行管理程序中运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="10724-126">To run the component that sends a message about a sale, run the following command in the Cloud Shell:</span></span>

```bash
dotnet run -p performancemessagesender
```

<span data-ttu-id="10724-127">在程序执行时, 您将看到已打印的邮件, 表明它发送了一封邮件。</span><span class="sxs-lookup"><span data-stu-id="10724-127">As the program executes, you'll see messages printed indicating that it's sending a message.</span></span> <span data-ttu-id="10724-128">每次运行应用程序时, 都会向主题中添加一条额外消息, 并且每个订阅者都将收到副本。</span><span class="sxs-lookup"><span data-stu-id="10724-128">Each time you run the app, one additional message will be added to the topic and each subscriber will receive a copy.</span></span>

<span data-ttu-id="10724-129">完成后, 运行以下命令, 以查看美洲订阅中有多少封邮件:</span><span class="sxs-lookup"><span data-stu-id="10724-129">Once it's finished, run the following command to see how many messages are in the Americas subscription:</span></span>

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

<span data-ttu-id="10724-130">如果要替换`EuropeAndAfrica` `Americas`, 应看到两个订阅的邮件数相同。</span><span class="sxs-lookup"><span data-stu-id="10724-130">If you substitute `EuropeAndAfrica` for `Americas`, you should see that both subscriptions have the same number of messages.</span></span>

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a><span data-ttu-id="10724-131">编写从主题订阅接收邮件的代码</span><span class="sxs-lookup"><span data-stu-id="10724-131">Write code that receives a message from a topic subscription</span></span>

<span data-ttu-id="10724-132">若要完成检索有关销售业绩的邮件的组件, 请按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="10724-132">To complete the component that retrieves messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="10724-133">在编辑器中打开**performancemessagereceiver/程序 .cs。**</span><span class="sxs-lookup"><span data-stu-id="10724-133">Open **performancemessagereceiver/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="10724-134">查找`MainAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="10724-134">Locate the `MainAsync()` method.</span></span>

1. <span data-ttu-id="10724-135">在该方法中, 找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="10724-135">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a subscription client here
    ```

1. <span data-ttu-id="10724-136">若要创建订阅客户端, 请将该行替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-136">To create a subscription client, replace that line with the following code:</span></span>

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. <span data-ttu-id="10724-137">查找`RegisterMessageHandler()`方法。</span><span class="sxs-lookup"><span data-stu-id="10724-137">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="10724-138">若要配置邮件处理选项, 请将该方法中的所有代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-138">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="10724-139">若要注册邮件处理程序, 在下一行中, 添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-139">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="10724-140">查找`ProcessMessagesAsync()`方法。</span><span class="sxs-lookup"><span data-stu-id="10724-140">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="10724-141">您已将此方法注册为处理传入邮件的方法。</span><span class="sxs-lookup"><span data-stu-id="10724-141">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="10724-142">若要在控制台中显示传入的邮件, 请将该方法中的所有代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-142">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="10724-143">若要从订阅中删除收到的邮件, 请在下一行中添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-143">To remove the received message from the subscription, on the next line, add the following code:</span></span>

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="10724-144">返回到`MainAsync()`方法并找到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="10724-144">Return to the `MainAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the subscription here
    ```

1. <span data-ttu-id="10724-145">若要关闭与服务总线的连接, 请将该代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="10724-145">To close the connection to Service Bus, replace that code with the following code:</span></span>

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. <span data-ttu-id="10724-146">在 Visual Studio Code 中, 关闭所有编辑器窗口并保存所有更改过的文件。</span><span class="sxs-lookup"><span data-stu-id="10724-146">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-a-topic-subscription"></a><span data-ttu-id="10724-147">从主题订阅中检索邮件</span><span class="sxs-lookup"><span data-stu-id="10724-147">Retrieve a message from a topic subscription</span></span>

<span data-ttu-id="10724-148">若要运行检索有关销售业绩的消息的组件, 请按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="10724-148">To run the component that retrieves a message about sales performance, follow these steps:</span></span>

```bash
dotnet run -p performancemessagereceiver
```

<span data-ttu-id="10724-149">当程序停止正在接收的邮件的打印通知时, 请`Enter`按键停止应用。</span><span class="sxs-lookup"><span data-stu-id="10724-149">When the program stops printing notifications that it is receiving messages, press `Enter` to stop the app.</span></span> <span data-ttu-id="10724-150">然后, 运行与之前相同的命令, 以确认`Americas`订阅中存在零个剩余邮件。</span><span class="sxs-lookup"><span data-stu-id="10724-150">Then, run the same command as before to confirm that there are zero remaining messages in the `Americas` subscription.</span></span>

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

<span data-ttu-id="10724-151">如果要替换`EuropeAndAfrica` `Americas`, 则会发现邮件计数尚未更改。</span><span class="sxs-lookup"><span data-stu-id="10724-151">If you substitute `EuropeAndAfrica` for `Americas`, you'll see that the message count has not changed.</span></span> <span data-ttu-id="10724-152">应用程序仅收到来自`Americas`订阅的邮件。</span><span class="sxs-lookup"><span data-stu-id="10724-152">The application only received messages from the `Americas` subscription.</span></span>
