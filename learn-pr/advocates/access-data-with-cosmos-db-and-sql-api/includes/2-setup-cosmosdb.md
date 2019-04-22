我们需要做的第一件事是创建一个空的 Azure Cosmos DB 数据库和集合以供使用。 我们希望这些用户与您在此学习路径中的最后一个模块中创建的数据库相匹配: 一个名为 **"Products"** 的数据库和一个名为 **"衣服"** 的集合。 使用屏幕右侧的以下说明和 Azure 云命令行管理程序重新创建数据库。

## <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a>使用 azure CLI 创建 azure Cosmos DB account + database

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-a-subscription"></a>选择订阅

如果你已使用 Azure 一段时间, 则可能会有多个订阅可供你使用。 对于可能具有 Visual Studio 订阅的开发人员, 以及对公司资源的另一种情况, 通常是这种情况。

Azure 沙盒已在云命令行管理程序中为你选择了 Concierge 订阅, 你可以使用这些步骤验证订阅设置。 或者, 在使用自己的订阅时, 可以使用以下步骤切换 Azure CLI 订阅。

1. 首先列出可用的订阅。

    ```azurecli
    az account list --output table
    ```

   如果您使用的是 Concierge 订阅, 则它应是唯一列出的项。

1. 接下来, 如果默认订阅不是要使用的订阅, 则可以使用以下`account set`命令进行更改:

    ```azurecli
    az account set --subscription "<subscription name>"
    ```
    
1. 获取沙盒为您创建的资源组。 如果使用的是自己的订阅, 请跳过此步骤, 只需在下面的`RESOURCE_GROUP`环境变量中提供要使用的唯一名称即可。 记下资源组名称。 这是我们将在其中创建数据库的位置。

    ```azurecli
    az group list --out table
    ```
### <a name="setup-environment-variables"></a>安装环境变量

1. 设置几个环境变量, 无需每次都键入公共值。 首先, 为 Azure Cosmos DB 帐户设置名称, 例如`export NAME="mycosmosdbaccount"`。 字段只能包含小写字母、数字和 '-' 字符, 并且必须介于3到31个字符之间。

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

1. 将资源组设置为使用现有沙盒资源组。

    ```azurecli
    export RESOURCE_GROUP="<rgn>[sandbox resource group name]</rgn>"
    ```

1. 选择最接近你的区域, 并设置环境变量, 例如`export LOCATION="EastUS"`。

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

1. 为数据库名称设置变量。 将其命名为 "Products", 使其与在最后一个模块中创建的数据库相匹配。

    ```azurecli
    export DB_NAME="Products"
    ```

### <a name="create-a-resource-group-in-your-subscription"></a>在订阅中创建资源组

当您在自己的订阅上创建 Cosmos DB 时, 您需要创建一个新的资源组来保存所有相关资源。

> [!IMPORTANT]
> 如果使用的是 Microsoft 学习提供的 Azure 沙箱, 则无需执行此步骤。 相反, 请确保将`RESOURCE_GROUP`上面的变量设置为**<rgn>[沙盒资源组名称</rgn>**。

在您自己的订阅中, 可以使用以下命令来创建资源组。 

```azurecli
az group create --name <name> --location <location>
```

### <a name="create-the-azure-cosmos-db-account"></a>创建 Azure Cosmos DB 帐户

1. 使用`cosmosdb create`命令创建 Azure Cosmos DB 帐户。 该命令使用以下参数, 如果将环境变量设置为 "建议", 则无任何修改即可运行。
    - `--name`: 资源的唯一名称。
    - `--kind`: 数据库的种类, 请使用_GlobalDocumentDB_。
    - `--resource-group`: 资源组。 使用**<rgn>[沙盒资源组]</rgn>**。 应将其分配给`RESOURCE_GROUP`变量。

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

    此命令需要几分钟的时间才能完成, 云命令行管理程序将在部署后显示新帐户的设置。

1. 在帐户`Products`中创建数据库。

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

1. 最后, 创建`Clothing`集合。

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

现在, 你已拥有 Azure Cosmos DB 帐户、数据库和集合, 让我们添加一些数据!
