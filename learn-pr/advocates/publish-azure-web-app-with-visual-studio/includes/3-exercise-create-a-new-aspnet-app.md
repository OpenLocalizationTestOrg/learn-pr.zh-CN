<span data-ttu-id="30dd1-101">在此单元中, 您将在本地计算机上创建、生成和运行新的 ASP.NET web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="30dd1-101">In this unit, you will create, build, and run a new ASP.NET web application on your local machine.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="30dd1-102">创建项目</span><span class="sxs-lookup"><span data-stu-id="30dd1-102">Create a project</span></span>

<span data-ttu-id="30dd1-103">第一步是启动 Visual Studio 并创建一个本地 ASP.NET Core web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="30dd1-103">The first step is to start Visual Studio and create a local ASP.NET Core web application.</span></span>

1. <span data-ttu-id="30dd1-104">在 Visual Studio "开始" 页上, 依次选择 "**文件**"、"**新建**" 和 "**项目 ...**"。</span><span class="sxs-lookup"><span data-stu-id="30dd1-104">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="30dd1-105">在 "**新建项目**" 对话框的左侧窗格中, 选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="30dd1-105">In the **New Project** dialog box, on the left-hand pane, select **Web**.</span></span>

1. <span data-ttu-id="30dd1-106">在中心窗格中, 单击 " **ASP.NET Core Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="30dd1-106">In the center pane, click **ASP.NET Core Web Application**.</span></span>

1. <span data-ttu-id="30dd1-107">在对话框底部的 "**名称**" 字段中, 输入**AlpineSkiHouse**。</span><span class="sxs-lookup"><span data-stu-id="30dd1-107">At the bottom of the dialog box, in the **Name** field, enter **AlpineSkiHouse**.</span></span>

1. <span data-ttu-id="30dd1-108">选择新解决方案的**位置**。</span><span class="sxs-lookup"><span data-stu-id="30dd1-108">Select a **Location** for your new solution.</span></span>

1. <span data-ttu-id="30dd1-109">单击 **"确定"** 按钮创建项目。</span><span class="sxs-lookup"><span data-stu-id="30dd1-109">Click the **OK** button to create your project.</span></span>

1. <span data-ttu-id="30dd1-110">在 "**新建 ASP.NET Core Web 应用程序**" 对话框中, 您将看到 "启动模板" 选项。</span><span class="sxs-lookup"><span data-stu-id="30dd1-110">In the **New ASP.NET Core Web Application** dialog box, you will see a selection of starting templates.</span></span> <span data-ttu-id="30dd1-111">在本练习中, 选择 " **Web 应用程序**", 然后单击 **"确定"** 以创建项目。</span><span class="sxs-lookup"><span data-stu-id="30dd1-111">For this exercise, select **Web Application**, and then click **OK** to create your project.</span></span>

    !['新建项目'对话框](../media/3-aspnet-templates.png)

    > [!NOTE]
    > <span data-ttu-id="30dd1-113">您还可以根据 web 开发要求, 在此对话框中选择不同的起始模板。</span><span class="sxs-lookup"><span data-stu-id="30dd1-113">You can also select different starting templates in this dialog box depending on your web development requirements.</span></span> <span data-ttu-id="30dd1-114">在对话框的顶部, 您还可以选择 ASP.NET Core 的版本。</span><span class="sxs-lookup"><span data-stu-id="30dd1-114">At the top of the dialog box, you are also able to select the version of ASP.NET Core.</span></span> <span data-ttu-id="30dd1-115">应选择 ASP.NET Core 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="30dd1-115">You should select ASP.NET Core 2.0 or later.</span></span>

1. <span data-ttu-id="30dd1-116">现在, 您应具有新的 ASP.NET Core web 应用程序解决方案。</span><span class="sxs-lookup"><span data-stu-id="30dd1-116">You should now have your new ASP.NET Core web application solution.</span></span>

    !['新建项目'对话框](../media/3-new-solution.png)

## <a name="build-and-test-on-your-local-machine"></a><span data-ttu-id="30dd1-118">在本地计算机上生成和测试</span><span class="sxs-lookup"><span data-stu-id="30dd1-118">Build and test on your local machine</span></span>

<span data-ttu-id="30dd1-119">现在, 让我们在将应用程序部署到 Azure 之前, 在本地计算机上生成并测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="30dd1-119">Now, let's build and test your application on your local machine before deploying to Azure.</span></span>

1. <span data-ttu-id="30dd1-120">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="30dd1-120">Run the app</span></span>

    <span data-ttu-id="30dd1-121">按<kbd>F5</kbd>生成项目并在调试模式下运行。</span><span class="sxs-lookup"><span data-stu-id="30dd1-121">Press <kbd>F5</kbd> to build the project and run in debug mode.</span></span>

    <span data-ttu-id="30dd1-122">按<kbd>Ctrl + F5</kbd>生成项目并运行而不附加调试器。</span><span class="sxs-lookup"><span data-stu-id="30dd1-122">Press <kbd>Ctrl+F5</kbd> to build the project and run without attaching the debugger.</span></span>
    
    > [!TIP]
    > <span data-ttu-id="30dd1-123">以非调试模式启动应用程序, 可以更改代码, 保存文件, 刷新浏览器, 并查看代码更改。</span><span class="sxs-lookup"><span data-stu-id="30dd1-123">Launching the app in non-debug mode allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="30dd1-124">许多开发人员更喜欢使用非调试模式来快速启动应用程序并查看更改。</span><span class="sxs-lookup"><span data-stu-id="30dd1-124">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

1. <span data-ttu-id="30dd1-125">Visual Studio 启动 IIS Express web 浏览器并加载该应用程序。</span><span class="sxs-lookup"><span data-stu-id="30dd1-125">Visual Studio starts the IIS Express web browser and loads the app.</span></span>

    ![在浏览器中运行的 web 应用程序](../media/3-webapp-launch-windows.png)

    <span data-ttu-id="30dd1-127">当 Visual Studio 创建 web 项目时, web 服务器将使用随机端口。</span><span class="sxs-lookup"><span data-stu-id="30dd1-127">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="30dd1-128">在上图中, 端口号为44381。</span><span class="sxs-lookup"><span data-stu-id="30dd1-128">In the preceding image, the port number is 44381.</span></span> <span data-ttu-id="30dd1-129">运行应用程序时, 可能会看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="30dd1-129">When you run the app, you'll likely see a different port number.</span></span>


    > [!IMPORTANT]
    > <span data-ttu-id="30dd1-130">您可能会注意到网页顶部的部分提供了用于您的隐私和 cookie 使用策略的位置。</span><span class="sxs-lookup"><span data-stu-id="30dd1-130">You might notice the section at the top of the web page that provides a place for your privacy and cookie use policy.</span></span> <span data-ttu-id="30dd1-131">选择 "**接受**" 以同意跟踪。</span><span class="sxs-lookup"><span data-stu-id="30dd1-131">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="30dd1-132">此应用不会跟踪个人信息。</span><span class="sxs-lookup"><span data-stu-id="30dd1-132">This app doesn't track personal information.</span></span> <span data-ttu-id="30dd1-133">模板生成的代码包括有助于满足常规数据保护法规 (GDPR) 的资产。</span><span class="sxs-lookup"><span data-stu-id="30dd1-133">The template-generated code includes assets to help meet General Data Protection Regulation (GDPR).</span></span>

<span data-ttu-id="30dd1-134">现在, 您已从示例模板中创建了一个 web 应用程序, 并且该应用程序在本地运行。</span><span class="sxs-lookup"><span data-stu-id="30dd1-134">You've now created a web application from the sample template and it is running locally.</span></span> <span data-ttu-id="30dd1-135">下一步是将其部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="30dd1-135">The next step is to deploy it to Azure.</span></span>

