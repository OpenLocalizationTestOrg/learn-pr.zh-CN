PowerShell 允许您编写命令并立即执行它们。 这称为 "**交互模式**"。

请记住, 客户关系管理 (CRM) 示例中的总体目标是创建三个包含 vm 的测试环境。 您将使用资源组来确保将 vm 组织到单独的环境中: 一个用于单元测试, 一个用于集成测试, 另一个用于验收测试。 您只需创建一次资源组, 这就意味着使用 PowerShell 的交互模式是一个不错的选择。

当您在 PowerShell 中键入命令时, 它会将它与执行请求的操作的_cmdlet_相匹配。 我们将介绍您可以使用的一些常见命令, 然后查看如何安装适用于 PowerShell 的 Azure 支持。

## <a name="what-are-powershell-cmdlets"></a>什么是 PowerShell cmdlet？
PowerShell 命令称为**cmdlet** (发音为 "命令-let")。 cmdlet 是操纵单个功能的命令。 术语 " **cmdlet** " 旨在暗示 "小型命令"。 根据约定, 应鼓励 cmdlet 作者将 cmdlet 保留为简单和单一用途。

基本 PowerShell 产品附带使用可处理诸如会话和后台作业等功能的 cmdlet。 将模块添加到 PowerShell 安装中, 以获取操作其他功能的 cmdlet。 例如, 有第三方模块可以使用 ftp、管理操作系统、访问文件系统等。

cmdlet 遵循动词-名词命名约定;例如, "**进程**"、"**格式表**" 和 "**启动服务**"。 还有一种谓词选择约定: "获取" 以检索数据、"设置" 以插入或更新数据、"格式" 以设置数据格式, "输出" 以将输出定向到目标, 等等。

建议使用 cmdlet 作者为每个 cmdlet 包含一个帮助文件。 **get-help** cmdlet 显示任何 cmdlet 的帮助文件。 例如, 我们可以使用以下语句获取有关`Get-ChildItem` cmdlet 的帮助:

```powershell
Get-Help Get-ChildItem -detailed
```

## <a name="what-is-a-powershell-module"></a>什么是 PowerShell 模块？

cmdlet 是在_模块_中发货的。 PowerShell 模块是一个 DLL, 其中包含用于 proces 每个可用 cmdlet 的代码。 您可以通过加载其包含的模块将 cmdlet 加载到 PowerShell 中。 您可以使用`Get-Module`命令获取加载的模块的列表:

```powershell
Get-Module
```

这将输出如下内容:

```output
ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Find-PackageProvider, Get-Package, Get-Pack...
Script     1.0.0.1    PowerShellGet                       {Find-Command, Find-DscResource, Find-Module, Find-RoleCap...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```

## <a name="what-is-the-az-module"></a>什么是 Az 模块？
**Az**是 Azure PowerShell 模块的正式名称, 其中包含使用 azure 功能的 cmdlet。 它包含数以百计的 cmdlet, 可让你控制每个 Azure 资源的几乎每个方面。 您可以使用资源组、存储、虚拟机、Azure Active Directory、容器、机器学习等。 此模块是[GitHub 上提供](https://github.com/Azure/azure-powershell)的开放源组件。

> [!NOTE]
> 您可能已看到或使用了`-AzureRM`使用格式的 Azure PowerShell 命令。 在10月 2018, 我们宣布将**AzureRM**模块替换为**Az**模块。 此新模块具有多个功能, 尤其是短的 cmdlet 名词`-Az`前缀 ( `-AzureRM`而不是)。 **Az**模块附带了与**AzureRM**模块的向后兼容性, `-AzureRM`因此该 cmdlet 格式将起作用, 但您应转换到**Az**模块并`-Az`使用前接个命令。

### <a name="install-the-az-module"></a>安装 Az 模块

Az 模块可从称为 PowerShell 库的全局存储库中获取。 您可以通过`Install-Module`命令将模块安装到本地计算机上。 您需要提升的 powershell 命令行管理程序才能从 PowerShell 库安装模块。 

::: zone pivot="windows"

若要安装最新的 Azure PowerShell 模块, 请运行以下命令:

1. 打开 "**开始**" 菜单并键入**Windows PowerShell**。

1. 右键单击 " **Windows PowerShell** " 图标, 然后选择 "**以管理员身份运行**"。

1. 在 "**用户帐户控制**" 对话框中, 选择 **"是"**。

1. 键入以下命令, 然后按 enter:

    ```powershell
    Install-Module -Name Az -AllowClobber
    ```

这将默认安装所有用户的模块 (由 scope 参数控制)。

该命令依赖 nuget 检索组件, 具体取决于您已安装的 nuget 版本, 您可能会收到下载并安装最新版本的 nuget 的提示。

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files (x86)\PackageManagement\ProviderAssemblies' or
'C:\Users\<username>\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import
 the NuGet provider now?
```

默认情况下, 不会将 PowerShell 库配置为 PowerShellGet 的受信任存储库。 第一次使用 PSGallery 时, 您会看到以下提示:

```output
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
```

#### <a name="script-execution-failed"></a>脚本执行失败
根据您的安全配置, `Import-Module`可能会失败, 如以下内容。

```output
import-module : File C:\Program Files (x86)\WindowsPowerShell\Modules\az\0.7.0\Az.psm1 cannot be loaded
because running scripts is disabled on this system. For more information, see about_Execution_Policies at
https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ import-module Az
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [Import-Module], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.ImportModuleCommand
```

这通常表示执行策略为 "受限制", 这意味着您不能执行从外部源 (包括 PowerShell 库) 下载的模块。 您可以通过执行命令`Get-ExecutionPolicy`来检查是否属于这种情况。 如果它返回 "受限", 则执行以下操作:

1. 打开提升的 PowerShell 命令提示符。
1. 使用`SetExecutionPolicy` cmdlet 将策略更改为 "RemoteSigned":

```powershell
Set-ExecutionPolicy RemoteSigned
```

这将提示你获取权限:

```output
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

然后, 您应该能够使用`Import-Module`加载 cmdlet。

:::zone-end

::: zone pivot="linux,macos"

我们使用相同的命令在 Linux 或 macOS 上安装 Azure PowerShell。

1. 在终端中, 键入以下命令以使用提升的权限启动 PowerShell Core。

    ```bash
    sudo pwsh
    ```

1. 在 PowerShell Core 提示符处运行以下命令, 以安装 Azure PowerShell。

    ```powershell
    Install-Module Az -AllowClobber
    ```

1. 如果系统询问您是否信任**PSGallery**中的模块, 回答 **"是"** 或 **"是" 全部**。

:::zone-end

### <a name="update-a-module"></a>更新模块

如果您收到一条警告或错误消息, 指示已安装 Azure PowerShell 模块的某个版本, 则可以通过发出以下命令更新到_最新_版本:

```powershell
Update-Module -Name Az
```

与`Install-Module`命令一样, 当系统提示您信任模块时, 回答 **"是"** 或 **"是"** 。 如果遇到问题, 还`Update-Module`可以使用命令重新安装模块。

## <a name="example-how-to-create-a-resource-group-with-azure-powershell"></a>示例: 如何使用 Azure PowerShell 创建资源组
加载 azure 模块后, 即可开始使用 azure。 我们来创建一个常见的任务-创建一个资源组。 如你所知, 我们使用资源组来管理相关的资源。 创建新的资源组是您在启动新的 Azure 解决方案时要执行的第一项任务。

我们需要执行四个步骤:

1. 导入 Azure cmdlet。

1. 连接到你的 Azure 订阅。

1. 创建资源组。

1. 验证创建是否成功 (如下所示)。

下图显示了这些步骤的概述。

![显示创建资源组的步骤的插图。](../media/5-create-resource-overview.png)

每个步骤对应不同的 cmdlet。

### <a name="import-the-azure-cmdlets"></a>导入 Azure cmdlet
启动时, PowerShell 仅在默认情况下加载核心 cmdlet。 这意味着你需要使用 Azure 的 cmdlet 将不会加载。 若要加载所需的 cmdlet, 最可靠的方法是在 PowerShell 会话开始时手动导入这些 cmdlet。

您可以使用**导入模块**cmdlet 加载模块。 此 cmdlet 具有许多用于处理各种情况的参数。 例如, 它可以加载多个模块、特定模块版本、模块的一部分, 等等。

例如,**在提升的 PowerShell 会话中**, 我们可以使用以下命令加载 Az 的所有 cmdlet:

```powershell
Import-Module Az
```

> [!TIP]
> 如果你发现频繁使用 Azure PowerShell, 可以通过两种方法来自动执行模块加载过程。 您可以向 powershell 配置文件中添加条目, 以在启动时导入 Azure 模块, 或使用最新版本的 powershell, 在使用 cmdlet 时自动加载包含模块。

### <a name="connect"></a>连接
当您使用 azure PowerShell 的本地安装时, 需要先进行身份验证, 然后才能执行 azure 命令。 **AzAccount** cmdlet 会提示你输入 azure 凭据, 然后连接到你的 azure 订阅。 它具有多个可选参数, 但如果您只需要交互式提示, 则不需要任何参数:

```powershell
Connect-AzAccount
```

您需要对您启动的每个新 PowerShell 会话重复这些步骤, 因为此模块不是核心集的一部分。


### <a name="working-with-subscriptions"></a>使用订阅
如果你不熟悉 Azure, 你可能只有一个订阅。 但是, 如果你已使用 Azure 一段时间, 则可能已创建了多个 azure 订阅。 您可以将 Azure PowerShell 配置为对特定订阅执行命令。

一次只能在一个订阅中。 使用`Get-AzContext` cmdlet 确定哪个订阅处于活动状态。 如果不正确, 可以对其进行更改。

1. 使用`Get-AzSubscription`命令获取帐户中所有订阅名称的列表。 

2. 通过传递要选择的订阅的名称来更改订阅。

```powershell
Select-AzSubscription -Subscription "Visual Studio Enterprise"
```

### <a name="get-a-list-of-all-resource-groups"></a>获取所有资源组的列表

您可以检索活动订阅中的所有资源组的列表:

```powershell
Get-AzResourceGroup
```

若要获得更简洁的视图, 可以使用管道 "|" `Get-AzResourceGroup`将输出`Format-Table`发送到 cmdlet。

```powershell
Get-AzResourceGroup | Format-Table
```

这将输出如下内容:

```output
ResourceGroupName                  Location       ProvisioningState Tags TagsTable ResourceId
-----------------                  --------       ----------------- ---- --------- ----------
cloud-shell-storage-southcentralus southcentralus Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
ExerciseResources                  eastus         Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
```

### <a name="create-a-resource-group"></a>创建资源组

正如您所知, 在 Azure 中创建资源时, 您将始终出于管理目的将它们放入资源组中。 资源组通常是启动新的应用程序时要创建的第一项。

您可以使用`New-AzResourceGroup` cmdlet 创建资源组。 您必须指定名称和位置。 该名称在你的订阅中必须是唯一的。 该位置确定将存储资源组的元数据的位置 (由于合规性原因, 可能对您很重要)。 您可以使用如 "west US"、"北欧" 或 "西印度" 指定位置的字符串。 与大多数 Azure cmdlet 一样, `New-AzResourceGroup`具有多个可选参数;但是, 核心语法为:

```powershell
New-AzResourceGroup -Name <name> -Location <location>
```

> [!NOTE]
> 请记住, 我们将在 Azure 沙箱中工作, 这将为你创建资源组。 如果您在自己的订阅中工作, 将使用上面的命令。

### <a name="verify-the-resources"></a>验证资源
`Get-AzResource`列出了 Azure 资源。 这在此处可用于验证资源组的创建是否成功。

```powershell
Get-AzResource
```

与`Get-AzResourceGroup`命令一样, 您可以通过`Format-Table` cmdlet 获得更简洁的视图。 此处, 我们将使用简写版本`ft`:

```powershell
Get-AzResource | ft
```

您还可以将其筛选到特定的资源组, 以仅列出与该组关联的资源:

```powershell
Get-AzResource -ResourceGroup ExerciseResources
```

### <a name="creating-an-azure-virtual-machine"></a>创建 Azure 虚拟机

可以使用 PowerShell 完成的另一个常见任务是创建虚拟机。

Azure PowerShell 提供用于`New-AzVm`创建虚拟机的 cmdlet。 cmdlet 具有许多参数, 以使其能够处理大量 VM 配置设置。 大多数参数都具有合理的默认值, 因此只需指定五项内容:

- **ResourceGroupName**: 将在其中放置新 VM 的资源组。
- **名称**: Azure 中的 VM 的名称。
- **位置**: 将在其中设置 VM 的地理位置。
- **Credential**: 包含 VM 管理员帐户的用户名和密码的对象。 我们将使用`Get-Credential` cmdlet。 此 cmdlet 将提示输入用户名和密码, 并将其打包到 credential 对象中。
- **Image**: 用于 VM 的操作系统映像。 这通常是 Linux 分发或 Windows Server。

```powershell
   New-AzVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

您可以直接向 cmdlet 提供这些参数, 如上所示。 或者, 可以使用其他 cmdlet 配置虚拟`Set-AzVMOperatingSystem`机, 例如`Set-AzVMSourceImage` `Add-AzVMNetworkInterface`、、和。 `Set-AzVMOSDisk`

下面的示例将`Get-Credential` cmdlet 与`-Credential`参数一起使用:

```powershell
New-AzVM -Name MyVm -ResourceGroupName ExerciseResources -Credential (Get-Credential) ...
```

`AzVM`后缀特定于 PowerShell 中基于 VM 的命令。 您可以使用的其他几个选项:

| 指挥 | 说明 |
|---------|-------------|
| `Remove-AzVM` | 删除 Azure VM。 |
| `Start-AzVM` | 启动已停止的 VM。 |
| `Stop-AzVM` | 停止正在运行的 VM。 |
| `Restart-AzVM` | 重新启动 VM。 |
| `Update-AzVM` | 更新 VM 的配置。 |

#### <a name="example-getting-the-information-for-a-vm"></a>示例: 获取 VM 的信息

您可以使用`Get-AzVM -Status`命令列出订阅中的虚拟机。 这还可以使用`-Name`属性指定 VM。 在这里, 我们将其分配给 PowerShell 变量:

```powershell
$vm = Get-AzVM  -Name MyVM -ResourceGroupName ExerciseResources
```

有趣的是, 这是您可以与之交互的_对象_。 例如, 您可以获取该对象, 进行更改, 然后使用以下`Update-AzVM`命令将更改重新推送到 Azure:

```powershell
$ResourceGroupName = "ExerciseResources"
$vm = Get-AzVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

PowerShell 的交互模式适用于一次性任务。 在我们的示例中, 我们可能在项目的生命周期中使用相同的资源组, 这意味着以交互方式创建它是合理的。 与编写脚本并只执行一次该脚本相比, 此任务的交互模式通常更快速且更容易。