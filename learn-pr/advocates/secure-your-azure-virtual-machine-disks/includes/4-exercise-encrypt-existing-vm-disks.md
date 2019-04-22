假设您正在开发一个用于新的商业起步的财务管理应用程序。 您希望确保所有客户的数据都是安全的, 因此您已决定在将承载此应用程序的服务器上的所有 OS 和数据磁盘中实施 Azure 磁盘加密 (ADE)。 作为合规性要求的一部分, 您还需要负责自己的加密密钥管理。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

在此单元中, 你将对现有虚拟机上的磁盘进行加密, 并使用你自己的 Azure 密钥保管库管理加密密钥。

## <a name="prepare-the-environment"></a>准备环境

我们将首先在 Azure 虚拟机中部署新的 Windows VM。

### <a name="deploy-windows-vm"></a>部署 Windows VM

使用 Azure PowerShell 创建和部署新的 Windows 虚拟机。

1. 首先, 决定放置新资源的位置。 从以下列表中选择邻近你的位置。

    <!-- Resource selection -->  
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]
    

1. 定义用于保存所选位置的 PowerShell 变量。 它在此处定义为 "东 US", 将其更改为你的首选位置。

    ```powershell
    $location = "eastus"
    ```
    
    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. 接下来, 定义一些更方便的变量, 以捕获 VM 和_资源组_的_名称_。 请注意, 我们在此处使用的是预先创建的资源组, 通常您会__ 使用`New-AzResourceGroup`在订阅中创建新的资源组。

    ```powershell
    $vmName = "fmdata-vm01"
    $rgName = "<rgn>[sandbox Resource Group]</rgn>"
    ```
    
1. 用于`New-AzVm`创建新的虚拟机。
    
    ```powershell
    New-AzVm `
        -ResourceGroupName $rgName `
        -Name $vmName `
        -Location $location `
        -OpenPorts 3389
    ```
    
    当你由云命令行管理程序提示时, 请输入 VM 的用户名和密码。 此帐户将用作为 VM 创建的初始帐户。
    
    > [!NOTE]
    > 此命令将使用一些默认值, 因为我们没有提供一组选项。 具体来说, 这将创建一个大小为_Standard_DS1_v2_的_Windows 2016 服务器_映像。 请注意, 如果您决定指定 VM 大小, 则基本层虚拟机不支持 ADE。

1. 虚拟机部署完成后, 在变量中捕获 vm 详细信息。 您可以使用此变量来浏览所创建的内容。

    ```powershell
    $vm = Get-AzVM -Name $vmName -ResourceGroupName $rgName
    ```
    
1. 您可以看到挂接到 VM 的 OS 磁盘:

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
        
1. 检查 OS 磁盘 (和所有数据磁盘) 上的当前加密状态。

    ```powershell
    Get-AzVmDiskEncryptionStatus  `
        -ResourceGroupName $rgName `
        -VMName $vmName
    ```

    您可以看到, 磁盘当前_未加密_。 

    ```output
    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : NotEncrypted
    OsVolumeEncryptionSettings :
    ProgressMessage            : No Encryption extension or metadata found on the VM
    ```
    
让我们对此进行更改。
    
## <a name="encrypt-the-vm-disks-with-azure-disk-encryption"></a>使用 Azure 磁盘加密对虚拟机磁盘进行加密

我们需要保护此数据, 让我们对磁盘进行加密。 请注意, 需要执行以下几个步骤:

1. 创建一个密钥存储库。
1. 将主要电子仓库设置为支持磁盘加密。
1. 通知 Azure 使用存储在密钥保管库中的密钥对虚拟机磁盘进行加密。

> [!TIP]
> 我们将逐个完成这些步骤, 但在您自己的订阅中执行此任务时, 可以使用此模块的摘要中链接的便利 PowerShell 脚本。

### <a name="create-a-key-vault"></a>创建密钥存储库

若要创建 Azure 密钥存储库, 我们需要在订阅中启用该服务。 这是一个一次性要求。

> [!TIP]
> 根据你的订阅, 你可能需要使用`Register-AzResourceProvider` cmdlet 启用**KeyVault**提供程序。 这在 Azure 沙盒订阅中不是必需的。

1. 确定新密钥存储库的名称。 它必须是唯一的, 并且可以是3到24个字符, 由数字、字母和短划线组成。 请尝试将一些随机号码添加到末尾, 并替换下面的 "1234"。

    ```powershell
    $keyVaultName = "mvmdsk-kv-1234"
    ```
        
1. 使用`New-AzKeyVault`创建 Azure Key Vault。
    - 确保它与你的 VM 放在同一资源组_和_位置。
    - 启用用于磁盘加密的密钥存储库。 
    - 指定唯一的密钥电子仓库名称。

    ```powershell
    New-AzKeyVault -VaultName $keyVaultName `
        -Location $location `
        -ResourceGroupName $rgName `
        -EnabledForDiskEncryption
    ```

    您将在此命令中收到一条关于没有用户拥有访问权限的警告。

    ```output
    WARNING: Access policy is not set. No user or application have access permission to use this vault. This can happen if the vault was created by a service principal. Please use Set-AzKeyVaultAccessPolicy to set access policies.
    ```

    这是正常的, 因为我们只是使用保管库来存储 VM 的加密密钥, 用户无需访问此数据。

### <a name="encrypt-the-disk"></a>加密磁盘

我们已准备好对磁盘进行加密。 在执行此操作之前, 请先创建备份的相关警告。

> [!IMPORTANT]
> 如果这是生产系统, 我们需要执行托管磁盘的备份 (使用 Azure 备份) 或创建快照。 您可以在 Azure 门户中或通过命令行创建快照。 在 PowerShell 中, 使用`New-AzSnapshot` cmdlet。 由于这是一个简单的练习, 我们将在你完成后将此数据扔掉, 我们将跳过此步骤。 

1. 首先定义一个变量以保存密钥存储库信息。

    ```powershell
    $keyVault = Get-AzKeyVault `
        -VaultName $keyVaultName `
        -ResourceGroupName $rgName
    ```

1. 然后, 使用`Set-AzVmDiskEncryptionExtension` cmdlet 对虚拟机磁盘进行加密。
    - 此`VolumeType`参数允许您指定要加密的磁盘: [_所有_ | _OS_ | _数据_]。 它将默认为 "_全部_"。 您只能对某些 linux 分布的数据磁盘进行加密。
    - 您必须提供托管磁盘`SkipVmBackup`的标志, 否则命令将失败, 因为没有快照。

    ```powershell
    Set-AzVmDiskEncryptionExtension `
        -ResourceGroupName $rgName `
        -VMName $vmName `
        -VolumeType All `
        -DiskEncryptionKeyVaultId $keyVault.ResourceId `
        -DiskEncryptionKeyVaultUrl $keyVault.VaultUri `
        -SkipVmBackup
    ```

1. cmdlet 将警告您 VM 必须脱机, 并且该任务可能需要几分钟才能完成。 继续操作, 让它继续运行。

    ```output
    Enable AzureDiskEncryption on the VM
    This cmdlet prepares the VM and enables encryption which may reboot the machine and takes 10-15 minutes to
    finish. Please save your work on the VM before confirming. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
    ```
    
1. 完成后, 再次检查加密状态。

    ```powershell
    Get-AzVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
    ```

    现在应对 OS 磁盘进行加密。 对 Windows 可见的任何附加数据磁盘也将进行加密。

    ```output
    OsVolumeEncrypted          : Encrypted
    DataVolumesEncrypted       : NoDiskFound
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : Provisioning succeeded
    ```

> [!NOTE]        
> 加密之后添加的新磁盘_不_会自动加密。 您可以重新运行`Set-AzVMDiskEncryptionExtension` cmdlet 以加密新磁盘。 如果将磁盘添加到已加密磁盘的虚拟机, 请确保提供新的序列号。 此外, 不会加密对操作系统不可见的磁盘-必须对磁盘进行正确的分区、格式化和装入, 才能由 Bitlocker 扩展进行查看。
