您已选择使用 Azure 服务总线主题在销售团队分布式应用程序中分发有关销售业绩的邮件。 由销售人员在其移动设备上使用的应用程序将发送汇总每个区域和时间段的销售数据的邮件。 这些邮件将分发到位于公司运营区域 (包括美洲和欧洲) 的 web 服务。

你已在 Azure 订阅中实施了必要的基础结构, 包括主题和订阅。 现在, 您需要编写向主题发送邮件并从订阅中检索邮件的代码。 在开始之前, 您需要通过在云命令行管理程序中执行以下命令来确保您在正确的目录中工作:

```bash
cd ~/mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>配置到服务总线命名空间的连接字符串

首先在 "发送" 和 "接收" 组件中配置连接字符串:

1. 在编辑器中, 打开**performancemessagesender/程序 .cs**并找到以下代码行:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    在引号之间粘贴连接字符串, 并通过 "..." 保存文件。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

1. 在 " **performancemessagereceiver/Program**" 中重复上述步骤, 在相同的 "连接字符串" 值中粘贴并保存文件。

## <a name="write-code-that-sends-a-message-to-the-topic"></a>编写向主题发送邮件的代码

若要完成发送有关销售业绩的邮件的组件, 请按照以下步骤操作:

1. 在编辑器中打开**performancemessagesender/程序 .cs。**

1. 查找`SendPerformanceMessageAsync()`方法。

1. 在该方法中, 找到以下代码行:

    ```C#
    // Create a Topic Client here
    ```

1. 若要创建主题客户端, 请将该行代码替换为以下代码:

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. 在`try...catch`块中, 找到以下代码行:

    ```C#
    // Create and send a message here
    ```

1. 若要为队列创建和设置邮件格式, 请将该行代码替换为以下代码:

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. 若要在控制台中显示邮件, 请在下一行中添加以下代码:

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. 若要将邮件发送到队列, 请在下一行中添加以下代码:

    ```C#
    await topicClient.SendAsync(message);
    ```

1. 找到以下代码行： 

    ```C#
    // Close the connection to the topic here
    ```

1. 若要关闭与服务总线的连接, 请将该行代码替换为以下代码:

    ```C#
    await topicClient.CloseAsync();
    ```

1. 保存该文件。

## <a name="send-a-message-to-the-topic"></a>向主题发送邮件

若要运行发送有关销售的消息的组件, 请在云命令行管理程序中运行以下命令:

```bash
dotnet run -p performancemessagesender
```

在程序执行时, 您将看到已打印的邮件, 表明它发送了一封邮件。 每次运行应用程序时, 都会向主题中添加一条额外消息, 并且每个订阅者都将收到副本。

完成后, 运行以下命令, 以查看美洲订阅中有多少封邮件:

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

如果要替换`EuropeAndAfrica` `Americas`, 应看到两个订阅的邮件数相同。

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a>编写从主题订阅接收邮件的代码

若要完成检索有关销售业绩的邮件的组件, 请按照以下步骤操作:

1. 在编辑器中打开**performancemessagereceiver/程序 .cs。**

1. 查找`MainAsync()`方法。

1. 在该方法中, 找到以下代码行:

    ```C#
    // Create a subscription client here
    ```

1. 若要创建订阅客户端, 请将该行替换为以下代码:

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. 查找`RegisterMessageHandler()`方法。

1. 若要配置邮件处理选项, 请将该方法中的所有代码替换为以下代码:

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. 若要注册邮件处理程序, 在下一行中, 添加以下代码:

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. 查找`ProcessMessagesAsync()`方法。 您已将此方法注册为处理传入邮件的方法。

1. 若要在控制台中显示传入的邮件, 请将该方法中的所有代码替换为以下代码:

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. 若要从订阅中删除收到的邮件, 请在下一行中添加以下代码:

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. 返回到`MainAsync()`方法并找到以下代码行:

    ```C#
    // Close the subscription here
    ```

1. 若要关闭与服务总线的连接, 请将该代码替换为以下代码:

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. 在 Visual Studio Code 中, 关闭所有编辑器窗口并保存所有更改过的文件。

## <a name="retrieve-a-message-from-a-topic-subscription"></a>从主题订阅中检索邮件

若要运行检索有关销售业绩的消息的组件, 请按照以下步骤操作:

```bash
dotnet run -p performancemessagereceiver
```

当程序停止正在接收的邮件的打印通知时, 请`Enter`按键停止应用。 然后, 运行与之前相同的命令, 以确认`Americas`订阅中存在零个剩余邮件。

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

如果要替换`EuropeAndAfrica` `Americas`, 则会发现邮件计数尚未更改。 应用程序仅收到来自`Americas`订阅的邮件。
