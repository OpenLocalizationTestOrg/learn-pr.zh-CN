现在我们有了一个应用程序, 我们需要一个 Azure 存储帐户才能使用。

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a>使用 azure CLI 创建 azure 存储帐户

我们将使用`az storage account create`命令创建新的存储帐户。 有几个参数可控制存储帐户的配置。

> [!div class="mx-tableFixed"]
> | 可选 | 说明 |
> |--------|-------------|
> | `--name` | 一个**存储帐户名称**。 该名称将用于生成用于访问帐户中的数据的公共 URL。 它在 Azure 中的所有现有存储帐户名称中必须是唯一的。 它的长度必须为3到24个字符, 并且只能包含小写字母和数字。 |
> | `--resource-group` | 使用**<rgn>[沙盒资源组名称]</rgn>** 将存储帐户放入免费沙盒中。 |
> | `--location` | 选择邻近的位置 (如下所示)。 |
> | `--kind` | 这将确定存储帐户_类型_。 选项包括`BlobStorage`、 `Storage`和`StorageV2`。 |
> | `--sku` | 这将决定存储帐户的性能和复制模型。 选项包括`Premium_LRS`、 `Standard_GRS`、 `Standard_LRS` `Standard_RAGRS`、和`Standard_ZRS`。 |
> | `--access-tier` | **访问层**仅用于 Blob 存储, 可用选项为 [`Cool` \| `Hot`]。 "**热访问" 层**非常适合于频繁访问的数据, 并且很**酷的 access 层**更适合于不经常访问的数据。 请注意, 这仅会__ 在您&mdash;创建 Blob 时设置默认值, 您可以为数据设置不同的值。 |
    
使用上表在右侧的云命令行管理程序中手工创建命令行以创建帐户。
- 使用唯一的名称。 我们建议将 "photostore" 之类的内容与你的姓名缩写和随机数字结合使用。 如果不是唯一的, 则会出现错误。
- 通常, 您会创建一个新的资源组来保存您的应用程序资源, 但在这种情况下, 请使用沙盒资源组 "**<rgn>[沙盒资源组名称]</rgn>**"。
- 将 "Standard_LRS" 用于**sku**。 这将使用标准存储和本地复制, 这在此示例中非常合适。
- 对**访问层**使用 "酷"。

### <a name="selecting-a-location"></a>选择位置
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

> [!TIP]
> 您可以使用`--location`参数选择一个位置, 如果您没有提供该存储帐户将在与您的资源组相同的位置中创建。 由于这是一个简单的练习, 如果愿意, 您可以省略以下命令中的参数。

### <a name="example-command"></a>示例命令

您可以使用下面的示例命令创建存储帐户。 请务必将`<name>`替换为唯一值。

```azurecli
az storage account create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --kind StorageV2 \
        --sku Standard_LRS \
        --access-tier Cool \
        --name <name>
```

> [!TIP]
> 如果你有兴趣浏览存储帐户的选项, 请务必完成**创建 Azure 存储帐户**模块, 在此模块中我们将深入介绍这些选项。

部署该帐户需要几分钟时间。 在 Azure 中工作时, 让我们来探究我们将用于此帐户的 api。
