<span data-ttu-id="2a8df-101">假设您低估了一些上载文件的大小, 以及您的上传磁盘空间不足的情况。</span><span class="sxs-lookup"><span data-stu-id="2a8df-101">Let's say you underestimated how large some of the uploaded files would be and that your upload disk is running out of space.</span></span> <span data-ttu-id="2a8df-102">您决定将空间从 64 gb 加倍到 128 gb。</span><span class="sxs-lookup"><span data-stu-id="2a8df-102">You decide to double the space from 64 GB to 128 GB.</span></span>

<span data-ttu-id="2a8df-103">在这里, 你将练习在以前的单元中学习的过程。</span><span class="sxs-lookup"><span data-stu-id="2a8df-103">Here you'll practice the process you learned about in the previous units.</span></span>

## <a name="resize-the-data-disk"></a><span data-ttu-id="2a8df-104">调整数据磁盘的大小</span><span class="sxs-lookup"><span data-stu-id="2a8df-104">Resize the data disk</span></span>

<span data-ttu-id="2a8df-105">若要调整磁盘大小, 您需要该磁盘的 ID 或名称。</span><span class="sxs-lookup"><span data-stu-id="2a8df-105">To resize a disk, you need the ID or name of the disk.</span></span> <span data-ttu-id="2a8df-106">在这种情况下, 您已经知道名称, **uploadDataDisk1**。</span><span class="sxs-lookup"><span data-stu-id="2a8df-106">In this case, you already know the name, **uploadDataDisk1**.</span></span> <span data-ttu-id="2a8df-107">但如果你不记得, 或者是由其他人创建的, 则可以运行`az disk list`以查找名称。</span><span class="sxs-lookup"><span data-stu-id="2a8df-107">But in case you didn't remember that, or it was created by someone else, you can run `az disk list` to find the name.</span></span>

1. <span data-ttu-id="2a8df-108">运行`az disk list`以打印资源组中的托管磁盘列表。</span><span class="sxs-lookup"><span data-stu-id="2a8df-108">Run `az disk list` to print the list of the managed disks in the resource group.</span></span> <span data-ttu-id="2a8df-109">如果同一资源组中有多个虚拟机, 则此列表可能包含其他磁盘。</span><span class="sxs-lookup"><span data-stu-id="2a8df-109">This list might include other disks if you have multiple VMs in the same resource group.</span></span>

    ```azurecli
    az disk list \
      --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
      --output table
    ```

    <span data-ttu-id="2a8df-110">您会看到名为**uploadDataDisk1**的磁盘。</span><span class="sxs-lookup"><span data-stu-id="2a8df-110">You see the disk named **uploadDataDisk1**.</span></span>

    ```output
    Name                                                        Gb
    ----------------------------------------------------------  ----
    support-web-vm01_OsDisk_1_141859cb21d64b85b9db3f70f0f5e851  30
    uploadDataDisk1                                             64
    ```

1. <span data-ttu-id="2a8df-111">运行以下`az vm deallocate`命令来停止和取消分配 VM。</span><span class="sxs-lookup"><span data-stu-id="2a8df-111">Run the following `az vm deallocate` command to stop and de-allocate your VM.</span></span> <span data-ttu-id="2a8df-112">这不会删除 VM, 但会将其置于可修改虚拟磁盘的状态。</span><span class="sxs-lookup"><span data-stu-id="2a8df-112">This does not delete your VM, but puts it in a state where you can modify the virtual disks.</span></span>

    ```azurecli
    az vm deallocate --name support-web-vm01
    ```

1. <span data-ttu-id="2a8df-113">运行`az disk update`以将磁盘大小调整为 128 GB。</span><span class="sxs-lookup"><span data-stu-id="2a8df-113">Run `az disk update` to resize the disk to 128 GB.</span></span>

    ```azurecli
    az disk update --name uploadDataDisk1 --size-gb 128
    ```

1. <span data-ttu-id="2a8df-114">运行`az vm start`以重新启动 VM。</span><span class="sxs-lookup"><span data-stu-id="2a8df-114">Run `az vm start` to restart the VM.</span></span>

    ```azurecli
    az vm start --name support-web-vm01
    ```

    <span data-ttu-id="2a8df-115">但我们尚未完成。</span><span class="sxs-lookup"><span data-stu-id="2a8df-115">But we aren't finished yet.</span></span> <span data-ttu-id="2a8df-116">VM 上的操作系统尚无法使用额外的空间。</span><span class="sxs-lookup"><span data-stu-id="2a8df-116">The operating system on the VM cannot use the extra space yet.</span></span> <span data-ttu-id="2a8df-117">这是在下一节中完成的。</span><span class="sxs-lookup"><span data-stu-id="2a8df-117">This is done in the next section.</span></span>

## <a name="expand-the-disk-partition"></a><span data-ttu-id="2a8df-118">展开磁盘分区</span><span class="sxs-lookup"><span data-stu-id="2a8df-118">Expand the disk partition</span></span>

<span data-ttu-id="2a8df-119">最后一步是告诉操作系统有关可用空间。</span><span class="sxs-lookup"><span data-stu-id="2a8df-119">The final step is to tell the OS about the available space.</span></span> <span data-ttu-id="2a8df-120">就像您之前执行的分区和格式步骤一样, 此过程与扩展物理、内部部署磁盘的过程相同。</span><span class="sxs-lookup"><span data-stu-id="2a8df-120">Just like the partitioning and format steps you did earlier, this process is identical to the one you'd follow to expand a physical, on-premises, disk.</span></span>

1. <span data-ttu-id="2a8df-121">虽然您可以为 vm 保留一个固定的公共 ip 地址, 但默认情况下, vm 会在取消分配并重新启动时收到新的公用 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="2a8df-121">Although you can reserve a fixed public IP address for your VM, by default your VM receives a new public IP address when it is de-allocated and restarted.</span></span> <span data-ttu-id="2a8df-122">运行以下`az vm show`命令以使用 VM 的新公共 IP 地址更新 Bash 变量。</span><span class="sxs-lookup"><span data-stu-id="2a8df-122">Run the following `az vm show` command to update your Bash variable with your VM's new public IP address.</span></span>

    ```azurecli
    ipaddress=$(az vm show --name support-web-vm01 -d --query [publicIps] --o tsv)
    ```

1. <span data-ttu-id="2a8df-123">正如您之前所做`lsblk`的那样, 请通过 SSH 在 VM 上运行以了解其当前状态。</span><span class="sxs-lookup"><span data-stu-id="2a8df-123">As you did earlier, run `lsblk` on your VM over SSH to understand its current state.</span></span>

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    <span data-ttu-id="2a8df-124">您可以看到磁盘`sdc/sdc1`大小为 64 GB。</span><span class="sxs-lookup"><span data-stu-id="2a8df-124">You can see that disk `sdc/sdc1` still has a size of 64 GB.</span></span>

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk 
    └─sdb1   8:17   0   14G  0 part /mnt
    sdc      8:32   0  128G  0 disk 
    └─sdc1   8:33   0   64G  0 part /uploads
    sda      8:0    0   30G  0 disk 
    └─sda1   8:1    0   30G  0 part /
    ```

1. <span data-ttu-id="2a8df-125">与您以前对磁盘初始化的方式类似, 运行此`az vm extension set`命令, 通过执行我们创建的预设的 Bash 脚本来帮助您, 在 VM 上告知有关新可用空间的操作系统。</span><span class="sxs-lookup"><span data-stu-id="2a8df-125">Similar to what you did previously to initialize your disk, run this `az vm extension set` command to tell the OS on the VM about the newly available space by executing a pre-made Bash script we create to help you along.</span></span>

    ```azurecli
    az vm extension set \
      --vm-name support-web-vm01 \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/resize-data-disk.sh"]}' \
      --protected-settings '{"commandToExecute": "./resize-data-disk.sh"}'
    ```

    <span data-ttu-id="2a8df-126">运行命令时, 可以从单独的浏览器选项卡[检查 Bash 脚本](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/resize-data-disk.sh?azure-portal=true)(如果需要)。</span><span class="sxs-lookup"><span data-stu-id="2a8df-126">While the command runs, you can [examine the Bash script](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/resize-data-disk.sh?azure-portal=true) from a separate browser tab if you'd like.</span></span>

    <span data-ttu-id="2a8df-127">总而言之, 脚本:</span><span class="sxs-lookup"><span data-stu-id="2a8df-127">To summarize, the script:</span></span>

    * <span data-ttu-id="2a8df-128">卸载磁盘`/dev/sdc1`。</span><span class="sxs-lookup"><span data-stu-id="2a8df-128">Unmounts the disk `/dev/sdc1`.</span></span>
    * <span data-ttu-id="2a8df-129">将分区1的大小调整为 128 GB。</span><span class="sxs-lookup"><span data-stu-id="2a8df-129">Resizes partition 1 to be 128 GB.</span></span>
    * <span data-ttu-id="2a8df-130">验证分区一致性。</span><span class="sxs-lookup"><span data-stu-id="2a8df-130">Verifies partition consistency.</span></span>
    * <span data-ttu-id="2a8df-131">调整文件系统的大小。</span><span class="sxs-lookup"><span data-stu-id="2a8df-131">Resizes the filesystem.</span></span>
    * <span data-ttu-id="2a8df-132">Remounts 将驱动器`/dev/sdc1`重新安装到装入点`/uploads`。</span><span class="sxs-lookup"><span data-stu-id="2a8df-132">Remounts the drive `/dev/sdc1` back to the mount point `/uploads`.</span></span>

1. <span data-ttu-id="2a8df-133">若要验证配置, 请`lsblk`再次在你的 VM 上运行 SSH。</span><span class="sxs-lookup"><span data-stu-id="2a8df-133">To verify the configuration, run `lsblk` on your VM over SSH a second time.</span></span>

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    <span data-ttu-id="2a8df-134">这次, 您会看到磁盘`sdc/sdc1`已扩展, 以适应磁盘大小的增长。</span><span class="sxs-lookup"><span data-stu-id="2a8df-134">This time, you see that disk `sdc/sdc1` is expanded to accommodate the increased size of your disk.</span></span>

    ```output
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0    14G  0 disk 
    └─sdb1   8:17   0    14G  0 part /mnt
    sdc      8:32   0   128G  0 disk 
    └─sdc1   8:33   0 119.2G  0 part /uploads
    sda      8:0    0    30G  0 disk 
    └─sda1   8:1    0    30G  0 part /
    ```

1. <span data-ttu-id="2a8df-135">作为最后的验证步骤, 请通过 SSH 在 VM `df`上运行操作系统的实用工具, 以证明 OS 可以正确地进行查看。</span><span class="sxs-lookup"><span data-stu-id="2a8df-135">As a final verification step, run the operating system's `df` utility on your VM over SSH to prove that the OS can see it correctly.</span></span>

    ```bash
    ssh azureuser@$ipaddress df -h
    ```

    <span data-ttu-id="2a8df-136">您会看到驱动器的大小为 128 GB。</span><span class="sxs-lookup"><span data-stu-id="2a8df-136">You see that the drive's size is 128 GB.</span></span>

    ```output
    Filesystem      Size  Used Avail Use% Mounted on
    udev            3.4G     0  3.4G   0% /dev
    tmpfs           697M  8.6M  689M   2% /run
    /dev/sda1        30G  1.4G   28G   5% /
    tmpfs           3.5G     0  3.5G   0% /dev/shm
    tmpfs           5.0M     0  5.0M   0% /run/lock
    tmpfs           3.5G     0  3.5G   0% /sys/fs/cgroup
    /dev/sdb1        14G   35M   13G   1% /mnt
    /dev/sdc1        63G   52M   60G   1% /uploads
    tmpfs           697M     0  697M   0% /run/user/1000
    ```