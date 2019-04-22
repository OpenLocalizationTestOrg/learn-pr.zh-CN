<span data-ttu-id="8f9ef-101">作为 Contoso 饮料分布的开发人员, 您负责构建和维护业务线应用程序, 让您的 frontline 分销商扫描和上传商店货位的图像以进行重新进货。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-101">As a lead developer at Contoso Beverage Distribution, you're responsible for building and maintaining a line-of-business app that lets your frontline distributors scan and upload images of store shelves where they are restocking.</span></span> 

<span data-ttu-id="8f9ef-102">您想要验证用户发布的任何图像是否遵循贵公司设置的内容规则。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-102">You want to validate that any images posted by users respect the content rules set by your company.</span></span> <span data-ttu-id="8f9ef-103">公司不希望将不良内容发布到公司网站。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-103">The company doesn't want inappropriate content posted to company sites.</span></span> <span data-ttu-id="8f9ef-104">鉴于人工智能中的进步, 你决定在应用中使用计算机远景 API。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-104">Given the advancements in Artificial Intelligence, you decide to use the Computer Vision API in your app.</span></span> 

<span data-ttu-id="8f9ef-105">若要开始, 请在 Azure 订阅中创建计算机远景帐户, 并开始测试 "**分析**" 功能。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-105">To get started, you create a Computer Vision account in your Azure subscription and start testing the **analyze** feature.</span></span>

## <a name="calling-the-computer-vision-api-to-analyze-images"></a><span data-ttu-id="8f9ef-106">调用计算机远景 API 以分析图像</span><span class="sxs-lookup"><span data-stu-id="8f9ef-106">Calling the Computer Vision API to analyze images</span></span>

<span data-ttu-id="8f9ef-107">该`analyze`操作将根据图像内容提取一组丰富的视觉功能。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-107">The `analyze` operation extracts a rich set of visual features based on the image content.</span></span> <span data-ttu-id="8f9ef-108">请求 URL 的格式如下:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-108">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=<...>&details=<...>&language=<...>`

<span data-ttu-id="8f9ef-109">发送到服务的参数为`visualFeatures`、 `details`和。 `languages`</span><span class="sxs-lookup"><span data-stu-id="8f9ef-109">The parameters that are sent to the service are `visualFeatures`, `details`, and `languages`.</span></span> <span data-ttu-id="8f9ef-110">将`details`参数设置为`Landmarks`或`Celebrities`可帮助您识别使或 celebrities。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-110">Set the `details` parameter to `Landmarks` or `Celebrities` to help you identify landmarks or celebrities.</span></span> <span data-ttu-id="8f9ef-111">`visualFeatures`确定您希望服务返回的信息类型。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-111">`visualFeatures` identify what kind of information you want the service to return you.</span></span> <span data-ttu-id="8f9ef-112">该`Categories`选项将对图像内容 (如树、建筑物等) 进行分类。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-112">The `Categories` option will categorize the content of the images like trees, buildings, and more.</span></span> <span data-ttu-id="8f9ef-113">`Faces`将识别人员的面孔并为你提供其性别和年龄。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-113">`Faces` will identify people's faces and give you their gender and age.</span></span>

<span data-ttu-id="8f9ef-114">当遇到计算机远景 API 上的所有操作时, 都将对您要求其处理的图像进行以下限制:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-114">All operations on the Computer Vision API have the following restrictions when it comes to the images you ask it to process:</span></span>

- <span data-ttu-id="8f9ef-115">支持的图像格式: JPEG、PNG、GIF、BMP。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-115">Supported image formats: JPEG, PNG, GIF, BMP.</span></span> 
- <span data-ttu-id="8f9ef-116">图像文件大小必须小于 4 MB。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-116">Image file size must be less than  4 MB.</span></span>
- <span data-ttu-id="8f9ef-117">图像尺寸必须至少为 50 x 50。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-117">Image dimensions must be at least 50 x 50.</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a><span data-ttu-id="8f9ef-118">确定图像中的使</span><span class="sxs-lookup"><span data-stu-id="8f9ef-118">Identify landmarks in an image</span></span>

<span data-ttu-id="8f9ef-119">让我们首先调用在图像中查找使。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-119">Let's start with a call to find landmarks in an image.</span></span> <span data-ttu-id="8f9ef-120">在此示例中, 我们将使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-120">We'll use the following image for this example, but you're free to try the same command with URLs to other images.</span></span> 

![在有 skies 的 mountains 上方具有蓝色的山地区间的图片。](../media/3-mountains.jpg)

<span data-ttu-id="8f9ef-122">在 Azure 云命令行管理程序中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-122">Execute the following command in Azure Cloud Shell.</span></span> <span data-ttu-id="8f9ef-123">将`<region>`命令中的替换为您的认知服务帐户所在的区域。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-123">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

- <span data-ttu-id="8f9ef-124">此调用在图像 URL 指定的图像中查找使。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-124">This call looks for landmarks in the image specified by the image URL.</span></span> <span data-ttu-id="8f9ef-125">我们正在分析的映像存储在此练习的 GitHub 存储库中。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-125">The image we are analyzing is stored in a GitHub repo for this exercise.</span></span> 
- <span data-ttu-id="8f9ef-126">该调用还会要求服务返回类别信息和图像说明。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-126">The call also asks the service to return category information and a description of the image.</span></span> <span data-ttu-id="8f9ef-127">该说明以完整的英文句子的形式返回。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-127">The description is returned as a complete English sentence.</span></span> 
- <span data-ttu-id="8f9ef-128">如你所知, 对 API 的每个调用都需要一个访问密钥。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-128">As you know, every call to the API needs an access key.</span></span> <span data-ttu-id="8f9ef-129">这是在请求的`Ocp-Apim-Subscription-Key`标头中设置的。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-129">This is set in the `Ocp-Apim-Subscription-Key` header of the request.</span></span> 

> [!TIP]
> <span data-ttu-id="8f9ef-130">请求的结果是原始 JSON, 描述中的图片`url`。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-130">The result of the request is the raw JSON describing the picture in the `url`.</span></span> <span data-ttu-id="8f9ef-131">我们在` | jq '.'`命令的末尾添加了 prettify JSON 输出。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-131">We added ` | jq '.'` at the end of the command to prettify the JSON output.</span></span>

<span data-ttu-id="8f9ef-132">此调用的 JSON 响应将返回以下内容:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-132">The JSON response from this call returns the following:</span></span>

- <span data-ttu-id="8f9ef-133">列出`categories`检测到的所有图像类别的数组, 以及介于0和1之间的分数, 表示该映像属于指定类别的服务的置信度。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-133">A `categories` array listing all image categories that were detected, along with a score between 0 and 1 of how confident the service is that the image belongs in the specified category.</span></span>
- <span data-ttu-id="8f9ef-134">包含`description`与图像相关的标记或词语的数组的条目。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-134">A `description` entry containing an array of tags or words that are related to the image.</span></span>
- <span data-ttu-id="8f9ef-135">带有`captions`文本字段的条目, 该字段以英语描述图像中的内容。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-135">A `captions` entry with a text field that describes in English what is in the image.</span></span> <span data-ttu-id="8f9ef-136">请注意, 文本也有确定性的分数。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-136">Observe that the text also has a certainty score.</span></span> <span data-ttu-id="8f9ef-137">此分数可帮助您通过此分析来决定下一步操作。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-137">This score can help you decide what to do next with this analysis.</span></span>


## <a name="check-for-inappropriate-content-in-an-image"></a><span data-ttu-id="8f9ef-138">检查图像中是否有不适当的内容</span><span class="sxs-lookup"><span data-stu-id="8f9ef-138">Check for inappropriate content in an image</span></span>

<span data-ttu-id="8f9ef-139">在此示例中, 我们将分析成人内容的图像。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-139">In this example, we'll analyze an image for adult content.</span></span> <span data-ttu-id="8f9ef-140">置信度分数表示图像包含成人或 racy 内容的可能性。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-140">The confidence score rates the likelihood that the image contains either adult or racy content.</span></span> 

<span data-ttu-id="8f9ef-141">在此示例中, 我们将使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-141">We'll use the following image for this example, but you're free to try the same command with URLs to other images.</span></span> 

![微笑的家庭的图片。](../media/3-people.png)

1. <span data-ttu-id="8f9ef-143">在 Azure 云命令行管理程序中执行以下`<region>`命令, 在 URL 中进行替换。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-143">Execute the following command in Azure Cloud Shell, replacing `<region>` in the URL.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

<span data-ttu-id="8f9ef-144">在此示例中, 我们将`visualFeatures`设置`Adult,Description`为。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-144">In this example, we set the `visualFeatures` to `Adult,Description`.</span></span> 

<span data-ttu-id="8f9ef-145">响应为我们提供了两个置信分数, 一个用于 racy 内容, 一个用于成人内容。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-145">The response gives us two confidence scores, one for racy content and one for adult content.</span></span> <span data-ttu-id="8f9ef-146">使用这些分数加上图像说明和其他可视功能, 您可以开始标记发送到服务器的图像。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-146">Using these scores plus the image description and other visual features, you can start to flag images posted to your server.</span></span>

<span data-ttu-id="8f9ef-147">本练习中我们尝试的示例为您提供了可使用该`analyze`操作执行的分析类型的概念。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-147">The examples we tried in this exercise give you an idea of the type of analysis that you can do with the `analyze` operation.</span></span> <span data-ttu-id="8f9ef-148">尝试使用不同的图像进行分析, 并尝试使用不同的 visualFeatures、details 和语言参数组合。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-148">Try out the analysis with different images and try different combinations of visualFeatures, details, and languages parameters.</span></span>

<span data-ttu-id="8f9ef-149">有关此`analyze`操作的详细信息, 请参阅[分析图像](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa)参考文档。</span><span class="sxs-lookup"><span data-stu-id="8f9ef-149">For more information about the `analyze` operation, see the [Analyze Image](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) reference documentation.</span></span>