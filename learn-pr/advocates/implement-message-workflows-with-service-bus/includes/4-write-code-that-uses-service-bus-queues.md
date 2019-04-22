<span data-ttu-id="eca51-101">分布式应用程序使用队列 (如服务总线队列) 作为等待传递到目标组件的邮件的临时存储位置。</span><span class="sxs-lookup"><span data-stu-id="eca51-101">Distributed applications use queues, such as Service Bus queues, as temporary storage locations for messages that are awaiting delivery to a destination component.</span></span> <span data-ttu-id="eca51-102">若要通过队列发送和接收邮件, 必须在源和目标组件中编写代码。</span><span class="sxs-lookup"><span data-stu-id="eca51-102">To send and receive messages through a queue, you must write code in the source and destination components.</span></span>

<span data-ttu-id="eca51-103">考虑 Contoso 切片应用程序。</span><span class="sxs-lookup"><span data-stu-id="eca51-103">Consider the Contoso Slices application.</span></span> <span data-ttu-id="eca51-104">客户通过网站或移动应用程序放置订单。</span><span class="sxs-lookup"><span data-stu-id="eca51-104">The customer places the order through a website or mobile app.</span></span> <span data-ttu-id="eca51-105">由于网站和移动应用程序在客户设备上运行, 因此一次可以进入多少个订单是没有限制的。</span><span class="sxs-lookup"><span data-stu-id="eca51-105">Because websites and mobile apps run on customer devices, there is really no limit to how many orders could come in at once.</span></span> <span data-ttu-id="eca51-106">通过让移动应用程序和网站将订单放在队列中, 我们可以允许后端组件 (web 应用) 按自己的步调处理该队列中的订单。</span><span class="sxs-lookup"><span data-stu-id="eca51-106">By having the mobile app and website deposit the orders in a queue, we can allow the back-end component (a web app) to process orders from that queue at its own pace.</span></span>

<span data-ttu-id="eca51-107">Contoso "切片" 应用程序实际上有几个步骤可用于处理新的订单。</span><span class="sxs-lookup"><span data-stu-id="eca51-107">The Contoso Slices application actually has several steps to handle a new order.</span></span> <span data-ttu-id="eca51-108">所有步骤都依赖于首次授权付款, 因此我们决定使用队列。</span><span class="sxs-lookup"><span data-stu-id="eca51-108">All the steps are dependent on first authorizing payment, so we decide to use a queue.</span></span> <span data-ttu-id="eca51-109">我们的接收组件的第一个作业将处理付款。</span><span class="sxs-lookup"><span data-stu-id="eca51-109">Our receiving component's first job will be processing the payment.</span></span>

<span data-ttu-id="eca51-110">在移动应用程序和网站中, Contoso 需要编写代码以将邮件添加到队列中。</span><span class="sxs-lookup"><span data-stu-id="eca51-110">In the mobile app and website, Contoso needs to write code that adds a message to the queue.</span></span> <span data-ttu-id="eca51-111">在后端 web 应用程序中, 他们将编写用于从队列中选取邮件的代码。</span><span class="sxs-lookup"><span data-stu-id="eca51-111">In the back-end web app, they'll write code that picks up messages from the queue.</span></span>

<span data-ttu-id="eca51-112">在这里, 你将了解如何编写该代码。</span><span class="sxs-lookup"><span data-stu-id="eca51-112">Here, you will learn how to write that code.</span></span>

## <a name="the-microsoftazureservicebus-nuget-package"></a><span data-ttu-id="eca51-113">Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="eca51-113">The Microsoft.Azure.ServiceBus NuGet package</span></span>

<span data-ttu-id="eca51-114">为了便于编写通过服务总线发送和接收邮件的代码, Microsoft 提供了一个 .net 类库, 您可以在任何 .net Framework 语言中使用这些类来与服务总线队列、主题或中继进行交互。</span><span class="sxs-lookup"><span data-stu-id="eca51-114">To make it easy to write code that sends and receives messages through Service Bus, Microsoft provides a library of .NET classes, which you can use in any .NET Framework language to interact with a Service Bus queue, topic, or relay.</span></span> <span data-ttu-id="eca51-115">您可以通过添加 the the the the **Azure.** application-Azure 的 NuGet 包将此库包含在应用程序中。</span><span class="sxs-lookup"><span data-stu-id="eca51-115">You can include this library in your application by adding the **Microsoft.Azure.ServiceBus** NuGet package.</span></span>

<span data-ttu-id="eca51-116">此库中用于队列的最重要的类是`QueueClient`类。</span><span class="sxs-lookup"><span data-stu-id="eca51-116">The most important class in this library for queues is the `QueueClient` class.</span></span> <span data-ttu-id="eca51-117">必须首先在发送和接收组件中实例化此类。</span><span class="sxs-lookup"><span data-stu-id="eca51-117">You must start by instantiating this class both in sending and receiving components.</span></span>

## <a name="connection-strings-and-keys"></a><span data-ttu-id="eca51-118">连接字符串和键</span><span class="sxs-lookup"><span data-stu-id="eca51-118">Connection strings and keys</span></span>

<span data-ttu-id="eca51-119">源组件和目标组件都需要两条信息以连接到服务总线命名空间中的队列:</span><span class="sxs-lookup"><span data-stu-id="eca51-119">Source components and destination components both need two pieces of information to connect to a queue in a Service Bus namespace:</span></span>

- <span data-ttu-id="eca51-120">服务总线命名空间 (也称为**终结点**) 的位置。</span><span class="sxs-lookup"><span data-stu-id="eca51-120">The location of the Service Bus namespace, also known as an **endpoint**.</span></span> <span data-ttu-id="eca51-121">该位置指定为**servicebus.windows.net**域中的完全限定的域名。</span><span class="sxs-lookup"><span data-stu-id="eca51-121">The location is specified as a fully qualified domain name within the **servicebus.windows.net** domain.</span></span> <span data-ttu-id="eca51-122">例如: **pizzaService.servicebus.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="eca51-122">For example: **pizzaService.servicebus.windows.net**.</span></span>
- <span data-ttu-id="eca51-123">一个访问键。</span><span class="sxs-lookup"><span data-stu-id="eca51-123">An access key.</span></span> <span data-ttu-id="eca51-124">服务总线通过要求访问键来限制对队列、主题和中继的访问。</span><span class="sxs-lookup"><span data-stu-id="eca51-124">Service Bus restricts access to queues, topics, and relays by requiring an access key.</span></span>

<span data-ttu-id="eca51-125">这两条信息都是以连接字符串的`QueueClient`形式提供给对象的。</span><span class="sxs-lookup"><span data-stu-id="eca51-125">Both of these pieces of information are provided to the `QueueClient` object in the form of a connection string.</span></span> <span data-ttu-id="eca51-126">您可以从 Azure 门户获取命名空间的正确连接字符串。</span><span class="sxs-lookup"><span data-stu-id="eca51-126">You can obtain the correct connection string for your namespace from the Azure portal.</span></span>

## <a name="calling-methods-asynchronously"></a><span data-ttu-id="eca51-127">异步调用方法</span><span class="sxs-lookup"><span data-stu-id="eca51-127">Calling methods asynchronously</span></span>

<span data-ttu-id="eca51-128">Azure 中的队列可能位于发送和接收组件之外的数千英里处。</span><span class="sxs-lookup"><span data-stu-id="eca51-128">The queue in Azure may be located thousands of miles away from sending and receiving components.</span></span> <span data-ttu-id="eca51-129">即使在物理上关闭, 连接速度慢和带宽争用也可能导致组件在队列上调用方法时出现延迟。</span><span class="sxs-lookup"><span data-stu-id="eca51-129">Even if it is physically close, slow connections and bandwidth contention may cause delays when a component calls a method on the queue.</span></span> <span data-ttu-id="eca51-130">出于此原因, 服务总线客户端库会`async`提供可用于与队列交互的方法。</span><span class="sxs-lookup"><span data-stu-id="eca51-130">For this reason, the Service Bus client library makes `async` methods available for interacting with the queues.</span></span> <span data-ttu-id="eca51-131">我们将使用这些方法来避免在等待调用完成的过程中阻止线程。</span><span class="sxs-lookup"><span data-stu-id="eca51-131">We'll use these methods to avoid blocking a thread while waiting for calls to complete.</span></span>

<span data-ttu-id="eca51-132">例如, 将邮件发送到队列时, 将`QueueClient.SendAsync()`方法与`await`关键字一起使用。</span><span class="sxs-lookup"><span data-stu-id="eca51-132">When sending a message to a queue, for example, use the `QueueClient.SendAsync()` method with the `await` keyword.</span></span>

## <a name="write-code-that-sends-to-queues"></a><span data-ttu-id="eca51-133">编写发送到队列的代码</span><span class="sxs-lookup"><span data-stu-id="eca51-133">Write code that sends to queues</span></span>

<span data-ttu-id="eca51-134">在任何发送或接收组件中, 应将以下`using`语句添加到调用服务总线队列的任何代码文件中:</span><span class="sxs-lookup"><span data-stu-id="eca51-134">In any sending or receiving component, you should add the following `using` statements to any code file that calls a Service Bus queue:</span></span>

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

<span data-ttu-id="eca51-135">接下来, 创建一个`QueueClient`新对象并向其传递连接字符串和队列的名称:</span><span class="sxs-lookup"><span data-stu-id="eca51-135">Next, create a new `QueueClient` object and pass it the connection string and the name of the queue:</span></span>

```C#
queueClient = new QueueClient(TextAppConnectionString, "PrivateMessageQueue");
```

<span data-ttu-id="eca51-136">您可以通过调用`QueueClient.SendAsync()`方法并以 utf-8 编码字符串的形式传递邮件, 将邮件发送到队列:</span><span class="sxs-lookup"><span data-stu-id="eca51-136">You can send a message to the queue by calling the `QueueClient.SendAsync()` method and passing the message in the form of a UTF-8 encoded string:</span></span>

```C#
string message = "Sure would like a large pepperoni!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await queueClient.SendAsync(encodedMessage);
```

## <a name="receive-messages-from-the-queue"></a><span data-ttu-id="eca51-137">接收来自队列的邮件</span><span class="sxs-lookup"><span data-stu-id="eca51-137">Receive messages from the queue</span></span>

<span data-ttu-id="eca51-138">若要接收邮件, 必须首先注册消息处理程序-这是代码中的方法, 当队列中有可用消息时将调用该方法。</span><span class="sxs-lookup"><span data-stu-id="eca51-138">To receive messages, you must first register a message handler - this is the method in your code that will be invoked when a message is available on the queue.</span></span>

```C#
queueClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

<span data-ttu-id="eca51-139">您的处理工作。</span><span class="sxs-lookup"><span data-stu-id="eca51-139">Do your processing work.</span></span> <span data-ttu-id="eca51-140">然后, 在邮件处理程序中, 调用`QueueClient.CompleteAsync()`方法以从队列中删除邮件:</span><span class="sxs-lookup"><span data-stu-id="eca51-140">Then, within the message handler, call the `QueueClient.CompleteAsync()` method to remove the message from the queue:</span></span>

```C#
await queueClient.CompleteAsync(message.SystemProperties.LockToken);
```