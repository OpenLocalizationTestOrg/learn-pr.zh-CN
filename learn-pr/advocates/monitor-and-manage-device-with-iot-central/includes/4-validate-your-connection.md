<span data-ttu-id="2381c-101">现在, 你已使用 azure iot 中心应用程序, 并已将咖啡计算机连接到 azure IoT central。</span><span class="sxs-lookup"><span data-stu-id="2381c-101">You’ve now worked with the Azure IoT Central application and connected the coffee machine to Azure IoT Central.</span></span> <span data-ttu-id="2381c-102">您可以很好地开始监视和管理远程咖啡机。</span><span class="sxs-lookup"><span data-stu-id="2381c-102">You are well on your way to begin to monitor and manage your remote coffee machine.</span></span> <span data-ttu-id="2381c-103">在此单元中, 你需要一段时间来验证你的设置和连接, 具体方法是使用之前定义的已连接的咖啡 Maker 模板。</span><span class="sxs-lookup"><span data-stu-id="2381c-103">In this unit, you take a moment to validate your setup and connection by using the Connected Coffee Maker template that you defined earlier.</span></span> <span data-ttu-id="2381c-104">您可以在 "设置" 中更新最佳温度, 运行命令以检查计算机的状态, 并在仪表板中查看连接的咖啡机。</span><span class="sxs-lookup"><span data-stu-id="2381c-104">You update the optimal temperature in settings, run commands to check for the state of your machine, and view your connected coffee machine in the dashboard.</span></span> 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a><span data-ttu-id="2381c-105">更新设置以将应用程序与咖啡机同步</span><span class="sxs-lookup"><span data-stu-id="2381c-105">Update settings to sync your application with the coffee machine</span></span>

<span data-ttu-id="2381c-106">在 "**设置**" 页上, 从应用程序向咖啡机发送配置数据。</span><span class="sxs-lookup"><span data-stu-id="2381c-106">On the **Settings** page, you send configuration data to the coffee machine from your application.</span></span> 

<span data-ttu-id="2381c-107">在这种情况下, 请更改最佳温度, 然后选择 "**更新**"。</span><span class="sxs-lookup"><span data-stu-id="2381c-107">In this scenario, change the optimal temperature and choose **Update**.</span></span> <span data-ttu-id="2381c-108">设置更改后, 该设置在 UI 中标记为挂起, 直到咖啡计算机确认已对设置更改做出响应。</span><span class="sxs-lookup"><span data-stu-id="2381c-108">When the setting is changed, the setting is marked as pending in the UI until the coffee machine acknowledges that it has responded to the setting change.</span></span> 

> [!NOTE]
> <span data-ttu-id="2381c-109">设置中成功的更新指示数据流并验证您的连接。</span><span class="sxs-lookup"><span data-stu-id="2381c-109">Successful updates in the setting indicate data flow and validate your  connection.</span></span> <span data-ttu-id="2381c-110">遥测度量将以最佳温度响应更新。</span><span class="sxs-lookup"><span data-stu-id="2381c-110">The telemetry measurements will respond to the update in optimal temperature.</span></span> <span data-ttu-id="2381c-111">您可以在 "**度量**" 页上观察更改。</span><span class="sxs-lookup"><span data-stu-id="2381c-111">You can observe the change on the **Measurements** page.</span></span> 

## <a name="run-commands-on-the-coffee-machine"></a><span data-ttu-id="2381c-112">在咖啡机上运行命令</span><span class="sxs-lookup"><span data-stu-id="2381c-112">Run commands on the coffee machine</span></span> 
<span data-ttu-id="2381c-113">导航到以下练习的 "**命令**" 页。</span><span class="sxs-lookup"><span data-stu-id="2381c-113">Navigate to the **Commands** page for the following exercise.</span></span> <span data-ttu-id="2381c-114">若要验证命令安装程序, 请从 IoT Central 在咖啡机上远程运行命令。</span><span class="sxs-lookup"><span data-stu-id="2381c-114">To validate the commands setup, you remotely run commands on the coffee machine from IoT Central.</span></span> <span data-ttu-id="2381c-115">如果命令成功, 则将从咖啡计算机发送确认消息。</span><span class="sxs-lookup"><span data-stu-id="2381c-115">If the commands are successful, confirmation messages are sent from the coffee machine.</span></span>

1. <span data-ttu-id="2381c-116">通过选择 "**运行**" 远程启动 brewing。</span><span class="sxs-lookup"><span data-stu-id="2381c-116">Start brewing remotely by choosing **Run**.</span></span> 
    
    <span data-ttu-id="2381c-117">如果满足这三个条件, 咖啡机将会启动:</span><span class="sxs-lookup"><span data-stu-id="2381c-117">The coffee machine will start if these three conditions are satisfied:</span></span>
    - <span data-ttu-id="2381c-118">检测到杯</span><span class="sxs-lookup"><span data-stu-id="2381c-118">Cup detected</span></span>
    - <span data-ttu-id="2381c-119">不在维护中</span><span class="sxs-lookup"><span data-stu-id="2381c-119">Not in maintenance</span></span>
    - <span data-ttu-id="2381c-120">未 brewing 已</span><span class="sxs-lookup"><span data-stu-id="2381c-120">Not brewing already</span></span>  

    > [!NOTE]
    > <span data-ttu-id="2381c-121">成功启动 brewing 后, 计算机的状态将更改为黄色, 如**度量** > **状态**中所示。</span><span class="sxs-lookup"><span data-stu-id="2381c-121">When you've successfully started brewing, the state of the machine changes to yellow as indicated in **Measurements** > **State**.</span></span> 
    
    <span data-ttu-id="2381c-122">在节点 .js 模拟的咖啡计算机的控制台日志中查找确认消息。</span><span class="sxs-lookup"><span data-stu-id="2381c-122">Look for confirmation messages in the console log on the node.js simulated coffee machine.</span></span> 

    ![显示在运行命令之后收到的确认消息的控制台日志的屏幕截图。](../media/4-commands-brewing.png)

1. <span data-ttu-id="2381c-125">通过选择 "**运行**" 设置维护模式。</span><span class="sxs-lookup"><span data-stu-id="2381c-125">Set maintenance mode by choosing **Run**.</span></span> <span data-ttu-id="2381c-126">如果咖啡计算机*尚未*处于维护中, 则会将其设置为 "维护"。</span><span class="sxs-lookup"><span data-stu-id="2381c-126">The coffee machine will set to maintenance if it's *not* already in maintenance.</span></span>
    
    <span data-ttu-id="2381c-127">在咖啡计算机的控制台日志中查找确认消息。</span><span class="sxs-lookup"><span data-stu-id="2381c-127">Look for confirmation messages in the console log on the coffee machine.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="2381c-128">在真实的生活中, 当技术人员将计算机脱机以在将其切换回 online 之前执行必要的修复时, 咖啡机将继续保持维护模式, 直到您重新启动客户端代码。</span><span class="sxs-lookup"><span data-stu-id="2381c-128">As in real life, when the technician takes the machine offline to perform necessary repairs before switching it back online, the coffee machine continues to stay in the maintenance mode until you reboot the client code.</span></span>

    ![控制台日志的屏幕截图, 显示在运行命令之后收到的确认消息。](../media/4-commands-maintenance.png)

> [!IMPORTANT]
> <span data-ttu-id="2381c-131">建议运行 node.js 应用程序的时间不超过60分钟, 以防止应用程序向您发送不需要的通知/电子邮件。</span><span class="sxs-lookup"><span data-stu-id="2381c-131">It's recommended that you run the Node.js application no more than 60 minutes or so to prevent the application from sending you unwanted notifications/emails.</span></span> <span data-ttu-id="2381c-132">在不处理模块时停止应用程序还会阻止您耗尽每日邮件配额。</span><span class="sxs-lookup"><span data-stu-id="2381c-132">Stopping the application when you're not working on the module also prevents you from exhausting the daily message quota.</span></span>

## <a name="view-the-coffee-machine-in-the-dashboard"></a><span data-ttu-id="2381c-133">在仪表板中查看咖啡机</span><span class="sxs-lookup"><span data-stu-id="2381c-133">View the coffee machine in the dashboard</span></span>

1. <span data-ttu-id="2381c-134">导航到 "**仪表板**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="2381c-134">Navigate to the **Dashboard** tab.</span></span>

1. <span data-ttu-id="2381c-135">选择 "**编辑模板**" 以编辑仪表板。</span><span class="sxs-lookup"><span data-stu-id="2381c-135">Select **Edit Template** to edit the dashboard.</span></span>

1. <span data-ttu-id="2381c-136">从侧菜单中选择 "**折线图**"。</span><span class="sxs-lookup"><span data-stu-id="2381c-136">Choose **Line Chart** from the side menu.</span></span>

1. <span data-ttu-id="2381c-137">在 "**配置图表**" 中的 " `Telemetry` **标题**" 字段中输入。</span><span class="sxs-lookup"><span data-stu-id="2381c-137">In **Configure Chart**  enter `Telemetry` in the **Title** field.</span></span> <span data-ttu-id="2381c-138">我们将使用此图表查看我们的遥测数据。</span><span class="sxs-lookup"><span data-stu-id="2381c-138">We'll view our telemetry data with this chart.</span></span> 

1. <span data-ttu-id="2381c-139">为**时间范围**选择 "**过去30分钟**"。</span><span class="sxs-lookup"><span data-stu-id="2381c-139">Select **Past 30 minutes** for **Time Range**.</span></span> 

1. <span data-ttu-id="2381c-140">在 "**度量**" 区域中, 选择每个度量右侧的可见性图标, 以使图表显示该度量。</span><span class="sxs-lookup"><span data-stu-id="2381c-140">In the **Measures** area, select the visibility icon to the right of each measurement to make that measurement visible for our chart.</span></span> 

1. <span data-ttu-id="2381c-141">选择 "**保存**" 以保存配置并显示折线图。</span><span class="sxs-lookup"><span data-stu-id="2381c-141">Select **Save** to save our configuration and display the line chart.</span></span> 

    ![显示已连接的咖啡 maker 设备模板的仪表板的屏幕截图。](../media/4-dashboard-a.png)

1. <span data-ttu-id="2381c-143">在左侧菜单中选择 "**设置" 和 "属性**", 打开 "**配置设备详细信息**" 面板。</span><span class="sxs-lookup"><span data-stu-id="2381c-143">Choose **Settings and Properties** in the left-hand menu to open the **Configure Device Details** panel.</span></span> 

1. <span data-ttu-id="2381c-144">在`Device properties` **标题**存档中输入。</span><span class="sxs-lookup"><span data-stu-id="2381c-144">Enter `Device properties` in the **Title** filed.</span></span>

1. <span data-ttu-id="2381c-145">在 "**添加/删除**" 中, 选择 "**咖啡者最大温度**"、"保修期**最低温度**" 和 "**设备保修期已过期**", 然后选择 **"确定"** 以完成选择。</span><span class="sxs-lookup"><span data-stu-id="2381c-145">In **Add/Remove**, choose **Coffee Makers Max Temperature**, **Coffee Makers Min Temperature**, **Device Warranty Expired** and then select **OK** to complete the selection.</span></span>

1. <span data-ttu-id="2381c-146">选择 "**保存**" 以在仪表板中创建一个新的*设备属性*面板。</span><span class="sxs-lookup"><span data-stu-id="2381c-146">Select **Save** to create a new *Device properties* panel in our dashboard.</span></span> 

1. <span data-ttu-id="2381c-147">再次选择 "**设置" 和**"属性`Optimal Temperature` ", 并输入作为标题。</span><span class="sxs-lookup"><span data-stu-id="2381c-147">Choose **Settings and Properties** again,  and enter `Optimal Temperature` as the title.</span></span> <span data-ttu-id="2381c-148">在 "**添加/删除**" 中, 选择 "**最佳温度**"。</span><span class="sxs-lookup"><span data-stu-id="2381c-148">In **Add/Remove**, choose **Optimal  Temperature**.</span></span>

1. <span data-ttu-id="2381c-149">选择 "**保存**" 以保存您的工作并在仪表板中显示一个新窗格。</span><span class="sxs-lookup"><span data-stu-id="2381c-149">Select **Save** to save your work and display a new pane in our dashboard.</span></span> 

1. <span data-ttu-id="2381c-150">选择 "**完成**" 以退出编辑模式并显示新仪表板。</span><span class="sxs-lookup"><span data-stu-id="2381c-150">Select **Done** to exit edit mode and display the new dashboard.</span></span> 