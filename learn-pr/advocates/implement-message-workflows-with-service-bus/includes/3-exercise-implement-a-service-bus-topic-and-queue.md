<span data-ttu-id="be8c7-101">假设您有一个适用于全球公司的销售团队的应用程序。</span><span class="sxs-lookup"><span data-stu-id="be8c7-101">Suppose you have an application for the sales team in your global company.</span></span> <span data-ttu-id="be8c7-102">每个团队成员都有一个移动电话, 将在其中安装应用程序。</span><span class="sxs-lookup"><span data-stu-id="be8c7-102">Each team member has a mobile phone where your app will be installed.</span></span> <span data-ttu-id="be8c7-103">azure 中托管的 web 服务实现应用程序的业务逻辑并将信息存储在 azure SQL 数据库中。</span><span class="sxs-lookup"><span data-stu-id="be8c7-103">A web service hosted in Azure implements the business logic for your application and stores information in Azure SQL Database.</span></span> <span data-ttu-id="be8c7-104">每个地理区域都有一个 web 服务实例。</span><span class="sxs-lookup"><span data-stu-id="be8c7-104">There is one instance of the web service for each geographical region.</span></span> <span data-ttu-id="be8c7-105">您已确定在移动应用程序和 web 服务之间发送邮件的以下目的:</span><span class="sxs-lookup"><span data-stu-id="be8c7-105">You have identified the following purposes for sending messages between the mobile app and the web service:</span></span>

- <span data-ttu-id="be8c7-106">与单个销售相关的邮件必须仅发送到用户区域中的 web 服务实例。</span><span class="sxs-lookup"><span data-stu-id="be8c7-106">Messages that relate to individual sales must be sent only to the web service instance in the user's region.</span></span>
- <span data-ttu-id="be8c7-107">必须将与销售业绩相关的邮件发送到 web 服务的所有实例。</span><span class="sxs-lookup"><span data-stu-id="be8c7-107">Messages that relate to sales performance must be sent to all instances of the web service.</span></span>

<span data-ttu-id="be8c7-108">您已决定为第一个用例实现服务总线队列, 为第二个用例实现服务总线主题。</span><span class="sxs-lookup"><span data-stu-id="be8c7-108">You have decided to implement a Service Bus queue for the first use case and the Service Bus topic for the second use case.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="be8c7-109">在本练习中, 将创建一个服务总线命名空间, 该命名空间将包含队列和包含订阅的主题。</span><span class="sxs-lookup"><span data-stu-id="be8c7-109">In this exercise, you will create a Service Bus namespace, which will contain both a queue and a topic with subscriptions.</span></span>

## <a name="create-a-service-bus-namespace"></a><span data-ttu-id="be8c7-110">创建服务总线命名空间</span><span class="sxs-lookup"><span data-stu-id="be8c7-110">Create a Service Bus namespace</span></span>

<span data-ttu-id="be8c7-111">在 Azure 服务总线中, 命名空间是一个容器, 其中包含唯一的完全限定的域名, 用于队列、主题和中继。</span><span class="sxs-lookup"><span data-stu-id="be8c7-111">In Azure Service Bus, a namespace is a container, with a unique fully qualified domain name, for queues, topics, and relays.</span></span> <span data-ttu-id="be8c7-112">必须首先创建命名空间。</span><span class="sxs-lookup"><span data-stu-id="be8c7-112">You must start by creating the namespace.</span></span>

<span data-ttu-id="be8c7-113">每个命名空间都有主要和次要共享访问签名加密密钥。</span><span class="sxs-lookup"><span data-stu-id="be8c7-113">Each namespace has primary and secondary shared access signature encryption keys.</span></span> <span data-ttu-id="be8c7-114">若要获取对命名空间中的对象的访问权限, 发送或接收组件在连接时必须提供这些密钥。</span><span class="sxs-lookup"><span data-stu-id="be8c7-114">To gain access to the objects within the namespace, a sending or receiving component must provide these keys when it connects.</span></span>

<span data-ttu-id="be8c7-115">若要使用 Azure 门户创建服务总线命名空间, 请按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="be8c7-115">To create a Service Bus namespace using the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="be8c7-116">登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="be8c7-116">Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).</span></span>

1. <span data-ttu-id="be8c7-117">在左侧的导航栏中, 单击 "**所有服务**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-117">In the navigation on the left, click **All services**.</span></span>

1. <span data-ttu-id="be8c7-118">在 "**所有服务**" 边栏选项卡中, 向下滚动到 "**集成**" 部分, 然后单击 "**服务总线**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-118">In the **All Services** blade, scroll down to the **INTEGRATION** section, and then click **Service Bus**.</span></span>

    ![显示所有服务总线处于突出显示状态的 "所有服务" 边栏集成部分的屏幕截图](../media/3-create-namespace-1.png)

1. <span data-ttu-id="be8c7-120">在**服务总线**刀片式服务器的左上角, 单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-120">In the top left of the **Service Bus** blade, click **Add**.</span></span>

1. <span data-ttu-id="be8c7-121">在 "**名称**" 文本框中, 键入命名空间的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="be8c7-121">In the **Name** text box, type a unique name for the namespace.</span></span> <span data-ttu-id="be8c7-122">例如: "salesteamapp" +*你的首字母缩写* + *当前日期*。</span><span class="sxs-lookup"><span data-stu-id="be8c7-122">For example: "salesteamapp" + *your initials* + *current date*.</span></span>

1. <span data-ttu-id="be8c7-123">在 "**定价层**" 下拉列表中, 选择 "**标准**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-123">In the **Pricing tier** drop-down list, select **Standard**.</span></span>

1. <span data-ttu-id="be8c7-124">在 "**订阅**" 下拉列表中, 选择您的订阅 ("Concierge 订阅")。</span><span class="sxs-lookup"><span data-stu-id="be8c7-124">In the **Subscription** drop-down list, select your subscription ("Concierge subscription").</span></span>

1. <span data-ttu-id="be8c7-125">在 "**资源组**" 下, 选择 "**使用现有**" 并选择 "<rgn>[沙盒资源组名称]</rgn>"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-125">Under **Resource group**, select **Use existing** and choose "<rgn>[sandbox resource group name]</rgn>".</span></span>

1. <span data-ttu-id="be8c7-126">在 "**位置**" 下拉列表中, 从下面的列表中选择邻近你的位置。</span><span class="sxs-lookup"><span data-stu-id="be8c7-126">In the **Location** drop-down list, select a location near you from the below list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="be8c7-127">单击 "**创建**" 以创建服务总线命名空间。</span><span class="sxs-lookup"><span data-stu-id="be8c7-127">Click **Create** to create the Service Bus namespace.</span></span>

    ![突出显示 "添加" 按钮和 "创建" 按钮的服务总线屏幕截图和创建命名空间刀片](../media/3-create-namespace-2.png)

## <a name="create-a-service-bus-queue"></a><span data-ttu-id="be8c7-129">创建服务总线队列</span><span class="sxs-lookup"><span data-stu-id="be8c7-129">Create a Service Bus queue</span></span>

<span data-ttu-id="be8c7-130">现在您已经有了一个命名空间, 您可以为每个销售的邮件创建队列。</span><span class="sxs-lookup"><span data-stu-id="be8c7-130">Now that you have a namespace, you can create a queue for messages about individual sales.</span></span> <span data-ttu-id="be8c7-131">为此, 请按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="be8c7-131">To do this, follow these steps:</span></span>

1. <span data-ttu-id="be8c7-132">在**服务总线**刀片中, 单击 "**刷新**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-132">In the **Service Bus** blade, click **Refresh**.</span></span> <span data-ttu-id="be8c7-133">将显示您刚创建的命名空间。</span><span class="sxs-lookup"><span data-stu-id="be8c7-133">The namespace you just created is displayed.</span></span>

1. <span data-ttu-id="be8c7-134">单击您刚创建的命名空间。</span><span class="sxs-lookup"><span data-stu-id="be8c7-134">Click the namespace you just created.</span></span>

1. <span data-ttu-id="be8c7-135">在命名空间边栏的左上角, 单击 " **+ 队列**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-135">In the top left of the namespace blade, click **+ Queue**.</span></span>

1. <span data-ttu-id="be8c7-136">在 "**创建队列**边栏" 中的 "**名称**" 文本框中, 键入**salesmessages**, 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-136">In the **Create queue** blade, in the **Name** text box, type **salesmessages**, and then click **Create**.</span></span> <span data-ttu-id="be8c7-137">Azure 在你的命名空间中创建队列。</span><span class="sxs-lookup"><span data-stu-id="be8c7-137">Azure creates the queue in your namespace.</span></span>

    ![突出显示 "创建" 按钮的 "创建队列" 边栏屏幕截图](../media/3-create-queue.png)

## <a name="create-a-service-bus-topic-and-subscriptions"></a><span data-ttu-id="be8c7-139">创建服务总线主题和订阅</span><span class="sxs-lookup"><span data-stu-id="be8c7-139">Create a Service Bus topic and subscriptions</span></span>

<span data-ttu-id="be8c7-140">此外, 您还需要创建一个将用于与销售业绩相关的邮件的主题。</span><span class="sxs-lookup"><span data-stu-id="be8c7-140">You also want to create a topic that will be used for messages that relate to sales performance.</span></span> <span data-ttu-id="be8c7-141">业务逻辑 web 服务的多个实例将订阅来自不同国家/地区的本主题。</span><span class="sxs-lookup"><span data-stu-id="be8c7-141">Multiple instances of the business logic web service will subscribe to this topic from different countries.</span></span> <span data-ttu-id="be8c7-142">每封邮件都将传递给多个实例。</span><span class="sxs-lookup"><span data-stu-id="be8c7-142">Each message will be delivered to multiple instances.</span></span>

<span data-ttu-id="be8c7-143">按照以下步骤操作:</span><span class="sxs-lookup"><span data-stu-id="be8c7-143">Follow these steps:</span></span>

1. <span data-ttu-id="be8c7-144">在**服务总线命名空间**刀片中, 单击 " **+ 主题**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-144">In the **Service Bus Namespace** blade, click **+ Topic**.</span></span>

1. <span data-ttu-id="be8c7-145">在 "**创建主题**边栏" 框的 "**名称**" 文本框中, 键入**salesperformancemessages**, 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-145">In the **Create topic** blade, in the **Name** text box, type **salesperformancemessages**, and then click **Create**.</span></span> <span data-ttu-id="be8c7-146">Azure 在你的命名空间中创建主题。</span><span class="sxs-lookup"><span data-stu-id="be8c7-146">Azure creates the topic in your namespace.</span></span>

    ![突出显示 "创建" 按钮的 "创建主题边栏" 屏幕截图](../media/3-create-topic.png)

1. <span data-ttu-id="be8c7-148">创建主题后, 在 "**服务总线命名空间**" 边栏中的 "**实体**" 下, 单击 "**主题**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-148">When the topic has been created, in the **Service Bus Namespace** blade, under **Entities**, click **Topics**.</span></span>

1. <span data-ttu-id="be8c7-149">在主题列表中, 单击 " **salesperformancemessages**", 然后单击 " **+ 订阅**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-149">In the list of topics, click **salesperformancemessages**, and then click **+ Subscription**.</span></span>

1. <span data-ttu-id="be8c7-150">在 "**名称**" 文本框中, 键入 "**美洲**", 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-150">In the **Name** text box, type **Americas**, and then click **Create**.</span></span>

1. <span data-ttu-id="be8c7-151">单击 " **+ 订阅**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-151">Click **+ Subscription**.</span></span>

1. <span data-ttu-id="be8c7-152">在 "**名称**" 文本框中, 键入**EuropeAndAfrica**, 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="be8c7-152">In the **Name** text box, type **EuropeAndAfrica**, and then click **Create**.</span></span>

<span data-ttu-id="be8c7-153">您已构建了使用服务总线以提高销售团队分布式应用程序的恢复能力所需的基础结构。</span><span class="sxs-lookup"><span data-stu-id="be8c7-153">You have built the infrastructure required to use Service Bus to increase the resilience of your sales force distributed application.</span></span> <span data-ttu-id="be8c7-154">您已为有关单个销售额的邮件创建了队列, 并为有关销售业绩的消息创建了一个主题。</span><span class="sxs-lookup"><span data-stu-id="be8c7-154">You have created a queue for messages about individual sales and a topic for messages about sales performance.</span></span> <span data-ttu-id="be8c7-155">主题包括多个订阅, 因为发送到该主题的邮件可传递到世界各地的多个收件人 web 服务。</span><span class="sxs-lookup"><span data-stu-id="be8c7-155">The topic includes multiple subscriptions because messages sent to that topic can be delivered to multiple recipient web services around the world.</span></span>
