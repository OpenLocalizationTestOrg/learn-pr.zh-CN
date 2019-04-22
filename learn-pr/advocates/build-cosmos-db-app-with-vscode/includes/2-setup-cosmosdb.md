<span data-ttu-id="2eede-101">Visual Studio Code 的 Azure Cosmos DB 扩展通过使您能够使用命令窗口创建资源, 从而简化了帐户、数据库和集合的创建。</span><span class="sxs-lookup"><span data-stu-id="2eede-101">The Azure Cosmos DB extension for Visual Studio Code simplifies account, database, and collection creation by enabling you to create resources using the command window.</span></span>

<span data-ttu-id="2eede-102">在此单元中, 将安装 Visual Studio 的 Azure Cosmos DB 扩展, 然后使用它创建帐户、数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="2eede-102">In this unit you will install the Azure Cosmos DB extension for Visual Studio, and then use it to create an account, database, and collection.</span></span>

## <a name="install-the-azure-cosmos-db-extension-for-visual-studio"></a><span data-ttu-id="2eede-103">安装 Visual Studio 的 Azure Cosmos DB 扩展</span><span class="sxs-lookup"><span data-stu-id="2eede-103">Install the Azure Cosmos DB extension for Visual Studio</span></span>

1. <span data-ttu-id="2eede-104">转到[visual studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb&azure-portal=true)并安装适用于 visual studio Code 的**Azure Cosmos DB**扩展。</span><span class="sxs-lookup"><span data-stu-id="2eede-104">Go to the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb&azure-portal=true) and install the **Azure Cosmos DB** extension for Visual Studio Code.</span></span>

1. <span data-ttu-id="2eede-105">在 Visual Studio Code 中加载 "扩展" 选项卡时, 单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="2eede-105">When the extension tab loads in Visual Studio Code, click **Install**.</span></span>

1. <span data-ttu-id="2eede-106">安装完成后, 单击 "**重新加载**"。</span><span class="sxs-lookup"><span data-stu-id="2eede-106">After installation is complete, click **Reload**.</span></span>

    <span data-ttu-id="2eede-107">Visual Studio Code 显示</span><span class="sxs-lookup"><span data-stu-id="2eede-107">Visual Studio Code displays the</span></span> ![Azure 图标](../media/2-setup/visual-studio-code-explorer-icon.png) <span data-ttu-id="2eede-109">安装并重新加载扩展后屏幕左侧的 Azure 图标。</span><span class="sxs-lookup"><span data-stu-id="2eede-109">Azure icon on the left side of the screen after the extension is installed and reloaded.</span></span>

## <a name="create-an-azure-cosmos-db-account-in-visual-studio-code"></a><span data-ttu-id="2eede-110">在 Visual Studio Code 中创建 Azure Cosmos DB 帐户</span><span class="sxs-lookup"><span data-stu-id="2eede-110">Create an Azure Cosmos DB account in Visual Studio Code</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

1. <span data-ttu-id="2eede-111">在 Visual Studio Code 中, 通过单击 "**查看** > **命令组件面板**" 并键入 " **azure: 登录**" 登录 azure。</span><span class="sxs-lookup"><span data-stu-id="2eede-111">In Visual Studio Code, sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span> <span data-ttu-id="2eede-112">您必须安装了[azure 帐户](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account&azure-portal=true)扩展才能使用 azure: 登录。</span><span class="sxs-lookup"><span data-stu-id="2eede-112">You must have the [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account&azure-portal=true) extension installed to use Azure: Sign In.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2eede-113">使用用于创建沙盒的相同帐户登录 Azure。</span><span class="sxs-lookup"><span data-stu-id="2eede-113">Login to Azure using the same account used to create the sandbox.</span></span> <span data-ttu-id="2eede-114">沙盒提供对 Concierge 订阅的访问权限。</span><span class="sxs-lookup"><span data-stu-id="2eede-114">The sandbox provides access to a Concierge Subscription.</span></span>

    <span data-ttu-id="2eede-115">按照提示复制并粘贴 web 浏览器中提供的代码, 这将对 Visual Studio code session 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="2eede-115">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

1. <span data-ttu-id="2eede-116">单击左侧![菜单上](../media/2-setup/visual-studio-code-explorer-icon.png)的 "azure 图标**azure** " 图标, 然后右键单击 " **Concierge 订阅**", 然后单击 "**创建帐户**"。</span><span class="sxs-lookup"><span data-stu-id="2eede-116">Click the ![Azure icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure** icon on the left menu, and then right-click **Concierge Subscription**, and click **Create Account**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2eede-117">如果你未看到列出的 Concierge 订阅, 请确保使用用于创建沙盒的相同帐户在 Visual Studio Code 中登录 Azure。</span><span class="sxs-lookup"><span data-stu-id="2eede-117">If you do not see the Concierge Subscription listed, ensure you logged into Azure in Visual Studio Code using the same account used to create the sandbox.</span></span> <span data-ttu-id="2eede-118">此外, 如果您已在 azure 帐户扩展中筛选出 azure 订阅, 请验证该`> Azure: Select Subscriptions`命令中是否已检查 Concierge 订阅。</span><span class="sxs-lookup"><span data-stu-id="2eede-118">Additionally, if you have filtered your Azure subscriptions in the Azure Account extension, verify the Concierge Subscription is checked in the `> Azure: Select Subscriptions` command.</span></span>

1. <span data-ttu-id="2eede-119">单击该__+__ 按钮以开始创建 Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="2eede-119">Click the __+__ button to start creating a Cosmos DB account.</span></span> <span data-ttu-id="2eede-120">如果您有多个订阅, 系统将要求您选择订阅。</span><span class="sxs-lookup"><span data-stu-id="2eede-120">You will be asked to select the subscription if you have more than one.</span></span>

1. <span data-ttu-id="2eede-121">在屏幕顶部的文本框中, 为您的 Azure Cosmos DB 帐户输入一个唯一的名称, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="2eede-121">In the text box at the top of the screen, enter a unique name for your Azure Cosmos DB account, and then press enter.</span></span> <span data-ttu-id="2eede-122">帐户名称只能包含小写字母、数字和 '-' 字符, 并且必须介于3和31个字符之间。</span><span class="sxs-lookup"><span data-stu-id="2eede-122">The account name can contain only lowercase letters, numbers and the '-' character, and must be between 3 and 31 characters.</span></span>

1. <span data-ttu-id="2eede-123">接下来, 选择 " **SQL (DocumentDB)**", 然后选择 " **<rgn>[沙盒资源组名称]</rgn>**", 然后选择一个位置。</span><span class="sxs-lookup"><span data-stu-id="2eede-123">Next, select **SQL (DocumentDB)**, then select **<rgn>[sandbox resource group name]</rgn>**, and then select a location.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    <span data-ttu-id="2eede-124">Visual Studio Code 中的 "输出" 选项卡显示帐户创建的进度。</span><span class="sxs-lookup"><span data-stu-id="2eede-124">The output tab in Visual Studio Code displays the progress of the account creation.</span></span> <span data-ttu-id="2eede-125">完成此过程需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="2eede-125">It takes a few minutes to complete.</span></span>

1. <span data-ttu-id="2eede-126">创建帐户后, 在**azure: Cosmos DB**窗格中展开你的 azure 订阅, 扩展将显示新的 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="2eede-126">After the account is created, expand your Azure subscription in the **Azure: Cosmos DB** pane and the extension displays the new Azure Cosmos DB account.</span></span> <span data-ttu-id="2eede-127">在下图中, 新帐户称为 "**学习模块**"。</span><span class="sxs-lookup"><span data-stu-id="2eede-127">In the following image, the new account is named **learning-modules**.</span></span>

    ![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/azure-cosmos-db-vs-code-extension.png)

## <a name="create-an-azure-cosmos-db-database-and-collection-in-visual-studio-code"></a><span data-ttu-id="2eede-129">在 Visual Studio Code 中创建 Azure Cosmos DB 数据库和集合</span><span class="sxs-lookup"><span data-stu-id="2eede-129">Create an Azure Cosmos DB database and collection in Visual Studio Code</span></span>

<span data-ttu-id="2eede-130">现在, 让我们为客户创建一个新的数据库和集合。</span><span class="sxs-lookup"><span data-stu-id="2eede-130">Now let's create a new database and collection for your customers.</span></span>

1. <span data-ttu-id="2eede-131">在 "Azure: Cosmos DB" 窗格中, 右键单击您的新帐户, 然后单击 "**创建数据库**"。</span><span class="sxs-lookup"><span data-stu-id="2eede-131">In the Azure: Cosmos DB pane, right-click your new account, and then click **Create Database**.</span></span>
1. <span data-ttu-id="2eede-132">在屏幕顶部的 "输入调色板" 中, 键入`Users`数据库名称, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="2eede-132">In the input palette at the top of the screen, type `Users` for the database name and press Enter.</span></span>
1. <span data-ttu-id="2eede-133">输入`WebCustomers`集合名称, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="2eede-133">Enter `WebCustomers` for the collection name and press Enter.</span></span>
1. <span data-ttu-id="2eede-134">为`userId`分区键输入, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="2eede-134">Enter `userId` for the partition key and press Enter.</span></span>
1. <span data-ttu-id="2eede-135">最后, 确认`1000`初始吞吐量容量, 然后按 enter 键。</span><span class="sxs-lookup"><span data-stu-id="2eede-135">Finally, confirm `1000` for the initial throughput capacity and press Enter.</span></span>
1. <span data-ttu-id="2eede-136">展开 " **Azure: Cosmos DB** " 窗格中的帐户, 将显示新的 "**用户**数据库" 和 " **WebCustomers** " 集合。</span><span class="sxs-lookup"><span data-stu-id="2eede-136">Expand the account in the **Azure: Cosmos DB** pane, and the new **Users** database and **WebCustomers** collection are displayed.</span></span>

    ![显示以上说明的动画在 Visual Studio Code 中通过 Azure Cosmos DB 扩展运行。](../media/2-setup/vs-code-azure-cosmos-db-extension.gif)

<span data-ttu-id="2eede-138">现在, 你已拥有 Azure Cosmos DB 帐户, 我们可以在 Visual Studio Code 中使用它!</span><span class="sxs-lookup"><span data-stu-id="2eede-138">Now that you have your Azure Cosmos DB account, lets get to work in Visual Studio Code!</span></span>
