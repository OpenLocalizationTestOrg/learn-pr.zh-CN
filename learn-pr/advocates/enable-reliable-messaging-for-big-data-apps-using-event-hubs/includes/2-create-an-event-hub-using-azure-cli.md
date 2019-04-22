<span data-ttu-id="b0c8d-101">您的团队已决定利用 Azure 事件中心的功能来管理和处理系统中不断增加的事务量。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-101">Your team has decided to leverage the capabilities of the Azure Event Hubs to manage and process the increasing transaction volumes coming through your system.</span></span>

<span data-ttu-id="b0c8d-102">事件中心是 azure 资源, 因此第一步是在 azure 中创建新集线器, 并将其配置为符合应用程序的特定要求。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-102">An Event Hub is an Azure resource, so your first step is to create a new hub in Azure and configure it to meet the specific requirements of your applications.</span></span>

## <a name="what-is-an-azure-event-hub"></a><span data-ttu-id="b0c8d-103">什么是 Azure 事件中心？</span><span class="sxs-lookup"><span data-stu-id="b0c8d-103">What is an Azure Event Hub?</span></span>

<span data-ttu-id="b0c8d-104">Azure 事件中心是一项基于云的事件处理服务, 能够接收和处理数百万个事件 (每秒)。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-104">Azure Event Hubs is a cloud-based, event-processing service that's capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="b0c8d-105">事件中心充当事件管道的前向门, 在其中接收传入的数据并存储它, 直到处理资源可用。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-105">Event Hubs acts as a front door for an event pipeline, where it receives incoming data and stores it until processing resources are available.</span></span>

<span data-ttu-id="b0c8d-106">将数据发送到事件中心的实体称为 "*发布者*", 从事件中心读取数据的实体称为 "*使用者*" 或 "*订阅*者"。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-106">An entity that sends data to the Event Hubs is called a *publisher* and an entity that reads data from the Event Hubs is called a *consumer* or a *subscriber*.</span></span> <span data-ttu-id="b0c8d-107">Azure 事件中心位于这两个实体之间, 用于划分事件流的生产 (从发布服务器) 和消耗 (到订阅者)。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-107">Azure Event Hubs sits between these two entities to divide the production (from publisher) and consumption (to subscriber) of an event stream.</span></span> <span data-ttu-id="b0c8d-108">这种分离有助于管理事件生产速率高于消耗量的情况。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-108">This decoupling helps to manage scenarios where the rate of event production is much higher than the consumption.</span></span> <span data-ttu-id="b0c8d-109">下图显示了事件中心的角色。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-109">The following illustration shows the role of an Event Hub.</span></span>

![显示在四个发布者和两个订阅者之间放置的 Azure 事件中心的插图。](../media/2-event-hub-overview.png)

### <a name="events"></a><span data-ttu-id="b0c8d-112">事件</span><span class="sxs-lookup"><span data-stu-id="b0c8d-112">Events</span></span>

<span data-ttu-id="b0c8d-113">**事件**是包含通知的小型信息数据包 (*数据报*)。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-113">An **event** is a small packet of information (a *datagram*) that contains a notification.</span></span> <span data-ttu-id="b0c8d-114">事件可以单独发布, 也可以成批发布, 但单个出版物 (个人或批处理) 不能超过 256 KB。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-114">Events can be published individually, or in batches, but a single publication (individual or batch) can't exceed 256 KB.</span></span>

### <a name="publishers-and-subscribers"></a><span data-ttu-id="b0c8d-115">发布服务器和订阅者</span><span class="sxs-lookup"><span data-stu-id="b0c8d-115">Publishers and subscribers</span></span>

<span data-ttu-id="b0c8d-116">事件发布者是可以使用 HTTPS 或高级消息队列协议 (AMQP) 1.0 发送事件的任何应用程序或设备。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-116">Event publishers are any application or device that can send out events using either HTTPS or Advanced Message Queuing Protocol (AMQP) 1.0.</span></span>

<span data-ttu-id="b0c8d-117">对于经常发送数据的发布服务器, AMQP 具有更好的性能。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-117">For publishers that send data frequently, AMQP has the better performance.</span></span> <span data-ttu-id="b0c8d-118">但是, 它会有更高的初始会话开销, 因为必须首先设置持久性双向套接字和传输级别安全性 (TLS) 或 SSL/TLS。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-118">However, it has a higher initial session overhead, because a persistent bidirectional socket and transport level security (TLS) or SSL/TLS has to be set up first.</span></span> 

<span data-ttu-id="b0c8d-119">若要进行更多间歇发布, HTTPS 是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-119">For more intermittent publishing, HTTPS is the better option.</span></span> <span data-ttu-id="b0c8d-120">尽管 HTTPS 对每个请求都需要额外开销, 但没有会话初始化开销。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-120">Though HTTPS requires additional overhead for each request, there isn’t the session initialization overhead.</span></span>

> [!NOTE] 
> <span data-ttu-id="b0c8d-121">使用 Apache Kafka 1.0 和更高版本的客户端版本的基于 Kafka 的现有客户端也可以充当事件中心发布者。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-121">Existing Kafka-based clients, using Apache Kafka 1.0 and newer client versions, can also act as Event Hubs publishers.</span></span>

<span data-ttu-id="b0c8d-122">事件订阅者是使用两种受支持的编程方法之一来接收和处理来自事件中心的事件的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-122">Event subscribers are applications that use one of two supported programmatic methods to receive and process events from an Event Hub.</span></span>

- <span data-ttu-id="b0c8d-123">**EventHubReceiver** -提供有限的管理选项的简单方法。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-123">**EventHubReceiver** - A simple method that provides limited management options.</span></span>
- <span data-ttu-id="b0c8d-124">**EventProcessorHost** -我们稍后将在本模块中使用的一种有效方法。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-124">**EventProcessorHost** - An efficient method that we’ll use later in this module.</span></span>

### <a name="consumer-groups"></a><span data-ttu-id="b0c8d-125">使用者组</span><span class="sxs-lookup"><span data-stu-id="b0c8d-125">Consumer groups</span></span>

<span data-ttu-id="b0c8d-126">事件中心**使用者组**表示事件中心数据流的特定视图。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-126">An Event Hub **consumer group** represents a specific view of an Event Hub data stream.</span></span> <span data-ttu-id="b0c8d-127">通过使用单独的使用者组, 多个订阅者应用程序可以独立处理事件流, 而不会影响其他应用程序。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-127">By using separate consumer groups, multiple subscriber applications can process an event stream independently, and without affecting other applications.</span></span> <span data-ttu-id="b0c8d-128">但是, 不要求使用多个使用者组, 而对于许多应用程序, 单个默认的使用者组就足够了。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-128">However, the use of multiple consumer groups is not a requirement, and for many applications, the single default consumer group is sufficient.</span></span>

### <a name="pricing"></a><span data-ttu-id="b0c8d-129">特价</span><span class="sxs-lookup"><span data-stu-id="b0c8d-129">Pricing</span></span>

<span data-ttu-id="b0c8d-130">Azure 事件中心有三个定价层: Basic、Standard 和专职。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-130">There are three pricing tiers for Azure Event Hubs: Basic, Standard, and Dedicated.</span></span> <span data-ttu-id="b0c8d-131">层的不同之处在于受支持的连接的数量、可用的使用者组数以及吞吐量。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-131">The tiers differ in terms of supported connections, number of available Consumer groups, and throughput.</span></span> <span data-ttu-id="b0c8d-132">使用 Azure CLI 创建事件中心命名空间时, 如果不指定定价层, 则分配默认的**标准**(20 个使用者组、1000个连接)。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-132">When using Azure CLI to create an Event Hubs namespace, if you don't specify a pricing tier, the default of **Standard** (20 Consumer groups, 1000 Brokered connections) is assigned.</span></span>

## <a name="creating-and-configuring-a-new-azure-event-hubs"></a><span data-ttu-id="b0c8d-133">创建和配置新的 Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="b0c8d-133">Creating and configuring a new Azure Event Hubs</span></span>

<span data-ttu-id="b0c8d-134">创建和配置新的 Azure 事件中心时有两个主要步骤。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-134">There are two main steps when creating and configuring a new Azure Event Hubs.</span></span> <span data-ttu-id="b0c8d-135">第一步是定义事件中心**命名空间**。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-135">The first step is to define an Event Hubs **namespace**.</span></span> <span data-ttu-id="b0c8d-136">第二步是在该命名空间中创建事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-136">The second step is to create an Event Hub in that namespace.</span></span>

### <a name="defining-an-event-hubs-namespace"></a><span data-ttu-id="b0c8d-137">定义事件中心命名空间</span><span class="sxs-lookup"><span data-stu-id="b0c8d-137">Defining an Event Hubs namespace</span></span>

<span data-ttu-id="b0c8d-138">事件中心命名空间是用于管理一个或多个事件中心的包含实体。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-138">An Event Hubs namespace is a containing entity for managing one or more Event Hubs.</span></span> <span data-ttu-id="b0c8d-139">创建事件中心命名空间通常涉及以下内容:</span><span class="sxs-lookup"><span data-stu-id="b0c8d-139">Creating an Event Hubs namespace typically involves the following:</span></span>

1. <span data-ttu-id="b0c8d-140">定义命名空间级设置。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-140">Defining namespace-level settings.</span></span> <span data-ttu-id="b0c8d-141">某些设置 (如命名空间容量配置使用**吞吐量单位**)、定价层和性能指标在命名空间级定义。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-141">Certain settings such as namespace capacity (configured using **throughput units**), pricing tier, and performance metrics are defined at the namespace level.</span></span> <span data-ttu-id="b0c8d-142">这些应用程序适用于该命名空间中的所有事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-142">These are applicable for all the Event Hubs within that namespace.</span></span> <span data-ttu-id="b0c8d-143">如果未定义这些设置, 则将使用默认值: *1*表示价格层的容量和*标准*。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-143">If you don't define these settings, a default value is used: *1* for capacity and *Standard* for pricing tier.</span></span>

    <span data-ttu-id="b0c8d-144">一旦设置了吞吐量单位, 就不能再对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-144">You cannot change the throughput unit once you set it.</span></span> <span data-ttu-id="b0c8d-145">您必须将您的配置与您的 Azure 预算预期进行权衡。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-145">You must balance your configuration against your Azure budget expectations.</span></span> <span data-ttu-id="b0c8d-146">您可以考虑为不同的吞吐量要求配置不同的事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-146">You might consider configuring different Event Hubs for different throughput requirements.</span></span> <span data-ttu-id="b0c8d-147">例如, 如果您有一个销售数据应用程序, 并且正在规划两个事件中心, 一个用于实时销售数据遥测的高吞吐量集合, 另一个用于不经常发生的事件日志收集, 则对每个中心使用单独的命名空间是有意义的。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-147">For example, if you have a sales data application and you are planning for two Event Hubs, one for high throughput collection of real-time sales data telemetry and one for infrequent event log collection, it would make sense to use a separate namespace for each hub.</span></span> <span data-ttu-id="b0c8d-148">这样一来, 您只需在遥测集线器上配置 (和支付) 高吞吐量容量。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-148">This way you only need to configure (and pay for) high throughput capacity on the telemetry hub.</span></span>

1. <span data-ttu-id="b0c8d-149">为命名空间选择唯一名称。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-149">Selecting a unique name for the namespace.</span></span> <span data-ttu-id="b0c8d-150">可通过此 url 访问命名空间: \* __ servicebus.windows.net\*</span><span class="sxs-lookup"><span data-stu-id="b0c8d-150">The namespace is accessible through this url: *_namespace_.servicebus.windows.net*</span></span>

1. <span data-ttu-id="b0c8d-151">定义以下可选属性:</span><span class="sxs-lookup"><span data-stu-id="b0c8d-151">Defining the following optional properties:</span></span>

    - <span data-ttu-id="b0c8d-152">启用 Kafka。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-152">Enable Kafka.</span></span> <span data-ttu-id="b0c8d-153">此选项使 Kafka 应用程序能够将事件发布到事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-153">This option enables Kafka applications to publish events to the Event Hub.</span></span>
    - <span data-ttu-id="b0c8d-154">将此命名空间区域设为冗余。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-154">Make this namespace zone redundant.</span></span> <span data-ttu-id="b0c8d-155">区域冗余跨不同的数据中心复制数据, 其自身独立的电源、网络和冷却基础结构。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-155">Zone-redundancy replicates data across separate data centers with their own independent power, networking, and cooling infrastructures.</span></span>
    - <span data-ttu-id="b0c8d-156">启用自动大吞吐量和自动放入最大吞吐量单位。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-156">Enable Auto-Inflate, and Auto-Inflate Maximum Throughput Units.</span></span> <span data-ttu-id="b0c8d-157">通过将吞吐量单位的数量增加到最大值, 自动扩展可提供自动向上扩展选项。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-157">Auto-Inflate provides an automatic scale-up option, by increasing the number of throughput units up to a maximum value.</span></span> <span data-ttu-id="b0c8d-158">这有助于避免在传入或传出数据速率超出当前设置的吞吐量单位的情况下进行限制。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-158">This is useful to avoid throttling in situations when incoming or outgoing data rates exceed the currently set number of throughput units.</span></span>

### <a name="azure-cli-commands-for-creating-an-event-hubs-namespace"></a><span data-ttu-id="b0c8d-159">用于创建事件中心命名空间的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="b0c8d-159">Azure CLI commands for creating an Event Hubs namespace</span></span>

<span data-ttu-id="b0c8d-160">若要创建新的事件中心命名空间, 您将`az eventhubs namespace`使用这些命令。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-160">To create a new Event Hubs namespace, you will use the `az eventhubs namespace` commands.</span></span> <span data-ttu-id="b0c8d-161">以下是我们将在练习中使用的子命令的简短说明。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-161">Here's a brief description of the sub-commands we will use in the exercise.</span></span>

| <span data-ttu-id="b0c8d-162">指挥</span><span class="sxs-lookup"><span data-stu-id="b0c8d-162">Command</span></span> | <span data-ttu-id="b0c8d-163">说明</span><span class="sxs-lookup"><span data-stu-id="b0c8d-163">Description</span></span> |
|---------|-------------|
| `create` | <span data-ttu-id="b0c8d-164">创建事件中心命名空间。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-164">Create the Event Hubs namespace.</span></span> |
| `authorization-rule` | <span data-ttu-id="b0c8d-165">同一事件中心命名空间中的所有事件中心共享公用连接凭据。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-165">All Event Hubs within the same Event Hubs namespace share common connection credentials.</span></span> <span data-ttu-id="b0c8d-166">当您将应用程序配置为使用事件中心发送和接收邮件时, 将需要这些凭据。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-166">You will need these credentials when you configure applications to send and receive messages using the Event Hub.</span></span> <span data-ttu-id="b0c8d-167">此命令返回事件中心命名空间的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-167">This command returns the connection string for your Event Hubs namespace.</span></span> |

### <a name="configuring-a-new-event-hub"></a><span data-ttu-id="b0c8d-168">配置新的事件中心</span><span class="sxs-lookup"><span data-stu-id="b0c8d-168">Configuring a new Event Hub</span></span>

<span data-ttu-id="b0c8d-169">创建事件中心命名空间后, 可以创建事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-169">After the Event Hubs namespace has been created, you can create an Event Hub.</span></span> <span data-ttu-id="b0c8d-170">创建新的事件中心时, 有几个强制参数。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-170">When creating a new Event Hub, there are several mandatory parameters.</span></span>

<span data-ttu-id="b0c8d-171">创建事件中心需要以下参数:</span><span class="sxs-lookup"><span data-stu-id="b0c8d-171">The following parameters are required to create an Event Hub:</span></span>

- <span data-ttu-id="b0c8d-172">**事件中心名称**-在订阅中唯一的事件中心名称和:</span><span class="sxs-lookup"><span data-stu-id="b0c8d-172">**Event Hub name** - Event Hub name that is unique within your subscription and:</span></span>
  - <span data-ttu-id="b0c8d-173">长度介于1到50个字符之间</span><span class="sxs-lookup"><span data-stu-id="b0c8d-173">Is between 1 and 50 characters long</span></span>
  - <span data-ttu-id="b0c8d-174">仅包含字母、数字、句点、连字符和下划线</span><span class="sxs-lookup"><span data-stu-id="b0c8d-174">Contains only letters, numbers, periods, hyphens, and underscores</span></span>
  - <span data-ttu-id="b0c8d-175">以字母或数字开头和结尾</span><span class="sxs-lookup"><span data-stu-id="b0c8d-175">Starts and ends with a letter or number</span></span>
- <span data-ttu-id="b0c8d-176">**分区计数**-事件中心中所需的分区数 (介于2和32之间)。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-176">**Partition Count** -  The number of partitions required in an Event Hub (between 2 and 32).</span></span> <span data-ttu-id="b0c8d-177">应直接与预期的并发使用者数相关。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-177">This should be directly related to the expected number of concurrent consumers.</span></span> <span data-ttu-id="b0c8d-178">创建中心后, 不能更改此字段。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-178">This cannot be changed after the hub has been created.</span></span> <span data-ttu-id="b0c8d-179">分区将分隔邮件流, 以便使用者或接收器应用程序只需读取数据流的特定子集。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-179">The partition separates the message stream, so that consumer or receiver applications only need to read a specific subset of the data stream.</span></span> <span data-ttu-id="b0c8d-180">如果未定义, 则默认值为*4*。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-180">If not defined, this defaults to *4*.</span></span>
- <span data-ttu-id="b0c8d-181">**邮件保留**时间 (1 到7之间的天数), 如果由于某种原因需要重播数据流, 则邮件将保持可用。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-181">**Message Retention** - The number of days (between 1 and 7) that messages will remain available, if the data stream needs to be replayed for any reason.</span></span> <span data-ttu-id="b0c8d-182">如果未定义, 则默认为*7*。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-182">If not defined, this defaults to *7*.</span></span>

<span data-ttu-id="b0c8d-183">您还可以选择将事件中心配置为将数据流式传输到 azure Blob 存储或 azure data Lake store 帐户。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-183">You can also optionally configure an Event Hub to stream data to an Azure Blob storage or Azure Data Lake Store account.</span></span>

### <a name="azure-cli-commands-for-creating-an-event-hub"></a><span data-ttu-id="b0c8d-184">用于创建事件中心的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="b0c8d-184">Azure CLI commands for creating an Event Hub</span></span>

<span data-ttu-id="b0c8d-185">若要使用 Azure CLI 创建新的事件中心, 您需要使用`az eventhubs eventhub`命令集。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-185">To create a new Event Hub with the Azure CLI, you will use the `az eventhubs eventhub` command set.</span></span> <span data-ttu-id="b0c8d-186">以下是我们将使用的子命令的简要说明:</span><span class="sxs-lookup"><span data-stu-id="b0c8d-186">Here's a brief description of the sub-commands we will be using:</span></span>

| <span data-ttu-id="b0c8d-187">指挥</span><span class="sxs-lookup"><span data-stu-id="b0c8d-187">Command</span></span> | <span data-ttu-id="b0c8d-188">说明</span><span class="sxs-lookup"><span data-stu-id="b0c8d-188">Description</span></span> |
|---------|-------------|
| `create` | <span data-ttu-id="b0c8d-189">这将在指定的命名空间中创建事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-189">This creates the Event Hub in a specified namespace.</span></span> |
| `show` | <span data-ttu-id="b0c8d-190">这将显示事件中心的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-190">This displays the details of your Event Hub.</span></span> |

## <a name="summary"></a><span data-ttu-id="b0c8d-191">摘要</span><span class="sxs-lookup"><span data-stu-id="b0c8d-191">Summary</span></span>

<span data-ttu-id="b0c8d-192">若要部署 Azure 事件中心, 必须配置事件中心命名空间, 然后配置事件中心本身。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-192">To deploy Azure Event Hubs, you must configure an Event Hubs namespace and then configure the Event Hub itself.</span></span> <span data-ttu-id="b0c8d-193">在下一节中, 您将完成详细的配置步骤, 以创建新的命名空间和事件中心。</span><span class="sxs-lookup"><span data-stu-id="b0c8d-193">In the next section, you will go through the detailed configuration steps to create a new namespace and Event Hub.</span></span>