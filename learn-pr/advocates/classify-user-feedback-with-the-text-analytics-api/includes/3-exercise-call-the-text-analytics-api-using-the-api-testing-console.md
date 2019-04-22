<span data-ttu-id="638e4-101">若要查看正在运行的文本分析 API, 我们可以使用位于联机参考文档中的内置 API 测试控制台工具进行一些调用。</span><span class="sxs-lookup"><span data-stu-id="638e4-101">To see the Text Analytics API in action, let's make some calls using the built-in API testing console tool located in the online reference documentation.</span></span> <span data-ttu-id="638e4-102">在执行此操作之前, 我们需要使用访问密钥才能进行这些呼叫。</span><span class="sxs-lookup"><span data-stu-id="638e4-102">Before we do that, we'll need an access key to make those calls.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-access-key"></a><span data-ttu-id="638e4-103">创建访问键</span><span class="sxs-lookup"><span data-stu-id="638e4-103">Create an access key</span></span>

<span data-ttu-id="638e4-104">每次调用 Text Analytics API 都需要订阅密钥。</span><span class="sxs-lookup"><span data-stu-id="638e4-104">Every call to Text Analytics API requires a subscription key.</span></span> <span data-ttu-id="638e4-105">通常称为访问密钥, 用于验证您是否具有进行呼叫的访问权限。</span><span class="sxs-lookup"><span data-stu-id="638e4-105">Often called an access key, it is used to validate that you have access to make the call.</span></span> <span data-ttu-id="638e4-106">我们将使用 Azure 门户来获取密钥。</span><span class="sxs-lookup"><span data-stu-id="638e4-106">We'll use the Azure portal to grab a key.</span></span>

1. <span data-ttu-id="638e4-107">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="638e4-107">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="638e4-108">单击 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="638e4-108">Click **Create a resource**.</span></span>

1. <span data-ttu-id="638e4-109">在 "**搜索市场"** 搜索框中, 键入*文本分析*和命中返回。</span><span class="sxs-lookup"><span data-stu-id="638e4-109">In the **Search the Marketplace** search box, type in *text analytics* and hit return.</span></span>

1. <span data-ttu-id="638e4-110">在搜索结果中选择 "**文本分析**", 然后选择屏幕右下角的 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="638e4-110">Select **Text Analytics** in the search results and then select the **Create** button in the bottom right of the screen.</span></span>

1. <span data-ttu-id="638e4-111">在打开的 "**创建**" 页中, 在每个字段中输入以下值。</span><span class="sxs-lookup"><span data-stu-id="638e4-111">In the **Create** page that opens, enter the following values into each field.</span></span>

    |<span data-ttu-id="638e4-112">属性</span><span class="sxs-lookup"><span data-stu-id="638e4-112">Property</span></span>  | <span data-ttu-id="638e4-113">值</span><span class="sxs-lookup"><span data-stu-id="638e4-113">Value</span></span>  | <span data-ttu-id="638e4-114">说明</span><span class="sxs-lookup"><span data-stu-id="638e4-114">Description</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="638e4-115">名称</span><span class="sxs-lookup"><span data-stu-id="638e4-115">Name</span></span>     |    <span data-ttu-id="638e4-116">MyTextAnalyticsAPIAccount</span><span class="sxs-lookup"><span data-stu-id="638e4-116">MyTextAnalyticsAPIAccount</span></span>     |  <span data-ttu-id="638e4-117">认知服务帐户的名称。</span><span class="sxs-lookup"><span data-stu-id="638e4-117">The name of the Cognitive Services account.</span></span> <span data-ttu-id="638e4-118">建议使用描述性名称。</span><span class="sxs-lookup"><span data-stu-id="638e4-118">We recommend using a descriptive name.</span></span> <span data-ttu-id="638e4-119">有效的字符`a-z`为`0-9`、和`-`。</span><span class="sxs-lookup"><span data-stu-id="638e4-119">Valid characters are `a-z`, `0-9`, and `-`.</span></span>    |
    |<span data-ttu-id="638e4-120">订购</span><span class="sxs-lookup"><span data-stu-id="638e4-120">Subscription</span></span>     |  <span data-ttu-id="638e4-121">Concierge 订阅</span><span class="sxs-lookup"><span data-stu-id="638e4-121">Concierge Subscription</span></span>    |   <span data-ttu-id="638e4-122">在其下创建此新的认知服务 API 帐户和**文本分析 API**所使用的订阅。</span><span class="sxs-lookup"><span data-stu-id="638e4-122">The subscription under which this new Cognitive Services API account with **Text Analytics API** is created.</span></span>      |
    |<span data-ttu-id="638e4-123">位置</span><span class="sxs-lookup"><span data-stu-id="638e4-123">Location</span></span>     |  <span data-ttu-id="638e4-124">*从下拉列表中选择区域*</span><span class="sxs-lookup"><span data-stu-id="638e4-124">*choose a region from the dropdown*</span></span>       |  <span data-ttu-id="638e4-125">由于你使用的是免费沙盒, 请从下拉列表中选择一个位置, 该位置**也**在下面所示的沙盒区域列表中。</span><span class="sxs-lookup"><span data-stu-id="638e4-125">Since you're using the free sandbox, select a location from the dropdown that is **also** on the sandbox region list shown below.</span></span>  |
    |<span data-ttu-id="638e4-126">定价层</span><span class="sxs-lookup"><span data-stu-id="638e4-126">Pricing tier</span></span>     | <span data-ttu-id="638e4-127">**F0 免费**</span><span class="sxs-lookup"><span data-stu-id="638e4-127">**F0 Free**</span></span>     |   <span data-ttu-id="638e4-128">您的认知服务帐户的成本取决于实际使用情况和您选择的选项。</span><span class="sxs-lookup"><span data-stu-id="638e4-128">The cost of your Cognitive Services account depends on the actual usage and the options you choose.</span></span> <span data-ttu-id="638e4-129">我们建议在此处选择免费的层。</span><span class="sxs-lookup"><span data-stu-id="638e4-129">We recommend selecting the free tier for our purposes here.</span></span>      |
    |<span data-ttu-id="638e4-130">资源组</span><span class="sxs-lookup"><span data-stu-id="638e4-130">Resource group</span></span>     |  <span data-ttu-id="638e4-131">选择 "**使用现有**" 并选择 " <rgn>[沙盒资源组名称]</rgn> "</span><span class="sxs-lookup"><span data-stu-id="638e4-131">Select **Use existing** and choose <rgn>[sandbox resource group name]</rgn></span></span>       |  <span data-ttu-id="638e4-132">要在其中创建您的认知服务文本分析 API 帐户的新资源组的名称。</span><span class="sxs-lookup"><span data-stu-id="638e4-132">Name for the new resource group in which to create your Cognitive Services Text Analytics API account.</span></span>       |

    ### <a name="sandbox-region-list"></a><span data-ttu-id="638e4-133">沙盒区域列表</span><span class="sxs-lookup"><span data-stu-id="638e4-133">Sandbox region list</span></span>
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    > [!TIP]
    > <span data-ttu-id="638e4-134">在创建文本分析认知服务帐户时, 请记住您选择的位置。</span><span class="sxs-lookup"><span data-stu-id="638e4-134">Remember the location you selected when creating the Text Analytics cognitive services account.</span></span> <span data-ttu-id="638e4-135">你将使用它来很快进行 API 调用。</span><span class="sxs-lookup"><span data-stu-id="638e4-135">You'll use it to make API calls shortly.</span></span> 

1. <span data-ttu-id="638e4-136">在页面底部选择 "**创建**" 以启动帐户创建过程。</span><span class="sxs-lookup"><span data-stu-id="638e4-136">Select **Create** at the bottom of the page to start the account creation process.</span></span> <span data-ttu-id="638e4-137">监视部署正在进行的通知。</span><span class="sxs-lookup"><span data-stu-id="638e4-137">Watch for a notification that the deployment is in progress.</span></span> <span data-ttu-id="638e4-138">然后, 你将收到一条通知, 表明已成功将该帐户部署到你的资源组。</span><span class="sxs-lookup"><span data-stu-id="638e4-138">You'll then get a notification that the account has been deployed successfully to your resource group.</span></span>

    ![部署已成功通知, 其中包含 "转到资源" 按钮和 "固定到仪表板" 按钮。](../media/deploy-resource-group-success.PNG)

## <a name="get-the-access-key"></a><span data-ttu-id="638e4-140">获取访问键</span><span class="sxs-lookup"><span data-stu-id="638e4-140">Get the access key</span></span>

<span data-ttu-id="638e4-141">现在我们有了认知服务帐户, 我们来查找访问键, 以便我们可以开始调用 API。</span><span class="sxs-lookup"><span data-stu-id="638e4-141">Now that we have our Cognitive Services account, let's find the access key so we can start calling the API.</span></span>

1. <span data-ttu-id="638e4-142">单击 "*部署成功*通知" 上的 "**转到资源**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="638e4-142">Click on the **Go to resource** button on the *Deployment succeeded* notification.</span></span> <span data-ttu-id="638e4-143">此操作将打开帐户快速入门。</span><span class="sxs-lookup"><span data-stu-id="638e4-143">This action opens the account Quickstart.</span></span>

1. <span data-ttu-id="638e4-144">从左侧的菜单中或在快速入门的 "*获取密钥*" 部分中选择 "**键**" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="638e4-144">Select the **Keys** menu item from the menu on the left, or in the *Grab your keys* section of the quickstart.</span></span> <span data-ttu-id="638e4-145">此操作将打开 "**管理密钥**" 页。</span><span class="sxs-lookup"><span data-stu-id="638e4-145">This action opens the **Manage keys** page.</span></span>

1. <span data-ttu-id="638e4-146">使用 "复制" 按钮复制其中一个键。</span><span class="sxs-lookup"><span data-stu-id="638e4-146">Copy one of the keys using the copy button.</span></span>

    !["管理密钥" 用户界面, 显示认知服务帐户和 key 1 和 key 2 条目的名称。](../media/manage-keys.PNG)

    > [!IMPORTANT]
    > <span data-ttu-id="638e4-148">始终保持访问密钥为安全, 永远不会共享它们。</span><span class="sxs-lookup"><span data-stu-id="638e4-148">Always keep your access keys safe and never share them.</span></span>

1. <span data-ttu-id="638e4-149">将此键存储在本模块的其余部分。</span><span class="sxs-lookup"><span data-stu-id="638e4-149">Store this key for the rest of this module.</span></span> <span data-ttu-id="638e4-150">我们很快就会使用它从测试控制台和模块中的其余部分进行 API 调用。</span><span class="sxs-lookup"><span data-stu-id="638e4-150">We'll use it shortly to make API calls from the testing console and throughout the rest of the module.</span></span>

## <a name="call-the-api-from-the-testing-console"></a><span data-ttu-id="638e4-151">从测试控制台调用 API</span><span class="sxs-lookup"><span data-stu-id="638e4-151">Call the API from the testing console</span></span>

<span data-ttu-id="638e4-152">现在我们拥有我们的关键, 我们可以转到测试控制台并采用 API 进行旋转。</span><span class="sxs-lookup"><span data-stu-id="638e4-152">Now that we have our key, we can head over to the testing console and take the API for a spin.</span></span>

1. <span data-ttu-id="638e4-153">导航到您喜爱的浏览器中的以下 URL。</span><span class="sxs-lookup"><span data-stu-id="638e4-153">Navigate to the following URL in your favorite browser.</span></span> <span data-ttu-id="638e4-154">在`[location]`此单元前面创建文本分析认知服务帐户时, 将替换为您选择的位置。</span><span class="sxs-lookup"><span data-stu-id="638e4-154">Replace `[location]` with the location you selected when creating the Text Analytics cognitive services account earlier in this unit.</span></span> <span data-ttu-id="638e4-155">例如, 如果您在*eastus*中创建了帐户, 您需要将`[location]`替换`eastus`为 URL 中的。</span><span class="sxs-lookup"><span data-stu-id="638e4-155">For example, if you created the account in *eastus*, you'd replace `[location]` with `eastus` in the URL.</span></span>

    ```bash
    https://[location].dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0
    ```

    <span data-ttu-id="638e4-156">登陆页面在左侧显示一个菜单, 并在右侧显示内容。</span><span class="sxs-lookup"><span data-stu-id="638e4-156">The landing page displays a menu on the left and content to the right.</span></span> <span data-ttu-id="638e4-157">该菜单列出了可以在文本分析 API 上调用的 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="638e4-157">The menu lists the POST methods you can call on the Text Analytics API.</span></span> <span data-ttu-id="638e4-158">这些终结点将**检测语言**、**实体**、**关键短语**和**看法**。</span><span class="sxs-lookup"><span data-stu-id="638e4-158">These endpoints are **Detect Language**, **Entities**, **Key Phrases**, and **Sentiment**.</span></span> <span data-ttu-id="638e4-159">若要调用这些操作之一, 我们需要执行几项操作。</span><span class="sxs-lookup"><span data-stu-id="638e4-159">To call one of these operations, we need to do a few things.</span></span>

    - <span data-ttu-id="638e4-160">选择我们要调用的方法。</span><span class="sxs-lookup"><span data-stu-id="638e4-160">Select the method we want to call.</span></span>
    - <span data-ttu-id="638e4-161">将我们之前在本课中保存的访问键添加到每个调用中。</span><span class="sxs-lookup"><span data-stu-id="638e4-161">Add the access key that we saved earlier in the lesson to each call.</span></span>

1. <span data-ttu-id="638e4-162">从左侧菜单中, 选择 "**看法**"。</span><span class="sxs-lookup"><span data-stu-id="638e4-162">From the left menu, select **Sentiment**.</span></span> <span data-ttu-id="638e4-163">此选择将向右打开看法文档。</span><span class="sxs-lookup"><span data-stu-id="638e4-163">This selection opens the Sentiment documentation to the right.</span></span> <span data-ttu-id="638e4-164">如文档所示, 我们将使用以下格式进行 REST 调用。</span><span class="sxs-lookup"><span data-stu-id="638e4-164">As the documentation shows, we'll be making a REST call in the following format.</span></span>  

    `https://[location].api.cognitive.microsoft.com/text/analytics/v2.0/sentiment`

     <span data-ttu-id="638e4-165">`[location]`将替换为您在创建文本分析帐户时选择的位置。</span><span class="sxs-lookup"><span data-stu-id="638e4-165">`[location]` is replaced with the location that you selected when you created the Text Analytics account.</span></span>  
<span data-ttu-id="638e4-166">我们将在**Apim-订阅密钥**标头中传入订阅密钥或访问密钥。</span><span class="sxs-lookup"><span data-stu-id="638e4-166">We'll pass in our subscription key, or access key, in the **ocp-Apim-Subscription-Key** header.</span></span>

## <a name="make-some-api-calls"></a><span data-ttu-id="638e4-167">进行一些 API 调用</span><span class="sxs-lookup"><span data-stu-id="638e4-167">Make some API calls</span></span>

1. <span data-ttu-id="638e4-168">选择 "**打开 API 测试控制台**" 按钮以打开 live、交互的 api 控制台。</span><span class="sxs-lookup"><span data-stu-id="638e4-168">Select the **Open API testing console** button to open the live, interactive, API console.</span></span>

1. <span data-ttu-id="638e4-169">将之前保存的访问密钥粘贴到标记为**Apim-key**的字段中。</span><span class="sxs-lookup"><span data-stu-id="638e4-169">Paste the access key you saved earlier into the field labeled **Ocp-Apim-Subscription-Key**.</span></span> <span data-ttu-id="638e4-170">请注意, 密钥将自动写入 HTTP 请求窗口作为标头值。</span><span class="sxs-lookup"><span data-stu-id="638e4-170">Notice that the key is written automatically into the HTTP request window as a header value.</span></span>

1. <span data-ttu-id="638e4-171">滚动到页面底部, 然后单击 "**发送**"。</span><span class="sxs-lookup"><span data-stu-id="638e4-171">Scroll to the bottom of the page and click **Send**.</span></span>

    <span data-ttu-id="638e4-172">让我们更详细地查看此屏幕的各个部分。</span><span class="sxs-lookup"><span data-stu-id="638e4-172">Let's examine the sections of this screen in more detail.</span></span>

    <span data-ttu-id="638e4-173">在用户界面的 "标头" 部分中, 我们设置请求的标头中的 "访问" 或 "订阅" 项。</span><span class="sxs-lookup"><span data-stu-id="638e4-173">In the Headers section of the user interface, we set the access, or subscription, key in the header of our request.</span></span>

    ![标头部分的屏幕截图。](../media/2-marker.PNG)

    <span data-ttu-id="638e4-175">接下来, 我们提供了 "请求正文" 部分, 其中包含一个**文档**数组。</span><span class="sxs-lookup"><span data-stu-id="638e4-175">Next, we have the request body section, which holds a **documents** array.</span></span> <span data-ttu-id="638e4-176">数组中的每个文档都有三个属性。</span><span class="sxs-lookup"><span data-stu-id="638e4-176">Each document in the array has three properties.</span></span> <span data-ttu-id="638e4-177">属性为 *"language"*、 *"id"* 和 *"text"*。</span><span class="sxs-lookup"><span data-stu-id="638e4-177">The properties are *"language"*, *"id"*, and *"text"*.</span></span> <span data-ttu-id="638e4-178">此示例中的 *"id"* 是一个数字, 但它可以是您想要的任何内容, 只要它在 documents 数组中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="638e4-178">The *"id"* is a number in this example, but it can be anything you want as long as it's unique in the documents array.</span></span> <span data-ttu-id="638e4-179">在此示例中, 我们还传递用三种不同语言编写的文档。</span><span class="sxs-lookup"><span data-stu-id="638e4-179">In this example, we're also passing in documents written in three different languages.</span></span> <span data-ttu-id="638e4-180">文本分析 API 的看法功能支持超过15种语言。</span><span class="sxs-lookup"><span data-stu-id="638e4-180">Over 15 languages are supported in the Sentiment feature of the Text Analytics API.</span></span> <span data-ttu-id="638e4-181">有关详细信息, 请参阅[Text Analytics API 中支持的语言](https://docs.microsoft.com//azure/cognitive-services/text-analytics/text-analytics-supported-languages)。</span><span class="sxs-lookup"><span data-stu-id="638e4-181">For more information, check out [Supported languages in the Text Analytics API](https://docs.microsoft.com//azure/cognitive-services/text-analytics/text-analytics-supported-languages).</span></span> <span data-ttu-id="638e4-182">单个文档的最大大小为5000个字符, 一个请求最多可以包含1000个文档。</span><span class="sxs-lookup"><span data-stu-id="638e4-182">The maximum size of a single document is 5,000 characters, and one request can have up to 1,000 documents.</span></span>

    !["请求正文" 部分的屏幕截图](../media/3-marker.PNG)

    <span data-ttu-id="638e4-184">包含标头和请求 URL 的完整请求将显示在下一节中。</span><span class="sxs-lookup"><span data-stu-id="638e4-184">The complete request, including the headers and the request URL are displayed in the next section.</span></span> <span data-ttu-id="638e4-185">在此示例中, 您可以看到请求被路由到以开头的 URL `westus`。</span><span class="sxs-lookup"><span data-stu-id="638e4-185">In this example, you can see that the requests are routed to a URL that begins with `westus`.</span></span> <span data-ttu-id="638e4-186">根据您在创建文本分析帐户时选择的位置, URL 会有所不同。</span><span class="sxs-lookup"><span data-stu-id="638e4-186">The URL differs depending on the location you selected when you created your Text Analytics account.</span></span>

    <span data-ttu-id="638e4-187">![显示请求 URL 的第四节的屏幕截图。](../media/4-marker.PNG)</span><span class="sxs-lookup"><span data-stu-id="638e4-187">![Screenshot of section number four showing the request URL.](../media/4-marker.PNG)</span></span>
    <span data-ttu-id="638e4-188">![第五部分的屏幕截图, 显示了详细的 HTTP 请求。](../media/5-marker.PNG)</span><span class="sxs-lookup"><span data-stu-id="638e4-188">![Screenshot of the section number five showing detailed HTTP request.](../media/5-marker.PNG)</span></span>

    <span data-ttu-id="638e4-189">然后, 我们提供有关响应的信息。</span><span class="sxs-lookup"><span data-stu-id="638e4-189">Then we have information about the response.</span></span> <span data-ttu-id="638e4-190">在此示例中, 我们发现请求成功, 并返回了代码`200` 。</span><span class="sxs-lookup"><span data-stu-id="638e4-190">In the example, we see that the request was a success and code `200` was returned.</span></span> <span data-ttu-id="638e4-191">此外, 我们还可以看到往返行程采用了38毫秒。</span><span class="sxs-lookup"><span data-stu-id="638e4-191">We can also see that the round trip took 38 ms.</span></span>

    ![第五部分显示响应状态的屏幕截图](../media/6-marker.PNG)

    <span data-ttu-id="638e4-193">最后, 我们会看到请求的响应。</span><span class="sxs-lookup"><span data-stu-id="638e4-193">Finally, we see the response to our request.</span></span> <span data-ttu-id="638e4-194">该响应包含文本分析 API 对我们的文档的洞察力。</span><span class="sxs-lookup"><span data-stu-id="638e4-194">The response holds the insight the Text Analytics API had about our documents.</span></span> <span data-ttu-id="638e4-195">在不使用原始文本的情况下, 将文档的数组返回给我们。</span><span class="sxs-lookup"><span data-stu-id="638e4-195">An array of documents is returned to us, without the original text.</span></span> <span data-ttu-id="638e4-196">我们获取每个文档的 *"id"* 和 *"得分"* 。</span><span class="sxs-lookup"><span data-stu-id="638e4-196">We get back an *"id"* and *"score"* for each document.</span></span> <span data-ttu-id="638e4-197">API 返回介于0和1之间的数值得分。</span><span class="sxs-lookup"><span data-stu-id="638e4-197">The API returns a numeric score between 0 and 1.</span></span> <span data-ttu-id="638e4-198">分数近1表示正看法, 而分数接近0表示负看法。</span><span class="sxs-lookup"><span data-stu-id="638e4-198">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="638e4-199">分数为0.5 表示缺少看法, 非特定语句。</span><span class="sxs-lookup"><span data-stu-id="638e4-199">A score of 0.5 indicates the lack of sentiment, a neutral statement.</span></span> <span data-ttu-id="638e4-200">在此示例中, 我们有两个非常积极的文档和一个负文档。</span><span class="sxs-lookup"><span data-stu-id="638e4-200">In this example, we have two pretty positive documents and one negative document.</span></span>

    ![显示响应内容的第五部分的屏幕截图。](../media/7-marker.PNG)

<span data-ttu-id="638e4-202">!!</span><span class="sxs-lookup"><span data-stu-id="638e4-202">Congratulations!</span></span> <span data-ttu-id="638e4-203">您已对文本分析 API 进行了第一次调用, 而无需编写代码行。</span><span class="sxs-lookup"><span data-stu-id="638e4-203">You've made your first call to the Text Analytics API without writing a line of code.</span></span> <span data-ttu-id="638e4-204">你可以随意保留在控制台中并尝试更多呼叫。</span><span class="sxs-lookup"><span data-stu-id="638e4-204">Feel free to stay in the console and try out more calls.</span></span> <span data-ttu-id="638e4-205">以下是一些建议:</span><span class="sxs-lookup"><span data-stu-id="638e4-205">Here are some suggestions:</span></span>

- <span data-ttu-id="638e4-206">更改第2部分中的文档, 并查看 API 返回的内容。</span><span class="sxs-lookup"><span data-stu-id="638e4-206">Change the documents in section number 2 and see what the API returns.</span></span>
- <span data-ttu-id="638e4-207">使用相同的订阅密钥尝试其他方法,**检测语言**、**实体**和**密钥短语**。</span><span class="sxs-lookup"><span data-stu-id="638e4-207">Try the other methods, **Detect Language**, **Entities**, and **Key Phrases**, using the same subscription key.</span></span>
- <span data-ttu-id="638e4-208">尝试使用与订阅的其他区域进行呼叫, 并观察发生的情况。</span><span class="sxs-lookup"><span data-stu-id="638e4-208">Try to make a call from a different region with your subscription and observe what happens.</span></span>

<span data-ttu-id="638e4-209">api 测试控制台是探索此 API 的功能的一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="638e4-209">The API testing console is a great way to explore the capabilities of this API.</span></span> <span data-ttu-id="638e4-210">现在, 你已对你进行了探索, 我们将继续将此智能放到现实世界的方案中。</span><span class="sxs-lookup"><span data-stu-id="638e4-210">Now that you've explored for yourself, let's move on to putting this intelligence into a real-world scenario.</span></span>