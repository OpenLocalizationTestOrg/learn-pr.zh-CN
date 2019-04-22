## <a name="create-a-twilio-account"></a><span data-ttu-id="22d0a-101">创建 Twilio 帐户</span><span class="sxs-lookup"><span data-stu-id="22d0a-101">Create a Twilio account</span></span>

<span data-ttu-id="22d0a-102">若要能够从 Azure 函数发送短信消息, 您需要一个 Twilio 帐户。</span><span class="sxs-lookup"><span data-stu-id="22d0a-102">To be able to send SMS messages from an Azure Functions, you'll need a Twilio account.</span></span> <span data-ttu-id="22d0a-103">免费帐户不足以开始。</span><span class="sxs-lookup"><span data-stu-id="22d0a-103">The free account is more than enough to get started.</span></span>

1. <span data-ttu-id="22d0a-104">头到[twilio.com](https://www.twilio.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="22d0a-104">Head to [twilio.com](https://www.twilio.com?azure-portal=true).</span></span>

1. <span data-ttu-id="22d0a-105">单击右上角的红色 "**注册**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="22d0a-105">Click the red **Sign Up** button in the top-right corner.</span></span>

1. <span data-ttu-id="22d0a-106">填写详细信息, 然后单击 "**开始**"。</span><span class="sxs-lookup"><span data-stu-id="22d0a-106">Fill in your details and click **Get Started**.</span></span>

1. <span data-ttu-id="22d0a-107">输入要验证的电话号码。</span><span class="sxs-lookup"><span data-stu-id="22d0a-107">Enter you phone number to verify.</span></span> <span data-ttu-id="22d0a-108">Twilio 免费帐户允许您仅将邮件发送到已验证的电话号码, 以阻止它们被用于垃圾邮件。</span><span class="sxs-lookup"><span data-stu-id="22d0a-108">Twilio free accounts let you send messages only to verified phone numbers to stop them from being used for spam.</span></span> <span data-ttu-id="22d0a-109">Twilio 将向您发送验证代码, 您需要输入该代码来验证您的电话。</span><span class="sxs-lookup"><span data-stu-id="22d0a-109">Twilio will send you a verification code that you need to enter to verify your phone.</span></span>

    ![Twilio 注册中的电话验证步骤的屏幕截图](../media/twilio-verify-phone.png)
1. <span data-ttu-id="22d0a-111">登录到您的 Twilio 帐户, 然后单击您的帐户仪表板中**的 "获取试用号码**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="22d0a-111">Log onto your Twilio account and click **Get a Trial Number** button in you account dashboard.</span></span> <span data-ttu-id="22d0a-112">Twilio 为您分配用于发送邮件的电话号码。</span><span class="sxs-lookup"><span data-stu-id="22d0a-112">Twilio assigns you a phone number that is used to send messages.</span></span>

    > [!NOTE]
    > <span data-ttu-id="22d0a-113">这些分配的号码可能无法在某些国家/地区发送邮件。</span><span class="sxs-lookup"><span data-stu-id="22d0a-113">These assigned numbers may not be able to send messages in some countries.</span></span> <span data-ttu-id="22d0a-114">Twilio 文档列出[了哪些国家/地区有限制](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), 并显示了使用[国际号码或字母数字发件人 Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true)发送短信的方法。</span><span class="sxs-lookup"><span data-stu-id="22d0a-114">The Twilio documentation lists [which countries have restrictions](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), and shows ways to send SMS messages using an [international number or AlphaNumeric sender Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true).</span></span>

1. <span data-ttu-id="22d0a-115">记录新的 Twilio 试用号码;您将在本模块后面的部分中需要它。</span><span class="sxs-lookup"><span data-stu-id="22d0a-115">Take a note of your new Twilio Trial Number; you will need it later in this module.</span></span> <span data-ttu-id="22d0a-116">您还可以随时单击左侧菜单底部的省略号, 然后导航到 "_超级网络_ > _电话号码_ > "_管理数字_ > _活动号码_。</span><span class="sxs-lookup"><span data-stu-id="22d0a-116">You can also get this number anytime by clicking the ellipses at the bottom of the left-hand menu and navigating to _SUPER NETWORK_ > _Phone Numbers_ > _Manage Numbers_ > _Active Numbers_.</span></span>

## <a name="create-a-new-twilio-project"></a><span data-ttu-id="22d0a-117">创建新的 Twilio 项目</span><span class="sxs-lookup"><span data-stu-id="22d0a-117">Create a new Twilio project</span></span>

<span data-ttu-id="22d0a-118">在开始使用 Twilio 向已验证的号码发送邮件之前, 请创建一个项目以发送 programable SMS。</span><span class="sxs-lookup"><span data-stu-id="22d0a-118">Before you start using Twilio to send messages to your verified number, you create a project to send programable SMS.</span></span>

1. <span data-ttu-id="22d0a-119">选择屏幕左上角的下拉框, 然后选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="22d0a-119">Select the drop-down at the top-left corner of the screen and select **Create New Project**.</span></span>

    ![创建新项目](../media/twilio-new-project.png)

1. <span data-ttu-id="22d0a-121">选择 "**产品**" 选项卡, 然后单击 "**可编程短信**", 然后单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="22d0a-121">Select the **Products** tab, and click **Programmable SMS**, then click **Continue**.</span></span>

1. <span data-ttu-id="22d0a-122">为第一个项目 (如 "我在这里") 提供一个名称, 然后单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="22d0a-122">Provide a name for your first project, such as "I'm here", then click **Continue**.</span></span>

1. <span data-ttu-id="22d0a-123">跳过要邀请团队配对的步骤。</span><span class="sxs-lookup"><span data-stu-id="22d0a-123">Skip the step to invite a team mate.</span></span>

1. <span data-ttu-id="22d0a-124">在 Twilio 消息仪表板中, 展开 "**项目信息**" 面板。</span><span class="sxs-lookup"><span data-stu-id="22d0a-124">From the Twilio messaging dashboard, expand the **Project Info** panel.</span></span>

    ![展开的 "项目信息" 面板的屏幕截图](../media/project-info.png)

1. <span data-ttu-id="22d0a-126">请注意, 你的**帐户 SID**和**身份验证令牌**, 因为稍后将需要这些值。</span><span class="sxs-lookup"><span data-stu-id="22d0a-126">Note your **ACCOUNT SID** and **AUTH TOKEN** because you will need these values later.</span></span>

## <a name="launch-visual-studio"></a><span data-ttu-id="22d0a-127">启动 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22d0a-127">Launch Visual Studio</span></span>

<span data-ttu-id="22d0a-128">对于本模块, 你将使用 Visual Studio 2017 开发移动应用和 Azure 函数应用。</span><span class="sxs-lookup"><span data-stu-id="22d0a-128">For this module, you'll develop the mobile app and Azure Functions app using Visual Studio 2017.</span></span> <span data-ttu-id="22d0a-129">[! 注意] 尽管可以构建用于在 iOS、Android 和通用 Windows 平台 (UWP) 上运行的 Xamarin 应用程序, 但本模块仅侧重于 UWP。</span><span class="sxs-lookup"><span data-stu-id="22d0a-129">Although Xamarin.Forms apps can be built to run on iOS, Android, and Universal Windows Platform (UWP), this module will just focus on UWP.</span></span>

<span data-ttu-id="22d0a-130">在系统上启动 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="22d0a-130">Launch Visual Studio 2017 on your system.</span></span>

## <a name="summary"></a><span data-ttu-id="22d0a-131">摘要</span><span class="sxs-lookup"><span data-stu-id="22d0a-131">Summary</span></span>

<span data-ttu-id="22d0a-132">在此单位中, 您创建了一个 Twilio 帐户, 用于发送短信并启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="22d0a-132">In this unit, you created a Twilio account that you'll use to send SMS and launched Visual Studio.</span></span> <span data-ttu-id="22d0a-133">接下来, 你将了解如何创建 xamarin 和添加 xamarin NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="22d0a-133">Next, you'll learn how to create a Xamarin.Forms app and add the Xamarin.Essentials NuGet package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22d0a-134">请记下您在此单元中收集的 Twilio**帐户 SID**和**AUTH TOKEN**以及**活动电话号码**值, 因为稍后将需要这些值。</span><span class="sxs-lookup"><span data-stu-id="22d0a-134">Keep note of the Twilio  **ACCOUNT SID** and **AUTH TOKEN** and **Active Phone Number** values that you gathered in this unit, because you'll need these values later.</span></span>
