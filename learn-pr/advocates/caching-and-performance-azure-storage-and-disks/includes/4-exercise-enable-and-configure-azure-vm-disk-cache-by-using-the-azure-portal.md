
<span data-ttu-id="50e2b-101">假设您运行的照片共享网站的数据存储在运行 SQL Server 和自定义应用程序的 Azure 虚拟机 (vm) 上。</span><span class="sxs-lookup"><span data-stu-id="50e2b-101">Suppose you run a photo sharing site with data stored on Azure virtual machines (VMs) running SQL Server and custom applications.</span></span> <span data-ttu-id="50e2b-102">您希望进行以下调整:</span><span class="sxs-lookup"><span data-stu-id="50e2b-102">You want to make the following adjustments:</span></span>

- <span data-ttu-id="50e2b-103">您需要更改 VM 上的磁盘缓存设置。</span><span class="sxs-lookup"><span data-stu-id="50e2b-103">You need to change the disk cache settings on a VM.</span></span>
- <span data-ttu-id="50e2b-104">您想要将新的数据磁盘添加到虚拟机, 并启用缓存。</span><span class="sxs-lookup"><span data-stu-id="50e2b-104">You want to add a new data disk to the VM with caching enabled.</span></span>

<span data-ttu-id="50e2b-105">你已决定通过 Azure 门户进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="50e2b-105">You've decided to make these changes through the Azure portal.</span></span>

<span data-ttu-id="50e2b-106">在本练习中, 我们将逐步完成对上面所述的 VM 进行的更改。</span><span class="sxs-lookup"><span data-stu-id="50e2b-106">In this exercise, we'll walk through making the changes to a VM that we described above.</span></span> <span data-ttu-id="50e2b-107">首先, 让我们登录到门户并创建 VM。</span><span class="sxs-lookup"><span data-stu-id="50e2b-107">First, let's sign in to the portal and create a VM.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-virtual-machine"></a><span data-ttu-id="50e2b-108">创建虚拟机</span><span class="sxs-lookup"><span data-stu-id="50e2b-108">Create a virtual machine</span></span>

<span data-ttu-id="50e2b-109">在此步骤中, 我们将创建具有以下属性的 VM:</span><span class="sxs-lookup"><span data-stu-id="50e2b-109">In this step, we're going to create a VM with the following properties:</span></span>

| <span data-ttu-id="50e2b-110">属性</span><span class="sxs-lookup"><span data-stu-id="50e2b-110">Property</span></span>        | <span data-ttu-id="50e2b-111">值</span><span class="sxs-lookup"><span data-stu-id="50e2b-111">Value</span></span>   |
|-----------------|---------|
| <span data-ttu-id="50e2b-112">图像</span><span class="sxs-lookup"><span data-stu-id="50e2b-112">Image</span></span>           | <span data-ttu-id="50e2b-113">**Windows Server 2016 Datacenter**</span><span class="sxs-lookup"><span data-stu-id="50e2b-113">**Windows Server 2016 Datacenter**</span></span> |
| <span data-ttu-id="50e2b-114">名称</span><span class="sxs-lookup"><span data-stu-id="50e2b-114">Name</span></span>            | <span data-ttu-id="50e2b-115">**fotoshareVM**</span><span class="sxs-lookup"><span data-stu-id="50e2b-115">**fotoshareVM**</span></span> |
| <span data-ttu-id="50e2b-116">资源组</span><span class="sxs-lookup"><span data-stu-id="50e2b-116">Resource group</span></span>  |   <span data-ttu-id="50e2b-117">**<rgn>[沙盒资源组名称]</rgn>**</span><span class="sxs-lookup"><span data-stu-id="50e2b-117">**<rgn>[sandbox resource group name]</rgn>**</span></span> |
| <span data-ttu-id="50e2b-118">位置</span><span class="sxs-lookup"><span data-stu-id="50e2b-118">Location</span></span>        | <span data-ttu-id="50e2b-119">请参见下文。</span><span class="sxs-lookup"><span data-stu-id="50e2b-119">See below.</span></span> |

1. <span data-ttu-id="50e2b-120">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="50e2b-120">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="50e2b-121">选择左侧侧栏菜单中的 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-121">Select **Create a resource** in the sidebar menu on the left.</span></span>

1. <span data-ttu-id="50e2b-122">_Windows Server 2016 VM_应位于**受欢迎**的 Marketplace 元素列表中。</span><span class="sxs-lookup"><span data-stu-id="50e2b-122">_Windows Server 2016 VM_ should be in the list of **Popular** Marketplace elements.</span></span> <span data-ttu-id="50e2b-123">如果不是, 请尝试使用顶部的搜索框搜索 "Windows Server 2016 DataCenter"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-123">If not, try searching for "Windows Server 2016 DataCenter" using the search box on the top.</span></span>

1. <span data-ttu-id="50e2b-124">选择 "Windows VM", 然后单击 "**创建**" 以启动 VM 创建过程。</span><span class="sxs-lookup"><span data-stu-id="50e2b-124">Select the Windows VM and click **Create** to start the VM creation process.</span></span>

1. <span data-ttu-id="50e2b-125">在 "**基础知识**" 面板中, 验证所选**订阅**是否为_Concierge 订阅_。</span><span class="sxs-lookup"><span data-stu-id="50e2b-125">In the **Basics** panel, verify the selected **Subscription** is _Concierge Subscription_.</span></span>

1. <span data-ttu-id="50e2b-126">在 "**资源组**" 下, 选择 "**使用现有**" 并选择 " _<rgn>[沙盒资源组名称]</rgn>_"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-126">Under **Resource Group**, select **Use Existing** and choose _<rgn>[sandbox resource group name]</rgn>_.</span></span>

1. <span data-ttu-id="50e2b-127">在 "**虚拟机名称**" 框中, 输入_fotoshareVM_。</span><span class="sxs-lookup"><span data-stu-id="50e2b-127">In the **Virtual machine name** box, enter _fotoshareVM_.</span></span>

1. <span data-ttu-id="50e2b-128">在 "**位置**" 下拉列表中, 从以下列表中选择最接近你的区域。</span><span class="sxs-lookup"><span data-stu-id="50e2b-128">In the **Location** drop-down list, select the closest region to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="50e2b-129">对于 VM**大小**, 默认值为**DS1 v2** , 它为您提供了一个 CPU 和 3.5 GB 的内存。</span><span class="sxs-lookup"><span data-stu-id="50e2b-129">For the VM **Size**, the default is **DS1 v2** which gives you a single CPU and 3.5 GB of memory.</span></span> <span data-ttu-id="50e2b-130">这在此示例中很不错。</span><span class="sxs-lookup"><span data-stu-id="50e2b-130">That's fine for this example.</span></span>

1. <span data-ttu-id="50e2b-131">在 "**管理员帐户**" 部分中, 为新 VM 上的管理员帐户输入**用户名**和**密码**/"**确认密码**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-131">In **ADMINISTRATOR ACCOUNT** section, enter a **Username** and **Password**/**Confirm password** for an administrator account on the new VM.</span></span>

1. <span data-ttu-id="50e2b-132">下面的图像是在填写时**基本**配置的外观示例。保留其余选项卡和字段的默认值, 然后单击 "**审阅 + 创建**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-132">The following image is an example of what the **Basics** configuration looks like when filled out. Leave the defaults for the remaining tabs and fields and click **Review + create**.</span></span>

    ![显示 "创建虚拟机" 边栏的 Azure 门户屏幕截图, 其中一些示例基本配置已按说明进行填写。](../media/4-basics-vm.png)

1. <span data-ttu-id="50e2b-134">检查新的 vm 设置后, 单击 "**创建**" 以开始部署新的 vm。</span><span class="sxs-lookup"><span data-stu-id="50e2b-134">After reviewing your new VM settings, click **Create** to start the deploying your new VM.</span></span>

<span data-ttu-id="50e2b-135">VM 创建可能需要几分钟时间, 因为它会创建所有不同的资源 (存储、网络接口等) 来支持虚拟机。</span><span class="sxs-lookup"><span data-stu-id="50e2b-135">VM creation can take a few minutes as it creates all the various resources (storage, network interface, etc.) to support the virtual machine.</span></span> <span data-ttu-id="50e2b-136">等待 VM 部署完毕, 然后再继续练习。</span><span class="sxs-lookup"><span data-stu-id="50e2b-136">Wait until the VM has deployed before continuing with the exercise.</span></span>

## <a name="view-os-disk-cache-status-in-the-portal"></a><span data-ttu-id="50e2b-137">在门户中查看 OS 磁盘缓存状态</span><span class="sxs-lookup"><span data-stu-id="50e2b-137">View OS disk cache status in the portal</span></span>

<span data-ttu-id="50e2b-138">部署虚拟机后, 我们可以使用以下步骤确认 OS 磁盘的缓存状态:</span><span class="sxs-lookup"><span data-stu-id="50e2b-138">Once our VM is deployed, we can confirm the caching status of the OS disk using the following steps:</span></span>

1. <span data-ttu-id="50e2b-139">选择 " **fotoshareVM** " 资源以在门户中打开 VM 详细信息。</span><span class="sxs-lookup"><span data-stu-id="50e2b-139">Select the **fotoshareVM** resource to open the VM details in the portal.</span></span> <span data-ttu-id="50e2b-140">或者, 您可以单击左侧边栏中的 "**所有资源**", 然后选择您的 VM **fotoshareVM**。</span><span class="sxs-lookup"><span data-stu-id="50e2b-140">Alternatively, you can click **All resources** in the left sidebar and then select your VM, **fotoshareVM**.</span></span>

1. <span data-ttu-id="50e2b-141">在 "**设置**" 下, 选择 "**磁盘**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-141">Under **Settings**, select **Disks**.</span></span>

1. <span data-ttu-id="50e2b-142">在**磁盘**窗格中, VM 具有一个磁盘, 即 OS 磁盘。</span><span class="sxs-lookup"><span data-stu-id="50e2b-142">On the **Disks** pane, the VM has one disk, the OS disk.</span></span> <span data-ttu-id="50e2b-143">其缓存类型当前设置为可**读/写**的默认值。</span><span class="sxs-lookup"><span data-stu-id="50e2b-143">Its cache type is currently set to the default value of **Read/write**.</span></span>

![显示 VM 刀片磁盘部分的 Azure 门户屏幕截图, 操作系统磁盘显示并设置为只读缓存。](../media/4-os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a><span data-ttu-id="50e2b-145">在门户中更改 OS 磁盘的缓存设置</span><span class="sxs-lookup"><span data-stu-id="50e2b-145">Change the cache settings of the OS disk in the portal</span></span>

1. <span data-ttu-id="50e2b-146">在 "**磁盘**" 窗格中, 选择屏幕左上角的 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-146">On the **Disks** pane, select **Edit** in the upper left of the screen.</span></span>

1. <span data-ttu-id="50e2b-147">使用下拉列表将 OS 磁盘的**主机缓存**值更改为**只读**, 然后选择屏幕左上角的 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-147">Change the **HOST CACHING** value for the OS disk to **Read-only** using the drop-down list, and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="50e2b-148">此更新可能需要一段时间。</span><span class="sxs-lookup"><span data-stu-id="50e2b-148">This update can take some time.</span></span> <span data-ttu-id="50e2b-149">原因是, 更改 Azure 磁盘的缓存设置会分离和将目标磁盘。</span><span class="sxs-lookup"><span data-stu-id="50e2b-149">The reason is that changing the cache setting of an Azure disk detaches and reattaches the target disk.</span></span> <span data-ttu-id="50e2b-150">如果它是操作系统磁盘, 也会重新启动虚拟机。</span><span class="sxs-lookup"><span data-stu-id="50e2b-150">If it's the operating system disk, the VM is also restarted.</span></span> <span data-ttu-id="50e2b-151">操作完成后, 你将收到一条通知, 指出 VM 磁盘已更新。</span><span class="sxs-lookup"><span data-stu-id="50e2b-151">When the operation completes, you'll get a notification saying the VM disks have been updated.</span></span>

1. <span data-ttu-id="50e2b-152">完成后, OS 磁盘缓存类型将设置为**只读**。</span><span class="sxs-lookup"><span data-stu-id="50e2b-152">Once complete, the OS disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="50e2b-153">让我们转到数据磁盘缓存配置。</span><span class="sxs-lookup"><span data-stu-id="50e2b-153">Let's move on to data disk cache configuration.</span></span> <span data-ttu-id="50e2b-154">若要配置磁盘, 我们需要先创建一个磁盘。</span><span class="sxs-lookup"><span data-stu-id="50e2b-154">To configure a disk, we'll need first to create one.</span></span>

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a><span data-ttu-id="50e2b-155">将数据磁盘添加到 VM 并设置缓存类型</span><span class="sxs-lookup"><span data-stu-id="50e2b-155">Add a data disk to the VM and set caching type</span></span>

1. <span data-ttu-id="50e2b-156">回到门户中的虚拟机的**磁盘**视图, 继续执行, 然后单击 "**添加数据磁盘**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-156">Back on the **Disks** view of our VM in the portal, go ahead and click **Add data disk**.</span></span> <span data-ttu-id="50e2b-157">"**名称**" 字段中会立即出现一个错误, 告诉我们该字段不能为空。</span><span class="sxs-lookup"><span data-stu-id="50e2b-157">An error immediately appears in the **Name** field, telling us that the field can't be empty.</span></span> <span data-ttu-id="50e2b-158">我们还没有数据磁盘, 因此我们创建一个。</span><span class="sxs-lookup"><span data-stu-id="50e2b-158">We don't have a data disk yet, so let's create one.</span></span>

1. <span data-ttu-id="50e2b-159">在 "**名称**" 列表中单击, 然后单击 "**创建磁盘**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-159">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="50e2b-160">在 "**创建托管磁盘**" 窗格中的 "**名称**" 框中, 键入**fotosharesVM-data**。</span><span class="sxs-lookup"><span data-stu-id="50e2b-160">In the **Create managed disk** pane, in the **Name** box, type **fotosharesVM-data**.</span></span>

1. <span data-ttu-id="50e2b-161">在 "**资源组**" 下, 选择 "**使用现有**", 然后选择 " _<rgn>[沙盒资源组名称]</rgn>_"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-161">Under **Resource Group**, select **Use existing**, and select _<rgn>[sandbox resource group name]</rgn>_.</span></span>

1. <span data-ttu-id="50e2b-162">记下剩余字段的默认值:</span><span class="sxs-lookup"><span data-stu-id="50e2b-162">Note the defaults for the remaining fields:</span></span>
    - <span data-ttu-id="50e2b-163">高级 SSD</span><span class="sxs-lookup"><span data-stu-id="50e2b-163">Premium SSD</span></span>
    - <span data-ttu-id="50e2b-164">1023 GB 大小</span><span class="sxs-lookup"><span data-stu-id="50e2b-164">1023 GB in size</span></span>
    - <span data-ttu-id="50e2b-165">在与 VM 相同的位置 (不可更改)。</span><span class="sxs-lookup"><span data-stu-id="50e2b-165">In the same location as the VM (not changeable).</span></span>
    - <span data-ttu-id="50e2b-166">IOPS 限制-5000</span><span class="sxs-lookup"><span data-stu-id="50e2b-166">IOPS limit - 5000</span></span>
    - <span data-ttu-id="50e2b-167">吞吐量限制 (MB/秒)-200</span><span class="sxs-lookup"><span data-stu-id="50e2b-167">Throughput limit (MB/s) - 200</span></span>

1. <span data-ttu-id="50e2b-168">在屏幕底部, 单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-168">Click **Create** at the bottom of the screen.</span></span>

    <span data-ttu-id="50e2b-169">等到创建完磁盘, 然后再继续。</span><span class="sxs-lookup"><span data-stu-id="50e2b-169">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="50e2b-170">使用下拉列表将新的数据磁盘的**主机缓存**值更改为**只读**(可能已设置), 然后单击屏幕左上角的 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="50e2b-170">Change the **HOST CACHING** value for our new data disk to **Read-only** using the drop-down list (it might be set already), and then click **Save** in the upper left of the screen.</span></span>

    <span data-ttu-id="50e2b-171">等待 VM 完成更新新数据磁盘。</span><span class="sxs-lookup"><span data-stu-id="50e2b-171">Wait for the VM to finish updating the new data disk.</span></span> <span data-ttu-id="50e2b-172">完成后, 你的虚拟机上将有一个新的数据磁盘。</span><span class="sxs-lookup"><span data-stu-id="50e2b-172">Once complete, you will have a new data disk on your virtual machine.</span></span>

<span data-ttu-id="50e2b-173">在本练习中, 我们使用 Azure 门户在新 VM 上配置缓存、更改现有磁盘上的缓存设置以及在新的数据磁盘上配置缓存。</span><span class="sxs-lookup"><span data-stu-id="50e2b-173">In this exercise, we used the Azure portal to configure caching on a new VM, change cache settings on an existing disk, and configure caching on a new data disk.</span></span> <span data-ttu-id="50e2b-174">下面的屏幕截图显示了最后的配置:</span><span class="sxs-lookup"><span data-stu-id="50e2b-174">The following screenshot shows the final configuration:</span></span>

![在我们的 VM 刀片的磁盘部分中显示操作系统磁盘和新数据磁盘的 Azure 门户屏幕截图, 同时将这两个磁盘设置为只读缓存。](../media/disks-final-config-portal.PNG)
