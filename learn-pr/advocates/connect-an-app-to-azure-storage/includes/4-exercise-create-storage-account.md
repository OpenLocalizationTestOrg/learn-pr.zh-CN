<span data-ttu-id="40682-101">现在我们有了一个应用程序, 我们需要一个 Azure 存储帐户才能使用。</span><span class="sxs-lookup"><span data-stu-id="40682-101">Now that we have an app, we need an Azure storage account to work with.</span></span>

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a><span data-ttu-id="40682-102">使用 azure CLI 创建 azure 存储帐户</span><span class="sxs-lookup"><span data-stu-id="40682-102">Use the Azure CLI to create an Azure storage account</span></span>

<span data-ttu-id="40682-103">我们将使用`az storage account create`命令创建新的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="40682-103">We will use the `az storage account create` command to create a new storage account.</span></span> <span data-ttu-id="40682-104">有几个参数可控制存储帐户的配置。</span><span class="sxs-lookup"><span data-stu-id="40682-104">There are several parameters to control the configuration of the storage account.</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="40682-105">可选</span><span class="sxs-lookup"><span data-stu-id="40682-105">Option</span></span> | <span data-ttu-id="40682-106">说明</span><span class="sxs-lookup"><span data-stu-id="40682-106">Description</span></span> |
> |--------|-------------|
> | `--name` | <span data-ttu-id="40682-107">一个**存储帐户名称**。</span><span class="sxs-lookup"><span data-stu-id="40682-107">A **Storage account name**.</span></span> <span data-ttu-id="40682-108">该名称将用于生成用于访问帐户中的数据的公共 URL。</span><span class="sxs-lookup"><span data-stu-id="40682-108">The name will be used to generate the public URL used to access the data in the account.</span></span> <span data-ttu-id="40682-109">它在 Azure 中的所有现有存储帐户名称中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="40682-109">It must be unique across all existing storage account names in Azure.</span></span> <span data-ttu-id="40682-110">它的长度必须为3到24个字符, 并且只能包含小写字母和数字。</span><span class="sxs-lookup"><span data-stu-id="40682-110">It must be 3 to 24 characters long and can contain only lowercase letters and numbers.</span></span> |
> | `--resource-group` | <span data-ttu-id="40682-111">使用**<rgn>[沙盒资源组名称]</rgn>** 将存储帐户放入免费沙盒中。</span><span class="sxs-lookup"><span data-stu-id="40682-111">Use **<rgn>[sandbox resource group name]</rgn>** to place the storage account into the free sandbox.</span></span> |
> | `--location` | <span data-ttu-id="40682-112">选择邻近的位置 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="40682-112">Select a location near you (see below).</span></span> |
> | `--kind` | <span data-ttu-id="40682-113">这将确定存储帐户_类型_。</span><span class="sxs-lookup"><span data-stu-id="40682-113">This determines the storage account _type_.</span></span> <span data-ttu-id="40682-114">选项包括`BlobStorage`、 `Storage`和`StorageV2`。</span><span class="sxs-lookup"><span data-stu-id="40682-114">Options include `BlobStorage`, `Storage`, and `StorageV2`.</span></span> |
> | `--sku` | <span data-ttu-id="40682-115">这将决定存储帐户的性能和复制模型。</span><span class="sxs-lookup"><span data-stu-id="40682-115">This decides the storage account performance and replication model.</span></span> <span data-ttu-id="40682-116">选项包括`Premium_LRS`、 `Standard_GRS`、 `Standard_LRS` `Standard_RAGRS`、和`Standard_ZRS`。</span><span class="sxs-lookup"><span data-stu-id="40682-116">Options include `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, and `Standard_ZRS`.</span></span> |
> | `--access-tier` | <span data-ttu-id="40682-117">**访问层**仅用于 Blob 存储, 可用选项为 [`Cool` \| `Hot`]。</span><span class="sxs-lookup"><span data-stu-id="40682-117">The **Access tier** is only used for Blob storage, available options are [`Cool` \| `Hot`].</span></span> <span data-ttu-id="40682-118">"**热访问" 层**非常适合于频繁访问的数据, 并且很**酷的 access 层**更适合于不经常访问的数据。</span><span class="sxs-lookup"><span data-stu-id="40682-118">The **Hot Access Tier** is ideal for frequently accessed data, and the **Cool Access Tier** is better for infrequently accessed data.</span></span> <span data-ttu-id="40682-119">请注意, 这仅会__ 在您&mdash;创建 Blob 时设置默认值, 您可以为数据设置不同的值。</span><span class="sxs-lookup"><span data-stu-id="40682-119">Note that this only sets the _default_ value&mdash;when you create a Blob, you can set a different value for the data.</span></span> |
    
<span data-ttu-id="40682-120">使用上表在右侧的云命令行管理程序中手工创建命令行以创建帐户。</span><span class="sxs-lookup"><span data-stu-id="40682-120">Use the above table to craft a command line in the Cloud Shell on the right to create the account.</span></span>
- <span data-ttu-id="40682-121">使用唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="40682-121">Use a unique name.</span></span> <span data-ttu-id="40682-122">我们建议将 "photostore" 之类的内容与你的姓名缩写和随机数字结合使用。</span><span class="sxs-lookup"><span data-stu-id="40682-122">We recommend something like "photostore" with your initials and a random number.</span></span> <span data-ttu-id="40682-123">如果不是唯一的, 则会出现错误。</span><span class="sxs-lookup"><span data-stu-id="40682-123">You will get an error if it's not unique.</span></span>
- <span data-ttu-id="40682-124">通常, 您会创建一个新的资源组来保存您的应用程序资源, 但在这种情况下, 请使用沙盒资源组 "**<rgn>[沙盒资源组名称]</rgn>**"。</span><span class="sxs-lookup"><span data-stu-id="40682-124">Normally you would create a new resource group to hold your app resources, but in this case, use the sandbox resource group "**<rgn>[sandbox resource group name]</rgn>**".</span></span>
- <span data-ttu-id="40682-125">将 "Standard_LRS" 用于**sku**。</span><span class="sxs-lookup"><span data-stu-id="40682-125">Use "Standard_LRS" for the **sku**.</span></span> <span data-ttu-id="40682-126">这将使用标准存储和本地复制, 这在此示例中非常合适。</span><span class="sxs-lookup"><span data-stu-id="40682-126">This will use standard storage with local replication, which is fine for this example.</span></span>
- <span data-ttu-id="40682-127">对**访问层**使用 "酷"。</span><span class="sxs-lookup"><span data-stu-id="40682-127">Use "Cool" for the **Access Tier**.</span></span>

### <a name="selecting-a-location"></a><span data-ttu-id="40682-128">选择位置</span><span class="sxs-lookup"><span data-stu-id="40682-128">Selecting a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

> [!TIP]
> <span data-ttu-id="40682-129">您可以使用`--location`参数选择一个位置, 如果您没有提供该存储帐户将在与您的资源组相同的位置中创建。</span><span class="sxs-lookup"><span data-stu-id="40682-129">You can select a location with the `--location` parameter, if you don't supply one the storage account will be created in the same location as your resource group.</span></span> <span data-ttu-id="40682-130">由于这是一个简单的练习, 如果愿意, 您可以省略以下命令中的参数。</span><span class="sxs-lookup"><span data-stu-id="40682-130">Since this is a simple exercise, you can omit the parameter from the below command if you prefer.</span></span>

### <a name="example-command"></a><span data-ttu-id="40682-131">示例命令</span><span class="sxs-lookup"><span data-stu-id="40682-131">Example command</span></span>

<span data-ttu-id="40682-132">您可以使用下面的示例命令创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="40682-132">You can use the following example command to create a storage account.</span></span> <span data-ttu-id="40682-133">请务必将`<name>`替换为唯一值。</span><span class="sxs-lookup"><span data-stu-id="40682-133">Remember to replace `<name>` with a unique value.</span></span>

```azurecli
az storage account create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --kind StorageV2 \
        --sku Standard_LRS \
        --access-tier Cool \
        --name <name>
```

> [!TIP]
> <span data-ttu-id="40682-134">如果你有兴趣浏览存储帐户的选项, 请务必完成**创建 Azure 存储帐户**模块, 在此模块中我们将深入介绍这些选项。</span><span class="sxs-lookup"><span data-stu-id="40682-134">If you are interested in exploring the options for the storage account, make sure to go through the **Create an Azure storage account** module where we go through them in depth.</span></span>

<span data-ttu-id="40682-135">部署该帐户需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="40682-135">It will take a few minutes to deploy the account.</span></span> <span data-ttu-id="40682-136">在 Azure 中工作时, 让我们来探究我们将用于此帐户的 api。</span><span class="sxs-lookup"><span data-stu-id="40682-136">While Azure is working on that, let's explore the APIs we'll use with this account.</span></span>
