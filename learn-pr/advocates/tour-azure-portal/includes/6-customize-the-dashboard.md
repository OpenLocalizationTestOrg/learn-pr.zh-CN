<span data-ttu-id="19177-101">我们来看看如何使用 Azure 门户创建和修改仪表板, 以及直接编辑基础 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="19177-101">Let's look at how to create and modify dashboards using the Azure Portal, and by editing the underlying JSON file directly.</span></span> <span data-ttu-id="19177-102">在此单元中, 你将了解如何解决问题, 在下一个单元中, 你将试用你学到的东西。</span><span class="sxs-lookup"><span data-stu-id="19177-102">In this unit, you'll learn your way around, and in the next unit you will try out the things you've learned.</span></span>

## <a name="what-is-a-dashboard"></a><span data-ttu-id="19177-103">什么是仪表板？</span><span class="sxs-lookup"><span data-stu-id="19177-103">What is a dashboard?</span></span>

<span data-ttu-id="19177-104">_仪表板_是 Azure 门户中显示的 UI 磁贴的可自定义集合。</span><span class="sxs-lookup"><span data-stu-id="19177-104">A _dashboard_ is a customizable collection of UI tiles displayed in the Azure portal.</span></span> <span data-ttu-id="19177-105">您可以添加、删除和放置图块来创建所需的确切视图, 然后将该视图另存为仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-105">You add, remove, and position tiles to create the exact view you want, and then save that view as a dashboard.</span></span> <span data-ttu-id="19177-106">支持多个仪表板, 并且可以根据需要在它们之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="19177-106">Multiple dashboards are supported, and you can switch between them as needed.</span></span> <span data-ttu-id="19177-107">您甚至可以与其他团队成员共享仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-107">You can even share your dashboards with other team members.</span></span>

<span data-ttu-id="19177-108">仪表板为你提供了相当大的灵活性, 与你管理 Azure 的方式有关。</span><span class="sxs-lookup"><span data-stu-id="19177-108">Dashboards give you considerable flexibility regarding how you manage Azure.</span></span> <span data-ttu-id="19177-109">例如, 您可以为组织内的特定角色创建仪表板, 然后使用基于角色的访问控制 (RBAC) 来控制谁可以访问该仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-109">For example, you can create dashboards for specific roles within the organization, and then use role-based access control (RBAC) to control who can access that dashboard.</span></span> <span data-ttu-id="19177-110">因此, 数据库管理员将拥有包含 SQL database service 视图的仪表板, 而您的 azure Active Directory 管理员将拥有 Azure AD 中的用户和组的视图。</span><span class="sxs-lookup"><span data-stu-id="19177-110">Hence, your database administrator would have a dashboard that contains views of the SQL database service, whereas your Azure Active Directory administrator would have views of the users and groups within Azure AD.</span></span> <span data-ttu-id="19177-111">您甚至可以在门户中的生产环境和开发环境之间自定义门户-为所管理的每个环境创建特定的仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-111">You can even customize the portal between your production and development environments within the portal - creating a specific dashboard for each environment you are managing.</span></span>

<span data-ttu-id="19177-112">仪表板存储为 JavaScript 对象表示法 (JSON) 文件。</span><span class="sxs-lookup"><span data-stu-id="19177-112">Dashboards are stored as JavaScript Object Notation (JSON) files.</span></span> <span data-ttu-id="19177-113">这意味着可以将它们上载并下载到其他计算机, 或与 Azure 目录的成员共享。</span><span class="sxs-lookup"><span data-stu-id="19177-113">This means they can be uploaded and downloaded to other computers, or shared with members of the Azure directory.</span></span> <span data-ttu-id="19177-114">Azure 将仪表板存储在资源组中, 就像可以在门户中管理的虚拟机或存储帐户一样。</span><span class="sxs-lookup"><span data-stu-id="19177-114">Azure stores dashboards within resource groups, just like virtual machines or storage accounts that you can manage within the portal.</span></span>

> [!TIP]
> <span data-ttu-id="19177-115">由于仪表板是 JSON 文件, 因此也可以[通过编程方式自定义它们](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically), 从而让它们成为引人注目的管理工具。</span><span class="sxs-lookup"><span data-stu-id="19177-115">Because dashboards are JSON files, you can also [customize them programmatically](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-create-programmatically), making them compelling administrative tools.</span></span> <span data-ttu-id="19177-116">此外, 某些图块类型可以是基于查询的, 因此它们会在源数据发生更改时自动更新。</span><span class="sxs-lookup"><span data-stu-id="19177-116">Also, some tile types can be query-based, so they update automatically when the source data changes.</span></span>

## <a name="explore-the-default-dashboard"></a><span data-ttu-id="19177-117">浏览默认仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-117">Explore the default dashboard</span></span>

<span data-ttu-id="19177-118">默认仪表板名为 "仪表板"。</span><span class="sxs-lookup"><span data-stu-id="19177-118">The default dashboard is named "Dashboard".</span></span> <span data-ttu-id="19177-119">当您首次登录门户时, 将显示包含四个磁贴的此仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-119">When you log into the portal for the first time, you are presented with this dashboard containing four tiles.</span></span>

![显示具有不同部件编号和突出显示的默认仪表板的屏幕截图。](../media/6-dashboard-default-webparts.png)

<span data-ttu-id="19177-121">这些默认 web 部件是</span><span class="sxs-lookup"><span data-stu-id="19177-121">These default web parts are</span></span>

1. <span data-ttu-id="19177-122">仪表板控件</span><span class="sxs-lookup"><span data-stu-id="19177-122">Dashboard controls</span></span>

1. <span data-ttu-id="19177-123">所有资源平铺</span><span class="sxs-lookup"><span data-stu-id="19177-123">All resources tile</span></span>

1. <span data-ttu-id="19177-124">快速入门 + 教程磁贴</span><span class="sxs-lookup"><span data-stu-id="19177-124">Quickstarts + tutorials tile</span></span>

1. <span data-ttu-id="19177-125">服务运行状况图块</span><span class="sxs-lookup"><span data-stu-id="19177-125">Service Health tile</span></span>

1. <span data-ttu-id="19177-126">Marketplace 磁贴</span><span class="sxs-lookup"><span data-stu-id="19177-126">Marketplace tile</span></span>

## <a name="creating-and-managing-dashboards"></a><span data-ttu-id="19177-127">创建和管理仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-127">Creating and managing dashboards</span></span>

<span data-ttu-id="19177-128">仪表板顶部是使您能够创建、上载、下载、编辑和共享仪表板的控件。</span><span class="sxs-lookup"><span data-stu-id="19177-128">Along the top of the dashboard are the controls that enable you to create, upload, download, edit, and share a dashboard.</span></span> <span data-ttu-id="19177-129">您还可以将仪表板切换到全屏, 进行克隆或将其删除。</span><span class="sxs-lookup"><span data-stu-id="19177-129">You can also switch a dashboard to full screen, clone it, or delete it.</span></span>

![显示自定义仪表板控件的屏幕截图](../media/6-customise-dashboard-controls.png)

## <a name="select-dashboard"></a><span data-ttu-id="19177-131">选择仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-131">Select dashboard</span></span>

<span data-ttu-id="19177-132">工具栏的最左侧是 "**选择仪表板**" 下拉控件。</span><span class="sxs-lookup"><span data-stu-id="19177-132">To the far left of the toolbar is the **Select Dashboard** drop-down control.</span></span> <span data-ttu-id="19177-133">通过单击此控件, 可以从已为您的帐户定义的仪表板中进行选择。</span><span class="sxs-lookup"><span data-stu-id="19177-133">Clicking this control enables you to select from dashboards that you have already defined for your account.</span></span> <span data-ttu-id="19177-134">此控件使您可以轻松地为不同的目的定义多个仪表板, 然后从一个仪表板切换到另一个, 具体取决于您在何时尝试执行的操作。</span><span class="sxs-lookup"><span data-stu-id="19177-134">This control makes it simple for you to define multiple dashboards for different purposes and then switch from one to another and back again, depending on what you are trying to do at the time.</span></span>

<span data-ttu-id="19177-135">请注意, 您创建的任何仪表板最初都是专用的;也就是说, 只有你可以看到它们。</span><span class="sxs-lookup"><span data-stu-id="19177-135">Note that any dashboards that you create will initially be private; that is, only you can see them.</span></span> <span data-ttu-id="19177-136">若要使仪表板在整个企业中可用, 您需要将其共享。</span><span class="sxs-lookup"><span data-stu-id="19177-136">To make a dashboard available across your enterprise, you need to share it.</span></span> <span data-ttu-id="19177-137">我们将很快查看该选项。</span><span class="sxs-lookup"><span data-stu-id="19177-137">We'll look at that option shortly.</span></span>

## <a name="create-a-new-dashboard"></a><span data-ttu-id="19177-138">创建新仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-138">Create a new dashboard</span></span>

<span data-ttu-id="19177-139">若要创建新仪表板, 请单击 "**新建仪表板**"。</span><span class="sxs-lookup"><span data-stu-id="19177-139">To create a new dashboard, click **New dashboard**.</span></span> <span data-ttu-id="19177-140">显示仪表板工作区, 无平铺显示。</span><span class="sxs-lookup"><span data-stu-id="19177-140">The dashboard workspace appears, with no tiles present.</span></span> <span data-ttu-id="19177-141">然后, 您可以添加、删除和调整磁贴 (但您喜欢)。</span><span class="sxs-lookup"><span data-stu-id="19177-141">You can then add, remove and adjust tiles however you like.</span></span> <span data-ttu-id="19177-142">完成自定义仪表板后, 单击 "**完成自定义**" 以保存并切换到该仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-142">When you are finished customizing the dashboard, click **Done customizing** to save and switch to that dashboard.</span></span>

## <a name="upload-and-download"></a><span data-ttu-id="19177-143">上载和下载</span><span class="sxs-lookup"><span data-stu-id="19177-143">Upload and Download</span></span>

<span data-ttu-id="19177-144">使用 "**上载**" 和 "**下载**" 按钮, 可以将当前仪表板下载为 JSON 文件, 对其进行自定义, 然后将其分发并上载, 或者让其他人将该文件上传回 Azure 门户, 从而将其替换为当前图表.</span><span class="sxs-lookup"><span data-stu-id="19177-144">The **Upload** and **Download** buttons enable you to download your current dashboard as a JSON file, customize it, and then distribute it and upload it or have someone else upload that file back to the Azure portal, thereby replacing their current dashboard.</span></span>

<span data-ttu-id="19177-145">如果单击 "**下载**", 则当前仪表板将 JSON 代码下载为可在本地编辑的文件。</span><span class="sxs-lookup"><span data-stu-id="19177-145">If you click **Download**, the current dashboard downloads the JSON code as a file you can edit locally.</span></span> <span data-ttu-id="19177-146">然后, 可以通过单击 "**上传**" 按钮将其上传回 Azure。</span><span class="sxs-lookup"><span data-stu-id="19177-146">You can then upload it back to Azure by clicking the **Upload** button.</span></span> <span data-ttu-id="19177-147">下面将对此进行进一步讨论。</span><span class="sxs-lookup"><span data-stu-id="19177-147">This is discussed further below.</span></span>

## <a name="edit-a-dashboard-using-the-portal"></a><span data-ttu-id="19177-148">使用门户编辑仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-148">Edit a dashboard using the portal</span></span>

<span data-ttu-id="19177-149">虽然您可以通过下载 JSON 文件、更改文件中的值以及将文件上传回 Azure 来编辑仪表板, 但这种方法在设计用户界面方面并不直观。</span><span class="sxs-lookup"><span data-stu-id="19177-149">Although you can edit a dashboard by downloading the JSON file, changing values in the file, and uploading the file back to Azure, that approach isn't intuitive for designing a user interface.</span></span> <span data-ttu-id="19177-150">若要使用 GUI 配置当前仪表板, 可以通过以下几种方式进入编辑模式:</span><span class="sxs-lookup"><span data-stu-id="19177-150">To use the GUI to configure your current dashboard you can enter edit mode in several ways:</span></span>

1. <span data-ttu-id="19177-151">单击 "**编辑**" (铅笔图标) 按钮。</span><span class="sxs-lookup"><span data-stu-id="19177-151">Click the **Edit** (pencil icon) button.</span></span>
1. <span data-ttu-id="19177-152">右键单击仪表板背景区域, 然后选择 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="19177-152">Right-click on the dashboard background area and select **Edit**.</span></span>
1. <span data-ttu-id="19177-153">右键单击磁贴, 菜单将显示 "编辑" 选项。</span><span class="sxs-lookup"><span data-stu-id="19177-153">Right-click on a tile and a menu will appear with edit options.</span></span>
1. <span data-ttu-id="19177-154">将鼠标悬停在仪表板上的图`...`块上-一个菜单将显示在顶部/右侧的 "编辑" 选项中。</span><span class="sxs-lookup"><span data-stu-id="19177-154">Hover over a tile on the dashboard - a `...` menu will appear on the top/right corner with edit options.</span></span>

<span data-ttu-id="19177-155">仪表板切换到编辑模式。</span><span class="sxs-lookup"><span data-stu-id="19177-155">The dashboard switches to edit mode.</span></span>

![在编辑模式下显示仪表板的屏幕截图](../media/6-edit-dashboard.png)

<span data-ttu-id="19177-157">左侧显示的是平铺库, 有几个可能的图块。</span><span class="sxs-lookup"><span data-stu-id="19177-157">On the left-hand side appears the Tile Gallery, with several possible tiles.</span></span> <span data-ttu-id="19177-158">您可以按类别和资源类型筛选磁贴库。</span><span class="sxs-lookup"><span data-stu-id="19177-158">You can filter the Tile Gallery by category and resource type.</span></span>

<span data-ttu-id="19177-159">添加磁贴就像从左侧列表中选择图块, 然后将其拖动到工作区一样简单。</span><span class="sxs-lookup"><span data-stu-id="19177-159">Adding tiles is as easy as selecting the tile from the list on the left and then dragging it to the work area.</span></span> <span data-ttu-id="19177-160">然后, 您可以移动每个图块、调整其大小或更改它显示的数据。</span><span class="sxs-lookup"><span data-stu-id="19177-160">You can then move each tile about, resize it, or change the data that it displays.</span></span>

> [!TIP]
> <span data-ttu-id="19177-161">很多人都不知道, 您可以在子刀片上获取元素并将其放在您的仪表板上。</span><span class="sxs-lookup"><span data-stu-id="19177-161">One cool feature a lot of people are unaware of is that you can take elements on child blades and put them on your dashboard.</span></span> <span data-ttu-id="19177-162">只需将鼠标悬停在项目上, `...`查找 "磁贴编辑" 菜单即可, 这将具有一个 "固定到仪表板" 选项, 使您可以快速从服务中获取磁贴, 并将其放在仪表板上。</span><span class="sxs-lookup"><span data-stu-id="19177-162">Just hover over the item and look for the `...` tile edit menu - this will have a "Pin to Dashboard" option which lets you quickly grab a tile from a service and put it onto the dashboard.</span></span>

<span data-ttu-id="19177-163">编辑模式下的工作区分成方形。</span><span class="sxs-lookup"><span data-stu-id="19177-163">The work area in edit mode is divided into squares.</span></span> <span data-ttu-id="19177-164">每个图块必须至少占用一个正方形, 图块将捕捉到最接近的最大图块分隔符集。</span><span class="sxs-lookup"><span data-stu-id="19177-164">Each tile must occupy at least one square, and tiles will snap to the nearest largest set of tile dividers.</span></span> <span data-ttu-id="19177-165">任何重叠的图块将移开。</span><span class="sxs-lookup"><span data-stu-id="19177-165">Any overlapping tiles are moved out of the way.</span></span> <span data-ttu-id="19177-166">当您缩小图块时, 周围的图块将随之向后移动。</span><span class="sxs-lookup"><span data-stu-id="19177-166">When you make a tile smaller, the surrounding tiles will move back up against it.</span></span>

#### <a name="change-tile-sizes"></a><span data-ttu-id="19177-167">更改磁贴大小</span><span class="sxs-lookup"><span data-stu-id="19177-167">Change tile sizes</span></span>

<span data-ttu-id="19177-168">有些图块具有设置的大小, 您只能以编程方式编辑它们的大小。</span><span class="sxs-lookup"><span data-stu-id="19177-168">Some tiles have a set size, and you can edit their size only programmatically.</span></span> <span data-ttu-id="19177-169">不过, 您可以通过拖动角指示器来编辑具有灰色右下角的图块。</span><span class="sxs-lookup"><span data-stu-id="19177-169">However, you can edit tiles with a gray bottom right-hand corner by dragging the corner indicator.</span></span>

![突出显示带角指示器的图块的屏幕截图。](../media/6-resizable-tile.png)

<span data-ttu-id="19177-171">或者, 右键单击上下文菜单并指定所需的大小。</span><span class="sxs-lookup"><span data-stu-id="19177-171">Alternatively, right-click the context menu and specify the size you want.</span></span>

![带有显示不同大小调整选项的上下文菜单的磁贴的屏幕截图。](../media/6-tile-size.png)

<span data-ttu-id="19177-173">若要创建仪表板, 请将图块从图块库拖动到工作区, 然后重新排列它们。</span><span class="sxs-lookup"><span data-stu-id="19177-173">To create your dashboard, pull tiles from the Tile Gallery onto the workspace and then rearrange them.</span></span>

#### <a name="change-tile-settings"></a><span data-ttu-id="19177-174">更改磁贴设置</span><span class="sxs-lookup"><span data-stu-id="19177-174">Change tile settings</span></span>

<span data-ttu-id="19177-175">有些图块具有可编辑的设置。</span><span class="sxs-lookup"><span data-stu-id="19177-175">Some tiles have editable settings.</span></span> <span data-ttu-id="19177-176">例如, 在时钟图块中, 将其拖动到工作区时, 将打开 "**编辑时钟**" 图块。</span><span class="sxs-lookup"><span data-stu-id="19177-176">For example, with the clock tile, when you drag it onto the workspace, it opens the **Edit clock** tile.</span></span> <span data-ttu-id="19177-177">然后, 您可以设置它显示的时区, 还可以设置是以12小时还是24小时格式显示。</span><span class="sxs-lookup"><span data-stu-id="19177-177">You can then set the time zone, which it displays, and also set whether it displays in 12- or 24-hour format.</span></span>

![显示时钟磁贴的编辑时钟设置的屏幕截图。](../media/6-edit-clock.png)

<span data-ttu-id="19177-179">对于多国或 transcontinental 公司, 可以添加时钟, 每个都位于不同的时区。</span><span class="sxs-lookup"><span data-stu-id="19177-179">For multi-national or transcontinental companies, you can add clocks, each in a different time zone.</span></span>

#### <a name="accepting-your-edits"></a><span data-ttu-id="19177-180">接受编辑</span><span class="sxs-lookup"><span data-stu-id="19177-180">Accepting your edits</span></span>

<span data-ttu-id="19177-181">根据需要排列磁贴后, 请单击 "**完成自定义**" 或右键单击, 然后单击 "**完成自定义**"。</span><span class="sxs-lookup"><span data-stu-id="19177-181">When you have arranged the tiles as you want them, either click **Done customizing**, or right-click and then click **Done customizing**.</span></span>

## <a name="edit-a-dashboard-by-changing-the-json-file"></a><span data-ttu-id="19177-182">通过更改 JSON 文件来编辑仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-182">Edit a dashboard by changing the JSON file</span></span>

<span data-ttu-id="19177-183">您还可以通过更改 JSON 文件来编辑仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-183">You can also edit a dashboard by changing the JSON file.</span></span> <span data-ttu-id="19177-184">此方法提供了更多用于更改设置的选项, 但在将文件上传回 Azure 之前无法看到这些更改。</span><span class="sxs-lookup"><span data-stu-id="19177-184">This approach provides more options for changing settings, but you cannot see the changes until you upload the file back into Azure.</span></span> <span data-ttu-id="19177-185">最简单的起点是下载前面所述的仪表板 JSON, 并编辑该文件。</span><span class="sxs-lookup"><span data-stu-id="19177-185">The easiest starting point is to download the dashboard JSON as previously described and edit that file.</span></span>

![下载的仪表板 JSON 文件的屏幕截图。](../media/6-json-code.png)

<span data-ttu-id="19177-187">例如, 在上面显示的 JSON 中, 若要更改磁贴的大小, 请编辑**colSpan**和**行宽**变量, 然后保存该文件并将其上传回 Azure。</span><span class="sxs-lookup"><span data-stu-id="19177-187">As an example, in the JSON shown above, to change the size of the tile you would edit the **colSpan** and **rowSpan** variables, then save the file and upload it back to Azure.</span></span>

> [!Tip]
> <span data-ttu-id="19177-188">您还可以将仪表板 JSON 文件分发给其他用户。</span><span class="sxs-lookup"><span data-stu-id="19177-188">You can also distribute the dashboard JSON file to other users.</span></span>

## <a name="reset-a-dashboard"></a><span data-ttu-id="19177-189">重置仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-189">Reset a dashboard</span></span>

<span data-ttu-id="19177-190">您可以将任何仪表板重置为默认样式。</span><span class="sxs-lookup"><span data-stu-id="19177-190">You can reset any dashboard to the default style.</span></span> <span data-ttu-id="19177-191">在编辑模式下, 右键单击仪表板背景, 然后选择 "**重置为默认状态**"。</span><span class="sxs-lookup"><span data-stu-id="19177-191">In edit mode, right-click the dashboard background and select **Reset to default state**.</span></span> <span data-ttu-id="19177-192">将有一个对话框要求您确认是否要重置该仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-192">A dialog box will ask you to confirm that you want to reset that dashboard.</span></span>

## <a name="share-or-unshare-a-dashboard"></a><span data-ttu-id="19177-193">共享或取消共享仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-193">Share or unshare a dashboard</span></span>

<span data-ttu-id="19177-194">当您定义新仪表板时, 它是私有的, 并且仅对您的帐户可见。</span><span class="sxs-lookup"><span data-stu-id="19177-194">When you define a new dashboard, it is private and visible only to your account.</span></span> <span data-ttu-id="19177-195">若要使其他人能够看到它, 您需要共享一个仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-195">To make it visible to others, you need to share a dashboard.</span></span> <span data-ttu-id="19177-196">但是, 与任何其他 Azure 资源一样, 您需要指定要在其中存储共享仪表板的新资源组 (或使用现有资源组)。</span><span class="sxs-lookup"><span data-stu-id="19177-196">However, as with any other Azure resource, you need to specify a new resource group (or use an existing resource group) in which to store shared dashboards.</span></span> <span data-ttu-id="19177-197">如果没有现有的资源组, Azure 将在指定的任何位置创建*仪表板*资源组。</span><span class="sxs-lookup"><span data-stu-id="19177-197">If you do not have an existing resource group, Azure will create a *dashboards* resource group in whichever location you specify.</span></span> <span data-ttu-id="19177-198">如果您有现有的资源组, 则可以指定该资源组来存储仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-198">If you have existing resource groups, you can specify that resource group to store the dashboards.</span></span>

![共享仪表板之前, 共享和访问控制刀片的屏幕截图。](../media/6-share-dashboards-default.png)

<span data-ttu-id="19177-200">共享模板后, 您将看到第二个共享和**访问控制**刀片。</span><span class="sxs-lookup"><span data-stu-id="19177-200">When you have shared the template, you will see a second **Sharing + access control** blade.</span></span>

![共享仪表板后, 共享和访问控制刀片的屏幕截图。](../media/6-share-dashboards-access-control.png)

<span data-ttu-id="19177-202">然后, 您可以单击 "**管理用户**" 来指定有权访问该仪表板的用户。</span><span class="sxs-lookup"><span data-stu-id="19177-202">You can then click **Manage users** to specify the users who have access to that dashboard.</span></span>

### <a name="switching-to-a-shared-dashboard"></a><span data-ttu-id="19177-203">切换到共享仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-203">Switching to a shared dashboard</span></span>

<span data-ttu-id="19177-204">若要切换到共享仪表板, 请单击仪表板列表, 然后单击 "**浏览所有仪表板**"。</span><span class="sxs-lookup"><span data-stu-id="19177-204">To switch to a shared dashboard, you click on the list of dashboards, and then click **Browse all dashboards**.</span></span>

![显示 "浏览所有仪表板" 链接突出显示的共享 dashobards 列表的屏幕截图。](../media/6-browse-dashboards.png)

<span data-ttu-id="19177-206">现在, 您将看到**所有仪表板**边栏, 并显示任何共享仪表板的名称。</span><span class="sxs-lookup"><span data-stu-id="19177-206">You will now see the **All dashboards** blade, with the names of any shared dashboards displayed.</span></span> <span data-ttu-id="19177-207">只需单击仪表板即可将其应用到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="19177-207">Just click on a dashboard to apply it to the Azure portal.</span></span>

![显示所有仪表板边栏共享仪表板的屏幕截图。](../media/6-select-shared-dashboard.png)

## <a name="display-a-dashboard-as-a-full-screen"></a><span data-ttu-id="19177-209">以全屏方式显示仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-209">Display a dashboard as a full screen</span></span>

<span data-ttu-id="19177-210">如果您想要最大的仪表板房地产, 请单击 "**全屏**" 按钮以显示不包含任何浏览器菜单的当前仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-210">If you want the largest dashboard real estate, click the **Full screen** button to display your current dashboard without any browser menus.</span></span> <span data-ttu-id="19177-211">如果屏幕显示边界之外的任何图块, 则屏幕的右侧和底部将显示滑块条。</span><span class="sxs-lookup"><span data-stu-id="19177-211">If you have any tiles outside the boundaries of your screen display, slider bars will appear at the right and bottom of your screen.</span></span>

<span data-ttu-id="19177-212">在全屏模式下工作后, 按 ESC 键或单击屏幕顶部的仪表板名称旁边的 "**退出全屏**"。</span><span class="sxs-lookup"><span data-stu-id="19177-212">When you have finished working in full-screen mode, press the ESC key or click **Exit Full Screen** next to the Dashboard name at the top of the screen.</span></span>

## <a name="clone-a-dashboard"></a><span data-ttu-id="19177-213">克隆仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-213">Clone a dashboard</span></span>

<span data-ttu-id="19177-214">克隆仪表板将创建一个名为 "复制\<仪表板 name>" 的即时副本, 并切换为该副本作为当前仪表板。</span><span class="sxs-lookup"><span data-stu-id="19177-214">Cloning a dashboard creates an instant copy called "Clone of \<dashboard name>" and switches to that copy as the current dashboard.</span></span> <span data-ttu-id="19177-215">克隆也是在共享仪表板之前创建仪表板的简单方法。</span><span class="sxs-lookup"><span data-stu-id="19177-215">Cloning is also an easy way to create dashboards before sharing them.</span></span> <span data-ttu-id="19177-216">例如, 如果您的仪表板几乎是您想要的, 请先克隆它, 再进行所需的更改, 然后再进行共享。</span><span class="sxs-lookup"><span data-stu-id="19177-216">For example, if you have a dashboard that is almost as you want it, clone it, make the changes that you need, and then share it.</span></span>

## <a name="delete-a-dashboard"></a><span data-ttu-id="19177-217">删除仪表板</span><span class="sxs-lookup"><span data-stu-id="19177-217">Delete a dashboard</span></span>

<span data-ttu-id="19177-218">删除仪表板会将其从可用仪表板列表中删除。</span><span class="sxs-lookup"><span data-stu-id="19177-218">Deleting a dashboard removes it from your list of available dashboards.</span></span> <span data-ttu-id="19177-219">系统将提示您确认是否要删除仪表板, 但没有用于恢复已删除的仪表板的功能。</span><span class="sxs-lookup"><span data-stu-id="19177-219">You are prompted to confirm that you want to delete the dashboard, but there is no facility to recover a dashboard that has been deleted.</span></span>

<span data-ttu-id="19177-220">让我们通过创建新仪表板来试用其中一些选项。</span><span class="sxs-lookup"><span data-stu-id="19177-220">Let's try out some of these options by creating a new dashboard.</span></span>
