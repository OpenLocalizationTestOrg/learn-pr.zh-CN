<span data-ttu-id="0da67-101">假设您的公司已决定在所有虚拟机上实施 Azure 磁盘加密 (ADE)。</span><span class="sxs-lookup"><span data-stu-id="0da67-101">Suppose your company has decided to implement Azure Disk Encryption (ADE) across all VMs.</span></span> <span data-ttu-id="0da67-102">您需要评估如何将加密部署到现有的虚拟机卷。</span><span class="sxs-lookup"><span data-stu-id="0da67-102">You need to evaluate how to roll out encryption to existing VM volumes.</span></span> <span data-ttu-id="0da67-103">在这里, 我们将介绍 ADE 的要求, 以及在对现有 Linux 和 Windows 虚拟机加密磁盘时涉及的步骤。</span><span class="sxs-lookup"><span data-stu-id="0da67-103">Here, we'll look at the requirements for ADE, and the steps involved in encrypting disks on existing Linux and Windows VMs.</span></span>

## <a name="azure-disk-encryption-prerequisites"></a><span data-ttu-id="0da67-104">Azure 磁盘加密先决条件</span><span class="sxs-lookup"><span data-stu-id="0da67-104">Azure Disk Encryption prerequisites</span></span>

<span data-ttu-id="0da67-105">必须先执行以下操作, 然后才能对虚拟机磁盘进行加密:</span><span class="sxs-lookup"><span data-stu-id="0da67-105">Before you can encrypt your VM disks, you need to:</span></span>

1. <span data-ttu-id="0da67-106">创建一个密钥存储库。</span><span class="sxs-lookup"><span data-stu-id="0da67-106">Create a key vault.</span></span>
1. <span data-ttu-id="0da67-107">设置密钥存储库访问策略以支持磁盘加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-107">Set the key vault access policy to support disk encryption.</span></span>
1. <span data-ttu-id="0da67-108">使用密钥存储库存储 ADE 的加密密钥。</span><span class="sxs-lookup"><span data-stu-id="0da67-108">Use the key vault to store the encryption keys for ADE.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="0da67-109">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0da67-109">Azure Key Vault</span></span>

<span data-ttu-id="0da67-110">可将 ADE 使用的加密密钥存储在 Azure Key Vault 中。</span><span class="sxs-lookup"><span data-stu-id="0da67-110">The encryption keys used by ADE can be stored in Azure Key Vault.</span></span> <span data-ttu-id="0da67-111">Azure Key Vault 是一个用于安全存储和访问机密的工具。</span><span class="sxs-lookup"><span data-stu-id="0da67-111">Azure Key Vault is a tool for securely storing and accessing secrets.</span></span> <span data-ttu-id="0da67-112">密码是您想要严格控制其访问权限的任何内容, 如 API 密钥、密码或证书。</span><span class="sxs-lookup"><span data-stu-id="0da67-112">A secret is anything that you want to tightly control access to, such as API keys, passwords, or certificates.</span></span> <span data-ttu-id="0da67-113">这提供了高度可用且可扩展的安全存储, 如联邦信息处理标准 (FIPS) 140-2 第2级验证的硬件安全模块 (hsm) 中所定义。</span><span class="sxs-lookup"><span data-stu-id="0da67-113">This provides highly available and scalable secure storage, as defined in Federal Information Processing Standards (FIPS) 140-2 Level 2 validated Hardware Security Modules (HSMs).</span></span> <span data-ttu-id="0da67-114">使用密钥存储库可以保持对用于加密数据的密钥的完全控制, 并且可以管理和审核密钥用法。</span><span class="sxs-lookup"><span data-stu-id="0da67-114">Using Key Vault, you keep full control of the keys used to encrypt your data, and you can manage and audit your key usage.</span></span> 

> [!NOTE]
> <span data-ttu-id="0da67-115">Azure 磁盘加密要求密钥保管库和 vm 位于同一个 Azure 区域中;这可确保加密机密不会跨越区域边界。</span><span class="sxs-lookup"><span data-stu-id="0da67-115">Azure Disk Encryption requires that your key vault and your VMs are in the same Azure region; this ensures that encryption secrets do not cross regional boundaries.</span></span>

<span data-ttu-id="0da67-116">您可以通过以下方式配置和管理密钥存储库:</span><span class="sxs-lookup"><span data-stu-id="0da67-116">You can configure and manage your key vault with:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0da67-117">Powershell</span><span class="sxs-lookup"><span data-stu-id="0da67-117">Powershell</span></span>

```powershell
New-AzKeyVault -Location <location> `
    -ResourceGroupName <resource-group> `
    -VaultName "myKeyVault" `
    -EnabledForDiskEncryption
```

### <a name="azure-cli"></a><span data-ttu-id="0da67-118">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0da67-118">Azure CLI</span></span>

```azurecli
az keyvault create \
    --name "myKeyVault" \
    --resource-group <resource-group> \
    --location <location> \
    --enabled-for-disk-encryption True
```

### <a name="azure-portal"></a><span data-ttu-id="0da67-119">Azure 门户</span><span class="sxs-lookup"><span data-stu-id="0da67-119">Azure portal</span></span>

<span data-ttu-id="0da67-120">azure Key Vault 是可使用常规资源创建过程在 Azure 门户中创建的资源。</span><span class="sxs-lookup"><span data-stu-id="0da67-120">An Azure Key Vault is a resource that can be created in the Azure portal using the normal resource creation process.</span></span>

1. <span data-ttu-id="0da67-121">单击左侧边栏中的 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="0da67-121">Click **Create a resource** in the sidebar on the left.</span></span>

1. <span data-ttu-id="0da67-122">搜索 "Key vault"。</span><span class="sxs-lookup"><span data-stu-id="0da67-122">Search for "Key vault".</span></span> <span data-ttu-id="0da67-123">在 "详细信息" 窗口中单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="0da67-123">Click **Create** in the details window.</span></span>

    ![显示 Azure Marketplace 中的关键电子仓库的屏幕截图](../media/3-create-keyvault.png)

1. <span data-ttu-id="0da67-125">输入新密钥保管库的详细信息:</span><span class="sxs-lookup"><span data-stu-id="0da67-125">Enter the details for the new Key Vault:</span></span>
    - <span data-ttu-id="0da67-126">为密钥存储库输入**名称**</span><span class="sxs-lookup"><span data-stu-id="0da67-126">Enter a **Name** for the Key Vault</span></span>
    - <span data-ttu-id="0da67-127">选择要将其放入的订阅 (默认为您的当前订阅)。</span><span class="sxs-lookup"><span data-stu-id="0da67-127">Select the subscription to place it in (defaults to your current subscription).</span></span>
    - <span data-ttu-id="0da67-128">选择**资源组**, 或创建新的资源组以拥有密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="0da67-128">Select a **Resource Group**, or create a new resource group to own the Key Vault.</span></span>
    - <span data-ttu-id="0da67-129">选择密钥存储库的**位置**。</span><span class="sxs-lookup"><span data-stu-id="0da67-129">Select a **Location** for the Key Vault.</span></span> <span data-ttu-id="0da67-130">请确保选择 VM 所在的位置。</span><span class="sxs-lookup"><span data-stu-id="0da67-130">Make sure to select the location the VM is in.</span></span>
    - <span data-ttu-id="0da67-131">您可以为定价层选择 "标准" 或 "高级"。</span><span class="sxs-lookup"><span data-stu-id="0da67-131">You can choose either Standard or Premium for the pricing tier.</span></span> <span data-ttu-id="0da67-132">主要区别在于, 高级层允许对硬件加密密钥进行备份。</span><span class="sxs-lookup"><span data-stu-id="0da67-132">The main difference is that the premium tier allows for Hardware-encryption backed keys.</span></span>

1. <span data-ttu-id="0da67-133">您必须更改访问策略以支持磁盘加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-133">You must change the Access policies to support Disk Encryption.</span></span> <span data-ttu-id="0da67-134">默认情况下, 它会将_您_的帐户添加到策略中。</span><span class="sxs-lookup"><span data-stu-id="0da67-134">By default it adds _your_ account to the policy.</span></span>
    - <span data-ttu-id="0da67-135">选择**访问策略**</span><span class="sxs-lookup"><span data-stu-id="0da67-135">Select **Access policies**</span></span>
    - <span data-ttu-id="0da67-136">单击 "**高级访问策略**"。</span><span class="sxs-lookup"><span data-stu-id="0da67-136">Click **Advanced access policies**.</span></span>
    - <span data-ttu-id="0da67-137">选中 "对**Azure 磁盘加密启用对卷加密的访问权限**"。</span><span class="sxs-lookup"><span data-stu-id="0da67-137">Check the **Enable access to Azure Disk Encryption for volume encryption**.</span></span>
    - <span data-ttu-id="0da67-138">如果你愿意, 可以删除你的帐户。如果你只打算使用密钥保管库进行磁盘加密, 则无需删除你的帐户。</span><span class="sxs-lookup"><span data-stu-id="0da67-138">You can remove your account if you like, it's not necessary if you only intend to use the Key Vault for disk encryption.</span></span>
    - <span data-ttu-id="0da67-139">单击 **"确定"** 保存更改。</span><span class="sxs-lookup"><span data-stu-id="0da67-139">Click **OK** to save the changes.</span></span>

    ![显示选中并突出显示了 "Azure 磁盘加密" 选项的 "关键保险存储" 高级属性的屏幕截图](../media/3-configure-access-policy.png)

1. <span data-ttu-id="0da67-141">单击 "**创建**" 以创建新的密钥存储库。</span><span class="sxs-lookup"><span data-stu-id="0da67-141">Click **Create** to create the new Key Vault.</span></span>

## <a name="enabling-access-policies-in-the-key-vault"></a><span data-ttu-id="0da67-142">在密钥保管库中启用访问策略</span><span class="sxs-lookup"><span data-stu-id="0da67-142">Enabling access policies in the key vault</span></span>
<span data-ttu-id="0da67-143">Azure 需要访问密钥保管库中的加密密钥或机密, 以使其可供 VM 用于引导和解密卷。</span><span class="sxs-lookup"><span data-stu-id="0da67-143">Azure needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="0da67-144">当我们更改了上面的**高级访问策略**时, 我们讨论了此门户。</span><span class="sxs-lookup"><span data-stu-id="0da67-144">We covered this for the portal when we changed the **Advanced access policies** above.</span></span>

<span data-ttu-id="0da67-145">可以启用三种策略。</span><span class="sxs-lookup"><span data-stu-id="0da67-145">There are three policies you can enable.</span></span>
1. <span data-ttu-id="0da67-146">**磁盘加密**-Azure 磁盘加密所必需的。</span><span class="sxs-lookup"><span data-stu-id="0da67-146">**Disk encryption** - Required for Azure Disk encryption.</span></span>
1. <span data-ttu-id="0da67-147">**部署**-(可选) 使 Microsoft. 计算资源提供程序可以在创建资源时 (例如, 在创建虚拟机时) 引用此密钥存储库时检索此密钥存储库中的机密。</span><span class="sxs-lookup"><span data-stu-id="0da67-147">**Deployment** - (Optional) Enables the Microsoft.Compute resource provider to retrieve secrets from this key vault when this key vault is referenced in resource creation, for example when creating a virtual machine.</span></span>
1. <span data-ttu-id="0da67-148">**模板部署**-(可选) 允许 Azure 资源管理器在模板部署中引用此密钥保管库时从该密钥保管库中获取机密。</span><span class="sxs-lookup"><span data-stu-id="0da67-148">**Template deployment** - (Optional) Enables Azure Resource Manager to get secrets from this key vault when this key vault is referenced in a template deployment.</span></span>

<span data-ttu-id="0da67-149">下面介绍如何启用磁盘加密策略。</span><span class="sxs-lookup"><span data-stu-id="0da67-149">Here's how to enable the disk encryption policy.</span></span> <span data-ttu-id="0da67-150">其他两个类似, 但使用不同的标志。</span><span class="sxs-lookup"><span data-stu-id="0da67-150">The other two are similar but use different flags.</span></span>

```powershell
Set-AzKeyVaultAccessPolicy -VaultName <keyvault-name> -ResourceGroupName <resource-group> -EnabledForDiskEncryption
```

```azurecli
az keyvault update --name <keyvault-name> --resource-group <resource-group> --enabled-for-disk-encryption "true"
```

## <a name="encrypting-an-existing-vm-disk"></a><span data-ttu-id="0da67-151">加密现有的虚拟磁盘</span><span class="sxs-lookup"><span data-stu-id="0da67-151">Encrypting an existing VM disk</span></span>

<span data-ttu-id="0da67-152">拥有密钥存储库安装程序后, 可以使用 azure CLI 或 azure PowerShell 对 VM 进行加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-152">Once you have the Key Vault setup, you can encrypt the VM using either Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="0da67-153">第一次加密 Windows VM 时, 您可以选择仅加密所有磁盘或 OS 磁盘。</span><span class="sxs-lookup"><span data-stu-id="0da67-153">The first time you encrypt a Windows VM, you can choose to encrypt either all disks or the OS disk only.</span></span> <span data-ttu-id="0da67-154">在某些 Linux 分发中, 只有数据磁盘可以加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-154">On some Linux distributions, only the data disks may be encrypted.</span></span> <span data-ttu-id="0da67-155">若要获得加密资格, 必须将 Windows 磁盘格式化为 NTFS 卷。</span><span class="sxs-lookup"><span data-stu-id="0da67-155">To be eligible for encryption, your Windows disks must be formatted as NTFS volumes.</span></span>

> [!WARNING]
> <span data-ttu-id="0da67-156">必须先拍摄快照或备份托管磁盘, 然后才能启用加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-156">You must take a snapshot or a backup of managed disks before you can turn on encryption.</span></span> <span data-ttu-id="0da67-157">下面`SkipVmBackup`指定的标志告诉工具备份已在托管磁盘上完成。</span><span class="sxs-lookup"><span data-stu-id="0da67-157">The `SkipVmBackup` flag specified below tells the tool that the backup is complete on managed disks.</span></span> <span data-ttu-id="0da67-158">如果没有备份, 您将无法恢复 VM (如果由于某种原因加密失败)。</span><span class="sxs-lookup"><span data-stu-id="0da67-158">Without the backup, you will be unable to recover the VM if the encryption fails for some reason.</span></span>

<span data-ttu-id="0da67-159">使用 PowerShell, 使用`Set-AzVmDiskEncryptionExtension` cmdlet 启用加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-159">With PowerShell, use the `Set-AzVmDiskEncryptionExtension` cmdlet to enable encryption.</span></span>

```powershell

Set-AzVmDiskEncryptionExtension `
    -ResourceGroupName <resource-group> `
    -VMName <vm-name> `
    -VolumeType [All | OS | Data]
    -DiskEncryptionKeyVaultId <keyVault.ResourceId> `
    -DiskEncryptionKeyVaultUrl <keyVault.VaultUri> `
     -SkipVmBackup
```

<span data-ttu-id="0da67-160">对于 Azure CLI, 请使用`az vm encryption enable`命令启用加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-160">For the Azure CLI, use the `az vm encryption enable` command to enable encryption.</span></span>

```azurecli
az vm encryption enable \
    --resource-group <resource-group> \
    --name <vm-name> \
    --disk-encryption-keyvault <keyvault-name> \
    --volume-type [all | os | data] \
    --skipvmbackup
```

## <a name="viewing-the-status-of-the-disk"></a><span data-ttu-id="0da67-161">查看磁盘的状态</span><span class="sxs-lookup"><span data-stu-id="0da67-161">Viewing the status of the disk</span></span>

<span data-ttu-id="0da67-162">您可以检查特定磁盘是否已加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-162">You can check whether specific disks are encrypted or not.</span></span>

```powershell
Get-AzVmDiskEncryptionStatus  -ResourceGroupName <resource-group> -VMName <vm-name>
```

```azurecli
az vm encryption show --resource-group <resource-group> --name <vm-name>
```

<span data-ttu-id="0da67-163">这两个命令将返回连接到指定 VM 的每个磁盘的状态。</span><span class="sxs-lookup"><span data-stu-id="0da67-163">Both of these commands will return the status of each disk attached to the specified VM.</span></span>

## <a name="decrypting-drives"></a><span data-ttu-id="0da67-164">解密驱动器</span><span class="sxs-lookup"><span data-stu-id="0da67-164">Decrypting drives</span></span>

<span data-ttu-id="0da67-165">您可以使用`Disable-AzVMDiskEncryption`从 PowerShell 反向加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-165">You can reverse the encryption through PowerShell using `Disable-AzVMDiskEncryption`.</span></span>

```powershell
Disable-AzVMDiskEncryption -ResourceGroupName <resource-group> -VMName <vm-name>
```

<span data-ttu-id="0da67-166">对于 Azure CLI, 请使用`vm encryption disable`命令。</span><span class="sxs-lookup"><span data-stu-id="0da67-166">For the Azure CLI, use the `vm encryption disable` command.</span></span>

```azurecli
az vm encryption disable --resource-group <resource-group> --name <vm-name>
```

<span data-ttu-id="0da67-167">这些命令禁用对指定虚拟机的所有类型的卷进行加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-167">These commands disable encryption for volumes of type all for the specified virtual machine.</span></span> <span data-ttu-id="0da67-168">就像加密版本一样, 您可以指定一个`-VolumeType`参数`[All | OS | Data]`来决定要解密的磁盘。</span><span class="sxs-lookup"><span data-stu-id="0da67-168">Just like the encrypt version, you can specify a `-VolumeType` parameter `[All | OS | Data]` to decide what disks to decrypt.</span></span> <span data-ttu-id="0da67-169">如果未提供`All` , 则默认为。</span><span class="sxs-lookup"><span data-stu-id="0da67-169">It defaults to `All` if not supplied.</span></span>

> [!WARNING]
> <span data-ttu-id="0da67-170">当操作系统和数据磁盘均已加密时, 在 Windows VM 上禁用数据磁盘加密不会按预期工作。</span><span class="sxs-lookup"><span data-stu-id="0da67-170">Disabling data disk encryption on Windows VM when both OS and data disks have been encrypted doesn't work as expected.</span></span> <span data-ttu-id="0da67-171">您必须对所有磁盘禁用加密。</span><span class="sxs-lookup"><span data-stu-id="0da67-171">You must disable encryption on all disks instead.</span></span>

<span data-ttu-id="0da67-172">让我们在新的 VM 上尝试一些命令。</span><span class="sxs-lookup"><span data-stu-id="0da67-172">Let's try some of these commands out on a new VM.</span></span>