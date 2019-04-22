> [!NOTE]
> <span data-ttu-id="91eb1-101">启动 VM 后, 您需要登录的用户名和密码位于说明旁边的 "**资源**" 选项卡上。</span><span class="sxs-lookup"><span data-stu-id="91eb1-101">After launching the VM, the username and password you need to sign in with is located on the **Resources** tab next to the instructions.</span></span>

<span data-ttu-id="91eb1-102">创建 bot 的第一步是为要在 Azure 中托管的 bot 提供一个位置。</span><span class="sxs-lookup"><span data-stu-id="91eb1-102">The first step in creating a bot is to provide a location for the bot to be hosted in Azure.</span></span> <span data-ttu-id="91eb1-103">azure 应用服务的 Web 应用功能非常适合承载机器人应用程序, azure bot 服务旨在为你进行预配。</span><span class="sxs-lookup"><span data-stu-id="91eb1-103">The Web Apps feature of Azure App Service is perfect for hosting bot applications, and the Azure Bot Service is designed to provision them for you.</span></span> <span data-ttu-id="91eb1-104">在此单元中, 你将使用 azure 门户预配 azure web 应用程序 bot。</span><span class="sxs-lookup"><span data-stu-id="91eb1-104">In this unit, you will use the Azure portal to provision an Azure web app bot.</span></span>

1. <span data-ttu-id="91eb1-105">通过在 VM 浏览器中打开https://portal.azure.com登录到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="91eb1-105">Sign into the Azure portal by opening https://portal.azure.com in the VM browser.</span></span>

1. <span data-ttu-id="91eb1-106">依次选择 " **+ 创建资源**" 和 " **AI + 机器学习**", 然后选择 " **Web 应用程序机器人**"。</span><span class="sxs-lookup"><span data-stu-id="91eb1-106">Select **+ Create a resource**, followed by **AI + Machine Learning**, then **Web App Bot**.</span></span>

    ![显示 "创建具有 Web 应用程序机器人资源类型的资源" 边栏的 Azure 门户屏幕截图。](../media/2-new-bot-service.png)

1. <span data-ttu-id="91eb1-108">在 "**应用程序名称**" 框中输入一个名称, 如 "factbot"。</span><span class="sxs-lookup"><span data-stu-id="91eb1-108">Enter a name, such as "qa-factbot", into the **App name** box.</span></span> <span data-ttu-id="91eb1-109">*此名称在 Azure 中必须是唯一的, 因此请确保旁边出现绿色的复选标记。*</span><span class="sxs-lookup"><span data-stu-id="91eb1-109">*This name must be unique within Azure, so make sure a green check mark appears next to it.*</span></span>

1. <span data-ttu-id="91eb1-110">在 "**订阅**和**资源组**" 下, 选择预先存在的资源。</span><span class="sxs-lookup"><span data-stu-id="91eb1-110">Under **Subscription** and **Resource group**, select the pre-existing resources.</span></span>

1. <span data-ttu-id="91eb1-111">从以下选项之一中选择**位置**:</span><span class="sxs-lookup"><span data-stu-id="91eb1-111">Select a **Location** from one of the following:</span></span>
    - <span data-ttu-id="91eb1-112">美国中部</span><span class="sxs-lookup"><span data-stu-id="91eb1-112">Central US</span></span>
    - <span data-ttu-id="91eb1-113">美国东部</span><span class="sxs-lookup"><span data-stu-id="91eb1-113">East US</span></span>
    - <span data-ttu-id="91eb1-114">美国东部2</span><span class="sxs-lookup"><span data-stu-id="91eb1-114">East US 2</span></span>
    - <span data-ttu-id="91eb1-115">美国中北部</span><span class="sxs-lookup"><span data-stu-id="91eb1-115">North Central US</span></span>
    - <span data-ttu-id="91eb1-116">美国中南部</span><span class="sxs-lookup"><span data-stu-id="91eb1-116">South Central US</span></span>
    - <span data-ttu-id="91eb1-117">美国西部</span><span class="sxs-lookup"><span data-stu-id="91eb1-117">West US</span></span>
    - <span data-ttu-id="91eb1-118">美国西部2</span><span class="sxs-lookup"><span data-stu-id="91eb1-118">West US 2</span></span>

    > [!NOTE]
    > <span data-ttu-id="91eb1-119">如果您在创建 Web 应用程序的 Bot 时看到资源策略错误, 请检查其位置是否设置为上述选项之一。</span><span class="sxs-lookup"><span data-stu-id="91eb1-119">If you see a resource policy error when you create the Web App Bot, then check that its location is set to one of the options above.</span></span>

1. <span data-ttu-id="91eb1-120">选择**S1**定价层。</span><span class="sxs-lookup"><span data-stu-id="91eb1-120">Select the **S1** pricing tier.</span></span>

1. <span data-ttu-id="91eb1-121">然后, 选择 " **Bot 模板**"。</span><span class="sxs-lookup"><span data-stu-id="91eb1-121">Then, select **Bot template**.</span></span> <span data-ttu-id="91eb1-122">选择 " **sdk v3** " 作为版本, **node.js**作为 SDK 语言, 并将**问题和答案**作为模板类型。</span><span class="sxs-lookup"><span data-stu-id="91eb1-122">Select **SDK v3** as the version, **Node.js** as the SDK language, and **Question and Answer** as the template type.</span></span> <span data-ttu-id="91eb1-123">然后, 选择刀片式服务器底部的 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="91eb1-123">Then, select **Select** at the bottom of the blade.</span></span>

    ![Azure 门户的屏幕截图, 其中显示了使用 node.js SDK 语言的 bot 创建进程的 bot 模板边栏和突出显示的问题和答案模板选项。](../media/2-portal-select-template.png)

1. <span data-ttu-id="91eb1-125">现在, 依次选择 " **app service plan/Location**" 和 "**新建**", 然后创建名为 "qa-服务-计划" 的应用程序服务计划, 或在上一步中选择的相同区域中的类似内容。</span><span class="sxs-lookup"><span data-stu-id="91eb1-125">Now, select **App service plan/Location**, followed by **Create New**, then create an App Service plan named "qa-factbot-service-plan" or something similar in the same region that you selected in the prior step.</span></span> <span data-ttu-id="91eb1-126">完成后, 选择 "Web 应用程序 Bot" 边栏底部的 "**创建**" 以启动部署。</span><span class="sxs-lookup"><span data-stu-id="91eb1-126">Once that's done, select **Create** at the bottom of the "Web App Bot" blade to start the deployment.</span></span>

    ![显示一个新 Web 应用程序的示例配置刀片的 Azure 门户屏幕截图。](../media/2-portal-start-bot-creation.png)

    > [!NOTE]
    > <span data-ttu-id="91eb1-128">部署通常需要两分钟或更短时间。</span><span class="sxs-lookup"><span data-stu-id="91eb1-128">Deployment generally requires two minutes or less.</span></span>

1. <span data-ttu-id="91eb1-129">部署完成后, 在门户左侧的功能区中选择 "**资源组**"。</span><span class="sxs-lookup"><span data-stu-id="91eb1-129">After your deployment completes, select **Resource groups** in the ribbon on the left side of the portal.</span></span>
1. <span data-ttu-id="91eb1-130">选择 "为此组预先创建的资源组", 打开部署了 Azure web app bot 的资源组。</span><span class="sxs-lookup"><span data-stu-id="91eb1-130">Select the resource group pre-created for this group to open the resource group where we deployed the Azure web app bot.</span></span>

<span data-ttu-id="91eb1-131">您现在应该会看到为您的 Azure web 应用程序机器人创建的几个资源。</span><span class="sxs-lookup"><span data-stu-id="91eb1-131">You should now see several resources created for your Azure web app bot.</span></span> <span data-ttu-id="91eb1-132">在幕后, 部署 Azure web 应用程序 bot 时会发生很大的情况。</span><span class="sxs-lookup"><span data-stu-id="91eb1-132">Behind the scenes, a lot happened when the Azure web app bot was deployed.</span></span> <span data-ttu-id="91eb1-133">已经创建并注册了一个 bot, 创建了一个[Azure web 应用程序](https://azure.microsoft.com/services/app-service/web/), 并将该 bot 配置为与[Microsoft QnA Maker](https://www.qnamaker.ai/)配合使用。</span><span class="sxs-lookup"><span data-stu-id="91eb1-133">A bot was created and registered, an [Azure web app](https://azure.microsoft.com/services/app-service/web/) was created to host it, and the bot was configured to work with [Microsoft QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="91eb1-134">下一步是使用 QnA Maker 创建包含智能的兼顾的问题和答案的知识库。</span><span class="sxs-lookup"><span data-stu-id="91eb1-134">The next step is to use QnA Maker to create a knowledge base of questions and answers to infuse the bot with intelligence.</span></span>
