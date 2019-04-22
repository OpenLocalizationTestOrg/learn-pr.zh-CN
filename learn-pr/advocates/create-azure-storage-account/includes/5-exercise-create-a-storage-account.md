<span data-ttu-id="2df02-101">在此单元中, 你将使用 Azure 门户创建适用于假想南加利福尼亚冲浪报表 web 应用的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2df02-101">In this unit, you will use the Azure portal to create a storage account that is appropriate for a fictitious southern California surf report web app.</span></span>

<span data-ttu-id="2df02-102">通过冲浪报告网站, 用户可以上载本地浮水条件的照片和视频。</span><span class="sxs-lookup"><span data-stu-id="2df02-102">The surf report site lets users upload photos and videos of local beach conditions.</span></span> <span data-ttu-id="2df02-103">查看者将使用内容来帮助他们选择具有最佳冲浪条件的海滩。</span><span class="sxs-lookup"><span data-stu-id="2df02-103">Viewers will use the content to help them choose the beach with the best surfing conditions.</span></span> <span data-ttu-id="2df02-104">您的设计和功能目标列表为:</span><span class="sxs-lookup"><span data-stu-id="2df02-104">Your list of design and feature goals is:</span></span>

- <span data-ttu-id="2df02-105">视频内容必须快速加载。</span><span class="sxs-lookup"><span data-stu-id="2df02-105">Video content must load quickly.</span></span>
- <span data-ttu-id="2df02-106">网站必须处理上传卷中的意外峰值。</span><span class="sxs-lookup"><span data-stu-id="2df02-106">The site must handle unexpected spikes in upload volume.</span></span>
- <span data-ttu-id="2df02-107">在冲浪条件更改时必须删除过期内容, 以便网站始终显示当前条件。</span><span class="sxs-lookup"><span data-stu-id="2df02-107">Outdated content must be removed as surf conditions change so the site always shows current conditions.</span></span>

<span data-ttu-id="2df02-108">为了满足这些要求, 您决定在 azure 队列中缓冲上载的内容以进行处理, 然后将其传输到适用于永久存储的 azure Blob。</span><span class="sxs-lookup"><span data-stu-id="2df02-108">To fulfill these requirements, you decide to buffer uploaded content in an Azure Queue for processing and then transfer it to an Azure Blob for persistent storage.</span></span> <span data-ttu-id="2df02-109">您需要一个存储帐户, 该帐户可以同时保存队列和 blob, 同时提供低延迟的内容访问。</span><span class="sxs-lookup"><span data-stu-id="2df02-109">You need a storage account that can hold both queues and blobs while delivering low-latency access to your content.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="use-the-azure-portal-to-create-a-storage-account"></a><span data-ttu-id="2df02-110">使用 Azure 门户创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="2df02-110">Use the Azure portal to create a storage account</span></span>

1. <span data-ttu-id="2df02-111">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="2df02-111">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="2df02-112">在 Azure 门户的左上角, 选择 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="2df02-112">In the top left of the Azure Portal, select **Create a resource**.</span></span>

1. <span data-ttu-id="2df02-113">在出现的选择面板中, 选择 "**存储**"。</span><span class="sxs-lookup"><span data-stu-id="2df02-113">In the selection panel that appears, select **Storage**.</span></span>

1. <span data-ttu-id="2df02-114">在该窗格的右侧, 选择 "**存储帐户-blob、文件、表、队列**"。</span><span class="sxs-lookup"><span data-stu-id="2df02-114">On the right side of that pane, select **Storage account - blob, file, table, queue**.</span></span>

    ![显示 "创建具有存储类别和存储帐户的资源边栏" 选项的 Azure 门户屏幕截图。](../media/5-portal-storage-select.png)

### <a name="configure-the-basic-options"></a><span data-ttu-id="2df02-116">配置基本选项</span><span class="sxs-lookup"><span data-stu-id="2df02-116">Configure the basic options</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

<span data-ttu-id="2df02-117">在 "**项目详细信息**" 下:</span><span class="sxs-lookup"><span data-stu-id="2df02-117">Under **PROJECT DETAILS**:</span></span>

1. <span data-ttu-id="2df02-118">选择相应的**订阅**。</span><span class="sxs-lookup"><span data-stu-id="2df02-118">Select the appropriate **Subscription**.</span></span>

1. <span data-ttu-id="2df02-119">从下拉列表中选择现有的资源组 ("**<rgn>[沙盒资源组名称]</rgn>**")。</span><span class="sxs-lookup"><span data-stu-id="2df02-119">Select the existing Resource Group ("**<rgn>[sandbox resource group name]</rgn>**") from the drop-down list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2df02-120">此免费资源组已由 Microsoft 作为学习体验的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="2df02-120">This free Resource Group has been provided by Microsoft as part of the learning experience.</span></span> <span data-ttu-id="2df02-121">为实际应用程序创建帐户时, 您需要在订阅中创建一个新的资源组, 以保存该应用程序的所有资源。</span><span class="sxs-lookup"><span data-stu-id="2df02-121">When you create an account for a real application, you will want to create a new Resource Group in your subscription to hold all the resources for the app.</span></span>

<span data-ttu-id="2df02-122">在 "**实例详细信息**" 下:</span><span class="sxs-lookup"><span data-stu-id="2df02-122">Under **INSTANCE DETAILS**:</span></span>

1. <span data-ttu-id="2df02-123">将**部署模型**保留为 "_资源管理器_"。</span><span class="sxs-lookup"><span data-stu-id="2df02-123">Leave the **Deployment model** as _Resource manager_.</span></span> <span data-ttu-id="2df02-124">这是 Azure 中所有资源部署的首选模型, 允许您将应用程序的所有相关资源组合到一个_资源组_中, 以便于管理。</span><span class="sxs-lookup"><span data-stu-id="2df02-124">This is the preferred model for all resource deployments in Azure and allows you to group all the related resources for your app into a _resource group_ for easier management.</span></span>

1. <span data-ttu-id="2df02-125">输入**存储帐户名称**。</span><span class="sxs-lookup"><span data-stu-id="2df02-125">Enter a **Storage account name**.</span></span> <span data-ttu-id="2df02-126">该名称将用于生成用于访问帐户中的数据的公共 URL。</span><span class="sxs-lookup"><span data-stu-id="2df02-126">The name will be used to generate the public URL used to access the data in the account.</span></span> <span data-ttu-id="2df02-127">该名称在 Azure 中的所有现有存储帐户名称中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2df02-127">The name must be unique across all existing storage account names in Azure.</span></span> <span data-ttu-id="2df02-128">名称的长度必须为3到24个字符, 并且只能包含小写字母和数字。</span><span class="sxs-lookup"><span data-stu-id="2df02-128">Names must be 3 to 24 characters long and can contain only lowercase letters and numbers.</span></span>

1. <span data-ttu-id="2df02-129">从上面的列表中选择你附近的**位置**。</span><span class="sxs-lookup"><span data-stu-id="2df02-129">Select a **Location** near to you from the list above.</span></span>

1. <span data-ttu-id="2df02-130">选择 "**性能**" 选项的_标准_。</span><span class="sxs-lookup"><span data-stu-id="2df02-130">Select _Standard_ for the **Performance** option.</span></span> <span data-ttu-id="2df02-131">这决定了用于保存存储帐户中的数据的磁盘存储的类型。</span><span class="sxs-lookup"><span data-stu-id="2df02-131">This decides the type of disk storage used to hold the data in the Storage account.</span></span> <span data-ttu-id="2df02-132">Standard 使用传统硬盘, 而 Premium 使用固态驱动器 (SSD) 以加快访问速度。</span><span class="sxs-lookup"><span data-stu-id="2df02-132">Standard uses traditional hard disks, and Premium uses solid-state drives (SSD) for faster access.</span></span> <span data-ttu-id="2df02-133">但请记住, Premium 仅支持_页面 blob_。</span><span class="sxs-lookup"><span data-stu-id="2df02-133">However, remember that Premium only supports _page blobs_.</span></span> <span data-ttu-id="2df02-134">你将需要视频的_块 blob_和缓冲的队列-这两个队列仅与_标准_选项一起使用。</span><span class="sxs-lookup"><span data-stu-id="2df02-134">You will need _block blobs_ for your videos, and a queue for buffering - both of which are only available with the _Standard_ option.</span></span>

1. <span data-ttu-id="2df02-135">为**帐户类型**选择 " _StorageV2" (常规用途 v2)_ 。</span><span class="sxs-lookup"><span data-stu-id="2df02-135">Select _StorageV2 (general purpose v2)_ for the **Account kind**.</span></span> <span data-ttu-id="2df02-136">这提供了对最新功能和定价的访问权限。</span><span class="sxs-lookup"><span data-stu-id="2df02-136">This provides access to the latest features and pricing.</span></span> <span data-ttu-id="2df02-137">尤其是, Blob 存储帐户具有可用于此帐户类型的更多选项。</span><span class="sxs-lookup"><span data-stu-id="2df02-137">In particular, Blob storage accounts have more options available with this account type.</span></span> <span data-ttu-id="2df02-138">您需要组合 blob 和队列, 因此_Blob 存储_选项将不起作用。</span><span class="sxs-lookup"><span data-stu-id="2df02-138">You need a mix of blobs and a queue, so the _Blob storage_ option will not work.</span></span> <span data-ttu-id="2df02-139">对于此应用程序, 选择_存储 (通用 v1)_ 帐户不会带来任何好处, 因为这将限制您可以访问的功能, 并且不大可能降低预期工作负荷的成本。</span><span class="sxs-lookup"><span data-stu-id="2df02-139">For this application, there would be no benefit to choosing a _Storage (general purpose v1)_ account, since that would limit the features you could access and would be unlikely to reduce the cost of your expected workload.</span></span>

1. <span data-ttu-id="2df02-140">为**复制**选项选择 "_本地冗余存储 (LRS)_ "。</span><span class="sxs-lookup"><span data-stu-id="2df02-140">Select _Locally-redundant storage (LRS)_ for the **Replication** option.</span></span> <span data-ttu-id="2df02-141">Azure 存储帐户中的数据始终进行复制以确保高可用性-通过此选项, 可以选择与您的持续性要求相比, 复制发生的距离。</span><span class="sxs-lookup"><span data-stu-id="2df02-141">Data in Azure storage accounts are always replicated to ensure high availability - this option lets you choose how far away the replication occurs to match your durability requirements.</span></span> <span data-ttu-id="2df02-142">在我们的示例中, 图像和视频会快速过期, 并从网站中删除。</span><span class="sxs-lookup"><span data-stu-id="2df02-142">In our case, the images and videos quickly become out-of-date and are removed from the site.</span></span> <span data-ttu-id="2df02-143">因此, 为全局冗余支付额外的价值没有什么价值。</span><span class="sxs-lookup"><span data-stu-id="2df02-143">As a result, there is little value to paying extra for global redundancy.</span></span> <span data-ttu-id="2df02-144">如果灾难性事件导致数据丢失, 则可以使用用户的新内容重新启动网站。</span><span class="sxs-lookup"><span data-stu-id="2df02-144">If a catastrophic event results in data loss, you can restart the site with fresh content from your users.</span></span>

1. <span data-ttu-id="2df02-145">将**访问级别**设置为 "_热_"。</span><span class="sxs-lookup"><span data-stu-id="2df02-145">Set the **Access tier** to _Hot_.</span></span> <span data-ttu-id="2df02-146">此设置仅用于 Blob 存储。</span><span class="sxs-lookup"><span data-stu-id="2df02-146">This setting is only used for Blob storage.</span></span> <span data-ttu-id="2df02-147">"**热访问" 层**非常适合于频繁访问的数据, 并且很**酷的 access 层**更适合于不经常访问的数据。</span><span class="sxs-lookup"><span data-stu-id="2df02-147">The **Hot Access Tier** is ideal for frequently accessed data, and the **Cool Access Tier** is better for infrequently accessed data.</span></span> <span data-ttu-id="2df02-148">请注意, 这只会设置_默认_值-创建 Blob 时, 可以为数据设置不同的值。</span><span class="sxs-lookup"><span data-stu-id="2df02-148">Note that this only sets the _default_ value - when you create a Blob, you can set a different value for the data.</span></span> <span data-ttu-id="2df02-149">在我们的示例中, 我们希望快速加载视频, 因此您将使用 blob 的高性能选项。</span><span class="sxs-lookup"><span data-stu-id="2df02-149">In our case, we want the videos to load quickly, so you will use the high-performance option for your blobs.</span></span>

<span data-ttu-id="2df02-150">下面的屏幕截图显示了 "**基本**" 选项卡的已完成设置。请注意, 资源组、订阅和名称将具有不同的值。</span><span class="sxs-lookup"><span data-stu-id="2df02-150">The following screenshot shows the completed settings for the **Basics** tab. Note that the resource group, subscription, and name will have different values.</span></span>

!["创建存储帐户" 边栏的屏幕截图 (选择了 \* \* 基础 \* \* 选项卡)。](../media/5-create-storage-account-basics.png)

### <a name="configure-the-advanced-options"></a><span data-ttu-id="2df02-152">配置高级选项</span><span class="sxs-lookup"><span data-stu-id="2df02-152">Configure the advanced options</span></span>

1. <span data-ttu-id="2df02-153">单击 "**下一步: 高级 >** " 按钮以移动到 "**高级**" 选项卡, 或选择屏幕顶部的 "**高级**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="2df02-153">Click the **Next: Advanced >** button to move to the **Advanced** tab, or select the **Advanced** tab at the top of the screen.</span></span>

1. <span data-ttu-id="2df02-154">将**必需的安全传输**设置为_启用_。</span><span class="sxs-lookup"><span data-stu-id="2df02-154">Set **Secure transfer required** to _Enabled_.</span></span> <span data-ttu-id="2df02-155">"**需要安全传输**" 设置用于控制是否可将**HTTP**用于访问存储帐户中的数据的 REST api。</span><span class="sxs-lookup"><span data-stu-id="2df02-155">The **Secure transfer required** setting controls whether **HTTP** can be used for the REST APIs used to access data in the Storage account.</span></span> <span data-ttu-id="2df02-156">将此选项设置为 "_启用_" 将强制所有客户端使用 SSL (**HTTPS**)。</span><span class="sxs-lookup"><span data-stu-id="2df02-156">Setting this option to _Enabled_ will force all clients to use SSL (**HTTPS**).</span></span> <span data-ttu-id="2df02-157">在大多数情况中, 您希望将其设置为 "_启用_" 以在网络上使用 HTTPS 被视为一种最佳做法。</span><span class="sxs-lookup"><span data-stu-id="2df02-157">Most of the time you will want to set this to _Enabled_ as using HTTPS over the network is considered a best practice.</span></span>

    > [!WARNING]
    > <span data-ttu-id="2df02-158">如果启用此选项, 它将强制实施一些额外的限制。</span><span class="sxs-lookup"><span data-stu-id="2df02-158">If this option is enabled, it will enforce some additional restrictions.</span></span> <span data-ttu-id="2df02-159">未加密的 Azure 文件服务连接将失败, 包括在 Linux 上使用 SMB 2.1 或3.0 的方案。</span><span class="sxs-lookup"><span data-stu-id="2df02-159">Azure files service connections without encryption will fail, including scenarios using SMB 2.1 or 3.0 on Linux.</span></span> <span data-ttu-id="2df02-160">由于 Azure 存储不支持自定义域名的 SSL, 因此此选项不能与自定义域名一起使用。</span><span class="sxs-lookup"><span data-stu-id="2df02-160">Because Azure storage doesn’t support SSL for custom domain names, this option cannot be used with a custom domain name.</span></span>

1. <span data-ttu-id="2df02-161">将 "**虚拟网络**" 选项设置为 "_所有网络_"。</span><span class="sxs-lookup"><span data-stu-id="2df02-161">Set the **Virtual networks** option to _All networks_.</span></span> <span data-ttu-id="2df02-162">此选项允许您隔离 Azure 虚拟网络上的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2df02-162">This option allows you to isolate the storage account on an Azure virtual network.</span></span> <span data-ttu-id="2df02-163">我们想要使用公共 Internet 访问。</span><span class="sxs-lookup"><span data-stu-id="2df02-163">We want to use public Internet access.</span></span> <span data-ttu-id="2df02-164">我们的内容面向公众, 你需要允许从公共客户端进行访问。</span><span class="sxs-lookup"><span data-stu-id="2df02-164">Our content is public facing and you need to allow access from public clients.</span></span>

1. <span data-ttu-id="2df02-165">将**Data Lake Storage Gen2**选项保留为 "_已禁用_"。</span><span class="sxs-lookup"><span data-stu-id="2df02-165">Leave the **Data Lake Storage Gen2** option as _Disabled_.</span></span> <span data-ttu-id="2df02-166">这适用于与此模块不相关的大型数据应用程序。</span><span class="sxs-lookup"><span data-stu-id="2df02-166">This is for big-data applications that aren't relevant to this module.</span></span>

<span data-ttu-id="2df02-167">下面的屏幕截图显示了 "**高级**" 选项卡的已完成设置。</span><span class="sxs-lookup"><span data-stu-id="2df02-167">The following screenshot shows the completed settings for the **Advanced** tab.</span></span>

!["创建存储帐户" 选项卡的屏幕截图, 其中 "高级 \* \*" 选项卡处于选定状态。](../media/5-create-storage-account-advanced.png)

### <a name="create"></a><span data-ttu-id="2df02-169">Create</span><span class="sxs-lookup"><span data-stu-id="2df02-169">Create</span></span>

1. <span data-ttu-id="2df02-170">您可以根据需要浏览**标签**设置。</span><span class="sxs-lookup"><span data-stu-id="2df02-170">You can explore the **Tags** settings if you like.</span></span> <span data-ttu-id="2df02-171">这使您可以将键/值对与您的分类帐户相关联, 并且是可用于任何 Azure 资源的功能。</span><span class="sxs-lookup"><span data-stu-id="2df02-171">This lets you associate key/value pairs to the account for your categorization and is a feature available to any Azure resource.</span></span>

1. <span data-ttu-id="2df02-172">单击 "**审阅 + 创建**" 以查看设置。</span><span class="sxs-lookup"><span data-stu-id="2df02-172">Click **Review + create** to review the settings.</span></span> <span data-ttu-id="2df02-173">这将对你的选项进行快速验证, 以确保选择了所有必需的字段。</span><span class="sxs-lookup"><span data-stu-id="2df02-173">This will do a quick validation of your options to make sure all the required fields are selected.</span></span> <span data-ttu-id="2df02-174">如果出现问题, 我们将在此处报告这些问题。</span><span class="sxs-lookup"><span data-stu-id="2df02-174">If there are issues, they'll be reported here.</span></span> <span data-ttu-id="2df02-175">查看设置后, 单击 "**创建**" 以设置存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2df02-175">Once you've reviewed the settings, click **Create** to provision the storage account.</span></span>

<span data-ttu-id="2df02-176">部署该帐户需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="2df02-176">It will take a few minutes to deploy the account.</span></span> <span data-ttu-id="2df02-177">在 Azure 中工作时, 让我们来探究我们将用于此帐户的 api。</span><span class="sxs-lookup"><span data-stu-id="2df02-177">While Azure is working on that, let's explore the APIs we'll use with this account.</span></span>

### <a name="verify"></a><span data-ttu-id="2df02-178">Verify</span><span class="sxs-lookup"><span data-stu-id="2df02-178">Verify</span></span>

1. <span data-ttu-id="2df02-179">选择左侧边栏中的 "**存储帐户**" 链接。</span><span class="sxs-lookup"><span data-stu-id="2df02-179">Select the **Storage accounts** link in the left sidebar.</span></span>

1. <span data-ttu-id="2df02-180">在列表中找到新的存储帐户以验证创建是否成功。</span><span class="sxs-lookup"><span data-stu-id="2df02-180">Locate the new storage account in the list to verify that creation succeeded.</span></span>

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

<span data-ttu-id="2df02-181">当您在自己的订阅中工作时, 可以在 Azure 门户中使用以下步骤来删除资源组和所有关联的资源。</span><span class="sxs-lookup"><span data-stu-id="2df02-181">When you are working in your own subscription, you can use the following steps in the Azure portal to delete the resource group and all associated resources.</span></span>

1. <span data-ttu-id="2df02-182">选择左侧边栏中的 "**资源组**" 链接。</span><span class="sxs-lookup"><span data-stu-id="2df02-182">Select the **Resource groups** link in the left sidebar.</span></span>

1. <span data-ttu-id="2df02-183">在列表中查找您创建的资源组。</span><span class="sxs-lookup"><span data-stu-id="2df02-183">Locate the resource group you created in the list.</span></span>

1. <span data-ttu-id="2df02-184">右键单击资源组条目, 然后从上下文菜单中选择 "**删除资源组**"。</span><span class="sxs-lookup"><span data-stu-id="2df02-184">Right-click on the resource group entry and select **Delete resource group** from the context menu.</span></span> <span data-ttu-id="2df02-185">也可以单击 "..."项右侧的 menu 元素, 以获取相同的上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="2df02-185">You can also click the "..." menu element on the right side of the entry to get to the same context menu.</span></span>

1. <span data-ttu-id="2df02-186">在 "确认" 字段中键入资源组的名称。</span><span class="sxs-lookup"><span data-stu-id="2df02-186">Type the resource group name into the confirmation field.</span></span>

1. <span data-ttu-id="2df02-187">单击 "**删除**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2df02-187">Click the **Delete** button.</span></span> <span data-ttu-id="2df02-188">这可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="2df02-188">This may take several minutes.</span></span>

<span data-ttu-id="2df02-189">您创建了包含由业务要求驱动的设置的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2df02-189">You created a storage account with settings driven by your business requirements.</span></span> <span data-ttu-id="2df02-190">例如, 您可能已经选择了 "美国西部" 数据中心, 因为您的客户主要位于南部加利福尼亚州。</span><span class="sxs-lookup"><span data-stu-id="2df02-190">For example, you might have selected a West US datacenter because your customers were primarily located in southern California.</span></span> <span data-ttu-id="2df02-191">这是典型的流程: 首先分析您的数据和目标, 然后配置要匹配的存储帐户选项。</span><span class="sxs-lookup"><span data-stu-id="2df02-191">This is a typical flow: first analyze your data and goals, and then configure the storage account options to match.</span></span>