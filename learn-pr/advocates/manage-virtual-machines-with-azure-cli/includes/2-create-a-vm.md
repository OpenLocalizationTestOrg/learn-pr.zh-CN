<span data-ttu-id="b40b4-101">让我们从最显而易见的任务入手: 创建 Azure 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b40b4-101">Let's start with the most obvious task: creating an Azure Virtual Machine.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="logins-subscriptions-and-resource-groups"></a><span data-ttu-id="b40b4-102">登录、订阅和资源组</span><span class="sxs-lookup"><span data-stu-id="b40b4-102">Logins, subscriptions, and resource groups</span></span>

<span data-ttu-id="b40b4-103">你将在右侧的 Azure 云命令行管理程序中工作。</span><span class="sxs-lookup"><span data-stu-id="b40b4-103">You'll be working in the Azure Cloud Shell on the right.</span></span> <span data-ttu-id="b40b4-104">激活沙盒后, 你将通过 Microsoft 学习管理的免费订阅登录 Azure。</span><span class="sxs-lookup"><span data-stu-id="b40b4-104">Once you activate the sandbox, you'll be logged into Azure with a free subscription managed by Microsoft Learn.</span></span> <span data-ttu-id="b40b4-105">您不必登录 Azure, 也不必选择订阅-这将为您完成。</span><span class="sxs-lookup"><span data-stu-id="b40b4-105">You don't have to log into Azure on your own, or select a subscription - this will be done for you.</span></span> <span data-ttu-id="b40b4-106">此外, 通常会创建一个_资源组_来保存新资源。</span><span class="sxs-lookup"><span data-stu-id="b40b4-106">In addition, normally you would create a _resource group_ to hold new resources.</span></span> <span data-ttu-id="b40b4-107">在此模块中, Azure 沙盒将为您创建一个资源组, 该资源组将用于执行所有命令。</span><span class="sxs-lookup"><span data-stu-id="b40b4-107">In this module, the Azure sandbox will create a resource group for you which will be used to execute all the commands.</span></span>

## <a name="create-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="b40b4-108">使用 Azure CLI 创建 Linux VM</span><span class="sxs-lookup"><span data-stu-id="b40b4-108">Create a Linux VM with the Azure CLI</span></span>

<span data-ttu-id="b40b4-109">azure CLI 包括使用 Azure `vm`中的虚拟机的命令。</span><span class="sxs-lookup"><span data-stu-id="b40b4-109">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="b40b4-110">我们可以提供几个子命令来完成特定任务。</span><span class="sxs-lookup"><span data-stu-id="b40b4-110">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="b40b4-111">最常见的包括:</span><span class="sxs-lookup"><span data-stu-id="b40b4-111">The most common include:</span></span>

| <span data-ttu-id="b40b4-112">子命令</span><span class="sxs-lookup"><span data-stu-id="b40b4-112">Sub-command</span></span> | <span data-ttu-id="b40b4-113">说明</span><span class="sxs-lookup"><span data-stu-id="b40b4-113">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="b40b4-114">创建新的虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-114">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="b40b4-115">解除分配虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-115">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="b40b4-116">删除虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-116">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="b40b4-117">列出订阅中创建的虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-117">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="b40b4-118">为入站流量打开特定的网络端口</span><span class="sxs-lookup"><span data-stu-id="b40b4-118">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="b40b4-119">重新启动虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-119">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="b40b4-120">获取虚拟机的详细信息</span><span class="sxs-lookup"><span data-stu-id="b40b4-120">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="b40b4-121">启动已停止的虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-121">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="b40b4-122">停止正在运行的虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-122">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="b40b4-123">更新虚拟机的属性</span><span class="sxs-lookup"><span data-stu-id="b40b4-123">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="b40b4-124">有关命令的完整列表, 可以查看[Azure CLI 参考文档](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)。</span><span class="sxs-lookup"><span data-stu-id="b40b4-124">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="b40b4-125">让我们从第一个开始: `az vm create`。</span><span class="sxs-lookup"><span data-stu-id="b40b4-125">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="b40b4-126">此命令用于在资源组中创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b40b4-126">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="b40b4-127">您可以通过多个参数来配置新 VM 的所有方面。</span><span class="sxs-lookup"><span data-stu-id="b40b4-127">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="b40b4-128">必须提供的三个参数为:</span><span class="sxs-lookup"><span data-stu-id="b40b4-128">The three parameters that must be supplied are:</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="b40b4-129">参数</span><span class="sxs-lookup"><span data-stu-id="b40b4-129">Parameter</span></span> | <span data-ttu-id="b40b4-130">说明</span><span class="sxs-lookup"><span data-stu-id="b40b4-130">Description</span></span> |
> |-----------|-------------|
> | `resource-group` | <span data-ttu-id="b40b4-131">将拥有虚拟机的资源组, 请使用**<rgn>[沙盒资源组]</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="b40b4-131">The resource group that will own the virtual machine, use **<rgn>[sandbox Resource Group]</rgn>**.</span></span> |
> | `name` | <span data-ttu-id="b40b4-132">虚拟机的名称-在资源组中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="b40b4-132">The name of the virtual machine - must be unique within the resource group.</span></span> |
> | `image` | <span data-ttu-id="b40b4-133">用于创建虚拟机的操作系统映像。</span><span class="sxs-lookup"><span data-stu-id="b40b4-133">The operating system image to use to create the VM.</span></span> |
> | `location` | <span data-ttu-id="b40b4-134">要放置 VM 的区域。</span><span class="sxs-lookup"><span data-stu-id="b40b4-134">The region to place the VM in.</span></span> <span data-ttu-id="b40b4-135">通常情况下, 这将接近 VM 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b40b4-135">Typically this would be close to the consumer of the VM.</span></span> <span data-ttu-id="b40b4-136">在本练习中, 请从以下列表中选择邻近的位置。</span><span class="sxs-lookup"><span data-stu-id="b40b4-136">In this exercise, choose a location nearby from the following list.</span></span> |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="b40b4-137">此外, 在创建 VM 时添加`--verbose`标志以查看进度很有帮助。</span><span class="sxs-lookup"><span data-stu-id="b40b4-137">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="b40b4-138">创建 Linux 虚拟机</span><span class="sxs-lookup"><span data-stu-id="b40b4-138">Create a Linux virtual machine</span></span>

<span data-ttu-id="b40b4-139">让我们创建一个新的 Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b40b4-139">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="b40b4-140">在 Azure 云命令行管理程序中执行以下命令, 以在 "West US" 位置创建 Debian Linux 计算机。</span><span class="sxs-lookup"><span data-stu-id="b40b4-140">Execute the following command in Azure Cloud Shell to create a Debian Linux machine in the "West US" location.</span></span> <span data-ttu-id="b40b4-141">如果不是附近, 请更改位置。</span><span class="sxs-lookup"><span data-stu-id="b40b4-141">Change the location if that one isn't nearby.</span></span>

```azurecli
az vm create --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --location westus --verbose 
```

[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


<span data-ttu-id="b40b4-142">此命令将创建一个名\*\*\*\* `SampleVM`为的新 Debian Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b40b4-142">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="b40b4-143">请注意, 在创建虚拟机时, Azure CLI 工具将等待。</span><span class="sxs-lookup"><span data-stu-id="b40b4-143">Notice that the Azure CLI tool waits while the VM is being created.</span></span> <span data-ttu-id="b40b4-144">您可以添加`--no-wait`选项以通知 azure CLI 工具立即返回, 并让 azure 继续在后台创建 VM。</span><span class="sxs-lookup"><span data-stu-id="b40b4-144">You can add the `--no-wait` option to tell the Azure CLI tool to return immediately and have Azure continue creating the VM in the background.</span></span> <span data-ttu-id="b40b4-145">如果要在脚本中执行命令, 这将非常有用。</span><span class="sxs-lookup"><span data-stu-id="b40b4-145">This is useful if you're executing the command in a script.</span></span> <span data-ttu-id="b40b4-146">稍后在脚本中, 使用`azure vm wait --name [vm-name]`命令等待 VM 完成创建。</span><span class="sxs-lookup"><span data-stu-id="b40b4-146">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="b40b4-147">如果你查看详细响应, 你还会看到`SampleVM`名称用于为 VM 命名各种依赖项。</span><span class="sxs-lookup"><span data-stu-id="b40b4-147">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```output
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="b40b4-148">您可以使用可选参数`vm create`(如`--vnet-name`和`--public-ip-address-dns-name`) 替代这些自动生成的资源名称。</span><span class="sxs-lookup"><span data-stu-id="b40b4-148">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="b40b4-149">我们正在通过`admin-username`标记指定 **"aldis"** 的管理员帐户名称。</span><span class="sxs-lookup"><span data-stu-id="b40b4-149">We are specifying the administrator account name through the `admin-username` flag to be **"aldis"**.</span></span> <span data-ttu-id="b40b4-150">如果省略此名称, 则`vm create`该命令将使用您的_当前用户名_。</span><span class="sxs-lookup"><span data-stu-id="b40b4-150">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="b40b4-151">由于每个 OS 的帐户名称规则各不相同, 因此指定特定名称比较安全。</span><span class="sxs-lookup"><span data-stu-id="b40b4-151">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> 

> [!NOTE]
> <span data-ttu-id="b40b4-152">大多数图像不允许使用常见名称, 例如 "root" 和 "admin"。</span><span class="sxs-lookup"><span data-stu-id="b40b4-152">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="b40b4-153">我们也在使用此`generate-ssh-keys`标志。</span><span class="sxs-lookup"><span data-stu-id="b40b4-153">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="b40b4-154">此参数用于 Linux 分发, 并创建一对安全密钥, 以便我们可以使用该`ssh`工具远程访问虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b40b4-154">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="b40b4-155">这两个文件放入您`.ssh`的计算机上的文件夹中, 在 VM 中。</span><span class="sxs-lookup"><span data-stu-id="b40b4-155">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="b40b4-156">如果目标文件夹中已有名为`id_rsa`的 SSH 密钥, 则将使用它, 而不是生成新密钥。</span><span class="sxs-lookup"><span data-stu-id="b40b4-156">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="b40b4-157">完成创建 VM 后, 你将获得一个 JSON 响应, 该响应包括 Azure 分配的虚拟机及其公用和专用 IP 地址的当前状态:</span><span class="sxs-lookup"><span data-stu-id="b40b4-157">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "westus",
  "macAddress": "00-0D-3A-58-F8-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
  "resourceGroup": "2568d0d0-efe3-4d04-a08f-df7f009f822a",
  "zones": ""
}
```
