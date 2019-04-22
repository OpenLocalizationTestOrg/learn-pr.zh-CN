<span data-ttu-id="0f239-101">到目前为止, 你已将你的咖啡计算机连接到 Azure IoT 中心应用程序, 并启用允许你监视和管理你的咖啡计算机的数据交换。</span><span class="sxs-lookup"><span data-stu-id="0f239-101">So far, you've connected your coffee machine to the Azure IoT Central application, enabling the exchange of data that allows you to monitor and manage your coffee machine.</span></span> <span data-ttu-id="0f239-102">在此单位中, 您将创建规则, 以在咖啡计算机的水源处于正常范围之外时触发操作。</span><span class="sxs-lookup"><span data-stu-id="0f239-102">In this unit, you create rules that trigger actions when the water temperature of the coffee machine is outside the normal range.</span></span> 

## <a name="create-rules-in-iot-central-with-email-as-the-action"></a><span data-ttu-id="0f239-103">在 IoT Central 中创建包含电子邮件作为操作的规则</span><span class="sxs-lookup"><span data-stu-id="0f239-103">Create rules in IoT Central with email as the action</span></span>

<span data-ttu-id="0f239-104">Azure IoT Central 提供了其本机电子邮件功能以发送通知。</span><span class="sxs-lookup"><span data-stu-id="0f239-104">Azure IoT Central has its native email capabilities to send notifications.</span></span> <span data-ttu-id="0f239-105">在这种情况下, 如果咖啡计算机超出最佳温度范围, 且不受保修保护, 则由客户的维护部门的 IoT 中心发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="0f239-105">In this scenario, if the coffee machine is outside the optimal temperature range and is not protected by the warranty, an email is sent by IoT Central to the client’s maintenance department.</span></span>

1. <span data-ttu-id="0f239-106">导航到此单元练习的 "**规则**" 页, 然后通过选择右侧的 "**编辑模板**" 进入编辑模式。</span><span class="sxs-lookup"><span data-stu-id="0f239-106">Navigate to the **Rules** page for the exercises in this unit and enter edit mode by selecting **Edit Template** on the right.</span></span> 
1. <span data-ttu-id="0f239-107">依次选择 " **+ 新建规则**" 和 "**遥测**"。</span><span class="sxs-lookup"><span data-stu-id="0f239-107">Select **+ New Rule** and then **Telemetry**.</span></span> 

1. <span data-ttu-id="0f239-108">输入名称`Coffee Maker Water Too Cold (Expired)`</span><span class="sxs-lookup"><span data-stu-id="0f239-108">Enter the name `Coffee Maker Water Too Cold (Expired)`</span></span>

1. <span data-ttu-id="0f239-109">在 "**+\*\*\*\*条件**" 的右侧选择加号 (), 然后单击 "**保存**", 将以下条件添加到规则中:</span><span class="sxs-lookup"><span data-stu-id="0f239-109">Add the following conditions to the rule by selecting the plus (**+**) sign to the right of **Conditions**, and then click **Save**:</span></span>      
    - <span data-ttu-id="0f239-110">水源温度低于咖啡的最小温度</span><span class="sxs-lookup"><span data-stu-id="0f239-110">Water Temperature is less than Coffee Maker's Min Temperature</span></span>
    - <span data-ttu-id="0f239-111">设备保修期已过期等于1</span><span class="sxs-lookup"><span data-stu-id="0f239-111">Device Warranty Expired equals 1</span></span>

    ![显示在 "配置遥测规则" 边栏中添加了新规则的已连接的 "咖啡 maker" 设备模板的 "规则" 页的屏幕截图。](../media/5-flow-a.png)

1. <span data-ttu-id="0f239-113">在 "**配置遥测规则**" 面板中向下**+** 滚动, 选择 "**操作**" 旁边的, 然后选择 "**电子邮件**"。</span><span class="sxs-lookup"><span data-stu-id="0f239-113">Scroll down on the **Configure Telemetry Rule** panel and choose **+** next to **Actions**, and then choose **Email**.</span></span>

1. <span data-ttu-id="0f239-114">输入您用于登录 IoT 中心应用程序的电子邮件地址, 并添加注释`Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span><span class="sxs-lookup"><span data-stu-id="0f239-114">Enter the email address that you used to sign in to the IoT Central application and add the note `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span></span>

1. <span data-ttu-id="0f239-115">选择"保存"。</span><span class="sxs-lookup"><span data-stu-id="0f239-115">Choose **Save**.</span></span> <span data-ttu-id="0f239-116">规则将列在 "**规则**" 页上。</span><span class="sxs-lookup"><span data-stu-id="0f239-116">Your rule is listed on the **Rules** page.</span></span>

<span data-ttu-id="0f239-117">现在, 让我们在水温度过高时对事例重复这些步骤。</span><span class="sxs-lookup"><span data-stu-id="0f239-117">Now let's repeat these steps for the case when the water is too hot.</span></span> 

1. <span data-ttu-id="0f239-118">依次选择 " **+ 新建规则**" 和 "**遥测**"。</span><span class="sxs-lookup"><span data-stu-id="0f239-118">Select **+ New Rule** and then **Telemetry**.</span></span>

1. <span data-ttu-id="0f239-119">添加一个新规则并为其指定名称`Coffee Maker Water Too Hot (Expired)`</span><span class="sxs-lookup"><span data-stu-id="0f239-119">Add a new rule and give it the name `Coffee Maker Water Too Hot (Expired)`</span></span>

1. <span data-ttu-id="0f239-120">在 "**+\*\*\*\*条件**" 的右侧选择加号 (), 然后单击 "**保存**", 将以下条件添加到规则中:</span><span class="sxs-lookup"><span data-stu-id="0f239-120">Add the following conditions to the rule by selecting the plus (**+**) sign to the right of **Conditions**, and then click **Save**:</span></span>      
    - <span data-ttu-id="0f239-121">水源温度大于咖啡决策者的最大温度</span><span class="sxs-lookup"><span data-stu-id="0f239-121">Water Temperature is greater than Coffee Makers Max Temperature</span></span>
    - <span data-ttu-id="0f239-122">设备保修期已过期等于1</span><span class="sxs-lookup"><span data-stu-id="0f239-122">Device Warranty Expired equals 1</span></span>

1. <span data-ttu-id="0f239-123">在 "**配置遥测规则**" 面板中向下**+** 滚动, 选择 "**操作**" 旁边的, 然后选择 "**电子邮件**"。</span><span class="sxs-lookup"><span data-stu-id="0f239-123">Scroll down on the **Configure Telemetry Rule** panel and choose **+** next to **Actions**, and then choose **Email**.</span></span>

1. <span data-ttu-id="0f239-124">输入您用于登录 IoT 中心应用程序的电子邮件地址, 并添加注释`Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span><span class="sxs-lookup"><span data-stu-id="0f239-124">Enter the email address that you used to sign in to the IoT Central application and add the note `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span></span>

1. <span data-ttu-id="0f239-125">选择"保存"。</span><span class="sxs-lookup"><span data-stu-id="0f239-125">Choose **Save**.</span></span> <span data-ttu-id="0f239-126">规则将列在 "**规则**" 页上。</span><span class="sxs-lookup"><span data-stu-id="0f239-126">Your rule is listed on the **Rules** page.</span></span>

<span data-ttu-id="0f239-127">若要触发该规则, 请在 "**属性**" 下指定的范围之外的**设置**中设置最佳温度。</span><span class="sxs-lookup"><span data-stu-id="0f239-127">To trigger the rule, set the optimal temperature in **Settings** outside the range that you specified under **Properties**.</span></span> <span data-ttu-id="0f239-128">完成验证后, 请关闭规则以避免使用电子邮件淹没收件箱。</span><span class="sxs-lookup"><span data-stu-id="0f239-128">Once you are done with the validation, turn off the rules to avoid flooding your inbox with emails.</span></span>