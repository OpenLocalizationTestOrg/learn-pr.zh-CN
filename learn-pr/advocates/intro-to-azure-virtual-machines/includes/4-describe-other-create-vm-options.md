Azure 门户是在你开始时创建资源 (如 vm) 的最简单方法。 但是, 不一定是使用 Azure 的最高效或最快的方法, 尤其是在需要创建多个资源的情况下。 在我们的示例中, 我们最终会创建数十个虚拟机来处理不同的任务。 在 Azure 门户中手动创建它们并不是一项有趣的任务!

让我们来看看在 Azure 中创建和管理资源的其他一些方法:

- Azure 资源管理器
- Azure PowerShell
- Azure CLI
- Azure REST API
- Azure 客户端 SDK
- Azure VM 扩展
- Azure 自动化服务

## <a name="azure-resource-manager"></a>Azure 资源管理器

假设您想要创建具有相同设置的 VM 副本。 你可以创建 VM 映像, 将其上载到 Azure, 并将其作为新 VM 的基础进行引用。 此过程效率低下且耗时。 Azure 为你提供了用于创建模板的选项, 可从该模板创建虚拟机的精确副本。

通常情况下, 您的 Azure 基础结构将包含许多资源, 其中许多资源以某种方式与其他资源相关。 例如, 我们创建的 VM 具有虚拟机本身、存储、网络接口、web 服务器和数据库-all 共同创建, 以运行 WordPress 网站。 **Azure 资源管理器**使与这些相关的资源的工作效率更高。 它将资源组织为已命名的**资源组**, 允许您同时部署、更新或删除所有资源。 创建 WordPress 站点时, 我们将资源组标识为 VM 创建的一部分, 资源管理器将相关联的资源放入同一个组。

资源管理器还允许您创建_模板_, 可用于创建和部署特定配置。

### <a name="what-are-resource-manager-templates"></a>什么是资源管理器模板？

**资源管理器模板**是 JSON 文件, 用于定义需要为解决方案部署的资源。

您可以通过选择 "自动化脚本" 选项, 从特定 VM 的 "**设置**" 部分创建资源模板。

![我们的虚拟机的自动化脚本](../media/4-automation-script.png)

您可以选择保存资源模板以供将来使用, 也可以立即部署基于此模板的新 VM。 例如, 您可以从测试环境中的模板创建 VM, 并发现它不能取代您的本地计算机。 您可以删除资源组, 这将删除所有资源, 并对模板进行调整, 然后重试。 如果只想对现有已部署的资源进行更改, 可以更改用于创建它的模板并再次部署它。 资源管理器将更改资源以与新模板相匹配。

按照您希望的方式工作后, 您可以获取该模板并轻松地重新创建多个版本的基础结构, 例如暂存和生产。 您可以使用不同的参数对每个环境进行自定义, 以对诸如 VM 名称、网络名称、存储帐户名称等字段进行参数化, 并重复加载模板。

您可以使用自动化脚本工具 (例如 azure CLI、azure PowerShell) 甚至 azure REST api 和喜欢的编程语言来处理资源模板, 从而使其成为快速旋转基础结构的强大工具。

## <a name="azure-powershell"></a>Azure PowerShell

创建管理脚本是优化工作流的一种有效方式。 您可以自动执行日常的重复性任务, 一旦脚本经过验证, 它将持续运行, 很可能会减少错误。 **Azure PowerShell**非常适合用于一次性交互任务和/或重复任务的自动化。

> [!NOTE]
> PowerShell 是跨平台命令行管理程序, 提供了命令行管理程序窗口和命令分析等服务。 Azure PowerShell 是可选的附加程序包, 可添加特定于 Azure 的命令 (称为**cmdlet**)。 您可以在单独的培训模块中了解有关安装和使用 Azure PowerShell 的详细信息。

例如, 可以使用`New-AzVM` cmdlet 创建新的 Azure 虚拟机。

```powershell
New-AzVm `
    -ResourceGroupName "TestResourceGroup" `
    -Name "test-wp1-eus-vm" `
    -Location "East US" `
    -VirtualNetworkName "test-wp1-eus-network" `
    -SubnetName "default" `
    -SecurityGroupName "test-wp1-eus-nsg" `
    -PublicIpAddressName "test-wp1-eus-pubip" `
    -OpenPorts 80,3389
```

如下所示, 提供各种参数来处理可用的大量 VM 配置设置。 大多数参数具有合理的值;您只需指定所需的参数。 通过使用 PowerShell 模块的脚本, 在**自动化 azure 任务**中了解如何使用 azure PowerShell 创建和管理 vm。

## <a name="azure-cli"></a>Azure CLI

脚本和命令行 azure 交互的另一个选项是**Azure CLI**。

azure CLI 是 Microsoft 跨平台命令行工具, 用于从命令行管理 Azure 资源 (例如虚拟机和磁盘)。 它可用于 macOS、Linux 和 Windows, 也可用于使用云命令行管理程序的浏览器中。 与 azure PowerShell 一样, azure CLI 也是简化管理工作流的一种强大方式。 与 azure PowerShell 不同, azure CLI 不需要 PowerShell 即可正常工作。

例如, 可以使用`az vm create`命令创建 Azure VM。

```azurecli
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image win2016datacenter \
    --admin-username jonc \
    --admin-password aReallyGoodPasswordHere
```

Azure CLI 可与其他脚本语言 (例如, Ruby 和 Python) 结合使用。 这两种语言通常用于非基于 Windows 的计算机上, 开发人员可能不熟悉 PowerShell。

详细了解如何**使用 Azure CLI 工具模块管理虚拟机中的虚拟机**来创建和管理虚拟机。

## <a name="programmatic-apis"></a>编程 (api)

一般来说, azure PowerShell 和 azure CLI 都是良好的选择, 如果你有运行简单的脚本并想要使用命令行工具。 当遇到更复杂的情况时, 在其中创建和管理 vm 的过程中构成了具有复杂逻辑的大型应用程序, 需要另一种方法。

您可以以编程方式与 Azure 中的每种类型的资源进行交互。

### <a name="azure-rest-api"></a>Azure REST API

Azure REST API 为开发人员提供了按资源分类的操作, 以及创建和管理虚拟机的能力。 操作`GET`通过相应的 HTTP 方法 (、 `PUT` `POST` `DELETE`、、和`PATCH`) 和相应的响应公开为 uri。

Azure 计算 api 使您能够以编程方式访问虚拟机及其支持资源。 使用此 API, 您可以执行以下操作:

- 创建和管理可用性集
- 添加和管理虚拟机扩展
- 创建和管理托管磁盘、快照和映像
- 访问 Azure 中可用的平台映像
- 检索资源的使用率信息
- 创建和管理虚拟机
- 创建和管理虚拟机扩展集

### <a name="azure-client-sdk"></a>Azure 客户端 SDK

尽管 REST API 是平台和语言不可知的, 但开发人员通常会更深入地了解更高级别的抽象。 azure 客户端 SDK 封装了 azure REST API, 使开发人员可以更轻松地与 azure 进行交互。

Azure 客户端 sdk 可用于多种语言和框架, 包括。基于网络的语言, 例如 c #、Java、node.js、PHP、Python、Ruby 和 Go。

以下是 c # 代码示例, 用于使用`Microsoft.Azure.Management.Fluent` NuGet 包创建 Azure VM:

```csharp
var azure = Azure
    .Configure()
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
// ...
var vmName = "test-wp1-eus-vm";

azure.VirtualMachines.Define(vmName)
    .WithRegion(Region.USEast)
    .WithExistingResourceGroup("TestResourceGroup")
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("jonc")
    .WithAdminPassword("aReallyGoodPasswordHere")
    .WithComputerName(vmName)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

下面是使用**Azure java SDK**的 Java 中的相同代码片段:

```java
String vmName = "test-wp1-eus-vm";
// ...
VirtualMachine virtualMachine = azure.virtualMachines()
    .define(vmName)
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("TestResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("jonc")
    .withAdminPassword("aReallyGoodPasswordHere")
    .withComputerName(vmName)
    .withSize("Standard_DS1")
    .create();
```

## <a name="azure-vm-extensions"></a>Azure VM 扩展

假设你想要在初始部署后在虚拟机上配置和安装其他软件。 您希望此任务使用特定的配置, 并自动进行监控和执行。

**azure VM 扩展**是小型应用程序, 可让你在初始部署后在 Azure vm 上配置和自动执行任务。 **azure VM 扩展**可与 azure CLI、PowerShell、azure 资源管理器模板和 azure 门户一起运行。

将扩展与新的 VM 部署捆绑在一起, 或对现有系统运行扩展。

## <a name="azure-automation-services"></a>Azure 自动化服务

在管理远程基础结构时, 节省时间、减少错误和提高效率是遇到的最重要的操作管理挑战。 如果您有大量的基础结构服务, 您可能需要考虑在 Azure 中使用更高级别的服务, 以帮助您从更高的级别进行操作。

通过**Azure 自动化**, 可以集成服务, 使您能够轻松地自动执行频繁、耗时且容易出错的管理任务。 这些服务包括**流程自动化**、**配置管理**和**更新管理**。

- **流程管理**。 假设您有一个针对特定错误事件监视的 VM。 您希望在报告问题时立即采取措施并修复问题。 通过进程自动化, 可以设置可响应数据中心中可能发生的事件的观察程序任务。

- **配置管理**。  或许您希望跟踪可用于在您的 VM 上运行的操作系统的软件更新。 您可能想要包含或排除特定的更新。 配置管理允许您跟踪这些更新并根据需要采取措施。 您可以使用**System Center Configuration Manager**管理公司的电脑、服务器和移动设备。 你可以使用 Configuration Manager 将此支持扩展到你的 Azure vm。

- **更新管理**。 这用于管理虚拟机的更新和修补程序。 使用此服务, 您可以评估可用更新的状态、计划安装并查看部署结果以验证是否成功应用了更新。 更新管理包含提供过程和配置管理的服务。 您可以从**Azure 自动化**帐户中直接启用对 VM 的更新管理。 您还可以从门户中的虚拟机边栏允许对单个虚拟机进行更新管理。

正如您所看到的, Azure 提供了多种工具来创建和管理资源, 以便您可以将管理操作集成到_适合您_的过程中。 让我们来看一下其他一些 Azure 服务, 以确保您的基础结构资源顺利运行。
