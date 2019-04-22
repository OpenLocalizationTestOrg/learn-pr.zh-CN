<span data-ttu-id="5e17d-101">在此单元中, 我们将创建一个使用计时器触发器每隔20秒调用的 Azure function app。</span><span class="sxs-lookup"><span data-stu-id="5e17d-101">In this unit, we create an Azure function app that's invoked every 20 seconds using a timer trigger.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="5e17d-102">创建 Azure 函数应用</span><span class="sxs-lookup"><span data-stu-id="5e17d-102">Create an Azure function app</span></span>

<span data-ttu-id="5e17d-103">让我们先在门户中创建一个 Azure 函数应用程序。</span><span class="sxs-lookup"><span data-stu-id="5e17d-103">Let’s start by creating an Azure Function app in the portal.</span></span>

1. <span data-ttu-id="5e17d-104">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="5e17d-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="5e17d-105">在左侧导航中, 选择 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="5e17d-106">选择 "**计算**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-106">Select **Compute**.</span></span>

1. <span data-ttu-id="5e17d-107">查找并选择**函数应用**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-107">Locate and select **Function App**.</span></span> <span data-ttu-id="5e17d-108">您还可以选择使用搜索栏来查找和创建新资源。</span><span class="sxs-lookup"><span data-stu-id="5e17d-108">You can also optionally use the search bar to locate and create the new resource.</span></span>

    ![显示 "创建资源" 边栏突出显示了 Function 应用程序的 Azure 门户屏幕截图。](../media/4-click-function-app.png)

1. <span data-ttu-id="5e17d-110">输入全局唯一的**应用程序名称**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-110">Enter a globally unique **App name**.</span></span>

1. <span data-ttu-id="5e17d-111">选择**订阅**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="5e17d-112">选择 "现有**资源组** <rgn>[沙盒资源组名称]</rgn>"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-112">Select the existing **Resource group** <rgn>[sandbox resource group name]</rgn>.</span></span>

1. <span data-ttu-id="5e17d-113">选择 " **Windows** " 作为**操作系统**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="5e17d-114">为您的**托管计划**选择**消耗计划**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="5e17d-115">使用消耗计划类型时, 将根据您的应用程序工作负载自动分配每个函数的执行费用, 并自动分配资源。</span><span class="sxs-lookup"><span data-stu-id="5e17d-115">When using the Consumption Plan type you're charged for each execution of your function and resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="5e17d-116">从下面的 "可用" 列表中选择一个**位置**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-116">Select a **Location** from the available list below.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="5e17d-117">对于**运行时堆栈**, 请将其保留为默认 *.net*, 这是我们在本练习中实现函数示例所采用的语言。</span><span class="sxs-lookup"><span data-stu-id="5e17d-117">For **Runtime Stack**, leave as default *.NET*, which is the language in which we implement the function examples in this exercise.</span></span>

1. <span data-ttu-id="5e17d-118">创建新的**存储**帐户, 可以根据需要更改名称-它将默认为应用程序名称的变体。</span><span class="sxs-lookup"><span data-stu-id="5e17d-118">Create a new **Storage** account, you can change the name if you like - it will default to a variation of the App name.</span></span>

1. <span data-ttu-id="5e17d-119">选择 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-119">Select **Create**.</span></span> <span data-ttu-id="5e17d-120">部署函数应用后, 请转到门户中的**所有资源**。</span><span class="sxs-lookup"><span data-stu-id="5e17d-120">Once the function app is deployed, go to **All resources** in the portal.</span></span> <span data-ttu-id="5e17d-121">将使用 type **app Service**列出函数应用程序, 并为其赋予名称。</span><span class="sxs-lookup"><span data-stu-id="5e17d-121">The function app will be listed with type **App Service** and has the name you gave it.</span></span>
 
## <a name="create-a-timer-trigger"></a><span data-ttu-id="5e17d-122">创建计时器触发器</span><span class="sxs-lookup"><span data-stu-id="5e17d-122">Create a timer trigger</span></span>

<span data-ttu-id="5e17d-123">现在, 我们要在函数中创建计时器触发器。</span><span class="sxs-lookup"><span data-stu-id="5e17d-123">Now we're going to create a timer trigger inside our function.</span></span>

1. <span data-ttu-id="5e17d-124">选择 "函数"**+** 旁边的 "添加\*\*\*\*" () 按钮。</span><span class="sxs-lookup"><span data-stu-id="5e17d-124">Select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="5e17d-125">此操作将启动函数创建过程。</span><span class="sxs-lookup"><span data-stu-id="5e17d-125">This action starts the function creation process.</span></span>

1. <span data-ttu-id="5e17d-126">在 "**适用于 .net 的 Azure 函数-入门**" 页上, 选择 "**在门户中**", 然后选择 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-126">On the **Azure Functions for .NET - getting started** page, select **In-portal** and then select **continue**.</span></span>

1. <span data-ttu-id="5e17d-127">在 "快速启动" 模板列表中, 选择 "**计时器**", 然后在屏幕底部选择 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-127">In the list of quick start templates, select **Timer** and then select **Create** at the bottom of the screen.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="5e17d-128">配置计时器触发器</span><span class="sxs-lookup"><span data-stu-id="5e17d-128">Configure the timer trigger</span></span>

<span data-ttu-id="5e17d-129">我们有一个使用逻辑将消息打印到日志窗口的 Azure function app。</span><span class="sxs-lookup"><span data-stu-id="5e17d-129">We have an Azure function app with logic to print a message to the log window.</span></span> <span data-ttu-id="5e17d-130">我们打算将计时器的日程安排设置为每隔20秒执行一次。</span><span class="sxs-lookup"><span data-stu-id="5e17d-130">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="5e17d-131">选择 "**集成**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-131">Select **Integrate**.</span></span>

1. <span data-ttu-id="5e17d-132">在 "**计划**" 框中输入以下值:</span><span class="sxs-lookup"><span data-stu-id="5e17d-132">Enter the following value into the **Schedule** box:</span></span>

    ```log
    */20 * * * * *
    ```

1. <span data-ttu-id="5e17d-133">选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-133">Select **Save**.</span></span>

## <a name="test-the-timer"></a><span data-ttu-id="5e17d-134">测试计时器</span><span class="sxs-lookup"><span data-stu-id="5e17d-134">Test the timer</span></span>

<span data-ttu-id="5e17d-135">现在我们已经配置了计时器, 它将按我们定义的间隔调用函数。</span><span class="sxs-lookup"><span data-stu-id="5e17d-135">Now that we've configured the timer, it will invoke the function on the interval we defined.</span></span>

1. <span data-ttu-id="5e17d-136">选择 " **TimerTrigger1**"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-136">Select **TimerTrigger1**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e17d-137">**TimerTrigger1**是默认名称。</span><span class="sxs-lookup"><span data-stu-id="5e17d-137">**TimerTrigger1** is a default name.</span></span> <span data-ttu-id="5e17d-138">当您创建触发器时, 它会自动选中。</span><span class="sxs-lookup"><span data-stu-id="5e17d-138">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="5e17d-139">打开屏幕底部的**日志**面板。</span><span class="sxs-lookup"><span data-stu-id="5e17d-139">Open the **Logs** panel at the bottom of the screen.</span></span>

1. <span data-ttu-id="5e17d-140">在日志窗口中观察新邮件每隔20秒到达一次。</span><span class="sxs-lookup"><span data-stu-id="5e17d-140">Observe new messages arrive every 20 seconds in the log window.</span></span>

1. <span data-ttu-id="5e17d-141">若要停止运行该函数, 请选择 "**管理**", 然后将 "**函数状态**" 切换为 "*已禁用*"。</span><span class="sxs-lookup"><span data-stu-id="5e17d-141">To stop the function from running, select **Manage** and then switch **Function State** to *Disabled*.</span></span>
