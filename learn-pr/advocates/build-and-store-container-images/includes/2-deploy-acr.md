<span data-ttu-id="e33c6-101">在此单元中, 你将使用 azure CLI 创建 azure 容器注册表。</span><span class="sxs-lookup"><span data-stu-id="e33c6-101">In this unit, you will create an Azure container registry using the Azure CLI.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]
 
## <a name="create-an-azure-container-registry"></a><span data-ttu-id="e33c6-102">创建 Azure 容器注册表</span><span class="sxs-lookup"><span data-stu-id="e33c6-102">Create an Azure container registry</span></span>

<span data-ttu-id="e33c6-103">我们将在免费沙盒中工作, 因此无需创建您自己的资源组。</span><span class="sxs-lookup"><span data-stu-id="e33c6-103">We'll be working in a free sandbox, so there's no need to create your own Resource Group.</span></span> <span data-ttu-id="e33c6-104">使用`az acr create`命令创建 Azure 容器注册表。</span><span class="sxs-lookup"><span data-stu-id="e33c6-104">Create an Azure container registry with the `az acr create` command.</span></span> <span data-ttu-id="e33c6-105">容器注册表名称在 Azure 中必须是唯一的, 并且包含5到50个字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="e33c6-105">The container registry name must be unique within Azure and contain between 5 and 50 alphanumeric characters.</span></span>

<span data-ttu-id="e33c6-106">在此示例中, 部署了高级注册表 SKU。</span><span class="sxs-lookup"><span data-stu-id="e33c6-106">In this example, a premium registry SKU is deployed.</span></span> <span data-ttu-id="e33c6-107">地理位置复制需要高级 SKU。</span><span class="sxs-lookup"><span data-stu-id="e33c6-107">The premium SKU is required for geo-replication.</span></span> 

<span data-ttu-id="e33c6-108">首先, 我们在云命令行管理程序中定义一个名为 " **ACR_NAME** " 的环境变量, 以保留我们想要为新的容器注册表命名的名称。</span><span class="sxs-lookup"><span data-stu-id="e33c6-108">To begin, we'll define an environment variable in the Cloud Shell called **ACR_NAME**  to hold the name we want to give our new container registry.</span></span>

1. <span data-ttu-id="e33c6-109">运行以下命令以定义名为 ACR_NAME 的变量。</span><span class="sxs-lookup"><span data-stu-id="e33c6-109">Run the following command to define a variable called ACR_NAME.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e33c6-110">在运行该命令之前, `<registry-name>`请将替换为您想要为新的容器注册表指定的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="e33c6-110">Before running the command, replace  `<registry-name>` with the unique name you want to give your new container registry.</span></span> <span data-ttu-id="e33c6-111">注册表名称在 Azure 中必须是唯一的, 并且包含5-50 个**字母数字**字符。</span><span class="sxs-lookup"><span data-stu-id="e33c6-111">The registry name must be unique within Azure, and contain 5-50 **alphanumeric** characters.</span></span> <span data-ttu-id="e33c6-112">有关命名的详细信息, 请参阅[Azure 资源的命名约定](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="e33c6-112">For more information on naming, see [Naming conventions for Azure resources](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions?azure-portal=true).</span></span>

    ```azurecli
    ACR_NAME=<registry-name>
    ```
1. <span data-ttu-id="e33c6-113">在云命令行管理程序编辑器中输入以下命令, 以创建新的容器注册表。</span><span class="sxs-lookup"><span data-stu-id="e33c6-113">Enter the following command into the cloud shell editor to create our new container registry.</span></span>

    ```azurecli
    az acr create --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACR_NAME --sku Premium
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    <span data-ttu-id="e33c6-114">下面的代码段是`az acr create`命令的示例响应。</span><span class="sxs-lookup"><span data-stu-id="e33c6-114">The following snippet is an example response from the `az acr create` command.</span></span> <span data-ttu-id="e33c6-115">在此示例中, 注册表名称为*myACR*。</span><span class="sxs-lookup"><span data-stu-id="e33c6-115">In this example, the registry name was *myACR*.</span></span> <span data-ttu-id="e33c6-116">请注意, 默认情况下, 以下 loginServer 值为小写形式的注册表名称。</span><span class="sxs-lookup"><span data-stu-id="e33c6-116">Note that the loginServer value below is the registry name in lowercase, by default.</span></span>  
    
    ```output
    {
      "adminUserEnabled": false,
      "creationDate": "2018-08-15T19:19:07.042178+00:00",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myACR0007",
      "location": "eastus",
      "loginServer": "myacr.azurecr.io",
      "name": "myACR",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sku": {
        "name": "Premium",
        "tier": "Premium"
      },
      "status": null,
      "storageAccount": null,
      "tags": {},
      "type": "Microsoft.ContainerRegistry/registries"
    }
    ```

> [!IMPORTANT]
> <span data-ttu-id="e33c6-117">本模块的其余部分中的命令将使用**ACR_NAME**变量值。</span><span class="sxs-lookup"><span data-stu-id="e33c6-117">Commands in the rest of this module will use the **ACR_NAME** variable value.</span></span> 

<span data-ttu-id="e33c6-118">在此单元中, 你使用 azure CLI 创建了 azure 容器注册表。</span><span class="sxs-lookup"><span data-stu-id="e33c6-118">In this unit, you created an Azure Container Registry using the Azure CLI.</span></span> <span data-ttu-id="e33c6-119">我们将在我们构建容器图像时在下一个单元中使用这个新的容器注册表。</span><span class="sxs-lookup"><span data-stu-id="e33c6-119">We'll use that new container registry in the next unit when we build container images.</span></span>
