<span data-ttu-id="acf58-101">请记住, 您的分析师的财务模型是在 Azure 虚拟机上运行的。</span><span class="sxs-lookup"><span data-stu-id="acf58-101">Recall that your analysts' financial models are run on Azure virtual machines.</span></span> <span data-ttu-id="acf58-102">若要进一步自动化部署, 您需要从 Azure CLI 命令和脚本迁移到资源管理器模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-102">To further automate your deployments, you want to move from Azure CLI commands and scripts to Resource Manager templates.</span></span>

<span data-ttu-id="acf58-103">在开始之前, 您可能首先想知道哪些现有模板存在, 您可以从中进行学习和构建。</span><span class="sxs-lookup"><span data-stu-id="acf58-103">Before you begin, you might first wonder what existing templates exist that you can learn from and build upon.</span></span>

<span data-ttu-id="acf58-104">在这里, 你将了解什么是 Azure 快速入门模板以及哪些预建模板可供你立即使用。</span><span class="sxs-lookup"><span data-stu-id="acf58-104">Here you'll explore what an Azure Quickstart template is and what prebuilt templates are available for you to use right now.</span></span>

> [!TIP]
> <span data-ttu-id="acf58-105">首选 Linux 或想要尝试一些新的功能？</span><span class="sxs-lookup"><span data-stu-id="acf58-105">Prefer Linux or want to try something new?</span></span> <span data-ttu-id="acf58-106">从本页顶部选择 " **linux** " 以部署 linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="acf58-106">Select **Linux** from the top of this page to deploy a Linux virtual machine.</span></span>

## <a name="what-are-azure-quickstart-templates"></a><span data-ttu-id="acf58-107">什么是 Azure 快速入门模板？</span><span class="sxs-lookup"><span data-stu-id="acf58-107">What are Azure Quickstart templates?</span></span>

<span data-ttu-id="acf58-108">azure 快速入门模板是由 Azure 社区提供的资源管理器模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-108">Azure Quickstart templates are Resource Manager templates that are provided by the Azure community.</span></span> <span data-ttu-id="acf58-109">GitHub 上提供了快速启动模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-109">Quickstart templates are available on GitHub.</span></span>

<span data-ttu-id="acf58-110">许多模板都提供了部署解决方案所需的一切。</span><span class="sxs-lookup"><span data-stu-id="acf58-110">Many templates provide everything you need to deploy your solution.</span></span> <span data-ttu-id="acf58-111">其他人可以作为你的模板的起始点。</span><span class="sxs-lookup"><span data-stu-id="acf58-111">Others might serve as a starting point for your template.</span></span> <span data-ttu-id="acf58-112">无论哪种方式, 都可以研究这些模板, 以了解如何最大限度地创作和构造自己的模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-112">Either way, you can study these templates to learn how to best author and structure your own templates.</span></span>

## <a name="discover-whats-on-the-quickstart-template-gallery"></a><span data-ttu-id="acf58-113">了解快速入门模板库中的内容</span><span class="sxs-lookup"><span data-stu-id="acf58-113">Discover what's on the Quickstart template gallery</span></span>

<span data-ttu-id="acf58-114">假设您要查找一个资源管理器模板, 该模板将提供一个包含 VM、 &ndash;基本网络设置和存储的基本 VM 配置。</span><span class="sxs-lookup"><span data-stu-id="acf58-114">Let's say you want to find a Resource Manager template that brings up a basic VM configuration &ndash; one that includes a VM, basic network settings, and storage.</span></span>

1. <span data-ttu-id="acf58-115">首先, 浏览到[快速入门模板库](https://azure.microsoft.com/resources/templates?azure-portal=true)以查看可用内容。</span><span class="sxs-lookup"><span data-stu-id="acf58-115">Start by browsing to the [Quickstart template gallery](https://azure.microsoft.com/resources/templates?azure-portal=true) to see what's available.</span></span>

    <span data-ttu-id="acf58-116">你将看到许多受欢迎和最近更新的模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-116">You see a number of popular and recently updated templates.</span></span> <span data-ttu-id="acf58-117">这些模板适用于 Azure 资源和受欢迎的软件包。</span><span class="sxs-lookup"><span data-stu-id="acf58-117">These templates work with both Azure resources and popular software packages.</span></span>

    ![Azure 快速入门模板库网页的一部分。](../../media/3-gallery-homepage.png)

1. <span data-ttu-id="acf58-119">假设您在[部署一个简单的 Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows?azure-portal=true)模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-119">Let's say you come across the [Deploy a simple Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows?azure-portal=true) template.</span></span>

    ![Windows VM 模板的库页面](../../media/3-gallery-page-windows.png)

    <span data-ttu-id="acf58-121">名称听起来像你所需的那样。</span><span class="sxs-lookup"><span data-stu-id="acf58-121">The name sounds like exactly what you need.</span></span> <span data-ttu-id="acf58-122">不过, 让我们进一步了解一下此模板的功能。</span><span class="sxs-lookup"><span data-stu-id="acf58-122">But let's take a closer look to see what this template accomplishes.</span></span>

    <span data-ttu-id="acf58-123">使用 "**部署到 Azure** " 按钮, 可以直接通过 Azure 门户部署模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-123">The **Deploy to Azure** button enables you to deploy the template directly through the Azure portal.</span></span> <span data-ttu-id="acf58-124">但此处不会执行此操作。</span><span class="sxs-lookup"><span data-stu-id="acf58-124">But you won't do that here.</span></span> <span data-ttu-id="acf58-125">相反, 你将使用 Azure CLI 从云命令行管理程序部署模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-125">Rather, you'll use the Azure CLI to deploy the template from Cloud Shell.</span></span>

1. <span data-ttu-id="acf58-126">单击**github 上**的 "浏览" 以导航到 github 上的模板源代码。</span><span class="sxs-lookup"><span data-stu-id="acf58-126">Click **Browse on GitHub** to navigate to the template's source code on GitHub.</span></span>

    <span data-ttu-id="acf58-127">你会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="acf58-127">You see this.</span></span>

    ![适用于资源管理器模板的 GitHub 自述文件](../../media/3-github-page-windows.png)

    <span data-ttu-id="acf58-129">使用 "**部署到 Azure** " 按钮, 可以直接通过 Azure 门户部署模板, 就像您在库页面上看到的那样。</span><span class="sxs-lookup"><span data-stu-id="acf58-129">The **Deploy to Azure** button enables you to deploy the template directly through the Azure portal, just like you saw on the gallery page.</span></span>

1. <span data-ttu-id="acf58-130">单击 "**可视化**" 以导航到 Azure 资源管理器可视化工具。</span><span class="sxs-lookup"><span data-stu-id="acf58-130">Click **Visualize** to navigate to the Azure Resource Manager Visualizer.</span></span>

    <span data-ttu-id="acf58-131">你将看到构成部署的资源, 包括 VM、存储帐户和网络资源。</span><span class="sxs-lookup"><span data-stu-id="acf58-131">You see the resources that make up the deployment, including a VM, a storage account, and network resources.</span></span>

    <span data-ttu-id="acf58-132">您可以使用鼠标对资源进行排列。</span><span class="sxs-lookup"><span data-stu-id="acf58-132">You can use your mouse to arrange the resources.</span></span> <span data-ttu-id="acf58-133">您还可以使用鼠标的滚轮向外缩放。</span><span class="sxs-lookup"><span data-stu-id="acf58-133">You can also use your mouse's scroll wheel to zoom in an out.</span></span>

    ![以可视化方式显示 azure 资源的 azure 资源管理器可视化工具](../../media/3-armviz-windows.png)

1. <span data-ttu-id="acf58-135">单击标有 " **SimpleWinVM**" 的**虚拟机**资源。</span><span class="sxs-lookup"><span data-stu-id="acf58-135">Click on the **Virtual Machine** resource labeled **SimpleWinVM**.</span></span>

    <span data-ttu-id="acf58-136">您将看到定义 VM 资源的源代码。</span><span class="sxs-lookup"><span data-stu-id="acf58-136">You see the source code that defines the VM resource.</span></span>

    ![显示模板源代码的 Azure 资源管理器可视化工具](../../media/3-armviz-vm-windows.png)

    <span data-ttu-id="acf58-138">你将有更多的时间来检查源代码, 只需一位。</span><span class="sxs-lookup"><span data-stu-id="acf58-138">You'll have more time to inspect the source code in just a bit.</span></span> <span data-ttu-id="acf58-139">但现在, 请花些时间来简短地查看。</span><span class="sxs-lookup"><span data-stu-id="acf58-139">But for now, take a moment to review it briefly.</span></span>

    <span data-ttu-id="acf58-140">您会发现:</span><span class="sxs-lookup"><span data-stu-id="acf58-140">You see that:</span></span>

    * <span data-ttu-id="acf58-141">资源的类型为`Microsoft.Compute/virtualMachines`。</span><span class="sxs-lookup"><span data-stu-id="acf58-141">The resource's type is `Microsoft.Compute/virtualMachines`.</span></span>
    * <span data-ttu-id="acf58-142">它的位置 (或 Azure 区域) 来自名为`location`的模板参数。</span><span class="sxs-lookup"><span data-stu-id="acf58-142">It's location, or Azure region, comes from the template parameter named `location`.</span></span>
    * <span data-ttu-id="acf58-143">VM 的大小为**Standard_A2**。</span><span class="sxs-lookup"><span data-stu-id="acf58-143">The VM's size is **Standard_A2**.</span></span>
    * <span data-ttu-id="acf58-144">将从模板变量读取计算机名称, 并从模板参数中读取 VM 的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="acf58-144">The computer name is read from a template variable and the username and password for the VM are read from template parameters.</span></span>

<span data-ttu-id="acf58-145">在实践中, 您可能会查看 GitHub 上的**README.md**文件, 并进一步检查源代码以查看此模板是否符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="acf58-145">In practice, you might review the **README.md** file on GitHub and further inspect the source code to see whether this template suits your needs.</span></span>

<span data-ttu-id="acf58-146">但现在, 此模板看起来是有代表性的。</span><span class="sxs-lookup"><span data-stu-id="acf58-146">But for now, this template looks promising.</span></span> <span data-ttu-id="acf58-147">在下一部分中, 你将继续并部署此模板。</span><span class="sxs-lookup"><span data-stu-id="acf58-147">In the next part, you'll go ahead and deploy this template.</span></span>
