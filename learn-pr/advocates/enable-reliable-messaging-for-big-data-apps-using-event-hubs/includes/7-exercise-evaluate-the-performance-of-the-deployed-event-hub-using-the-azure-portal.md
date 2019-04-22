<span data-ttu-id="ea0be-101">在此单元中, 你将使用 Azure 门户验证你的事件中心是否正在工作并根据所需的预期执行。</span><span class="sxs-lookup"><span data-stu-id="ea0be-101">In this unit, you'll use the Azure portal to verify your Event Hub is working and performing according to the desired expectations.</span></span> <span data-ttu-id="ea0be-102">您还将测试事件中心邮件在暂时不可用时的工作方式, 并使用事件中心指标检查事件中心的性能。</span><span class="sxs-lookup"><span data-stu-id="ea0be-102">You'll also test how Event Hub messaging works when it's temporarily unavailable and use Event Hubs metrics to check the performance of your Event Hub.</span></span>

## <a name="view-event-hub-activity"></a><span data-ttu-id="ea0be-103">查看事件中心活动</span><span class="sxs-lookup"><span data-stu-id="ea0be-103">View Event Hub activity</span></span>

1. <span data-ttu-id="ea0be-104">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="ea0be-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="ea0be-105">使用搜索栏查找事件中心并将其打开。</span><span class="sxs-lookup"><span data-stu-id="ea0be-105">Find your Event Hub, using the Search bar, and open it.</span></span>

1. <span data-ttu-id="ea0be-106">在 "概述" 页上, 查看邮件数。</span><span class="sxs-lookup"><span data-stu-id="ea0be-106">On the Overview page, view the message counts.</span></span>

    ![显示具有邮件计数的事件中心命名空间的 Azure 门户屏幕截图](../media/6-view-messages.png)

1. <span data-ttu-id="ea0be-108">SimpleSend 和 EventProcessorSample 应用程序配置为发送/接收100消息。</span><span class="sxs-lookup"><span data-stu-id="ea0be-108">The SimpleSend and EventProcessorSample applications are configured to send/receive 100 messages.</span></span> <span data-ttu-id="ea0be-109">您将看到事件中心已处理 SimpleSend 应用程序中的100邮件, 并已将100邮件传输到 EventProcessorSample 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea0be-109">You'll see that the Event Hub has processed 100 messages from the SimpleSend application and has transmitted 100 messages to the EventProcessorSample application.</span></span>

## <a name="test-event-hub-resilience"></a><span data-ttu-id="ea0be-110">测试事件中心恢复能力</span><span class="sxs-lookup"><span data-stu-id="ea0be-110">Test Event Hub resilience</span></span>

<span data-ttu-id="ea0be-111">使用以下步骤可查看当应用程序在事件中心暂时不可用时向其发送邮件时, 会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="ea0be-111">Use the following steps to see what happens when an application sends messages to an Event Hub while it's temporarily unavailable.</span></span>

1. <span data-ttu-id="ea0be-112">使用 SimpleSend 应用程序将邮件重新发送到事件中心。</span><span class="sxs-lookup"><span data-stu-id="ea0be-112">Resend messages to the Event Hub using the SimpleSend application.</span></span> <span data-ttu-id="ea0be-113">使用以下命令:</span><span class="sxs-lookup"><span data-stu-id="ea0be-113">Use the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="ea0be-114">如果看到 "**发送完成 ...**", 请按<kbd>enter</kbd>。</span><span class="sxs-lookup"><span data-stu-id="ea0be-114">When you see **Send Complete...**, press <kbd>ENTER</kbd>.</span></span>

1. <span data-ttu-id="ea0be-115">在**概述**屏幕中选择事件中心-这将显示特定于事件中心的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ea0be-115">Select your Event Hub in the **Overview** screen - this will show details specific to the Event Hub.</span></span> <span data-ttu-id="ea0be-116">您还可以通过命名空间页面中的**事件中心**条目访问此屏幕。</span><span class="sxs-lookup"><span data-stu-id="ea0be-116">You can also get to this screen through the **Event Hubs** entry from the namespace page.</span></span>

1. <span data-ttu-id="ea0be-117">选择 "**设置** > **属性**"。</span><span class="sxs-lookup"><span data-stu-id="ea0be-117">Select **Settings** > **Properties**.</span></span>

1. <span data-ttu-id="ea0be-118">在事件中心状态下, 单击 "**禁用**"。</span><span class="sxs-lookup"><span data-stu-id="ea0be-118">Under Event Hub state, click **Disabled**.</span></span> <span data-ttu-id="ea0be-119">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="ea0be-119">Save the changes.</span></span>

    ![禁用事件中心](../media/7-disable-event-hub.png)

    <span data-ttu-id="ea0be-121">**等待至少5分钟。**</span><span class="sxs-lookup"><span data-stu-id="ea0be-121">**Wait for a minimum of five minutes.**</span></span>

1. <span data-ttu-id="ea0be-122">单击 "事件中心状态" 下的 "**活动**" 以重新启用事件中心并保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="ea0be-122">Click **Active** under Event Hub state to re-enable your Event Hub and save your changes.</span></span>

1. <span data-ttu-id="ea0be-123">重新运行 EventProcessorSample 应用程序以接收邮件。</span><span class="sxs-lookup"><span data-stu-id="ea0be-123">Rerun the EventProcessorSample application to receive messages.</span></span> <span data-ttu-id="ea0be-124">使用以下命令。</span><span class="sxs-lookup"><span data-stu-id="ea0be-124">Use the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="ea0be-125">当邮件停止显示到控制台时, 请按<kbd>enter</kbd>。</span><span class="sxs-lookup"><span data-stu-id="ea0be-125">When messages stop being displayed to the console, press <kbd>ENTER</kbd>.</span></span>

1. <span data-ttu-id="ea0be-126">返回到 "Azure 门户", 返回到事件中心命名空间。</span><span class="sxs-lookup"><span data-stu-id="ea0be-126">Back in the Azure portal, go back to your Event Hub Namespace.</span></span> <span data-ttu-id="ea0be-127">如果仍在 "事件中心" 页上, 则可以使用屏幕顶部的痕迹导航向后。</span><span class="sxs-lookup"><span data-stu-id="ea0be-127">If you are still on the Event Hub page, you can use the breadcrumb on the top of the screen to go backwards.</span></span> <span data-ttu-id="ea0be-128">或者, 您可以搜索命名空间并选择它。</span><span class="sxs-lookup"><span data-stu-id="ea0be-128">Or you can search for the namespace and select it.</span></span>

1. <span data-ttu-id="ea0be-129">单击 "**监视** > **指标 (预览)**"。</span><span class="sxs-lookup"><span data-stu-id="ea0be-129">Click **MONITORING** > **Metrics (preview)**.</span></span>

    ![显示事件中心指标以及显示的传入和传出邮件数量的屏幕截图。](../media/7-event-hub-metrics.png)

1. <span data-ttu-id="ea0be-131">从 "**指标**" 列表中, 选择 "**传入邮件**", 然后单击 "**添加指标**"。</span><span class="sxs-lookup"><span data-stu-id="ea0be-131">From the **Metric** list, select **Incoming Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="ea0be-132">从 "**指标**" 列表中, 选择 "**传出邮件**", 然后单击 "**添加指标**"。</span><span class="sxs-lookup"><span data-stu-id="ea0be-132">From the **Metric** list, select **Outgoing Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="ea0be-133">在图表顶部, 单击 "**最近24小时 (自动)** ", 将时间段更改为**最近30分钟**以展开数据图形。</span><span class="sxs-lookup"><span data-stu-id="ea0be-133">At the top of the chart, click **Last 24 hours (Automatic)** to change the time period to **Last 30 minutes** to expand the data graph.</span></span>

<span data-ttu-id="ea0be-134">您会发现, 虽然在事件中心在一段时间内脱机之前已发送邮件, 但所有100邮件都已成功传输。</span><span class="sxs-lookup"><span data-stu-id="ea0be-134">You'll see that though the messages were sent before the Event Hub was taken offline for a period, all 100 messages were successfully transmitted.</span></span>

## <a name="summary"></a><span data-ttu-id="ea0be-135">摘要</span><span class="sxs-lookup"><span data-stu-id="ea0be-135">Summary</span></span>

<span data-ttu-id="ea0be-136">在此单元中, 您使用事件中心指标测试事件中心是否成功处理发送和接收邮件。</span><span class="sxs-lookup"><span data-stu-id="ea0be-136">In this unit, you used the Event Hubs metrics to test that your Event Hub is successfully processing the sending and receiving messages.</span></span>
