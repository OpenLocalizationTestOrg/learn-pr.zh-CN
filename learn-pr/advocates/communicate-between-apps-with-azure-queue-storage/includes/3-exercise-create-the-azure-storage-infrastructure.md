<span data-ttu-id="c9036-101">你已发现流量峰值会严重影响中间层。</span><span class="sxs-lookup"><span data-stu-id="c9036-101">You've discovered that spikes in traffic can overwhelm our middle-tier.</span></span> <span data-ttu-id="c9036-102">为处理这种情况, 您已决定在您的文章上载应用程序中的前端和中间层之间添加队列。</span><span class="sxs-lookup"><span data-stu-id="c9036-102">To deal with this, you've decided to add a queue between the front-end and the middle tier in your article-upload application.</span></span>

<span data-ttu-id="c9036-103">创建队列的第一步是创建将存储数据的 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="c9036-103">The first step in creating a queue is to create the Azure Storage Account that will store our data.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a><span data-ttu-id="c9036-104">使用 Azure CLI 创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="c9036-104">Create a Storage Account with the Azure CLI</span></span>

> [!TIP] 
> <span data-ttu-id="c9036-105">通常情况下, 您应通过创建_资源组_来保存所有关联的资源来启动新项目。</span><span class="sxs-lookup"><span data-stu-id="c9036-105">Normally, you'd start a new project by creating a _resource group_ to hold all the associated resources.</span></span> <span data-ttu-id="c9036-106">在这种情况下, 我们将使用 Azure 沙盒, 它提供名为<rgn>[沙盒资源组名称]</rgn>的资源组。</span><span class="sxs-lookup"><span data-stu-id="c9036-106">In this case, we'll be using the Azure sandbox which provides a resource group named <rgn>[sandbox resource group name]</rgn>.</span></span>

<span data-ttu-id="c9036-107">使用`az storage account create`命令创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="c9036-107">Use the `az storage account create` command to create the storage account.</span></span> <span data-ttu-id="c9036-108">可以在右侧的 "云命令行管理器" 窗口中键入命令。</span><span class="sxs-lookup"><span data-stu-id="c9036-108">You can type the command into the Cloud Shell window on the right.</span></span>

<span data-ttu-id="c9036-109">该命令需要几个参数:</span><span class="sxs-lookup"><span data-stu-id="c9036-109">The command needs several parameters:</span></span>

| <span data-ttu-id="c9036-110">参数</span><span class="sxs-lookup"><span data-stu-id="c9036-110">Parameter</span></span> | <span data-ttu-id="c9036-111">值</span><span class="sxs-lookup"><span data-stu-id="c9036-111">Value</span></span> |
|-----------|-------|
| `--name`  | <span data-ttu-id="c9036-112">设置名称。</span><span class="sxs-lookup"><span data-stu-id="c9036-112">Sets the name.</span></span> <span data-ttu-id="c9036-113">请注意, 存储帐户使用名称生成公用 URL-因此它必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c9036-113">Remember that storage accounts use the name to generate a public URL - so it has to be unique.</span></span> <span data-ttu-id="c9036-114">此外, 帐户名称必须介于3到24个字符之间, 并且只能由数字和小写字母组成。</span><span class="sxs-lookup"><span data-stu-id="c9036-114">In addition, the account name must be between 3 and 24 characters, and be composed of numbers and lowercase letters only.</span></span> <span data-ttu-id="c9036-115">我们建议您将前缀**文章**与随机号码后缀结合使用, 但你可以使用你喜欢的任何内容。</span><span class="sxs-lookup"><span data-stu-id="c9036-115">We recommend you use the prefix **articles** with a random number suffix but you can use whatever you like.</span></span> |
| `-g`        | <span data-ttu-id="c9036-116">提供**资源组**, 请使用_<rgn>[沙盒资源组名称]</rgn>_ 作为值。</span><span class="sxs-lookup"><span data-stu-id="c9036-116">Supplies the **Resource Group**, use _<rgn>[sandbox resource group name]</rgn>_ as the value.</span></span> |
| `--kind`    | <span data-ttu-id="c9036-117">设置**存储帐户类型**-使用_StorageV2_创建常规用途的 V2 帐户。</span><span class="sxs-lookup"><span data-stu-id="c9036-117">Sets the **Storage Account type** - use _StorageV2_ to create a general-purpose V2 account.</span></span> |
| `--sku`     | <span data-ttu-id="c9036-118">设置**复制和存储类型**, 其默认值为_Standard_RAGRS_。</span><span class="sxs-lookup"><span data-stu-id="c9036-118">Sets the **Replication and Storage type**, it defaults to _Standard_RAGRS_.</span></span> <span data-ttu-id="c9036-119">我们使用_Standard_LRS_ , 这意味着它只是数据中心内的本地冗余。</span><span class="sxs-lookup"><span data-stu-id="c9036-119">Let's use _Standard_LRS_ which means it's only locally redundant within the data center.</span></span> |
| `-l`        | <span data-ttu-id="c9036-120">设置独立于资源组所有者的**位置**。</span><span class="sxs-lookup"><span data-stu-id="c9036-120">Sets the **Location** independent of the resource group owner.</span></span> <span data-ttu-id="c9036-121">它是可选的, 但您可以使用它将队列放置在与资源组不同的区域中。</span><span class="sxs-lookup"><span data-stu-id="c9036-121">It's optional, but you can use it to place the queue in a different region than the resource group.</span></span> <span data-ttu-id="c9036-122">将其靠近您, 在沙盒中的可用区域列表中进行选择。</span><span class="sxs-lookup"><span data-stu-id="c9036-122">Place it close to you, choosing from the below list of available regions in the sandbox.</span></span> |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="c9036-123">下面是一个使用上述参数的示例命令行。</span><span class="sxs-lookup"><span data-stu-id="c9036-123">Here's an example command line that uses the above parameters.</span></span> <span data-ttu-id="c9036-124">请务必更改`--name`参数。</span><span class="sxs-lookup"><span data-stu-id="c9036-124">Make sure to change the `--name` parameter.</span></span>

```azurecli
az storage account create --name [unique-name] -g <rgn>[sandbox resource group name]</rgn> --kind StorageV2 --sku Standard_LRS
```

<!-- Paste tip-->
[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
