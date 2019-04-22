<span data-ttu-id="50976-101">您决定创建用于 PostgreSQL 服务器的 Azure 数据库, 以存储从服务器的健康设备捕获的路由。</span><span class="sxs-lookup"><span data-stu-id="50976-101">You decide to create an Azure Database for PostgreSQL server to store routes captured from runners' fitness devices.</span></span> <span data-ttu-id="50976-102">根据历史捕获的数据量, 您知道您的服务器存储要求应设置为 20 GB。</span><span class="sxs-lookup"><span data-stu-id="50976-102">Based on historic captured data volumes, you know your server storage requirements should be set at 20 GB.</span></span> <span data-ttu-id="50976-103">为了支持您的处理需求, 您需要具有 1 vCore 的计算第5代支持。</span><span class="sxs-lookup"><span data-stu-id="50976-103">To support your processing requirements, you need compute Gen 5 support with 1 vCore.</span></span> <span data-ttu-id="50976-104">您还知道需要保留期为数据备份15天。</span><span class="sxs-lookup"><span data-stu-id="50976-104">You also know that you require a retention period of 15 days for data backups.</span></span>

## <a name="create-an-azure-postgresql-database-server-with-the-azure-cli"></a><span data-ttu-id="50976-105">使用 azure CLI 创建 azure PostgreSQL 数据库服务器</span><span class="sxs-lookup"><span data-stu-id="50976-105">Create an Azure PostgreSQL database server with the Azure CLI</span></span>

<span data-ttu-id="50976-106">请注意, 您想要将服务器存储大小设置为 20 GB, 计算第5个时使用1个 vCore, 而保留期为15天, 用于备份数据。</span><span class="sxs-lookup"><span data-stu-id="50976-106">Keep in mind you want to set your server storage size at 20 GB, compute Gen 5 support with 1 vCore and a retention period of 15 days for data backups.</span></span>

1. <span data-ttu-id="50976-107">使用`az postgres server create`方法创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="50976-107">Use the `az postgres server create` method to create a new database.</span></span> <span data-ttu-id="50976-108">有几个参数可供您指定:</span><span class="sxs-lookup"><span data-stu-id="50976-108">There are several parameters that you'll specify:</span></span>
    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`

2. <span data-ttu-id="50976-109">查看是否可以生成命令并完成参数, 而无需查看下面的解决方案。</span><span class="sxs-lookup"><span data-stu-id="50976-109">See if you can build the command and complete the parameters without looking at the solution below.</span></span> <span data-ttu-id="50976-110">下面是一些提示。</span><span class="sxs-lookup"><span data-stu-id="50976-110">Here are some tips.</span></span>
    - <span data-ttu-id="50976-111">将`<values>`替换为您自己的值。</span><span class="sxs-lookup"><span data-stu-id="50976-111">Replace the `<values>` with your own values.</span></span> 
    - <span data-ttu-id="50976-112">请注意, 服务器名称必须由小写字母 "a'-'z" 组成, 数字0-9 和连字符。</span><span class="sxs-lookup"><span data-stu-id="50976-112">Remember that the server name must be  made up of lowercase letters 'a'-'z', the numbers 0-9 and the hyphen.</span></span>
    - <span data-ttu-id="50976-113">将<rgn>[沙盒资源组名称]</rgn>用作资源组。</span><span class="sxs-lookup"><span data-stu-id="50976-113">Use <rgn>[sandbox resource group name]</rgn> as the resource group.</span></span>
    - <span data-ttu-id="50976-114">使用以下列表中的位置:</span><span class="sxs-lookup"><span data-stu-id="50976-114">Use a location from the following list:</span></span>  
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

    <span data-ttu-id="50976-115">在执行时, 系统将需要几分钟的时间来处理信息。</span><span class="sxs-lookup"><span data-stu-id="50976-115">The system will take a few minutes to process the information when executed.</span></span> <span data-ttu-id="50976-116">继续执行并等待命令完成。</span><span class="sxs-lookup"><span data-stu-id="50976-116">Go ahead and wait for the command to complete.</span></span>

    <span data-ttu-id="50976-117">完成后, 将返回描述服务器的 JavaScript 对象表示法 (JSON) 字符串。</span><span class="sxs-lookup"><span data-stu-id="50976-117">Once it's done, a JavaScript Object Notation (JSON) string that describes the server is returned.</span></span> <span data-ttu-id="50976-118">如果出现故障, 则会显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="50976-118">If there was a failure, an error message is displayed.</span></span> <span data-ttu-id="50976-119">您可以使用此错误信息查看并修复命令参数, 然后重试。</span><span class="sxs-lookup"><span data-stu-id="50976-119">You can use this error information to review and fix your command parameters and try again.</span></span>

    <span data-ttu-id="50976-120">JSON 对象的外观如下所示:</span><span class="sxs-lookup"><span data-stu-id="50976-120">The JSON object will look something like:</span></span>

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

<span data-ttu-id="50976-121">你已使用 Azure CLI 成功创建了 PostgreSQL 服务器。</span><span class="sxs-lookup"><span data-stu-id="50976-121">You've successfully created a PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="50976-122">在下一个设备中, 你将了解如何配置服务器的安全设置。</span><span class="sxs-lookup"><span data-stu-id="50976-122">In the next unit, you'll see how to configure your server's security settings.</span></span>
