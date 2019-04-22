在此单元中, 你将使用 azure CLI 创建 azure 容器注册表。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]
 
## <a name="create-an-azure-container-registry"></a>创建 Azure 容器注册表

我们将在免费沙盒中工作, 因此无需创建您自己的资源组。 使用`az acr create`命令创建 Azure 容器注册表。 容器注册表名称在 Azure 中必须是唯一的, 并且包含5到50个字母数字字符。

在此示例中, 部署了高级注册表 SKU。 地理位置复制需要高级 SKU。 

首先, 我们在云命令行管理程序中定义一个名为 " **ACR_NAME** " 的环境变量, 以保留我们想要为新的容器注册表命名的名称。

1. 运行以下命令以定义名为 ACR_NAME 的变量。

    > [!IMPORTANT]
    > 在运行该命令之前, `<registry-name>`请将替换为您想要为新的容器注册表指定的唯一名称。 注册表名称在 Azure 中必须是唯一的, 并且包含5-50 个**字母数字**字符。 有关命名的详细信息, 请参阅[Azure 资源的命名约定](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions?azure-portal=true)。

    ```azurecli
    ACR_NAME=<registry-name>
    ```
1. 在云命令行管理程序编辑器中输入以下命令, 以创建新的容器注册表。

    ```azurecli
    az acr create --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACR_NAME --sku Premium
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    下面的代码段是`az acr create`命令的示例响应。 在此示例中, 注册表名称为*myACR*。 请注意, 默认情况下, 以下 loginServer 值为小写形式的注册表名称。  
    
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
> 本模块的其余部分中的命令将使用**ACR_NAME**变量值。 

在此单元中, 你使用 azure CLI 创建了 azure 容器注册表。 我们将在我们构建容器图像时在下一个单元中使用这个新的容器注册表。
