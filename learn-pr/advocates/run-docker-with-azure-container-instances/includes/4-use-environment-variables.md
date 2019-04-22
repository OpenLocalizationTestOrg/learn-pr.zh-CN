使用环境变量可以动态配置容器运行的应用程序或脚本。 您可以使用 azure CLI、PowerShell 或 azure 门户在创建容器时设置变量。 使用受保护的环境变量, 可以防止敏感信息在容器的输出中显示。

在这里, 你将创建一个 azure Cosmos DB 实例, 并使用环境变量将连接信息传递给 Azure 容器实例。 容器中的应用程序使用变量来写入和读取 Cosmos DB 中的数据。 您将创建环境变量和安全环境变量, 以便您可以看到它们之间的差异。

## <a name="deploy-azure-cosmos-db"></a>部署 Azure Cosmos DB

1. 当您部署 Azure Cosmos DB 时, 请提供一个唯一的数据库名称。 若要了解学习目的, 请从云命令行管理程序中运行此命令, 以创建保存唯一名称的 Bash 变量。

    ```bash
    COSMOS_DB_NAME=aci-cosmos-db-$RANDOM
    ```

1. 运行此`az cosmosdb create`命令以创建你的 Azure Cosmos DB 实例。

    ```azurecli
    COSMOS_DB_ENDPOINT=$(az cosmosdb create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $COSMOS_DB_NAME \
      --query documentEndpoint \
      --output tsv)
    ```

    此命令可能需要几分钟的时间才能完成。

    `$COSMOS_DB_NAME`指定唯一的数据库名称。 该命令将打印您的数据库的终结点地址。 此命令会将此地址保存到 Bash 变量`COSMOS_DB_ENDPOINT`中。

1. 运行`az cosmosdb list-keys`以获取 Azure Cosmos DB 连接密钥, 并将其存储在名为`COSMOS_DB_MASTERKEY`的 Bash 变量中。

    ```azurecli
    COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $COSMOS_DB_NAME \
      --query primaryMasterKey \
      --output tsv)
    ```

## <a name="deploy-a-container-that-works-with-your-database"></a>部署与您的数据库配合使用的容器

在这里, 你将创建可在 azure Cosmos DB 实例中读取和写入记录的 Azure 容器实例。

您在上一部分中创建的两个环境`COSMOS_DB_ENDPOINT`变量`COSMOS_DB_MASTERKEY`, 并保留连接到 Azure Cosmos DB 实例所需的值。

1. 运行以下`az container create`命令以创建容器。

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo \
      --image microsoft/azure-vote-front:cosmosdb \
      --ip-address Public \
      --location eastus \
      --environment-variables \
        COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
        COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
    ```

    **microsoft/azure-投票-前面: cosmosdb**是指运行虚拟投票应用程序的 Docker 图像。

    记下`--environment-variables`该参数。 此参数指定在容器启动时传递给容器的环境变量。 容器图像配置为查找这些环境变量。 在这里, 将传递 Azure Cosmos DB 终结点及其连接密钥的名称。

1. 运行`az container show`以获取容器的公共 IP 地址。

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo \
      --query ipAddress.ip \
      --output tsv
    ```

1. 在浏览器中, 导航到容器的 IP 地址。

    > [!IMPORTANT]
    > 有时, 容器需要一分钟或两分钟才能完全启动并能够接收连接。 如果在浏览器中导航到 IP 地址时没有响应, 请稍等片刻, 然后刷新页面。

    在应用程序可用后, 您会看到此情况。

    ![具有两种选择、猫或狗的 Azure 投票应用程序。](../media/4-azure-vote.png)

    尝试为猫或狗转换投票。 每个投票存储在 Azure Cosmos DB 实例中。

## <a name="use-secured-environment-variables-to-hide-connection-information"></a>使用安全环境变量隐藏连接信息

在前面的部分中, 您使用了两个环境变量来创建容器。 默认情况下, 可以通过 Azure 门户和纯文本形式的命令行工具访问这些环境变量。

在此部分中, 你将了解如何防止敏感信息 (如连接密钥) 以纯文本格式显示。

1. 让我们先查看操作中的当前行为。 运行以下`az container show`命令以显示容器的环境变量。

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo \
      --query containers[0].environmentVariables
    ```

    您会发现这两个值都显示为纯文本。 下面是一个示例。

    ```json
    [
      {
        "name": "COSMOS_DB_ENDPOINT",
        "secureValue": null,
        "value": "https://aci-cosmos.documents.azure.com:443/"
      },
      {
        "name": "COSMOS_DB_MASTERKEY",
        "secureValue": null,
        "value": "Xm5BwdLlCllBvrR26V00000000S2uOusuglhzwkE7dOPMBQ3oA30n3rKd8PKA13700000000095ynys863Ghgw=="
      }
    ]
    ```

    虽然这些值不会通过投票应用程序显示给用户, 但为了确保敏感信息 (如连接密钥) 不以纯文本格式存储, 这是一种很好的安全做法。

    安全环境变量阻止清除文本输出。 若要使用安全环境变量, 请使用`--secure-environment-variables`参数而不是`--environment-variables`参数。

1. 运行以下命令以创建一个名为**aci-secure**的第二个容器, 该容器使用安全环境变量。

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-secure \
      --image microsoft/azure-vote-front:cosmosdb \
      --ip-address Public \
      --location eastus \
      --secure-environment-variables \
        COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
        COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
    ```

    请注意`--secure-environment-variables`参数的用法。

1. 运行以下`az container show`命令以显示容器的环境变量。

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-secure \
      --query containers[0].environmentVariables
    ```

    此时, 您会看到您的环境变量不以纯文本格式显示。

    ```json
    [
      {
        "name": "COSMOS_DB_ENDPOINT",
        "secureValue": null,
        "value": null
      },
      {
        "name": "COSMOS_DB_MASTERKEY",
        "secureValue": null,
        "value": null
      }
    ]
    ```

    事实上, 环境变量的值根本不会出现。 这是正常的, 因为这些值指的是敏感信息。 在这里, 您只需知道环境变量存在。
