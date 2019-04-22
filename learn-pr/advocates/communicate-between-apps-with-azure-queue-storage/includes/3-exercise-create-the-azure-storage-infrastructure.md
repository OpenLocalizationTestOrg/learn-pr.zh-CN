你已发现流量峰值会严重影响中间层。 为处理这种情况, 您已决定在您的文章上载应用程序中的前端和中间层之间添加队列。

创建队列的第一步是创建将存储数据的 Azure 存储帐户。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a>使用 Azure CLI 创建存储帐户

> [!TIP] 
> 通常情况下, 您应通过创建_资源组_来保存所有关联的资源来启动新项目。 在这种情况下, 我们将使用 Azure 沙盒, 它提供名为<rgn>[沙盒资源组名称]</rgn>的资源组。

使用`az storage account create`命令创建存储帐户。 可以在右侧的 "云命令行管理器" 窗口中键入命令。

该命令需要几个参数:

| 参数 | 值 |
|-----------|-------|
| `--name`  | 设置名称。 请注意, 存储帐户使用名称生成公用 URL-因此它必须是唯一的。 此外, 帐户名称必须介于3到24个字符之间, 并且只能由数字和小写字母组成。 我们建议您将前缀**文章**与随机号码后缀结合使用, 但你可以使用你喜欢的任何内容。 |
| `-g`        | 提供**资源组**, 请使用_<rgn>[沙盒资源组名称]</rgn>_ 作为值。 |
| `--kind`    | 设置**存储帐户类型**-使用_StorageV2_创建常规用途的 V2 帐户。 |
| `--sku`     | 设置**复制和存储类型**, 其默认值为_Standard_RAGRS_。 我们使用_Standard_LRS_ , 这意味着它只是数据中心内的本地冗余。 |
| `-l`        | 设置独立于资源组所有者的**位置**。 它是可选的, 但您可以使用它将队列放置在与资源组不同的区域中。 将其靠近您, 在沙盒中的可用区域列表中进行选择。 |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

下面是一个使用上述参数的示例命令行。 请务必更改`--name`参数。

```azurecli
az storage account create --name [unique-name] -g <rgn>[sandbox resource group name]</rgn> --kind StorageV2 --sku Standard_LRS
```

<!-- Paste tip-->
[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
