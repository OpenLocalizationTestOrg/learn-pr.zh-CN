假设您的公司已决定在所有虚拟机上实施 Azure 磁盘加密 (ADE)。 您需要评估如何将加密部署到现有的虚拟机卷。 在这里, 我们将介绍 ADE 的要求, 以及在对现有 Linux 和 Windows 虚拟机加密磁盘时涉及的步骤。

## <a name="azure-disk-encryption-prerequisites"></a>Azure 磁盘加密先决条件

必须先执行以下操作, 然后才能对虚拟机磁盘进行加密:

1. 创建一个密钥存储库。
1. 设置密钥存储库访问策略以支持磁盘加密。
1. 使用密钥存储库存储 ADE 的加密密钥。

### <a name="azure-key-vault"></a>Azure Key Vault

可将 ADE 使用的加密密钥存储在 Azure Key Vault 中。 Azure Key Vault 是一个用于安全存储和访问机密的工具。 密码是您想要严格控制其访问权限的任何内容, 如 API 密钥、密码或证书。 这提供了高度可用且可扩展的安全存储, 如联邦信息处理标准 (FIPS) 140-2 第2级验证的硬件安全模块 (hsm) 中所定义。 使用密钥存储库可以保持对用于加密数据的密钥的完全控制, 并且可以管理和审核密钥用法。 

> [!NOTE]
> Azure 磁盘加密要求密钥保管库和 vm 位于同一个 Azure 区域中;这可确保加密机密不会跨越区域边界。

您可以通过以下方式配置和管理密钥存储库:

#### <a name="powershell"></a>Powershell

```powershell
New-AzKeyVault -Location <location> `
    -ResourceGroupName <resource-group> `
    -VaultName "myKeyVault" `
    -EnabledForDiskEncryption
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az keyvault create \
    --name "myKeyVault" \
    --resource-group <resource-group> \
    --location <location> \
    --enabled-for-disk-encryption True
```

### <a name="azure-portal"></a>Azure 门户

azure Key Vault 是可使用常规资源创建过程在 Azure 门户中创建的资源。

1. 单击左侧边栏中的 "**创建资源**"。

1. 搜索 "Key vault"。 在 "详细信息" 窗口中单击 "**创建**"。

    ![显示 Azure Marketplace 中的关键电子仓库的屏幕截图](../media/3-create-keyvault.png)

1. 输入新密钥保管库的详细信息:
    - 为密钥存储库输入**名称**
    - 选择要将其放入的订阅 (默认为您的当前订阅)。
    - 选择**资源组**, 或创建新的资源组以拥有密钥保管库。
    - 选择密钥存储库的**位置**。 请确保选择 VM 所在的位置。
    - 您可以为定价层选择 "标准" 或 "高级"。 主要区别在于, 高级层允许对硬件加密密钥进行备份。

1. 您必须更改访问策略以支持磁盘加密。 默认情况下, 它会将_您_的帐户添加到策略中。
    - 选择**访问策略**
    - 单击 "**高级访问策略**"。
    - 选中 "对**Azure 磁盘加密启用对卷加密的访问权限**"。
    - 如果你愿意, 可以删除你的帐户。如果你只打算使用密钥保管库进行磁盘加密, 则无需删除你的帐户。
    - 单击 **"确定"** 保存更改。

    ![显示选中并突出显示了 "Azure 磁盘加密" 选项的 "关键保险存储" 高级属性的屏幕截图](../media/3-configure-access-policy.png)

1. 单击 "**创建**" 以创建新的密钥存储库。

## <a name="enabling-access-policies-in-the-key-vault"></a>在密钥保管库中启用访问策略
Azure 需要访问密钥保管库中的加密密钥或机密, 以使其可供 VM 用于引导和解密卷。 当我们更改了上面的**高级访问策略**时, 我们讨论了此门户。

可以启用三种策略。
1. **磁盘加密**-Azure 磁盘加密所必需的。
1. **部署**-(可选) 使 Microsoft. 计算资源提供程序可以在创建资源时 (例如, 在创建虚拟机时) 引用此密钥存储库时检索此密钥存储库中的机密。
1. **模板部署**-(可选) 允许 Azure 资源管理器在模板部署中引用此密钥保管库时从该密钥保管库中获取机密。

下面介绍如何启用磁盘加密策略。 其他两个类似, 但使用不同的标志。

```powershell
Set-AzKeyVaultAccessPolicy -VaultName <keyvault-name> -ResourceGroupName <resource-group> -EnabledForDiskEncryption
```

```azurecli
az keyvault update --name <keyvault-name> --resource-group <resource-group> --enabled-for-disk-encryption "true"
```

## <a name="encrypting-an-existing-vm-disk"></a>加密现有的虚拟磁盘

拥有密钥存储库安装程序后, 可以使用 azure CLI 或 azure PowerShell 对 VM 进行加密。 第一次加密 Windows VM 时, 您可以选择仅加密所有磁盘或 OS 磁盘。 在某些 Linux 分发中, 只有数据磁盘可以加密。 若要获得加密资格, 必须将 Windows 磁盘格式化为 NTFS 卷。

> [!WARNING]
> 必须先拍摄快照或备份托管磁盘, 然后才能启用加密。 下面`SkipVmBackup`指定的标志告诉工具备份已在托管磁盘上完成。 如果没有备份, 您将无法恢复 VM (如果由于某种原因加密失败)。

使用 PowerShell, 使用`Set-AzVmDiskEncryptionExtension` cmdlet 启用加密。

```powershell

Set-AzVmDiskEncryptionExtension `
    -ResourceGroupName <resource-group> `
    -VMName <vm-name> `
    -VolumeType [All | OS | Data]
    -DiskEncryptionKeyVaultId <keyVault.ResourceId> `
    -DiskEncryptionKeyVaultUrl <keyVault.VaultUri> `
     -SkipVmBackup
```

对于 Azure CLI, 请使用`az vm encryption enable`命令启用加密。

```azurecli
az vm encryption enable \
    --resource-group <resource-group> \
    --name <vm-name> \
    --disk-encryption-keyvault <keyvault-name> \
    --volume-type [all | os | data] \
    --skipvmbackup
```

## <a name="viewing-the-status-of-the-disk"></a>查看磁盘的状态

您可以检查特定磁盘是否已加密。

```powershell
Get-AzVmDiskEncryptionStatus  -ResourceGroupName <resource-group> -VMName <vm-name>
```

```azurecli
az vm encryption show --resource-group <resource-group> --name <vm-name>
```

这两个命令将返回连接到指定 VM 的每个磁盘的状态。

## <a name="decrypting-drives"></a>解密驱动器

您可以使用`Disable-AzVMDiskEncryption`从 PowerShell 反向加密。

```powershell
Disable-AzVMDiskEncryption -ResourceGroupName <resource-group> -VMName <vm-name>
```

对于 Azure CLI, 请使用`vm encryption disable`命令。

```azurecli
az vm encryption disable --resource-group <resource-group> --name <vm-name>
```

这些命令禁用对指定虚拟机的所有类型的卷进行加密。 就像加密版本一样, 您可以指定一个`-VolumeType`参数`[All | OS | Data]`来决定要解密的磁盘。 如果未提供`All` , 则默认为。

> [!WARNING]
> 当操作系统和数据磁盘均已加密时, 在 Windows VM 上禁用数据磁盘加密不会按预期工作。 您必须对所有磁盘禁用加密。

让我们在新的 VM 上尝试一些命令。