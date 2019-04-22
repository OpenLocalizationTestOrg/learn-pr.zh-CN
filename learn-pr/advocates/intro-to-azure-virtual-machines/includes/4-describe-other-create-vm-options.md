<span data-ttu-id="15c9b-101">Azure 门户是在你开始时创建资源 (如 vm) 的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="15c9b-101">The Azure portal is the easiest way to create resources such as VMs when you are getting started.</span></span> <span data-ttu-id="15c9b-102">但是, 不一定是使用 Azure 的最高效或最快的方法, 尤其是在需要创建多个资源的情况下。</span><span class="sxs-lookup"><span data-stu-id="15c9b-102">However, it's not necessarily the most efficient or quickest way to work with Azure, particularly if you need to create several resources together.</span></span> <span data-ttu-id="15c9b-103">在我们的示例中, 我们最终会创建数十个虚拟机来处理不同的任务。</span><span class="sxs-lookup"><span data-stu-id="15c9b-103">In our case, we will eventually be creating dozens of VMs to handle different tasks.</span></span> <span data-ttu-id="15c9b-104">在 Azure 门户中手动创建它们并不是一项有趣的任务!</span><span class="sxs-lookup"><span data-stu-id="15c9b-104">Creating them manually in the Azure portal wouldn't be a fun task!</span></span>

<span data-ttu-id="15c9b-105">让我们来看看在 Azure 中创建和管理资源的其他一些方法:</span><span class="sxs-lookup"><span data-stu-id="15c9b-105">Let's look at some other ways to create and administer resources in Azure:</span></span>

- <span data-ttu-id="15c9b-106">Azure 资源管理器</span><span class="sxs-lookup"><span data-stu-id="15c9b-106">Azure Resource Manager</span></span>
- <span data-ttu-id="15c9b-107">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15c9b-107">Azure PowerShell</span></span>
- <span data-ttu-id="15c9b-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15c9b-108">Azure CLI</span></span>
- <span data-ttu-id="15c9b-109">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="15c9b-109">Azure REST API</span></span>
- <span data-ttu-id="15c9b-110">Azure 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="15c9b-110">Azure Client SDK</span></span>
- <span data-ttu-id="15c9b-111">Azure VM 扩展</span><span class="sxs-lookup"><span data-stu-id="15c9b-111">Azure VM Extensions</span></span>
- <span data-ttu-id="15c9b-112">Azure 自动化服务</span><span class="sxs-lookup"><span data-stu-id="15c9b-112">Azure Automation Services</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="15c9b-113">Azure 资源管理器</span><span class="sxs-lookup"><span data-stu-id="15c9b-113">Azure Resource Manager</span></span>

<span data-ttu-id="15c9b-114">假设您想要创建具有相同设置的 VM 副本。</span><span class="sxs-lookup"><span data-stu-id="15c9b-114">Let's assume you want to create a copy of a VM with the same settings.</span></span> <span data-ttu-id="15c9b-115">你可以创建 VM 映像, 将其上载到 Azure, 并将其作为新 VM 的基础进行引用。</span><span class="sxs-lookup"><span data-stu-id="15c9b-115">You could create a VM image, upload it to Azure, and reference it as the basis for your new VM.</span></span> <span data-ttu-id="15c9b-116">此过程效率低下且耗时。</span><span class="sxs-lookup"><span data-stu-id="15c9b-116">This process is inefficient and time-consuming.</span></span> <span data-ttu-id="15c9b-117">Azure 为你提供了用于创建模板的选项, 可从该模板创建虚拟机的精确副本。</span><span class="sxs-lookup"><span data-stu-id="15c9b-117">Azure provides you with the option to create a template from which to create an exact copy of a VM.</span></span>

<span data-ttu-id="15c9b-118">通常情况下, 您的 Azure 基础结构将包含许多资源, 其中许多资源以某种方式与其他资源相关。</span><span class="sxs-lookup"><span data-stu-id="15c9b-118">Typically, your Azure infrastructure will contain many resources, many of them related to one another in some way.</span></span> <span data-ttu-id="15c9b-119">例如, 我们创建的 VM 具有虚拟机本身、存储、网络接口、web 服务器和数据库-all 共同创建, 以运行 WordPress 网站。</span><span class="sxs-lookup"><span data-stu-id="15c9b-119">For example, the VM we created has the virtual machine itself, storage, network interface, web server, and a database - all created together to run the WordPress site.</span></span> <span data-ttu-id="15c9b-120">**Azure 资源管理器**使与这些相关的资源的工作效率更高。</span><span class="sxs-lookup"><span data-stu-id="15c9b-120">**Azure Resource Manager** makes working with these related resources more efficient.</span></span> <span data-ttu-id="15c9b-121">它将资源组织为已命名的**资源组**, 允许您同时部署、更新或删除所有资源。</span><span class="sxs-lookup"><span data-stu-id="15c9b-121">It organizes resources into named **resource groups** that let you deploy, update, or delete all of the resources together.</span></span> <span data-ttu-id="15c9b-122">创建 WordPress 站点时, 我们将资源组标识为 VM 创建的一部分, 资源管理器将相关联的资源放入同一个组。</span><span class="sxs-lookup"><span data-stu-id="15c9b-122">When we created the WordPress site, we identified the resource group as part of the VM creation, and Resource Manager placed the associated resources into the same group.</span></span>

<span data-ttu-id="15c9b-123">资源管理器还允许您创建_模板_, 可用于创建和部署特定配置。</span><span class="sxs-lookup"><span data-stu-id="15c9b-123">Resource Manager also allows you to create _templates_, which can be used to create and deploy specific configurations.</span></span>

### <a name="what-are-resource-manager-templates"></a><span data-ttu-id="15c9b-124">什么是资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="15c9b-124">What are Resource Manager templates?</span></span>

<span data-ttu-id="15c9b-125">**资源管理器模板**是 JSON 文件, 用于定义需要为解决方案部署的资源。</span><span class="sxs-lookup"><span data-stu-id="15c9b-125">**Resource Manager templates** are JSON files that define the resources you need to deploy for your solution.</span></span>

<span data-ttu-id="15c9b-126">您可以通过选择 "自动化脚本" 选项, 从特定 VM 的 "**设置**" 部分创建资源模板。</span><span class="sxs-lookup"><span data-stu-id="15c9b-126">You can create resource templates from the **Settings** section for a specific VM by selecting the Automation script option.</span></span>

![我们的虚拟机的自动化脚本](../media/4-automation-script.png)

<span data-ttu-id="15c9b-128">您可以选择保存资源模板以供将来使用, 也可以立即部署基于此模板的新 VM。</span><span class="sxs-lookup"><span data-stu-id="15c9b-128">You have the option to save the resource template for later use or immediately deploy a new VM based on this template.</span></span> <span data-ttu-id="15c9b-129">例如, 您可以从测试环境中的模板创建 VM, 并发现它不能取代您的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="15c9b-129">For example, you might create a VM from a template in a test environment and find it doesn’t quite work to replace your on-premises machine.</span></span> <span data-ttu-id="15c9b-130">您可以删除资源组, 这将删除所有资源, 并对模板进行调整, 然后重试。</span><span class="sxs-lookup"><span data-stu-id="15c9b-130">You can delete the resource group, which deletes all of the resources, tweak the template, and try again.</span></span> <span data-ttu-id="15c9b-131">如果只想对现有已部署的资源进行更改, 可以更改用于创建它的模板并再次部署它。</span><span class="sxs-lookup"><span data-stu-id="15c9b-131">If you only want to make changes to the existing deployed resources, you can change the template used to create it and deploy it again.</span></span> <span data-ttu-id="15c9b-132">资源管理器将更改资源以与新模板相匹配。</span><span class="sxs-lookup"><span data-stu-id="15c9b-132">Resource Manager will change the resources to match the new template.</span></span>

<span data-ttu-id="15c9b-133">按照您希望的方式工作后, 您可以获取该模板并轻松地重新创建多个版本的基础结构, 例如暂存和生产。</span><span class="sxs-lookup"><span data-stu-id="15c9b-133">Once you have it working the way you want it, you can take that template and easily re-create multiple versions of your infrastructure, such as staging and production.</span></span> <span data-ttu-id="15c9b-134">您可以使用不同的参数对每个环境进行自定义, 以对诸如 VM 名称、网络名称、存储帐户名称等字段进行参数化, 并重复加载模板。</span><span class="sxs-lookup"><span data-stu-id="15c9b-134">You can parameterize fields such as the VM name, network name, storage account name, etc., and load the template repeatedly, using different parameters to customize each environment.</span></span>

<span data-ttu-id="15c9b-135">您可以使用自动化脚本工具 (例如 azure CLI、azure PowerShell) 甚至 azure REST api 和喜欢的编程语言来处理资源模板, 从而使其成为快速旋转基础结构的强大工具。</span><span class="sxs-lookup"><span data-stu-id="15c9b-135">You can use automation scripting tools such as the Azure CLI, Azure PowerShell, or even the Azure REST APIs with your favorite programming language to process resource templates, making this a powerful tool for quickly spinning up your infrastructure.</span></span>

## <a name="azure-powershell"></a><span data-ttu-id="15c9b-136">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15c9b-136">Azure PowerShell</span></span>

<span data-ttu-id="15c9b-137">创建管理脚本是优化工作流的一种有效方式。</span><span class="sxs-lookup"><span data-stu-id="15c9b-137">Creating administration scripts is a powerful way to optimize your workflow.</span></span> <span data-ttu-id="15c9b-138">您可以自动执行日常的重复性任务, 一旦脚本经过验证, 它将持续运行, 很可能会减少错误。</span><span class="sxs-lookup"><span data-stu-id="15c9b-138">You can automate everyday, repetitive tasks, and once a script has been verified, it will run consistently, likely reducing errors.</span></span> <span data-ttu-id="15c9b-139">**Azure PowerShell**非常适合用于一次性交互任务和/或重复任务的自动化。</span><span class="sxs-lookup"><span data-stu-id="15c9b-139">**Azure PowerShell** is ideal for one-off interactive tasks and/or the automation of repeated tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="15c9b-140">PowerShell 是跨平台命令行管理程序, 提供了命令行管理程序窗口和命令分析等服务。</span><span class="sxs-lookup"><span data-stu-id="15c9b-140">PowerShell is a cross-platform shell that provides services like the shell window and command parsing.</span></span> <span data-ttu-id="15c9b-141">Azure PowerShell 是可选的附加程序包, 可添加特定于 Azure 的命令 (称为**cmdlet**)。</span><span class="sxs-lookup"><span data-stu-id="15c9b-141">Azure PowerShell is an optional add-on package that adds the Azure-specific commands (referred to as **cmdlets**).</span></span> <span data-ttu-id="15c9b-142">您可以在单独的培训模块中了解有关安装和使用 Azure PowerShell 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="15c9b-142">You can learn more about installing and using Azure PowerShell in a separate training module.</span></span>

<span data-ttu-id="15c9b-143">例如, 可以使用`New-AzVM` cmdlet 创建新的 Azure 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="15c9b-143">For example, you can use the `New-AzVM` cmdlet to create a new Azure virtual machine.</span></span>

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

<span data-ttu-id="15c9b-144">如下所示, 提供各种参数来处理可用的大量 VM 配置设置。</span><span class="sxs-lookup"><span data-stu-id="15c9b-144">As shown here, you supply various parameters to handle the large number of VM configuration settings available.</span></span> <span data-ttu-id="15c9b-145">大多数参数具有合理的值;您只需指定所需的参数。</span><span class="sxs-lookup"><span data-stu-id="15c9b-145">Most of the parameters have reasonable values; you only need to specify the required parameters.</span></span> <span data-ttu-id="15c9b-146">通过使用 PowerShell 模块的脚本, 在**自动化 azure 任务**中了解如何使用 azure PowerShell 创建和管理 vm。</span><span class="sxs-lookup"><span data-stu-id="15c9b-146">Learn more about creating and managing VMs with Azure PowerShell in the **Automate Azure tasks using scripts with PowerShell** module.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="15c9b-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15c9b-147">Azure CLI</span></span>

<span data-ttu-id="15c9b-148">脚本和命令行 azure 交互的另一个选项是**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="15c9b-148">Another option for scripting and command-line Azure interaction is the **Azure CLI**.</span></span>

<span data-ttu-id="15c9b-149">azure CLI 是 Microsoft 跨平台命令行工具, 用于从命令行管理 Azure 资源 (例如虚拟机和磁盘)。</span><span class="sxs-lookup"><span data-stu-id="15c9b-149">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources such as virtual machines and disks from the command line.</span></span> <span data-ttu-id="15c9b-150">它可用于 macOS、Linux 和 Windows, 也可用于使用云命令行管理程序的浏览器中。</span><span class="sxs-lookup"><span data-stu-id="15c9b-150">It's available for macOS, Linux, and Windows, or in the browser using the Cloud Shell.</span></span> <span data-ttu-id="15c9b-151">与 azure PowerShell 一样, azure CLI 也是简化管理工作流的一种强大方式。</span><span class="sxs-lookup"><span data-stu-id="15c9b-151">Like Azure PowerShell, the Azure CLI is a powerful way to streamline your administrative workflow.</span></span> <span data-ttu-id="15c9b-152">与 azure PowerShell 不同, azure CLI 不需要 PowerShell 即可正常工作。</span><span class="sxs-lookup"><span data-stu-id="15c9b-152">Unlike Azure PowerShell, the Azure CLI does not need PowerShell to function.</span></span>

<span data-ttu-id="15c9b-153">例如, 可以使用`az vm create`命令创建 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="15c9b-153">For example, you can create an Azure VM with the `az vm create` command.</span></span>

```azurecli
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image win2016datacenter \
    --admin-username jonc \
    --admin-password aReallyGoodPasswordHere
```

<span data-ttu-id="15c9b-154">Azure CLI 可与其他脚本语言 (例如, Ruby 和 Python) 结合使用。</span><span class="sxs-lookup"><span data-stu-id="15c9b-154">The Azure CLI can be used with other scripting languages, for example, Ruby and Python.</span></span> <span data-ttu-id="15c9b-155">这两种语言通常用于非基于 Windows 的计算机上, 开发人员可能不熟悉 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="15c9b-155">Both languages are commonly used on non-Windows-based machines where the developer might not be familiar with PowerShell.</span></span>

<span data-ttu-id="15c9b-156">详细了解如何**使用 Azure CLI 工具模块管理虚拟机中的虚拟机**来创建和管理虚拟机。</span><span class="sxs-lookup"><span data-stu-id="15c9b-156">Learn more about creating and managing VMs in the **Manage virtual machines with the Azure CLI tool** module.</span></span>

## <a name="programmatic-apis"></a><span data-ttu-id="15c9b-157">编程 (api)</span><span class="sxs-lookup"><span data-stu-id="15c9b-157">Programmatic (APIs)</span></span>

<span data-ttu-id="15c9b-158">一般来说, azure PowerShell 和 azure CLI 都是良好的选择, 如果你有运行简单的脚本并想要使用命令行工具。</span><span class="sxs-lookup"><span data-stu-id="15c9b-158">Generally speaking, both Azure PowerShell and Azure CLI are good options if you have simple scripts to run and want to stick to command-line tools.</span></span> <span data-ttu-id="15c9b-159">当遇到更复杂的情况时, 在其中创建和管理 vm 的过程中构成了具有复杂逻辑的大型应用程序, 需要另一种方法。</span><span class="sxs-lookup"><span data-stu-id="15c9b-159">When it comes to more complex scenarios, where the creation and management of VMs form part of a larger application with complex logic, another approach is needed.</span></span>

<span data-ttu-id="15c9b-160">您可以以编程方式与 Azure 中的每种类型的资源进行交互。</span><span class="sxs-lookup"><span data-stu-id="15c9b-160">You can interact with every type of resource in Azure programmatically.</span></span>

### <a name="azure-rest-api"></a><span data-ttu-id="15c9b-161">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="15c9b-161">Azure REST API</span></span>

<span data-ttu-id="15c9b-162">Azure REST API 为开发人员提供了按资源分类的操作, 以及创建和管理虚拟机的能力。</span><span class="sxs-lookup"><span data-stu-id="15c9b-162">The Azure REST API provides developers with operations categorized by resource as well as the ability to create and manage VMs.</span></span> <span data-ttu-id="15c9b-163">操作`GET`通过相应的 HTTP 方法 (、 `PUT` `POST` `DELETE`、、和`PATCH`) 和相应的响应公开为 uri。</span><span class="sxs-lookup"><span data-stu-id="15c9b-163">Operations are exposed as URIs with corresponding HTTP methods (`GET`, `PUT`, `POST`, `DELETE`, and `PATCH`) and a corresponding response.</span></span>

<span data-ttu-id="15c9b-164">Azure 计算 api 使您能够以编程方式访问虚拟机及其支持资源。</span><span class="sxs-lookup"><span data-stu-id="15c9b-164">The Azure Compute APIs give you programmatic access to virtual machines and their supporting resources.</span></span> <span data-ttu-id="15c9b-165">使用此 API, 您可以执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="15c9b-165">With this API, you have operations to:</span></span>

- <span data-ttu-id="15c9b-166">创建和管理可用性集</span><span class="sxs-lookup"><span data-stu-id="15c9b-166">Create and manage availability sets</span></span>
- <span data-ttu-id="15c9b-167">添加和管理虚拟机扩展</span><span class="sxs-lookup"><span data-stu-id="15c9b-167">Add and manage virtual machine extensions</span></span>
- <span data-ttu-id="15c9b-168">创建和管理托管磁盘、快照和映像</span><span class="sxs-lookup"><span data-stu-id="15c9b-168">Create and manage managed disks, snapshots, and images</span></span>
- <span data-ttu-id="15c9b-169">访问 Azure 中可用的平台映像</span><span class="sxs-lookup"><span data-stu-id="15c9b-169">Access the platform images available in Azure</span></span>
- <span data-ttu-id="15c9b-170">检索资源的使用率信息</span><span class="sxs-lookup"><span data-stu-id="15c9b-170">Retrieve usage information of your resources</span></span>
- <span data-ttu-id="15c9b-171">创建和管理虚拟机</span><span class="sxs-lookup"><span data-stu-id="15c9b-171">Create and manage virtual machines</span></span>
- <span data-ttu-id="15c9b-172">创建和管理虚拟机扩展集</span><span class="sxs-lookup"><span data-stu-id="15c9b-172">Create and manage virtual machine scale sets</span></span>

### <a name="azure-client-sdk"></a><span data-ttu-id="15c9b-173">Azure 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="15c9b-173">Azure Client SDK</span></span>

<span data-ttu-id="15c9b-174">尽管 REST API 是平台和语言不可知的, 但开发人员通常会更深入地了解更高级别的抽象。</span><span class="sxs-lookup"><span data-stu-id="15c9b-174">Even though the REST API is platform and language agnostic, most often developers will look toward a higher level of abstraction.</span></span> <span data-ttu-id="15c9b-175">azure 客户端 SDK 封装了 azure REST API, 使开发人员可以更轻松地与 azure 进行交互。</span><span class="sxs-lookup"><span data-stu-id="15c9b-175">The Azure Client SDK encapsulates the Azure REST API, making it much easier for developers to interact with Azure.</span></span>

<span data-ttu-id="15c9b-176">Azure 客户端 sdk 可用于多种语言和框架, 包括。基于网络的语言, 例如 c #、Java、node.js、PHP、Python、Ruby 和 Go。</span><span class="sxs-lookup"><span data-stu-id="15c9b-176">The Azure Client SDKs are available for a variety of languages and frameworks, including .NET-based languages such as C#, Java, Node.js, PHP, Python, Ruby, and Go.</span></span>

<span data-ttu-id="15c9b-177">以下是 c # 代码示例, 用于使用`Microsoft.Azure.Management.Fluent` NuGet 包创建 Azure VM:</span><span class="sxs-lookup"><span data-stu-id="15c9b-177">Here's an example snippet of C# code to create an Azure VM using the `Microsoft.Azure.Management.Fluent` NuGet package:</span></span>

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

<span data-ttu-id="15c9b-178">下面是使用**Azure java SDK**的 Java 中的相同代码片段:</span><span class="sxs-lookup"><span data-stu-id="15c9b-178">Here's the same snippet in Java using the **Azure Java SDK**:</span></span>

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

## <a name="azure-vm-extensions"></a><span data-ttu-id="15c9b-179">Azure VM 扩展</span><span class="sxs-lookup"><span data-stu-id="15c9b-179">Azure VM Extensions</span></span>

<span data-ttu-id="15c9b-180">假设你想要在初始部署后在虚拟机上配置和安装其他软件。</span><span class="sxs-lookup"><span data-stu-id="15c9b-180">Let's assume you want to configure and install additional software on your virtual machine after the initial deployment.</span></span> <span data-ttu-id="15c9b-181">您希望此任务使用特定的配置, 并自动进行监控和执行。</span><span class="sxs-lookup"><span data-stu-id="15c9b-181">You want this task to use a specific configuration, monitored and executed automatically.</span></span>

<span data-ttu-id="15c9b-182">**azure VM 扩展**是小型应用程序, 可让你在初始部署后在 Azure vm 上配置和自动执行任务。</span><span class="sxs-lookup"><span data-stu-id="15c9b-182">**Azure VM extensions** are small applications that allow you to configure and automate tasks on Azure VMs after initial deployment.</span></span> <span data-ttu-id="15c9b-183">**azure VM 扩展**可与 azure CLI、PowerShell、azure 资源管理器模板和 azure 门户一起运行。</span><span class="sxs-lookup"><span data-stu-id="15c9b-183">**Azure VM extensions** can be run with the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span>

<span data-ttu-id="15c9b-184">将扩展与新的 VM 部署捆绑在一起, 或对现有系统运行扩展。</span><span class="sxs-lookup"><span data-stu-id="15c9b-184">You bundle extensions with a new VM deployment or run them against an existing system.</span></span>

## <a name="azure-automation-services"></a><span data-ttu-id="15c9b-185">Azure 自动化服务</span><span class="sxs-lookup"><span data-stu-id="15c9b-185">Azure Automation Services</span></span>

<span data-ttu-id="15c9b-186">在管理远程基础结构时, 节省时间、减少错误和提高效率是遇到的最重要的操作管理挑战。</span><span class="sxs-lookup"><span data-stu-id="15c9b-186">Saving time, reducing errors, and increasing efficiency are some of the most significant operational management challenges faced when managing remote infrastructure.</span></span> <span data-ttu-id="15c9b-187">如果您有大量的基础结构服务, 您可能需要考虑在 Azure 中使用更高级别的服务, 以帮助您从更高的级别进行操作。</span><span class="sxs-lookup"><span data-stu-id="15c9b-187">If you have a lot of infrastructure services, you might want to consider using higher-level services in Azure to help you operate from a higher level.</span></span>

<span data-ttu-id="15c9b-188">通过**Azure 自动化**, 可以集成服务, 使您能够轻松地自动执行频繁、耗时且容易出错的管理任务。</span><span class="sxs-lookup"><span data-stu-id="15c9b-188">**Azure Automation** allows you to integrate services that allow you to automate frequent, time-consuming, and error-prone management tasks with ease.</span></span> <span data-ttu-id="15c9b-189">这些服务包括**流程自动化**、**配置管理**和**更新管理**。</span><span class="sxs-lookup"><span data-stu-id="15c9b-189">These services include **process automation**, **configuration management**, and **update management**.</span></span>

- <span data-ttu-id="15c9b-190">**流程管理**。</span><span class="sxs-lookup"><span data-stu-id="15c9b-190">**Process Management**.</span></span> <span data-ttu-id="15c9b-191">假设您有一个针对特定错误事件监视的 VM。</span><span class="sxs-lookup"><span data-stu-id="15c9b-191">Let's assume you have a VM that is monitored for a specific error event.</span></span> <span data-ttu-id="15c9b-192">您希望在报告问题时立即采取措施并修复问题。</span><span class="sxs-lookup"><span data-stu-id="15c9b-192">You want to take action and fix the problem as soon as it's reported.</span></span> <span data-ttu-id="15c9b-193">通过进程自动化, 可以设置可响应数据中心中可能发生的事件的观察程序任务。</span><span class="sxs-lookup"><span data-stu-id="15c9b-193">Process automation allows you to set up watcher tasks that can respond to events that may occur in your datacenter.</span></span>

- <span data-ttu-id="15c9b-194">**配置管理**。</span><span class="sxs-lookup"><span data-stu-id="15c9b-194">**Configuration Management**.</span></span>  <span data-ttu-id="15c9b-195">或许您希望跟踪可用于在您的 VM 上运行的操作系统的软件更新。</span><span class="sxs-lookup"><span data-stu-id="15c9b-195">Perhaps you want to track software updates that become available for the operating system that runs on your VM.</span></span> <span data-ttu-id="15c9b-196">您可能想要包含或排除特定的更新。</span><span class="sxs-lookup"><span data-stu-id="15c9b-196">There are specific updates you may want to include or exclude.</span></span> <span data-ttu-id="15c9b-197">配置管理允许您跟踪这些更新并根据需要采取措施。</span><span class="sxs-lookup"><span data-stu-id="15c9b-197">Configuration management allows you to track these updates and take action as required.</span></span> <span data-ttu-id="15c9b-198">您可以使用**System Center Configuration Manager**管理公司的电脑、服务器和移动设备。</span><span class="sxs-lookup"><span data-stu-id="15c9b-198">You use **System Center Configuration Manager** to manage your company's PC, servers, and mobile devices.</span></span> <span data-ttu-id="15c9b-199">你可以使用 Configuration Manager 将此支持扩展到你的 Azure vm。</span><span class="sxs-lookup"><span data-stu-id="15c9b-199">You can extend this support to your Azure VMs with Configuration Manager.</span></span>

- <span data-ttu-id="15c9b-200">**更新管理**。</span><span class="sxs-lookup"><span data-stu-id="15c9b-200">**Update Management**.</span></span> <span data-ttu-id="15c9b-201">这用于管理虚拟机的更新和修补程序。</span><span class="sxs-lookup"><span data-stu-id="15c9b-201">This is used to manage updates and patches for your VMs.</span></span> <span data-ttu-id="15c9b-202">使用此服务, 您可以评估可用更新的状态、计划安装并查看部署结果以验证是否成功应用了更新。</span><span class="sxs-lookup"><span data-stu-id="15c9b-202">With this service, you're able to assess the status of available updates, schedule installation, and review deployment results to verify updates applied successfully.</span></span> <span data-ttu-id="15c9b-203">更新管理包含提供过程和配置管理的服务。</span><span class="sxs-lookup"><span data-stu-id="15c9b-203">Update management incorporates services that provide process and configuration management.</span></span> <span data-ttu-id="15c9b-204">您可以从**Azure 自动化**帐户中直接启用对 VM 的更新管理。</span><span class="sxs-lookup"><span data-stu-id="15c9b-204">You enable update management for a VM directly from your **Azure Automation** account.</span></span> <span data-ttu-id="15c9b-205">您还可以从门户中的虚拟机边栏允许对单个虚拟机进行更新管理。</span><span class="sxs-lookup"><span data-stu-id="15c9b-205">You can also allow update management for a single virtual machine from the virtual machine blade in the portal.</span></span>

<span data-ttu-id="15c9b-206">正如您所看到的, Azure 提供了多种工具来创建和管理资源, 以便您可以将管理操作集成到_适合您_的过程中。</span><span class="sxs-lookup"><span data-stu-id="15c9b-206">As you can see, Azure provides a variety of tools to create and administer resources so that you can integrate management operations into a process _that works for you_.</span></span> <span data-ttu-id="15c9b-207">让我们来看一下其他一些 Azure 服务, 以确保您的基础结构资源顺利运行。</span><span class="sxs-lookup"><span data-stu-id="15c9b-207">Let's examine some of the other Azure services to make sure your infrastructure resources are running smoothly.</span></span>
