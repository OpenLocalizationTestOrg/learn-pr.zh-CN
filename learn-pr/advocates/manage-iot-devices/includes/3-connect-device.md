<span data-ttu-id="41954-101">捕获天气数据是一项重要任务, 因为天气可能会影响流量模式与零售商店中的加热、通风和空气调节 (HVAC) 系统的运营方式之间的所有内容。</span><span class="sxs-lookup"><span data-stu-id="41954-101">Capturing of weather data is an important task as weather can effect everything from traffic patterns to how heating, ventilation, and air conditioning (HVAC) systems in retail stores are operated.</span></span> <span data-ttu-id="41954-102">在本练习中, 你将与在线 Raspberry Pi 模拟器进行交互, 你学习了如何在上一个单元中捕获模拟的天气数据, 并通过 Azure IoT 中心进行操作。</span><span class="sxs-lookup"><span data-stu-id="41954-102">In this exercise, you will be interacting with the online Raspberry Pi simulator you learned about in the previous unit to capture simulated weather data and via the Azure IoT Hub.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="41954-103">虽然在模拟环境中执行此操作, 但在模拟设备上运行的应用程序可以在将来转移到实际设备。</span><span class="sxs-lookup"><span data-stu-id="41954-103">While this exercise is being conducted in a simulated environment, the application running on the simulated device can be transferred to a real device in the future.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="41954-104">创建 IoT 中心</span><span class="sxs-lookup"><span data-stu-id="41954-104">Create an IoT hub</span></span>
<span data-ttu-id="41954-105">Azure IoT 中心提供了功能和可扩展性模型, 使设备和后端开发人员能够构建强大的设备管理解决方案。</span><span class="sxs-lookup"><span data-stu-id="41954-105">Azure IoT Hub provides the features and an extensibility model that enable device and back-end developers to build robust device management solutions.</span></span> <span data-ttu-id="41954-106">设备的范围从受约束的传感器和单一目的 microcontrollers, 到路由设备组通信的功能强大的网关。</span><span class="sxs-lookup"><span data-stu-id="41954-106">Devices range from constrained sensors and single purpose microcontrollers, to powerful gateways that route communications for groups of devices.</span></span> <span data-ttu-id="41954-107">此外, IoT 运算符的用例和要求在各行业中的变化显著不同。</span><span class="sxs-lookup"><span data-stu-id="41954-107">In addition, the use cases and requirements for IoT operators vary significantly across industries.</span></span> <span data-ttu-id="41954-108">尽管这种变化, 但使用 IoT 中心的设备管理还提供了可适应各种设备和最终用户的功能、模式和代码库。</span><span class="sxs-lookup"><span data-stu-id="41954-108">Despite this variation, device management with IoT Hub provides the capabilities, patterns, and code libraries to cater to a diverse set of devices and end users.</span></span>

<span data-ttu-id="41954-109">若要从 Raspberry Pi 模拟器开始收集数据, 需要先创建 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="41954-109">In order to start collecting the data from the Raspberry Pi simulator, you need to first create an IoT hub.</span></span>

1. <span data-ttu-id="41954-110">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="41954-110">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

2. <span data-ttu-id="41954-111">选择 "在 Azure 门户的左上角**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="41954-111">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="41954-112">选择 " **Internet 内容**", 然后选择 " **IoT 中心**"。</span><span class="sxs-lookup"><span data-stu-id="41954-112">Select **Internet of Things**, and then select **IoT Hub**.</span></span>

![指向 IoT 中心的 Azure 门户导航的屏幕截图](../media/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. <span data-ttu-id="41954-114">在**iot 中心**窗格中, 输入你的 iot 中心的以下信息:</span><span class="sxs-lookup"><span data-stu-id="41954-114">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

   - <span data-ttu-id="41954-115">**订阅**: 使用此示例的默认订阅。</span><span class="sxs-lookup"><span data-stu-id="41954-115">**Subscription**: Use the default subscription for this example.</span></span>
   - <span data-ttu-id="41954-116">**资源组**: 使用现有的资源组。</span><span class="sxs-lookup"><span data-stu-id="41954-116">**Resource group**: Use the existing resource group.</span></span> <span data-ttu-id="41954-117">通过将所有相关资源放在同一个组中, 可以将它们全部管理在一起。</span><span class="sxs-lookup"><span data-stu-id="41954-117">By putting all related resources in the same group you can manage them all together.</span></span> <span data-ttu-id="41954-118">例如, 删除资源组将删除该组中包含的所有资源。</span><span class="sxs-lookup"><span data-stu-id="41954-118">For example, deleting the resource group deletes all resources contained in that group.</span></span>
   - <span data-ttu-id="41954-119">**名称**: 为 IoT 中心创建唯一名称。</span><span class="sxs-lookup"><span data-stu-id="41954-119">**Name**: Create a unique name for your IoT hub.</span></span> <span data-ttu-id="41954-120">如果输入的名称可用, 则会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="41954-120">If the name you enter is available, a green check mark appears.</span></span>
   - <span data-ttu-id="41954-121">**区域**: 从以下列表中选择最接近你的位置。</span><span class="sxs-lookup"><span data-stu-id="41954-121">**Region**: Select the closest location to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    > [!IMPORTANT]
    > <span data-ttu-id="41954-122">IoT 中心将公开为 DNS 终结点, 因此在对其命名时, 请务必避免任何敏感信息。</span><span class="sxs-lookup"><span data-stu-id="41954-122">The IoT hub will be publicly discoverable as a DNS endpoint, so make sure to avoid any sensitive information while naming it.</span></span>

    ![IoT 中心基础知识窗口](./../media/dbb7319388673b8ee0e0b407536156c0.png)

1. <span data-ttu-id="41954-124">选择 "**下一步: 大小和缩放**" 以继续创建 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="41954-124">Select **Next: Size and scale** to continue creating your IoT hub.</span></span>
2. <span data-ttu-id="41954-125">选择**定价和扩展层**。</span><span class="sxs-lookup"><span data-stu-id="41954-125">Choose your **Pricing and scale tier**.</span></span> <span data-ttu-id="41954-126">对于此示例, 请选择**无 F1**的层。</span><span class="sxs-lookup"><span data-stu-id="41954-126">For this example, select the **F1 - Free** tier.</span></span>

    ![IoT 中心大小和缩放窗口](../media/b506eb3293fa4aa9d4785ad498fc476c.png)

3. <span data-ttu-id="41954-128">选择 "**审阅 + 创建**"。</span><span class="sxs-lookup"><span data-stu-id="41954-128">Select **Review + create**.</span></span>

4. <span data-ttu-id="41954-129">查看 IoT 中心信息, 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="41954-129">Review your IoT hub information, then click **Create**.</span></span> <span data-ttu-id="41954-130">你的 IoT 中心可能需要几分钟的时间才能创建。</span><span class="sxs-lookup"><span data-stu-id="41954-130">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="41954-131">您可以在 "**通知**" 窗格中监视进度。</span><span class="sxs-lookup"><span data-stu-id="41954-131">You can monitor the progress in the **Notifications** pane.</span></span>

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up exercise. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a><span data-ttu-id="41954-132">注册设备</span><span class="sxs-lookup"><span data-stu-id="41954-132">Register a device</span></span>
<span data-ttu-id="41954-133">在可以连接之前, 必须向你的 IoT 中心注册设备。</span><span class="sxs-lookup"><span data-stu-id="41954-133">A device must be registered with your IoT hub before it can connect.</span></span>

1. <span data-ttu-id="41954-134">在 iot 中心导航菜单中, 打开**iot 设备**, 然后单击 "**添加**" 以在 IoT 中心中注册设备。</span><span class="sxs-lookup"><span data-stu-id="41954-134">In your IoT hub navigation menu, open **IoT devices**, then click **Add** to register a device in your IoT hub.</span></span>

   ![在 iot 中心的 iot 设备中添加设备](../media/ee5f177abcf06b86dd007fce3b8448ad.png)

2. <span data-ttu-id="41954-136">为新设备输入**设备 ID** 。</span><span class="sxs-lookup"><span data-stu-id="41954-136">Enter a **Device ID** for the new device.</span></span> <span data-ttu-id="41954-137">选择一个有意义的 ID 来表示设备。</span><span class="sxs-lookup"><span data-stu-id="41954-137">Choose a meaningful ID to represent your device.</span></span> <span data-ttu-id="41954-138">设备 id 区分大小写。</span><span class="sxs-lookup"><span data-stu-id="41954-138">Device IDs are case sensitive.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="41954-139">设备 ID 可能在为客户支持和故障排除收集的日志中可见, 因此, 请务必在对其命名时避免任何敏感信息。</span><span class="sxs-lookup"><span data-stu-id="41954-139">The device ID may be visible in the logs collected for customer support and troubleshooting, so make sure to avoid any sensitive information while naming it.</span></span>

3. <span data-ttu-id="41954-140">单击"保存"。</span><span class="sxs-lookup"><span data-stu-id="41954-140">Click **Save**.</span></span>
4. <span data-ttu-id="41954-141">创建设备后, 从 " **IoT 设备**" 窗格的列表中打开该设备。</span><span class="sxs-lookup"><span data-stu-id="41954-141">After the device is created, open the device from the list in the **IoT devices** pane.</span></span>
5. <span data-ttu-id="41954-142">将 **---主键的连接字符串**复制到稍后使用。</span><span class="sxs-lookup"><span data-stu-id="41954-142">Copy the **Connection string---primary key** to use later.</span></span>

   ![获取设备连接字符串](../media/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a><span data-ttu-id="41954-144">发送模拟遥测</span><span class="sxs-lookup"><span data-stu-id="41954-144">Send simulated telemetry</span></span>

1. <span data-ttu-id="41954-145">打开[Raspberry Pi Azure IoT 模拟器](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="41954-145">Open the [Raspberry Pi Azure IoT Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true).</span></span>
1. <span data-ttu-id="41954-146">将第15行中的占位符替换为您刚复制的 Azure IoT 中心设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="41954-146">Replace the placeholder in Line 15 with the Azure IoT hub device connection string you just copied.</span></span>
1. <span data-ttu-id="41954-147">单击 " `Run`控制台" 窗口`npm start`中的按钮或键入以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="41954-147">Click the `Run` button or type `npm start` in the console window to run the application.</span></span>

    ![替换设备连接字符串](../media/Line15.png)

1. <span data-ttu-id="41954-149">您应该会看到以下输出, 其中显示传感器数据和发送到 IoT 中心的邮件。</span><span class="sxs-lookup"><span data-stu-id="41954-149">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

    ![从 Raspberry Pi 发送到 IoT 中心的输出传感器数据](../media/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="41954-151">从你的中心读取遥测</span><span class="sxs-lookup"><span data-stu-id="41954-151">Read the telemetry from your hub</span></span>
<span data-ttu-id="41954-152">那么, 会发生什么情况呢？</span><span class="sxs-lookup"><span data-stu-id="41954-152">So what's happening?</span></span> <span data-ttu-id="41954-153">IoT 中心正在接收从模拟设备发送的设备到云消息。</span><span class="sxs-lookup"><span data-stu-id="41954-153">IoT hub is receiving the device-to-cloud messages sent from the simulated device.</span></span> <span data-ttu-id="41954-154">为了了解这一点, 让我们快速了解 Azure IoT 中心处理传入数据的方式。</span><span class="sxs-lookup"><span data-stu-id="41954-154">In order to see that, let's take a quick look at how Azure IoT Hub is processing the incoming data.</span></span> <span data-ttu-id="41954-155">在 IoT 中心中的 "**监视**" 下, 选择 "**指标**"。</span><span class="sxs-lookup"><span data-stu-id="41954-155">In your IoT Hub, under **Monitoring**, select **Metrics**.</span></span> <span data-ttu-id="41954-156">等待数据进入图片时, 请等待几分钟, 然后重试。</span><span class="sxs-lookup"><span data-stu-id="41954-156">Give it a few minutes as you wait for the data to come into the picture.</span></span>

![IoT 中心指标](../media/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
