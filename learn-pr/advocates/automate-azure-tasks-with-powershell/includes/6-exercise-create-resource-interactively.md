<span data-ttu-id="92dd4-101">回想一下我们的原始方案-创建虚拟机以测试我们的 CRM 软件。</span><span class="sxs-lookup"><span data-stu-id="92dd4-101">Recall our original scenario - creating VMs to test our CRM software.</span></span> <span data-ttu-id="92dd4-102">当有新的内部版本时, 我们想要加速新的 VM, 以便我们可以从干净的映像测试完整的安装体验。</span><span class="sxs-lookup"><span data-stu-id="92dd4-102">When a new build is available, we want to spin up a new VM so we can test the full install experience from a clean image.</span></span> <span data-ttu-id="92dd4-103">完成后, 我们想要删除 VM。</span><span class="sxs-lookup"><span data-stu-id="92dd4-103">Then when we are finished, we want to delete the VM.</span></span>

<span data-ttu-id="92dd4-104">让我们尝试用于创建 VM 的命令。</span><span class="sxs-lookup"><span data-stu-id="92dd4-104">Let's try the commands you would use to create a VM.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm-with-azure-powershell"></a><span data-ttu-id="92dd4-105">使用 Azure PowerShell 创建 Linux VM</span><span class="sxs-lookup"><span data-stu-id="92dd4-105">Create a Linux VM with Azure PowerShell</span></span>

<span data-ttu-id="92dd4-106">由于我们使用的是 Azure 沙箱, 因此您无需创建资源组。</span><span class="sxs-lookup"><span data-stu-id="92dd4-106">Since we are using the Azure sandbox, you won't have to create a Resource Group.</span></span> <span data-ttu-id="92dd4-107">请改为使用资源组**<rgn>[沙盒资源组名称]</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="92dd4-107">Instead, use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span> <span data-ttu-id="92dd4-108">此外, 请注意位置限制。</span><span class="sxs-lookup"><span data-stu-id="92dd4-108">In addition, be aware of the location restrictions.</span></span>

<span data-ttu-id="92dd4-109">让我们使用 PowerShell 创建新的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="92dd4-109">Let's create a new Azure VM with PowerShell.</span></span>

1. <span data-ttu-id="92dd4-110">使用`New-AzVm` cmdlet 创建 VM。</span><span class="sxs-lookup"><span data-stu-id="92dd4-110">Use the `New-AzVm` cmdlet to create a VM.</span></span>
    - <span data-ttu-id="92dd4-111">使用 "资源组**<rgn>[沙盒资源组名称]</rgn>**"。</span><span class="sxs-lookup"><span data-stu-id="92dd4-111">Use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span>
    - <span data-ttu-id="92dd4-112">为 vm 提供一个名称, 通常是您希望使用一些有意义的内容, 用于标识 vm、位置以及 (如果有多个) 实例号的用途。</span><span class="sxs-lookup"><span data-stu-id="92dd4-112">Give the VM a name - typically you want to use something meaningful that identifies the purposes of the VM, location, and (if there is more than one) instance number.</span></span> <span data-ttu-id="92dd4-113">我们将使用 "testvm-eus-01" 作为 "与我们联系, instance 1" 中的 "测试虚拟机"。</span><span class="sxs-lookup"><span data-stu-id="92dd4-113">We'll use "testvm-eus-01" for "Test VM in East US, instance 1".</span></span> <span data-ttu-id="92dd4-114">根据你放置虚拟机的位置提供你自己的名称。</span><span class="sxs-lookup"><span data-stu-id="92dd4-114">Come up with your own name based on where you place the VM.</span></span>
    - <span data-ttu-id="92dd4-115">从 Azure 沙箱中提供的以下列表中选择一个与你接近的位置。</span><span class="sxs-lookup"><span data-stu-id="92dd4-115">Select a location close to you from the following list available in the Azure sandbox.</span></span> <span data-ttu-id="92dd4-116">如果使用复制和粘贴, 请务必更改以下示例命令中的值。</span><span class="sxs-lookup"><span data-stu-id="92dd4-116">Make sure to change the value in the below example command if you are using copy and paste.</span></span>

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - <span data-ttu-id="92dd4-117">对图像使用 "UbuntuLTS"-这是 Ubuntu Linux。</span><span class="sxs-lookup"><span data-stu-id="92dd4-117">Use "UbuntuLTS" for the image - this is Ubuntu Linux.</span></span>
    - <span data-ttu-id="92dd4-118">使用`Get-Credential` cmdlet 并将结果输送到`Credential`参数中。</span><span class="sxs-lookup"><span data-stu-id="92dd4-118">Use the `Get-Credential` cmdlet and feed the results into the `Credential` parameter.</span></span>
      > [!IMPORTANT]
      > <span data-ttu-id="92dd4-119">有关用户名和密码限制, 请参阅[Linux VM 常见问题解答](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="92dd4-119">Please see the [Linux VM FAQ](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm?azure-portal=true) for username and password limitations.</span></span> <span data-ttu-id="92dd4-120">密码长度必须为 12-123 个字符, 并满足以下4个复杂性要求中的3个:</span><span class="sxs-lookup"><span data-stu-id="92dd4-120">Passwords must be 12 - 123 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>
      > - <span data-ttu-id="92dd4-121">包含较少字符</span><span class="sxs-lookup"><span data-stu-id="92dd4-121">Have lower characters</span></span>
      > - <span data-ttu-id="92dd4-122">包含大写字符</span><span class="sxs-lookup"><span data-stu-id="92dd4-122">Have upper characters</span></span>
      > - <span data-ttu-id="92dd4-123">有一个数字</span><span class="sxs-lookup"><span data-stu-id="92dd4-123">Have a digit</span></span>
      > - <span data-ttu-id="92dd4-124">包含特殊字符 (正则表达式匹配 [\W_])</span><span class="sxs-lookup"><span data-stu-id="92dd4-124">Have a special character (Regex match [\W_])</span></span>
    - <span data-ttu-id="92dd4-125">添加`-OpenPorts`参数并将 "22" 作为端口传递, 这将使我们成为此计算机的 SSH。</span><span class="sxs-lookup"><span data-stu-id="92dd4-125">Add the `-OpenPorts` parameter and pass "22" as the port - this will let us SSH into the machine.</span></span>
 
    ```powershell
    New-AzVm -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image UbuntuLTS -OpenPorts 22
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
    
1. <span data-ttu-id="92dd4-126">这将需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="92dd4-126">This will take a few minutes to complete.</span></span> <span data-ttu-id="92dd4-127">完成后, 可以对其进行查询, 并将 VM 对象分配给变量 (`$vm`)。</span><span class="sxs-lookup"><span data-stu-id="92dd4-127">Once it does, you can query it and assign the VM object to a variable (`$vm`).</span></span>

    ```powershell
    $vm = Get-AzVM -Name "testvm-eus-01" -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```
    
1. <span data-ttu-id="92dd4-128">然后查询值, 以转储有关 VM 的信息:</span><span class="sxs-lookup"><span data-stu-id="92dd4-128">Then query the value to dump out the information about the VM:</span></span>

    ```powershell
    $vm
    ```

    <span data-ttu-id="92dd4-129">您应该会看到类似这样的内容:</span><span class="sxs-lookup"><span data-stu-id="92dd4-129">You should see something like:</span></span>

    ```powershell
    ResourceGroupName : <rgn>[sandbox resource group name]</rgn>
    Id                : /subscriptions/xxxxxxxx-xxxx-aaaa-bbbb-cccccccccccc/resourceGroups/<rgn>[sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/testvm-eus-01
    VmId              : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    Name              : testvm-eus-01
    Type              : Microsoft.Compute/virtualMachines
    Location          : eastus
    Tags              : {}
    HardwareProfile   : {VmSize}
    NetworkProfile    : {NetworkInterfaces}
    OSProfile         : {ComputerName, AdminUsername, LinuxConfiguration, Secrets}
    ProvisioningState : Succeeded
    StorageProfile    : {ImageReference, OsDisk, DataDisks}
    ```
    
1. <span data-ttu-id="92dd4-130">您可以通过点 (".") 语法进入复杂对象。</span><span class="sxs-lookup"><span data-stu-id="92dd4-130">You can reach into complex objects through a dot (".") syntax.</span></span> <span data-ttu-id="92dd4-131">例如, 若要查看与 HardwareProfile 节相关`VMSize`联的对象中的属性, 您可以键入:</span><span class="sxs-lookup"><span data-stu-id="92dd4-131">For example, to see the properties in the `VMSize` object associated with the HardwareProfile section you can type:</span></span>

    ```powershell
    $vm.HardwareProfile
    ```

1. <span data-ttu-id="92dd4-132">若要获取其中一个磁盘的信息, 请执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="92dd4-132">Or to get information on one of the disks:</span></span>

    ```powershell
    $vm.StorageProfile.OsDisk
    ```

1. <span data-ttu-id="92dd4-133">您甚至可以将 VM 对象传递到其他 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="92dd4-133">You can even pass the VM object into other cmdlets.</span></span> <span data-ttu-id="92dd4-134">例如, 这将检索 VM 的公共 IP 地址:</span><span class="sxs-lookup"><span data-stu-id="92dd4-134">For example, this will retrieve the public IP address of your VM:</span></span>

    ```powershell
    $vm | Get-AzPublicIpAddress
    ```

1. <span data-ttu-id="92dd4-135">使用 IP 地址, 你可以使用 SSH 连接到 VM。</span><span class="sxs-lookup"><span data-stu-id="92dd4-135">With the IP address, you can connect to the VM with SSH.</span></span> <span data-ttu-id="92dd4-136">例如, 如果您使用用户名 "bob", 并且 IP 地址为 "205.22.16.5", 则此命令将连接到 Linux 计算机:</span><span class="sxs-lookup"><span data-stu-id="92dd4-136">For example, if you used the username "bob", and the IP address is "205.22.16.5", then this command would connect to the Linux machine:</span></span>

    ```powershell
    ssh bob@205.22.16.5
    ```

    <span data-ttu-id="92dd4-137">通过键入`exit`来继续执行并注销。</span><span class="sxs-lookup"><span data-stu-id="92dd4-137">Go ahead and log out by typing `exit`.</span></span>


## <a name="delete-a-vm"></a><span data-ttu-id="92dd4-138">删除 VM</span><span class="sxs-lookup"><span data-stu-id="92dd4-138">Delete a VM</span></span>

<span data-ttu-id="92dd4-139">只需尝试一些更多命令, 让我们删除 VM。</span><span class="sxs-lookup"><span data-stu-id="92dd4-139">Just to try out some more commands, let's delete the VM.</span></span> <span data-ttu-id="92dd4-140">我们将首先将其关闭。</span><span class="sxs-lookup"><span data-stu-id="92dd4-140">We'll shut it down first.</span></span>

```powershell
Stop-AzVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

<span data-ttu-id="92dd4-141">现在, 让我们使用`Remove-AzVM` cmdlet 删除 VM:</span><span class="sxs-lookup"><span data-stu-id="92dd4-141">Now, let's delete the VM with the `Remove-AzVM` cmdlet:</span></span>

```powershell
Remove-AzVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

<span data-ttu-id="92dd4-142">尝试此命令列出资源组中的所有资源:</span><span class="sxs-lookup"><span data-stu-id="92dd4-142">Try this command to list all the resources in your resource group:</span></span>

```powershell
Get-AzResource -ResourceGroupName $vm.ResourceGroupName | ft
```

<span data-ttu-id="92dd4-143">您应该会看到所有仍然存在的资源组 (磁盘、虚拟网络等)。</span><span class="sxs-lookup"><span data-stu-id="92dd4-143">You should see a bunch of resources (disks, virtual networks, etc.) that all still exist.</span></span> 

```output
Microsoft.Compute/disks
Microsoft.Network/networkInterfaces
Microsoft.Network/networkSecurityGroups
Microsoft.Network/publicIPAddresses
Microsoft.Network/virtualNetworks
```

<span data-ttu-id="92dd4-144">这是因为`Remove-AzVM`命令_仅删除了 VM_。</span><span class="sxs-lookup"><span data-stu-id="92dd4-144">This is because the `Remove-AzVM` command _just deletes the VM_.</span></span> <span data-ttu-id="92dd4-145">它不会清除任何其他资源!</span><span class="sxs-lookup"><span data-stu-id="92dd4-145">It doesn't cleanup any of the other resources!</span></span> <span data-ttu-id="92dd4-146">在这种情况下, 我们很可能只是删除资源组本身并使用它完成。</span><span class="sxs-lookup"><span data-stu-id="92dd4-146">At this point, we'd likely just delete the Resource Group itself and be done with it.</span></span> <span data-ttu-id="92dd4-147">不过, 我们只需运行练习, 即可手动对其进行清理。</span><span class="sxs-lookup"><span data-stu-id="92dd4-147">However, let's just run through the exercise to clean it up manually.</span></span> <span data-ttu-id="92dd4-148">您应该会在命令中看到模式。</span><span class="sxs-lookup"><span data-stu-id="92dd4-148">You should see a pattern in the commands.</span></span>

1. <span data-ttu-id="92dd4-149">删除网络接口。</span><span class="sxs-lookup"><span data-stu-id="92dd4-149">Delete the Network Interface.</span></span>

    ```powershell
    $vm | Remove-AzNetworkInterface –Force
    ```
    
1. <span data-ttu-id="92dd4-150">删除托管 OS 磁盘和存储帐户</span><span class="sxs-lookup"><span data-stu-id="92dd4-150">Delete the managed OS disks and storage account</span></span>

    ```powershell
    Get-AzDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzDisk -Force
    ```

1. <span data-ttu-id="92dd4-151">接下来, 删除虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="92dd4-151">Next, delete the virtual network.</span></span>

    ```powershell
    Get-AzVirtualNetwork -ResourceGroup $vm.ResourceGroupName | Remove-AzVirtualNetwork -Force
    ```

1. <span data-ttu-id="92dd4-152">删除网络安全组。</span><span class="sxs-lookup"><span data-stu-id="92dd4-152">Delete the network security group.</span></span>

    ```powershell
    Get-AzNetworkSecurityGroup -ResourceGroup $vm.ResourceGroupName | Remove-AzNetworkSecurityGroup -Force
    ```

1. <span data-ttu-id="92dd4-153">最后是公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="92dd4-153">And finally, the public IP address.</span></span>

    ```powershell
    Get-AzPublicIpAddress -ResourceGroup $vm.ResourceGroupName | Remove-AzPublicIpAddress -Force
    ```

<span data-ttu-id="92dd4-154">我们应该已捕获所有创建的资源;请检查资源组, 以确保。</span><span class="sxs-lookup"><span data-stu-id="92dd4-154">We should have caught all the created resources; check the resource group just to be sure.</span></span> <span data-ttu-id="92dd4-155">我们在此处执行了许多手动命令, 但更好的方法是编写一个_脚本_, 以便以后可以重用此逻辑来创建或删除 VM。</span><span class="sxs-lookup"><span data-stu-id="92dd4-155">We did a lot of manual commands here but a better approach would have been to write a _script_ so we could reuse this logic later to create or delete a VM.</span></span> <span data-ttu-id="92dd4-156">让我们来看一下使用 PowerShell 编写脚本。</span><span class="sxs-lookup"><span data-stu-id="92dd4-156">Let's look at scripting with PowerShell.</span></span>