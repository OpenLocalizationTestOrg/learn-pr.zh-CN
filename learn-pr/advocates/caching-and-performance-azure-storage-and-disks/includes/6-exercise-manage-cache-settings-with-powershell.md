<span data-ttu-id="eaecb-101">在上一个练习中, 我们使用 Azure 门户执行以下任务:</span><span class="sxs-lookup"><span data-stu-id="eaecb-101">In the previous exercise, we performed the following tasks using the Azure portal:</span></span>

- <span data-ttu-id="eaecb-102">查看 OS 磁盘缓存状态</span><span class="sxs-lookup"><span data-stu-id="eaecb-102">View OS disk cache status</span></span>
- <span data-ttu-id="eaecb-103">更改 OS 磁盘的缓存设置</span><span class="sxs-lookup"><span data-stu-id="eaecb-103">Change the cache settings of the OS disk</span></span>
- <span data-ttu-id="eaecb-104">将数据磁盘添加到 VM</span><span class="sxs-lookup"><span data-stu-id="eaecb-104">Add a data disk to the VM</span></span>
- <span data-ttu-id="eaecb-105">更改新数据磁盘上的缓存类型</span><span class="sxs-lookup"><span data-stu-id="eaecb-105">Change caching type on a new data disk</span></span>

<span data-ttu-id="eaecb-106">让我们使用 Azure PowerShell 来练习这些操作。</span><span class="sxs-lookup"><span data-stu-id="eaecb-106">Let's practice these operations using Azure PowerShell.</span></span> 

> [!NOTE]
> <span data-ttu-id="eaecb-107">我们将使用 azure PowerShell, 但您也可以使用 azure CLI, 它提供了与基于控制台的工具类似的功能。</span><span class="sxs-lookup"><span data-stu-id="eaecb-107">We're going to use Azure PowerShell, but you could also use the Azure CLI, which provides similar functionality as a console-based tool.</span></span> <span data-ttu-id="eaecb-108">它在 macOS、Linux 和 Windows 上运行。</span><span class="sxs-lookup"><span data-stu-id="eaecb-108">It runs on macOS, Linux, and Windows.</span></span> <span data-ttu-id="eaecb-109">如果你有兴趣了解有关 azure cli 的详细信息, 请参阅**使用 azure cli 模块管理虚拟机**。</span><span class="sxs-lookup"><span data-stu-id="eaecb-109">If you are interested in learning more about the Azure CLI, check out the **Manage Virtual Machines with the Azure CLI** module.</span></span>

<span data-ttu-id="eaecb-110">我们将使用我们在上一个练习中创建的 VM。</span><span class="sxs-lookup"><span data-stu-id="eaecb-110">We're going to use the VM we created in the previous exercise.</span></span> <span data-ttu-id="eaecb-111">此实验室中的操作假定:</span><span class="sxs-lookup"><span data-stu-id="eaecb-111">The operations in this lab assume:</span></span>

- <span data-ttu-id="eaecb-112">我们的 VM 已存在, 并被称为**fotoshareVM**</span><span class="sxs-lookup"><span data-stu-id="eaecb-112">Our VM exists and is called **fotoshareVM**</span></span>
- <span data-ttu-id="eaecb-113">我们的 VM 位于名为\*\* <rgn>[沙盒资源组名称]</rgn>的资源组中\*\*</span><span class="sxs-lookup"><span data-stu-id="eaecb-113">Our VM lives in a resource group called **<rgn>[sandbox resource group name]</rgn>**</span></span>

<span data-ttu-id="eaecb-114">如果你已使用一组不同的名称, 请将这些值替换为您的名称。</span><span class="sxs-lookup"><span data-stu-id="eaecb-114">If you've gone with a different set of names, replace these values with yours.</span></span>

<span data-ttu-id="eaecb-115">以下是我们在上一个练习中的虚拟磁盘的当前状态:</span><span class="sxs-lookup"><span data-stu-id="eaecb-115">Here's the current state of our VM disks from the last exercise:</span></span>

![操作系统和数据磁盘的屏幕截图, 都设置为只读缓存。](../media/disks-final-config-portal.PNG)

<span data-ttu-id="eaecb-117">我们使用了门户为 OS 和数据磁盘设置**主机缓存**字段。</span><span class="sxs-lookup"><span data-stu-id="eaecb-117">We used the portal to set the **HOST CACHING** field for both the OS and data disks.</span></span> <span data-ttu-id="eaecb-118">按照以下步骤操作, 请记住这一初始状态。</span><span class="sxs-lookup"><span data-stu-id="eaecb-118">Keep this initial state in mind as we work through the following steps.</span></span>

### <a name="set-up-some-variables"></a><span data-ttu-id="eaecb-119">设置一些变量</span><span class="sxs-lookup"><span data-stu-id="eaecb-119">Set up some variables</span></span>

<span data-ttu-id="eaecb-120">首先, 让我们存储一些资源名称, 以便以后可以使用它们。</span><span class="sxs-lookup"><span data-stu-id="eaecb-120">First, let's store some resource names so we can use them later.</span></span>

1. <span data-ttu-id="eaecb-121">使用右侧的 "Azure 云命令行管理程序" 终端运行以下 PowerShell 命令:</span><span class="sxs-lookup"><span data-stu-id="eaecb-121">Use the Azure Cloud Shell terminal on the right to run the following PowerShell commands:</span></span>

    > [!NOTE]
    > <span data-ttu-id="eaecb-122">在尝试这些命令之前, 请先将云命令行管理程序会话切换到**PowerShell** , 如果尚未尝试。</span><span class="sxs-lookup"><span data-stu-id="eaecb-122">Switch your Cloud Shell session to **PowerShell** before trying these commands, if it isn't already.</span></span>
    
    ```powershell
    $myRgName = "<rgn>[sandbox resource group name]</rgn>"
    $myVMName = "fotoshareVM"
    ```
    
    > [!TIP]
    > <span data-ttu-id="eaecb-123">如果云命令行管理程序会话超时, 则必须再次设置这些变量。因此, 如果可能, 请在单个会话中完成整个实验。</span><span class="sxs-lookup"><span data-stu-id="eaecb-123">You'll have to set these variables again if your Cloud Shell session times out. So, if possible, work through this entire lab in a single session.</span></span>
    
### <a name="get-info-about-our-vm"></a><span data-ttu-id="eaecb-124">获取有关我们的虚拟机的信息</span><span class="sxs-lookup"><span data-stu-id="eaecb-124">Get info about our VM</span></span>

1. <span data-ttu-id="eaecb-125">运行以下命令以获取我们的虚拟机的属性:</span><span class="sxs-lookup"><span data-stu-id="eaecb-125">Run the following command to get the properties of our VM:</span></span>

    ```powershell
    $myVM = Get-AzVM -ResourceGroupName $myRgName -VMName $myVmName
    ```
    
1. <span data-ttu-id="eaecb-126">我们将响应存储在`$myVM`变量中。</span><span class="sxs-lookup"><span data-stu-id="eaecb-126">We store the response in our `$myVM` variable.</span></span> <span data-ttu-id="eaecb-127">我们可以通过管道将输出通过`select-object`管道传递到 cmdlet, 以将显示筛选为特定属性:</span><span class="sxs-lookup"><span data-stu-id="eaecb-127">We can pipe the output into the `select-object` cmdlet to filter the display to specific properties:</span></span>

    ```powershell
    $myVM | select-object -property ResourceGroupName, Name, Type, Location
    ```
    
1. <span data-ttu-id="eaecb-128">您应该会看到如下所示的内容。</span><span class="sxs-lookup"><span data-stu-id="eaecb-128">You should get something like the following.</span></span>

    ```powershell
    ResourceGroupName Name        Type                              Location
    ----------------- ----        ----                              --------
    <rgn>[sandbox resource group name]</rgn> fotoshareVM Microsoft.Compute/virtualMachines eastus
    ```
    
### <a name="view-os-disk-cache-status"></a><span data-ttu-id="eaecb-129">查看 OS 磁盘缓存状态</span><span class="sxs-lookup"><span data-stu-id="eaecb-129">View OS disk cache status</span></span>

1. <span data-ttu-id="eaecb-130">我们可以通过`StorageProfile`对象检查缓存设置, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="eaecb-130">We can check the caching  setting through  the `StorageProfile` object, as follows:</span></span>

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching
    ```

    ```output
    ReadOnly
    ```
   
1. <span data-ttu-id="eaecb-131">让我们将其重新更改为 OS 磁盘的默认值, 即_ReadWrite_。</span><span class="sxs-lookup"><span data-stu-id="eaecb-131">Let's change it back to the default for an OS disk, which is _ReadWrite_.</span></span>

### <a name="change-the-cache-settings-of-the-os-disk"></a><span data-ttu-id="eaecb-132">更改 OS 磁盘的缓存设置</span><span class="sxs-lookup"><span data-stu-id="eaecb-132">Change the cache settings of the OS disk</span></span>

1. <span data-ttu-id="eaecb-133">可以使用相同`StorageProfile`的对象设置缓存类型的值, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="eaecb-133">We can set the value for the cache type using the same `StorageProfile` object, as follows:</span></span>

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
    ```
    
    <span data-ttu-id="eaecb-134">此命令运行速度快, 应告诉你它在本地执行某些操作。</span><span class="sxs-lookup"><span data-stu-id="eaecb-134">This command runs fast, which should tell you it's doing something locally.</span></span> <span data-ttu-id="eaecb-135">该命令仅更改`myVM`对象的属性。</span><span class="sxs-lookup"><span data-stu-id="eaecb-135">The command only changes the property on the `myVM` object.</span></span> <span data-ttu-id="eaecb-136">如下面的屏幕截图所示, 如果使用`$myVM` `Get-AzVM` cmdlet 重新分配变量来刷新变量, 则缓存值在 VM 上未发生更改。</span><span class="sxs-lookup"><span data-stu-id="eaecb-136">As the following screenshot shows, if you refresh the `$myVM` variable by reassigning it using the `Get-AzVM` cmdlet, the caching value won't have changed on the VM.</span></span>

1. <span data-ttu-id="eaecb-137">若要在 VM 本身上进行更改, 请`Update-AzVM`调用, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="eaecb-137">To make the change on the VM itself, call `Update-AzVM`, as follows:</span></span>

    ```powershell
    Update-AzVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
    <span data-ttu-id="eaecb-138">请注意, 此调用需要一段时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="eaecb-138">Notice that this call takes a while to complete.</span></span> <span data-ttu-id="eaecb-139">这是因为我们正在更新实际 vm 和 Azure 以进行更改。</span><span class="sxs-lookup"><span data-stu-id="eaecb-139">That's because we're updating the actual VM and Azure restarts the VM  to make the change.</span></span>

    ```output
    RequestId IsSuccessStatusCode StatusCode ReasonPhrase
    --------- ------------------- ---------- ------------
                             True         OK OK
    ```
    
1. <span data-ttu-id="eaecb-140">如果再次刷新该`$myVM`变量, 则会看到该对象上的更改。</span><span class="sxs-lookup"><span data-stu-id="eaecb-140">If you refresh the `$myVM` variable again, you'll see the change on the object.</span></span> <span data-ttu-id="eaecb-141">在门户中查看磁盘时, 您还会看到此处的更改。</span><span class="sxs-lookup"><span data-stu-id="eaecb-141">Looking at the disk in the portal, you'd also see the change there.</span></span> 

    ```powershell
    $myVM = Get-AzVM -ResourceGroupName $myRgName -VMName $myVmName
    $myVM.StorageProfile.OsDisk.Caching
    ```
    
    ```output
    ReadWrite
    ```
    
### <a name="list-data-disk-info"></a><span data-ttu-id="eaecb-142">列出数据磁盘信息</span><span class="sxs-lookup"><span data-stu-id="eaecb-142">List data disk info</span></span>

1. <span data-ttu-id="eaecb-143">若要查看我们在 VM 上拥有哪些数据磁盘, 请运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="eaecb-143">To see what data disks we have on our VM, run the following command:</span></span>

    ```powershell
    $myVM.StorageProfile.DataDisks
    ```
    
    ```output
    Name            : fotosharesVM-data
    DiskSizeGB      : 1023
    Lun             : 0
    Caching         : ReadOnly
    CreateOption    : Attach
    SourceImage     :
    VirtualHardDisk :
    ```
    
<span data-ttu-id="eaecb-144">目前仅有一个数据磁盘。</span><span class="sxs-lookup"><span data-stu-id="eaecb-144">We have only one data disk at the moment.</span></span> <span data-ttu-id="eaecb-145">`Lun`字段很重要。</span><span class="sxs-lookup"><span data-stu-id="eaecb-145">The `Lun` field is important.</span></span> <span data-ttu-id="eaecb-146">它是唯一的**L**ogical **U**nit **N**号码。</span><span class="sxs-lookup"><span data-stu-id="eaecb-146">It's the unique **L**ogical **U**nit **N**umber.</span></span> <span data-ttu-id="eaecb-147">当我们添加另一个数据磁盘时, 我们会为其`Lun`指定一个唯一值。</span><span class="sxs-lookup"><span data-stu-id="eaecb-147">When we add another data disk, we'll give it a unique `Lun` value.</span></span>

### <a name="add-a-new-data-disk-to-our-vm"></a><span data-ttu-id="eaecb-148">将新的数据磁盘添加到我们的虚拟机</span><span class="sxs-lookup"><span data-stu-id="eaecb-148">Add a new data disk to our VM</span></span>

1. <span data-ttu-id="eaecb-149">为方便起见, 我们将存储新的磁盘名称:</span><span class="sxs-lookup"><span data-stu-id="eaecb-149">For convenience, we'll store our new disk name:</span></span>

    ```powershell
    $newDiskName = "fotoshareVM-data2"
    ```
    
1. <span data-ttu-id="eaecb-150">运行以下`Add-AzVMDataDisk`命令以定义一个新的空 1 GB 数据磁盘:</span><span class="sxs-lookup"><span data-stu-id="eaecb-150">Run the following `Add-AzVMDataDisk` command to define a new empty 1 GB data disk:</span></span>

    ```powershell
    Add-AzVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
    ```
    <span data-ttu-id="eaecb-151">你将收到类似以下内容的响应:</span><span class="sxs-lookup"><span data-stu-id="eaecb-151">You'll get a response like:</span></span>

    ```powershell
    ResourceGroupName  : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx
    Id                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxx-xxxxxxx/resourceGroups/<rgn>[sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/fotoshareVM
    VmId               : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx
    Name               : fotoshareVM
    Type               : Microsoft.Compute/virtualMachines
    Location           : eastus
    Tags               : {}
    DiagnosticsProfile : {BootDiagnostics}
    HardwareProfile    : {VmSize}
    NetworkProfile     : {NetworkInterfaces}
    OSProfile          : {ComputerName, AdminUsername, WindowsConfiguration, Secrets}
    ProvisioningState  : Succeeded
    StorageProfile     : {ImageReference, OsDisk, DataDisks}
    ```
    
1. <span data-ttu-id="eaecb-152">我们为此磁盘提供了`Lun`一个值`1` , 因为它没有获取。</span><span class="sxs-lookup"><span data-stu-id="eaecb-152">We've given this disk a `Lun` value of `1` because it's not taken.</span></span> <span data-ttu-id="eaecb-153">我们定义了要创建的磁盘, 因此, 请运行`Update-AzVM`以进行实际更改:</span><span class="sxs-lookup"><span data-stu-id="eaecb-153">We defined the disk we want to create, so it's time to run `Update-AzVM` to make the actual change:</span></span>

    ```powershell
    Update-AzVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
1. <span data-ttu-id="eaecb-154">接下来, 我们来看看我们的数据磁盘信息:</span><span class="sxs-lookup"><span data-stu-id="eaecb-154">Let's look at our data disk info again:</span></span>

    ```powershell
    $myVM.StorageProfile.DataDisks
    ```
    
    ```output
    Name            : fotosharesVM-data
    DiskSizeGB      : 1023
    Lun             : 0
    Caching         : ReadOnly
    CreateOption    : Attach
    SourceImage     :
    VirtualHardDisk :
    
    Name            : fotoshareVM-data2
    DiskSizeGB      : 1
    Lun             : 1
    Caching         : None
    CreateOption    : Empty
    SourceImage     :
    VirtualHardDisk :
    ```

<span data-ttu-id="eaecb-155">现在, 我们有两个磁盘。</span><span class="sxs-lookup"><span data-stu-id="eaecb-155">We now have two disks.</span></span> <span data-ttu-id="eaecb-156">`Lun`新磁盘具有`1`的和的默认值`Caching`为。 `None`</span><span class="sxs-lookup"><span data-stu-id="eaecb-156">Our new disk has a `Lun` of `1` and the default value for `Caching` is `None`.</span></span> <span data-ttu-id="eaecb-157">让我们更改该值。</span><span class="sxs-lookup"><span data-stu-id="eaecb-157">Let's change that value.</span></span>

### <a name="change-cache-settings-of-new-data-disk"></a><span data-ttu-id="eaecb-158">更改新数据磁盘的缓存设置</span><span class="sxs-lookup"><span data-stu-id="eaecb-158">Change cache settings of new data disk</span></span>

1. <span data-ttu-id="eaecb-159">我们使用`Set-AzVMDataDisk` cmdlet 修改虚拟机数据磁盘的属性, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="eaecb-159">We modify properties of a virtual machine data disk with the `Set-AzVMDataDisk` cmdlet, as follows:</span></span>

    ```powershell
    Set-AzVMDataDisk -VM $myVM -Lun "1" -Caching ReadWrite
    ```
    
1. <span data-ttu-id="eaecb-160">与往常一样, 要提交更改`Update-AzVM`, 请执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="eaecb-160">As always, commit the changes with `Update-AzVM`:</span></span>

    ```powershell
    Update-AzVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
<span data-ttu-id="eaecb-161">以下是我们在此练习中已完成的操作的门户视图。</span><span class="sxs-lookup"><span data-stu-id="eaecb-161">Here's a view from the portal of what we've accomplished in this exercise.</span></span> <span data-ttu-id="eaecb-162">我们的 VM 现在有两个数据磁盘, 并且我们调整了所有**主机缓存**设置。</span><span class="sxs-lookup"><span data-stu-id="eaecb-162">Our VM now has two data disks, and we've adjusted all **HOST CACHING** settings.</span></span> <span data-ttu-id="eaecb-163">我们只需几个命令即可完成所有这些操作。</span><span class="sxs-lookup"><span data-stu-id="eaecb-163">We did all of that with just a few commands.</span></span> <span data-ttu-id="eaecb-164">这就是 Azure PowerShell 的强大功能。</span><span class="sxs-lookup"><span data-stu-id="eaecb-164">That's the power of Azure PowerShell.</span></span>

![显示包含两个数据磁盘的 VM 刀片磁盘部分的 Azure 门户屏幕截图。](../media/disks-final-config-portal2.png)
