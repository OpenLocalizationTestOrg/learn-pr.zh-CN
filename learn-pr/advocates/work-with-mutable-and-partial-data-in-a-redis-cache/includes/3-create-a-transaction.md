<span data-ttu-id="ea3f4-101">首先, 创建 Redis 的 Azure 缓存实例, 然后创建一个简单的事务, 将两个数据值插入到缓存中。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-101">Let's start by creating an instance of Azure Cache for Redis, and then create a simple transaction that inserts two data values into the cache.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-cache-for-redis"></a><span data-ttu-id="ea3f4-102">为 Redis 创建 Azure 缓存</span><span class="sxs-lookup"><span data-stu-id="ea3f4-102">Create an Azure Cache for Redis</span></span>

<span data-ttu-id="ea3f4-103">让我们先通过 azure CLI 为 Redis 创建 azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-103">Let's start by creating an Azure Cache for Redis with the Azure CLI.</span></span> <span data-ttu-id="ea3f4-104">使用浏览器窗口右侧的云命令行管理程序与 Azure 进行交互。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-104">Use the Cloud Shell on the right side of the browser window to interact with Azure.</span></span>

<span data-ttu-id="ea3f4-105">我们将使用`az redis create`命令为 Redis 创建新的 Azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-105">We'll use the `az redis create` command to create a new Azure Cache for Redis.</span></span> <span data-ttu-id="ea3f4-106">它需要多个参数。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-106">It takes several parameters.</span></span> <span data-ttu-id="ea3f4-107">下面列出了最常见的内容 (若要获取完整列表, 请查看文档)。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-107">Here are the most common (to get a full list, check the documentation).</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="ea3f4-108">参数</span><span class="sxs-lookup"><span data-stu-id="ea3f4-108">Parameter</span></span> | <span data-ttu-id="ea3f4-109">说明</span><span class="sxs-lookup"><span data-stu-id="ea3f4-109">Description</span></span> |
> |-----------|-------------|
> | `--name`    | <span data-ttu-id="ea3f4-110">缓存的名称-这必须全局唯一且由字母、数字和短划线组成。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-110">The name of the cache - this must be globally unique and composed of letters, numbers, and dashes.</span></span> |
> | `--resource-group` | <span data-ttu-id="ea3f4-111">使用预创建的资源组**<rgn>[沙盒资源组名称]</rgn>**, 它是 Azure 沙箱的一部分。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-111">Use the pre-created Resource Group **<rgn>[sandbox resource group name]</rgn>**, which is part of the Azure sandbox.</span></span> |
> | `--location` | <span data-ttu-id="ea3f4-112">指定缓存应位于的位置。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-112">Specify the location where the cache should be located.</span></span> <span data-ttu-id="ea3f4-113">通常情况下, 您需要选择靠近数据使用者的位置。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-113">Normally, you will want to choose a location close to the data consumers.</span></span> <span data-ttu-id="ea3f4-114">在这种情况下, 您仅限于在 Azure 沙盒中提供的位置。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-114">In this case, you are limited to the locations available in the Azure sandbox.</span></span> <span data-ttu-id="ea3f4-115">选择最接近的一个。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-115">Select the closest one to you.</span></span> |
> | `--size` | <span data-ttu-id="ea3f4-116">Redis 的 Azure 缓存大小。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-116">The size of the Azure Cache for Redis.</span></span> <span data-ttu-id="ea3f4-117">有效值为 [C0、C1、C2、C3、C4、C5、C6、P1、P2、P3、P4]。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-117">Valid values are [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4].</span></span> |
> | `--sku` | <span data-ttu-id="ea3f4-118">Redis SKU 的 Azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-118">The Azure Cache for Redis SKU.</span></span> <span data-ttu-id="ea3f4-119">有效值为 [Basic, Standard, Premium]。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-119">Valid values are [Basic, Standard, Premium].</span></span> |

### <a name="select-a-location"></a><span data-ttu-id="ea3f4-120">选择位置</span><span class="sxs-lookup"><span data-stu-id="ea3f4-120">Select a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="ea3f4-121">使用以下选项创建缓存:</span><span class="sxs-lookup"><span data-stu-id="ea3f4-121">Create a cache using the following options:</span></span>
    - <span data-ttu-id="ea3f4-122">大小: C0</span><span class="sxs-lookup"><span data-stu-id="ea3f4-122">Size: C0</span></span>
    - <span data-ttu-id="ea3f4-123">SKU: 基本</span><span class="sxs-lookup"><span data-stu-id="ea3f4-123">SKU: Basic</span></span>

1. <span data-ttu-id="ea3f4-124">下面是一个示例命令行。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-124">Here's an example command line.</span></span> <span data-ttu-id="ea3f4-125">请务必将`[name]`参数替换为唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-125">Make sure to replace the `[name]` parameter with a unique name.</span></span> <span data-ttu-id="ea3f4-126">如果需要与美国东部区域不同的区域, 可以替换该位置。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-126">You can replace the location if you want a different region than East US.</span></span>

    ```azurecli
    REDIS_NAME=[name]

    az redis create \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location eastus \
        --vm-size C0 \
        --sku Basic
    ```

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="ea3f4-127">创建 .net Core 控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="ea3f4-127">Create a .NET Core console application</span></span>

<span data-ttu-id="ea3f4-128">接下来, 创建一个 .net Core 控制台应用程序, 该应用程序将用于将数据值插入到 Redis 的 Azure 缓存中。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-128">Next, create a .NET Core console application, which will be used to insert data values into our Azure Cache for Redis.</span></span>

1. <span data-ttu-id="ea3f4-129">使用窗口右侧的集成云命令行管理程序创建新的 .net Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-129">Create a new .NET Core application using the integrated Cloud Shell on the right hand side of the window.</span></span> <span data-ttu-id="ea3f4-130">将其命名为 "RedisData"。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-130">Name it "RedisData".</span></span>

    ```bash
    cd ~
    dotnet new console --name RedisData
    ```

1. <span data-ttu-id="ea3f4-131">更改为您的应用程序创建的新目录。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-131">Change into the new directory created for your app.</span></span>

    ```bash
    cd RedisData
    ```

1. <span data-ttu-id="ea3f4-132">生成并运行应用程序-它应输出 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="ea3f4-132">Build and run the application - it should output "Hello World!"</span></span>

    ```bash
    dotnet run
    ```

## <a name="add-the-servicestackredis-nuget-package"></a><span data-ttu-id="ea3f4-133">添加 Redis NuGet 包 ServiceStack</span><span class="sxs-lookup"><span data-stu-id="ea3f4-133">Add the ServiceStack.Redis NuGet package</span></span>

<span data-ttu-id="ea3f4-134">至此, 我们已拥有控制台应用程序, 我们需要添加**ServiceStack** NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-134">Now that we have our console application, we need to add the **ServiceStack.Redis** NuGet package.</span></span> <span data-ttu-id="ea3f4-135">这将允许我们在 c # 中连接到适用于 Redis 的 Azure 缓存并发出命令。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-135">This will allow us to connect to the Azure Cache for Redis and issue commands in C#.</span></span>

1. <span data-ttu-id="ea3f4-136">使用终端命令行管理程序添加 NuGet 程序包**ServiceStack Redis** 。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-136">Add the NuGet package **ServiceStack.Redis** using the terminal shell.</span></span>

    ```bash
    dotnet add package ServiceStack.Redis
    ```

1. <span data-ttu-id="ea3f4-137">再次生成并运行应用程序以确保所有编译都能进行编译。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-137">Build and run the application again to make sure it all compiles.</span></span> <span data-ttu-id="ea3f4-138">它仍应输出 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="ea3f4-138">It should still output "Hello World!"</span></span>

## <a name="get-your-azure-cache-for-redis-connection-string"></a><span data-ttu-id="ea3f4-139">获取 Redis 连接字符串的 Azure 缓存</span><span class="sxs-lookup"><span data-stu-id="ea3f4-139">Get your Azure Cache for Redis connection string</span></span>

<span data-ttu-id="ea3f4-140">若要连接到 Redis 的 Azure 缓存, 您需要一个包含您的密码和 URL 的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-140">To connect to your Azure Cache for Redis, you need a connection string that contains your password and URL.</span></span> <span data-ttu-id="ea3f4-141">**ServiceStack**具有其自己的连接字符串格式: `[password]@[hostname]:[sslport]?ssl=true`。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-141">**ServiceStack.Redis** has its own connection string format: `[password]@[hostname]:[sslport]?ssl=true`.</span></span>

<span data-ttu-id="ea3f4-142">你可以使用 Azure 门户或命令行检索你的密码。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-142">You can retrieve your password with the Azure portal, or with the command line.</span></span> <span data-ttu-id="ea3f4-143">由于我们在 "通过将只读数据缓存到 Redis" 模块中使用了 "优化 web 应用程序" 中的门户方法, 因此我们在这里使用这一方法。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-143">Let's use the latter here, since we used the portal approach in the "Optimize your web applications by caching read-only data with Redis" module.</span></span>

<span data-ttu-id="ea3f4-144">使用`az redis list-keys`命令获取访问键。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-144">Use the `az redis list-keys` command to get the access keys.</span></span> <span data-ttu-id="ea3f4-145">运行这些命令以获取主键, 将其存储在名`REDIS_KEY`为的变量中, 并显示该主键:</span><span class="sxs-lookup"><span data-stu-id="ea3f4-145">Run these commands to get the primary key, store it in a variable called `REDIS_KEY`, and display it:</span></span>

```azurecli
REDIS_KEY=$(az redis list-keys \
    --name "$REDIS_NAME" \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query primaryKey \
    --output tsv)

echo $REDIS_KEY
```

<span data-ttu-id="ea3f4-146">接下来, 运行此命令以将连接字符串放在一起, 并在命令行中显示它。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-146">Next, run this command to put the connection string together and display it on the command line.</span></span> <span data-ttu-id="ea3f4-147">请注意, 主机名是后跟的缓存的名称`.redis.cache.windows.net`, 端口是**6380**, 是默认的 Redis SSL 端口。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-147">Note that the hostname is the name of the cache followed by `.redis.cache.windows.net`, and the port is **6380**, the default Redis SSL port.</span></span>

```bash
echo "$REDIS_KEY"@"$REDIS_NAME".redis.cache.windows.net:6380?ssl=true
```

<span data-ttu-id="ea3f4-148">将连接字符串复制到您将&mdash;在下一步中使用的剪贴板。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-148">Copy the connection string to the clipboard &mdash; you'll be using it in the next step.</span></span>

## <a name="add-the-connection-string-to-your-app"></a><span data-ttu-id="ea3f4-149">将连接字符串添加到应用程序</span><span class="sxs-lookup"><span data-stu-id="ea3f4-149">Add the connection string to your app</span></span>

1. <span data-ttu-id="ea3f4-150">从应用程序文件夹中打开云命令行管理程序编辑器。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-150">Open the Cloud Shell editor from the application folder.</span></span>

    ```bash
    cd ~/RedisData
    code .
    ```

1. <span data-ttu-id="ea3f4-151">选择 " **Program.cs** " 源文件。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-151">Select the **Program.cs** source file.</span></span>

1. <span data-ttu-id="ea3f4-152">在`Program`类中创建以下字段, 并将连接字符串粘贴为值。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-152">Create the following field in the `Program` class and paste in your connection string as the value.</span></span>

    ```csharp
    static string redisConnectionString = "<connection string>";
    ```

    <span data-ttu-id="ea3f4-153">下面是一个示例:</span><span class="sxs-lookup"><span data-stu-id="ea3f4-153">Here's an example:</span></span>

    ```csharp
    static string redisConnectionString = "ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6380?ssl=true";
    ```

## <a name="insert-two-data-values-into-your-azure-cache-for-redis"></a><span data-ttu-id="ea3f4-154">将两个数据值插入到 Redis 的 Azure 缓存中</span><span class="sxs-lookup"><span data-stu-id="ea3f4-154">Insert two data values into your Azure Cache for Redis</span></span>

<span data-ttu-id="ea3f4-155">最后, 我们要将数据添加到 Redis 的 Azure 缓存中。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-155">Finally, we're going to add data into your Azure Cache for Redis.</span></span>

1. <span data-ttu-id="ea3f4-156">将以下`using`语句添加到**Program.cs**文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-156">Add the following `using` statement to the top of the **Program.cs** file.</span></span>

    ```csharp
    using ServiceStack.Redis;
    ```

1. <span data-ttu-id="ea3f4-157">将`Main`方法的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-157">Replace the contents of the `Main` method with the following code.</span></span> <span data-ttu-id="ea3f4-158">这将使用事务来添加两个值。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-158">This will use a transaction to add two values.</span></span>

    ```csharp
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    if (transactionResult)
    {
        Console.WriteLine("Transaction committed");
    }
    else
    {
        Console.WriteLine("Transaction failed to commit");
    }
    ```

1. <span data-ttu-id="ea3f4-159">在生成和运行应用程序之前, 请进行检查以确保已完全预配 Redis 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-159">Before building and running the application, check to make sure that the Redis cache has been fully provisioned.</span></span> <span data-ttu-id="ea3f4-160">在完成后`az redis create` , 有时可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-160">It can sometimes take a few minutes after `az redis create` completes.</span></span> <span data-ttu-id="ea3f4-161">运行以下命令以检查状态。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-161">Run the following command to check the status.</span></span>

    ```azurecli
    az redis show \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --query provisioningState
    ```

    <span data-ttu-id="ea3f4-162">如果状态为`Creating`, 请尝试在几分钟内再次检查。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-162">If the status is `Creating`, try checking again in a couple of minutes.</span></span> <span data-ttu-id="ea3f4-163">完成后, `Succeeded`它将显示。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-163">It will show `Succeeded` when finished.</span></span>

1. <span data-ttu-id="ea3f4-164">运行应用程序, 并验证控制台是否显示**事务已提交**。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-164">Run the application and verify that the console says **Transaction committed**.</span></span>

    ```bash
    dotnet run
    ```

## <a name="verify-your-data"></a><span data-ttu-id="ea3f4-165">验证数据</span><span class="sxs-lookup"><span data-stu-id="ea3f4-165">Verify your data</span></span>

<span data-ttu-id="ea3f4-166">若要结束, 我们将验证我们添加的数据是否在 Redis 的 Azure 缓存中。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-166">To finish off, let's verify that the data we added is in our Azure Cache for Redis.</span></span>

1. <span data-ttu-id="ea3f4-167">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-167">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="ea3f4-168">通过选择左侧侧栏中的 "**所有资源**", 然后使用左侧的 "筛选器" 框为 Redis 实例选择 azure 缓存, 找到 Redis 的 azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-168">Locate your Azure Cache for Redis by selecting **All Resources** in the left-hand sidebar, and using the filter box on the left to select Azure Cache for Redis instances.</span></span> <span data-ttu-id="ea3f4-169">或者, 也可以使用顶部的搜索框, 并键入缓存的名称。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-169">Alternatively, you can use the search box at the top, and type the name of the cache.</span></span>

1. <span data-ttu-id="ea3f4-170">为 Redis 实例选择 Azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-170">Select your Azure Cache for Redis instance.</span></span>

1. <span data-ttu-id="ea3f4-171">在用于 Redis 的 Azure 缓存的**概述**刀片中, 选择 "**控制台**"。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-171">In the **Overview** blade for your Azure Cache for Redis, select **Console**.</span></span> <span data-ttu-id="ea3f4-172">这将打开 Redis 控制台的 Azure 缓存, 使您可以为 Redis 命令输入低级别 Azure 缓存。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-172">This will open an Azure Cache for Redis console, which allows you to enter low-level Azure Cache for Redis commands.</span></span>

1. <span data-ttu-id="ea3f4-173">运行命令`get MyKey1`。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-173">Run the command `get MyKey1`.</span></span> <span data-ttu-id="ea3f4-174">验证返回的值是否为**MyValue1**。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-174">Verify that the value returned is **MyValue1**.</span></span>

1. <span data-ttu-id="ea3f4-175">运行命令`get MyKey2`。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-175">Run the command `get MyKey2`.</span></span> <span data-ttu-id="ea3f4-176">验证返回的值是否为**MyValue2**。</span><span class="sxs-lookup"><span data-stu-id="ea3f4-176">Verify that the value returned is **MyValue2**.</span></span>

    ![Redis 控制台的 Azure 缓存的屏幕截图, 显示 MyKey1 和 MyKey2 的值。](../media/4-redis-console.png)