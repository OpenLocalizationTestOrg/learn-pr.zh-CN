<span data-ttu-id="e6674-101">Mojifier 是一个宽延时间 bot, 它会检测并将图像中的图符替换为与其情感相匹配的表情符号。</span><span class="sxs-lookup"><span data-stu-id="e6674-101">The Mojifier is a Slack bot which detects and then replaces faces in images with emojis  that match their emotion.</span></span> <span data-ttu-id="e6674-102">例如：</span><span class="sxs-lookup"><span data-stu-id="e6674-102">For example:</span></span>  

![示例 Mojified 脸。](../media/example-mojify-image.png)

<span data-ttu-id="e6674-105">它旨在作为自定义命令在可宽延时间中工作。</span><span class="sxs-lookup"><span data-stu-id="e6674-105">It's designed to work from Slack as a custom command.</span></span> <span data-ttu-id="e6674-106">虽然您可以将命令命名为您喜欢的命令, 但本模块将把`mojify`它称为。</span><span class="sxs-lookup"><span data-stu-id="e6674-106">While you can name the command what you like, this module will refer to it as `mojify`.</span></span> <span data-ttu-id="e6674-107">若要执行命令, 请`/mojify <image to mojify>`输入。</span><span class="sxs-lookup"><span data-stu-id="e6674-107">To execute the command, enter `/mojify <image to mojify>`.</span></span>

<span data-ttu-id="e6674-108">然后, Mojifier 将:</span><span class="sxs-lookup"><span data-stu-id="e6674-108">The Mojifier then will:</span></span>

  1. <span data-ttu-id="e6674-109">计算图像中任何人员的情感</span><span class="sxs-lookup"><span data-stu-id="e6674-109">Calculate the emotion of any people in the image</span></span>
  2. <span data-ttu-id="e6674-110">将感受与表情符号匹配</span><span class="sxs-lookup"><span data-stu-id="e6674-110">Match emotions to emojis</span></span>
  3. <span data-ttu-id="e6674-111">将图像中的面孔替换为表情符号</span><span class="sxs-lookup"><span data-stu-id="e6674-111">Replaces faces in the image with emojis</span></span>
  4. <span data-ttu-id="e6674-112">将更新后的图像作为答复投递到可宽延时间</span><span class="sxs-lookup"><span data-stu-id="e6674-112">Post the updated image to Slack as a reply</span></span>

<span data-ttu-id="e6674-113">这将导致新 mojified 图像显示在可宽延时间中, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="e6674-113">This should result in your newly mojified image appearing in Slack, like so:</span></span> 

![调用可宽延时间 Mojifier 应用将表情符号添加到 URL 上的图像。](../media/8.slack-type-mojify.png)

<span data-ttu-id="e6674-116">Mojifier 是使用 TypeScript、 [azure 函数](https://azure.microsoft.com/services/functions?azure-portal=true)和[azure 认知服务](https://azure.microsoft.com/services/cognitive-services?azure-portal=true)编写而成。</span><span class="sxs-lookup"><span data-stu-id="e6674-116">The Mojifier is written using TypeScript, [Azure Functions](https://azure.microsoft.com/services/functions?azure-portal=true) and [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services?azure-portal=true).</span></span> <span data-ttu-id="e6674-117">您可以使用这些程序制作自己的 Mojifier 版本。</span><span class="sxs-lookup"><span data-stu-id="e6674-117">You use these to make your own version of The Mojifier.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="e6674-118">学习目标</span><span class="sxs-lookup"><span data-stu-id="e6674-118">Learning objectives</span></span>

<span data-ttu-id="e6674-119">在本模块中, 您将:</span><span class="sxs-lookup"><span data-stu-id="e6674-119">In this module, you will:</span></span>

- <span data-ttu-id="e6674-120">对图像中任何人员的情感进行分类</span><span class="sxs-lookup"><span data-stu-id="e6674-120">Classify the emotion of any people in the image</span></span>
- <span data-ttu-id="e6674-121">将感受与表情符号匹配</span><span class="sxs-lookup"><span data-stu-id="e6674-121">Match emotions to emojis</span></span>
- <span data-ttu-id="e6674-122">将图像中的面孔替换为表情符号</span><span class="sxs-lookup"><span data-stu-id="e6674-122">Replaces faces in the image with emojis</span></span>
- <span data-ttu-id="e6674-123">将更新后的图像作为答复投递到可宽延时间</span><span class="sxs-lookup"><span data-stu-id="e6674-123">Post the updated image to Slack as a reply</span></span>

## <a name="tools-youll-use"></a><span data-ttu-id="e6674-124">您将使用的工具</span><span class="sxs-lookup"><span data-stu-id="e6674-124">Tools you'll use</span></span>

### <a name="azure-cognitive-services"></a><span data-ttu-id="e6674-125">Azure 认知服务</span><span class="sxs-lookup"><span data-stu-id="e6674-125">Azure Cognitive Services</span></span>

<span data-ttu-id="e6674-126">Azure 认知服务是一组高级 api, 可用于将高级人工智能 (AI) 功能快速添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="e6674-126">Azure Cognitive Services are a set of high-level APIs you can use to quickly add advanced artificial intelligence (AI) functionality into an app.</span></span> <span data-ttu-id="e6674-127">如果您知道如何发出 HTTP 请求, 那么您应该能够使用认知服务。</span><span class="sxs-lookup"><span data-stu-id="e6674-127">If you know how to make an HTTP request, then you should be able to use Cognitive Services.</span></span>

### <a name="azure-functions"></a><span data-ttu-id="e6674-128">Azure 函数</span><span class="sxs-lookup"><span data-stu-id="e6674-128">Azure Functions</span></span>

<span data-ttu-id="e6674-129">通过 Azure 函数, 可以托管可响应事件或 HTTP 请求的代码段。</span><span class="sxs-lookup"><span data-stu-id="e6674-129">Azure Functions lets you host code snippets that can respond to events or HTTP requests.</span></span> <span data-ttu-id="e6674-130">Azure 会自动处理缩放问题, 您只需付费即可使用。</span><span class="sxs-lookup"><span data-stu-id="e6674-130">Azure automatically handles scaling issues, and you only pay for what you use.</span></span> <span data-ttu-id="e6674-131">与 Microsoft 学习的任何内容一样, 我们都会在学习环境中向你介绍任何成本。</span><span class="sxs-lookup"><span data-stu-id="e6674-131">As with anything on Microsoft Learn, we'll cover any costs for you in the learning environment.</span></span>

> [!NOTE]
> <span data-ttu-id="e6674-132">[GitHub](https://github.com/MicrosoftDocs/mslearn-the-mojifier?azure-portal=true)上提供了 Mojifier 的所有代码。</span><span class="sxs-lookup"><span data-stu-id="e6674-132">All code for The Mojifier is available on [GitHub](https://github.com/MicrosoftDocs/mslearn-the-mojifier?azure-portal=true).</span></span>
