您已选择使用服务总线队列来交换有关销售人员使用的移动应用程序与托管在 azure 中的 web 服务之间的单个销售的消息, 这些邮件将存储 azure SQL 数据库实例中每个销售的详细信息。

你已在 Azure 订阅中实现必要的对象。 现在, 您想要编写将邮件发送到该队列并检索邮件的代码。

## <a name="clone-and-open-the-starter-application"></a>克隆并打开起始应用程序

在此单元中, 将生成两个控制台应用程序。 第一个应用程序将邮件放入服务总线队列, 第二个应用程序将其检索。 应用程序是单个 .net Core 解决方案的一部分。

1. 通过克隆解决方案开始: 在云命令行管理程序中运行以下命令:

```bash
cd ~
git clone https://github.com/MicrosoftDocs/mslearn-connect-services-together.git
```

2. 接下来, 将目录更改为起始文件夹, 然后打开云命令行管理程序编辑器。

```bash
cd mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
code .
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>配置到服务总线命名空间的连接字符串

为了访问服务总线命名空间并使用队列, 您必须在控制台应用程序中配置两条信息:

* 命名空间的终结点
* 用于身份验证的共享访问密钥

这两个值都可以从 Azure 门户获取, 形式为完整的连接字符串。

> [!NOTE]
> 为简单起见, 您将在两个控制台应用程序的**Program.cs**文件中对连接字符串进行硬编码。 在生产应用程序中, 您可以使用配置文件甚至 Azure 密钥存储库来存储连接字符串。

1. 在 CloudShell 中运行以下命令, 以显示服务总线命名空间的主连接字符串。 将`<namespace-name>`替换为服务总线命名空间的名称。

    ```azurecli
    az servicebus namespace authorization-rule keys list \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name RootManageSharedAccessKey \
        --query primaryConnectionString \
        --output tsv \
        --namespace-name <namespace-name>
    ```

    此模块中将多次需要此连接字符串, 因此您可能需要将其粘贴到某个位置。

1. 从云命令行管理程序复制密钥。 在编辑器中, 打开**privatemessagesender/程序 .cs**并找到以下代码行:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    在引号之间粘贴连接字符串。 使用<kbd>Ctrl + S</kbd>键保存文件。

1. 在 " **privatemessagereceiver/Program**" 中重复上述步骤, 在相同的 "连接字符串" 值中粘贴。 通过 "..." 保存文件菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

## <a name="write-code-that-sends-a-message-to-the-queue"></a>编写用于将邮件发送到队列的代码

若要完成发送有关销售的邮件的组件, 请按照以下步骤操作:

1. 在编辑器中打开**privatemessagesender/程序 .cs。**

1. 查找`SendSalesMessageAsync()`方法。

1. 在该方法中, 找到以下代码行:

    ```C#
    // Create a queue client here
    ```

1. 若要创建队列客户端, 请将该行代码替换为以下代码:

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. 在`try...catch`块中, 找到以下代码行:

    ```C#
    // Create and send a message here
    ```

1. 若要为队列创建和设置邮件格式, 请将该行代码替换为以下代码:

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. 若要在控制台中显示邮件, 请在下一行中添加以下代码:

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. 若要将邮件发送到队列, 请在下一行中添加以下代码:

    ```C#
    await queueClient.SendAsync(message);
    ```

1. 找到以下代码行： 

    ```C#
    // Close the connection to the queue here
    ```

1. 若要关闭与服务总线的连接, 请将该行代码替换为以下代码:

    ```C#
    await queueClient.CloseAsync();
    ```

1. 保存该文件。

## <a name="send-a-message-to-the-queue"></a>将邮件发送到队列

若要运行发送有关销售的消息的组件, 请在云命令行管理程序中运行以下命令:

```bash
dotnet run -p privatemessagesender
```

> [!NOTE]
> 您在此练习中运行的应用程序可能需要一段时间才能启动`dotnet` , 就像从远程源还原包并在首次运行应用程序时生成这些应用程序一样。

在程序执行时, 您将看到已打印的邮件, 表明它发送了一封邮件。 每次运行应用程序时, 都会向队列中添加一封其他消息。

完成后, 运行以下命令以查看队列中的邮件数:

```azurecli
az servicebus queue show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name salesmessages \
    --query messageCount \
    --namespace-name <namespace-name>
```

## <a name="write-code-that-receives-a-message-from-the-queue"></a>编写从队列中接收邮件的代码

1. 在编辑器中打开**privatemessagereceiver/程序 .cs**

1. 查找`ReceiveSalesMessageAsync()`方法。

1. 在该方法中, 找到以下代码行:

    ```C#
    // Create a queue client here
    ```

1. 若要创建队列客户端, 请将该行替换为以下代码:

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
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
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. 查找`ProcessMessagesAsync()`方法。 您已将此方法注册为处理传入邮件的方法。

1. 若要在控制台中显示传入的邮件, 请将该方法中的所有代码替换为以下代码:

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. 若要从队列中删除收到的邮件, 请在下一行中添加以下代码:

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. 返回到`ReceiveSalesMessageAsync()`方法并找到以下代码行:

    ```C#
    // Close the queue here
    ```

1. 若要关闭与服务总线的连接, 请将该行替换为以下代码:

    ```C#
    await queueClient.CloseAsync();
    ```

1. 保存该文件。

## <a name="retrieve-a-message-from-the-queue"></a>从队列中检索邮件

若要运行发送有关销售的消息的组件, 请在云命令行管理程序中运行以下命令:

```bash
dotnet run -p privatemessagereceiver
```

当您看到邮件已接收并显示在控制台中时, 按键`Enter`停止应用。 然后, 运行与之前相同的命令, 以确认已从队列中删除了所有邮件:

```azurecli
az servicebus queue show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name salesmessages \
    --query messageCount \
    --namespace-name <namespace-name>
```

这将显示`0`是否已删除所有邮件。

您编写的代码将有关单个销售的消息发送到服务总线队列。 在销售团队分布式应用程序中, 应在销售人员在设备上使用的移动应用中编写此代码。

您还编写了从服务总线队列中接收邮件的代码。 在销售团队分布式应用程序中, 应在运行在 Azure 中的 web 服务中编写此代码并处理收到的邮件。
