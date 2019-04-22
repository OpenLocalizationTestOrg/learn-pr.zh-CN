您现在可以创建新的事件中心了。 创建事件中心后, 你将使用 Azure 门户查看你的新中心。

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-some-defaults-in-the-azure-cli"></a>在 Azure CLI 中设置一些默认值

首先, 我们在云命令行管理程序中为 Azure CLI 提供一些默认值。 这将使您无需每次都键入这些项。 尤其是, 让我们设置_资源组_和_位置_。 从以下列表中选择一个位置。

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

然后, 在 Azure CLI 中键入以下命令, 确保用一个接近你的位置替换该位置。

```azurecli
az configure --defaults group=<rgn>[sandbox Resource Group]</rgn> location=westus2
```

## <a name="create-an-event-hubs-namespace"></a>创建事件中心命名空间

使用以下步骤, 通过 Azure 云命令行管理程序支持的 bash 命令行管理程序来创建事件中心命名空间:

1. 使用`az eventhubs namespace create`命令创建事件中心命名空间。 使用以下参数。

    > [!div class="mx-tableFixed"]
    > |参数      |说明|
    > |---------------|-----------|
    > |--名称 (必需)      |为事件中心命名空间输入6-50 个字符的唯一名称。 名称应仅包含字母、数字和连字符。 它应以字母开头, 以字母或数字结尾。|
    > |--资源-组 (必需) | 这将是由默认值提供的预创建的 Azure 沙盒资源组。 |
    > |--l (可选)     |输入你最近的 Azure 数据中心的位置, 这将使用你的默认位置。|
    > |--sku (可选) | 命名空间的定价层 [Basic | standard], 默认值为_Standard_。 这将确定连接和消费者阈值。 |

    将名称设置为环境变量, 以便我们可以重复使用它。

    ```azurecli
    NS_NAME=myEvt-HubNs1
    ````

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```azurecli
    az eventhubs namespace create --name $NS_NAME
    ```

    > [!NOTE]
    > Azure 非常高有关名称的信息, 如果名称存在或无效, CLI 将返回**错误的请求**。 通过更改环境变量并重新发起命令来尝试其他名称。


1. 使用以下命令提取事件中心命名空间的连接字符串。 你将需要此信息来配置应用程序, 以使用事件中心发送和接收邮件。

    ```azurecli
    az eventhubs namespace authorization-rule keys list --name RootManageSharedAccessKey --namespace-name $NS_NAME
    ```

    > [!div class="mx-tableFixed"]
    > |参数      |说明|
    > |---------------|-----------|
    > |--资源-组 (必需)  | 这将是由默认值提供的预创建的 Azure 沙盒资源组。 |
    > |--命名空间名称 (必需)  | 输入您创建的命名空间的名称。 |

    此命令返回一个包含事件中心命名空间的连接字符串的 JSON 块, 稍后将使用该块配置发布者和使用者应用程序。 保存以下项的值以供将来使用。

    - **primaryConnectionString**
    - **关键字**

## <a name="create-an-event-hub"></a>创建事件中心

使用以下步骤创建新的事件中心:

1. 使用`eventhub create`命令创建新的事件中心。 它需要以下参数:

    > [!div class="mx-tableFixed"]
    > |参数      |说明|
    > |---------------|-----------|
    > |--名称 (必需)  |为事件中心输入名称。|
    > |--资源-组 (必需)  |资源组所有者。|
    > |--命名空间名称 (必需)      |输入您创建的命名空间。|

    让我们先在环境变量中定义事件中心名称。

    ```azurecli
    HUB_NAME=[name]
    ```

    ```azurecli
    az eventhubs eventhub create --name $HUB_NAME --namespace-name $NS_NAME
    ```

1. 使用`eventhub show`命令查看事件中心的详细信息。 它采用了:

    > [!div class="mx-tableFixed"]
    > |参数      |说明|
    > |---------------|-----------|
    > |--资源-组 (必需)  |资源组所有者。|
    > |--命名空间名称 (必需)      |输入您创建的命名空间。|
    > |--名称 (必需)|事件中心的名称。|

    ```azurecli
    az eventhubs eventhub show --namespace-name $NS_NAME --name $HUB_NAME
    ```

## <a name="view-the-event-hub-in-the-azure-portal"></a>在 Azure 门户中查看事件中心

接下来, 我们来看看它在 Azure 门户中的显示效果。

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 使用门户顶部的搜索栏查找事件中心命名空间。

1. 选择您的命名空间将其打开。

1. 在 "**实体**" 部分下选择 "**事件中心命名空间**"。

1. 单击 "**事件中心**"。

    事件中心显示状态为 "**活动**", "**邮件保留**" 的默认值为 "(*7*)" 和 "**分区计数**为 (*4*)"。

    ![Azure 门户中显示的事件中心](../media/3-event-hub.png)

## <a name="summary"></a>摘要

现在, 您已经创建了一个新的事件中心, 并且您已准备好配置发布者和使用者应用程序所需的所有信息。
