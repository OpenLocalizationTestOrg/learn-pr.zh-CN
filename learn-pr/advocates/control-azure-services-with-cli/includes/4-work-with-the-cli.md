Azure CLI 允许您键入命令, 并立即从命令行执行这些命令。 请记住, 软件开发示例中的总体目标是部署 web 应用程序的新内部版本以供测试。 我们来讨论您可以使用 Azure CLI 执行的任务的种类。

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>哪些 azure 资源可以使用 azure CLI 进行管理？

通过 azure CLI, 你可以控制每个 Azure 资源的几乎每个方面。 您可以使用资源组、存储、虚拟机、azure Active Directory (azure AD)、容器、机器学习等。

CLI 中的命令是按_组_和_子_组进行构造的。 每个组代表一个由 Azure 提供的服务, 子组将这些服务的命令分成一个逻辑分组。 `storage`例如, 组包含子组, 其中**包括帐户**、 **blob**、**存储**和**队列**。

那么, 您如何查找所需的特定命令呢？ 一种方法是使用`az find`。 例如, 如果您要查找可能有助于管理存储 blob 的命令, 则可以使用以下 find 命令:

```azurecli
az find -q blob
```

如果您已经知道所需的命令的名称, 则该`--help`命令的参数将提供有关命令的更多详细信息, 以及命令组的可用子命令的列表。 因此, 在我们的存储示例中, 您可以通过以下方式获取子组的列表和用于管理 blob 存储的命令:

```azurecli
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>如何创建 Azure 资源

创建新的 Azure 资源时, 通常有三个步骤: 连接到 Azure 订阅, 创建资源, 并验证创建是否成功。 下图显示了该过程的高级概述。

![该图显示了使用命令行界面创建 Azure 资源的步骤。](../media/4-create-resources-overview.png)

每个步骤对应于不同的 Azure CLI 命令。

### <a name="connect"></a>连接

由于你使用的是 azure cli 的本地安装, 因此需要先进行身份验证, 然后才能执行 azure 命令, 方法是使用 azure cli**登录**命令。

```azurecli
az login
```

azure CLI 通常会启动您的默认浏览器, 以打开 Azure 登录页。 如果这样做不起作用, 请按照命令行说明操作, 并在[https://aka.ms/devicelogin](https://aka.ms/devicelogin)中输入授权代码。

登录成功后, 你将连接到你的 Azure 订阅。

### <a name="create"></a>Create

您通常需要在创建新的 Azure 服务之前创建新的资源组, 因此我们将使用资源组作为示例来说明如何从 CLI 创建 Azure 资源。

Azure CLI**组 create**命令创建一个资源组。 您必须指定名称和位置。 该名称在你的订阅中必须是唯一的。 该位置确定将存储资源组的元数据的位置。 您可以使用如 "west US"、"北欧" 或 "西印度" 指定位置的字符串;或者, 可以使用单个等效词, 如 westus、northeurope 或 westindia。 核心语法为:

```azurecli
az group create --name <name> --location <location>
```

> [!IMPORTANT]
> 使用免费的 Azure 沙箱时, 不需要创建资源组。 相反, 您将使用预先创建的资源组。

### <a name="verify"></a>Verify

对于许多 azure 资源, azure CLI 提供了用于查看资源详细信息的**列表**子命令。 例如, azure CLI**组列表**命令列出了 azure 资源组。 在这里, 可以通过以下方法来验证资源组的创建是否成功:

```azurecli
az group list
```

若要获得更简洁的视图, 可以将输出格式设置为简单表格:

```azurecli
az group list --output table
```
