<span data-ttu-id="44c8a-101">现在, 我们已创建了 function 应用程序, 我们来看看如何生成、配置和执行函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-101">Now that we have a function app created, let's look at how to build, configure, and execute a function.</span></span>

### <a name="triggers"></a><span data-ttu-id="44c8a-102">触发</span><span class="sxs-lookup"><span data-stu-id="44c8a-102">Triggers</span></span>

<span data-ttu-id="44c8a-103">函数是事件驱动的, 这意味着它们在响应事件时运行。</span><span class="sxs-lookup"><span data-stu-id="44c8a-103">Functions are event driven, which means they run in response to an event.</span></span>

<span data-ttu-id="44c8a-104">启动函数的事件的类型称为**触发器**。</span><span class="sxs-lookup"><span data-stu-id="44c8a-104">The type of event that starts the function is called a **trigger**.</span></span> <span data-ttu-id="44c8a-105">必须使用恰好一个触发器配置函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-105">You must configure a function with exactly one trigger.</span></span>

<span data-ttu-id="44c8a-106">Azure 支持以下服务的触发器。</span><span class="sxs-lookup"><span data-stu-id="44c8a-106">Azure supports triggers for the following services.</span></span>

| <span data-ttu-id="44c8a-107">服务</span><span class="sxs-lookup"><span data-stu-id="44c8a-107">Service</span></span>                 | <span data-ttu-id="44c8a-108">触发器说明</span><span class="sxs-lookup"><span data-stu-id="44c8a-108">Trigger description</span></span>  |
|-------------------------|---------|
| <span data-ttu-id="44c8a-109">Blob 存储</span><span class="sxs-lookup"><span data-stu-id="44c8a-109">Blob storage</span></span>            | <span data-ttu-id="44c8a-110">在检测到新的或更新的 blob 时启动函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-110">Start a function when a new or updated blob is detected.</span></span>       |
| <span data-ttu-id="44c8a-111">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44c8a-111">Cosmos DB</span></span>               | <span data-ttu-id="44c8a-112">在检测到插入和更新时启动函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-112">Start a function when inserts and updates are detected.</span></span>      |
| <span data-ttu-id="44c8a-113">事件网格</span><span class="sxs-lookup"><span data-stu-id="44c8a-113">Event Grid</span></span>              | <span data-ttu-id="44c8a-114">从事件网格收到事件时启动函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-114">Start a function when an event is received from Event Grid.</span></span>       |
| <span data-ttu-id="44c8a-115">http.sys</span><span class="sxs-lookup"><span data-stu-id="44c8a-115">HTTP</span></span>                    | <span data-ttu-id="44c8a-116">启动具有 HTTP 请求的函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-116">Start a function with an HTTP request.</span></span>      |
| <span data-ttu-id="44c8a-117">Microsoft Graph 事件</span><span class="sxs-lookup"><span data-stu-id="44c8a-117">Microsoft Graph Events</span></span>  | <span data-ttu-id="44c8a-118">启动用于响应来自 Microsoft Graph 的传入 webhook 的函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-118">Start a function in response to an incoming webhook from the Microsoft Graph.</span></span> <span data-ttu-id="44c8a-119">此触发器的每个实例都可以对一种 Microsoft Graph 资源类型做出反应。</span><span class="sxs-lookup"><span data-stu-id="44c8a-119">Each instance of this trigger can react to one Microsoft Graph resource type.</span></span>       |
| <span data-ttu-id="44c8a-120">队列存储</span><span class="sxs-lookup"><span data-stu-id="44c8a-120">Queue storage</span></span>           | <span data-ttu-id="44c8a-121">当队列上收到新项目时, 启动一个函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-121">Start a function when a new item is received on a queue.</span></span> <span data-ttu-id="44c8a-122">队列消息作为函数的输入提供。</span><span class="sxs-lookup"><span data-stu-id="44c8a-122">The queue message is provided as input to the function.</span></span>      |
| <span data-ttu-id="44c8a-123">服务总线</span><span class="sxs-lookup"><span data-stu-id="44c8a-123">Service Bus</span></span>             | <span data-ttu-id="44c8a-124">启动用于响应来自服务总线队列的邮件的函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-124">Start a function in response to messages from a Service Bus queue.</span></span>       |
| <span data-ttu-id="44c8a-125">计时器</span><span class="sxs-lookup"><span data-stu-id="44c8a-125">Timer</span></span>                   | <span data-ttu-id="44c8a-126">按计划启动函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-126">Start a function on a schedule.</span></span>       |

### <a name="bindings"></a><span data-ttu-id="44c8a-127">绑定</span><span class="sxs-lookup"><span data-stu-id="44c8a-127">Bindings</span></span>

<span data-ttu-id="44c8a-128">绑定是一种将数据和服务连接到您的函数的声明性方法。</span><span class="sxs-lookup"><span data-stu-id="44c8a-128">Bindings are a declarative way to connect data and services to your function.</span></span> <span data-ttu-id="44c8a-129">绑定知道如何与不同的服务进行通信, 这意味着您无需在函数中编写代码即可连接到数据源和管理连接。</span><span class="sxs-lookup"><span data-stu-id="44c8a-129">Bindings know how to talk to different services, which means you don't have to write code in your function to connect to data sources and manage connections.</span></span> <span data-ttu-id="44c8a-130">平台会将此复杂性作为绑定代码的一部分。</span><span class="sxs-lookup"><span data-stu-id="44c8a-130">The platform takes care of that complexity for you as part of the binding code.</span></span> <span data-ttu-id="44c8a-131">每个绑定都有一个方向代码从*输入*绑定中读取数据并将数据写入*输出*绑定。</span><span class="sxs-lookup"><span data-stu-id="44c8a-131">Each binding has a direction - your code reads data from *input* bindings and writes data to *output* bindings.</span></span> <span data-ttu-id="44c8a-132">每个函数都可以有零个或多个绑定, 以管理由函数处理的输入和输出数据。</span><span class="sxs-lookup"><span data-stu-id="44c8a-132">Each function can have zero or more bindings to manage the input and output data processed by the function.</span></span>

<span data-ttu-id="44c8a-133">触发器是一种特殊类型的输入绑定, 它具有启动执行的额外功能。</span><span class="sxs-lookup"><span data-stu-id="44c8a-133">A trigger is a special type of input binding that has the additional capability of initiating execution.</span></span>

<span data-ttu-id="44c8a-134">Azure 提供了[大量绑定](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)以连接到不同的存储和邮件服务。</span><span class="sxs-lookup"><span data-stu-id="44c8a-134">Azure provides a [large number of bindings](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings) to connect to different storage and messaging services.</span></span>

### <a name="a-sample-binding-definition"></a><span data-ttu-id="44c8a-135">示例绑定定义</span><span class="sxs-lookup"><span data-stu-id="44c8a-135">A sample binding definition</span></span>

<span data-ttu-id="44c8a-136">我们来看一个使用输入绑定 (触发器) 和输出绑定配置函数的示例。</span><span class="sxs-lookup"><span data-stu-id="44c8a-136">Let's look at an example of configuring a function with an input binding (trigger) and an output binding.</span></span> <span data-ttu-id="44c8a-137">假设我们要从 Blob 存储中读取数据, 在我们的函数中进行处理, 然后向队列中写入一条消息。</span><span class="sxs-lookup"><span data-stu-id="44c8a-137">Let's say we want to read data from Blob storage, process it in our function, and then write a message to a queue.</span></span> <span data-ttu-id="44c8a-138">您可以配置类型为*blob*的_输入绑定_和类型为*queue*的_输出绑定_。</span><span class="sxs-lookup"><span data-stu-id="44c8a-138">You would configure an _input binding_ of type *blob* and an _output binding_ of type *queue*.</span></span>

<span data-ttu-id="44c8a-139">可以在 Azure 门户中定义绑定, 并将其存储为 JSON 文件, 也可以直接编辑它们。</span><span class="sxs-lookup"><span data-stu-id="44c8a-139">Bindings can be defined in the Azure portal, and are stored as JSON files, which you can also edit directly.</span></span> <span data-ttu-id="44c8a-140">下面的 JSON 是函数的触发器和绑定的示例定义。</span><span class="sxs-lookup"><span data-stu-id="44c8a-140">The following JSON is sample definition of a trigger and binding for a function.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

<span data-ttu-id="44c8a-141">此示例显示了一个函数, 该函数由添加到名为**myqueue**的队列中的邮件触发。</span><span class="sxs-lookup"><span data-stu-id="44c8a-141">This example shows a function that is triggered by a message being added to a queue named **myqueue-items**.</span></span> <span data-ttu-id="44c8a-142">然后, 它将函数的返回值发送到 Azure 表存储中的**outTable**表。</span><span class="sxs-lookup"><span data-stu-id="44c8a-142">It then sends the return value of the function to the **outTable** table in Azure Table storage.</span></span> <span data-ttu-id="44c8a-143">这是一个非常简单的示例, 我们可以将输出更改为使用 SendGrid 绑定的电子邮件, 或将事件放在服务总线上, 以在体系结构中通知某个其他组件, 甚至让多个输出绑定将数据推送到各种服务。</span><span class="sxs-lookup"><span data-stu-id="44c8a-143">This is a very simple example, we could change the output to be an email using a SendGrid binding, or put an event onto a Service Bus to notify some other component in our architecture, or even have multiple output bindings to push data to various services.</span></span>

## <a name="creating-a-function-in-the-azure-portal"></a><span data-ttu-id="44c8a-144">在 Azure 门户中创建函数</span><span class="sxs-lookup"><span data-stu-id="44c8a-144">Creating a function in the Azure portal</span></span>

<span data-ttu-id="44c8a-145">Azure 为常见方案提供了几个预先准备的函数模板。</span><span class="sxs-lookup"><span data-stu-id="44c8a-145">Azure provides several pre-made function templates for common scenarios.</span></span>

### <a name="quickstart-templates"></a><span data-ttu-id="44c8a-146">快速入门模板</span><span class="sxs-lookup"><span data-stu-id="44c8a-146">Quickstart templates</span></span>

<span data-ttu-id="44c8a-147">添加您的第一个函数时, 将显示快速入门屏幕。</span><span class="sxs-lookup"><span data-stu-id="44c8a-147">When adding your first function, you are presented with the Quickstart screen.</span></span> <span data-ttu-id="44c8a-148">此屏幕允许您选择触发器类型 (HTTP、计时器或数据) 和编程语言 (c #、JavaScript、F # 或 Java)。</span><span class="sxs-lookup"><span data-stu-id="44c8a-148">This screen allows you to choose a trigger type (HTTP, Timer, or Data) and programming language (C#, JavaScript, F# or Java).</span></span> <span data-ttu-id="44c8a-149">然后, 根据你的选择, Azure 将使用提供的一些示例代码为你生成函数代码和配置, 以显示日志中收到的输入数据。</span><span class="sxs-lookup"><span data-stu-id="44c8a-149">Then, based on your selections, Azure will generate the function code and configuration for you with some sample code provided to display out the input data received in the log.</span></span>

### <a name="custom-function-templates"></a><span data-ttu-id="44c8a-150">自定义函数模板</span><span class="sxs-lookup"><span data-stu-id="44c8a-150">Custom function templates</span></span>

<span data-ttu-id="44c8a-151">通过选择快速入门模板, 可轻松访问最常见的方案。</span><span class="sxs-lookup"><span data-stu-id="44c8a-151">The selection of Quickstart templates provides easy access to the most common scenarios.</span></span> <span data-ttu-id="44c8a-152">但是, Azure 提供了30多个可供你使用的其他模板。</span><span class="sxs-lookup"><span data-stu-id="44c8a-152">However, Azure provides over 30 additional templates you can start with.</span></span> <span data-ttu-id="44c8a-153">在创建后续函数或使用快速入门屏幕上的 "**自定义函数**" 选项进行选择时, 可以从 "模板列表" 屏幕中选择这些功能。</span><span class="sxs-lookup"><span data-stu-id="44c8a-153">These can be selected from the template list screen when creating subsequent functions or be selected by using the **Custom function** option on the Quickstart screen.</span></span>

- <span data-ttu-id="44c8a-154">HTTP 触发器 w/c #、F # 或 JavaScript</span><span class="sxs-lookup"><span data-stu-id="44c8a-154">HTTP trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="44c8a-155">带有 c #、F # 或 JavaScript 的计时器触发器</span><span class="sxs-lookup"><span data-stu-id="44c8a-155">Timer trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="44c8a-156">带有 c #、F # 或 JavaScript 的队列触发器</span><span class="sxs-lookup"><span data-stu-id="44c8a-156">Queue trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="44c8a-157">服务总线队列触发器 w/c #、F # 或 JavaScript</span><span class="sxs-lookup"><span data-stu-id="44c8a-157">Service Bus Queue trigger w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="44c8a-158">Cosmos DB 触发器 w/c # 或 JavaScript</span><span class="sxs-lookup"><span data-stu-id="44c8a-158">Cosmos DB trigger w/ C# or JavaScript</span></span>
- <span data-ttu-id="44c8a-159">带有 c #、F # 或 JavaScript 的 IoT 中心 (事件中心)</span><span class="sxs-lookup"><span data-stu-id="44c8a-159">IoT Hub (Event Hub) w/ C#, F#, or JavaScript</span></span>
- <span data-ttu-id="44c8a-160">...以及更多</span><span class="sxs-lookup"><span data-stu-id="44c8a-160">... and many more</span></span>

## <a name="navigating-to-your-function-and-files"></a><span data-ttu-id="44c8a-161">导航到您的函数和文件</span><span class="sxs-lookup"><span data-stu-id="44c8a-161">Navigating to your function and files</span></span>

<span data-ttu-id="44c8a-162">从模板创建函数时, 将创建多个文件。</span><span class="sxs-lookup"><span data-stu-id="44c8a-162">When you create a function from a template, several files are created.</span></span> <span data-ttu-id="44c8a-163">例如, 如果您选择使用 JavaScript + API 快速入门, 则生成的文件将是配置文件、**函数 json**和源代码文件 (即 **.js**)。</span><span class="sxs-lookup"><span data-stu-id="44c8a-163">For example, if you opted to use the Webhook + API Quickstart using JavaScript, the files generated would be a configuration file, **function.json**, and a source code file, **index.js**.</span></span> <span data-ttu-id="44c8a-164">在函数应用门户中创建的函数将显示在 function 应用门户中的 "**函数**" 菜单项下。</span><span class="sxs-lookup"><span data-stu-id="44c8a-164">The functions you create in a function app appear under the **Functions** menu item in the function app portal.</span></span>

<span data-ttu-id="44c8a-165">当您在函数应用程序中选择函数时, 代码编辑器将打开并显示函数的代码, 如以下屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="44c8a-165">When you select a function in your function app, a code editor opens and displays the code for your function, as illustrated in the following screenshot.</span></span>

![显示 "函数编辑器" 边栏的 Azure 门户屏幕截图, 其中包括展开的 "视图文件" 菜单, 在应用程序服务导航中选择 "HttpTriggerJS1" 功能, 并突出显示 "查看文件" 菜单。](../media/4-file-navigation.png)

<span data-ttu-id="44c8a-167">如前面的屏幕截图中所示, 在右侧有一个弹出菜单, 其中包含用于**查看文件**的选项卡。</span><span class="sxs-lookup"><span data-stu-id="44c8a-167">As you can see in the preceding screenshot, there's a flyout menu on the right that includes a tab to **View files**.</span></span> <span data-ttu-id="44c8a-168">选择此选项卡将显示构成函数的文件结构。</span><span class="sxs-lookup"><span data-stu-id="44c8a-168">Selecting this tab shows the file structure that makes up your function.</span></span>

## <a name="testing-your-azure-function"></a><span data-ttu-id="44c8a-169">测试 Azure 函数</span><span class="sxs-lookup"><span data-stu-id="44c8a-169">Testing your Azure function</span></span>

<span data-ttu-id="44c8a-170">创建函数后, 需要对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="44c8a-170">Once you've created a function, you'll want to test it.</span></span> <span data-ttu-id="44c8a-171">有几种方法: 从 Azure 门户本身内部手动执行和测试。</span><span class="sxs-lookup"><span data-stu-id="44c8a-171">There are a couple of approaches: manual execution and testing from within the Azure portal itself.</span></span>

### <a name="manual-execution"></a><span data-ttu-id="44c8a-172">手动执行</span><span class="sxs-lookup"><span data-stu-id="44c8a-172">Manual execution</span></span>

<span data-ttu-id="44c8a-173">您可以通过手动触发已配置的触发器来启动函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-173">You can start a function by manually triggering the configured trigger.</span></span> <span data-ttu-id="44c8a-174">例如, 如果您使用的是 HTTP 触发器, 则可以使用 Postman 或卷曲的工具启动对函数终结点 URL 的 http 请求, 该 URL 可从 HTTP 触发器定义 (**Get function url**)。</span><span class="sxs-lookup"><span data-stu-id="44c8a-174">For instance, if you are using an HTTP trigger - you can use a tool such as Postman or cURL to initiate an HTTP request to your function endpoint URL, which is available from the HTTP trigger definition (**Get function URL**).</span></span>

### <a name="testing-in-the-azure-portal"></a><span data-ttu-id="44c8a-175">在 Azure 门户中进行测试</span><span class="sxs-lookup"><span data-stu-id="44c8a-175">Testing in the Azure portal</span></span>

<span data-ttu-id="44c8a-176">门户还提供了一种方便的方法来测试您的函数。</span><span class="sxs-lookup"><span data-stu-id="44c8a-176">The portal also provides a convenient way to test your functions.</span></span> <span data-ttu-id="44c8a-177">在代码窗口的右侧有一个弹出菜单选项卡式导航菜单。</span><span class="sxs-lookup"><span data-stu-id="44c8a-177">On the right side of the code window, there is a flyout tabbed navigation menu.</span></span> <span data-ttu-id="44c8a-178">此菜单包含一个**测试**项。</span><span class="sxs-lookup"><span data-stu-id="44c8a-178">This menu contains a **Test** item.</span></span> <span data-ttu-id="44c8a-179">展开菜单并选择此选项卡将为您提供执行函数和查看结果的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="44c8a-179">Expanding the menu and selecting this tab gives you another way to execute your function and view the result.</span></span> <span data-ttu-id="44c8a-180">当您在此测试窗口中单击 "**运行**" 时, 结果将显示在 "输出" 窗口中, 并显示一个状态代码。</span><span class="sxs-lookup"><span data-stu-id="44c8a-180">When you click **Run** in this test window, the results are displayed in the output window, along with a status code.</span></span>

## <a name="monitoring-dashboard"></a><span data-ttu-id="44c8a-181">监控仪表板</span><span class="sxs-lookup"><span data-stu-id="44c8a-181">Monitoring dashboard</span></span>

<span data-ttu-id="44c8a-182">在开发和生产过程中, 监视函数的能力非常关键。</span><span class="sxs-lookup"><span data-stu-id="44c8a-182">The ability to monitor your functions is critical during development and in production.</span></span> <span data-ttu-id="44c8a-183">如果你启用 application Insights 集成, Azure 门户将提供一个可用的监控仪表板。</span><span class="sxs-lookup"><span data-stu-id="44c8a-183">The Azure portal provides a monitoring dashboard available if you turn on the Application Insights integration.</span></span> <span data-ttu-id="44c8a-184">在函数应用程序导航菜单中, 展开函数节点后, 您将看到一个**监视器**菜单项。</span><span class="sxs-lookup"><span data-stu-id="44c8a-184">In the function app navigation menu, once you expand the function node you'll see a **Monitor** menu item.</span></span> <span data-ttu-id="44c8a-185">此监视器仪表板提供了查看函数执行的历史记录的快速方法, 并显示了 Application Insights 填充的时间戳、结果代码、持续时间和操作 ID。</span><span class="sxs-lookup"><span data-stu-id="44c8a-185">This monitor dashboard provides a quick way to view the history of function executions and displays the timestamp, result code, duration, and operation ID populated by Application Insights.</span></span>

![显示 http 函数监视器刀片的 Azure 门户屏幕截图, 其中包含多个函数结果及其对应的 HTTP 状态代码, 并突出显示函数的模块菜单项。](../media/4-monitor-function.png)

## <a name="streaming-log-window"></a><span data-ttu-id="44c8a-187">流式处理日志窗口</span><span class="sxs-lookup"><span data-stu-id="44c8a-187">Streaming log window</span></span>

<span data-ttu-id="44c8a-188">您还可以将日志记录语句添加到您的函数以在 Azure 门户中进行调试。</span><span class="sxs-lookup"><span data-stu-id="44c8a-188">You're also able to add logging statements to your function for debugging in the Azure portal.</span></span> <span data-ttu-id="44c8a-189">向每种语言的被调用方法传递一个 "日志记录" 对象, 该对象可用于将信息记录到位于 "代码" 窗口底部的选项卡式弹出菜单中的 "日志" 窗口中。</span><span class="sxs-lookup"><span data-stu-id="44c8a-189">The called methods for each language are passed a "logging" object, which may be used to log information to the log window located in a tabbed flyout menu located at the bottom of the code window.</span></span>

<span data-ttu-id="44c8a-190">以下 JavaScript 代码段显示了如何使用`context.log`方法记录消息 ( `context`对象传递给处理程序)。</span><span class="sxs-lookup"><span data-stu-id="44c8a-190">The following JavaScript code snippet shows how to log a message using the `context.log` method (the `context` object is passed to the handler).</span></span>

```javascript
  context.log('Enter your logging statement here');
```

<span data-ttu-id="44c8a-191">我们可以使用`log.Info`方法在 c # 中执行相同的操作。</span><span class="sxs-lookup"><span data-stu-id="44c8a-191">We could do the same thing in C# using the `log.Info` method.</span></span> <span data-ttu-id="44c8a-192">在这种情况下`log` , 对象将传递给处理函数的 c # 方法。</span><span class="sxs-lookup"><span data-stu-id="44c8a-192">In this case, the `log` object is passed to the C# method processing the function.</span></span>

```csharp
  log.Info("Enter your logging statement here");
```

### <a name="errors-and-warnings-window"></a><span data-ttu-id="44c8a-193">"错误和警告" 窗口</span><span class="sxs-lookup"><span data-stu-id="44c8a-193">Errors and warnings window</span></span>

<span data-ttu-id="44c8a-194">您可以在日志窗口所在的同一个弹出菜单中找到 "错误和警告" 窗口选项卡。</span><span class="sxs-lookup"><span data-stu-id="44c8a-194">You can locate the errors and warnings window tab in the same flyout menu as the log window.</span></span> <span data-ttu-id="44c8a-195">此窗口将显示代码中的编译错误和警告。</span><span class="sxs-lookup"><span data-stu-id="44c8a-195">This window will show compilation errors and warnings within your code.</span></span>
