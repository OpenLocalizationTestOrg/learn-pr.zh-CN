您可以使用各种工具和平台配置和管理 Azure。 有一些工具可用于命令行、特定于语言的软件开发工具包 (sdk)、开发人员工具、用于迁移的工具和许多其他工具。 

日常管理和交互通常使用的工具包括: 

- **azure 门户**, 用于通过图形用户界面 (GUI) 与 Azure 进行交互
- **azure PowerShell**和**azure 命令行接口**(CLI), 用于命令行和与 azure 的基于自动化的交互
- 基于 web 的命令行界面的**Azure 云**命令行管理程序

创建管理脚本和使用自动化工具是优化工作流的一种有效方式。 您可以自动执行重复的任务, 一旦脚本经过验证, 它将持续运行, 从而减少错误。

## <a name="azure-portal"></a>Azure 门户

Azure 门户是一个可通过 web 浏览器访问的网站, 可转到 URL [https://portal.azure.com](https://portal.azure.com)。 从这里, 你可以手动与所有 Azure 服务交互。 您可以确定要查找的服务, 获取有关特定主题的帮助和更多学习的链接, 以及部署、管理和删除资源。 此外, 它还将指导您使用向导和工具提示完成复杂的管理任务。

仪表板视图提供有关 Azure 环境的高级别详细信息。 您可以根据需要, 通过移动和调整图块、显示感兴趣的特定服务、访问帮助和支持的链接以及提供反馈来自定义门户外观。

门户不提供自动执行重复任务的任何方法。 例如, 若要设置多个虚拟机, 您需要通过完成每个 vm 的向导一次创建一个虚拟机。 这使得门户方法非常耗时且容易出错, 从而实现复杂的任务。
 
 ## <a name="azure-powershell"></a>Azure PowerShell

Azure PowerShell 是一个添加到 Windows PowerShell 或 PowerShell Core 的模块, 可让您连接到 Azure 订阅并管理资源。 Azure PowerShell 需要 Windows PowerShell 才能正常工作。 PowerShell 提供命令行管理程序窗口和命令分析等服务。 然后, azure PowerShell 将添加特定于 azure 的命令。

例如, azure PowerShell 提供了在`New-AzureRmVM` Azure 订阅中为您创建虚拟机的命令。 若要使用它, 请启动 PowerShell, 使用命令`Connect-AzureRMAccount`登录 Azure 帐户, 然后发出如下命令:

```powershell
New-AzureRmVm `
    -ResourceGroupName "MyResourceGroup" `
    -Name "TestVm" `
    -Image "UbuntuLTS"
    ...
```
> [!NOTE]
> powershell Core 是运行在 Windows、Linux 或 macOS 上的跨平台版本的 powershell。

## <a name="azure-cli"></a>Azure CLI

azure CLI 是跨平台命令行程序, 它连接到 azure 并在 azure 资源上执行管理命令。 *跨平台*意味着它可以在 Windows、Linux 或 macOS 上运行。 例如, 若要创建 VM, 请打开命令提示符窗口, 使用命令`az login`登录 Azure, 创建资源组, 然后使用类似如下的命令:

```azurecli
az vm create \
  --resource-group MyResourceGroup \
  --name TestVm \
  --image UbuntuLTS
  --generate-ssh-keys
  ...
```

## <a name="azure-cloud-shell"></a>Azure 云命令行管理程序

Azure 云命令行管理程序是门户中基于浏览器的脚本环境。 它提供了选择最适合您工作方式的命令行管理程序体验的灵活性。 Linux 用户可以选择获取 Bash 体验, 而 Windows 用户可以选择使用 PowerShell。

azure 存储帐户是使用云命令行管理程序所必需的, 在访问 azure 云命令行管理程序时, 系统会提示你创建一个。

在 Microsoft 学习版中, 我们将使用云命令行管理程序来尝试使用 Azure 功能的许多交互式练习。

> [!NOTE] 
> 你可以转到[https://shell.azure.com/](https://shell.azure.com/)访问 Azure 云命令行管理程序。

## <a name="other-options"></a>其他选项

此外, 还有适用于一系列语言和框架的 Azure sdk, 以及可用于以编程方式管理和控制 Azure 资源的 REST api。 有关可用工具的完整列表, 请参阅[下载](https://azure.microsoft.com/en-us/downloads/)页面。

从 azure 开始时, 通常会使用 azure 门户。 让我们进一步了解一下门户的方法。