<span data-ttu-id="2d5cb-101">让我们更新函数实现以调用文本分析 API 服务, 并返回看法分数。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-101">Let's update our function implementation to call the Text Analytics API service and get back a sentiment score.</span></span>

1. <span data-ttu-id="2d5cb-102">在门户的函数[!INCLUDE [func-name-discover](./func-name-discover.md)]应用中, 选择我们的函数。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-102">Select our function, [!INCLUDE [func-name-discover](./func-name-discover.md)], in our function app in the portal.</span></span>

1. <span data-ttu-id="2d5cb-103">展开屏幕右侧的 "**查看文件**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-103">Expand the **View files** menu on the right of the screen.</span></span>

1. <span data-ttu-id="2d5cb-104">在 "**查看文件**" 选项卡下, 选择**index .js**以在编辑器中打开代码文件。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-104">Under the **View files** tab, select **index.js** to open the code file in the editor.</span></span>

1. <span data-ttu-id="2d5cb-105">将包含以下 JavaScript 的\*\*\*\* 所有内容替换为以下 JavaScript 并**保存**。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-105">Replace the entire content of **index.js** with the following JavaScript and **Save**.</span></span>

    [!code-javascript[](../code/discover-sentiment-sort.js?highlight=7)]

1. <span data-ttu-id="2d5cb-106">使用您之前在`accessKey`本模块中保存的文本分析 API 的访问键更新您粘贴的代码中的值。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-106">Update the value of `accessKey` in the code you pasted with the access key for the Text Analytics API that you saved earlier in this module.</span></span> 

1. <span data-ttu-id="2d5cb-107">使用从中`uri`获取访问键的区域更新值。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-107">Update the `uri` value with the region from which you obtained your access key.</span></span>

<span data-ttu-id="2d5cb-108">让我们看一下此代码中发生的情况:</span><span class="sxs-lookup"><span data-stu-id="2d5cb-108">Let's look at what's happening in this code:</span></span>

- <span data-ttu-id="2d5cb-109">每次调用 Text Analytics service 时, 都需要访问密钥, 我们将其添加为`Ocp-Apim-Subscription-Key`标头。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-109">Each call to the Text Analytics service, needs the access key, which we add as the `Ocp-Apim-Subscription-Key` header.</span></span> 
- <span data-ttu-id="2d5cb-110">每次调用的区域特定终结点, `uri`在我们的代码中进行定义。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-110">Each call is made to a region-specific endpoint, defined by `uri` in our code.</span></span>
- <span data-ttu-id="2d5cb-111">在代码文件的底部, 定义了一个`documents`数组。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-111">At the bottom of the code file, we've defined a `documents` array.</span></span> <span data-ttu-id="2d5cb-112">此数组是我们向 Text Analytics service 发送的有效负载。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-112">This array is the payload we send to the Text Analytics service.</span></span>
- <span data-ttu-id="2d5cb-113">在`documents`这种情况下, 该数组具有单个条目, 即触发我们的函数的队列消息。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-113">The `documents` array has a single entry in this case, which is the queue message that triggered our function.</span></span> <span data-ttu-id="2d5cb-114">尽管我们的数组中仅有一个文档, 但并不意味着我们的解决方案一次只能处理一封邮件。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-114">Although we only have one document in our array, it doesn't mean that our solution can only handle one message at a time.</span></span> <span data-ttu-id="2d5cb-115">Azure 函数运行时以批处理方式检索和处理消息,*同时*调用我们的函数的多个实例。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-115">The Azure Functions runtime retrieves and processes messages in batches, calling several instances of our function *in parallel*.</span></span> <span data-ttu-id="2d5cb-116">目前, 默认批次大小为 16, 最大批处理大小为32。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-116">Currently, the default batch size is 16 and the maximum batch size is 32.</span></span>
- <span data-ttu-id="2d5cb-117">在`id`数组中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-117">The `id` must be unique within the array.</span></span> <span data-ttu-id="2d5cb-118">`language`属性指定文档文本的语言。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-118">The `language` property specifies the language of the document text.</span></span>
- <span data-ttu-id="2d5cb-119">然后, 我们调用方法`get_sentiments`, 该方法使用 HTTPS 模块对 Text Analytics API 进行调用。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-119">We then call our method `get_sentiments`, which uses the HTTPS module to make the call to Text Analytics API.</span></span> <span data-ttu-id="2d5cb-120">请注意, 我们会在每个请求的标头中传递订阅或访问密钥。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-120">Notice that we pass our subscription, or access, key in the header of every request.</span></span>
- <span data-ttu-id="2d5cb-121">当服务返回时, 我们`response_handler`将被称为, 我们会将此响应记录在使用`context.log`</span><span class="sxs-lookup"><span data-stu-id="2d5cb-121">When the service returns, our `response_handler` is called, and we log the response to the console using `context.log`</span></span>


## <a name="try-it-out"></a><span data-ttu-id="2d5cb-122">试用</span><span class="sxs-lookup"><span data-stu-id="2d5cb-122">Try it out</span></span>

<span data-ttu-id="2d5cb-123">在查看队列中的排序之前, 让我们对测试运行采取相应的操作。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-123">Before we look at sorting into queues, let's take what we have for a test run.</span></span>

1. <span data-ttu-id="2d5cb-124">使用我们的函数[!INCLUDE [func-name-discover](./func-name-discover.md)], 在门户的 "函数应用" 区域中选择, 单击最右侧的 "**测试**" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-124">With our function, [!INCLUDE [func-name-discover](./func-name-discover.md)], selected in the Function Apps area of the portal, click on the **Test** menu item on the far right.</span></span>

1. <span data-ttu-id="2d5cb-125">选择 "**测试**" 菜单项, 并验证是否打开了测试面板。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-125">Select the **Test** menu item, and verify that you have the test panel open.</span></span>

1. <span data-ttu-id="2d5cb-126">将文本字符串添加到请求正文中, 如屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-126">Add a string of text into the request body as shown in the screenshot.</span></span>

    ![显示已展开的函数测试面板的屏幕截图。](../media/test-panel-open-small.png)

1.  <span data-ttu-id="2d5cb-128">单击 "测试" 面板底部的 "**运行**"。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-128">Click **Run** at the bottom of the test panel.</span></span>

1. <span data-ttu-id="2d5cb-129">请确保 "**日志**" 选项卡在主屏幕的左下角展开, 在代码编辑器下。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-129">Make sure the **Logs** tab is expanded at the bottom left of the main screen, under the code editor.</span></span>

1. <span data-ttu-id="2d5cb-130">验证 "**日志**" 选项卡是否显示函数已完成的日志信息。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-130">Verify that the **Logs** tab displays log information that the function completed.</span></span> <span data-ttu-id="2d5cb-131">该窗口还将显示来自文本分析 API 调用的响应。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-131">The window will also display the response from the Text Analytics API call.</span></span>

    ![显示测试面板和成功测试结果的屏幕截图。](../media/sentiment-response-log1.png)

<span data-ttu-id="2d5cb-133">!!</span><span class="sxs-lookup"><span data-stu-id="2d5cb-133">Congratulations!</span></span> <span data-ttu-id="2d5cb-134">按[!INCLUDE [func-name-discover](./func-name-discover.md)]设计方式工作。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-134">The [!INCLUDE [func-name-discover](./func-name-discover.md)] works as designed.</span></span> <span data-ttu-id="2d5cb-135">在此示例中, 我们传递了一个非常 upbeat 的邮件并收到超过0.98 的分数。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-135">In this example, we passed in a very upbeat message and received a score of over 0.98.</span></span> <span data-ttu-id="2d5cb-136">尝试将邮件更改为 "乐观不变", 再重新运行测试, 并记下响应。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-136">Try changing the message to something less optimistic, rerun the test, and note the response.</span></span>

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="2d5cb-137">向队列中添加消息</span><span class="sxs-lookup"><span data-stu-id="2d5cb-137">Add a message to the queue</span></span>

<span data-ttu-id="2d5cb-138">让我们重复此测试。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-138">Let's repeat the test.</span></span> <span data-ttu-id="2d5cb-139">在这段时间, 我们实际上会将一条消息放入输入队列并观看所发生的情况, 而不是使用门户的测试窗口。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-139">This time, instead of using the Test window of the portal, we'll actually place a message into the input queue and watch what happens.</span></span>

1. <span data-ttu-id="2d5cb-140">导航到门户的 "**资源组**" 部分中的资源组。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-140">Navigate to your resource group in the **Resource Groups** section of the portal.</span></span>

1. <span data-ttu-id="2d5cb-141">选择<rgn>[沙盒资源组名称]</rgn>, 在本课中使用的资源组。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-141">Select <rgn>[sandbox resource group name]</rgn>, the resource group used in this lesson.</span></span>

1. <span data-ttu-id="2d5cb-142">在出现的 "**资源组**" 面板中, 找到 "存储帐户" 条目, 然后选择它。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-142">In the **Resource group** panel that appears, locate the Storage Account entry, and select it.</span></span>

    ![在资源组窗口中选择的屏幕截图存储帐户](../media/select-storage-account.png)

1. <span data-ttu-id="2d5cb-144">从 "存储帐户" 主窗口的左侧菜单中选择 "**存储资源管理器 (预览)** "。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-144">Select **Storage Explorer (preview)** from the left menu of the Storage Account main window.</span></span> <span data-ttu-id="2d5cb-145">此操作将在门户中打开 Azure 存储资源管理器。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-145">This action opens the Azure Storage Explorer inside the portal.</span></span> 

    ![存储资源管理器显示存储帐户的屏幕截图, 当前没有队列。](../media/sa-no-queue.png)

    <span data-ttu-id="2d5cb-147">正如你所看到的, 我们尚未拥有此存储帐户中的任何队列, 因此我们添加一个队列。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-147">As you can see, we don't have any queues in this storage account yet, so let's add one.</span></span>

1. <span data-ttu-id="2d5cb-148">如果您记得本课前面的部分, 我们命名了与我们的触发**新反馈-q**关联的队列。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-148">If you remember from earlier in this lesson, we named the queue associated with our trigger **new-feedback-q**.</span></span> <span data-ttu-id="2d5cb-149">右键单击存储资源管理器中的 "**队列**" 项, 然后选择 "*创建队列*"。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-149">Right-click on the **Queues** item in the Storage Explorer, and select *Create Queue*.</span></span>

1. <span data-ttu-id="2d5cb-150">在打开的对话框中, 输入 "**新反馈-q** ", 然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-150">In the dialog that opens, enter **new-feedback-q** and click **OK**.</span></span> <span data-ttu-id="2d5cb-151">现在, 我们提供了输入队列。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-151">We now have our input queue.</span></span>

1. <span data-ttu-id="2d5cb-152">在左侧菜单中选择新队列, 以查看此队列的数据资源管理器。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-152">Select the new queue in the left-hand menu to see the data explorer for this queue.</span></span> <span data-ttu-id="2d5cb-153">正如预期的那样, 队列是空的。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-153">As expected, the queue is empty.</span></span> <span data-ttu-id="2d5cb-154">让我们使用窗口顶部的 "**添加消息**" 命令向队列中添加一条消息。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-154">Let's add a message to the queue using the **Add Message** command at the top of the window.</span></span>

1. <span data-ttu-id="2d5cb-155">在 "**添加消息**" 对话框中, 在 "**消息" 文本**字段中输入 "此消息来自我们的输入队列, 新的反馈-q", 然后单击对话框底部的 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-155">In the **Add Message** dialog, enter "This message came from our input queue, new-feedback-q" into the **Message text** field, and click **OK** at the bottom of the dialog.</span></span>

1. <span data-ttu-id="2d5cb-156">在数据浏览器中观察消息, 与以下屏幕截图中的消息类似。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-156">Observe the message, similar to the message in the following screenshot, in the data explorer.</span></span>
    <span data-ttu-id="2d5cb-157">![显示存储资源管理器的屏幕截图, 其中包含我们在队列中创建的消息。](../media/message-in-input-queue.png)</span><span class="sxs-lookup"><span data-stu-id="2d5cb-157">![Screenshot of Storage Explorer showing our storage account, with the message we created in the queue.](../media/message-in-input-queue.png)</span></span>

1. <span data-ttu-id="2d5cb-158">几秒钟后, 单击 "**刷新**" 以刷新队列视图。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-158">After a few seconds, click **Refresh** to refresh the view of the queue.</span></span> <span data-ttu-id="2d5cb-159">再次观察队列是否为**空**。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-159">Observe that the queue is **empty** once again.</span></span> <span data-ttu-id="2d5cb-160">必须已从队列中读取邮件。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-160">Something must have read the message from the queue.</span></span>

1. <span data-ttu-id="2d5cb-161">导航回门户中的函数, 并打开 "**监视器**" 选项卡。选择列表中的最新邮件。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-161">Navigate back to our function in the portal, and open the **Monitor** tab. Select the newest message in the list.</span></span> <span data-ttu-id="2d5cb-162">请注意, 我们的函数处理了我们发布到新反馈-q 的队列消息。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-162">Observe that our function processed the queue message we had posted to the new-feedback-q.</span></span> <span data-ttu-id="2d5cb-163">在此日志中可能会延迟结果, 因此您可能需要等待几分钟, 然后再进行命中*刷新*。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-163">Results may be delayed by in this log, so you might have to wait a few minutes and hit *Refresh*.</span></span>

    ![监视器仪表板的屏幕截图, 显示一个条目, 告诉我们我们的函数处理了我们发布到新反馈-q 的队列消息。](../media/message-in-monitor.png)

    <span data-ttu-id="2d5cb-165">在此测试中, 我们完成了在队列中发布内容的完整往返行程, 然后查看函数对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-165">In this test, we did a complete round trip of posting something into our queue and then seeing the function process it.</span></span>

<span data-ttu-id="2d5cb-166">我们正在为我们的解决方案做进展!</span><span class="sxs-lookup"><span data-stu-id="2d5cb-166">We're making progress with our solution!</span></span> <span data-ttu-id="2d5cb-167">我们的函数现在要做一些有用的事情。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-167">Our function is now doing something useful.</span></span> <span data-ttu-id="2d5cb-168">它从输入队列中接收文本, 然后调出到文本分析 API 服务, 以获取看法分数。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-168">It's receiving text from our input queue and then calling out to the Text Analytics API service to get a sentiment score.</span></span> <span data-ttu-id="2d5cb-169">我们还学习了如何通过 Azure 门户和存储浏览器测试函数。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-169">We've also learned how to test our function through the Azure portal and the Storage Explorer.</span></span> <span data-ttu-id="2d5cb-170">在下一个练习中, 我们将了解使用输出绑定向队列中写入的难易程度。</span><span class="sxs-lookup"><span data-stu-id="2d5cb-170">In the next exercise, we'll see how easy it is to write to queues using output bindings.</span></span>