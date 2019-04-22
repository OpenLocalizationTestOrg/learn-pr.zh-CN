<span data-ttu-id="daf96-101">在此单元中, 我们将创建一个 Azure 函数, 在创建或更新 blob 时显示 blob 的名称和大小。</span><span class="sxs-lookup"><span data-stu-id="daf96-101">In this unit, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="daf96-102">创建 blob 触发器</span><span class="sxs-lookup"><span data-stu-id="daf96-102">Create a blob trigger</span></span>

<span data-ttu-id="daf96-103">同样, 让我们继续使用现有的 Azure 函数应用程序, 并添加 blob 触发器。</span><span class="sxs-lookup"><span data-stu-id="daf96-103">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="daf96-104">请确保使用随激活沙盒的相同帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="daf96-104">Make sure you are signed into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="daf96-105">导航到 "**所有资源**" 屏幕, 然后选择您的函数应用程序。</span><span class="sxs-lookup"><span data-stu-id="daf96-105">Navigate to the **All resources** screen and select your function app.</span></span>

1. <span data-ttu-id="daf96-106">指向 "**函数**", 然后选择加号 (+) 图标。</span><span class="sxs-lookup"><span data-stu-id="daf96-106">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="daf96-107">选择 " **Blob 触发器**"。</span><span class="sxs-lookup"><span data-stu-id="daf96-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="daf96-108">如果您看到一条消息, 指出**未安装扩展**, 请选择 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="daf96-108">If you see a message saying  **Extensions not installed**, select **Install**.</span></span> <span data-ttu-id="daf96-109">依赖项安装可能需要几分钟时间, 因此请耐心等待。</span><span class="sxs-lookup"><span data-stu-id="daf96-109">Dependency installation can take a couple of minutes, so please be patient.</span></span> <span data-ttu-id="daf96-110">等待安装完成, 然后再继续。</span><span class="sxs-lookup"><span data-stu-id="daf96-110">Wait until the installation completes before continuing.</span></span>

1. <span data-ttu-id="daf96-111">将 "**名称**" 设置为默认值。</span><span class="sxs-lookup"><span data-stu-id="daf96-111">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="daf96-112">将**路径**设置为默认值。</span><span class="sxs-lookup"><span data-stu-id="daf96-112">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="daf96-113">选择 "**存储帐户连接**" 下拉列表旁边的 "_新建_" 链接。</span><span class="sxs-lookup"><span data-stu-id="daf96-113">Select the _new_ link next to the **Storage account connection** dropdown.</span></span> <span data-ttu-id="daf96-114">在显示的 "**存储帐户**选择" 对话框中, 选择此函数应用的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="daf96-114">In the **Storage Account** selection dialog that appears, select the storage account for this function app.</span></span>

1. <span data-ttu-id="daf96-115">返回到新的函数屏幕后, 选择 "**创建**" 以创建函数。</span><span class="sxs-lookup"><span data-stu-id="daf96-115">Once you have returned to the New Function screen, select **Create** to create the function.</span></span>

## <a name="create-a-blob-container"></a><span data-ttu-id="daf96-116">创建 blob 容器</span><span class="sxs-lookup"><span data-stu-id="daf96-116">Create a blob container</span></span>

<span data-ttu-id="daf96-117">现在, 我们已创建 blob 触发器, 我们将使用存储资源管理器创建 blob 并触发函数。</span><span class="sxs-lookup"><span data-stu-id="daf96-117">Now that we've created a blob trigger, let's use the Storage Explorer to create a blob and trigger the function.</span></span>

1. <span data-ttu-id="daf96-118">打开在新选项卡中使用 (或创建) 的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="daf96-118">Open the storage account you used (or created) in a new tab.</span></span>

    > [!TIP]
    > <span data-ttu-id="daf96-119">您可以在大多数浏览器中复制选项卡, 方法是右键单击 "问题" 选项卡, 然后从出现的菜单中选择 "**重复**"。</span><span class="sxs-lookup"><span data-stu-id="daf96-119">You can duplicate a tab in most browsers by right-clicking on the tab in question and selecting **Duplicate** from the menu that appears.</span></span> <span data-ttu-id="daf96-120">我们想要使用新的选项卡, 以便我们可以在正在使用的两个服务之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="daf96-120">We want to use a new tab so we can switch between the two services we are working with.</span></span>

1. <span data-ttu-id="daf96-121">选择侧栏中的 "**存储帐户**", 或选择侧栏中的 "**所有资源**", 然后按名称进行筛选。</span><span class="sxs-lookup"><span data-stu-id="daf96-121">Select **Storage accounts** in the sidebar, or select **All resources** in the sidebar and then filter by the name.</span></span>

1. <span data-ttu-id="daf96-122">单击 "**存储资源管理器 (预览)** " 部分, 这将打开一个新的面板, 可以在其中使用 blob 和文件。</span><span class="sxs-lookup"><span data-stu-id="daf96-122">Click on the **Storage Explorer (preview)** section - this will open a new panel where you can work with blobs and files.</span></span>

<span data-ttu-id="daf96-123">请记住, 我们的 blob 触发器仅监视**路径**字段中所述的位置。</span><span class="sxs-lookup"><span data-stu-id="daf96-123">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="daf96-124">默认情况下, 路径应为:</span><span class="sxs-lookup"><span data-stu-id="daf96-124">By default, our path should be:</span></span>

> <span data-ttu-id="daf96-125">示例-工作项/{名称}</span><span class="sxs-lookup"><span data-stu-id="daf96-125">samples-workitems/{name}</span></span>

<span data-ttu-id="daf96-126">我们需要创建一个名为 "**示例-工作项**" 的容器。</span><span class="sxs-lookup"><span data-stu-id="daf96-126">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="daf96-127">右键单击 " **BLOB 容器**", 然后选择 "**创建 BLOB 容器**"。</span><span class="sxs-lookup"><span data-stu-id="daf96-127">Right-click **BLOB CONTAINERS** and select **Create Blob Container**.</span></span>

1. <span data-ttu-id="daf96-128">输入**示例-工作项**作为名称, 将访问级别保留为默认的**专用**设置, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="daf96-128">Enter **samples-workitems** as the name, leave the access level at the default **Private** setting, and select **OK**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="daf96-129">打开 blob 触发器</span><span class="sxs-lookup"><span data-stu-id="daf96-129">Turn on your blob trigger</span></span>

<span data-ttu-id="daf96-130">现在我们已经创建了要监视的容器, 让我们运行我们的函数, 以便在创建 blob 时可以看到输出。</span><span class="sxs-lookup"><span data-stu-id="daf96-130">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="daf96-131">使用 Azure 函数切换回 "浏览器" 选项卡 (或重新打开)。</span><span class="sxs-lookup"><span data-stu-id="daf96-131">Switch back to the browser tab with your Azure Function (or reopen it).</span></span>

1. <span data-ttu-id="daf96-132">选择您的 blob 触发器以打开 "代码" 屏幕。</span><span class="sxs-lookup"><span data-stu-id="daf96-132">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="daf96-133">打开屏幕底部的 "**日志**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="daf96-133">Open the **Logs** tab at the bottom of the screen.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="daf96-134">创建 blob</span><span class="sxs-lookup"><span data-stu-id="daf96-134">Create a blob</span></span>

<span data-ttu-id="daf96-135">我们的 blob 触发器现已准备好并在侦听活动。</span><span class="sxs-lookup"><span data-stu-id="daf96-135">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="daf96-136">让我们创建一个 blob, 以查看我们是否收到日志消息。</span><span class="sxs-lookup"><span data-stu-id="daf96-136">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="daf96-137">使用存储资源管理器切换回 "浏览器" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="daf96-137">Switch back to the browser tab with Storage Explorer.</span></span>

1. <span data-ttu-id="daf96-138">在存储资源管理器中, 从 " **BLOB 容器**" 列表中选择**示例工作项**容器。</span><span class="sxs-lookup"><span data-stu-id="daf96-138">In Storage Explorer, select the **samples-workitems** container from the **BLOB CONTAINERS** list.</span></span>

1. <span data-ttu-id="daf96-139">从工具栏中选择 "**上传**"。</span><span class="sxs-lookup"><span data-stu-id="daf96-139">Select **Upload** from the toolbar.</span></span>

1. <span data-ttu-id="daf96-140">从计算机中选择任何文件。</span><span class="sxs-lookup"><span data-stu-id="daf96-140">Select any file from your computer.</span></span>

1. <span data-ttu-id="daf96-141">在 "**身份验证类型**" 下, 选择**SAS**。</span><span class="sxs-lookup"><span data-stu-id="daf96-141">Under **Authentication type**, select **SAS**.</span></span>

1. <span data-ttu-id="daf96-142">选择 "**上传**"。</span><span class="sxs-lookup"><span data-stu-id="daf96-142">Select **Upload**.</span></span>

1. <span data-ttu-id="daf96-143">切换回 "Azure 函数" 选项卡, 并检查输出日志中是否有显示上载的文件的消息。</span><span class="sxs-lookup"><span data-stu-id="daf96-143">Switch back to the Azure Function tab and check the output logs for a message that displays what file was uploaded.</span></span> <span data-ttu-id="daf96-144">blob 触发器应自动执行。</span><span class="sxs-lookup"><span data-stu-id="daf96-144">Your blob trigger should automatically execute.</span></span> <span data-ttu-id="daf96-145">请注意, 如果单击 "函数" 窗口中的 "**运行**" 按钮, 则可能会由于**测试**请求正文中指定的默认值而出错。</span><span class="sxs-lookup"><span data-stu-id="daf96-145">Note that if you click the **Run** button in the function window, it will likely error due to the default value that is specified in the **Test** request body.</span></span> <span data-ttu-id="daf96-146">您需要将 "请求正文" 窗口中的路径更改为有效文件, 才能成功执行测试对话框。</span><span class="sxs-lookup"><span data-stu-id="daf96-146">You will need to change the path in the request body window to a valid file in order for the test dialog to execute successfully.</span></span>