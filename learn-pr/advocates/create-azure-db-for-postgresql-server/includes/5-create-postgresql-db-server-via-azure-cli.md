您决定创建用于 PostgreSQL 服务器的 Azure 数据库, 以存储从服务器的健康设备捕获的路由。 根据历史捕获的数据量, 您知道您的服务器存储要求应设置为 20 GB。 为了支持您的处理需求, 您需要具有 1 vCore 的计算第5代支持。 您还知道需要保留期为数据备份15天。

## <a name="create-an-azure-postgresql-database-server-with-the-azure-cli"></a>使用 azure CLI 创建 azure PostgreSQL 数据库服务器

请注意, 您想要将服务器存储大小设置为 20 GB, 计算第5个时使用1个 vCore, 而保留期为15天, 用于备份数据。

1. 使用`az postgres server create`方法创建新的数据库。 有几个参数可供您指定:
    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`

2. 查看是否可以生成命令并完成参数, 而无需查看下面的解决方案。 下面是一些提示。
    - 将`<values>`替换为您自己的值。 
    - 请注意, 服务器名称必须由小写字母 "a'-'z" 组成, 数字0-9 和连字符。
    - 将<rgn>[沙盒资源组名称]</rgn>用作资源组。
    - 使用以下列表中的位置:  
        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    ```azurecli
    az postgres server create \
        --name <unique_server_name> \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location eastus \
        --sku-name B_Gen5_1 \
        --storage-size 20480 \
        --backup-retention 15 \
        --version 10 \
        --admin-user <admin_user_name> \
        --admin-password <server_admin_password>
    ```

    在执行时, 系统将需要几分钟的时间来处理信息。 继续执行并等待命令完成。

    完成后, 将返回描述服务器的 JavaScript 对象表示法 (JSON) 字符串。 如果出现故障, 则会显示一条错误消息。 您可以使用此错误信息查看并修复命令参数, 然后重试。

    JSON 对象的外观如下所示:

    ```json
    {
      "administratorLogin": "azureuser",
      "earliestRestoreDate": "2018-09-17T00:35:50.170000+00:00",
      "fullyQualifiedDomainName": "secondserver8.postgres.database.azure.com",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/<rgn>[sandbox Resource Group]</rgn>/providers/Microsoft.DBforPostgreSQL/servers/secondserver8",
      "location": "eastus",
      "name": "secondserver8",
      "resourceGroup": "<rgn>[sandbox Resource Group]</rgn>",
      "sku": {
        "capacity": 1,
        "family": "Gen5",
        "name": "B_Gen5_1",
        "size": null,
        "tier": "Basic"
      },
      "sslEnforcement": "Enabled",
      "storageProfile": {
        "backupRetentionDays": 15,
        "geoRedundantBackup": "Disabled",
        "storageMb": 20480
      },
      "tags": null,
      "type": "Microsoft.DBforPostgreSQL/servers",
      "userVisibleState": "Ready",
      "version": "10"
    }
    ```

你已使用 Azure CLI 成功创建了 PostgreSQL 服务器。 在下一个设备中, 你将了解如何配置服务器的安全设置。
