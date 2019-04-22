假设您的公司具有部署到多个地区的计算工作负载, 以确保您有本地状态以满足您的分布式客户群的需要。 

您的目标是将容器注册表放置在运行图像的每个区域中。 此策略将允许网络关闭操作, 从而实现快速、可靠的图像层传输。 

地理位置复制使 Azure 容器注册表能够充当单个注册表, 为多个具有多主机区域注册表的区域提供服务。

地域复制的注册表具有以下优点:

- 可以跨多个区域使用单个注册表/图像/标记名称
- 网络-关闭来自区域部署的注册表访问
- 没有额外的出口费用, 因为图像是从本地副本、与容器主机位于同一区域的复制注册表中提取的
- 跨多个区域的注册表的单个管理

## <a name="replicate-a-registry-to-multiple-locations"></a>将注册表复制到多个位置

在本练习中, 你将使用`az acr replication create` Azure CLI 命令将注册表从一个区域复制到另一个区域。 

1. 运行以下命令, 将注册表复制到另一个区域。 在此示例中, 我们将复制到`japaneast`区域。 *$ACR _name*是您之前在模块中定义的用于保存容器注册表名称的变量。

    ```azurecli
    az acr replication create --registry $ACR_NAME --location japaneast
    ```

    下面的示例展示了此命令的输出如下所示:
    
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

1. 最后一步是通过运行以下命令检索创建的所有容器图像副本。 

    ```azurecli
    az acr replication list --registry $ACR_NAME --output table
    ```

    输出应如下所示:
    
    ```console
    NAME       LOCATION    PROVISIONING STATE    STATUS
    ---------  ----------  --------------------  --------
    japaneast  japaneast   Succeeded             Ready
    eastus     eastus      Succeeded             Ready
    ```

请注意, 您并不局限于 Azure CLI 来列出你的映像副本。 在 azure 门户中, 选择`Replications` "azure 容器注册表" 将显示详细说明当前复制的地图。 通过选择地图上的区域, 可以将容器图像复制到其他区域。

![Azure 门户中显示的容器复制映射](../media/replication-map.png)

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]
 

## <a name="summary"></a>摘要

现在, 你已使用 Azure CLI 成功将容器映像复制到多个 azure 数据中心。 