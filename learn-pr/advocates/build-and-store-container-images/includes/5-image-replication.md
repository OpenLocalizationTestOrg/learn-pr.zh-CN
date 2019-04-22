<span data-ttu-id="c0d16-101">假设您的公司具有部署到多个地区的计算工作负载, 以确保您有本地状态以满足您的分布式客户群的需要。</span><span class="sxs-lookup"><span data-stu-id="c0d16-101">Suppose your company has compute workloads deployed to several regions to make sure you have a local presence to serve your distributed customer base.</span></span> 

<span data-ttu-id="c0d16-102">您的目标是将容器注册表放置在运行图像的每个区域中。</span><span class="sxs-lookup"><span data-stu-id="c0d16-102">Your aim is to place a container registry in each region where images are run.</span></span> <span data-ttu-id="c0d16-103">此策略将允许网络关闭操作, 从而实现快速、可靠的图像层传输。</span><span class="sxs-lookup"><span data-stu-id="c0d16-103">This strategy will allow for network-close operations, enabling fast, reliable image layer transfers.</span></span> 

<span data-ttu-id="c0d16-104">地理位置复制使 Azure 容器注册表能够充当单个注册表, 为多个具有多主机区域注册表的区域提供服务。</span><span class="sxs-lookup"><span data-stu-id="c0d16-104">Geo-replication enables an Azure container registry to function as a single registry, serving several regions with multi-master regional registries.</span></span>

<span data-ttu-id="c0d16-105">地域复制的注册表具有以下优点:</span><span class="sxs-lookup"><span data-stu-id="c0d16-105">A geo-replicated registry provides the following benefits:</span></span>

- <span data-ttu-id="c0d16-106">可以跨多个区域使用单个注册表/图像/标记名称</span><span class="sxs-lookup"><span data-stu-id="c0d16-106">Single registry/image/tag names can be used across multiple regions</span></span>
- <span data-ttu-id="c0d16-107">网络-关闭来自区域部署的注册表访问</span><span class="sxs-lookup"><span data-stu-id="c0d16-107">Network-close registry access from regional deployments</span></span>
- <span data-ttu-id="c0d16-108">没有额外的出口费用, 因为图像是从本地副本、与容器主机位于同一区域的复制注册表中提取的</span><span class="sxs-lookup"><span data-stu-id="c0d16-108">No additional egress fees, as images are pulled from a local, replicated registry in the same region as your container host</span></span>
- <span data-ttu-id="c0d16-109">跨多个区域的注册表的单个管理</span><span class="sxs-lookup"><span data-stu-id="c0d16-109">Single management of a registry across multiple regions</span></span>

## <a name="replicate-a-registry-to-multiple-locations"></a><span data-ttu-id="c0d16-110">将注册表复制到多个位置</span><span class="sxs-lookup"><span data-stu-id="c0d16-110">Replicate a registry to multiple locations</span></span>

<span data-ttu-id="c0d16-111">在本练习中, 你将使用`az acr replication create` Azure CLI 命令将注册表从一个区域复制到另一个区域。</span><span class="sxs-lookup"><span data-stu-id="c0d16-111">In this exercise, you'll use the `az acr replication create` Azure CLI command to replicate your registry from one region to another.</span></span> 

1. <span data-ttu-id="c0d16-112">运行以下命令, 将注册表复制到另一个区域。</span><span class="sxs-lookup"><span data-stu-id="c0d16-112">Run the following command to replicate your registry to another region.</span></span> <span data-ttu-id="c0d16-113">在此示例中, 我们将复制到`japaneast`区域。</span><span class="sxs-lookup"><span data-stu-id="c0d16-113">In this example, we are replicating to the `japaneast` region.</span></span> <span data-ttu-id="c0d16-114">*$ACR _name*是您之前在模块中定义的用于保存容器注册表名称的变量。</span><span class="sxs-lookup"><span data-stu-id="c0d16-114">*$ACR_NAME* is the variable you defined earlier in the module to hold your container registry name.</span></span>

    ```azurecli
    az acr replication create --registry $ACR_NAME --location japaneast
    ```

    <span data-ttu-id="c0d16-115">下面的示例展示了此命令的输出如下所示:</span><span class="sxs-lookup"><span data-stu-id="c0d16-115">Here's an example of what the output from this command looks like:</span></span>
    
    ```output
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myACR0007/replications/japaneast",
      "location": "japaneast",
      "name": "japaneast",
      "provisioningState": "Succeeded",
      "resourceGroup": "myresourcegroup",
      "status": {
        "displayStatus": "Syncing",
        "message": null,
        "timestamp": "2018-08-15T20:22:09.275792+00:00"
      },
      "tags": {},
      "type": "Microsoft.ContainerRegistry/registries/replications"
    }
    ```

1. <span data-ttu-id="c0d16-116">最后一步是通过运行以下命令检索创建的所有容器图像副本。</span><span class="sxs-lookup"><span data-stu-id="c0d16-116">As a final step,  retrieve all container image replicas created by running the following command.</span></span> 

    ```azurecli
    az acr replication list --registry $ACR_NAME --output table
    ```

    <span data-ttu-id="c0d16-117">输出应如下所示:</span><span class="sxs-lookup"><span data-stu-id="c0d16-117">The output should look similar to the following:</span></span>
    
    ```console
    NAME       LOCATION    PROVISIONING STATE    STATUS
    ---------  ----------  --------------------  --------
    japaneast  japaneast   Succeeded             Ready
    eastus     eastus      Succeeded             Ready
    ```

<span data-ttu-id="c0d16-118">请注意, 您并不局限于 Azure CLI 来列出你的映像副本。</span><span class="sxs-lookup"><span data-stu-id="c0d16-118">Keep in mind that you are not limited to the Azure CLI to list your image replicas.</span></span> <span data-ttu-id="c0d16-119">在 azure 门户中, 选择`Replications` "azure 容器注册表" 将显示详细说明当前复制的地图。</span><span class="sxs-lookup"><span data-stu-id="c0d16-119">From within the Azure portal, selecting `Replications` for an Azure Container Registry displays a map that details current replications.</span></span> <span data-ttu-id="c0d16-120">通过选择地图上的区域, 可以将容器图像复制到其他区域。</span><span class="sxs-lookup"><span data-stu-id="c0d16-120">Container images can be replicated to additional regions by selecting the regions on the map.</span></span>

![Azure 门户中显示的容器复制映射](../media/replication-map.png)

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]
 

## <a name="summary"></a><span data-ttu-id="c0d16-122">摘要</span><span class="sxs-lookup"><span data-stu-id="c0d16-122">Summary</span></span>

<span data-ttu-id="c0d16-123">现在, 你已使用 Azure CLI 成功将容器映像复制到多个 azure 数据中心。</span><span class="sxs-lookup"><span data-stu-id="c0d16-123">You've now successfully replicated a container image to multiple Azure datacenters using the Azure CLI.</span></span> 