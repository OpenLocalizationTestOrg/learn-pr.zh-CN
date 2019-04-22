<span data-ttu-id="2f58b-101">安全性的最大问题之一是能够查看您需要保护的所有方面, 并在黑客执行之前发现漏洞。</span><span class="sxs-lookup"><span data-stu-id="2f58b-101">One of the biggest problems with security is being able to see all the areas you need to protect and to find vulnerabilities before hackers do.</span></span> <span data-ttu-id="2f58b-102">azure 提供了一种服务, 使其更易于被称为 "Azure 安全中心"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-102">Azure provides a service which makes this much easier called Azure Security Center.</span></span>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="2f58b-103">什么是 Azure 安全中心？</span><span class="sxs-lookup"><span data-stu-id="2f58b-103">What is Azure Security Center?</span></span>

<span data-ttu-id="2f58b-104">azure 安全中心 (ASC) 是一种监视服务, 可在 Azure 和本地的所有服务中提供威胁保护。</span><span class="sxs-lookup"><span data-stu-id="2f58b-104">Azure Security Center (ASC) is a monitoring service that provides threat protection across all of your services both in Azure, and on-premises.</span></span> <span data-ttu-id="2f58b-105">它可以:</span><span class="sxs-lookup"><span data-stu-id="2f58b-105">It can:</span></span>

- <span data-ttu-id="2f58b-106">根据您的配置、资源和网络提供安全建议。</span><span class="sxs-lookup"><span data-stu-id="2f58b-106">Provide security recommendations based on your configurations, resources, and networks.</span></span>
- <span data-ttu-id="2f58b-107">监视本地和云工作负载中的安全设置, 并在新服务联机时自动对其应用所需的安全性。</span><span class="sxs-lookup"><span data-stu-id="2f58b-107">Monitor security settings across on-premises and cloud workloads and automatically apply required security to new services as they come online.</span></span>
- <span data-ttu-id="2f58b-108">持续监视你的所有服务并执行自动安全评估, 以确定潜在的漏洞, 然后才能利用它们。</span><span class="sxs-lookup"><span data-stu-id="2f58b-108">Continuously monitor all your services and perform automatic security assessments to identify potential vulnerabilities before they can be exploited.</span></span>
- <span data-ttu-id="2f58b-109">使用机器学习检测并阻止恶意软件安装在您的服务和虚拟机中。</span><span class="sxs-lookup"><span data-stu-id="2f58b-109">Use machine learning to detect and block malware from being installed in your services and virtual machines.</span></span> <span data-ttu-id="2f58b-110">您也可以使用白色列表应用程序, 以确保只允许执行验证的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f58b-110">You can also white-list applications to ensure that only the apps you validate are allowed to execute.</span></span>
- <span data-ttu-id="2f58b-111">分析并识别潜在的入站攻击, 并帮助调查威胁以及可能发生的任何后续入侵活动。</span><span class="sxs-lookup"><span data-stu-id="2f58b-111">Analyze and identify potential inbound attacks and help to investigate threats and any post-breach activity which might have occurred.</span></span>
- <span data-ttu-id="2f58b-112">对端口的实时访问控制, 通过确保网络仅允许您需要的流量来减少攻击面。</span><span class="sxs-lookup"><span data-stu-id="2f58b-112">Just-In-Time access control for ports, reducing your attack surface by ensuring the network only allows traffic you require.</span></span>

<span data-ttu-id="2f58b-113">ASC 是[Internet 安全](https://www.cisecurity.org/cis-benchmarks/)(ci) 建议中心的一部分。</span><span class="sxs-lookup"><span data-stu-id="2f58b-113">ASC is part of the [Center for Internet Security](https://www.cisecurity.org/cis-benchmarks/) (CIS) recommendations.</span></span>

## <a name="activating-azure-security-center"></a><span data-ttu-id="2f58b-114">激活 Azure 安全中心</span><span class="sxs-lookup"><span data-stu-id="2f58b-114">Activating Azure Security Center</span></span>

<span data-ttu-id="2f58b-115">Azure 安全中心为混合云工作负载提供统一的安全管理和高级威胁保护, 并在两层中提供: 免费和标准。</span><span class="sxs-lookup"><span data-stu-id="2f58b-115">Azure Security Center provides unified security management and advanced threat protection for hybrid cloud workloads and is offered in two tiers: Free and Standard.</span></span> <span data-ttu-id="2f58b-116">免费层提供了安全策略、评估和建议, 而标准层提供了一组功能强大的功能, 包括威胁智能。</span><span class="sxs-lookup"><span data-stu-id="2f58b-116">The free tier provides security policies, assessments, and recommendations while the Standard tier provides a robust set of features, including threat intelligence.</span></span>

<span data-ttu-id="2f58b-117">考虑到 ASC 的优势, 贵公司的安全团队已决定为你的办公室中的所有订阅启用此功能。</span><span class="sxs-lookup"><span data-stu-id="2f58b-117">Given the benefits of ASC, the security team at your company has decided that it be turned on for all subscriptions at your office.</span></span> <span data-ttu-id="2f58b-118">您早上收到一封电子邮件, 以便为您的应用程序打开它, 让我们来看看如何做到这一点。</span><span class="sxs-lookup"><span data-stu-id="2f58b-118">You got an email this morning to turn it on for your applications - so let's look at how to do that.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f58b-119">azure 安全中心在免费 azure 沙盒中不受支持。</span><span class="sxs-lookup"><span data-stu-id="2f58b-119">Azure Security Center is not supported in the free Azure sandbox.</span></span> <span data-ttu-id="2f58b-120">您可以在您自己的订阅中执行这些步骤, 或仅按照了解如何激活 ASC。</span><span class="sxs-lookup"><span data-stu-id="2f58b-120">You can perform these steps in your own subscription, or just follow along to understand how to activate ASC.</span></span>

1. <span data-ttu-id="2f58b-121">打开[azure 门户](https://portal.azure.com?azure-portal=true)并从左侧菜单中选择 " **azure 安全中心**" (如果您看不到它), 可以选择 "安全性" 部分中的 "**所有服务**" 和 "查找**安全中心**", 如下所示。</span><span class="sxs-lookup"><span data-stu-id="2f58b-121">Open the [Azure portal](https://portal.azure.com?azure-portal=true) and select **Azure Security Center** from the left-hand menu, if you don't see it there, you can select **All services** and find **Security Center** in the security section as shown below.</span></span>

   ![显示已突出显示 "安全中心" 的 "所有服务" 边栏的屏幕截图。](../media/2-ASC-Menu.png)

1. <span data-ttu-id="2f58b-123">如果从未打开 ASC, 则刀片式服务器将从 "**入门**" 项开始, 这可能会要求您升级订阅。</span><span class="sxs-lookup"><span data-stu-id="2f58b-123">If you have never opened ASC, the blade will start on the **Getting started** entry which might ask you to upgrade your subscription.</span></span> <span data-ttu-id="2f58b-124">忽略这一点, 请在页面底部选择 "**跳过**", 然后选择 "**概述**"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-124">Ignore that for now, select **Skip** at the bottom of the page, and then select **Overview**.</span></span>
    - <span data-ttu-id="2f58b-125">这将在你的订阅中提供的所有元素中显示 "大型安全图片"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-125">This will display the "big security picture" across all the elements available in your subscription.</span></span>
    - <span data-ttu-id="2f58b-126">这有大量有用的信息可供您浏览。</span><span class="sxs-lookup"><span data-stu-id="2f58b-126">This has a ton of great information you can explore.</span></span>

1. <span data-ttu-id="2f58b-127">接下来, 选择 "策略和合规性" 下的 "**覆盖范围**"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-127">Next, select **Coverage**, under "Policy and Compliance".</span></span> <span data-ttu-id="2f58b-128">这将显示 ASC 中包含 (或未覆盖) 的订阅元素。</span><span class="sxs-lookup"><span data-stu-id="2f58b-128">This will display what subscription elements are being covered (or not covered) by ASC.</span></span> <span data-ttu-id="2f58b-129">你可以在此处为你有权访问的任何订阅启用 ASC。</span><span class="sxs-lookup"><span data-stu-id="2f58b-129">Here you can turn on ASC for any subscription you have access to.</span></span> <span data-ttu-id="2f58b-130">尝试在三个覆盖率区域之间切换: "未涵盖"、"基本覆盖范围" 和 "标准覆盖范围"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-130">Try switching between the three coverage areas: "Not covered", "Basic coverage" and "Standard coverage".</span></span>

1. <span data-ttu-id="2f58b-131">未覆盖的订阅将提示激活 ASC。</span><span class="sxs-lookup"><span data-stu-id="2f58b-131">Subscriptions that are not covered will have a prompt to activate ASC.</span></span> <span data-ttu-id="2f58b-132">您可以按 "立即升级" 按钮, 为订阅中的所有资源启用 ASC。</span><span class="sxs-lookup"><span data-stu-id="2f58b-132">You can press the "Upgrade Now" button to enable ASC for all the resources in the subscription.</span></span>

![显示 "安全中心-覆盖范围" 页的 "基本覆盖范围" 选项卡中的 "立即升级" 按钮的屏幕截图。](../media/2-Upgrade-Now.png)

### <a name="free-vs-standard-pricing-tier"></a><span data-ttu-id="2f58b-134">免费和标准定价层</span><span class="sxs-lookup"><span data-stu-id="2f58b-134">Free vs. Standard pricing tier</span></span>

<span data-ttu-id="2f58b-135">虽然您可以使用具有 ASC 的免费 Azure 订阅层, 但仅限于 Azure 资源的评估和建议。</span><span class="sxs-lookup"><span data-stu-id="2f58b-135">While you can use a free Azure subscription tier with ASC, it is limited to assessments and recommendations of Azure resources only.</span></span> <span data-ttu-id="2f58b-136">若要真正利用 ASC, 您需要升级到标准层订阅, 如上所示。</span><span class="sxs-lookup"><span data-stu-id="2f58b-136">To really leverage ASC, you will need to upgrade to a Standard tier subscription as shown above.</span></span> <span data-ttu-id="2f58b-137">您可以通过**覆盖范围**刀片中的 "立即升级" 按钮升级订阅, 如上文所述。</span><span class="sxs-lookup"><span data-stu-id="2f58b-137">You can upgrade your subscription through the "Upgrade Now" button in the **Coverage** blade as noted above.</span></span> <span data-ttu-id="2f58b-138">您还可以在 ASC 菜单中切换到 "**入门**" 边栏, 它将引导您完成更改订阅级别的步骤。</span><span class="sxs-lookup"><span data-stu-id="2f58b-138">You can also switch to the **Getting Started** blade in the ASC menu which will walk you through changing your subscription level.</span></span> <span data-ttu-id="2f58b-139">定价和功能可能会根据区域而变化, 您可以在 "[定价" 页](https://azure.microsoft.com/pricing/details/security-center/)上获得全面概述。</span><span class="sxs-lookup"><span data-stu-id="2f58b-139">The pricing and features may change based on the region, you can get a full overview on the [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span></span>

> [!NOTE]
> <span data-ttu-id="2f58b-140">若要将订阅升级到标准层, 必须为订阅所有者、订阅参与者或安全管理员分配角色。</span><span class="sxs-lookup"><span data-stu-id="2f58b-140">To upgrade a subscription to the Standard tier, you must be assigned the role of Subscription Owner, Subscription Contributor, or Security Admin.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f58b-141">在60天的试用期结束后, ASC 将**按每月每月的 15/节点**定价, 并将向你的帐户收费。</span><span class="sxs-lookup"><span data-stu-id="2f58b-141">After the 60-day trial period is over, ASC is priced at **$15/node per month** and will be billed to your account.</span></span>

## <a name="turning-off-azure-security-center"></a><span data-ttu-id="2f58b-142">关闭 Azure 安全中心</span><span class="sxs-lookup"><span data-stu-id="2f58b-142">Turning off Azure Security Center</span></span>

<span data-ttu-id="2f58b-143">对于生产系统, 您肯定希望将 Azure 安全中心保持打开状态, 以便它可以监控所有资源的威胁。</span><span class="sxs-lookup"><span data-stu-id="2f58b-143">For production systems, you will definitely want to keep Azure Security Center turned on so it can monitor all your resources for threats.</span></span> <span data-ttu-id="2f58b-144">但是, 如果只是使用 ASC 并将其打开, 则很可能要将其禁用, 以确保不会向您收取费用。</span><span class="sxs-lookup"><span data-stu-id="2f58b-144">However, if you are just playing with ASC and turned it on, you will likely want to disable it to ensure you are not charged.</span></span> <span data-ttu-id="2f58b-145">现在我们来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="2f58b-145">Let's do that now.</span></span>

1. <span data-ttu-id="2f58b-146">打开[azure 门户](https://portal.azure.com?azure-portal=true)并从左侧菜单中选择 " **azure 安全中心**" (如果您看不到它), 可以选择 "安全性" 部分中的 "**所有服务**" 和 "查找**安全中心**", 如下所示。</span><span class="sxs-lookup"><span data-stu-id="2f58b-146">Open the [Azure portal](https://portal.azure.com?azure-portal=true) and select **Azure Security Center** from the left-hand menu, if you don't see it there, you can select **All services** and find **Security Center** in the security section as shown below.</span></span>

    ![显示已突出显示 "安全中心" 的 "所有服务" 边栏的屏幕截图。](../media/2-ASC-Menu.png)

1. <span data-ttu-id="2f58b-148">从左侧菜单中选择 "**安全策略**"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-148">Select **Security Policy** from the left-hand menu.</span></span>

1. <span data-ttu-id="2f58b-149">接下来, 选择要降级其 ASC 的订阅旁边的 "**编辑设置 >**"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-149">Next, select **Edit settings >**, next to the subscription for which you want to downgrade ASC.</span></span>

1. <span data-ttu-id="2f58b-150">在下一个屏幕上, 从左侧菜单中选择 "定价层"。</span><span class="sxs-lookup"><span data-stu-id="2f58b-150">On the next screen select "Pricing Tier" from the left-hand menu.</span></span>

1. <span data-ttu-id="2f58b-151">将显示一个新页面, 如下图所示。</span><span class="sxs-lookup"><span data-stu-id="2f58b-151">A new page will appear that looks like the image below.</span></span> <span data-ttu-id="2f58b-152">单击左侧的 "免费 (仅适用于 Azure 资源)" 的框。</span><span class="sxs-lookup"><span data-stu-id="2f58b-152">Click on the box on the left that says "Free (for Azure resources only)".</span></span>

    ![显示免费和标准定价层选项的屏幕截图。](../media/2-Pricing-Tier.png)

1. <span data-ttu-id="2f58b-154">按屏幕顶部的 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2f58b-154">Press the **Save** button at the top of the screen.</span></span>

<span data-ttu-id="2f58b-155">现在, 你已将订阅降级到免费的 Azure 安全中心层。</span><span class="sxs-lookup"><span data-stu-id="2f58b-155">You have now downgraded your subscription to the free tier of Azure Security Center.</span></span>

<span data-ttu-id="2f58b-156">恭喜, 你已采取第一个 (最重要的) 步骤来保护你的应用程序、数据和网络!</span><span class="sxs-lookup"><span data-stu-id="2f58b-156">Congratulations, you have taken your first (and most important) step to securing your application, data and network!</span></span>