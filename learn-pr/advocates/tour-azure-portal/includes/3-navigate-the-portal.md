<span data-ttu-id="51b3d-101">使用 Azure 帐户, 我们可以登录到**azure 门户**。</span><span class="sxs-lookup"><span data-stu-id="51b3d-101">With an Azure account, we can sign into the **Azure portal**.</span></span> <span data-ttu-id="51b3d-102">门户是一个基于 web 的管理网站, 可让您与您所创建的所有订阅和资源进行交互。</span><span class="sxs-lookup"><span data-stu-id="51b3d-102">The portal is a web-based administration site that lets you interact with all of your subscriptions and resources you have created.</span></span> <span data-ttu-id="51b3d-103">通过此 web 界面几乎可以完成 Azure 的所有操作。</span><span class="sxs-lookup"><span data-stu-id="51b3d-103">Almost everything you do with Azure can be done through this web interface.</span></span>

## <a name="azure-portal-layout"></a><span data-ttu-id="51b3d-104">Azure 门户布局</span><span class="sxs-lookup"><span data-stu-id="51b3d-104">Azure portal layout</span></span>

<span data-ttu-id="51b3d-105">Azure 门户是用于控制 Microsoft Azure 的主要图形用户界面 (GUI)。</span><span class="sxs-lookup"><span data-stu-id="51b3d-105">The Azure portal is the primary graphical user interface (GUI) for controlling Microsoft Azure.</span></span> <span data-ttu-id="51b3d-106">您可以在门户中执行大部分管理操作, 这通常是执行单个任务或要详细查看配置选项的最佳界面。</span><span class="sxs-lookup"><span data-stu-id="51b3d-106">You can carry out the majority of management actions in the portal, and it is typically the best interface for carrying out single tasks or where you want to look at the configuration options in detail.</span></span>

![Azure 门户的屏幕截图](../media/3-portal.png)

:::row:::
    :::column:::
    ![资源和收藏夹边栏屏幕截图](../media/3-favorites.png)
    :::column-end:::
    :::column span="3":::
    <span data-ttu-id="51b3d-109">**资源面板**</span><span class="sxs-lookup"><span data-stu-id="51b3d-109">**Resource Panel**</span></span>
    
    <span data-ttu-id="51b3d-110">在门户的左侧边栏中是 "资源" 窗格, 其中列出了主要资源类型。</span><span class="sxs-lookup"><span data-stu-id="51b3d-110">In the left-hand sidebar of the portal is the resource pane, which lists the main resource types.</span></span> <span data-ttu-id="51b3d-111">请注意, Azure 的资源类型比显示的多。</span><span class="sxs-lookup"><span data-stu-id="51b3d-111">Note that Azure has more resource types than just those shown.</span></span> <span data-ttu-id="51b3d-112">列出的资源是_收藏夹_的一部分。</span><span class="sxs-lookup"><span data-stu-id="51b3d-112">The resources listed are part of your _favorites_.</span></span> 

    <span data-ttu-id="51b3d-113">您可以使用您通常要创建或管理的特定资源类型对此进行自定义。</span><span class="sxs-lookup"><span data-stu-id="51b3d-113">You can customize this with the specific resource types you tend to create or administer most often.</span></span> 

    <span data-ttu-id="51b3d-114">您还可以折叠此窗格;使用**<<** 插入符号。</span><span class="sxs-lookup"><span data-stu-id="51b3d-114">You can also collapse this pane; with the **<<** caret.</span></span> <span data-ttu-id="51b3d-115">这样可以将其最小化为图标, 如果你使用的是有限的屏幕房地产, 这会非常方便。</span><span class="sxs-lookup"><span data-stu-id="51b3d-115">This will minimize it to just icons which can be convenient if you are working with limited screen real-estate.</span></span>
    :::column-end:::
:::row-end:::

<span data-ttu-id="51b3d-116">门户视图的其余部分是针对您正在使用的特定元素的。</span><span class="sxs-lookup"><span data-stu-id="51b3d-116">The remainder of the portal view is for the specific elements you are working with.</span></span> <span data-ttu-id="51b3d-117">默认 (主) 页面是_仪表板_。</span><span class="sxs-lookup"><span data-stu-id="51b3d-117">The default (main) page is the _dashboard_.</span></span> <span data-ttu-id="51b3d-118">我们将在后面介绍, 但这表示你的资源可自定义的鸟瞰视图。</span><span class="sxs-lookup"><span data-stu-id="51b3d-118">We'll cover later, but this represents a customizable birds-eye-view of your resources.</span></span> <span data-ttu-id="51b3d-119">您可以使用它来跳转到您想要管理的特定资源, 或使用资源面板中的 "**所有资源**" 条目搜索资源。</span><span class="sxs-lookup"><span data-stu-id="51b3d-119">You can use it to jump into specific resources you want to manage or search for resources with the **All resources** entry in the resource panel.</span></span> <span data-ttu-id="51b3d-120">在管理资源 (例如虚拟机或 web 应用程序) 时, 您将使用提供有关资源的特定信息的_刀片式服务器_。</span><span class="sxs-lookup"><span data-stu-id="51b3d-120">When you are managing a resource, such as a virtual machine or a web app, you will work with a _blade_ that presents specific information about the resource.</span></span>

## <a name="what-is-a-blade"></a><span data-ttu-id="51b3d-121">什么是刀片？</span><span class="sxs-lookup"><span data-stu-id="51b3d-121">What is a blade?</span></span>

<span data-ttu-id="51b3d-122">Azure 门户使用刀片模型进行导航。</span><span class="sxs-lookup"><span data-stu-id="51b3d-122">The Azure portal uses a blades model for navigation.</span></span> <span data-ttu-id="51b3d-123">_刀片式服务器_是一个幻灯片输出面板, 其中包含导航序列中一个级别的 UI。</span><span class="sxs-lookup"><span data-stu-id="51b3d-123">A _blade_ is a slide-out panel containing the UI for a single level in a navigation sequence.</span></span> <span data-ttu-id="51b3d-124">例如, 此序列中的每个元素都将由刀片表示:**虚拟机** > **计算** > **Ubuntu 服务器**。</span><span class="sxs-lookup"><span data-stu-id="51b3d-124">For example, each of these elements in this sequence would be represented by a blade: **Virtual machines** > **Compute** > **Ubuntu Server**.</span></span>

<span data-ttu-id="51b3d-125">每个刀片都包含一些信息和可配置的选项。</span><span class="sxs-lookup"><span data-stu-id="51b3d-125">Each blade contains some information and configurable options.</span></span> <span data-ttu-id="51b3d-126">其中一些选项生成另一个叶片, 后者将自身显示在任何现有刀片式服务器的右侧。</span><span class="sxs-lookup"><span data-stu-id="51b3d-126">Some of these options generate another blade, which reveals itself to the right of any existing blade.</span></span> <span data-ttu-id="51b3d-127">在新的刀片式服务器上, 任何可进一步配置的选项将会产生其他刀片, 依此类推。</span><span class="sxs-lookup"><span data-stu-id="51b3d-127">On the new blade, any further configurable options will spawn another blade, and so on.</span></span> <span data-ttu-id="51b3d-128">很快你就可以同时打开多个刀片。</span><span class="sxs-lookup"><span data-stu-id="51b3d-128">Soon, you can end up with several blades open at the same time.</span></span> <span data-ttu-id="51b3d-129">您可以最大限度地利用刀片, 使其填满整个屏幕。</span><span class="sxs-lookup"><span data-stu-id="51b3d-129">You can maximize blades as well so that they fill the entire screen.</span></span>

<span data-ttu-id="51b3d-130">由于新的刀片式服务器总是添加到所有者的右侧, 因此您可以使用窗口底部的滚动条向后查看您在配置中对此点的访问方式。</span><span class="sxs-lookup"><span data-stu-id="51b3d-130">Since new blades are always added to the right of the owner, you can use the scrollbar at the bottom of the window to go backward to see how you got to this spot in the configuration.</span></span> <span data-ttu-id="51b3d-131">或者, 可以通过单击刀片式服务器上角的`X`按钮单独关闭刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="51b3d-131">Alternatively, you can close blades individually by clicking the `X` button in the top corner of the blade.</span></span> <span data-ttu-id="51b3d-132">如果你有未保存的更改, Azure 将提示你, 如果继续, 你的更改将会丢失。</span><span class="sxs-lookup"><span data-stu-id="51b3d-132">If you have unsaved changes, Azure will prompt you to let you know that the changes will be lost if you continue.</span></span>

## <a name="what-is-the-azure-marketplace"></a><span data-ttu-id="51b3d-133">什么是 Azure Marketplace？</span><span class="sxs-lookup"><span data-stu-id="51b3d-133">What is the Azure Marketplace?</span></span>

<span data-ttu-id="51b3d-134">您可以在门户中访问的一个 blade 是_Azure Marketplace_。</span><span class="sxs-lookup"><span data-stu-id="51b3d-134">One of the blades you can access in the portal is the _Azure Marketplace_.</span></span> <span data-ttu-id="51b3d-135">在 Azure 中创建新资源时, 通常会启动此刀片。</span><span class="sxs-lookup"><span data-stu-id="51b3d-135">This blade is often where you will start when creating new resources in Azure.</span></span> <span data-ttu-id="51b3d-136">通过市场, 客户可以从数百个领先的服务提供商处查找、试用、购买和预配应用程序和服务, 所有这些都已通过认证即可在 Azure 上运行。</span><span class="sxs-lookup"><span data-stu-id="51b3d-136">The Marketplace allows customers to find, try, purchase, and provision applications and services from hundreds of leading service providers, all certified to run on Azure.</span></span>

<span data-ttu-id="51b3d-137">解决方案目录跨多个行业类别, 包括但不限于开放源代码容器平台、虚拟机映像、数据库、应用程序生成和部署软件、开发人员工具、威胁检测和 blockchain。</span><span class="sxs-lookup"><span data-stu-id="51b3d-137">The solution catalog spans several industry categories, including but not limited to open-source container platforms, virtual machine images, databases, application build and deployment software, developer tools, threat detection, and blockchain.</span></span> <span data-ttu-id="51b3d-138">使用 Azure Marketplace, 可以在自己的 Azure 环境中快速且可靠地设置端到端解决方案。</span><span class="sxs-lookup"><span data-stu-id="51b3d-138">Using Azure Marketplace, you can provision end-to-end solutions quickly and reliably, hosted in your own Azure environment.</span></span> <span data-ttu-id="51b3d-139">在编写时, 这包括超过8000个列表。</span><span class="sxs-lookup"><span data-stu-id="51b3d-139">At the time of writing, this includes over 8,000 listings.</span></span>

> [!NOTE]
> <span data-ttu-id="51b3d-140">虽然 Azure Marketplace 专为面向商业和 IT 软件的 IT 专业人员和云开发人员而设计, 但 Microsoft 合作伙伴也将其用作所有联合走向市场活动的启动点。</span><span class="sxs-lookup"><span data-stu-id="51b3d-140">While Azure Marketplace is designed for IT professionals and cloud developers interested in commercial and IT software, Microsoft Partners also use it as a launch point for all joint Go-To-Market activities.</span></span>

## <a name="configuring-settings-in-the-azure-portal"></a><span data-ttu-id="51b3d-141">在 Azure 门户中配置设置</span><span class="sxs-lookup"><span data-stu-id="51b3d-141">Configuring settings in the Azure portal</span></span>

<span data-ttu-id="51b3d-142">Azure 门户显示了几个配置选项, 它们主要位于屏幕右上角的状态栏中。</span><span class="sxs-lookup"><span data-stu-id="51b3d-142">The Azure portal displays several configuration options, mostly in the status bar at the top-right of the screen.</span></span>

### <a name="notifications"></a><span data-ttu-id="51b3d-143">通知</span><span class="sxs-lookup"><span data-stu-id="51b3d-143">Notifications</span></span>

<span data-ttu-id="51b3d-144">单击电铃图标将显示 "**通知**" 窗格。</span><span class="sxs-lookup"><span data-stu-id="51b3d-144">Clicking the bell icon displays the **Notifications** pane.</span></span> <span data-ttu-id="51b3d-145">此窗格列出了上次执行的操作及其状态。</span><span class="sxs-lookup"><span data-stu-id="51b3d-145">This pane lists the last actions that have been carried out, along with their status.</span></span>

### <a name="cloud-shell"></a><span data-ttu-id="51b3d-146">云命令行管理程序</span><span class="sxs-lookup"><span data-stu-id="51b3d-146">Cloud Shell</span></span>

<span data-ttu-id="51b3d-147">如果单击**云命令行**管理程序图标 (>_), 将创建新的 Azure 云 shell 会话。</span><span class="sxs-lookup"><span data-stu-id="51b3d-147">If you click the **Cloud Shell** icon (>_), you will create a new Azure Cloud Shell session.</span></span> <span data-ttu-id="51b3d-148">回想一下, azure 云命令行管理程序是用于管理 Azure 资源的交互式、浏览器访问的命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="51b3d-148">Recall that Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span> <span data-ttu-id="51b3d-149">它提供了选择最适合您工作方式的命令行管理程序体验的灵活性。</span><span class="sxs-lookup"><span data-stu-id="51b3d-149">It provides the flexibility of choosing the shell experience that best suits the way you work.</span></span> <span data-ttu-id="51b3d-150">Linux 用户可以选择获取 Bash 体验, 而 Windows 用户可以选择使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="51b3d-150">Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.</span></span> <span data-ttu-id="51b3d-151">通过此基于浏览器的终端, 可以通过在门户中内置的命令行界面来控制和管理当前订阅中的所有 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="51b3d-151">This browser-based terminal lets you control and administer all of your Azure resources in the current subscription through a command-line interface built right into the portal.</span></span>

### <a name="settings"></a><span data-ttu-id="51b3d-152">Settings</span><span class="sxs-lookup"><span data-stu-id="51b3d-152">Settings</span></span>

<span data-ttu-id="51b3d-153">单击**齿轮**图标可更改 Azure 门户设置。</span><span class="sxs-lookup"><span data-stu-id="51b3d-153">Click the **gear** icon to change the Azure portal settings.</span></span> <span data-ttu-id="51b3d-154">这些设置包括:</span><span class="sxs-lookup"><span data-stu-id="51b3d-154">These settings include:</span></span>

- <span data-ttu-id="51b3d-155">注销时间</span><span class="sxs-lookup"><span data-stu-id="51b3d-155">Sign out time</span></span>
- <span data-ttu-id="51b3d-156">颜色和对比度主题</span><span class="sxs-lookup"><span data-stu-id="51b3d-156">Color and contrast themes</span></span>
- <span data-ttu-id="51b3d-157">Toast 通知 (移动设备)</span><span class="sxs-lookup"><span data-stu-id="51b3d-157">Toast notifications (to a mobile device)</span></span>
- <span data-ttu-id="51b3d-158">语言和区域格式</span><span class="sxs-lookup"><span data-stu-id="51b3d-158">Language and regional format</span></span>

![门户设置边栏的屏幕截图](../media/3-settings-blade.png)

<span data-ttu-id="51b3d-160">更改设置后, 单击 "**应用**" 接受更改。</span><span class="sxs-lookup"><span data-stu-id="51b3d-160">When you have changed settings, click **Apply** to accept your changes.</span></span>

### <a name="feedback-blade"></a><span data-ttu-id="51b3d-161">反馈刀片</span><span class="sxs-lookup"><span data-stu-id="51b3d-161">Feedback blade</span></span>

<span data-ttu-id="51b3d-162">**笑脸**图标将打开 "**向我们发送反馈**" 边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="51b3d-162">The **smiley face** icon opens the **Send us feedback** blade.</span></span> <span data-ttu-id="51b3d-163">你可以在此处向 Microsoft 发送关于 Azure 的反馈。</span><span class="sxs-lookup"><span data-stu-id="51b3d-163">Here you can send feedback to Microsoft about Azure.</span></span> <span data-ttu-id="51b3d-164">你可以作为反馈的一部分决定 Microsoft 能否通过电子邮件响应你的反馈。</span><span class="sxs-lookup"><span data-stu-id="51b3d-164">You can decide as part of your feedback whether Microsoft can respond to your feedback by email.</span></span>

### <a name="help-blade"></a><span data-ttu-id="51b3d-165">帮助边栏</span><span class="sxs-lookup"><span data-stu-id="51b3d-165">Help blade</span></span>

<span data-ttu-id="51b3d-166">单击**问号**图标以显示 "**帮助**" 边栏选项卡。</span><span class="sxs-lookup"><span data-stu-id="51b3d-166">Click the **question mark** icon to show the **Help** blade.</span></span> <span data-ttu-id="51b3d-167">从多个选项中进行选择, 包括:</span><span class="sxs-lookup"><span data-stu-id="51b3d-167">Here you choose from several options, including:</span></span>

- <span data-ttu-id="51b3d-168">帮助 + 支持</span><span class="sxs-lookup"><span data-stu-id="51b3d-168">Help + Support</span></span>
- <span data-ttu-id="51b3d-169">新增功能</span><span class="sxs-lookup"><span data-stu-id="51b3d-169">What's new</span></span>
- <span data-ttu-id="51b3d-170">Azure 路线图</span><span class="sxs-lookup"><span data-stu-id="51b3d-170">Azure roadmap</span></span>
- <span data-ttu-id="51b3d-171">启动引导教程</span><span class="sxs-lookup"><span data-stu-id="51b3d-171">Launch guided tour</span></span>
- <span data-ttu-id="51b3d-172">键盘快捷方式</span><span class="sxs-lookup"><span data-stu-id="51b3d-172">Keyboard shortcuts</span></span>
- <span data-ttu-id="51b3d-173">显示诊断</span><span class="sxs-lookup"><span data-stu-id="51b3d-173">Show diagnostics</span></span>
- <span data-ttu-id="51b3d-174">隐私 + 条款</span><span class="sxs-lookup"><span data-stu-id="51b3d-174">Privacy + terms</span></span>

#### <a name="help--support-options"></a><span data-ttu-id="51b3d-175">帮助 + 支持选项</span><span class="sxs-lookup"><span data-stu-id="51b3d-175">Help + Support options</span></span>

<span data-ttu-id="51b3d-176">这将打开 Azure 门户的主要支持区域, 其中包含各种常见问题的文档选项。</span><span class="sxs-lookup"><span data-stu-id="51b3d-176">This opens the main support area for the Azure portal and includes documentation options for a variety of common questions.</span></span> <span data-ttu-id="51b3d-177">此处的一个隐藏区域是此页上的**新的支持请求**链接。</span><span class="sxs-lookup"><span data-stu-id="51b3d-177">One of the hidden areas here is the **New support request** link which is on this page.</span></span> <span data-ttu-id="51b3d-178">这是你可以使用 Azure 团队打开支持票证的方法。</span><span class="sxs-lookup"><span data-stu-id="51b3d-178">This is how you can open a support ticket with the Azure team.</span></span>

> [!NOTE] 
> <span data-ttu-id="51b3d-179">所有 Azure 客户都可以访问帐单、配额和订阅管理支持。</span><span class="sxs-lookup"><span data-stu-id="51b3d-179">All Azure customers can access billing, quota, and subscription-management support.</span></span> <span data-ttu-id="51b3d-180">对*其他问题的支持可用性取决于您所拥有的支持计划*。</span><span class="sxs-lookup"><span data-stu-id="51b3d-180">*The availability of support for other issues depends on the support plan you have*.</span></span>

<span data-ttu-id="51b3d-181">当您打开支持票证时, 您将使用所提供的下拉列表和文本输入字段来完成表单的 "**问题**" 部分。</span><span class="sxs-lookup"><span data-stu-id="51b3d-181">When you open a support ticket, you will complete the **Problem** section of the form by using provided dropdown lists and text-entry fields.</span></span>
    - <span data-ttu-id="51b3d-182">在 "**标题**文本-输入" 字段中, 简要说明问题。</span><span class="sxs-lookup"><span data-stu-id="51b3d-182">In the **Title** text-entry field, describe your issue briefly.</span></span>  <span data-ttu-id="51b3d-183">在**详细**信息文本输入字段中提供有关问题的其他信息。</span><span class="sxs-lookup"><span data-stu-id="51b3d-183">Provide additional information about your issue in the **Details** text-entry field.</span></span>
    - <span data-ttu-id="51b3d-184">通过选择**首选的 contact 方法**并按照窗体提示输入联系人详细信息来提供您的联系人信息。</span><span class="sxs-lookup"><span data-stu-id="51b3d-184">Provide your contact information by choosing your **preferred contact method** and entering your contact details, as prompted by the form.</span></span>

<span data-ttu-id="51b3d-185">填写表单后, 选择 "**创建**" 以提交你的支持请求。</span><span class="sxs-lookup"><span data-stu-id="51b3d-185">Once you've filled out the form, select **Create** to submit your support request.</span></span> <span data-ttu-id="51b3d-186">提交请求后, Azure 支持团队将与你联系。</span><span class="sxs-lookup"><span data-stu-id="51b3d-186">The Azure support team will contact you after you submit your request.</span></span>

<span data-ttu-id="51b3d-187">然后, 可以通过 "**帮助 + 支持**" 刀片中的 "**所有支持请求**" 查看你的支持请求的状态和详细信息。</span><span class="sxs-lookup"><span data-stu-id="51b3d-187">You can then check the status and details of your support request, through the **All support requests** from the **Help + support** blade.</span></span>

### <a name="directory-and-subscription"></a><span data-ttu-id="51b3d-188">目录和订阅</span><span class="sxs-lookup"><span data-stu-id="51b3d-188">Directory and subscription</span></span>

<span data-ttu-id="51b3d-189">单击 "**书籍和筛选器**" 图标以显示**目录 + 订阅**边栏。</span><span class="sxs-lookup"><span data-stu-id="51b3d-189">Click the **Book and Filter** icon to show the **Directory + subscription** blade.</span></span>

<span data-ttu-id="51b3d-190">Azure 允许您将多个订阅与一个目录相关联。</span><span class="sxs-lookup"><span data-stu-id="51b3d-190">Azure allows you to have more than one subscription associated with one directory.</span></span> <span data-ttu-id="51b3d-191">在**目录 + 订阅**边栏上, 您可以在两个订阅之间更改。</span><span class="sxs-lookup"><span data-stu-id="51b3d-191">On the **Directory + subscription** blade, you can change between subscriptions.</span></span> <span data-ttu-id="51b3d-192">在这里, 您可以更改订阅或更改为另一个目录。</span><span class="sxs-lookup"><span data-stu-id="51b3d-192">Here, you can change your subscription or change to another directory.</span></span>

![目录和订阅边栏的屏幕截图。](../media/3-directory-blade.png)

### <a name="profile-settings"></a><span data-ttu-id="51b3d-194">配置文件设置</span><span class="sxs-lookup"><span data-stu-id="51b3d-194">Profile settings</span></span>

<span data-ttu-id="51b3d-195">如果您在右上角单击您的姓名, 将打开一个菜单, 其中包含几个选项:</span><span class="sxs-lookup"><span data-stu-id="51b3d-195">If you click on your name in the top right-hand corner, a menu opens with a few options:</span></span>

- <span data-ttu-id="51b3d-196">使用其他帐户登录, 或完全注销</span><span class="sxs-lookup"><span data-stu-id="51b3d-196">Sign in with another account, or sign out entirely</span></span>
- <span data-ttu-id="51b3d-197">查看你的帐户配置文件, 你可以在其中更改你的密码</span><span class="sxs-lookup"><span data-stu-id="51b3d-197">View your account profile, where you can change your password</span></span>
- <span data-ttu-id="51b3d-198">检查你的权限</span><span class="sxs-lookup"><span data-stu-id="51b3d-198">Check your permissions</span></span>
- <span data-ttu-id="51b3d-199">查看你的帐单 (单击 "..."按钮右侧)</span><span class="sxs-lookup"><span data-stu-id="51b3d-199">View your bill (click the "..." button on the right-hand side)</span></span>
- <span data-ttu-id="51b3d-200">更新您的联系信息 (单击 "..."按钮右侧)</span><span class="sxs-lookup"><span data-stu-id="51b3d-200">Update your contact information (click the "..." button on the right-hand side)</span></span>

<span data-ttu-id="51b3d-201">如果单击 "..."然后**查看我的帐单**, Azure 将转到 "**成本管理 + 计费-发票**" 页面, 该页面可帮助您分析 Azure 生成成本的位置。</span><span class="sxs-lookup"><span data-stu-id="51b3d-201">If you click "..." and then **View my bill**, Azure takes you to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.</span></span>

<span data-ttu-id="51b3d-202">azure 是一种大型产品, azure 门户用户界面 (UI) 反映了这一点。</span><span class="sxs-lookup"><span data-stu-id="51b3d-202">Azure is a large product, and the Azure portal user interface (UI) reflects this.</span></span> <span data-ttu-id="51b3d-203">滑动刀片方法允许您轻松地在各种管理任务之间来回切换。</span><span class="sxs-lookup"><span data-stu-id="51b3d-203">The sliding blade approach allows you to navigate back and forth through the various administrative tasks with ease.</span></span> <span data-ttu-id="51b3d-204">让我们试一试一下此 UI, 这样你就可以实现一些练习。</span><span class="sxs-lookup"><span data-stu-id="51b3d-204">Let's experiment a bit with this UI so you get some practice.</span></span>

### <a name="azure-advisor"></a><span data-ttu-id="51b3d-205">Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="51b3d-205">Azure Advisor</span></span>
<span data-ttu-id="51b3d-206">最后, azure Advisor 是一个内置于 azure 中的免费服务, 可提供有关高可用性、安全性、性能和成本方面的建议。</span><span class="sxs-lookup"><span data-stu-id="51b3d-206">Finally, the Azure Advisor is a free service built into Azure that provides recommendations on high availability, security, performance, and cost.</span></span> <span data-ttu-id="51b3d-207">Advisor 分析已部署的服务, 并寻找在这四个领域改进环境的方法。</span><span class="sxs-lookup"><span data-stu-id="51b3d-207">Advisor analyzes your deployed services and looks for ways to improve your environment across those four areas.</span></span> <span data-ttu-id="51b3d-208">您可以查看门户中的建议或以 PDF 或 CSV 格式下载它们。</span><span class="sxs-lookup"><span data-stu-id="51b3d-208">You can view recommendations in the portal or download them in PDF or CSV format.</span></span>

<span data-ttu-id="51b3d-209">使用 Azure Advisor, 可以执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="51b3d-209">With Azure Advisor, you can:</span></span>
- <span data-ttu-id="51b3d-210">获取主动、可操作和个性化的最佳实践建议。</span><span class="sxs-lookup"><span data-stu-id="51b3d-210">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
- <span data-ttu-id="51b3d-211">在发现可降低您的总体 Azure 成本的机会时, 提高资源的性能、安全性和高可用性。</span><span class="sxs-lookup"><span data-stu-id="51b3d-211">Improve the performance, security, and high availability of your resources as you identify opportunities to reduce your overall Azure costs.</span></span>
- <span data-ttu-id="51b3d-212">以内嵌建议的操作获取建议。</span><span class="sxs-lookup"><span data-stu-id="51b3d-212">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="51b3d-213">您可以从导航菜单中选择 " **Advisor** ", 或在 "**所有服务**" 菜单中搜索它, 以访问 Azure Advisor。</span><span class="sxs-lookup"><span data-stu-id="51b3d-213">You can access Azure Advisor by selecting **Advisor** from the navigation menu, or search for it in the **All Services** menu.</span></span>

![azure 门户中显示的 azure Advisor 仪表板, 显示了高可用性、安全性、性能和成本的建议](../media/3-advisordashboard.png)

<span data-ttu-id="51b3d-215">让我们尝试一下其中一些功能!</span><span class="sxs-lookup"><span data-stu-id="51b3d-215">Let's try some of these features out!</span></span>