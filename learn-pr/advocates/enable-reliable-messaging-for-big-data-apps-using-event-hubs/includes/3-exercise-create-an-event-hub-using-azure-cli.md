<span data-ttu-id="cc58d-101">您现在可以创建新的事件中心了。</span><span class="sxs-lookup"><span data-stu-id="cc58d-101">You're now ready to create a new Event Hub.</span></span> <span data-ttu-id="cc58d-102">创建事件中心后, 你将使用 Azure 门户查看你的新中心。</span><span class="sxs-lookup"><span data-stu-id="cc58d-102">After creating the Event Hub, you'll use the Azure portal to view your new hub.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-some-defaults-in-the-azure-cli"></a><span data-ttu-id="cc58d-103">在 Azure CLI 中设置一些默认值</span><span class="sxs-lookup"><span data-stu-id="cc58d-103">Set some defaults in the Azure CLI</span></span>

<span data-ttu-id="cc58d-104">首先, 我们在云命令行管理程序中为 Azure CLI 提供一些默认值。</span><span class="sxs-lookup"><span data-stu-id="cc58d-104">Let's start by providing some default values for the Azure CLI in the Cloud Shell.</span></span> <span data-ttu-id="cc58d-105">这将使您无需每次都键入这些项。</span><span class="sxs-lookup"><span data-stu-id="cc58d-105">This will keep you from having to type these in every time.</span></span> <span data-ttu-id="cc58d-106">尤其是, 让我们设置_资源组_和_位置_。</span><span class="sxs-lookup"><span data-stu-id="cc58d-106">In particular, let's set the _resource group_ and _location_.</span></span> <span data-ttu-id="cc58d-107">从以下列表中选择一个位置。</span><span class="sxs-lookup"><span data-stu-id="cc58d-107">Select a location from the following list.</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="cc58d-108">然后, 在 Azure CLI 中键入以下命令, 确保用一个接近你的位置替换该位置。</span><span class="sxs-lookup"><span data-stu-id="cc58d-108">Then type the following command into the Azure CLI, make sure to replace the location with one close to you.</span></span>

```azurecli
az configure --defaults group=<rgn>[sandbox Resource Group]</rgn> location=westus2
```

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="cc58d-109">创建事件中心命名空间</span><span class="sxs-lookup"><span data-stu-id="cc58d-109">Create an Event Hubs namespace</span></span>

<span data-ttu-id="cc58d-110">使用以下步骤, 通过 Azure 云命令行管理程序支持的 bash 命令行管理程序来创建事件中心命名空间:</span><span class="sxs-lookup"><span data-stu-id="cc58d-110">Use the following steps to create an Event Hubs namespace using bash shell supported by Azure Cloud shell:</span></span>

1. <span data-ttu-id="cc58d-111">使用`az eventhubs namespace create`命令创建事件中心命名空间。</span><span class="sxs-lookup"><span data-stu-id="cc58d-111">Create the Event Hubs namespace using the `az eventhubs namespace create` command.</span></span> <span data-ttu-id="cc58d-112">使用以下参数。</span><span class="sxs-lookup"><span data-stu-id="cc58d-112">Use the following parameters.</span></span>

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="cc58d-113">参数</span><span class="sxs-lookup"><span data-stu-id="cc58d-113">Parameter</span></span>      |<span data-ttu-id="cc58d-114">说明</span><span class="sxs-lookup"><span data-stu-id="cc58d-114">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="cc58d-115">--名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-115">--name (required)</span></span>      |<span data-ttu-id="cc58d-116">为事件中心命名空间输入6-50 个字符的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="cc58d-116">Enter a 6-50 characters-long unique name for your Event Hubs namespace.</span></span> <span data-ttu-id="cc58d-117">名称应仅包含字母、数字和连字符。</span><span class="sxs-lookup"><span data-stu-id="cc58d-117">The name should contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="cc58d-118">它应以字母开头, 以字母或数字结尾。</span><span class="sxs-lookup"><span data-stu-id="cc58d-118">It should start with a letter and end with a letter or number.</span></span>|
    > |<span data-ttu-id="cc58d-119">--资源-组 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-119">--resource-group (required)</span></span> | <span data-ttu-id="cc58d-120">这将是由默认值提供的预创建的 Azure 沙盒资源组。</span><span class="sxs-lookup"><span data-stu-id="cc58d-120">This will be the pre-created Azure sandbox resource group supplied from the defaults.</span></span> |
    > |<span data-ttu-id="cc58d-121">--l (可选)</span><span class="sxs-lookup"><span data-stu-id="cc58d-121">--l (optional)</span></span>     |<span data-ttu-id="cc58d-122">输入你最近的 Azure 数据中心的位置, 这将使用你的默认位置。</span><span class="sxs-lookup"><span data-stu-id="cc58d-122">Enter the location of your nearest Azure datacenter, this will use your default.</span></span>|
    > |<span data-ttu-id="cc58d-123">--sku (可选)</span><span class="sxs-lookup"><span data-stu-id="cc58d-123">--sku (optional)</span></span> | <span data-ttu-id="cc58d-124">命名空间的定价层 [Basic</span><span class="sxs-lookup"><span data-stu-id="cc58d-124">The pricing tier for the namespace [Basic</span></span> | <span data-ttu-id="cc58d-125">standard], 默认值为_Standard_。</span><span class="sxs-lookup"><span data-stu-id="cc58d-125">Standard], defaults to _Standard_.</span></span> <span data-ttu-id="cc58d-126">这将确定连接和消费者阈值。</span><span class="sxs-lookup"><span data-stu-id="cc58d-126">This determines the connections and consumer thresholds.</span></span> |

    <span data-ttu-id="cc58d-127">将名称设置为环境变量, 以便我们可以重复使用它。</span><span class="sxs-lookup"><span data-stu-id="cc58d-127">Set the name into an environment variable so we can reuse it.</span></span>

    ```azurecli
    NS_NAME=myEvt-HubNs1
    ````

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```azurecli
    az eventhubs namespace create --name $NS_NAME
    ```

    > [!NOTE]
    > <span data-ttu-id="cc58d-128">Azure 非常高有关名称的信息, 如果名称存在或无效, CLI 将返回**错误的请求**。</span><span class="sxs-lookup"><span data-stu-id="cc58d-128">Azure is very picky about the name and the CLI returns **Bad Request** if the name exists or is invalid.</span></span> <span data-ttu-id="cc58d-129">通过更改环境变量并重新发起命令来尝试其他名称。</span><span class="sxs-lookup"><span data-stu-id="cc58d-129">Try a different name by changing your environment variable and reissuing the command.</span></span>


1. <span data-ttu-id="cc58d-130">使用以下命令提取事件中心命名空间的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="cc58d-130">Fetch the connection string for your Event Hubs namespace using the following command.</span></span> <span data-ttu-id="cc58d-131">你将需要此信息来配置应用程序, 以使用事件中心发送和接收邮件。</span><span class="sxs-lookup"><span data-stu-id="cc58d-131">You'll need this to configure applications to send and receive messages using your Event Hub.</span></span>

    ```azurecli
    az eventhubs namespace authorization-rule keys list --name RootManageSharedAccessKey --namespace-name $NS_NAME
    ```

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="cc58d-132">参数</span><span class="sxs-lookup"><span data-stu-id="cc58d-132">Parameter</span></span>      |<span data-ttu-id="cc58d-133">说明</span><span class="sxs-lookup"><span data-stu-id="cc58d-133">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="cc58d-134">--资源-组 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-134">--resource-group (required)</span></span>  | <span data-ttu-id="cc58d-135">这将是由默认值提供的预创建的 Azure 沙盒资源组。</span><span class="sxs-lookup"><span data-stu-id="cc58d-135">This will be the pre-created Azure sandbox resource group supplied from the defaults.</span></span> |
    > |<span data-ttu-id="cc58d-136">--命名空间名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-136">--namespace-name (required)</span></span>  | <span data-ttu-id="cc58d-137">输入您创建的命名空间的名称。</span><span class="sxs-lookup"><span data-stu-id="cc58d-137">Enter the name of the namespace you created.</span></span> |

    <span data-ttu-id="cc58d-138">此命令返回一个包含事件中心命名空间的连接字符串的 JSON 块, 稍后将使用该块配置发布者和使用者应用程序。</span><span class="sxs-lookup"><span data-stu-id="cc58d-138">This command returns a JSON block with the connection string for your Event Hubs namespace that you'll use later to configure your publisher and consumer applications.</span></span> <span data-ttu-id="cc58d-139">保存以下项的值以供将来使用。</span><span class="sxs-lookup"><span data-stu-id="cc58d-139">Save the value of the following keys for later use.</span></span>

    - <span data-ttu-id="cc58d-140">**primaryConnectionString**</span><span class="sxs-lookup"><span data-stu-id="cc58d-140">**primaryConnectionString**</span></span>
    - <span data-ttu-id="cc58d-141">**关键字**</span><span class="sxs-lookup"><span data-stu-id="cc58d-141">**primaryKey**</span></span>

## <a name="create-an-event-hub"></a><span data-ttu-id="cc58d-142">创建事件中心</span><span class="sxs-lookup"><span data-stu-id="cc58d-142">Create an Event Hub</span></span>

<span data-ttu-id="cc58d-143">使用以下步骤创建新的事件中心:</span><span class="sxs-lookup"><span data-stu-id="cc58d-143">Use the following steps to create your new Event Hub:</span></span>

1. <span data-ttu-id="cc58d-144">使用`eventhub create`命令创建新的事件中心。</span><span class="sxs-lookup"><span data-stu-id="cc58d-144">Create a new Event Hub using the `eventhub create` command.</span></span> <span data-ttu-id="cc58d-145">它需要以下参数:</span><span class="sxs-lookup"><span data-stu-id="cc58d-145">It needs the following parameters:</span></span>

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="cc58d-146">参数</span><span class="sxs-lookup"><span data-stu-id="cc58d-146">Parameter</span></span>      |<span data-ttu-id="cc58d-147">说明</span><span class="sxs-lookup"><span data-stu-id="cc58d-147">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="cc58d-148">--名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-148">--name (required)</span></span>  |<span data-ttu-id="cc58d-149">为事件中心输入名称。</span><span class="sxs-lookup"><span data-stu-id="cc58d-149">Enter a name for your Event Hub.</span></span>|
    > |<span data-ttu-id="cc58d-150">--资源-组 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-150">--resource-group (required)</span></span>  |<span data-ttu-id="cc58d-151">资源组所有者。</span><span class="sxs-lookup"><span data-stu-id="cc58d-151">Resource group owner.</span></span>|
    > |<span data-ttu-id="cc58d-152">--命名空间名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-152">--namespace-name (required)</span></span>      |<span data-ttu-id="cc58d-153">输入您创建的命名空间。</span><span class="sxs-lookup"><span data-stu-id="cc58d-153">Enter the namespace you created.</span></span>|

    <span data-ttu-id="cc58d-154">让我们先在环境变量中定义事件中心名称。</span><span class="sxs-lookup"><span data-stu-id="cc58d-154">Let's define the Event Hub name in an environment variable first.</span></span>

    ```azurecli
    HUB_NAME=[name]
    ```

    ```azurecli
    az eventhubs eventhub create --name $HUB_NAME --namespace-name $NS_NAME
    ```

1. <span data-ttu-id="cc58d-155">使用`eventhub show`命令查看事件中心的详细信息。</span><span class="sxs-lookup"><span data-stu-id="cc58d-155">View the details of your Event Hub using the `eventhub show` command.</span></span> <span data-ttu-id="cc58d-156">它采用了:</span><span class="sxs-lookup"><span data-stu-id="cc58d-156">It takes:</span></span>

    > [!div class="mx-tableFixed"]
    > |<span data-ttu-id="cc58d-157">参数</span><span class="sxs-lookup"><span data-stu-id="cc58d-157">Parameter</span></span>      |<span data-ttu-id="cc58d-158">说明</span><span class="sxs-lookup"><span data-stu-id="cc58d-158">Description</span></span>|
    > |---------------|-----------|
    > |<span data-ttu-id="cc58d-159">--资源-组 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-159">--resource-group (required)</span></span>  |<span data-ttu-id="cc58d-160">资源组所有者。</span><span class="sxs-lookup"><span data-stu-id="cc58d-160">Resource group owner.</span></span>|
    > |<span data-ttu-id="cc58d-161">--命名空间名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-161">--namespace-name (required)</span></span>      |<span data-ttu-id="cc58d-162">输入您创建的命名空间。</span><span class="sxs-lookup"><span data-stu-id="cc58d-162">Enter the namespace you created.</span></span>|
    > |<span data-ttu-id="cc58d-163">--名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="cc58d-163">--name  (required)</span></span>|<span data-ttu-id="cc58d-164">事件中心的名称。</span><span class="sxs-lookup"><span data-stu-id="cc58d-164">Name of the Event Hub.</span></span>|

    ```azurecli
    az eventhubs eventhub show --namespace-name $NS_NAME --name $HUB_NAME
    ```

## <a name="view-the-event-hub-in-the-azure-portal"></a><span data-ttu-id="cc58d-165">在 Azure 门户中查看事件中心</span><span class="sxs-lookup"><span data-stu-id="cc58d-165">View the Event Hub in the Azure portal</span></span>

<span data-ttu-id="cc58d-166">接下来, 我们来看看它在 Azure 门户中的显示效果。</span><span class="sxs-lookup"><span data-stu-id="cc58d-166">Next, let's see what this looks like in the Azure portal.</span></span>

1. <span data-ttu-id="cc58d-167">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="cc58d-167">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="cc58d-168">使用门户顶部的搜索栏查找事件中心命名空间。</span><span class="sxs-lookup"><span data-stu-id="cc58d-168">Find your Event Hubs namespace using the Search bar at the top of portal.</span></span>

1. <span data-ttu-id="cc58d-169">选择您的命名空间将其打开。</span><span class="sxs-lookup"><span data-stu-id="cc58d-169">Select your namespace to open it.</span></span>

1. <span data-ttu-id="cc58d-170">在 "**实体**" 部分下选择 "**事件中心命名空间**"。</span><span class="sxs-lookup"><span data-stu-id="cc58d-170">Select **Event Hubs namespace** under the **ENTITIES** section.</span></span>

1. <span data-ttu-id="cc58d-171">单击 "**事件中心**"。</span><span class="sxs-lookup"><span data-stu-id="cc58d-171">Click **Event Hubs**.</span></span>

    <span data-ttu-id="cc58d-172">事件中心显示状态为 "**活动**", "**邮件保留**" 的默认值为 "(*7*)" 和 "**分区计数**为 (*4*)"。</span><span class="sxs-lookup"><span data-stu-id="cc58d-172">Your Event Hub displays with a status of **Active**, and default values for **Message Retention** (*7*) and **Partition Count** of (*4*).</span></span>

    ![Azure 门户中显示的事件中心](../media/3-event-hub.png)

## <a name="summary"></a><span data-ttu-id="cc58d-174">摘要</span><span class="sxs-lookup"><span data-stu-id="cc58d-174">Summary</span></span>

<span data-ttu-id="cc58d-175">现在, 您已经创建了一个新的事件中心, 并且您已准备好配置发布者和使用者应用程序所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="cc58d-175">You've now created a new Event Hub, and you've all the necessary information ready to configure your publisher and consumer applications.</span></span>
