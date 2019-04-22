创建管理脚本是优化工作流的一种有效方式。 您可以自动执行常见的重复性任务。 脚本经过验证后, 它将持续运行, 这很可能会减少错误。 在上一个练习中, 我们创建了一个 VM, 添加了数据磁盘, 并通过 Azure 门户进行了更改的缓存设置。 如果我们需要在多个区域中跨多个 vm 重复这些任务, 该怎么办？ 我们可以使用 Azure PowerShell 执行此操作。

> [!TIP]
> 我们将在**使用 PowerShell 模块自动化 azure 任务**中详细介绍 azure PowerShell。 若要详细了解如何安装、配置和使用 PowerShell, 请务必检查模块。

## <a name="what-is-azure-powershell"></a>什么是 Azure PowerShell？

Azure PowerShell 是一种跨平台命令行工具, 用于连接到 Azure 订阅并管理资源。 它是以下两项的组合: **PowerShell**, 提供命令行工具支持;和**Az** PowerShell 模块, 它提供了可与 Azure 配合使用的命令 (称为 "cmdlet")。 

azure PowerShell 包含用于操作 Azure 资源的大多数方面的 cmdlet。 您可以使用资源组、存储、虚拟机、Azure Active Directory、容器、机器学习等。 我们在其他培训模块中讨论了所有这些详细信息。

### <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>用于管理 Azure 磁盘缓存的 PowerShell cmdlet

Azure PowerShell 具有特定的 cmdlet, 可帮助管理虚拟机和磁盘。

|指挥  | 说明 |
|---------|-------------|
| `Get-AzVM`         | 获取虚拟机的属性。       |
| `Update-AzVM`      | 更新 Azure 虚拟机的状态。  |
| `New-AzDiskConfig` | 创建一个可配置的磁盘对象。             |
| `Add-AzVMDataDisk` | 将数据磁盘添加到虚拟机。          |

通过这些操作, 我们可以执行在 Azure 门户中执行的所有任务。 让我们在 VM 上试用。
