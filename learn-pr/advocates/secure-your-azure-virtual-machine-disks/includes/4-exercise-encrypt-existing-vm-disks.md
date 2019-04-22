<span data-ttu-id="c13ce-101">假设您正在开发一个用于新的商业起步的财务管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="c13ce-101">Suppose you are developing a financial management application for new business startups.</span></span> <span data-ttu-id="c13ce-102">您希望确保所有客户的数据都是安全的, 因此您已决定在将承载此应用程序的服务器上的所有 OS 和数据磁盘中实施 Azure 磁盘加密 (ADE)。</span><span class="sxs-lookup"><span data-stu-id="c13ce-102">You want to ensure that all your customers' data is secured, so you have decided to implement Azure Disk Encryption (ADE) across all OS and data disks on the servers that will host this application.</span></span> <span data-ttu-id="c13ce-103">作为合规性要求的一部分, 您还需要负责自己的加密密钥管理。</span><span class="sxs-lookup"><span data-stu-id="c13ce-103">As part of your compliance requirements, you also need to be responsible for your own encryption key management.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="c13ce-104">在此单元中, 你将对现有虚拟机上的磁盘进行加密, 并使用你自己的 Azure 密钥保管库管理加密密钥。</span><span class="sxs-lookup"><span data-stu-id="c13ce-104">In this unit, you'll encrypt disks on an existing virtual machine, and manage the encryption keys using your own Azure Key Vault.</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="c13ce-105">准备环境</span><span class="sxs-lookup"><span data-stu-id="c13ce-105">Prepare the environment</span></span>

<span data-ttu-id="c13ce-106">我们将首先在 Azure 虚拟机中部署新的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="c13ce-106">We'll start by deploying a new Windows VM in an Azure Virtual Machine.</span></span>

### <a name="deploy-windows-vm"></a><span data-ttu-id="c13ce-107">部署 Windows VM</span><span class="sxs-lookup"><span data-stu-id="c13ce-107">Deploy Windows VM</span></span>

<span data-ttu-id="c13ce-108">使用 Azure PowerShell 创建和部署新的 Windows 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c13ce-108">Use the Azure PowerShell to create and deploy a new Windows virtual machine.</span></span>

1. <span data-ttu-id="c13ce-109">首先, 决定放置新资源的位置。</span><span class="sxs-lookup"><span data-stu-id="c13ce-109">Start by deciding where to place the new resources.</span></span> <span data-ttu-id="c13ce-110">从以下列表中选择邻近你的位置。</span><span class="sxs-lookup"><span data-stu-id="c13ce-110">Select a location near you from the following list.</span></span>

    <!-- Resource selection -->  
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]
    

1. <span data-ttu-id="c13ce-111">定义用于保存所选位置的 PowerShell 变量。</span><span class="sxs-lookup"><span data-stu-id="c13ce-111">Define a PowerShell variable to hold the selected location.</span></span> <span data-ttu-id="c13ce-112">它在此处定义为 "东 US", 将其更改为你的首选位置。</span><span class="sxs-lookup"><span data-stu-id="c13ce-112">It's defined as "East US" here, change it to your preferred location.</span></span>

    ```powershell
    $location = "eastus"
    ```
    
    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="c13ce-113">接下来, 定义一些更方便的变量, 以捕获 VM 和_资源组_的_名称_。</span><span class="sxs-lookup"><span data-stu-id="c13ce-113">Next, define a few more convenient variables to capture the _name_ of the VM and the _resource group_.</span></span> <span data-ttu-id="c13ce-114">请注意, 我们在此处使用的是预先创建的资源组, 通常您会__ 使用`New-AzResourceGroup`在订阅中创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="c13ce-114">Note that we are using the pre-created resource group here, normally you would create a _new_ resource group in your subscription using `New-AzResourceGroup`.</span></span>

    ```powershell
    $vmName = "fmdata-vm01"
    $rgName = "<rgn>[sandbox Resource Group]</rgn>"
    ```
    
1. <span data-ttu-id="c13ce-115">用于`New-AzVm`创建新的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c13ce-115">Use `New-AzVm` to create a new virtual machine.</span></span>
    
    ```powershell
    New-AzVm `
        -ResourceGroupName $rgName `
        -Name $vmName `
        -Location $location `
        -OpenPorts 3389
    ```
    
    <span data-ttu-id="c13ce-116">当你由云命令行管理程序提示时, 请输入 VM 的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="c13ce-116">Enter a username and password for the VM when you are prompted by the Cloud Shell.</span></span> <span data-ttu-id="c13ce-117">此帐户将用作为 VM 创建的初始帐户。</span><span class="sxs-lookup"><span data-stu-id="c13ce-117">This will be used as the initial account created for the VM.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c13ce-118">此命令将使用一些默认值, 因为我们没有提供一组选项。</span><span class="sxs-lookup"><span data-stu-id="c13ce-118">This command will use some defaults since we didn't supply a bunch of options.</span></span> <span data-ttu-id="c13ce-119">具体来说, 这将创建一个大小为_Standard_DS1_v2_的_Windows 2016 服务器_映像。</span><span class="sxs-lookup"><span data-stu-id="c13ce-119">Specifically, this will create a _Windows 2016 Server_ image with the size to _Standard_DS1_v2_.</span></span> <span data-ttu-id="c13ce-120">请注意, 如果您决定指定 VM 大小, 则基本层虚拟机不支持 ADE。</span><span class="sxs-lookup"><span data-stu-id="c13ce-120">Remember that the Basic tier VMs do not support ADE if you decide to specify the VM size.</span></span>

1. <span data-ttu-id="c13ce-121">虚拟机部署完成后, 在变量中捕获 vm 详细信息。</span><span class="sxs-lookup"><span data-stu-id="c13ce-121">Once the VM finishes deploying, capture the VM details in a variable.</span></span> <span data-ttu-id="c13ce-122">您可以使用此变量来浏览所创建的内容。</span><span class="sxs-lookup"><span data-stu-id="c13ce-122">You can use this variable to explore what was created.</span></span>

    ```powershell
    $vm = Get-AzVM -Name $vmName -ResourceGroupName $rgName
    ```
    
1. <span data-ttu-id="c13ce-123">您可以看到挂接到 VM 的 OS 磁盘:</span><span class="sxs-lookup"><span data-stu-id="c13ce-123">You can see the OS disk attached to the VM:</span></span>

    ```powershell
    $vm.StorageProfile.OSDisk
    ```

    ```output
    OsType                  : Windows
    EncryptionSettings      :
    Name                    : fmdata-vm01_OsDisk_1_6bcf8dcd49794aa785bad45221ec4433
    Vhd                     :
    Image                   :
    Caching                 : ReadWrite
    WriteAcceleratorEnabled :
    CreateOption            : FromImage
    DiskSizeGB              : 127
    ManagedDisk             : Microsoft.Azure.Management.Compute.Models.ManagedDiskP
                              arameters
    ```
        
1. <span data-ttu-id="c13ce-124">检查 OS 磁盘 (和所有数据磁盘) 上的当前加密状态。</span><span class="sxs-lookup"><span data-stu-id="c13ce-124">Check the current status of encryption on the OS disk (and any data disks).</span></span>

    ```powershell
    Get-AzVmDiskEncryptionStatus  `
        -ResourceGroupName $rgName `
        -VMName $vmName
    ```

    <span data-ttu-id="c13ce-125">您可以看到, 磁盘当前_未加密_。</span><span class="sxs-lookup"><span data-stu-id="c13ce-125">As you can see the disks are current _unencrypted_.</span></span> 

    ```output
    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : NotEncrypted
    OsVolumeEncryptionSettings :
    ProgressMessage            : No Encryption extension or metadata found on the VM
    ```
    
<span data-ttu-id="c13ce-126">让我们对此进行更改。</span><span class="sxs-lookup"><span data-stu-id="c13ce-126">Let's change that.</span></span>
    
## <a name="encrypt-the-vm-disks-with-azure-disk-encryption"></a><span data-ttu-id="c13ce-127">使用 Azure 磁盘加密对虚拟机磁盘进行加密</span><span class="sxs-lookup"><span data-stu-id="c13ce-127">Encrypt the VM disks with Azure Disk Encryption</span></span>

<span data-ttu-id="c13ce-128">我们需要保护此数据, 让我们对磁盘进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-128">We need to protect this data, so let's encrypt the disks.</span></span> <span data-ttu-id="c13ce-129">请注意, 需要执行以下几个步骤:</span><span class="sxs-lookup"><span data-stu-id="c13ce-129">Recall that there are several steps we need to perform:</span></span>

1. <span data-ttu-id="c13ce-130">创建一个密钥存储库。</span><span class="sxs-lookup"><span data-stu-id="c13ce-130">Create a key vault.</span></span>
1. <span data-ttu-id="c13ce-131">将主要电子仓库设置为支持磁盘加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-131">Set the key vault up to support disk encryption.</span></span>
1. <span data-ttu-id="c13ce-132">通知 Azure 使用存储在密钥保管库中的密钥对虚拟机磁盘进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-132">Tell Azure to encrypt the VM disks using the key stored in the Key Vault.</span></span>

> [!TIP]
> <span data-ttu-id="c13ce-133">我们将逐个完成这些步骤, 但在您自己的订阅中执行此任务时, 可以使用此模块的摘要中链接的便利 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="c13ce-133">We're going to walk through the steps individually, but when you're doing this task in your own subscription, you can use a handy PowerShell script which is linked in the Summary of this module.</span></span>

### <a name="create-a-key-vault"></a><span data-ttu-id="c13ce-134">创建密钥存储库</span><span class="sxs-lookup"><span data-stu-id="c13ce-134">Create a key vault</span></span>

<span data-ttu-id="c13ce-135">若要创建 Azure 密钥存储库, 我们需要在订阅中启用该服务。</span><span class="sxs-lookup"><span data-stu-id="c13ce-135">To create an Azure Key Vault, we need to enable the service in our subscription.</span></span> <span data-ttu-id="c13ce-136">这是一个一次性要求。</span><span class="sxs-lookup"><span data-stu-id="c13ce-136">This is a one-time requirement.</span></span>

> [!TIP]
> <span data-ttu-id="c13ce-137">根据你的订阅, 你可能需要使用`Register-AzResourceProvider` cmdlet 启用**KeyVault**提供程序。</span><span class="sxs-lookup"><span data-stu-id="c13ce-137">Depending on your subscription, you might need to enable the **Microsoft.KeyVault** provider with the `Register-AzResourceProvider` cmdlet.</span></span> <span data-ttu-id="c13ce-138">这在 Azure 沙盒订阅中不是必需的。</span><span class="sxs-lookup"><span data-stu-id="c13ce-138">This is not necessary in the Azure sandbox subscription.</span></span>

1. <span data-ttu-id="c13ce-139">确定新密钥存储库的名称。</span><span class="sxs-lookup"><span data-stu-id="c13ce-139">Decide on a name for your new key vault.</span></span> <span data-ttu-id="c13ce-140">它必须是唯一的, 并且可以是3到24个字符, 由数字、字母和短划线组成。</span><span class="sxs-lookup"><span data-stu-id="c13ce-140">It must be unique and can be between 3 and 24 characters, composed of numbers, letters, and and dashes.</span></span> <span data-ttu-id="c13ce-141">请尝试将一些随机号码添加到末尾, 并替换下面的 "1234"。</span><span class="sxs-lookup"><span data-stu-id="c13ce-141">Try adding some random numbers to the end, replacing the "1234" below.</span></span>

    ```powershell
    $keyVaultName = "mvmdsk-kv-1234"
    ```
        
1. <span data-ttu-id="c13ce-142">使用`New-AzKeyVault`创建 Azure Key Vault。</span><span class="sxs-lookup"><span data-stu-id="c13ce-142">Create an Azure Key Vault with `New-AzKeyVault`.</span></span>
    - <span data-ttu-id="c13ce-143">确保它与你的 VM 放在同一资源组_和_位置。</span><span class="sxs-lookup"><span data-stu-id="c13ce-143">Make sure it's placed in the same resource group _and_ location as your VM.</span></span>
    - <span data-ttu-id="c13ce-144">启用用于磁盘加密的密钥存储库。</span><span class="sxs-lookup"><span data-stu-id="c13ce-144">Enable the Key Vault for use with disk encryption.</span></span> 
    - <span data-ttu-id="c13ce-145">指定唯一的密钥电子仓库名称。</span><span class="sxs-lookup"><span data-stu-id="c13ce-145">Specify a unique Key Vault name.</span></span>

    ```powershell
    New-AzKeyVault -VaultName $keyVaultName `
        -Location $location `
        -ResourceGroupName $rgName `
        -EnabledForDiskEncryption
    ```

    <span data-ttu-id="c13ce-146">您将在此命令中收到一条关于没有用户拥有访问权限的警告。</span><span class="sxs-lookup"><span data-stu-id="c13ce-146">You will get a warning from this command about no users having access.</span></span>

    ```output
    WARNING: Access policy is not set. No user or application have access permission to use this vault. This can happen if the vault was created by a service principal. Please use Set-AzKeyVaultAccessPolicy to set access policies.
    ```

    <span data-ttu-id="c13ce-147">这是正常的, 因为我们只是使用保管库来存储 VM 的加密密钥, 用户无需访问此数据。</span><span class="sxs-lookup"><span data-stu-id="c13ce-147">This is ok since we are just using the vault to store the encryption keys for the VM and users won't need to access this data.</span></span>

### <a name="encrypt-the-disk"></a><span data-ttu-id="c13ce-148">加密磁盘</span><span class="sxs-lookup"><span data-stu-id="c13ce-148">Encrypt the disk</span></span>

<span data-ttu-id="c13ce-149">我们已准备好对磁盘进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-149">We are almost ready to encrypt the disks.</span></span> <span data-ttu-id="c13ce-150">在执行此操作之前, 请先创建备份的相关警告。</span><span class="sxs-lookup"><span data-stu-id="c13ce-150">Before we do, a warning about creating backups.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c13ce-151">如果这是生产系统, 我们需要执行托管磁盘的备份 (使用 Azure 备份) 或创建快照。</span><span class="sxs-lookup"><span data-stu-id="c13ce-151">If this were a production system, we would need to perform a backup of the managed disks - either using Azure Backup, or by creating a snapshot.</span></span> <span data-ttu-id="c13ce-152">您可以在 Azure 门户中或通过命令行创建快照。</span><span class="sxs-lookup"><span data-stu-id="c13ce-152">You can create snapshots in the Azure portal, or through the command line.</span></span> <span data-ttu-id="c13ce-153">在 PowerShell 中, 使用`New-AzSnapshot` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c13ce-153">In PowerShell, use the `New-AzSnapshot` cmdlet.</span></span> <span data-ttu-id="c13ce-154">由于这是一个简单的练习, 我们将在你完成后将此数据扔掉, 我们将跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="c13ce-154">Since this is a simple exercise and we're going to throw this data away when you're done, we're going to skip this step.</span></span> 

1. <span data-ttu-id="c13ce-155">首先定义一个变量以保存密钥存储库信息。</span><span class="sxs-lookup"><span data-stu-id="c13ce-155">Start by defining a variable to hold the Key Vault information.</span></span>

    ```powershell
    $keyVault = Get-AzKeyVault `
        -VaultName $keyVaultName `
        -ResourceGroupName $rgName
    ```

1. <span data-ttu-id="c13ce-156">然后, 使用`Set-AzVmDiskEncryptionExtension` cmdlet 对虚拟机磁盘进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-156">Then, use the `Set-AzVmDiskEncryptionExtension` cmdlet to encrypt the VM disks.</span></span>
    - <span data-ttu-id="c13ce-157">此`VolumeType`参数允许您指定要加密的磁盘: [_所有_ | _OS_ | _数据_]。</span><span class="sxs-lookup"><span data-stu-id="c13ce-157">The `VolumeType` parameter allows you to specify which disks to encrypt: [_All_ | _OS_ | _Data_].</span></span> <span data-ttu-id="c13ce-158">它将默认为 "_全部_"。</span><span class="sxs-lookup"><span data-stu-id="c13ce-158">It will default to _All_.</span></span> <span data-ttu-id="c13ce-159">您只能对某些 linux 分布的数据磁盘进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-159">You can only encrypt data disks for some distributions of Linux.</span></span>
    - <span data-ttu-id="c13ce-160">您必须提供托管磁盘`SkipVmBackup`的标志, 否则命令将失败, 因为没有快照。</span><span class="sxs-lookup"><span data-stu-id="c13ce-160">You have to supply the `SkipVmBackup` flag for managed disks or the command will fail because there is no snapshot.</span></span>

    ```powershell
    Set-AzVmDiskEncryptionExtension `
        -ResourceGroupName $rgName `
        -VMName $vmName `
        -VolumeType All `
        -DiskEncryptionKeyVaultId $keyVault.ResourceId `
        -DiskEncryptionKeyVaultUrl $keyVault.VaultUri `
        -SkipVmBackup
    ```

1. <span data-ttu-id="c13ce-161">cmdlet 将警告您 VM 必须脱机, 并且该任务可能需要几分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="c13ce-161">The cmdlet will warn you that the VM must be taken offline, and that the task may take several minutes to complete.</span></span> <span data-ttu-id="c13ce-162">继续操作, 让它继续运行。</span><span class="sxs-lookup"><span data-stu-id="c13ce-162">Go ahead and let it continue.</span></span>

    ```output
    Enable AzureDiskEncryption on the VM
    This cmdlet prepares the VM and enables encryption which may reboot the machine and takes 10-15 minutes to
    finish. Please save your work on the VM before confirming. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
    ```
    
1. <span data-ttu-id="c13ce-163">完成后, 再次检查加密状态。</span><span class="sxs-lookup"><span data-stu-id="c13ce-163">Once it's complete, check the encryption status again.</span></span>

    ```powershell
    Get-AzVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
    ```

    <span data-ttu-id="c13ce-164">现在应对 OS 磁盘进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-164">Now the OS disk should be encrypted.</span></span> <span data-ttu-id="c13ce-165">对 Windows 可见的任何附加数据磁盘也将进行加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-165">Any attached data disks that are visible to Windows will also be encrypted.</span></span>

    ```output
    OsVolumeEncrypted          : Encrypted
    DataVolumesEncrypted       : NoDiskFound
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : Provisioning succeeded
    ```

> [!NOTE]        
> <span data-ttu-id="c13ce-166">加密之后添加的新磁盘_不_会自动加密。</span><span class="sxs-lookup"><span data-stu-id="c13ce-166">New disks added after encryption will _not_ be automatically encrypted.</span></span> <span data-ttu-id="c13ce-167">您可以重新运行`Set-AzVMDiskEncryptionExtension` cmdlet 以加密新磁盘。</span><span class="sxs-lookup"><span data-stu-id="c13ce-167">You can re-run the `Set-AzVMDiskEncryptionExtension` cmdlet to encrypt new disks.</span></span> <span data-ttu-id="c13ce-168">如果将磁盘添加到已加密磁盘的虚拟机, 请确保提供新的序列号。</span><span class="sxs-lookup"><span data-stu-id="c13ce-168">Make sure to provide a new sequence number if you add disks to a VM that has already had disks encrypted.</span></span> <span data-ttu-id="c13ce-169">此外, 不会加密对操作系统不可见的磁盘-必须对磁盘进行正确的分区、格式化和装入, 才能由 Bitlocker 扩展进行查看。</span><span class="sxs-lookup"><span data-stu-id="c13ce-169">In addition, disks that are not visible to the operating system will not be encrypted - the disk must be properly partitioned, formatted, and mounted to be seen by the Bitlocker extension.</span></span>
