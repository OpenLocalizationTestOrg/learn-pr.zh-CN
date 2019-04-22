在分布式应用程序中, 需要将某些邮件发送到单个收件人组件。 其他邮件需要到达多个目标。

我们来讨论当用户取消比萨饼订单时, 会发生什么情况。 这与置入初始顺序稍有不同。 在这种情况下, 我们希望等到订单清除付款处理之后, 才会将订单发送到后续步骤 (即在本地店面准备和 cooked)。 但对于取消操作, 我们将同时通知店面*和*付款处理器。 此方法可最大限度地减少浪费原料或交付驱动程序时间的机会。

若要允许多个组件接收同一条消息, 我们将使用 Azure 服务总线主题。

## <a name="code-with-topics-vs-code-with-queues"></a>带有队列的主题与代码的代码

如果您希望发送的每封邮件都发送到所有订阅组件, 您将使用主题。 编写使用主题的代码是替换队列的一种方法。 你将使用相同的**Microsoft Azure.** 配置连接字符串和使用异步编程模式。

但是, 您将使用`TopicClient`类 (而不是`QueueClient`类) 来发送邮件和`SubscriptionClient`类以接收邮件。

## <a name="setting-filters-on-subscriptions"></a>在订阅上设置筛选器

如果要控制发送给主题的特定邮件传递给特定订阅, 可以在主题中的每个订阅上放置筛选器。 例如, 在比萨饼应用程序中, 我们的店面运行的是通用 Windows 平台 (UWP) 应用程序。 每个商店都可以订阅 "OrderCancellation" 主题, 但会针对自己的 StoreId 进行筛选。 我们节省 internet 带宽, 因为我们不会将不必要的邮件发送到较远的存储位置。 同时, 付款处理组件会订阅所有取消邮件。

筛选器可以是以下三种类型之一:

- **布尔筛选器。** `TrueFilter`确保发送到该主题的所有邮件都将传递到当前订阅。 `FalseFilter`确保不会将任何邮件传递到当前订阅。 (这将有效阻止或关闭订阅。)
- **SQL 筛选器。** sql 筛选器通过使用与 SQL 查询中的`WHERE`子句相同的语法来指定条件。 只有在对此`True`订阅评估时返回的邮件才会传递给订阅者。
- **关联筛选器。** 关联筛选器具有一组与每个邮件的属性相匹配的条件。 如果筛选器中的属性和邮件中的属性具有相同的值, 则会将其视为匹配。

对于我们的 StoreId 筛选器, 我们*可以*使用 SQL 筛选器。 SQL 筛选器是最灵活的, 但它们也是开销最大的计算开销, 可能会降低服务总线吞吐量。 在这种情况下, 请改为选择关联筛选器。 

## <a name="topicclient-example"></a>TopicClient 示例

在任何发送或接收组件中, 应将以下`using`语句添加到调用服务总线主题的任何代码文件中:

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

若要发送邮件, 请首先创建一个新`TopicClient`对象并向其传递连接字符串和主题名称:

```C#
topicClient = new TopicClient(TextAppConnectionString, "GroupMessageTopic");
```

您可以通过调用`TopicClient.SendAsync()`方法并传递邮件, 向主题发送邮件。 与队列一样, 邮件必须采用 utf-8 编码字符串的形式:

```C#
string message = "Cancel! I can't believe you use canned mushrooms!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await topicClient.SendAsync(encodedMessage);
```

若要接收邮件, 必须创建一个`SubscriptionClient`对象, 而不`TopicClient`是一个对象, 并向其传递连接字符串、主题名称**和**订阅的名称:

```C#
subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, "GroupMessageTopic", "NorthAmerica");
```

然后注册一个消息处理程序-这是代码中处理检索到的消息的异步方法。

```C#
subscriptionClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

在邮件处理程序中, 调用`SubscriptionClient.CompleteAsync()`方法以从队列中删除邮件:

```C#
await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
```