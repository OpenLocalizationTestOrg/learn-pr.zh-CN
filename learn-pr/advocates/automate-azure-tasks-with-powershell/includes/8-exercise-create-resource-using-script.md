<span data-ttu-id="3ccef-101">在此单元中, 你将继续使用一个构成 Linux 管理员工具的公司的示例。</span><span class="sxs-lookup"><span data-stu-id="3ccef-101">In this unit, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="3ccef-102">请记住, 您计划使用 Linux 虚拟机以让潜在客户测试您的软件。</span><span class="sxs-lookup"><span data-stu-id="3ccef-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="3ccef-103">您有资源组准备好了, 现在是时候创建虚拟机了。</span><span class="sxs-lookup"><span data-stu-id="3ccef-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="3ccef-104">你的公司已在大型 Linux 商业展览上为展台付费。</span><span class="sxs-lookup"><span data-stu-id="3ccef-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="3ccef-105">您规划一个演示区域, 其中包含每个连接到单独 Linux VM 的终端。</span><span class="sxs-lookup"><span data-stu-id="3ccef-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="3ccef-106">在每天结束时, 您想要删除并重新创建虚拟机, 以便它们每天在上午开始进行刷新。</span><span class="sxs-lookup"><span data-stu-id="3ccef-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="3ccef-107">如果在您厌倦时手动创建 vm, 则会容易出错。</span><span class="sxs-lookup"><span data-stu-id="3ccef-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="3ccef-108">您希望编写 PowerShell 脚本以自动执行 VM 创建过程。</span><span class="sxs-lookup"><span data-stu-id="3ccef-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="3ccef-109">编写用于创建虚拟机的脚本</span><span class="sxs-lookup"><span data-stu-id="3ccef-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="3ccef-110">请在右侧的云命令行管理程序中执行以下步骤, 以编写脚本:</span><span class="sxs-lookup"><span data-stu-id="3ccef-110">Follow these steps in the Cloud Shell on the right to write the script:</span></span>

1. <span data-ttu-id="3ccef-111">切换到云命令行管理程序中的主文件夹。</span><span class="sxs-lookup"><span data-stu-id="3ccef-111">Switch to your home folder in the Cloud Shell.</span></span>

    ```powershell
    cd $HOME\clouddrive
    ```

1. <span data-ttu-id="3ccef-112">创建一个名为**ConferenceDailyReset**的新文本文件。</span><span class="sxs-lookup"><span data-stu-id="3ccef-112">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

    ```powershell
    touch "./ConferenceDailyReset.ps1"
    ```

1. <span data-ttu-id="3ccef-113">打开集成编辑器并选择**ConferenceDailyReset**文件。</span><span class="sxs-lookup"><span data-stu-id="3ccef-113">Open the integrated editor and select the **ConferenceDailyReset.ps1** file.</span></span>

    ```powershell
    code "./ConferenceDailyReset.ps1"
    ```
    > [!TIP]
    > <span data-ttu-id="3ccef-114">集成云命令行管理程序还支持 vim、nano 和 emacs (如果您希望使用其中一个编辑器)。</span><span class="sxs-lookup"><span data-stu-id="3ccef-114">The integrated Cloud Shell also supports vim, nano, and emacs if you'd prefer to use one of those editors.</span></span>

1. <span data-ttu-id="3ccef-115">首先, 在变量中捕获输入参数。</span><span class="sxs-lookup"><span data-stu-id="3ccef-115">Start by capturing the input parameter in a variable.</span></span> <span data-ttu-id="3ccef-116">在脚本中添加以下行:</span><span class="sxs-lookup"><span data-stu-id="3ccef-116">Add the following line to your script:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

    > [!NOTE]
    > <span data-ttu-id="3ccef-117">通常情况下, 您必须使用您的凭据通过 Azure 进行`Connect-AzAccount`身份验证, 并且可以在脚本中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3ccef-117">Normally, you'd have to authenticate with Azure using your credentials using `Connect-AzAccount` and this could be done in the script.</span></span> <span data-ttu-id="3ccef-118">但是, 在云命令行管理程序环境中, 您将已经过身份验证, 因此这是不必要的。</span><span class="sxs-lookup"><span data-stu-id="3ccef-118">However, in the Cloud Shell environment you will already be authenticated so this is unnecessary.</span></span>

1. <span data-ttu-id="3ccef-119">为 VM 的管理员帐户提示输入用户名和密码, 并将结果捕获到变量中:</span><span class="sxs-lookup"><span data-stu-id="3ccef-119">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. <span data-ttu-id="3ccef-120">创建一个执行三次的循环:</span><span class="sxs-lookup"><span data-stu-id="3ccef-120">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

1. <span data-ttu-id="3ccef-121">在循环正文中, 为每个 VM 创建一个名称, 并将其存储在一个变量中, 并将其输出到控制台:</span><span class="sxs-lookup"><span data-stu-id="3ccef-121">In the loop body, create a name for each VM and store it in a variable and output it to the console:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    ```

1. <span data-ttu-id="3ccef-122">接下来, 使用`$vmName`变量创建 VM:</span><span class="sxs-lookup"><span data-stu-id="3ccef-122">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
   ```

1. <span data-ttu-id="3ccef-123">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="3ccef-123">Save the file.</span></span> <span data-ttu-id="3ccef-124">您可以使用 "..."编辑器右上角的菜单。</span><span class="sxs-lookup"><span data-stu-id="3ccef-124">You can use the "..." menu at the top right corner of the editor.</span></span> <span data-ttu-id="3ccef-125">还有用于保存的常用加速键。</span><span class="sxs-lookup"><span data-stu-id="3ccef-125">There are also common accelerator keys for Save.</span></span>

<span data-ttu-id="3ccef-126">已完成的脚本应如下所示:</span><span class="sxs-lookup"><span data-stu-id="3ccef-126">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="3ccef-127">执行脚本</span><span class="sxs-lookup"><span data-stu-id="3ccef-127">Execute the script</span></span>

<span data-ttu-id="3ccef-128">通过 "..." 关闭编辑器。上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="3ccef-128">Close the editor through the "..." context menu.</span></span>

1. <span data-ttu-id="3ccef-129">执行脚本。</span><span class="sxs-lookup"><span data-stu-id="3ccef-129">Execute the script.</span></span>

    ```powershell
    .\ConferenceDailyReset.ps1 <rgn>[sandbox resource group name]</rgn>
    ```
    
<span data-ttu-id="3ccef-130">脚本将需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="3ccef-130">The script will take several minutes to complete.</span></span> <span data-ttu-id="3ccef-131">完成后, 通过查看您在资源组中现在所拥有的资源来验证它是否成功运行:</span><span class="sxs-lookup"><span data-stu-id="3ccef-131">When it is finished, verify that it ran successfully by looking at the resources you now have in your resource group:</span></span>

```powershell
Get-AzResource -ResourceType Microsoft.Compute/virtualMachines
```

<span data-ttu-id="3ccef-132">您应该会看到三个虚拟机, 每个虚拟机具有唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="3ccef-132">You should see three VMs, each with a unique name.</span></span>

<span data-ttu-id="3ccef-133">您编写了一个脚本, 该脚本可自动创建由 script 参数指示的资源组中的三个虚拟机。</span><span class="sxs-lookup"><span data-stu-id="3ccef-133">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="3ccef-134">该脚本非常简短且简单, 但自动化了需要很长时间才能通过门户手动完成的过程。</span><span class="sxs-lookup"><span data-stu-id="3ccef-134">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>