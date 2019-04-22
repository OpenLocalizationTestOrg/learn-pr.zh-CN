<span data-ttu-id="305f1-101">azure 将 VHD 映像存储为 Azure 存储帐户中的页面 blob。</span><span class="sxs-lookup"><span data-stu-id="305f1-101">Azure stores your VHD images as page blobs in an Azure Storage account.</span></span> <span data-ttu-id="305f1-102">使用托管磁盘时, Azure 会按代表管理存储-它是选择托管磁盘的最佳原因之一。</span><span class="sxs-lookup"><span data-stu-id="305f1-102">With managed disks, Azure takes care of managing the storage on your behalf - it's one of the best reasons to choose managed disks.</span></span>

<span data-ttu-id="305f1-103">创建 VM 时, 它会选择 OS 磁盘的大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-103">When you create the VM, it chooses a size for the OS disk.</span></span> <span data-ttu-id="305f1-104">根据您选择的图像的具体大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-104">The specific size is based on the image you select.</span></span> <span data-ttu-id="305f1-105">在 Linux 中, 通常约为 30 gb, 在 Windows 上约为 127 gb。</span><span class="sxs-lookup"><span data-stu-id="305f1-105">On Linux, it's often around 30 GB, and on Windows about 127 GB.</span></span>

<span data-ttu-id="305f1-106">你可以添加数据磁盘以提供额外的存储空间, 但你可能还希望扩展现有磁盘-可能是旧应用程序无法跨驱动器拆分其数据, 或者你正在将物理电脑驱动器迁移到 Azure 并需要更大的 OS 驱动器。</span><span class="sxs-lookup"><span data-stu-id="305f1-106">You can add data disks to provide for additional storage space, but you may also wish to expand an existing disk - perhaps a legacy application cannot split its data across drives, or you are migrating a physical PC's drive to Azure and need a larger OS drive.</span></span>

> [!NOTE]
> <span data-ttu-id="305f1-107">您只能将磁盘大小调整为_较大_大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-107">You can only resize a disk to a _larger_ size.</span></span> <span data-ttu-id="305f1-108">不支持缩小托管磁盘。</span><span class="sxs-lookup"><span data-stu-id="305f1-108">Shrinking managed disks is not supported.</span></span>

<span data-ttu-id="305f1-109">更改磁盘的大小还可以更改磁盘的级别 (例如, 从 P10 到 P20)。</span><span class="sxs-lookup"><span data-stu-id="305f1-109">Changing the size of the disk can also change the level of the disk (for example from P10 to P20).</span></span> <span data-ttu-id="305f1-110">请注意, 这可能会对性能升级有好处, 但在您上移到高级层时, 成本也会更高。</span><span class="sxs-lookup"><span data-stu-id="305f1-110">Keep this in mind - this can be beneficial for performance upgrades, but will also cost more as you move up the premium tiers.</span></span>

## <a name="vm-size-versus-disk-size"></a><span data-ttu-id="305f1-111">VM 大小与磁盘大小</span><span class="sxs-lookup"><span data-stu-id="305f1-111">VM size versus disk size</span></span>

<span data-ttu-id="305f1-112">创建 vm 时选择的 VM 大小决定了它可以分配多少个资源。</span><span class="sxs-lookup"><span data-stu-id="305f1-112">The VM size you choose when you create your VM determines how many resources it can allocate.</span></span> <span data-ttu-id="305f1-113">对于 storage, 大小控制可添加到 VM 的磁盘数以及每个磁盘的最大大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-113">For storage, the size controls the number of disks you can add to the VM and the maximum size of each disk.</span></span>

<span data-ttu-id="305f1-114">如前所述, 某些 VM 大小仅支持标准存储驱动器-限制 i/o 性能。</span><span class="sxs-lookup"><span data-stu-id="305f1-114">As mentioned previously, some VM sizes support only Standard storage drives - limiting the I/O performance.</span></span>

<span data-ttu-id="305f1-115">如果发现您需要的存储空间超过您的 VM 大小允许的数量, 则可以更改 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-115">If you find that you need more storage than what your VM size allows for, you can change the VM size.</span></span> <span data-ttu-id="305f1-116">我们将在 " [Azure 虚拟机模块简介](/learn/modules/intro-to-azure-virtual-machines?azure-portal=true)" 中介绍该主题。</span><span class="sxs-lookup"><span data-stu-id="305f1-116">We cover that topic in the [Introduction to Azure Virtual Machines](/learn/modules/intro-to-azure-virtual-machines?azure-portal=true) module.</span></span>

## <a name="expanding-a-disk-using-the-azure-cli"></a><span data-ttu-id="305f1-117">使用 Azure CLI 扩展磁盘</span><span class="sxs-lookup"><span data-stu-id="305f1-117">Expanding a disk using the Azure CLI</span></span>

> [!WARNING]
> <span data-ttu-id="305f1-118">始终确保在执行磁盘大小调整操作之前备份数据!</span><span class="sxs-lookup"><span data-stu-id="305f1-118">Always make sure that you back up your data before performing disk resize operations!</span></span>

<span data-ttu-id="305f1-119">无法在运行的虚拟机上执行 vhd 上的操作。</span><span class="sxs-lookup"><span data-stu-id="305f1-119">Operations on VHDs cannot be performed with the VM running.</span></span> <span data-ttu-id="305f1-120">第一步是通过`az vm deallocate`提供虚拟机名称和资源组名称来停止和取消分配 vm。</span><span class="sxs-lookup"><span data-stu-id="305f1-120">The first step is to stop and deallocate the VM with `az vm deallocate`, supplying the VM name and resource group name.</span></span>

<span data-ttu-id="305f1-121">取消分配 vm 与仅_停止_vm 不同, 它将释放相关的计算资源, 并允许 Azure 对虚拟化的硬件进行配置更改。</span><span class="sxs-lookup"><span data-stu-id="305f1-121">Deallocating a VM, unlike just _stopping_ a VM, releases the associated computing resources and allows Azure to make configuration changes to the virtualized hardware.</span></span>

> [!NOTE]
> <span data-ttu-id="305f1-122">请勿立即运行这些命令。</span><span class="sxs-lookup"><span data-stu-id="305f1-122">Don't run these commands just yet.</span></span> <span data-ttu-id="305f1-123">将在下一部分中练习此过程。</span><span class="sxs-lookup"><span data-stu-id="305f1-123">You'll practice the process in the next part.</span></span>

```azurecli
az vm deallocate \
  --resource-group <resource-group-name> \
  --name <vm-name>
```

<span data-ttu-id="305f1-124">接下来, 要调整磁盘大小, 请`az disk update`使用, 传递磁盘名称、资源组名称和新请求的大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-124">Next, to resize a disk, you use `az disk update`, passing the disk name, resource group name, and newly requested size.</span></span> <span data-ttu-id="305f1-125">扩展托管磁盘时, 指定的大小将映射到最接近的托管磁盘大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-125">When you expand a managed disk, the specified size is mapped to the nearest managed disk size.</span></span>

```azurecli
az disk update \
  --resource-group <resource-group-name> \
  --name <disk-name> \
  --size-gb 200
```

<span data-ttu-id="305f1-126">最后, 运行`az vm start`以重新启动 VM。</span><span class="sxs-lookup"><span data-stu-id="305f1-126">Finally, you run `az vm start` to restart the VM.</span></span>

```azurecli
az vm start \
  --resource-group <resource-group-name> \
  --name <vm-name>
```

## <a name="expanding-a-disk-using-the-azure-portal"></a><span data-ttu-id="305f1-127">使用 Azure 门户扩展磁盘</span><span class="sxs-lookup"><span data-stu-id="305f1-127">Expanding a disk using the Azure portal</span></span>

<span data-ttu-id="305f1-128">您还可以通过 Azure 门户扩展磁盘。</span><span class="sxs-lookup"><span data-stu-id="305f1-128">You can also expand a disk through the Azure portal.</span></span>

1. <span data-ttu-id="305f1-129">使用 vm 的 "**概述**" 页上工具栏中的 "**停止**" 按钮停止 VM。</span><span class="sxs-lookup"><span data-stu-id="305f1-129">Stop the VM using the **Stop** button in the toolbar on the **Overview** page for the VM.</span></span>

1. <span data-ttu-id="305f1-130">在 "**设置**" 部分中单击 "**磁盘**"。</span><span class="sxs-lookup"><span data-stu-id="305f1-130">Click **Disks** in the **Settings** section.</span></span>

1. <span data-ttu-id="305f1-131">选择要调整大小的数据磁盘。</span><span class="sxs-lookup"><span data-stu-id="305f1-131">Select the data disk you want to resize.</span></span>

    ![显示要编辑的 VHD 的虚拟机的磁盘部分的屏幕截图](../media/5-portal-disks.png)

1. <span data-ttu-id="305f1-133">在 "磁盘详细信息" 中, __ 键入大于当前大小的大小。</span><span class="sxs-lookup"><span data-stu-id="305f1-133">In the disk details, type a size _larger_ than the current size.</span></span> <span data-ttu-id="305f1-134">您还可以在此处从 Premium 更改为标准 (反之亦然)。</span><span class="sxs-lookup"><span data-stu-id="305f1-134">You can also change from Premium to Standard (or vice-versa) here.</span></span> <span data-ttu-id="305f1-135">这些设置将调整您的性能, 如 "预测 IOPS" 部分所示。</span><span class="sxs-lookup"><span data-stu-id="305f1-135">These settings will adjust your performance as shown in the predicted IOPS section.</span></span>

    ![显示 "新大小" 字段并突出显示 "VHD 编辑" 屏幕的屏幕截图](../media/5-resize-disk.png)

1. <span data-ttu-id="305f1-137">单击 "**保存**" 以保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="305f1-137">Click **Save** to save the changes.</span></span>

1. <span data-ttu-id="305f1-138">重新启动 VM。</span><span class="sxs-lookup"><span data-stu-id="305f1-138">Restart the VM.</span></span>


### <a name="expanding-the-partition"></a><span data-ttu-id="305f1-139">扩展分区</span><span class="sxs-lookup"><span data-stu-id="305f1-139">Expanding the partition</span></span>

<span data-ttu-id="305f1-140">就像添加新的数据磁盘一样, 展开的磁盘在您扩展分区和文件系统之前不会添加任何可用空间。</span><span class="sxs-lookup"><span data-stu-id="305f1-140">Just like adding a new data disk, an expanded disk won't add any usable space until you expand the partition and filesystem.</span></span> <span data-ttu-id="305f1-141">必须使用可供 VM 使用的 OS 工具来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="305f1-141">This must be done using the OS tools available to the VM.</span></span>

<span data-ttu-id="305f1-142">在 Windows 上, 您可以使用磁盘管理器工具或`diskpart`命令行工具。</span><span class="sxs-lookup"><span data-stu-id="305f1-142">On Windows, you might use the Disk Manager tool or the `diskpart` command line tool.</span></span>

<span data-ttu-id="305f1-143">在 Linux 上, 您可以`parted`使用`resize2fs`和。</span><span class="sxs-lookup"><span data-stu-id="305f1-143">On Linux, you might use `parted` and `resize2fs`.</span></span> <span data-ttu-id="305f1-144">您将在下一部分中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="305f1-144">You'll do that in the next part.</span></span>