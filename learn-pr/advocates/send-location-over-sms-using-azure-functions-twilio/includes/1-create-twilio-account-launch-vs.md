> [!TIP]
> <span data-ttu-id="7a974-101">登录到 VM 所需的用户名和密码位于 "**资源**" 选项卡上。</span><span class="sxs-lookup"><span data-stu-id="7a974-101">The username and password you need to sign in to the VM are located on the **Resources** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="7a974-102">如果您使用的是 Mac, 则在启动虚拟机后, 您可能需要使用工具栏上的闪电图标, 或从\*\*\*\* "资源" 选项卡上的 "**资源**" 选项卡中的 "资源" 选项卡旁边的 "打开", 以解除对 VM 的锁定。</span><span class="sxs-lookup"><span data-stu-id="7a974-102">If you are using a Mac, after launching the VM you may need to use either the lightning icon on the toolbar, or the **Ctrl+Alt+Delete** option from the **Resources** tab next to the instructions to unlock the VM.</span></span>


<span data-ttu-id="7a974-103">在本模块中, 将创建具有无服务器后端的跨平台 Xamarin. 表单应用程序。</span><span class="sxs-lookup"><span data-stu-id="7a974-103">In this module, you'll create a cross-platform Xamarin.Forms app with a serverless back end.</span></span> <span data-ttu-id="7a974-104">此应用将从其设备中获取用户的位置, 并将电话号码列表发送到 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="7a974-104">This app will get the user's location from their device and send it with a list of phone numbers to an Azure function.</span></span> <span data-ttu-id="7a974-105">然后, 该函数将使用与第三方服务 (Twilio) 的绑定将您的位置作为短信发送给提供的所有电话号码。</span><span class="sxs-lookup"><span data-stu-id="7a974-105">The function will then use a binding to a third-party service (Twilio) to send your location as an SMS message to all the phone numbers provided.</span></span>

<span data-ttu-id="7a974-106">此过程涉及以下步骤:</span><span class="sxs-lookup"><span data-stu-id="7a974-106">This process involves the following steps:</span></span>

1. <span data-ttu-id="7a974-107">应用程序使用 Xamarin 作为抽象来捕获您在特定于设备的位置 api 上的位置。</span><span class="sxs-lookup"><span data-stu-id="7a974-107">The app captures your location using Xamarin.Essentials as an abstraction over device-specific location APIs.</span></span>

1. <span data-ttu-id="7a974-108">位置和电话号码打包到 JSON 有效负载中并发送到 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="7a974-108">The location and phone numbers are packaged up into a JSON payload and sent to an Azure function.</span></span>

1. <span data-ttu-id="7a974-109">Azure 函数对 JSON 有效负载进行解码并创建 SMS 消息。</span><span class="sxs-lookup"><span data-stu-id="7a974-109">The Azure function decodes the JSON payload and creates SMS messages.</span></span>

1. <span data-ttu-id="7a974-110">SMS 消息通过[Twilio](https://www.twilio.com/?azure-portal=true)发送。</span><span class="sxs-lookup"><span data-stu-id="7a974-110">The SMS messages are sent via [Twilio](https://www.twilio.com/?azure-portal=true).</span></span>

<span data-ttu-id="7a974-111">下图显示了此过程的概述。</span><span class="sxs-lookup"><span data-stu-id="7a974-111">The following illustration shows an overview of this process.</span></span>

![该图显示了通过短信共享位置的过程的高级别体系结构。](../media/1-architecture.png)

## <a name="create-a-twilio-account"></a><span data-ttu-id="7a974-113">创建 Twilio 帐户</span><span class="sxs-lookup"><span data-stu-id="7a974-113">Create a Twilio account</span></span>

<span data-ttu-id="7a974-114">若要能够从 Azure 函数发送短信消息, 您需要一个 Twilio 帐户。</span><span class="sxs-lookup"><span data-stu-id="7a974-114">To be able to send SMS messages from an Azure function, you'll need a Twilio account.</span></span> <span data-ttu-id="7a974-115">免费帐户不足以开始。</span><span class="sxs-lookup"><span data-stu-id="7a974-115">The free account is more than enough to get started.</span></span>

1. <span data-ttu-id="7a974-116">头到[twilio.com](https://www.twilio.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="7a974-116">Head to [twilio.com](https://www.twilio.com?azure-portal=true).</span></span>

1. <span data-ttu-id="7a974-117">单击右上角的红色 "**注册**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="7a974-117">Click the red **Sign Up** button in the top-right corner.</span></span>

1. <span data-ttu-id="7a974-118">填写详细信息, 然后单击 "**开始**"。</span><span class="sxs-lookup"><span data-stu-id="7a974-118">Fill in your details and click **Get Started**.</span></span>

1. <span data-ttu-id="7a974-119">你需要验证你的电话号码。</span><span class="sxs-lookup"><span data-stu-id="7a974-119">You'll need to verify your phone number.</span></span> <span data-ttu-id="7a974-120">Twilio 免费帐户允许您仅将邮件发送到已验证的电话号码, 以阻止它们用于垃圾邮件。</span><span class="sxs-lookup"><span data-stu-id="7a974-120">Twilio free accounts let you send messages only to verified phone numbers to stop them being used for spam.</span></span> <span data-ttu-id="7a974-121">Twilio 将向您发送验证代码, 您需要输入该代码来验证您的电话。</span><span class="sxs-lookup"><span data-stu-id="7a974-121">Twilio will send you a verification code that you need to enter to verify your phone.</span></span>

1. <span data-ttu-id="7a974-122">选择 "**产品**" 选项卡, 然后单击 "**可编程短信**", 然后单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="7a974-122">Select the **Products** tab, and click **Programmable SMS**, then click **Continue**.</span></span>

1. <span data-ttu-id="7a974-123">为第一个项目 (如 "我在这里") 提供一个名称, 然后单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="7a974-123">Provide a name for your first project, such as "I'm here", then click **Continue**.</span></span>

1. <span data-ttu-id="7a974-124">跳过要邀请团队配对的步骤。</span><span class="sxs-lookup"><span data-stu-id="7a974-124">Skip the step to invite a team mate.</span></span>

1. <span data-ttu-id="7a974-125">在 Twilio 消息仪表板中, 展开 "**项目信息**" 面板。</span><span class="sxs-lookup"><span data-stu-id="7a974-125">From the Twilio messaging dashboard, expand the **Project Info** panel.</span></span>

1. <span data-ttu-id="7a974-126">请注意, 你的**帐户 SID**和**身份验证令牌**, 因为稍后将需要这些值。</span><span class="sxs-lookup"><span data-stu-id="7a974-126">Note your **ACCOUNT SID** and **AUTH TOKEN** because you will need these values later.</span></span>

    <span data-ttu-id="7a974-127">创建 Twilio 帐户时, 会向您分配一个可从其发送邮件的电话号码。</span><span class="sxs-lookup"><span data-stu-id="7a974-127">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="7a974-128">您可以在 "Twilio**电话号码**" 仪表板上找到此电话号码。</span><span class="sxs-lookup"><span data-stu-id="7a974-128">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span>

1. <span data-ttu-id="7a974-129">在 Twilio 网站中, 选择左侧菜单底部的省略号。</span><span class="sxs-lookup"><span data-stu-id="7a974-129">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="7a974-130">然后, 选择 "*超级网络->Phone 号码*"。</span><span class="sxs-lookup"><span data-stu-id="7a974-130">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="7a974-131">您可以使用 pin 图标将此仪表板固定到左侧菜单。</span><span class="sxs-lookup"><span data-stu-id="7a974-131">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="7a974-132">您的 Twilio 号码将位于 "*管理号码->Active 号码*" 下。</span><span class="sxs-lookup"><span data-stu-id="7a974-132">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span>

    ![查找您的 Twilio 号码](../media/7-twilio-find-number.png)

    > [!TIP]
    > <span data-ttu-id="7a974-134">如果还没有活动号码, 请选择 "活动\*\*\*\* 号码" 页中的 "开始", 开始创建号码的过程。</span><span class="sxs-lookup"><span data-stu-id="7a974-134">If you don't have an active number yet, select **Get Started** in the Active Numbers page to begin the process of creating a number.</span></span>

1. <span data-ttu-id="7a974-135">记下您的活动电话号码。</span><span class="sxs-lookup"><span data-stu-id="7a974-135">Note your active phone number.</span></span> <span data-ttu-id="7a974-136">本模块后面将会用到它。</span><span class="sxs-lookup"><span data-stu-id="7a974-136">It will be used later in this module.</span></span>


> [!NOTE]
> <span data-ttu-id="7a974-137">当你注册时, 你将被分配一个将用于发送短信的 Twilio 电话号码。</span><span class="sxs-lookup"><span data-stu-id="7a974-137">When you sign up, you will be assigned a Twilio phone number that will be used to send SMS messages.</span></span> <span data-ttu-id="7a974-138">在某些国家/地区, 这些号码可能无法发送短信消息。</span><span class="sxs-lookup"><span data-stu-id="7a974-138">In some countries, these numbers may not be able to send SMS messages.</span></span> <span data-ttu-id="7a974-139">Twilio 文档列出[了哪些国家/地区有限制](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), 并显示了使用[国际号码或字母数字发件人 Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true)发送短信的方法。</span><span class="sxs-lookup"><span data-stu-id="7a974-139">The Twilio documentation lists [which countries have restrictions](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), and shows ways to send SMS messages using an [international number or AlphaNumeric sender Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true).</span></span>

## <a name="launch-visual-studio"></a><span data-ttu-id="7a974-140">启动 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a974-140">Launch Visual Studio</span></span>

<span data-ttu-id="7a974-141">对于本模块, 你将使用 Visual Studio 2017 (通过虚拟机提供) 开发移动应用和 Azure 函数应用。</span><span class="sxs-lookup"><span data-stu-id="7a974-141">For this module, you'll develop the mobile app and Azure Functions app using Visual Studio 2017, available via a virtual machine.</span></span> <span data-ttu-id="7a974-142">[! 注意] 尽管可以构建用于在 iOS、Android 和通用 Windows 平台 (UWP) 上运行的 Xamarin 应用程序, 但此模块仅侧重于 UWP, 以便它可以在实验室虚拟机中运行。</span><span class="sxs-lookup"><span data-stu-id="7a974-142">Although Xamarin.Forms apps can be built to run on iOS, Android, and Universal Windows Platform (UWP), this module will just focus on UWP so that it works inside the lab virtual machine.</span></span>

<span data-ttu-id="7a974-143">从 VM 的 "开始" 菜单或从桌面快捷方式启动 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="7a974-143">Launch Visual Studio 2017 from the VM's Start Menu, or from the desktop shortcut.</span></span>

## <a name="summary"></a><span data-ttu-id="7a974-144">摘要</span><span class="sxs-lookup"><span data-stu-id="7a974-144">Summary</span></span>

<span data-ttu-id="7a974-145">在此单位中, 您创建了一个 Twilio 帐户, 用于发送短信并启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7a974-145">In this unit, you created a Twilio account to use to send SMS messages and launched Visual Studio.</span></span> <span data-ttu-id="7a974-146">接下来, 您将了解如何创建 xamarin 和添加 xamarin NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="7a974-146">Next, you learn how to create a Xamarin.Forms app and add the Xamarin.Essentials NuGet package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a974-147">请记下您在此单元中收集的 Twilio**帐户 SID**和**AUTH TOKEN**以及**活动电话号码**值, 因为稍后将需要这些值。</span><span class="sxs-lookup"><span data-stu-id="7a974-147">Keep note of the Twilio  **ACCOUNT SID** and **AUTH TOKEN** and **Active Phone Number** values that you gathered in this unit, because you'll need these values later.</span></span>
