<span data-ttu-id="e6a9d-101">访问和处理数据是许多软件解决方案中的关键任务。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-101">Accessing and processing data are key tasks in many software solutions.</span></span> <span data-ttu-id="e6a9d-102">请考虑以下几种情况:</span><span class="sxs-lookup"><span data-stu-id="e6a9d-102">Consider some of these scenarios:</span></span>

* <span data-ttu-id="e6a9d-103">您已要求实现将传入数据从 Blob 存储移动到 Azure Cosmos DB 的方法。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-103">You've been asked to implement a way to move incoming data from Blob storage to Azure Cosmos DB.</span></span>
* <span data-ttu-id="e6a9d-104">您想要将传入的邮件发送到队列以供企业中的其他组件进行处理。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-104">You want to post incoming messages to a queue for processing by another component in your enterprise.</span></span>
* <span data-ttu-id="e6a9d-105">您的服务需要从队列中获取游戏者得分并更新联机记分板。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-105">Your service needs to grab gamer scores from a queue and update an online scoreboard.</span></span>

<span data-ttu-id="e6a9d-106">所有这些示例都是关于移动数据的。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-106">All of these examples are about moving data.</span></span> <span data-ttu-id="e6a9d-107">数据源和目标与方案的不同之处, 但模式类似。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-107">The data source and destinations differ from scenario to scenario, but the pattern is similar.</span></span> <span data-ttu-id="e6a9d-108">连接到数据源, 并读取和写入数据。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-108">You connect to a data source, and you read and write data.</span></span> <span data-ttu-id="e6a9d-109">Azure 函数可帮助您使用绑定与数据和服务集成。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-109">Azure Functions helps you integrate with data and services by using bindings.</span></span> 

## <a name="what-is-a-binding"></a><span data-ttu-id="e6a9d-110">绑定是什么？</span><span class="sxs-lookup"><span data-stu-id="e6a9d-110">What is a binding?</span></span>

<span data-ttu-id="e6a9d-111">在 Azure 函数中, 绑定提供了从代码中连接到数据的声明性方式。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-111">In Azure Functions, bindings provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="e6a9d-112">它们使在函数中一致地与数据流相集成变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-112">They make it easier to integrate with data streams consistently in a function.</span></span> <span data-ttu-id="e6a9d-113">可以有多个绑定提供对不同数据元素的访问。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-113">You can have multiple bindings providing access to different data elements.</span></span> <span data-ttu-id="e6a9d-114">此功能非常强大, 因为您可以连接到数据源, 而无需对特定连接逻辑 (如数据库连接或 web API 接口) 进行编码。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-114">This is powerful because you can connect to your data sources without having to code specific connection logic (like database connections or web API interfaces).</span></span>

### <a name="types-of-bindings"></a><span data-ttu-id="e6a9d-115">绑定类型</span><span class="sxs-lookup"><span data-stu-id="e6a9d-115">Types of bindings</span></span>

<span data-ttu-id="e6a9d-116">有两种类型的绑定可用于函数:</span><span class="sxs-lookup"><span data-stu-id="e6a9d-116">There are two kinds of bindings you can use with functions:</span></span>

1. <span data-ttu-id="e6a9d-117">**输入绑定**输入绑定是与数据**源**的连接。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-117">**Input binding** An input binding is a connection to a data **source**.</span></span> <span data-ttu-id="e6a9d-118">我们的函数可以从这些输入中读取数据。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-118">Our function can read data from these inputs.</span></span>

1. <span data-ttu-id="e6a9d-119">**输出绑定**输出绑定是与数据**目标**的连接。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-119">**Output binding** An output binding is a connection to a data **destination**.</span></span> <span data-ttu-id="e6a9d-120">我们的函数可以将数据写入这些目标。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-120">Our function can write data to these destinations.</span></span>

<span data-ttu-id="e6a9d-121">此外, 还有一些触发器。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-121">There are also triggers.</span></span> <span data-ttu-id="e6a9d-122">触发器是导致函数执行的特殊类型的输入绑定。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-122">Triggers are special types of input bindings that cause a function to execute.</span></span> <span data-ttu-id="e6a9d-123">例如, 可以将 Azure 事件网格通知配置为触发器。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-123">For example, an Azure Event Grid notification can be configured as a trigger.</span></span> <span data-ttu-id="e6a9d-124">事件发生时, 函数将运行。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-124">When an event occurs, the function will run.</span></span>

### <a name="types-of-supported-bindings"></a><span data-ttu-id="e6a9d-125">支持的绑定类型</span><span class="sxs-lookup"><span data-stu-id="e6a9d-125">Types of supported bindings</span></span>

<span data-ttu-id="e6a9d-126">绑定的*类型*定义了我们在读取或发送数据的位置。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-126">The *type* of binding defines where we are reading or sending data.</span></span> <span data-ttu-id="e6a9d-127">有一个绑定可响应 web 请求, 并有大量的绑定可直接与各种 Azure 服务和第三方服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-127">There is a binding to respond to web requests and a large selection of bindings to interact directly with various Azure services as well as third-party services.</span></span>

<span data-ttu-id="e6a9d-128">绑定类型可用作输入、输出或同时用作这两者。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-128">A binding type can be used as an input, an output or both.</span></span> <span data-ttu-id="e6a9d-129">例如, 函数可以写入 Azure Blob 存储输出绑定, 但 Blob 存储更新可能会触发另一个函数。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-129">For example, a function can write to Azure Blob Storage output binding, but a blob storage update could trigger another function.</span></span>

<span data-ttu-id="e6a9d-130">下面列出了一些常见的绑定类型:</span><span class="sxs-lookup"><span data-stu-id="e6a9d-130">Some common binding types are listed below:</span></span>
- <span data-ttu-id="e6a9d-131">Blob 存储</span><span class="sxs-lookup"><span data-stu-id="e6a9d-131">Blob Storage</span></span>
- <span data-ttu-id="e6a9d-132">Azure 服务总线队列</span><span class="sxs-lookup"><span data-stu-id="e6a9d-132">Azure Service Bus Queues</span></span>
- <span data-ttu-id="e6a9d-133">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e6a9d-133">Azure Cosmos DB</span></span>
- <span data-ttu-id="e6a9d-134">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="e6a9d-134">Azure Event Hubs</span></span>
- <span data-ttu-id="e6a9d-135">外部文件</span><span class="sxs-lookup"><span data-stu-id="e6a9d-135">External Files</span></span>
- <span data-ttu-id="e6a9d-136">外部表</span><span class="sxs-lookup"><span data-stu-id="e6a9d-136">External Tables</span></span>
- <span data-ttu-id="e6a9d-137">HTTP 终结点</span><span class="sxs-lookup"><span data-stu-id="e6a9d-137">HTTP endpoints</span></span>

<span data-ttu-id="e6a9d-138">这些类型只是一个示例。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-138">These types are just a sample.</span></span> <span data-ttu-id="e6a9d-139">还有更多的 plus 函数具有可扩展性模型以添加更多绑定。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-139">There are more, plus functions have an extensibility model to add more bindings.</span></span>

### <a name="binding-properties"></a><span data-ttu-id="e6a9d-140">绑定属性</span><span class="sxs-lookup"><span data-stu-id="e6a9d-140">Binding properties</span></span>

<span data-ttu-id="e6a9d-141">所有绑定中都需要三个属性。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-141">Three properties are required in all bindings.</span></span> <span data-ttu-id="e6a9d-142">您可能需要根据要使用的绑定和存储的类型提供其他属性。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-142">You may have to supply additional properties based on the type of binding and storage you are using.</span></span>

1. <span data-ttu-id="e6a9d-143">**名称**定义用于访问数据的函数参数。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-143">**Name** Defines the function parameter through which you access the data.</span></span> <span data-ttu-id="e6a9d-144">例如, 在队列输入绑定中, 这是接收队列消息内容的函数参数的名称。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-144">For example, in a queue input binding, this is the name of the function parameter that receives the queue message content.</span></span> 

1. <span data-ttu-id="e6a9d-145">**类型**标识绑定的类型, 即要与之交互的数据或服务的类型。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-145">**Type** Identifies the type of binding, i.e., the type of data or service we want to interact with.</span></span>

1. <span data-ttu-id="e6a9d-146">**方向**指示数据的流动方向 (即, 它是否为输入或输出绑定)？</span><span class="sxs-lookup"><span data-stu-id="e6a9d-146">**Direction** Indicates the direction data is flowing, i.e., is it an input or output binding?</span></span>

<span data-ttu-id="e6a9d-147">此外, 大多数绑定类型还需要第四个属性:</span><span class="sxs-lookup"><span data-stu-id="e6a9d-147">Additionally, most binding types also need a fourth property:</span></span> 

4. <span data-ttu-id="e6a9d-148">**连接**提供包含连接字符串的应用设置密钥的名称。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-148">**Connection** Provides the name of an app setting key that contains the connection string.</span></span> <span data-ttu-id="e6a9d-149">绑定使用存储在应用程序设置中的连接字符串将机密信息保留在函数代码之外。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-149">Bindings use connection strings stored in app settings to keep secrets out of the function code.</span></span> <span data-ttu-id="e6a9d-150">这将使您的代码更具可配置性和安全性。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-150">This makes your code more configurable and secure.</span></span>

## <a name="create-a-binding"></a><span data-ttu-id="e6a9d-151">创建绑定</span><span class="sxs-lookup"><span data-stu-id="e6a9d-151">Create a binding</span></span>

<span data-ttu-id="e6a9d-152">绑定是在 JSON 中定义的。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-152">Bindings are defined in JSON.</span></span> <span data-ttu-id="e6a9d-153">绑定是在函数的配置文件中配置的, 该文件命名为*函数 json*并与您的函数代码位于同一文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-153">A binding is configured in your function's configuration file, which is named *function.json* and lives in the same folder as your function code.</span></span>

 <span data-ttu-id="e6a9d-154">我们来看一下示例*输入绑定*:</span><span class="sxs-lookup"><span data-stu-id="e6a9d-154">Let's examine a sample *input binding*:</span></span>

```json
    ...
    {
      "name": "headshotBlob",
      "type": "blob",
      "path": "thumbnail-images/{filename}",
      "connection": "HeadshotStorageConnection",
      "direction": "in"
    },
    ...
```

<span data-ttu-id="e6a9d-155">若要创建此绑定, 我们需要:</span><span class="sxs-lookup"><span data-stu-id="e6a9d-155">To create this binding, we:</span></span>

1. <span data-ttu-id="e6a9d-156">在*函数 json*文件中创建绑定。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-156">Create a binding in our *function.json* file.</span></span>

1. <span data-ttu-id="e6a9d-157">提供`name`变量的值。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-157">Provide the value for the `name` variable.</span></span> <span data-ttu-id="e6a9d-158">在此示例中, 变量保存 blob 数据。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-158">In this example, the variable holds the blob data.</span></span>

1. <span data-ttu-id="e6a9d-159">提供存储空间`type`。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-159">Provide the storage `type`.</span></span> <span data-ttu-id="e6a9d-160">在上面的示例中, 我们使用的是 Blob 存储。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-160">In the preceding example, we are using Blob storage.</span></span>

1. <span data-ttu-id="e6a9d-161">提供`path`, 它指定容器以及其中的项名称。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-161">Provide the `path`, which specifies the container and the item name that goes in it.</span></span> <span data-ttu-id="e6a9d-162">blob `path`的属性是必需的。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-162">The `path` property is required for blobs.</span></span>

1. <span data-ttu-id="e6a9d-163">提供在`connection`应用程序的设置文件中定义的字符串设置名称。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-163">Provide the `connection` string setting name defined in the application's settings file.</span></span> <span data-ttu-id="e6a9d-164">它用作查找连接字符串以连接到存储帐户的键。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-164">It's used as a key to find the connection string to connect to your storage account.</span></span>

1. <span data-ttu-id="e6a9d-165">将`direction`定义为`in`。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-165">Define the `direction` as `in`.</span></span> <span data-ttu-id="e6a9d-166">它读取 blob 中的数据。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-166">It reads data from the blob.</span></span>

<span data-ttu-id="e6a9d-167">绑定用于连接到函数中的数据。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-167">Bindings are used to connect to data in your function.</span></span> <span data-ttu-id="e6a9d-168">在此示例中, 我们使用了输入绑定来将我们的函数作为缩略图处理的用户图像连接起来。</span><span class="sxs-lookup"><span data-stu-id="e6a9d-168">In this example, we used an input binding to connect user images to be processed by our function as thumbnails.</span></span>
