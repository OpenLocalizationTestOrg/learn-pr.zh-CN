<span data-ttu-id="2cad5-101">与大多数应用程序框架一样, 您可以在许多不同的环境中运行您的平均堆栈应用程序。</span><span class="sxs-lookup"><span data-stu-id="2cad5-101">Like most application frameworks, you can run your MEAN stack application in many different environments.</span></span> <span data-ttu-id="2cad5-102">您可以在服务器机房、VM 或容器上的物理计算机上运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="2cad5-102">You can run your application on a physical computer in your server room, on a VM, or on containers.</span></span>

<span data-ttu-id="2cad5-103">在这里, 你将在 Azure 上运行的 VM 上运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2cad5-103">Here you'll run your application on a VM running on Azure.</span></span> <span data-ttu-id="2cad5-104">均值支持许多不同的操作系统。</span><span class="sxs-lookup"><span data-stu-id="2cad5-104">MEAN supports many different operating systems.</span></span> <span data-ttu-id="2cad5-105">为了便于学习, 您将使用 Ubuntu Linux。</span><span class="sxs-lookup"><span data-stu-id="2cad5-105">For learning purposes, here you'll use Ubuntu Linux.</span></span>

## <a name="create-an-ubuntu-linux-vm"></a><span data-ttu-id="2cad5-106">创建 Ubuntu Linux 虚拟机</span><span class="sxs-lookup"><span data-stu-id="2cad5-106">Create an Ubuntu Linux VM</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="2cad5-107">通常情况下, 先创建_资源组_, 然后再在 Azure 上创建其他资源。</span><span class="sxs-lookup"><span data-stu-id="2cad5-107">Normally, you create a _resource group_ before you create other resources on Azure.</span></span> <span data-ttu-id="2cad5-108">资源组将相关资源分组。</span><span class="sxs-lookup"><span data-stu-id="2cad5-108">A resource group groups related resources.</span></span> <span data-ttu-id="2cad5-109">Azure 沙盒为你提供了资源组。</span><span class="sxs-lookup"><span data-stu-id="2cad5-109">The Azure sandbox provides a resource group for you.</span></span> <span data-ttu-id="2cad5-110">当您在自己的 Azure 订阅中工作时, 请使用以下命令在你附近的位置创建资源组。</span><span class="sxs-lookup"><span data-stu-id="2cad5-110">When you work in your own Azure subscription, use the following command to create a resource group in a location near you.</span></span>

```azurecli
az group create \
  --name <resource-group-name> \
  --location <resource-group-location>
```

1. <span data-ttu-id="2cad5-111">从云命令行管理程序`az vm create`中, 运行命令以创建 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="2cad5-111">From Cloud Shell, run the `az vm create` command to create an Ubuntu VM.</span></span>

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name MeanStack \
      --image UbuntuLTS \
      --admin-username azureuser \
      --generate-ssh-keys
    ```

    <span data-ttu-id="2cad5-112">此命令大约需要两分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="2cad5-112">The command takes about two minutes to complete.</span></span> <span data-ttu-id="2cad5-113">命令完成后, 你将看到类似于此的输出。</span><span class="sxs-lookup"><span data-stu-id="2cad5-113">When the command finishes, you'll see output similar to this.</span></span>

    ```json
    {
      "fqdns": "",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/MeanStack",
      "location": "eastus",
      "macAddress": "00-0D-3A-1E-1B-3B",
      "powerState": "VM running",
      "privateIpAddress": "10.0.0.5",
      "publicIpAddress": "104.211.9.245",
      "resourceGroup": "<rgn>[sandbox resource group name]</rgn>",
      "zones": ""
    }
    ```

    <span data-ttu-id="2cad5-114">VM 的名称为 "MeanStack"。</span><span class="sxs-lookup"><span data-stu-id="2cad5-114">The VM's name is "MeanStack".</span></span> <span data-ttu-id="2cad5-115">你将在将来的命令中使用此名称来标识你要使用的 VM。</span><span class="sxs-lookup"><span data-stu-id="2cad5-115">You'll use this name in future commands to identify the VM you want to work with.</span></span>

1. <span data-ttu-id="2cad5-116">打开 VM 上的端口 80, 以允许传入的 HTTP 流量到您稍后创建的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2cad5-116">Open port 80 on the VM to allow incoming HTTP traffic to the web application you'll later create.</span></span>

    ```azurecli
    az vm open-port \
      --port 80 \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name MeanStack
    ```

1. <span data-ttu-id="2cad5-117">创建到你的 VM 的 SSH 连接。</span><span class="sxs-lookup"><span data-stu-id="2cad5-117">Create an SSH connection to your VM.</span></span>

    <span data-ttu-id="2cad5-118">尽管`az vm create`命令的输出显示你的 VM 的公共 IP 地址, 但你可能会发现将地址存储在 Bash 变量中非常有用。</span><span class="sxs-lookup"><span data-stu-id="2cad5-118">Although the output from the `az vm create` command displays your VM's public IP address, you may find it useful to store the address in a Bash variable.</span></span>

    <span data-ttu-id="2cad5-119">从运行`az vm show`。</span><span class="sxs-lookup"><span data-stu-id="2cad5-119">Start by running `az vm show`.</span></span> <span data-ttu-id="2cad5-120">此命令将 IP 地址保存在名为`ipaddress`的 Bash 变量中。</span><span class="sxs-lookup"><span data-stu-id="2cad5-120">This command saves the IP address in a Bash variable named `ipaddress`.</span></span>

    ```azurecli
    ipaddress=$(az vm show \
      --name MeanStack \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --show-details \
      --query [publicIps] \
      --output tsv)
    ```

    <span data-ttu-id="2cad5-121">连接到你的 VM, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="2cad5-121">Connect to your VM like this.</span></span>

    ```bash
    ssh azureuser@$ipaddress
    ```

    <span data-ttu-id="2cad5-122">出现提示时, 回答 "是" 以在本地保存 VM 的标识, 以便将来的连接受到信任。</span><span class="sxs-lookup"><span data-stu-id="2cad5-122">When prompted, answer "yes" to save the VM's identity locally so future connections are trusted.</span></span>

    <span data-ttu-id="2cad5-123">保持 SSH 连接处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="2cad5-123">Keep your SSH connection open.</span></span> <span data-ttu-id="2cad5-124">你将使用它在下一部分中配置软件。</span><span class="sxs-lookup"><span data-stu-id="2cad5-124">You'll use it to configure software in the next parts.</span></span>

## <a name="summary"></a><span data-ttu-id="2cad5-125">摘要</span><span class="sxs-lookup"><span data-stu-id="2cad5-125">Summary</span></span>

<span data-ttu-id="2cad5-126">使用 Ubuntu VM 准备就绪后, 即可安装平均堆栈的每个组件。</span><span class="sxs-lookup"><span data-stu-id="2cad5-126">With your Ubuntu VM ready to go, you're ready to install each component of the MEAN stack.</span></span> <span data-ttu-id="2cad5-127">首先, 你将安装 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="2cad5-127">You'll start by installing MongoDB.</span></span>