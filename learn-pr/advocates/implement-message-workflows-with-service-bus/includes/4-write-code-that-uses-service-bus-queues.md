分布式应用程序使用队列 (如服务总线队列) 作为等待传递到目标组件的邮件的临时存储位置。 若要通过队列发送和接收邮件, 必须在源和目标组件中编写代码。

考虑 Contoso 切片应用程序。 客户通过网站或移动应用程序放置订单。 由于网站和移动应用程序在客户设备上运行, 因此一次可以进入多少个订单是没有限制的。 通过让移动应用程序和网站将订单放在队列中, 我们可以允许后端组件 (web 应用) 按自己的步调处理该队列中的订单。

Contoso "切片" 应用程序实际上有几个步骤可用于处理新的订单。 所有步骤都依赖于首次授权付款, 因此我们决定使用队列。 我们的接收组件的第一个作业将处理付款。

在移动应用程序和网站中, Contoso 需要编写代码以将邮件添加到队列中。 在后端 web 应用程序中, 他们将编写用于从队列中选取邮件的代码。

在这里, 你将了解如何编写该代码。

## <a name="the-microsoftazureservicebus-nuget-package"></a>Microsoft Azure。

为了便于编写通过服务总线发送和接收邮件的代码, Microsoft 提供了一个 .net 类库, 您可以在任何 .net Framework 语言中使用这些类来与服务总线队列、主题或中继进行交互。 您可以通过添加 the the the the **Azure.** application-Azure 的 NuGet 包将此库包含在应用程序中。

此库中用于队列的最重要的类是`QueueClient`类。 必须首先在发送和接收组件中实例化此类。

## <a name="connection-strings-and-keys"></a>连接字符串和键

源组件和目标组件都需要两条信息以连接到服务总线命名空间中的队列:

- 服务总线命名空间 (也称为**终结点**) 的位置。 该位置指定为**servicebus.windows.net**域中的完全限定的域名。 例如: **pizzaService.servicebus.windows.net**。
- 一个访问键。 服务总线通过要求访问键来限制对队列、主题和中继的访问。

这两条信息都是以连接字符串的`QueueClient`形式提供给对象的。 您可以从 Azure 门户获取命名空间的正确连接字符串。

## <a name="calling-methods-asynchronously"></a>异步调用方法

Azure 中的队列可能位于发送和接收组件之外的数千英里处。 即使在物理上关闭, 连接速度慢和带宽争用也可能导致组件在队列上调用方法时出现延迟。 出于此原因, 服务总线客户端库会`async`提供可用于与队列交互的方法。 我们将使用这些方法来避免在等待调用完成的过程中阻止线程。

例如, 将邮件发送到队列时, 将`QueueClient.SendAsync()`方法与`await`关键字一起使用。

## <a name="write-code-that-sends-to-queues"></a>编写发送到队列的代码

在任何发送或接收组件中, 应将以下`using`语句添加到调用服务总线队列的任何代码文件中:

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

接下来, 创建一个`QueueClient`新对象并向其传递连接字符串和队列的名称:

```C#
queueClient = new QueueClient(TextAppConnectionString, "PrivateMessageQueue");
```

您可以通过调用`QueueClient.SendAsync()`方法并以 utf-8 编码字符串的形式传递邮件, 将邮件发送到队列:

```C#
string message = "Sure would like a large pepperoni!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await queueClient.SendAsync(encodedMessage);
```

## <a name="receive-messages-from-the-queue"></a>接收来自队列的邮件

若要接收邮件, 必须首先注册消息处理程序-这是代码中的方法, 当队列中有可用消息时将调用该方法。

```C#
queueClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

您的处理工作。 然后, 在邮件处理程序中, 调用`QueueClient.CompleteAsync()`方法以从队列中删除邮件:

```C#
await queueClient.CompleteAsync(message.SystemProperties.LockToken);
```