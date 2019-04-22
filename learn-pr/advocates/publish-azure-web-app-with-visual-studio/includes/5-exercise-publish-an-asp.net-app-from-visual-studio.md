<span data-ttu-id="a941a-101">现在, 你已在本地运行 ASP.NET Core web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a941a-101">You now have an ASP.NET Core web application running locally.</span></span> <span data-ttu-id="a941a-102">在此部分中, 你将应用程序发布到 Azure 应用服务。</span><span class="sxs-lookup"><span data-stu-id="a941a-102">In this part, you'll publish your application to Azure App Service.</span></span>

1. <span data-ttu-id="a941a-103">在 "解决方案资源管理器" 中, 右键单击您的项目, 然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="a941a-103">In Solution Explorer, right-click your project and select **Publish**.</span></span>

1. <span data-ttu-id="a941a-104">单击 "**启动**"。</span><span class="sxs-lookup"><span data-stu-id="a941a-104">Click **Start**.</span></span>

1. <span data-ttu-id="a941a-105">在出现的对话框中, 选择左侧的 "**应用程序服务**" 作为发布目标。</span><span class="sxs-lookup"><span data-stu-id="a941a-105">In the dialog box that appears, on the left, choose **App Service** as your publish target.</span></span>  <span data-ttu-id="a941a-106">在右侧, 选择 "**新建**" 以创建应用服务应用。</span><span class="sxs-lookup"><span data-stu-id="a941a-106">On the right, select **Create New** to create an App Service app.</span></span>

1. <span data-ttu-id="a941a-107">单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="a941a-107">Click **Publish**.</span></span>

### <a name="configure-your-new-azure-app-service"></a><span data-ttu-id="a941a-108">配置新的 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="a941a-108">Configure your new Azure App Service</span></span>

1. <span data-ttu-id="a941a-109">在 "**创建应用服务**" 对话框中, 单击 "**添加帐户**", 然后登录到 Azure。</span><span class="sxs-lookup"><span data-stu-id="a941a-109">In the **Create App Service** dialog box, click **Add an account**, and sign in to Azure.</span></span>

1. <span data-ttu-id="a941a-110">输入有关应用服务计划的必需信息。</span><span class="sxs-lookup"><span data-stu-id="a941a-110">Enter the required information about your App Service plan.</span></span>

    <span data-ttu-id="a941a-111">在 "**创建应用服务**" 对话框中, 提供以下信息:</span><span class="sxs-lookup"><span data-stu-id="a941a-111">In the **Create App Service** dialog box, provide the following information:</span></span>

    - <span data-ttu-id="a941a-112">**应用名称**: 应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="a941a-112">**App Name**: the name of your application.</span></span>  <span data-ttu-id="a941a-113">该名称确定已发布的应用程序的 URL, 该 URL 将&lt;为&gt;https://azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="a941a-113">The name determines the URL of the published application, which will be https://&lt;AppName&gt;.azurewebsites.net.</span></span> <span data-ttu-id="a941a-114">它必须是一个唯一值。</span><span class="sxs-lookup"><span data-stu-id="a941a-114">It must be a unique value.</span></span> <span data-ttu-id="a941a-115">您可能需要试用一些不同的名称来查找唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="a941a-115">You may have to try out some different names to find one that is unique.</span></span>

    - <span data-ttu-id="a941a-116">**订阅**: 要将应用部署到的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="a941a-116">**Subscription**: The Azure subscription you wish to deploy the app to.</span></span> <span data-ttu-id="a941a-117">选择**Concierge 订阅**, 我们通过沙盒为你提供此订阅。</span><span class="sxs-lookup"><span data-stu-id="a941a-117">Choose **Concierge Subscription**, which we provide to you through the sandbox.</span></span>

    - <span data-ttu-id="a941a-118">**资源组:** 选择 "现有<rgn>[沙盒资源组名称]</rgn> " 资源组。</span><span class="sxs-lookup"><span data-stu-id="a941a-118">**Resource Group:** Select the existing <rgn>[sandbox resource group name]</rgn> resource group.</span></span>

    - <span data-ttu-id="a941a-119">**托管计划:** 托管计划指定承载您的应用程序的 web 服务器场的位置、大小和功能。</span><span class="sxs-lookup"><span data-stu-id="a941a-119">**Hosting Plan:** The hosting plan specifies the location, size, and features of the web server farm that hosts your app.</span></span>  <span data-ttu-id="a941a-120">在此练习中, 创建新的托管计划。</span><span class="sxs-lookup"><span data-stu-id="a941a-120">For this exercise, create a new hosting plan.</span></span>

        <span data-ttu-id="a941a-121">单击托管计划旁边的 "**新建 ...** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="a941a-121">Click the **New...** button next to the hosting plan.</span></span>

    - <span data-ttu-id="a941a-122">**application Insights:** 指定是否要将 application Insights 用于应用程序。</span><span class="sxs-lookup"><span data-stu-id="a941a-122">**Application Insights:** Specifies if you want to use Application Insights for your application.</span></span> <span data-ttu-id="a941a-123">在本练习中, 我们建议您选择 "**无"。**</span><span class="sxs-lookup"><span data-stu-id="a941a-123">For this exercise, we recommend that you choose **None.**</span></span>

1. <span data-ttu-id="a941a-124">单击 "**创建**" 按钮开始发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="a941a-124">Click the **Create** button to start publishing your app.</span></span> <span data-ttu-id="a941a-125">在部署过程中, 你将看到进度。</span><span class="sxs-lookup"><span data-stu-id="a941a-125">You will see progress as it deploys.</span></span>

1. <span data-ttu-id="a941a-126">恭喜, 你的 ASP.NET 核心 web 应用程序现已发布并处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="a941a-126">Congratulations, your ASP.NET Core web application is now published and live.</span></span> <span data-ttu-id="a941a-127">网站在生成输出中的最终 URL 以及 Visual Studio 中的发布页面。</span><span class="sxs-lookup"><span data-stu-id="a941a-127">The final URL for your site in the build output and also on the publishing page in Visual Studio.</span></span>

1. <span data-ttu-id="a941a-128">若要测试您的网站, 请转到指示的 URL。</span><span class="sxs-lookup"><span data-stu-id="a941a-128">To test your website, go to the URL indicated.</span></span>

    ![活动网站](../media/5-WebPageLive.png)

    > [!NOTE]
    > <span data-ttu-id="a941a-130">如果您无法从输出中找到该 URL, 请导航到&lt;https://&gt;appname. azurewebsites.net, &lt;其中&gt; AppName 是您之前提供的名称。</span><span class="sxs-lookup"><span data-stu-id="a941a-130">If you can't locate the URL from the output, navigate to https://&lt;AppName&gt;.azurewebsites.net, where &lt;AppName&gt; is the name you provided earlier.</span></span> <span data-ttu-id="a941a-131">例如, **https://alpineskihouse123.azurewebsites.net/**。</span><span class="sxs-lookup"><span data-stu-id="a941a-131">For example, **https://alpineskihouse123.azurewebsites.net/**.</span></span>

<span data-ttu-id="a941a-132">你现在有一个实时 web 应用!</span><span class="sxs-lookup"><span data-stu-id="a941a-132">You now have a live web app!</span></span> <span data-ttu-id="a941a-133">你的 Azure 应用服务计划已创建, 应用程序正在运行, 并已准备好接受更新。</span><span class="sxs-lookup"><span data-stu-id="a941a-133">Your Azure App Service plan has been created, and the app is running, and ready to accept updates.</span></span>
  