假设您需要选择一个工具来管理用于测试客户关系管理 (CRM) 系统的 Azure 资源。 您的测试要求您创建资源组和预配虚拟机 (vm)。

您需要便于管理员学习的内容, 但功能强大, 可自动执行多个虚拟机的安装和设置或编写完整的应用程序环境。 有多个可用工具;您需要查找最适合您的人员和任务的一个。

## <a name="what-tools-are-available"></a>有哪些工具可用？
Azure 提供了三个管理工具供您选择:

- Azure 门户
- Azure CLI
- Azure PowerShell

它们都提供了大致相同的控制量;您可以使用其中一种工具执行的任何任务, 您很可能会使用其他两个。 这三种都是跨平台, 在 Windows、macOS 和 Linux 上运行。 它们在语法、安装要求以及是否支持自动化方面有所不同。

在这里, 我们将介绍这三个选项中的每一个, 并提供有关如何在它们之间进行决定的指导。 

## <a name="what-is-the-azure-portal"></a>什么是 Azure 门户？
azure 门户是一个网站, 可让你创建、配置和更改 Azure 订阅中的资源。 门户是一个图形用户界面 (GUI), 便于查找所需的资源并执行所需的任何更改。 它还通过提供向导和工具提示来指导您完成复杂的管理任务。

门户不提供自动执行重复任务的任何方法。 例如, 要设置15台虚拟机, 您需要通过完成每个 VM 的向导来创建一个虚拟机。 对于复杂的任务, 这可能非常耗时且容易出错。 

## <a name="what-is-the-azure-cli"></a>什么是 Azure CLI？
azure CLI 是跨平台命令行程序, 用于连接到 azure 并在 azure 资源上执行管理命令。 例如, 若要创建 VM, 应使用类似如下的命令:

```azurecli
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

可通过两种方式使用 azure CLI: 在浏览器中通过 Azure 云命令行管理程序或在 Linux、Mac 或 Windows 上进行本地安装。 在这两种情况下, 可以交互使用, 也可以编写脚本。 为进行交互式使用, 首先启动命令行管理程序`cmd.exe` (如 Windows 或 Bash 上的 macOS), 然后在命令行管理程序提示符处发出命令。 若要自动执行重复任务, 请使用所选命令行管理程序的脚本语法将命令组合到命令行管理程序脚本中, 然后执行该脚本。

## <a name="what-is-azure-powershell"></a>什么是 Azure PowerShell？
Azure PowerShell 是您添加到 Windows powershell 或 PowerShell Core 以允许您连接到 Azure 订阅并管理资源的模块。 Azure powershell 需要 PowerShell 才能正常工作。 PowerShell 提供命令行管理程序窗口、命令分析等服务。 azure PowerShell 添加了特定于 azure 的命令。

例如, azure PowerShell 提供了可在 Azure 订阅中为您创建虚拟机的**新的 AzVM**命令。 若要使用它, 请启动 PowerShell 应用程序, 然后发出如下所示的命令:

```powershell
New-AzVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

azure PowerShell 也有两种方法: 在浏览器中通过 Azure 云命令行管理程序或在 Linux、Mac 或 Windows 上的本地安装。 在这两种情况下, 您都有两种模式可供选择。 您可以在交互模式下使用它, 在这种模式下, 您可以一次手动发布一个命令, 也可以在脚本模式下执行, 在此模式下, 您可以执行包含多个命令的脚本。

## <a name="how-to-choose-an-administrative-tool"></a>如何选择管理工具
门户、azure CLI 和 azure PowerShell 之间有近似的奇偶校验, 与他们可以管理的 Azure 对象以及他们可以创建的配置有关。 它们也都是跨平台。 这意味着, 在做出选择时, 您通常会考虑几个其他因素:

- **自动化**: 是否需要自动执行一组复杂或重复的任务？ 在门户不支持这种情况下, azure PowerShell 和 azure CLI 支持此功能。

- **学习曲线**: 是否需要快速完成任务而不学习新的命令或语法？ Azure 门户不需要你了解语法或记忆命令。 在 azure PowerShell 和 azure CLI 中, 必须了解您使用的每个命令的详细语法。

- **团队 skillset**: 您的团队是否具有现有专业技能？ 例如, 您的团队可能已使用 PowerShell 来管理 Windows。 如果是这样, 他们将很快就使用 Azure PowerShell 感到舒适。

## <a name="example"></a>示例
请记住, 您正在选择一个管理工具来为您的 CRM 应用程序创建测试环境。 您的管理员有两个需要执行的特定 Azure 任务:

1. 为每个测试类别 (计价单位、集成和接受) 创建一个资源组。
2. 在每一轮测试之前, 在每个资源组中创建多个虚拟机。

若要创建资源组, Azure 门户是一个合理的选择。 这些任务是一次性任务, 因此您不需要脚本即可执行这些任务。

查找最佳工具以创建虚拟机是一种更具挑战性的决策。 您需要创建其中的多个, 并且您需要重复执行此操作, 每周可能会发生多次。 这意味着你将需要自动化, 因此 Azure 门户不是一个好的选择。 在这种情况下, azure PowerShell 或 azure CLI 将满足你的需求。 如果你的团队成员有一些现有的 PowerShell 知识, 则 Azure PowerShell 可能是最佳匹配。 Azure PowerShell 可在您的管理员团队使用的操作系统上使用, 它支持自动化, 并且应快速为您的团队进行学习。

大多数管理员对 Azure 的首次体验都在门户中。 这是一个很好的起点, 因为它提供了清晰、结构良好的图形界面, 但提供了自动化的有限选项。 当你需要自动化时, azure 会为你提供两个选项: azure powershell for admins for admins with PowerShell 体验和 azure CLI for 其他所有人。

在实践中, 企业通常会组合一次性任务和重复性任务。 这意味着, 通常使用门户和脚本解决方案。 在我们的 CRM 示例中, 适合通过门户创建资源组, 并使用 PowerShell 自动执行 VM 创建。

本模块的其余部分重点介绍了如何安装和使用 Azure PowerShell。
