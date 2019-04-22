<span data-ttu-id="17209-101">我们需要做的第一件事是创建一个空的 Azure Cosmos DB 数据库和集合以供使用。</span><span class="sxs-lookup"><span data-stu-id="17209-101">The first thing we need to do is create an empty Azure Cosmos DB database and collection to work with.</span></span> <span data-ttu-id="17209-102">我们希望这些用户与您在此学习路径中的最后一个模块中创建的数据库相匹配: 一个名为 **"Products"** 的数据库和一个名为 **"衣服"** 的集合。</span><span class="sxs-lookup"><span data-stu-id="17209-102">We want them to match the ones you created in the last module in this Learning Path: a database named **"Products"** and a collection named **"Clothing"**.</span></span> <span data-ttu-id="17209-103">使用屏幕右侧的以下说明和 Azure 云命令行管理程序重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="17209-103">Use the following instructions and the Azure Cloud Shell on the right side of the screen to recreate the database.</span></span>

## <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a><span data-ttu-id="17209-104">使用 azure CLI 创建 azure Cosmos DB account + database</span><span class="sxs-lookup"><span data-stu-id="17209-104">Create an Azure Cosmos DB account + database with the Azure CLI</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-a-subscription"></a><span data-ttu-id="17209-105">选择订阅</span><span class="sxs-lookup"><span data-stu-id="17209-105">Select a subscription</span></span>

<span data-ttu-id="17209-106">如果你已使用 Azure 一段时间, 则可能会有多个订阅可供你使用。</span><span class="sxs-lookup"><span data-stu-id="17209-106">If you've been using Azure for a while, you might have multiple subscriptions available to you.</span></span> <span data-ttu-id="17209-107">对于可能具有 Visual Studio 订阅的开发人员, 以及对公司资源的另一种情况, 通常是这种情况。</span><span class="sxs-lookup"><span data-stu-id="17209-107">This is often the case for developers who might have a subscription for Visual Studio, and another for corporate resources.</span></span>

<span data-ttu-id="17209-108">Azure 沙盒已在云命令行管理程序中为你选择了 Concierge 订阅, 你可以使用这些步骤验证订阅设置。</span><span class="sxs-lookup"><span data-stu-id="17209-108">The Azure sandbox has already selected the Concierge Subscription for you in the Cloud Shell, and you can validate the subscription setting using these steps.</span></span> <span data-ttu-id="17209-109">或者, 在使用自己的订阅时, 可以使用以下步骤切换 Azure CLI 订阅。</span><span class="sxs-lookup"><span data-stu-id="17209-109">Or, when you are working with your own subscription, you can use the following steps to switch subscriptions with the Azure CLI.</span></span>

1. <span data-ttu-id="17209-110">首先列出可用的订阅。</span><span class="sxs-lookup"><span data-stu-id="17209-110">Start by listing the available subscriptions.</span></span>

    ```azurecli
    az account list --output table
    ```

   <span data-ttu-id="17209-111">如果您使用的是 Concierge 订阅, 则它应是唯一列出的项。</span><span class="sxs-lookup"><span data-stu-id="17209-111">If you're working with a Concierge Subscription, it should be the only one listed.</span></span>

1. <span data-ttu-id="17209-112">接下来, 如果默认订阅不是要使用的订阅, 则可以使用以下`account set`命令进行更改:</span><span class="sxs-lookup"><span data-stu-id="17209-112">Next, if the default subscription isn't the one you want to use, you can change it with the `account set` command:</span></span>

    ```azurecli
    az account set --subscription "<subscription name>"
    ```
    
1. <span data-ttu-id="17209-113">获取沙盒为您创建的资源组。</span><span class="sxs-lookup"><span data-stu-id="17209-113">Get the Resource Group that has been created for you by the sandbox.</span></span> <span data-ttu-id="17209-114">如果使用的是自己的订阅, 请跳过此步骤, 只需在下面的`RESOURCE_GROUP`环境变量中提供要使用的唯一名称即可。</span><span class="sxs-lookup"><span data-stu-id="17209-114">If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below.</span></span> <span data-ttu-id="17209-115">记下资源组名称。</span><span class="sxs-lookup"><span data-stu-id="17209-115">Take note of the Resource Group name.</span></span> <span data-ttu-id="17209-116">这是我们将在其中创建数据库的位置。</span><span class="sxs-lookup"><span data-stu-id="17209-116">This is where we will create our database.</span></span>

    ```azurecli
    az group list --out table
    ```
### <a name="setup-environment-variables"></a><span data-ttu-id="17209-117">安装环境变量</span><span class="sxs-lookup"><span data-stu-id="17209-117">Setup environment variables</span></span>

1. <span data-ttu-id="17209-118">设置几个环境变量, 无需每次都键入公共值。</span><span class="sxs-lookup"><span data-stu-id="17209-118">Set a few environment variables so you don't have to type the common values each time.</span></span> <span data-ttu-id="17209-119">首先, 为 Azure Cosmos DB 帐户设置名称, 例如`export NAME="mycosmosdbaccount"`。</span><span class="sxs-lookup"><span data-stu-id="17209-119">Start by setting a name for the Azure Cosmos DB account, for example `export NAME="mycosmosdbaccount"`.</span></span> <span data-ttu-id="17209-120">字段只能包含小写字母、数字和 '-' 字符, 并且必须介于3到31个字符之间。</span><span class="sxs-lookup"><span data-stu-id="17209-120">The field can contain only lowercase letters, numbers and the '-' character, and must be between 3 and 31 characters.</span></span>

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

1. <span data-ttu-id="17209-121">将资源组设置为使用现有沙盒资源组。</span><span class="sxs-lookup"><span data-stu-id="17209-121">Set the resource group to use the existing sandbox resource group.</span></span>

    ```azurecli
    export RESOURCE_GROUP="<rgn>[sandbox resource group name]</rgn>"
    ```

1. <span data-ttu-id="17209-122">选择最接近你的区域, 并设置环境变量, 例如`export LOCATION="EastUS"`。</span><span class="sxs-lookup"><span data-stu-id="17209-122">Select the region closest to you, and set the environment variable, such as `export LOCATION="EastUS"`.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

1. <span data-ttu-id="17209-123">为数据库名称设置变量。</span><span class="sxs-lookup"><span data-stu-id="17209-123">Set a variable for the database name.</span></span> <span data-ttu-id="17209-124">将其命名为 "Products", 使其与在最后一个模块中创建的数据库相匹配。</span><span class="sxs-lookup"><span data-stu-id="17209-124">Name it "Products" so it matches the database we created in the last module.</span></span>

    ```azurecli
    export DB_NAME="Products"
    ```

### <a name="create-a-resource-group-in-your-subscription"></a><span data-ttu-id="17209-125">在订阅中创建资源组</span><span class="sxs-lookup"><span data-stu-id="17209-125">Create a resource group in your subscription</span></span>

<span data-ttu-id="17209-126">当您在自己的订阅上创建 Cosmos DB 时, 您需要创建一个新的资源组来保存所有相关资源。</span><span class="sxs-lookup"><span data-stu-id="17209-126">When you are creating a Cosmos DB on your own subscription you will want to create a new resource group to hold all the related resources.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17209-127">如果使用的是 Microsoft 学习提供的 Azure 沙箱, 则无需执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="17209-127">If you are using the Azure sandbox provided by Microsoft Learn, then you do not need to execute this step.</span></span> <span data-ttu-id="17209-128">相反, 请确保将`RESOURCE_GROUP`上面的变量设置为**<rgn>[沙盒资源组名称</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="17209-128">Instead, make sure the `RESOURCE_GROUP` variable above is set to **<rgn>[sandbox Resource Group Name</rgn>**.</span></span>

<span data-ttu-id="17209-129">在您自己的订阅中, 可以使用以下命令来创建资源组。</span><span class="sxs-lookup"><span data-stu-id="17209-129">In your own subscription you would use the following command to create the Resource Group.</span></span> 

```azurecli
az group create --name <name> --location <location>
```

### <a name="create-the-azure-cosmos-db-account"></a><span data-ttu-id="17209-130">创建 Azure Cosmos DB 帐户</span><span class="sxs-lookup"><span data-stu-id="17209-130">Create the Azure Cosmos DB account</span></span>

1. <span data-ttu-id="17209-131">使用`cosmosdb create`命令创建 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="17209-131">Create the Azure Cosmos DB account with the `cosmosdb create` command.</span></span> <span data-ttu-id="17209-132">该命令使用以下参数, 如果将环境变量设置为 "建议", 则无任何修改即可运行。</span><span class="sxs-lookup"><span data-stu-id="17209-132">The command uses the following parameters and can be run with no modifications if you set the environment variables as recommended.</span></span>
    - <span data-ttu-id="17209-133">`--name`: 资源的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="17209-133">`--name`: Unique name for the resource.</span></span>
    - <span data-ttu-id="17209-134">`--kind`: 数据库的种类, 请使用_GlobalDocumentDB_。</span><span class="sxs-lookup"><span data-stu-id="17209-134">`--kind`: Kind of database, use _GlobalDocumentDB_.</span></span>
    - <span data-ttu-id="17209-135">`--resource-group`: 资源组。</span><span class="sxs-lookup"><span data-stu-id="17209-135">`--resource-group`: The resource group.</span></span> <span data-ttu-id="17209-136">使用**<rgn>[沙盒资源组]</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="17209-136">Use **<rgn>[sandbox Resource Group]</rgn>**.</span></span> <span data-ttu-id="17209-137">应将其分配给`RESOURCE_GROUP`变量。</span><span class="sxs-lookup"><span data-stu-id="17209-137">It should be assigned to the `RESOURCE_GROUP` variable.</span></span>

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

    <span data-ttu-id="17209-138">此命令需要几分钟的时间才能完成, 云命令行管理程序将在部署后显示新帐户的设置。</span><span class="sxs-lookup"><span data-stu-id="17209-138">The command takes a few minutes to complete and the cloud shell displays the settings for the new account once it's deployed.</span></span>

1. <span data-ttu-id="17209-139">在帐户`Products`中创建数据库。</span><span class="sxs-lookup"><span data-stu-id="17209-139">Create the `Products` database in the account.</span></span>

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

1. <span data-ttu-id="17209-140">最后, 创建`Clothing`集合。</span><span class="sxs-lookup"><span data-stu-id="17209-140">Finally, create the `Clothing` collection.</span></span>

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

<span data-ttu-id="17209-141">现在, 你已拥有 Azure Cosmos DB 帐户、数据库和集合, 让我们添加一些数据!</span><span class="sxs-lookup"><span data-stu-id="17209-141">Now that you have your Azure Cosmos DB account, database, and collection, let's go add some data!</span></span>
