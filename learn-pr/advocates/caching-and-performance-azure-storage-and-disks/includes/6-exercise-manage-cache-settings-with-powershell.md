在上一个练习中, 我们使用 Azure 门户执行以下任务:

- 查看 OS 磁盘缓存状态
- 更改 OS 磁盘的缓存设置
- 将数据磁盘添加到 VM
- 更改新数据磁盘上的缓存类型

让我们使用 Azure PowerShell 来练习这些操作。 

> [!NOTE]
> 我们将使用 azure PowerShell, 但您也可以使用 azure CLI, 它提供了与基于控制台的工具类似的功能。 它在 macOS、Linux 和 Windows 上运行。 如果你有兴趣了解有关 azure cli 的详细信息, 请参阅**使用 azure cli 模块管理虚拟机**。

我们将使用我们在上一个练习中创建的 VM。 此实验室中的操作假定:

- 我们的 VM 已存在, 并被称为**fotoshareVM**
- 我们的 VM 位于名为** <rgn>[沙盒资源组名称]</rgn>的资源组中**

如果你已使用一组不同的名称, 请将这些值替换为您的名称。

以下是我们在上一个练习中的虚拟磁盘的当前状态:

![操作系统和数据磁盘的屏幕截图, 都设置为只读缓存。](../media/disks-final-config-portal.PNG)

我们使用了门户为 OS 和数据磁盘设置**主机缓存**字段。 按照以下步骤操作, 请记住这一初始状态。

### <a name="set-up-some-variables"></a>设置一些变量

首先, 让我们存储一些资源名称, 以便以后可以使用它们。

1. 使用右侧的 "Azure 云命令行管理程序" 终端运行以下 PowerShell 命令:

    > [!NOTE]
    > 在尝试这些命令之前, 请先将云命令行管理程序会话切换到**PowerShell** , 如果尚未尝试。
    
    ```powershell
    $myRgName = "<rgn>[sandbox resource group name]</rgn>"
    $myVMName = "fotoshareVM"
    ```
    
    > [!TIP]
    > 如果云命令行管理程序会话超时, 则必须再次设置这些变量。因此, 如果可能, 请在单个会话中完成整个实验。
    
### <a name="get-info-about-our-vm"></a>获取有关我们的虚拟机的信息

1. 运行以下命令以获取我们的虚拟机的属性:

    ```powershell
    $myVM = Get-AzVM -ResourceGroupName $myRgName -VMName $myVmName
    ```
    
1. 我们将响应存储在`$myVM`变量中。 我们可以通过管道将输出通过`select-object`管道传递到 cmdlet, 以将显示筛选为特定属性:

    ```powershell
    $myVM | select-object -property ResourceGroupName, Name, Type, Location
    ```
    
1. 您应该会看到如下所示的内容。

    ```powershell
    ResourceGroupName Name        Type                              Location
    ----------------- ----        ----                              --------
    <rgn>[sandbox resource group name]</rgn> fotoshareVM Microsoft.Compute/virtualMachines eastus
    ```
    
### <a name="view-os-disk-cache-status"></a>查看 OS 磁盘缓存状态

1. 我们可以通过`StorageProfile`对象检查缓存设置, 如下所示:

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching
    ```

    ```output
    ReadOnly
    ```
   
1. 让我们将其重新更改为 OS 磁盘的默认值, 即_ReadWrite_。

### <a name="change-the-cache-settings-of-the-os-disk"></a>更改 OS 磁盘的缓存设置

1. 可以使用相同`StorageProfile`的对象设置缓存类型的值, 如下所示:

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
    ```
    
    此命令运行速度快, 应告诉你它在本地执行某些操作。 该命令仅更改`myVM`对象的属性。 如下面的屏幕截图所示, 如果使用`$myVM` `Get-AzVM` cmdlet 重新分配变量来刷新变量, 则缓存值在 VM 上未发生更改。

1. 若要在 VM 本身上进行更改, 请`Update-AzVM`调用, 如下所示:

    ```powershell
    Update-AzVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
    请注意, 此调用需要一段时间才能完成。 这是因为我们正在更新实际 vm 和 Azure 以进行更改。

    ```output
    RequestId IsSuccessStatusCode StatusCode ReasonPhrase
    --------- ------------------- ---------- ------------
                             True         OK OK
    ```
    
1. 如果再次刷新该`$myVM`变量, 则会看到该对象上的更改。 在门户中查看磁盘时, 您还会看到此处的更改。 

    ```powershell
    $myVM = Get-AzVM -ResourceGroupName $myRgName -VMName $myVmName
    $myVM.StorageProfile.OsDisk.Caching
    ```
    
    ```output
    ReadWrite
    ```
    
### <a name="list-data-disk-info"></a>列出数据磁盘信息

1. 若要查看我们在 VM 上拥有哪些数据磁盘, 请运行以下命令:

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
    
目前仅有一个数据磁盘。 `Lun`字段很重要。 它是唯一的**L**ogical **U**nit **N**号码。 当我们添加另一个数据磁盘时, 我们会为其`Lun`指定一个唯一值。

### <a name="add-a-new-data-disk-to-our-vm"></a>将新的数据磁盘添加到我们的虚拟机

1. 为方便起见, 我们将存储新的磁盘名称:

    ```powershell
    $newDiskName = "fotoshareVM-data2"
    ```
    
1. 运行以下`Add-AzVMDataDisk`命令以定义一个新的空 1 GB 数据磁盘:

    ```powershell
    Add-AzVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
    ```
    你将收到类似以下内容的响应:

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
    
1. 我们为此磁盘提供了`Lun`一个值`1` , 因为它没有获取。 我们定义了要创建的磁盘, 因此, 请运行`Update-AzVM`以进行实际更改:

    ```powershell
    Update-AzVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
1. 接下来, 我们来看看我们的数据磁盘信息:

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

现在, 我们有两个磁盘。 `Lun`新磁盘具有`1`的和的默认值`Caching`为。 `None` 让我们更改该值。

### <a name="change-cache-settings-of-new-data-disk"></a>更改新数据磁盘的缓存设置

1. 我们使用`Set-AzVMDataDisk` cmdlet 修改虚拟机数据磁盘的属性, 如下所示:

    ```powershell
    Set-AzVMDataDisk -VM $myVM -Lun "1" -Caching ReadWrite
    ```
    
1. 与往常一样, 要提交更改`Update-AzVM`, 请执行以下操作:

    ```powershell
    Update-AzVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
以下是我们在此练习中已完成的操作的门户视图。 我们的 VM 现在有两个数据磁盘, 并且我们调整了所有**主机缓存**设置。 我们只需几个命令即可完成所有这些操作。 这就是 Azure PowerShell 的强大功能。

![显示包含两个数据磁盘的 VM 刀片磁盘部分的 Azure 门户屏幕截图。](../media/disks-final-config-portal2.png)
