此单元将在您实际执行练习以创建服务器时熟悉下一个单元中所执行的步骤。 如果你在下一个设备中停滞, 请返回此部分。

## <a name="scenario"></a>方案

假设你使用的是本地 PostgreSQL 数据库。 你的公司现在正在寻找通过将你的服务器迁移到 Azure 中而扩展设备支持、可用性、数据跟踪和处理功能的信息。 您将研究自动为 PostgreSQL 服务器创建 Azure 数据库所需的工作量。

使用 azure 门户为 PostgreSQL 服务器创建单个 Azure 数据库非常简单。 创建多个数据库并在仅使用该门户的情况运行进行中维护可能会变得单调乏味。 当您希望自动执行管理任务时, 您将使用 Azure CLI 创建脚本。

使用 azure CLI, 可以自动创建 Microsoft Azure 内几乎所有资源。 在此单元中, 你将了解如何使用 azure CLI 自动管理对 PostgreSQL 服务器的 Azure 数据库。

## <a name="what-is-the-azure-cli"></a>什么是 Azure CLI？

[azure CLI](https://docs.microsoft.com/cli/azure?azure-portal=true)是 Microsoft 的用于管理 Azure 资源的跨平台命令行环境。 您可以从浏览器使用 azure 云命令行管理程序, 也可以在 macOS、Linux 或 Windows 上本地安装 azure cli。 Azure CLI 是通过使用 bash 或 PowerShell 从本地命令行运行的。 在本地运行 Azure CLI 需要额外的设置。 我们将使用 azure 云命令行管理程序执行 azure CLI 命令。

## <a name="what-is-azure-cloud-shell"></a>什么是 Azure 云命令行管理程序？

Azure 云命令行管理程序是一个托管在云中的基于浏览器的命令行管理程序, 允许您使用经过身份验证的会话连接到 Azure。 您可以执行 azure CLI 命令, 以自动管理 PostgreSQL 服务器的 Azure 数据库。 在云命令行管理程序中预安装并配置了常见的 Azure CLI 工具, 以便将其用于你的帐户。

> [!NOTE]
> 云命令行管理程序需要 Azure 存储资源, 以保留在云命令行管理程序中工作时创建的任何文件。 在首次启动时, 云命令行管理程序会代表你创建资源组、存储帐户和 Azure 文件共享。 这是一次性步骤, 将自动附加以供将来的所有云命令行管理器会话使用。

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a>使用 azure CLI 为 PostgreSQL 服务器创建 Azure 数据库

你将使用右侧的 azure 云命令行管理程序终端, 为使用 azure CLI 的 PostgreSQL 服务器创建 azure 数据库。

Azure CLI server 创建命令用法帮助显示所有可用参数, 如以下示例所示:

```azurecli
az postgres server create [-h] [--verbose] [--debug]
                            [--output {json,jsonc,table,tsv}]
                            [--query JMESPATH]
                            --resource-group RESOURCE_GROUP_NAME --name SERVER_NAME
                            --sku-name SKU_NAME [--location LOCATION]
                            --admin-user ADMINISTRATOR_LOGIN
                            [--admin-password ADMINISTRATOR_LOGIN_PASSWORD]
                            [--backup-retention BACKUP_RETENTION]
                            [--geo-redundant-backup GEO_REDUNDANT_BACKUP]
                            [--ssl-enforcement {Enabled,Disabled}]
                            [--storage-size STORAGE_MB]
                            [--tags [TAGS [TAGS ...]]]
                            [--version VERSION]
                            [--subscription _SUBSCRIPTION]

```

可选参数括在方括号中。 让我们来看一下常见的一些常见情况。

### <a name="parameters"></a>参数

`--resource-group <resource_group_name>`参数指定要在其中创建服务器的资源组。

您指定`admin-user`的`admin-password`服务器必须登录到服务器及其数据库。 请记住或记录此信息, 以便在以后与新服务器交互时使用。

您可以使用`--sku-name`参数指定定价层的一部分, 在此示例中为 "计算资源"。 值遵循约定`{pricing tier}_{compute generation}_{vCores}`。

说明

- `--sku-name B_Gen4_4`映射到 Basic、Gen 4 和 4 vCores。
- `--sku-name GP_Gen5_32`映射到常规用途、第5代和 32 vCores。
- `--sku-name MO_Gen5_2`映射到内存优化、第5代和第 2 vCores。

回想一下, 我们在使用门户创建服务器的单位中讨论了这三个定价层。

假设您要使用基本、第5个和1个 vCore 计算资源。 将参数指定为`--sku-name B_Gen5_1`。

您可以使用`--storage-size`参数指定定价层的一部分。 如果未指定值, 则默认为 5120 MB。 有效的存储大小范围为 5120 mb, 并以 1024 mb 增量增加到 1048576 mb。

当`--backup-retention`您需要指定备份的保留期 (以天为单位指定) 时, 使用此参数。 如果未指定值, 则默认为七天。

您可以使用`--version`参数指定要使用的 PostgreSQL 的主要版本。

现在, 您已看到使用 azure CLI 为 PostgreSQL 服务器创建 Azure 数据库的步骤。 在下一个单元中, 你将使用 azure CLI 为 PostgreSQL 服务器创建 Azure 数据库。