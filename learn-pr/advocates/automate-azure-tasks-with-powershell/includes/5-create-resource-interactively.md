<span data-ttu-id="3f0fa-101">PowerShell 允许您编写命令并立即执行它们。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-101">PowerShell lets you write commands and execute them immediately.</span></span> <span data-ttu-id="3f0fa-102">这称为 "**交互模式**"。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-102">This is known as **interactive mode**.</span></span>

<span data-ttu-id="3f0fa-103">请记住, 客户关系管理 (CRM) 示例中的总体目标是创建三个包含 vm 的测试环境。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-103">Recall that the overall goal in the Customer Relationship Management (CRM) example is to create three test environments containing VMs.</span></span> <span data-ttu-id="3f0fa-104">您将使用资源组来确保将 vm 组织到单独的环境中: 一个用于单元测试, 一个用于集成测试, 另一个用于验收测试。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-104">You will use resource groups to ensure the VMs are organized into separate environments: one for unit testing, one for integration testing, and one for acceptance testing.</span></span> <span data-ttu-id="3f0fa-105">您只需创建一次资源组, 这就意味着使用 PowerShell 的交互模式是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-105">You only need to create the resource groups once, which means using the interactive mode of PowerShell is a good choice.</span></span>

<span data-ttu-id="3f0fa-106">当您在 PowerShell 中键入命令时, 它会将它与执行请求的操作的_cmdlet_相匹配。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-106">When you type a command into PowerShell, it matches it to a _cmdlet_ which then performs the requested action.</span></span> <span data-ttu-id="3f0fa-107">我们将介绍您可以使用的一些常见命令, 然后查看如何安装适用于 PowerShell 的 Azure 支持。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-107">We're going to look at some of the common commands you can use, and then look at installing the Azure support for PowerShell.</span></span>

## <a name="what-are-powershell-cmdlets"></a><span data-ttu-id="3f0fa-108">什么是 PowerShell cmdlet？</span><span class="sxs-lookup"><span data-stu-id="3f0fa-108">What are PowerShell cmdlets?</span></span>
<span data-ttu-id="3f0fa-109">PowerShell 命令称为**cmdlet** (发音为 "命令-let")。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-109">A PowerShell command is called a **cmdlet** (pronounced "command-let").</span></span> <span data-ttu-id="3f0fa-110">cmdlet 是操纵单个功能的命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-110">A cmdlet is a command that manipulates a single feature.</span></span> <span data-ttu-id="3f0fa-111">术语 " **cmdlet** " 旨在暗示 "小型命令"。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-111">The term **cmdlet** is intended to imply "small command".</span></span> <span data-ttu-id="3f0fa-112">根据约定, 应鼓励 cmdlet 作者将 cmdlet 保留为简单和单一用途。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-112">By convention, cmdlet authors are encouraged to keep cmdlets simple and single-purpose.</span></span>

<span data-ttu-id="3f0fa-113">基本 PowerShell 产品附带使用可处理诸如会话和后台作业等功能的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-113">The base PowerShell product ships with cmdlets that work with features such as sessions and background jobs.</span></span> <span data-ttu-id="3f0fa-114">将模块添加到 PowerShell 安装中, 以获取操作其他功能的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-114">You add modules to your PowerShell installation to get cmdlets that manipulate other features.</span></span> <span data-ttu-id="3f0fa-115">例如, 有第三方模块可以使用 ftp、管理操作系统、访问文件系统等。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-115">For example, there are third-party modules to work with ftp, administer your operating system, access the file system, and so on.</span></span>

<span data-ttu-id="3f0fa-116">cmdlet 遵循动词-名词命名约定;例如, "**进程**"、"**格式表**" 和 "**启动服务**"。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-116">Cmdlets follow a verb-noun naming convention; for example, **Get-Process**, **Format-Table**, and **Start-Service**.</span></span> <span data-ttu-id="3f0fa-117">还有一种谓词选择约定: "获取" 以检索数据、"设置" 以插入或更新数据、"格式" 以设置数据格式, "输出" 以将输出定向到目标, 等等。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-117">There is also a convention for verb choice: "get" to retrieve data, "set" to insert or update data, "format" to format data, "out" to direct output to a destination, and so on.</span></span>

<span data-ttu-id="3f0fa-118">建议使用 cmdlet 作者为每个 cmdlet 包含一个帮助文件。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-118">Cmdlet authors are encouraged to include a help file for each cmdlet.</span></span> <span data-ttu-id="3f0fa-119">**get-help** cmdlet 显示任何 cmdlet 的帮助文件。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-119">The **Get-Help** cmdlet displays the help file for any cmdlet.</span></span> <span data-ttu-id="3f0fa-120">例如, 我们可以使用以下语句获取有关`Get-ChildItem` cmdlet 的帮助:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-120">For example, we could get help on the `Get-ChildItem` cmdlet with the following statement:</span></span>

```powershell
Get-Help Get-ChildItem -detailed
```

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="3f0fa-121">什么是 PowerShell 模块？</span><span class="sxs-lookup"><span data-stu-id="3f0fa-121">What is a PowerShell module?</span></span>

<span data-ttu-id="3f0fa-122">cmdlet 是在_模块_中发货的。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-122">Cmdlets are shipped in _modules_.</span></span> <span data-ttu-id="3f0fa-123">PowerShell 模块是一个 DLL, 其中包含用于 proces 每个可用 cmdlet 的代码。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-123">A PowerShell Module is a DLL that includes the code to proces each available cmdlet.</span></span> <span data-ttu-id="3f0fa-124">您可以通过加载其包含的模块将 cmdlet 加载到 PowerShell 中。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-124">You load cmdlets into PowerShell by loading the module they are contained in.</span></span> <span data-ttu-id="3f0fa-125">您可以使用`Get-Module`命令获取加载的模块的列表:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-125">You can get a list of loaded modules using the `Get-Module` command:</span></span>

```powershell
Get-Module
```

<span data-ttu-id="3f0fa-126">这将输出如下内容:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-126">This will output something like:</span></span>

```output
ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Find-PackageProvider, Get-Package, Get-Pack...
Script     1.0.0.1    PowerShellGet                       {Find-Command, Find-DscResource, Find-Module, Find-RoleCap...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```

## <a name="what-is-the-az-module"></a><span data-ttu-id="3f0fa-127">什么是 Az 模块？</span><span class="sxs-lookup"><span data-stu-id="3f0fa-127">What is the Az module?</span></span>
<span data-ttu-id="3f0fa-128">**Az**是 Azure PowerShell 模块的正式名称, 其中包含使用 azure 功能的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-128">**Az** is the formal name for the Azure PowerShell module containing cmdlets to work with Azure features.</span></span> <span data-ttu-id="3f0fa-129">它包含数以百计的 cmdlet, 可让你控制每个 Azure 资源的几乎每个方面。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-129">It contains hundreds of cmdlets that let you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="3f0fa-130">您可以使用资源组、存储、虚拟机、Azure Active Directory、容器、机器学习等。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-130">You can work with resource groups, storage, virtual machines, Azure Active Directory, containers, machine learning, and so on.</span></span> <span data-ttu-id="3f0fa-131">此模块是[GitHub 上提供](https://github.com/Azure/azure-powershell)的开放源组件。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-131">This module is an open source component [available on GitHub](https://github.com/Azure/azure-powershell).</span></span>

> [!NOTE]
> <span data-ttu-id="3f0fa-132">您可能已看到或使用了`-AzureRM`使用格式的 Azure PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-132">You may have seen or used Azure PowerShell commands that used a `-AzureRM` format.</span></span> <span data-ttu-id="3f0fa-133">在10月 2018, 我们宣布将**AzureRM**模块替换为**Az**模块。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-133">In October 2018 we announced the replacement of the **AzureRM** module with the **Az** module.</span></span> <span data-ttu-id="3f0fa-134">此新模块具有多个功能, 尤其是短的 cmdlet 名词`-Az`前缀 ( `-AzureRM`而不是)。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-134">This new module has several features, notably a shortened cmdlet noun prefix of `-Az` instead of `-AzureRM`.</span></span> <span data-ttu-id="3f0fa-135">**Az**模块附带了与**AzureRM**模块的向后兼容性, `-AzureRM`因此该 cmdlet 格式将起作用, 但您应转换到**Az**模块并`-Az`使用前接个命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-135">The **Az** module ships with backwards compatibility with the **AzureRM** module so the `-AzureRM` cmdlet format will work, but you should transition to the **Az** module and use the `-Az` commands going forward.</span></span>

### <a name="install-the-az-module"></a><span data-ttu-id="3f0fa-136">安装 Az 模块</span><span class="sxs-lookup"><span data-stu-id="3f0fa-136">Install the Az module</span></span>

<span data-ttu-id="3f0fa-137">Az 模块可从称为 PowerShell 库的全局存储库中获取。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-137">The Az module is available from a global repository called the PowerShell Gallery.</span></span> <span data-ttu-id="3f0fa-138">您可以通过`Install-Module`命令将模块安装到本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-138">You can install the module onto your local machine through the `Install-Module` command.</span></span> <span data-ttu-id="3f0fa-139">您需要提升的 powershell 命令行管理程序才能从 PowerShell 库安装模块。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-139">You need an elevated PowerShell shell to install modules from the PowerShell Gallery.</span></span> 

::: zone pivot="windows"

<span data-ttu-id="3f0fa-140">若要安装最新的 Azure PowerShell 模块, 请运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-140">To install the latest Azure PowerShell module, run the following commands:</span></span>

1. <span data-ttu-id="3f0fa-141">打开 "**开始**" 菜单并键入**Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-141">Open the **Start** menu and type **Windows PowerShell**.</span></span>

1. <span data-ttu-id="3f0fa-142">右键单击 " **Windows PowerShell** " 图标, 然后选择 "**以管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-142">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>

1. <span data-ttu-id="3f0fa-143">在 "**用户帐户控制**" 对话框中, 选择 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-143">In the **User Account Control** dialog, select **Yes**.</span></span>

1. <span data-ttu-id="3f0fa-144">键入以下命令, 然后按 enter:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-144">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name Az -AllowClobber
    ```

<span data-ttu-id="3f0fa-145">这将默认安装所有用户的模块 (由 scope 参数控制)。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-145">This installs the module for all users by default (controlled by the scope parameter).</span></span>

<span data-ttu-id="3f0fa-146">该命令依赖 nuget 检索组件, 具体取决于您已安装的 nuget 版本, 您可能会收到下载并安装最新版本的 nuget 的提示。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-146">The command relies on NuGet to retrieve components, depending on the version of NuGet you have installed you might get a prompt to download and install the latest version of NuGet.</span></span>

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files (x86)\PackageManagement\ProviderAssemblies' or
'C:\Users\<username>\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import
 the NuGet provider now?
```

<span data-ttu-id="3f0fa-147">默认情况下, 不会将 PowerShell 库配置为 PowerShellGet 的受信任存储库。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-147">By default, the PowerShell gallery isn't configured as a trusted repository for PowerShellGet.</span></span> <span data-ttu-id="3f0fa-148">第一次使用 PSGallery 时, 您会看到以下提示:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-148">The first time you use the PSGallery you see the following prompt:</span></span>

```output
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
```

#### <a name="script-execution-failed"></a><span data-ttu-id="3f0fa-149">脚本执行失败</span><span class="sxs-lookup"><span data-stu-id="3f0fa-149">Script execution failed</span></span>
<span data-ttu-id="3f0fa-150">根据您的安全配置, `Import-Module`可能会失败, 如以下内容。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-150">Depending on your security configuration, `Import-Module` might fail with something like the following.</span></span>

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

<span data-ttu-id="3f0fa-151">这通常表示执行策略为 "受限制", 这意味着您不能执行从外部源 (包括 PowerShell 库) 下载的模块。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-151">This normally indicates that the execution policy is "restricted", meaning you can't execute modules you download from an external source - including the PowerShell gallery.</span></span> <span data-ttu-id="3f0fa-152">您可以通过执行命令`Get-ExecutionPolicy`来检查是否属于这种情况。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-152">You can check whether this is the case by executing the command `Get-ExecutionPolicy`.</span></span> <span data-ttu-id="3f0fa-153">如果它返回 "受限", 则执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-153">If it returns "Restricted", then do the following:</span></span>

1. <span data-ttu-id="3f0fa-154">打开提升的 PowerShell 命令提示符。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-154">Open an elevated PowerShell command prompt.</span></span>
1. <span data-ttu-id="3f0fa-155">使用`SetExecutionPolicy` cmdlet 将策略更改为 "RemoteSigned":</span><span class="sxs-lookup"><span data-stu-id="3f0fa-155">Use the `SetExecutionPolicy` cmdlet to change the policy to "RemoteSigned":</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<span data-ttu-id="3f0fa-156">这将提示你获取权限:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-156">This will prompt you for permission:</span></span>

```output
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

<span data-ttu-id="3f0fa-157">然后, 您应该能够使用`Import-Module`加载 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-157">You should then be able to use `Import-Module` to load the cmdlets.</span></span>

:::zone-end

::: zone pivot="linux,macos"

<span data-ttu-id="3f0fa-158">我们使用相同的命令在 Linux 或 macOS 上安装 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-158">We use the same commands to install the Azure PowerShell on either Linux or macOS.</span></span>

1. <span data-ttu-id="3f0fa-159">在终端中, 键入以下命令以使用提升的权限启动 PowerShell Core。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-159">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="3f0fa-160">在 PowerShell Core 提示符处运行以下命令, 以安装 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-160">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module Az -AllowClobber
    ```

1. <span data-ttu-id="3f0fa-161">如果系统询问您是否信任**PSGallery**中的模块, 回答 **"是"** 或 **"是" 全部**。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-161">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

:::zone-end

### <a name="update-a-module"></a><span data-ttu-id="3f0fa-162">更新模块</span><span class="sxs-lookup"><span data-stu-id="3f0fa-162">Update a module</span></span>

<span data-ttu-id="3f0fa-163">如果您收到一条警告或错误消息, 指示已安装 Azure PowerShell 模块的某个版本, 则可以通过发出以下命令更新到_最新_版本:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-163">If you get a warning or error message indicating that a version of the Azure PowerShell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>

```powershell
Update-Module -Name Az
```

<span data-ttu-id="3f0fa-164">与`Install-Module`命令一样, 当系统提示您信任模块时, 回答 **"是"** 或 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-164">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span> <span data-ttu-id="3f0fa-165">如果遇到问题, 还`Update-Module`可以使用命令重新安装模块。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-165">You can also use the `Update-Module` command to re-install a module if you are having trouble with it.</span></span>

## <a name="example-how-to-create-a-resource-group-with-azure-powershell"></a><span data-ttu-id="3f0fa-166">示例: 如何使用 Azure PowerShell 创建资源组</span><span class="sxs-lookup"><span data-stu-id="3f0fa-166">Example: How to create a resource group with Azure PowerShell</span></span>
<span data-ttu-id="3f0fa-167">加载 azure 模块后, 即可开始使用 azure。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-167">Once you have the Azure module loaded, you can begin working with Azure.</span></span> <span data-ttu-id="3f0fa-168">我们来创建一个常见的任务-创建一个资源组。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-168">Let's do a common task - create a Resource Group.</span></span> <span data-ttu-id="3f0fa-169">如你所知, 我们使用资源组来管理相关的资源。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-169">As you know, we use resource groups to administer related resources together.</span></span> <span data-ttu-id="3f0fa-170">创建新的资源组是您在启动新的 Azure 解决方案时要执行的第一项任务。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-170">Creating a new resource group is one of the first tasks you'll do when starting a new Azure solution.</span></span>

<span data-ttu-id="3f0fa-171">我们需要执行四个步骤:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-171">There are four steps we need to perform:</span></span>

1. <span data-ttu-id="3f0fa-172">导入 Azure cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-172">Import the Azure cmdlets.</span></span>

1. <span data-ttu-id="3f0fa-173">连接到你的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-173">Connect to your Azure subscription.</span></span>

1. <span data-ttu-id="3f0fa-174">创建资源组。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-174">Create the resource group.</span></span>

1. <span data-ttu-id="3f0fa-175">验证创建是否成功 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-175">Verify that creation was successful (see below).</span></span>

<span data-ttu-id="3f0fa-176">下图显示了这些步骤的概述。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-176">The following illustration shows an overview of these steps.</span></span>

![显示创建资源组的步骤的插图。](../media/5-create-resource-overview.png)

<span data-ttu-id="3f0fa-178">每个步骤对应不同的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-178">Each step corresponds to a different cmdlet.</span></span>

### <a name="import-the-azure-cmdlets"></a><span data-ttu-id="3f0fa-179">导入 Azure cmdlet</span><span class="sxs-lookup"><span data-stu-id="3f0fa-179">Import the Azure cmdlets</span></span>
<span data-ttu-id="3f0fa-180">启动时, PowerShell 仅在默认情况下加载核心 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-180">At startup, PowerShell loads only the core cmdlets by default.</span></span> <span data-ttu-id="3f0fa-181">这意味着你需要使用 Azure 的 cmdlet 将不会加载。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-181">This means the cmdlets you need to work with Azure won't be loaded.</span></span> <span data-ttu-id="3f0fa-182">若要加载所需的 cmdlet, 最可靠的方法是在 PowerShell 会话开始时手动导入这些 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-182">The most reliable way to load the cmdlets you need is to import them manually at the start of your PowerShell session.</span></span>

<span data-ttu-id="3f0fa-183">您可以使用**导入模块**cmdlet 加载模块。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-183">You use the **Import-Module** cmdlet to load modules.</span></span> <span data-ttu-id="3f0fa-184">此 cmdlet 具有许多用于处理各种情况的参数。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-184">This cmdlet has many parameters to handle a variety of situations.</span></span> <span data-ttu-id="3f0fa-185">例如, 它可以加载多个模块、特定模块版本、模块的一部分, 等等。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-185">For example, it can load multiple modules, a specific module version, part of a module, and so on.</span></span>

<span data-ttu-id="3f0fa-186">例如,**在提升的 PowerShell 会话中**, 我们可以使用以下命令加载 Az 的所有 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-186">For example, we can load all the cmdlets for Az with the following command **in an elevated PowerShell session**:</span></span>

```powershell
Import-Module Az
```

> [!TIP]
> <span data-ttu-id="3f0fa-187">如果你发现频繁使用 Azure PowerShell, 可以通过两种方法来自动执行模块加载过程。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-187">If you find that you work with Azure PowerShell frequently, there are two ways you can automate the module-loading process.</span></span> <span data-ttu-id="3f0fa-188">您可以向 powershell 配置文件中添加条目, 以在启动时导入 Azure 模块, 或使用最新版本的 powershell, 在使用 cmdlet 时自动加载包含模块。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-188">You can add an entry to your PowerShell profile to import the Azure module at startup or use the latest versions of PowerShell, which loads the containing module automatically when you use a cmdlet.</span></span>

### <a name="connect"></a><span data-ttu-id="3f0fa-189">连接</span><span class="sxs-lookup"><span data-stu-id="3f0fa-189">Connect</span></span>
<span data-ttu-id="3f0fa-190">当您使用 azure PowerShell 的本地安装时, 需要先进行身份验证, 然后才能执行 azure 命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-190">When you are working with a local install of Azure PowerShell, you will need to authenticate before you can execute Azure commands.</span></span> <span data-ttu-id="3f0fa-191">**AzAccount** cmdlet 会提示你输入 azure 凭据, 然后连接到你的 azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-191">The **Connect-AzAccount** cmdlet prompts for your Azure credentials and then connects to your Azure subscription.</span></span> <span data-ttu-id="3f0fa-192">它具有多个可选参数, 但如果您只需要交互式提示, 则不需要任何参数:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-192">It has many optional parameters, but if all you need is an interactive prompt, no parameters are needed:</span></span>

```powershell
Connect-AzAccount
```

<span data-ttu-id="3f0fa-193">您需要对您启动的每个新 PowerShell 会话重复这些步骤, 因为此模块不是核心集的一部分。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-193">You'll need to repeat these steps for every new PowerShell session you start since this module is not part of the core set.</span></span>


### <a name="working-with-subscriptions"></a><span data-ttu-id="3f0fa-194">使用订阅</span><span class="sxs-lookup"><span data-stu-id="3f0fa-194">Working with subscriptions</span></span>
<span data-ttu-id="3f0fa-195">如果你不熟悉 Azure, 你可能只有一个订阅。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-195">If you are new to Azure, you probably only have a single subscription.</span></span> <span data-ttu-id="3f0fa-196">但是, 如果你已使用 Azure 一段时间, 则可能已创建了多个 azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-196">But if you have been using Azure for a while, you may have created multiple Azure subscriptions.</span></span> <span data-ttu-id="3f0fa-197">您可以将 Azure PowerShell 配置为对特定订阅执行命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-197">You can configure Azure PowerShell to execute commands against a particular subscription.</span></span>

<span data-ttu-id="3f0fa-198">一次只能在一个订阅中。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-198">You can only be in one subscription at a time.</span></span> <span data-ttu-id="3f0fa-199">使用`Get-AzContext` cmdlet 确定哪个订阅处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-199">Use the `Get-AzContext` cmdlet to determine which subscription is active.</span></span> <span data-ttu-id="3f0fa-200">如果不正确, 可以对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-200">If it's not the correct one, you can change it.</span></span>

1. <span data-ttu-id="3f0fa-201">使用`Get-AzSubscription`命令获取帐户中所有订阅名称的列表。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-201">Get a list of all subscription names in your account with the `Get-AzSubscription` command.</span></span> 

2. <span data-ttu-id="3f0fa-202">通过传递要选择的订阅的名称来更改订阅。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-202">Change the subscription by passing the name of the one to select.</span></span>

```powershell
Select-AzSubscription -Subscription "Visual Studio Enterprise"
```

### <a name="get-a-list-of-all-resource-groups"></a><span data-ttu-id="3f0fa-203">获取所有资源组的列表</span><span class="sxs-lookup"><span data-stu-id="3f0fa-203">Get a list of all Resource Groups</span></span>

<span data-ttu-id="3f0fa-204">您可以检索活动订阅中的所有资源组的列表:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-204">You can retrieve a list of all Resource Groups in the active subscription:</span></span>

```powershell
Get-AzResourceGroup
```

<span data-ttu-id="3f0fa-205">若要获得更简洁的视图, 可以使用管道 "|" `Get-AzResourceGroup`将输出`Format-Table`发送到 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-205">To get a more concise view, you can send the output from the `Get-AzResourceGroup` to the `Format-Table` cmdlet using a pipe '|'.</span></span>

```powershell
Get-AzResourceGroup | Format-Table
```

<span data-ttu-id="3f0fa-206">这将输出如下内容:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-206">This will output something like:</span></span>

```output
ResourceGroupName                  Location       ProvisioningState Tags TagsTable ResourceId
-----------------                  --------       ----------------- ---- --------- ----------
cloud-shell-storage-southcentralus southcentralus Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
ExerciseResources                  eastus         Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
```

### <a name="create-a-resource-group"></a><span data-ttu-id="3f0fa-207">创建资源组</span><span class="sxs-lookup"><span data-stu-id="3f0fa-207">Create a Resource Group</span></span>

<span data-ttu-id="3f0fa-208">正如您所知, 在 Azure 中创建资源时, 您将始终出于管理目的将它们放入资源组中。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-208">As you know, when you are creating resources in Azure, you will always place them into a resource group for management purposes.</span></span> <span data-ttu-id="3f0fa-209">资源组通常是启动新的应用程序时要创建的第一项。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-209">A resource group is often one of the first things you will create when starting a new application.</span></span>

<span data-ttu-id="3f0fa-210">您可以使用`New-AzResourceGroup` cmdlet 创建资源组。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-210">You can create resource groups with the `New-AzResourceGroup` cmdlet.</span></span> <span data-ttu-id="3f0fa-211">您必须指定名称和位置。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-211">You must specify a name and location.</span></span> <span data-ttu-id="3f0fa-212">该名称在你的订阅中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-212">The name must be unique within your subscription.</span></span> <span data-ttu-id="3f0fa-213">该位置确定将存储资源组的元数据的位置 (由于合规性原因, 可能对您很重要)。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-213">The location determines where the metadata for your resource group will be stored (which may be important to you for compliance reasons).</span></span> <span data-ttu-id="3f0fa-214">您可以使用如 "west US"、"北欧" 或 "西印度" 指定位置的字符串。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-214">You use strings like "West US", "North Europe", or "West India" to specify the location.</span></span> <span data-ttu-id="3f0fa-215">与大多数 Azure cmdlet 一样, `New-AzResourceGroup`具有多个可选参数;但是, 核心语法为:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-215">As with most of the Azure cmdlets, `New-AzResourceGroup` has many optional parameters; however, the core syntax is:</span></span>

```powershell
New-AzResourceGroup -Name <name> -Location <location>
```

> [!NOTE]
> <span data-ttu-id="3f0fa-216">请记住, 我们将在 Azure 沙箱中工作, 这将为你创建资源组。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-216">Remember, we will be working in the Azure sandbox which creates the Resource Group for you.</span></span> <span data-ttu-id="3f0fa-217">如果您在自己的订阅中工作, 将使用上面的命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-217">The above command would be used if you work in your own subscription.</span></span>

### <a name="verify-the-resources"></a><span data-ttu-id="3f0fa-218">验证资源</span><span class="sxs-lookup"><span data-stu-id="3f0fa-218">Verify the resources</span></span>
<span data-ttu-id="3f0fa-219">`Get-AzResource`列出了 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-219">The `Get-AzResource` lists your Azure resources.</span></span> <span data-ttu-id="3f0fa-220">这在此处可用于验证资源组的创建是否成功。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-220">This is useful here to verify whether creation of the resource group was successful.</span></span>

```powershell
Get-AzResource
```

<span data-ttu-id="3f0fa-221">与`Get-AzResourceGroup`命令一样, 您可以通过`Format-Table` cmdlet 获得更简洁的视图。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-221">Like the `Get-AzResourceGroup` command, you can get a more concise view through the `Format-Table` cmdlet.</span></span> <span data-ttu-id="3f0fa-222">此处, 我们将使用简写版本`ft`:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-222">Here we will use a shorthand version `ft`:</span></span>

```powershell
Get-AzResource | ft
```

<span data-ttu-id="3f0fa-223">您还可以将其筛选到特定的资源组, 以仅列出与该组关联的资源:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-223">You can also filter it to specific resource groups to only list resources associated with that group:</span></span>

```powershell
Get-AzResource -ResourceGroup ExerciseResources
```

### <a name="creating-an-azure-virtual-machine"></a><span data-ttu-id="3f0fa-224">创建 Azure 虚拟机</span><span class="sxs-lookup"><span data-stu-id="3f0fa-224">Creating an Azure Virtual Machine</span></span>

<span data-ttu-id="3f0fa-225">可以使用 PowerShell 完成的另一个常见任务是创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-225">Another common task that could be done with PowerShell is to create VMs.</span></span>

<span data-ttu-id="3f0fa-226">Azure PowerShell 提供用于`New-AzVm`创建虚拟机的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-226">Azure PowerShell provides the `New-AzVm` cmdlet to create a virtual machine.</span></span> <span data-ttu-id="3f0fa-227">cmdlet 具有许多参数, 以使其能够处理大量 VM 配置设置。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-227">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="3f0fa-228">大多数参数都具有合理的默认值, 因此只需指定五项内容:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-228">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>

- <span data-ttu-id="3f0fa-229">**ResourceGroupName**: 将在其中放置新 VM 的资源组。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-229">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="3f0fa-230">**名称**: Azure 中的 VM 的名称。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-230">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="3f0fa-231">**位置**: 将在其中设置 VM 的地理位置。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-231">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="3f0fa-232">**Credential**: 包含 VM 管理员帐户的用户名和密码的对象。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-232">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="3f0fa-233">我们将使用`Get-Credential` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-233">We will use the `Get-Credential` cmdlet.</span></span> <span data-ttu-id="3f0fa-234">此 cmdlet 将提示输入用户名和密码, 并将其打包到 credential 对象中。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-234">This cmdlet will prompt for a username and password and package it into a credential object.</span></span>
- <span data-ttu-id="3f0fa-235">**Image**: 用于 VM 的操作系统映像。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-235">**Image**: The operating system image to use for the VM.</span></span> <span data-ttu-id="3f0fa-236">这通常是 Linux 分发或 Windows Server。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-236">This is often a Linux distribution, or Windows Server.</span></span>

```powershell
   New-AzVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

<span data-ttu-id="3f0fa-237">您可以直接向 cmdlet 提供这些参数, 如上所示。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-237">You can supply these parameters directly to the cmdlet as shown above.</span></span> <span data-ttu-id="3f0fa-238">或者, 可以使用其他 cmdlet 配置虚拟`Set-AzVMOperatingSystem`机, 例如`Set-AzVMSourceImage` `Add-AzVMNetworkInterface`、、和。 `Set-AzVMOSDisk`</span><span class="sxs-lookup"><span data-stu-id="3f0fa-238">Alternatively, other cmdlets can be used to configure the virtual machine, such as `Set-AzVMOperatingSystem`, `Set-AzVMSourceImage`, `Add-AzVMNetworkInterface`, and `Set-AzVMOSDisk`.</span></span>

<span data-ttu-id="3f0fa-239">下面的示例将`Get-Credential` cmdlet 与`-Credential`参数一起使用:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-239">Here's an example that strings the `Get-Credential` cmdlet together with the `-Credential` parameter:</span></span>

```powershell
New-AzVM -Name MyVm -ResourceGroupName ExerciseResources -Credential (Get-Credential) ...
```

<span data-ttu-id="3f0fa-240">`AzVM`后缀特定于 PowerShell 中基于 VM 的命令。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-240">The `AzVM` suffix is specific to VM-based commands in PowerShell.</span></span> <span data-ttu-id="3f0fa-241">您可以使用的其他几个选项:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-241">There are several others you can use:</span></span>

| <span data-ttu-id="3f0fa-242">指挥</span><span class="sxs-lookup"><span data-stu-id="3f0fa-242">Command</span></span> | <span data-ttu-id="3f0fa-243">说明</span><span class="sxs-lookup"><span data-stu-id="3f0fa-243">Description</span></span> |
|---------|-------------|
| `Remove-AzVM` | <span data-ttu-id="3f0fa-244">删除 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-244">Deletes an Azure VM.</span></span> |
| `Start-AzVM` | <span data-ttu-id="3f0fa-245">启动已停止的 VM。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-245">Start a stopped VM.</span></span> |
| `Stop-AzVM` | <span data-ttu-id="3f0fa-246">停止正在运行的 VM。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-246">Stop a running VM.</span></span> |
| `Restart-AzVM` | <span data-ttu-id="3f0fa-247">重新启动 VM。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-247">Restart a VM.</span></span> |
| `Update-AzVM` | <span data-ttu-id="3f0fa-248">更新 VM 的配置。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-248">Updates the configuration for a VM.</span></span> |

#### <a name="example-getting-the-information-for-a-vm"></a><span data-ttu-id="3f0fa-249">示例: 获取 VM 的信息</span><span class="sxs-lookup"><span data-stu-id="3f0fa-249">Example: getting the information for a VM</span></span>

<span data-ttu-id="3f0fa-250">您可以使用`Get-AzVM -Status`命令列出订阅中的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-250">You can list the VMs in your subscription with the `Get-AzVM -Status` command.</span></span> <span data-ttu-id="3f0fa-251">这还可以使用`-Name`属性指定 VM。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-251">This can also specify a VM with the `-Name` property.</span></span> <span data-ttu-id="3f0fa-252">在这里, 我们将其分配给 PowerShell 变量:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-252">Here we assign it to a PowerShell variable:</span></span>

```powershell
$vm = Get-AzVM  -Name MyVM -ResourceGroupName ExerciseResources
```

<span data-ttu-id="3f0fa-253">有趣的是, 这是您可以与之交互的_对象_。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-253">The interesting thing is this is an _object_ you can interact with.</span></span> <span data-ttu-id="3f0fa-254">例如, 您可以获取该对象, 进行更改, 然后使用以下`Update-AzVM`命令将更改重新推送到 Azure:</span><span class="sxs-lookup"><span data-stu-id="3f0fa-254">For example, you can take that object, make changes and then push changes back to Azure with the `Update-AzVM` command:</span></span>

```powershell
$ResourceGroupName = "ExerciseResources"
$vm = Get-AzVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

<span data-ttu-id="3f0fa-255">PowerShell 的交互模式适用于一次性任务。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-255">PowerShell's interactive mode is appropriate for one-off tasks.</span></span> <span data-ttu-id="3f0fa-256">在我们的示例中, 我们可能在项目的生命周期中使用相同的资源组, 这意味着以交互方式创建它是合理的。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-256">In our example, we'll likely use the same resource group for the lifetime of the project, which means creating it interactively is reasonable.</span></span> <span data-ttu-id="3f0fa-257">与编写脚本并只执行一次该脚本相比, 此任务的交互模式通常更快速且更容易。</span><span class="sxs-lookup"><span data-stu-id="3f0fa-257">Interactive mode is often quicker and easier for this task than writing a script and executing that script exactly once.</span></span>