<span data-ttu-id="0cdda-101">在分布式应用程序中, 需要将某些邮件发送到单个收件人组件。</span><span class="sxs-lookup"><span data-stu-id="0cdda-101">In a distributed application, some messages need to be sent to a single recipient component.</span></span> <span data-ttu-id="0cdda-102">其他邮件需要到达多个目标。</span><span class="sxs-lookup"><span data-stu-id="0cdda-102">Other messages need to reach more than one destination.</span></span>

<span data-ttu-id="0cdda-103">我们来讨论当用户取消比萨饼订单时, 会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="0cdda-103">Let's discuss what happens when a user cancels a pizza order.</span></span> <span data-ttu-id="0cdda-104">这与置入初始顺序稍有不同。</span><span class="sxs-lookup"><span data-stu-id="0cdda-104">This is a little different than placing the initial order.</span></span> <span data-ttu-id="0cdda-105">在这种情况下, 我们希望等到订单清除付款处理之后, 才会将订单发送到后续步骤 (即在本地店面准备和 cooked)。</span><span class="sxs-lookup"><span data-stu-id="0cdda-105">In that case, we wanted to wait until the order cleared payment processing before sending the order on to the next steps (which is having it prepared and cooked at the local storefront).</span></span> <span data-ttu-id="0cdda-106">但对于取消操作, 我们将同时通知店面*和*付款处理器。</span><span class="sxs-lookup"><span data-stu-id="0cdda-106">But for the cancel operation, we are going to notify both the storefront *and* the payment processor at the same time.</span></span> <span data-ttu-id="0cdda-107">此方法可最大限度地减少浪费原料或交付驱动程序时间的机会。</span><span class="sxs-lookup"><span data-stu-id="0cdda-107">This approach minimizes the chances that we waste ingredients or delivery driver time.</span></span>

<span data-ttu-id="0cdda-108">若要允许多个组件接收同一条消息, 我们将使用 Azure 服务总线主题。</span><span class="sxs-lookup"><span data-stu-id="0cdda-108">To allow multiple components to receive the same message, we'll use an Azure Service Bus topic.</span></span>

## <a name="code-with-topics-vs-code-with-queues"></a><span data-ttu-id="0cdda-109">带有队列的主题与代码的代码</span><span class="sxs-lookup"><span data-stu-id="0cdda-109">Code with topics vs. code with queues</span></span>

<span data-ttu-id="0cdda-110">如果您希望发送的每封邮件都发送到所有订阅组件, 您将使用主题。</span><span class="sxs-lookup"><span data-stu-id="0cdda-110">If you want every message sent to be delivered to all subscribing components, you'll use topics.</span></span> <span data-ttu-id="0cdda-111">编写使用主题的代码是替换队列的一种方法。</span><span class="sxs-lookup"><span data-stu-id="0cdda-111">Writing code that uses topics is a way to replace queues.</span></span> <span data-ttu-id="0cdda-112">你将使用相同的**Microsoft Azure.** 配置连接字符串和使用异步编程模式。</span><span class="sxs-lookup"><span data-stu-id="0cdda-112">You will use the same **Microsoft.Azure.ServiceBus** NuGet package, configure connection strings, and use asynchronous programming patterns.</span></span>

<span data-ttu-id="0cdda-113">但是, 您将使用`TopicClient`类 (而不是`QueueClient`类) 来发送邮件和`SubscriptionClient`类以接收邮件。</span><span class="sxs-lookup"><span data-stu-id="0cdda-113">However, you'll use the `TopicClient` class instead of the `QueueClient` class to send messages and the `SubscriptionClient` class to receive messages.</span></span>

## <a name="setting-filters-on-subscriptions"></a><span data-ttu-id="0cdda-114">在订阅上设置筛选器</span><span class="sxs-lookup"><span data-stu-id="0cdda-114">Setting filters on subscriptions</span></span>

<span data-ttu-id="0cdda-115">如果要控制发送给主题的特定邮件传递给特定订阅, 可以在主题中的每个订阅上放置筛选器。</span><span class="sxs-lookup"><span data-stu-id="0cdda-115">If you want to control that specific messages sent to the topic are delivered to particular subscriptions, you can place filters on each subscription in the topic.</span></span> <span data-ttu-id="0cdda-116">例如, 在比萨饼应用程序中, 我们的店面运行的是通用 Windows 平台 (UWP) 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0cdda-116">In the pizza application, for instance, our storefronts are running Universal Windows Platform (UWP) applications.</span></span> <span data-ttu-id="0cdda-117">每个商店都可以订阅 "OrderCancellation" 主题, 但会针对自己的 StoreId 进行筛选。</span><span class="sxs-lookup"><span data-stu-id="0cdda-117">Each store can subscribe to the "OrderCancellation" topic but filter for its own StoreId.</span></span> <span data-ttu-id="0cdda-118">我们节省 internet 带宽, 因为我们不会将不必要的邮件发送到较远的存储位置。</span><span class="sxs-lookup"><span data-stu-id="0cdda-118">We save internet bandwidth because we are not sending unnecessary messages to distant store locations.</span></span> <span data-ttu-id="0cdda-119">同时, 付款处理组件会订阅所有取消邮件。</span><span class="sxs-lookup"><span data-stu-id="0cdda-119">Meanwhile, the payment processing component subscribes to all our cancellation messages.</span></span>

<span data-ttu-id="0cdda-120">筛选器可以是以下三种类型之一:</span><span class="sxs-lookup"><span data-stu-id="0cdda-120">Filters can be one of three types:</span></span>

- <span data-ttu-id="0cdda-121">**布尔筛选器。**</span><span class="sxs-lookup"><span data-stu-id="0cdda-121">**Boolean Filters.**</span></span> <span data-ttu-id="0cdda-122">`TrueFilter`确保发送到该主题的所有邮件都将传递到当前订阅。</span><span class="sxs-lookup"><span data-stu-id="0cdda-122">The `TrueFilter` ensures that all messages sent to the topic are delivered to the current subscription.</span></span> <span data-ttu-id="0cdda-123">`FalseFilter`确保不会将任何邮件传递到当前订阅。</span><span class="sxs-lookup"><span data-stu-id="0cdda-123">The `FalseFilter` ensures that none of the messages are delivered to the current subscription.</span></span> <span data-ttu-id="0cdda-124">(这将有效阻止或关闭订阅。)</span><span class="sxs-lookup"><span data-stu-id="0cdda-124">(This effectively blocks or switches off the subscription.)</span></span>
- <span data-ttu-id="0cdda-125">**SQL 筛选器。**</span><span class="sxs-lookup"><span data-stu-id="0cdda-125">**SQL Filters.**</span></span> <span data-ttu-id="0cdda-126">sql 筛选器通过使用与 SQL 查询中的`WHERE`子句相同的语法来指定条件。</span><span class="sxs-lookup"><span data-stu-id="0cdda-126">A SQL filter specifies a condition by using the same syntax as a `WHERE` clause in a SQL query.</span></span> <span data-ttu-id="0cdda-127">只有在对此`True`订阅评估时返回的邮件才会传递给订阅者。</span><span class="sxs-lookup"><span data-stu-id="0cdda-127">Only messages that return `True` when evaluated against this subscription will be delivered to the subscribers.</span></span>
- <span data-ttu-id="0cdda-128">**关联筛选器。**</span><span class="sxs-lookup"><span data-stu-id="0cdda-128">**Correlation Filters.**</span></span> <span data-ttu-id="0cdda-129">关联筛选器具有一组与每个邮件的属性相匹配的条件。</span><span class="sxs-lookup"><span data-stu-id="0cdda-129">A correlation filter holds a set of conditions that are matched against the properties of each message.</span></span> <span data-ttu-id="0cdda-130">如果筛选器中的属性和邮件中的属性具有相同的值, 则会将其视为匹配。</span><span class="sxs-lookup"><span data-stu-id="0cdda-130">If the property in the filter and the property on the message have the same value, it is considered a match.</span></span>

<span data-ttu-id="0cdda-131">对于我们的 StoreId 筛选器, 我们*可以*使用 SQL 筛选器。</span><span class="sxs-lookup"><span data-stu-id="0cdda-131">For our StoreId filter, we *could* use a SQL filter.</span></span> <span data-ttu-id="0cdda-132">SQL 筛选器是最灵活的, 但它们也是开销最大的计算开销, 可能会降低服务总线吞吐量。</span><span class="sxs-lookup"><span data-stu-id="0cdda-132">SQL filters are the most flexible, but they're also the most computationally expensive and could slow down our Service Bus throughput.</span></span> <span data-ttu-id="0cdda-133">在这种情况下, 请改为选择关联筛选器。</span><span class="sxs-lookup"><span data-stu-id="0cdda-133">In this case, we choose a correlation filter instead.</span></span> 

## <a name="topicclient-example"></a><span data-ttu-id="0cdda-134">TopicClient 示例</span><span class="sxs-lookup"><span data-stu-id="0cdda-134">TopicClient example</span></span>

<span data-ttu-id="0cdda-135">在任何发送或接收组件中, 应将以下`using`语句添加到调用服务总线主题的任何代码文件中:</span><span class="sxs-lookup"><span data-stu-id="0cdda-135">In any sending or receiving component, you should add the following `using` statements to any code file that calls a Service Bus topic:</span></span>

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

<span data-ttu-id="0cdda-136">若要发送邮件, 请首先创建一个新`TopicClient`对象并向其传递连接字符串和主题名称:</span><span class="sxs-lookup"><span data-stu-id="0cdda-136">To send a message, start by creating a new `TopicClient` object and passing it the connection string and the name of the topic:</span></span>

```C#
topicClient = new TopicClient(TextAppConnectionString, "GroupMessageTopic");
```

<span data-ttu-id="0cdda-137">您可以通过调用`TopicClient.SendAsync()`方法并传递邮件, 向主题发送邮件。</span><span class="sxs-lookup"><span data-stu-id="0cdda-137">You can send a message to the topic by calling the `TopicClient.SendAsync()` method and passing the message.</span></span> <span data-ttu-id="0cdda-138">与队列一样, 邮件必须采用 utf-8 编码字符串的形式:</span><span class="sxs-lookup"><span data-stu-id="0cdda-138">As with queues, the message must be in the form of a UTF-8 encoded string:</span></span>

```C#
string message = "Cancel! I can't believe you use canned mushrooms!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await topicClient.SendAsync(encodedMessage);
```

<span data-ttu-id="0cdda-139">若要接收邮件, 必须创建一个`SubscriptionClient`对象, 而不`TopicClient`是一个对象, 并向其传递连接字符串、主题名称**和**订阅的名称:</span><span class="sxs-lookup"><span data-stu-id="0cdda-139">To receive messages, you must create a `SubscriptionClient` object, not a `TopicClient` object, and pass it the connection string, the name of the topic, **and** the name of the subscription:</span></span>

```C#
subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, "GroupMessageTopic", "NorthAmerica");
```

<span data-ttu-id="0cdda-140">然后注册一个消息处理程序-这是代码中处理检索到的消息的异步方法。</span><span class="sxs-lookup"><span data-stu-id="0cdda-140">Then register a message handler - this is the asynchronous method in your code that processes the retrieved message.</span></span>

```C#
subscriptionClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

<span data-ttu-id="0cdda-141">在邮件处理程序中, 调用`SubscriptionClient.CompleteAsync()`方法以从队列中删除邮件:</span><span class="sxs-lookup"><span data-stu-id="0cdda-141">Within the message handler, call the `SubscriptionClient.CompleteAsync()` method to remove the message from the queue:</span></span>

```C#
await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
```