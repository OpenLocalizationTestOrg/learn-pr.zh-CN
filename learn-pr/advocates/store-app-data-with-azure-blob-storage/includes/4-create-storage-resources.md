一旦我们了解如何跨存储帐户、容器和 blob 存储数据, 我们就可以考虑我们需要创建的 Azure 资源来支持应用。

### <a name="storage-accounts"></a>存储帐户

存储帐户创建是部署和运行应用之前发生的管理/管理活动。 帐户通常由部署或环境安装脚本、Azure 资源管理器模板创建, 或由管理员手动创建。 除管理工具之外的应用程序通常不应具有创建存储帐户的权限。

### <a name="containers"></a>存放

与存储帐户创建不同, 创建容器是一个从应用程序中执行的轻型活动。 应用程序在其工作过程中创建和删除容器的情况并不常见。

对于依赖于具有硬编码或预配置名称的已知容器集的应用程序, 通常的做法是让应用在启动时创建所需的容器, 如果它们尚不存在, 则使用第一次使用。 如果让您的应用程序创建容器, 而不是将其作为应用程序的部署的一部分, 则无需应用程序和部署过程来了解应用程序使用的容器的名称。

## <a name="exercise"></a>健身

我们将通过添加代码来使用 Azure Blob 存储来完成未完成的 ASP.NET 核心应用。 此练习更详细地介绍了如何浏览 Blob 存储 API, 而不仅仅是设计组织和命名方案, 但下面是有关应用程序及其存储数据的方式的快速概述。

![FileUploader web 应用程序的屏幕截图](../media/4-fileuploader-with-files.PNG)

我们的应用程序的工作方式类似于接受文件上载并使其可供下载的共享文件夹。 它不使用数据库来组织 blob &mdash; , 它会 sanitizes 上载文件的名称, 并直接将其用作 blob 名称。 所有上载的文件都存储在单个容器中。

我们将首先编译和运行的代码, 但负责存储和加载数据的部分是空的。 完成此代码后, 我们会将应用程序部署到 Azure 应用服务, 并对其进行测试。

[!include[](../../../includes/azure-sandbox-activate.md)]

让我们为我们的应用程序设置存储基础结构。

### <a name="storage-account"></a>存储帐户

我们将通过 azure CLI 使用 azure 云命令行管理程序创建存储帐户。 你需要为存储帐户&mdash;提供一个唯一的名称, 以便稍后对其进行记录。 在下面的示例中, 我们使用的是 "东 US", 但您可以将其更改为 "任何可用的位置" 列表中的。

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

执行以下命令以创建存储帐户。 

```azurecli
az storage account create \
  --kind StorageV2 \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --location eastus \
  --name <your-unique-storage-account-name>
```

> [!NOTE]
> 为什么`--kind StorageV2`？ 有几种不同类型的存储帐户。 在大多数情况下, 应使用通用 v2 帐户。 您需要明确指定`--kind StorageV2`的唯一原因是, 通用 v2 帐户仍是非常新的, 并且尚未在 azure 门户或 azure CLI 中进行默认设置。

### <a name="container"></a>Container

我们将在此模块中使用的应用程序使用单个容器。 我们将按照最佳做法, 让应用在启动时创建容器。 但是, 可以从 Azure CLI 中执行容器创建: 如果想`az storage container create -h`要查看文档, 请在云命令行管理程序终端中运行。