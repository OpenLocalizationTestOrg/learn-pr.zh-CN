<span data-ttu-id="f7e33-101">让我们创建一个用于 Redis 实例的 Azure 缓存, 以存储和返回常用的值。</span><span class="sxs-lookup"><span data-stu-id="f7e33-101">Let's create an Azure Cache for Redis instance to store and return commonly used values.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-redis-cache-in-azure"></a><span data-ttu-id="f7e33-102">在 Azure 中创建 Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="f7e33-102">Create a Redis cache in Azure</span></span>

1. <span data-ttu-id="f7e33-103">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="f7e33-103">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="f7e33-104">单击 "**创建资源**", 单击 "**数据库**", 然后单击 " **Redis Cache**"。</span><span class="sxs-lookup"><span data-stu-id="f7e33-104">Click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="f7e33-105">下面的屏幕截图显示了 Azure 门户上各种数据库资源选项中的 Redis 缓存位置。</span><span class="sxs-lookup"><span data-stu-id="f7e33-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![显示 Azure 门户数据库选项的屏幕截图, 其中突出显示了创建资源、数据库和 Redis 缓存选项。](../media/4-create-a-cache-1.png)

### <a name="configure-your-cache"></a><span data-ttu-id="f7e33-107">配置缓存</span><span class="sxs-lookup"><span data-stu-id="f7e33-107">Configure your cache</span></span>

<span data-ttu-id="f7e33-108">在缓存上应用以下设置。</span><span class="sxs-lookup"><span data-stu-id="f7e33-108">Apply the following settings on the cache.</span></span>

1. <span data-ttu-id="f7e33-109">**DNS 名称:** 创建一个全局唯一名称, 例如**ContosoSportsApp [nnn]**, 其中`[nnn]`的 where 将替换为随机数字。</span><span class="sxs-lookup"><span data-stu-id="f7e33-109">**DNS Name:** Create a globally unique name such as **ContosoSportsApp[nnn]**, where `[nnn]` is replaced with random numbers.</span></span>

1. <span data-ttu-id="f7e33-110">**订阅:** 选择 "Concierge" 订阅。</span><span class="sxs-lookup"><span data-stu-id="f7e33-110">**Subscription:** Select the Concierge subscription.</span></span>

1. <span data-ttu-id="f7e33-111">**资源组:** 为资源组选择 " <rgn>[沙盒资源组名称]</rgn> "。</span><span class="sxs-lookup"><span data-stu-id="f7e33-111">**Resource group:** Select <rgn>[sandbox resource group name]</rgn> for the Resource Group.</span></span>

1. <span data-ttu-id="f7e33-112">**位置:** 通常情况下, 应选择靠近您的客户的位置-在此示例中, 这种情况下为东海岸。</span><span class="sxs-lookup"><span data-stu-id="f7e33-112">**Location:** Normally, you would select a location near your customers - in this case, the East Coast.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]

5. <span data-ttu-id="f7e33-113">**定价层:** 选择 "**基本 c0**"。</span><span class="sxs-lookup"><span data-stu-id="f7e33-113">**Pricing tier:** Select **Basic C0**.</span></span> <span data-ttu-id="f7e33-114">这是您可以使用的最低层。</span><span class="sxs-lookup"><span data-stu-id="f7e33-114">This is the lowest tier you can use.</span></span> <span data-ttu-id="f7e33-115">生产应用程序可能需要存储更多数据, 并利用一些高级功能 (如群集), 这将需要更高的层次选择。</span><span class="sxs-lookup"><span data-stu-id="f7e33-115">Production apps would likely want to store more data and utilize some of the Premium features such as clustering which would require a higher tier selection.</span></span>

1. <span data-ttu-id="f7e33-116">单击"创建"。</span><span class="sxs-lookup"><span data-stu-id="f7e33-116">Click **Create**.</span></span> <span data-ttu-id="f7e33-117">Azure 将为您创建和部署 Redis 缓存实例。</span><span class="sxs-lookup"><span data-stu-id="f7e33-117">Azure will create and deploy the Redis Cache instance for you.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f7e33-118">通常情况下, Redis 缓存资源将在 Azure 门户中快速创建并查看, 但缓存本身在几分钟内将不可用。</span><span class="sxs-lookup"><span data-stu-id="f7e33-118">Usually, the Redis cache resource will be created and viewable in the Azure portal very quickly, but the cache itself will not be available for a few minutes.</span></span> <span data-ttu-id="f7e33-119">接下来的步骤演示如何检查缓存的状态。</span><span class="sxs-lookup"><span data-stu-id="f7e33-119">The next steps show how to check the status of your cache.</span></span>

## <a name="verify-your-data"></a><span data-ttu-id="f7e33-120">验证数据</span><span class="sxs-lookup"><span data-stu-id="f7e33-120">Verify your data</span></span>

<span data-ttu-id="f7e33-121">您可以使用 Azure 门户中的**控制台**功能, 在创建 Redis 缓存实例后向其发出命令。</span><span class="sxs-lookup"><span data-stu-id="f7e33-121">You can use the **Console** feature in the Azure portal to issue commands to your Redis cache instance after it has been created.</span></span>

1. <span data-ttu-id="f7e33-122">完成部署后, 通过**通知**弹出窗口找到 Redis 缓存, 或者通过选择左侧\*\*\*\* 边栏中的 "筛选器" 框并使用左侧的 "筛选器" 框选择 Redis 缓存实例。</span><span class="sxs-lookup"><span data-stu-id="f7e33-122">Locate your Redis cache through the **Notification** popup when it finishes deployment, or by selecting **All Resources** in the left-hand sidebar and using the filter box on the left to select Redis Cache instances.</span></span> <span data-ttu-id="f7e33-123">或者, 也可以使用顶部的搜索框并键入缓存的名称。</span><span class="sxs-lookup"><span data-stu-id="f7e33-123">Alternatively, you can use the search box at the top and type the name of the cache.</span></span>

1. <span data-ttu-id="f7e33-124">选择您的 Redis 缓存实例。</span><span class="sxs-lookup"><span data-stu-id="f7e33-124">Select your Redis cache instance.</span></span>

1. <span data-ttu-id="f7e33-125">检查 "状态" 字段的值。</span><span class="sxs-lookup"><span data-stu-id="f7e33-125">Check the value of the "Status" field.</span></span> <span data-ttu-id="f7e33-126">在状态为 "正在运行" 之前, 缓存未准备就绪。</span><span class="sxs-lookup"><span data-stu-id="f7e33-126">The cache is not ready until the status is "Running".</span></span> <span data-ttu-id="f7e33-127">您可能需要等待几分钟, 然后才能继续。</span><span class="sxs-lookup"><span data-stu-id="f7e33-127">You might have to wait for a few minutes before proceeding.</span></span>

1. <span data-ttu-id="f7e33-128">在缓存运行后, 单击**概述**边栏`>_ Console`上的工具栏上的 Redis 缓存中的按钮。</span><span class="sxs-lookup"><span data-stu-id="f7e33-128">Once the cache is running, Click the `>_ Console` button in the toolbar on the **Overview** blade for your Redis Cache.</span></span> <span data-ttu-id="f7e33-129">这将打开一个 Redis 控制台, 使您可以输入低级 Redis 命令。</span><span class="sxs-lookup"><span data-stu-id="f7e33-129">This will open a Redis console, which allows you to enter low-level Redis commands.</span></span> <span data-ttu-id="f7e33-130">请尝试以下部分:</span><span class="sxs-lookup"><span data-stu-id="f7e33-130">Try some of the following:</span></span>

    ```console
    ping
    ```

    ```output
    PONG
    ```

    ```console
    set test one
    ```

    ```output
    OK
    ```

    ```console
    get test
    ```

    ```output
    "one"
    ```

<span data-ttu-id="f7e33-131">通过顶部的痕迹导航栏切换回**概述**面板, 或使用滚动条将视图向后滑回到左侧。</span><span class="sxs-lookup"><span data-stu-id="f7e33-131">Switch back to the **Overview** panel either through the breadcrumb bar on the top, or use the scrollbar to slide the view back to the left.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="f7e33-132">检索访问键和主机名</span><span class="sxs-lookup"><span data-stu-id="f7e33-132">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="f7e33-133">选择 "**设置** > **访问密钥**"。</span><span class="sxs-lookup"><span data-stu-id="f7e33-133">Select **Settings** > **Access keys**.</span></span>

1. <span data-ttu-id="f7e33-134">将**主连接字符串 (StackExchange)** 复制到安全位置, 在下一个练习中将需要它。</span><span class="sxs-lookup"><span data-stu-id="f7e33-134">Copy the **Primary connection string (StackExchange.Redis)** to a safe place, you will need it for the next exercise.</span></span>

    <span data-ttu-id="f7e33-135">此项将主键和主机名包含在完整的连接字符串中, 以供在要使用的**StackExchange**程序包的应用程序设置中使用。</span><span class="sxs-lookup"><span data-stu-id="f7e33-135">This key includes your primary key and host name in a complete connection string for use within your application settings for the **StackExchange.Redis** package we are going to use.</span></span>

<span data-ttu-id="f7e33-136">接下来, 我们来了解一些可用于询问缓存的命令。</span><span class="sxs-lookup"><span data-stu-id="f7e33-136">Next, let's learn about some of the commands we can use to interrogate the cache.</span></span>