回想一下我们的原始方案-创建虚拟机以测试我们的 CRM 软件。 当有新的内部版本时, 我们想要加速新的 VM, 以便我们可以从干净的映像测试完整的安装体验。 完成后, 我们想要删除 VM。

让我们尝试用于创建 VM 的命令。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm-with-azure-powershell"></a>使用 Azure PowerShell 创建 Linux VM

由于我们使用的是 Azure 沙箱, 因此您无需创建资源组。 请改为使用资源组**<rgn>[沙盒资源组名称]</rgn>**。 此外, 请注意位置限制。

让我们使用 PowerShell 创建新的 Azure VM。

1. 使用`New-AzVm` cmdlet 创建 VM。
    - 使用 "资源组**<rgn>[沙盒资源组名称]</rgn>**"。
    - 为 vm 提供一个名称, 通常是您希望使用一些有意义的内容, 用于标识 vm、位置以及 (如果有多个) 实例号的用途。 我们将使用 "testvm-eus-01" 作为 "与我们联系, instance 1" 中的 "测试虚拟机"。 根据你放置虚拟机的位置提供你自己的名称。
    - 从 Azure 沙箱中提供的以下列表中选择一个与你接近的位置。 如果使用复制和粘贴, 请务必更改以下示例命令中的值。

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - 对图像使用 "UbuntuLTS"-这是 Ubuntu Linux。
    - 使用`Get-Credential` cmdlet 并将结果输送到`Credential`参数中。
      > [!IMPORTANT]
      > 有关用户名和密码限制, 请参阅[Linux VM 常见问题解答](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm?azure-portal=true)。 密码长度必须为 12-123 个字符, 并满足以下4个复杂性要求中的3个:
      > - 包含较少字符
      > - 包含大写字符
      > - 有一个数字
      > - 包含特殊字符 (正则表达式匹配 [\W_])
    - 添加`-OpenPorts`参数并将 "22" 作为端口传递, 这将使我们成为此计算机的 SSH。
 
    ```powershell
    New-AzVm -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image UbuntuLTS -OpenPorts 22
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
    
1. 这将需要几分钟的时间才能完成。 完成后, 可以对其进行查询, 并将 VM 对象分配给变量 (`$vm`)。

    ```powershell
    $vm = Get-AzVM -Name "testvm-eus-01" -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```
    
1. 然后查询值, 以转储有关 VM 的信息:

    ```powershell
    $vm
    ```

    您应该会看到类似这样的内容:

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
    
1. 您可以通过点 (".") 语法进入复杂对象。 例如, 若要查看与 HardwareProfile 节相关`VMSize`联的对象中的属性, 您可以键入:

    ```powershell
    $vm.HardwareProfile
    ```

1. 若要获取其中一个磁盘的信息, 请执行以下操作:

    ```powershell
    $vm.StorageProfile.OsDisk
    ```

1. 您甚至可以将 VM 对象传递到其他 cmdlet。 例如, 这将检索 VM 的公共 IP 地址:

    ```powershell
    $vm | Get-AzPublicIpAddress
    ```

1. 使用 IP 地址, 你可以使用 SSH 连接到 VM。 例如, 如果您使用用户名 "bob", 并且 IP 地址为 "205.22.16.5", 则此命令将连接到 Linux 计算机:

    ```powershell
    ssh bob@205.22.16.5
    ```

    通过键入`exit`来继续执行并注销。


## <a name="delete-a-vm"></a>删除 VM

只需尝试一些更多命令, 让我们删除 VM。 我们将首先将其关闭。

```powershell
Stop-AzVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

现在, 让我们使用`Remove-AzVM` cmdlet 删除 VM:

```powershell
Remove-AzVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

尝试此命令列出资源组中的所有资源:

```powershell
Get-AzResource -ResourceGroupName $vm.ResourceGroupName | ft
```

您应该会看到所有仍然存在的资源组 (磁盘、虚拟网络等)。 

```output
Microsoft.Compute/disks
Microsoft.Network/networkInterfaces
Microsoft.Network/networkSecurityGroups
Microsoft.Network/publicIPAddresses
Microsoft.Network/virtualNetworks
```

这是因为`Remove-AzVM`命令_仅删除了 VM_。 它不会清除任何其他资源! 在这种情况下, 我们很可能只是删除资源组本身并使用它完成。 不过, 我们只需运行练习, 即可手动对其进行清理。 您应该会在命令中看到模式。

1. 删除网络接口。

    ```powershell
    $vm | Remove-AzNetworkInterface –Force
    ```
    
1. 删除托管 OS 磁盘和存储帐户

    ```powershell
    Get-AzDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzDisk -Force
    ```

1. 接下来, 删除虚拟网络。

    ```powershell
    Get-AzVirtualNetwork -ResourceGroup $vm.ResourceGroupName | Remove-AzVirtualNetwork -Force
    ```

1. 删除网络安全组。

    ```powershell
    Get-AzNetworkSecurityGroup -ResourceGroup $vm.ResourceGroupName | Remove-AzNetworkSecurityGroup -Force
    ```

1. 最后是公共 IP 地址。

    ```powershell
    Get-AzPublicIpAddress -ResourceGroup $vm.ResourceGroupName | Remove-AzPublicIpAddress -Force
    ```

我们应该已捕获所有创建的资源;请检查资源组, 以确保。 我们在此处执行了许多手动命令, 但更好的方法是编写一个_脚本_, 以便以后可以重用此逻辑来创建或删除 VM。 让我们来看一下使用 PowerShell 编写脚本。