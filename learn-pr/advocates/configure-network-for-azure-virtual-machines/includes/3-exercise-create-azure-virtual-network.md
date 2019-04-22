<span data-ttu-id="93c34-101">在本练习中, 你将在 Microsoft Azure 中创建虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="93c34-101">In this exercise, you will create a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="93c34-102">然后, 创建两个虚拟机, 并使用虚拟网络将虚拟机和 Internet 连接到 Internet。</span><span class="sxs-lookup"><span data-stu-id="93c34-102">You will then create two virtual machines and use the virtual network to connect the virtual machines and to the Internet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93c34-103">此模块中的练习需要完整的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="93c34-103">The exercises in this module require a full Azure subscription.</span></span> <span data-ttu-id="93c34-104">练习是可选的, 不需要完成此模块。</span><span class="sxs-lookup"><span data-stu-id="93c34-104">The exercises are optional and are not required to complete this module.</span></span> <span data-ttu-id="93c34-105">参加本模块中的交互式练习将会向你用来完成它们的 Azure 订阅收取费用。</span><span class="sxs-lookup"><span data-stu-id="93c34-105">Participating in the interactive exercises in this module will result in charges billed to the Azure subscription you use to complete them.</span></span>  <span data-ttu-id="93c34-106">通过尽可能快地清除所创建的资源, 可以最大限度地减少费用。</span><span class="sxs-lookup"><span data-stu-id="93c34-106">Incurred charges can be minimized by cleaning up the resources you create as soon as possible.</span></span> <span data-ttu-id="93c34-107">清理方向在最后单位中。</span><span class="sxs-lookup"><span data-stu-id="93c34-107">Cleanup directions are in the final unit.</span></span>

## <a name="log-in-to-your-subscription-with-the-azure-cli"></a><span data-ttu-id="93c34-108">使用 Azure CLI 登录到你的订阅</span><span class="sxs-lookup"><span data-stu-id="93c34-108">Log in to your subscription with the Azure CLI</span></span>

<span data-ttu-id="93c34-109">本第一个练习将使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="93c34-109">This first exercise will use the Azure CLI.</span></span> <span data-ttu-id="93c34-110">如果你有 Azure CLI 的本地安装, 请不要使用它&mdash; 。请确保使用`az account`登录到要使用的订阅。</span><span class="sxs-lookup"><span data-stu-id="93c34-110">If you have a local installation of the Azure CLI, feel free to use it &mdash; make sure to use `az account` to log in to the subscription you want to use.</span></span> <span data-ttu-id="93c34-111">如果不是, 可以登录到[shell.azure.com](https://shell.azure.com)上的 Azure 帐户, 并从那里使用命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="93c34-111">If not, you can log into your Azure account on [shell.azure.com](https://shell.azure.com) and use the shell from there.</span></span>

> [!NOTE]
> <span data-ttu-id="93c34-112">如果使用的是 CloudShell 环境, 请选择**Bash**命令行管理程序选项。</span><span class="sxs-lookup"><span data-stu-id="93c34-112">If you are using the CloudShell environment, select the **Bash** shell option.</span></span> <span data-ttu-id="93c34-113">如果您在本地或在云中使用 PowerShell, 则需要通过更改`""`为`'""'`将空字符串正确地传递到命令中来对所有空参数进行转义。</span><span class="sxs-lookup"><span data-stu-id="93c34-113">If you are using PowerShell, locally or in the cloud, then you will need to escape all empty parameters by changing `""` to `'""'` to properly pass an empty string into the command.</span></span> <span data-ttu-id="93c34-114">如果不这样做, PowerShell 不会传递空字符串, 并且将从命令中收到一个错误, 指示它缺少参数。</span><span class="sxs-lookup"><span data-stu-id="93c34-114">Without this, PowerShell will not pass the empty string, and you will get an error from the command indicating it's missing a parameter.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="93c34-115">创建资源组</span><span class="sxs-lookup"><span data-stu-id="93c34-115">Create a resource group</span></span>

<span data-ttu-id="93c34-116">首先, 创建一个资源组, 以包含您将在此模块中创建的所有资源。</span><span class="sxs-lookup"><span data-stu-id="93c34-116">First, create a resource group to contain all of the resources you'll create in this module.</span></span> <span data-ttu-id="93c34-117">将其`vm-networks`命名。</span><span class="sxs-lookup"><span data-stu-id="93c34-117">Name it `vm-networks`.</span></span>

```azurecli
az group create --name vm-networks
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="93c34-118">创建虚拟网络</span><span class="sxs-lookup"><span data-stu-id="93c34-118">Create a virtual network</span></span>

<span data-ttu-id="93c34-119">若要创建虚拟网络, 请输入以下命令, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="93c34-119">To create a virtual network, enter the following command and press Enter.</span></span>

```azurecli
az network vnet create \
    --name myVnet \
    --resource-group vm-networks \
    --subnet-name default
```

## <a name="create-two-virtual-machines"></a><span data-ttu-id="93c34-120">创建两台虚拟机</span><span class="sxs-lookup"><span data-stu-id="93c34-120">Create two virtual machines</span></span>

<span data-ttu-id="93c34-121">所有 Azure 虚拟机都已连接到虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="93c34-121">All Azure virtual machines are connected to a virtual network.</span></span> <span data-ttu-id="93c34-122">如果使用 Azure CLI 创建虚拟机, 但未指定现有虚拟网络的名称, 则 CLI 将根据位置和子网的可用性搜索相应虚拟网络的目标资源组。</span><span class="sxs-lookup"><span data-stu-id="93c34-122">If you create a virtual machine using the Azure CLI and don't specify the name of an existing virtual network, the CLI will search the target resource group for an appropriate virtual network to use, based on location and subnet availability.</span></span> <span data-ttu-id="93c34-123">如果找不到匹配项, 则会自动创建一个新的虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="93c34-123">If no match is found, a new virtual network will be created automatically.</span></span>

<span data-ttu-id="93c34-124">在这里, 我们创建两个虚拟机, 而不指定任何虚拟网络信息。</span><span class="sxs-lookup"><span data-stu-id="93c34-124">Here, we create two virtual machines without specifying any virtual network information.</span></span> <span data-ttu-id="93c34-125">默认网络规范与的`myVnet`属性相匹配, 因此 CLI 将自动找到并使用它。</span><span class="sxs-lookup"><span data-stu-id="93c34-125">The default network specifications match the attributes of `myVnet`, so the CLI will automatically locate and use it.</span></span>

1. <span data-ttu-id="93c34-126">若要创建第一台虚拟机, 请执行以下命令, 创建具有可通过端口 3389 (远程桌面) 访问的公共 IP 地址的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="93c34-126">To create the first virtual machine, execute the following command to create a Windows VM with a public IP address that is accessible over port 3389 (Remote Desktop).</span></span> <span data-ttu-id="93c34-127">这将创建一个名为`dataProcStage1`的 Windows 2016 数据中心虚拟机。</span><span class="sxs-lookup"><span data-stu-id="93c34-127">This will create a Windows 2016 Datacenter VM named `dataProcStage1`.</span></span>

    ```azurecli
    az vm create \
        --name dataProcStage1 \
        --resource-group vm-networks \
        --admin-username "DataAdmin" \
        --image Win2016Datacenter
    ```

1. <span data-ttu-id="93c34-128">在提示符处为你的密码提供值。</span><span class="sxs-lookup"><span data-stu-id="93c34-128">Supply values for your password at the prompts.</span></span> <span data-ttu-id="93c34-129">请记住, 请记下此密码, 因为稍后你将需要它来访问服务器。</span><span class="sxs-lookup"><span data-stu-id="93c34-129">Remember to write this password down as you'll need it later to access the server.</span></span>

1. <span data-ttu-id="93c34-130">从创建您的 VM 复制返回的 JSON 中的**publicIpAddress**值, 以便以后可以使用它。</span><span class="sxs-lookup"><span data-stu-id="93c34-130">Copy the **publicIpAddress** value in the returned JSON from creating your VM so you can use it later.</span></span>

1. <span data-ttu-id="93c34-131">现在, 你将创建第二个 VM。</span><span class="sxs-lookup"><span data-stu-id="93c34-131">You'll now create the second VM.</span></span> <span data-ttu-id="93c34-132">此 VM 将被命名`dataProcStage2` , 并且不会有公用 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="93c34-132">This VM will be named `dataProcStage2` and will not have a public IP address.</span></span>

    ```azurecli
    az vm create \
        --name dataProcStage2 \
        --resource-group vm-networks \
        --public-ip-address "" \
        --admin-username "DataAdmin" \
        --image Win2016Datacenter
    ```

## <a name="connect-to-dataprocstage1-using-remote-desktop"></a><span data-ttu-id="93c34-133">使用远程桌面连接到 dataProcStage1</span><span class="sxs-lookup"><span data-stu-id="93c34-133">Connect to dataProcStage1 using Remote Desktop</span></span>

1. <span data-ttu-id="93c34-134">打开 "远程桌面", `dataProcStage1`并使用前面步骤中提到的公共 IP 地址连接到。</span><span class="sxs-lookup"><span data-stu-id="93c34-134">Open Remote Desktop and connect to `dataProcStage1` with the public IP address you noted from the previous steps.</span></span>

1. <span data-ttu-id="93c34-135">使用您创建的用户名`DataAdmin`和密码登录到远程计算机。</span><span class="sxs-lookup"><span data-stu-id="93c34-135">Log into the remote machine with the username `DataAdmin` and the password you created.</span></span>

1. <span data-ttu-id="93c34-136">在远程会话中, 打开 Windows 命令提示符, 然后运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="93c34-136">In the remote session, open the Windows command prompt and run the following command:</span></span>

    ```cmd
    ping dataProcStage2 -4
    ```

1. <span data-ttu-id="93c34-137">在结果中, 您将看到所有请求`dataProcStage2`超时。这是因为中`dataProcStage2`的默认 Windows 防火墙配置会阻止它响应 ping。</span><span class="sxs-lookup"><span data-stu-id="93c34-137">In the results, you'll see that all requests to `dataProcStage2` time out. This is because the default Windows Firewall configuration on `dataProcStage2` prevents it from responding to pings.</span></span>

## <a name="connect-to-dataprocstage2-using-remote-desktop"></a><span data-ttu-id="93c34-138">使用远程桌面连接到 dataProcStage2</span><span class="sxs-lookup"><span data-stu-id="93c34-138">Connect to dataProcStage2 using Remote Desktop</span></span>

<span data-ttu-id="93c34-139">你将`dataProcStage2`使用新的远程桌面会话配置 Windows 防火墙。</span><span class="sxs-lookup"><span data-stu-id="93c34-139">You'll configure the Windows Firewall on `dataProcStage2` using a new remote desktop session.</span></span> <span data-ttu-id="93c34-140">但是, 你将无法从你的`dataProcStage2`桌面进行访问。</span><span class="sxs-lookup"><span data-stu-id="93c34-140">However, you'll not able to access `dataProcStage2` from your desktop.</span></span> <span data-ttu-id="93c34-141">撤回, `dataProcStage2`不具有公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="93c34-141">Recall, `dataProcStage2` does not have a public IP address.</span></span> <span data-ttu-id="93c34-142">您将使用的`dataProcStage1`远程桌面连接到。 `dataProcStage2`</span><span class="sxs-lookup"><span data-stu-id="93c34-142">You will use remote desktop from `dataProcStage1` to connect to `dataProcStage2`.</span></span>

1. <span data-ttu-id="93c34-143">在`dataProcStage1`远程会话中, 打开 "远程桌面"。</span><span class="sxs-lookup"><span data-stu-id="93c34-143">In the `dataProcStage1` remote session, open Remote Desktop.</span></span>

1. <span data-ttu-id="93c34-144">按名称`dataProcStage2`连接到。</span><span class="sxs-lookup"><span data-stu-id="93c34-144">Connect to `dataProcStage2` by name.</span></span> <span data-ttu-id="93c34-145">根据默认网络配置, `dataProcStage1`可以解析`dataProcStage2`使用计算机名称的地址。</span><span class="sxs-lookup"><span data-stu-id="93c34-145">Based on the default network configuration, `dataProcStage1` can resolve the address for `dataProcStage2` using the computer name.</span></span>

1. <span data-ttu-id="93c34-146">使用您创建`dataProcStage2`的用户名`DataAdmin`和密码登录到。</span><span class="sxs-lookup"><span data-stu-id="93c34-146">Log in to `dataProcStage2` with the username `DataAdmin` and the password you created.</span></span>

1. <span data-ttu-id="93c34-147">在`dataProcStage2`上, 单击 "开始" 菜单, 键入**Firewall**, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="93c34-147">On `dataProcStage2`, click the Start Menu, type **Firewall**, and press Enter.</span></span> <span data-ttu-id="93c34-148">将显示 "**高级安全 Windows 防火墙**" 控制台。</span><span class="sxs-lookup"><span data-stu-id="93c34-148">The **Windows Firewall with Advanced Security** console appears.</span></span>

1. <span data-ttu-id="93c34-149">在左侧窗格中, 单击 "**入站规则**"。</span><span class="sxs-lookup"><span data-stu-id="93c34-149">In the left-hand pane, click **Inbound Rules**.</span></span>

1. <span data-ttu-id="93c34-150">在右侧窗格中, 向下滚动, 右键单击 "**文件和打印机共享 (回显请求-icmpv4-in)**", 然后单击 "**启用规则**"。</span><span class="sxs-lookup"><span data-stu-id="93c34-150">In the right-hand pane, scroll down, and right-click **File and Printer Sharing (Echo Request - ICMPv4-In)**, and then click **Enable Rule**.</span></span>

1. <span data-ttu-id="93c34-151">切换回`dataProcStage1`远程会话, 并在命令提示符处运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="93c34-151">Switch back to the `dataProcStage1` remote session and run the following command in the command prompt.</span></span>

    ```cmd
    ping dataProcStage2 -4
    ```

1. <span data-ttu-id="93c34-152">`dataProcStage2`响应四个答复, 演示两个虚拟机之间的连接。</span><span class="sxs-lookup"><span data-stu-id="93c34-152">`dataProcStage2` responds with four replies, demonstrating connectivity between the two VMs.</span></span>

<span data-ttu-id="93c34-153">您已成功创建虚拟网络, 创建了连接到该虚拟网络的两个虚拟机, 连接到其中一个 vm 并在同一虚拟网络中显示到其他 vm 的网络连接。</span><span class="sxs-lookup"><span data-stu-id="93c34-153">You have successfully created a virtual network, created two VMs that are attached to that virtual network, connected to one of the VMs and shown network connectivity to the other VM within the same virtual network.</span></span> <span data-ttu-id="93c34-154">您可以使用 azure 虚拟网络连接 azure 网络中的资源。</span><span class="sxs-lookup"><span data-stu-id="93c34-154">You can use Azure Virtual Network to connect resources within the Azure network.</span></span> <span data-ttu-id="93c34-155">但是, 这些资源必须位于相同的资源组和订阅中。</span><span class="sxs-lookup"><span data-stu-id="93c34-155">However, those resources need to be within the same resource group and subscription.</span></span> <span data-ttu-id="93c34-156">接下来, 我们将看一下 VPN 网关, 它使你能够在不同的资源组、订阅甚至地理区域中连接虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="93c34-156">Next, we will look at VPN gateways, which enable you to connect virtual network in different resource groups, subscriptions, and even geographical regions.</span></span>
