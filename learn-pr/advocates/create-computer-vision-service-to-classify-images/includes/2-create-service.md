
## <a name="what-is-microsoft-cognitive-services"></a><span data-ttu-id="4b5b6-101">什么是 Microsoft 认知服务？</span><span class="sxs-lookup"><span data-stu-id="4b5b6-101">What is Microsoft Cognitive Services?</span></span>

<span data-ttu-id="4b5b6-102">Microsoft 认知服务是一组可用作任何用户使用的服务的机器学习算法。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-102">Microsoft Cognitive Services is a set of machine learning algorithms available as a service for anyone to use.</span></span> <span data-ttu-id="4b5b6-103">我们可以使用这些服务进行远景、语音、语言、知识和搜索, 而无需从头开始为我们的应用构建此智能。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-103">Instead of building this intelligence for our apps from scratch, we can use these services for vision, speech, language, knowledge, and search.</span></span> <span data-ttu-id="4b5b6-104">你可以免费试用每个服务。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-104">You can try each service for free.</span></span> <span data-ttu-id="4b5b6-105">在决定将服务集成到您的应用程序时, 请注册付费订阅。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-105">When you decide to integrate a service into your app, you sign up for a paid subscription.</span></span> <span data-ttu-id="4b5b6-106">我们将重点关注此模型中的计算机远景 API。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-106">We'll focus our attention on the Computer Vision API in this model.</span></span>

> [!TIP]
> <span data-ttu-id="4b5b6-107">若要查看所有认知服务的列表, 请查看[认知服务目录](https://azure.microsoft.com/services/cognitive-services/directory/)。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-107">To see a list of all Cognitive Services, check out the [Cognitive Services Directory](https://azure.microsoft.com/services/cognitive-services/directory/).</span></span> 

## <a name="what-is-the-computer-vision-api"></a><span data-ttu-id="4b5b6-108">什么是计算机远景 API？</span><span class="sxs-lookup"><span data-stu-id="4b5b6-108">What is the Computer Vision API?</span></span>

<span data-ttu-id="4b5b6-109">计算机远景 API 提供用于处理图像和返回见解的算法。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-109">The Computer Vision API provides algorithms to process images and return insights.</span></span> <span data-ttu-id="4b5b6-110">例如, 您可以找出某个图像是否包含成人内容, 或能否使用它来查找图像中的所有表面。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-110">For example, you can find out if an image has mature content, or can use it to find all the faces in an image.</span></span> <span data-ttu-id="4b5b6-111">它还具有其他功能, 如估计主要和强调颜色、使用完整的英文句子对图像内容进行分类以及描述图像。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-111">It also has other features like estimating dominant and accent colors, categorizing the content of images, and describing an image with complete English sentences.</span></span> <span data-ttu-id="4b5b6-112">此外, 它还可以智能地生成图像缩略图, 以有效显示大图像。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-112">Additionally, it can also intelligently generate images thumbnails for displaying large images effectively.</span></span>

> [!TIP]
> <span data-ttu-id="4b5b6-113">计算机远景 API 在全球范围内提供了许多区域。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-113">The Computer Vision API is available in many regions across the globe.</span></span> <span data-ttu-id="4b5b6-114">若要查找离你最近的地区, 请参阅[按地区提供的产品](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all)。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-114">To find the region nearest you, see the [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all).</span></span>

<span data-ttu-id="4b5b6-115">您可以使用计算机远景 API 执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="4b5b6-115">You can use the Computer Vision API to:</span></span>

- <span data-ttu-id="4b5b6-116">分析图像的洞察力</span><span class="sxs-lookup"><span data-stu-id="4b5b6-116">Analyze images for insight</span></span>
- <span data-ttu-id="4b5b6-117">使用光学字符识别 (OCR) 从图像中提取打印的文本。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-117">Extract printed text from images using optical character recognition (OCR).</span></span>
- <span data-ttu-id="4b5b6-118">从图像中识别打印的和手写的文本</span><span class="sxs-lookup"><span data-stu-id="4b5b6-118">Recognize printed and handwritten text from images</span></span>
- <span data-ttu-id="4b5b6-119">识别 celebrities 和使</span><span class="sxs-lookup"><span data-stu-id="4b5b6-119">Recognize celebrities and landmarks</span></span>
- <span data-ttu-id="4b5b6-120">分析视频</span><span class="sxs-lookup"><span data-stu-id="4b5b6-120">Analyze video</span></span> 
- <span data-ttu-id="4b5b6-121">生成图像的缩略图</span><span class="sxs-lookup"><span data-stu-id="4b5b6-121">Generate a thumbnail of an image</span></span> 

## <a name="how-to-call-the-computer-vision-api"></a><span data-ttu-id="4b5b6-122">如何调用计算机远景 API</span><span class="sxs-lookup"><span data-stu-id="4b5b6-122">How to call the Computer Vision API</span></span>

<span data-ttu-id="4b5b6-123">您可以使用客户端库或 REST API 直接调用应用程序中的计算机远景。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-123">You call Computer Vision in your application using client libraries or the REST API directly.</span></span> <span data-ttu-id="4b5b6-124">我们将在此模块中调用 REST API。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-124">We'll call the REST API in this module.</span></span> <span data-ttu-id="4b5b6-125">拨打电话:</span><span class="sxs-lookup"><span data-stu-id="4b5b6-125">To make a call:</span></span>

1. <span data-ttu-id="4b5b6-126">获取 API 访问密钥</span><span class="sxs-lookup"><span data-stu-id="4b5b6-126">Get an API access key</span></span>

    <span data-ttu-id="4b5b6-127">注册计算机远景服务帐户时, 系统会向你分配访问密钥。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-127">You are assigned access keys when you sign up for a Computer Vision service account.</span></span> <span data-ttu-id="4b5b6-128">必须在**每个**请求的标头中传递一个键。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-128">A key must be passed in the header of **every** request.</span></span> 

1. <span data-ttu-id="4b5b6-129">向 API 发出 POST 调用</span><span class="sxs-lookup"><span data-stu-id="4b5b6-129">Make a POST call to the API</span></span>

    <span data-ttu-id="4b5b6-130">设置 URL 格式, 如下所\*\*\*\* 示: api.cognitive.microsoft.com/vision/v2.0/**资源**/**[parameters]**</span><span class="sxs-lookup"><span data-stu-id="4b5b6-130">Format the URL as follows: **region**.api.cognitive.microsoft.com/vision/v2.0/**resource**/**[parameters]**</span></span> 

    - <span data-ttu-id="4b5b6-131">**region** -您在其中创建帐户的区域, 例如, *westus*。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-131">**region** - the region where you created the account, for example, *westus*.</span></span>
    - <span data-ttu-id="4b5b6-132">**resource** -你正在呼叫的计算机远景资源`analyze`, `describe` `generateThumbnail` `ocr` `models`如、、、、、 `recognizeText`、 `tag`。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-132">**resource** - the Computer Vision resource you are calling such as `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText`, `tag`.</span></span>

    <span data-ttu-id="4b5b6-133">您可以提供要作为原始图像二进制文件或图像 URL 处理的图像。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-133">You can supply the image to be processed either as a raw image binary or an image URL.</span></span>

    <span data-ttu-id="4b5b6-134">请求标头必须包含订阅密钥, 该密钥提供对此 API 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-134">The request header must contain the subscription key, which provides access to this API.</span></span>

1. <span data-ttu-id="4b5b6-135">分析响应</span><span class="sxs-lookup"><span data-stu-id="4b5b6-135">Parse the response</span></span>

    <span data-ttu-id="4b5b6-136">该响应包含计算机远景 API 对你的图像的见解, 作为 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-136">The response holds the insight the Computer Vision API has about your image, as a JSON payload.</span></span>

<span data-ttu-id="4b5b6-137">在本模块中, 我们将使用集成云命令行管理程序运行 Azure CLI 中的所有练习。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-137">In this module, we'll run all exercises in the Azure CLI using the integrated Cloud Shell.</span></span> <span data-ttu-id="4b5b6-138">让我们进一步了解一下此设置。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-138">Let's find out a little more about this setup.</span></span>

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="4b5b6-139">什么是 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4b5b6-139">What is the Azure CLI</span></span>

<span data-ttu-id="4b5b6-140">azure CLI 是 Microsoft 的用于管理 Azure 资源的跨平台命令行工具。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-140">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="4b5b6-141">它可用于 macOS、Linux 和 Windows, 也可用于使用[Azure 云命令行](https://docs.microsoft.com/azure/cloud-shell/overview)管理程序的浏览器。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-141">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b5b6-142">有两个版本的 azure cli 工具现已推出: azure cli 1.0 和 Azure cli 2.0。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-142">There are two versions of the Azure CLI tool available today: Azure CLI 1.0 and Azure CLI 2.0.</span></span> <span data-ttu-id="4b5b6-143">我们将使用 Azure CLI 2.0, 它是最新版本, 建议使用, 除非您运行的是旧版脚本。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-143">We'll be using Azure CLI 2.0, which is the latest version and is recommended unless you're running legacy scripts.</span></span> <span data-ttu-id="4b5b6-144">azure cli 1.0 是通过`azure`命令启动的, 并且使用`az`命令启动 azure cli 2.0。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-144">Azure CLI 1.0 is started with the `azure` command, and Azure CLI 2.0 is started with the `az` command.</span></span>

## <a name="az-cognitiveservices-commands"></a><span data-ttu-id="4b5b6-145">az cognitiveservices 命令</span><span class="sxs-lookup"><span data-stu-id="4b5b6-145">az cognitiveservices commands</span></span>

<span data-ttu-id="4b5b6-146">azure CLI 包含用于管理`cognitiveservices` Azure 中的认知服务帐户的命令。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-146">The Azure CLI includes the `cognitiveservices` command to manage Cognitive Services accounts in Azure.</span></span> <span data-ttu-id="4b5b6-147">我们可以提供几个子命令来完成特定任务。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-147">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="4b5b6-148">最常见的包括:</span><span class="sxs-lookup"><span data-stu-id="4b5b6-148">The most common include:</span></span>

| <span data-ttu-id="4b5b6-149">子命令</span><span class="sxs-lookup"><span data-stu-id="4b5b6-149">Subcommand</span></span> | <span data-ttu-id="4b5b6-150">说明</span><span class="sxs-lookup"><span data-stu-id="4b5b6-150">Description</span></span> |
|-------------|-------------|
| `list` | <span data-ttu-id="4b5b6-151">列出可用的 Azure 认知服务帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-151">List available Azure Cognitive Services accounts.</span></span> |
| `account show` | <span data-ttu-id="4b5b6-152">获取 Azure 认知服务帐户的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-152">Get the details of an Azure Cognitive Services account.</span></span> |
| `account create` | <span data-ttu-id="4b5b6-153">创建 Azure 认知服务帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-153">Create an Azure Cognitive Services account.</span></span> |
| `account delete` | <span data-ttu-id="4b5b6-154">删除 Azure 认知服务帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-154">Delete an Azure Cognitive Services account.</span></span> |
| `keys list` | <span data-ttu-id="4b5b6-155">列出 Azure 认知服务帐户的密钥。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-155">List the keys of an Azure Cognitive Services account.</span></span> |

<span data-ttu-id="4b5b6-156">让我们在 Azure CLI 中创建一个认知服务。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-156">Let's create a Cognitive Services with the Azure CLI.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="4b5b6-157">创建认知服务帐户</span><span class="sxs-lookup"><span data-stu-id="4b5b6-157">Create a Cognitive Services account</span></span>

<span data-ttu-id="4b5b6-158">我们需要一个 API 访问密钥来调用计算机远景 API。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-158">We need an API access key to make calls to the Computer Vision API.</span></span> <span data-ttu-id="4b5b6-159">若要获取访问密钥, 我们需要一个适用于计算机远景 API 的认知服务帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-159">To get access keys, we need a Cognitive Services account for the Computer Vision API.</span></span> <span data-ttu-id="4b5b6-160">我们将使用`az cognitiveservices create`在订阅中创建帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-160">We'll use `az cognitiveservices create` to create the account in our subscription.</span></span>

 <span data-ttu-id="4b5b6-161">该命令`az cognitiveservices create`用于在资源组中创建认知服务帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-161">The command `az cognitiveservices create` is used to create a Cognitive Services account in a resource group.</span></span>  <span data-ttu-id="4b5b6-162">调用此命令时, 必须提供以下五个参数。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-162">The following five parameters must be supplied when calling this command.</span></span>

> [!Tip]
> <span data-ttu-id="4b5b6-163">大多数 Azure CLI 参数的标志都可以缩写为单个字符。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-163">Most flags for Azure CLI parameters can be abbreviated to a single character.</span></span> <span data-ttu-id="4b5b6-164">例如, 我们可以说`-l` , 而不`--location`是。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-164">For example, we could say `-l` instead of `--location`.</span></span> <span data-ttu-id="4b5b6-165">为清楚起见, 使用长格式。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-165">The long-form is used for clarity.</span></span>

| <span data-ttu-id="4b5b6-166">参数</span><span class="sxs-lookup"><span data-stu-id="4b5b6-166">Parameter</span></span> | <span data-ttu-id="4b5b6-167">说明</span><span class="sxs-lookup"><span data-stu-id="4b5b6-167">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="4b5b6-168">将拥有认知服务帐户的资源组。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-168">The resource group that will own the cognitive services account.</span></span> <span data-ttu-id="4b5b6-169">在此交互式沙盒会话中, 将使用<rgn>[沙盒资源组名称]</rgn></span><span class="sxs-lookup"><span data-stu-id="4b5b6-169">In this interactive sandbox session, you'll use <rgn>[sandbox resource group name]</rgn></span></span> |
| `kind` | <span data-ttu-id="4b5b6-170">认知服务帐户的 API 名称。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-170">The API name of cognitive services account.</span></span> <span data-ttu-id="4b5b6-171">对于此练习计算机愿景, 但可以基于内容审阅者、面对面 API 等。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-171">For this exercise Computer Vision, but can be based on Content Moderator, Face API, etc.</span></span>|
| `name` | <span data-ttu-id="4b5b6-172">认知服务帐户名称。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-172">Cognitive service account name.</span></span> |
| `sku` | <span data-ttu-id="4b5b6-173">认知服务帐户的 Sku (库存单位)。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-173">The Sku (Stock Keeping Unit) of cognitive services account.</span></span> <span data-ttu-id="4b5b6-174">在此练习 S1 中, 但可以是 F0 (free 层)、S1、S2、S3 或 S4。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-174">For this exercise S1, but can be F0 (free tier), S1, S2, S3, or S4.</span></span> |
| `location` | <span data-ttu-id="4b5b6-175">要从中调用此 API 的位置或区域。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-175">The location, or region, from which you want to make calls to this API.</span></span> <span data-ttu-id="4b5b6-176">从以下列表中选择一个位置。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-176">Select one of the locations from the list below.</span></span> |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

<span data-ttu-id="4b5b6-177">在 Azure 云命令行管理程序中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-177">Execute the following command in Azure Cloud Shell.</span></span> <span data-ttu-id="4b5b6-178">请务必将替换`[location]`为你附近的位置。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-178">Make sure to replace `[location]` with a location near you.</span></span>

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--name ComputerVisionService \
--sku S1 \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--location [location]
```

> [!NOTE]
> <span data-ttu-id="4b5b6-179">记住您选择的位置。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-179">Remember the location you have selected.</span></span> <span data-ttu-id="4b5b6-180">你将从该区域对 API 进行所有调用。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-180">You'll make all calls to the API from that region.</span></span>

<span data-ttu-id="4b5b6-181">我们为**ComputerVision** API 创建了一个认知服务帐户。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-181">We've created a cognitive services account for the **ComputerVision** API.</span></span> <span data-ttu-id="4b5b6-182">我们选择了*S1* sku 并命名为 "我们的帐户**ComputerVisionService**"。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-182">We selected the *S1* sku and named our account **ComputerVisionService**.</span></span> <span data-ttu-id="4b5b6-183">我们的帐户归资源组**<rgn>[沙盒资源组名称]</rgn>** 所有, 我们将从在`--location`参数中设置的位置调用 API。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-183">Our account is owned by the resource group **<rgn>[sandbox resource group name]</rgn>** and we'll call the API from the location we set in the `--location` parameter.</span></span> 

<span data-ttu-id="4b5b6-184">命令完成创建认知服务帐户后, 您将获得 JSON 响应, 其中包括设置为 "**成功**" 的**provisioningState**属性。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-184">Once the command finishes creating the cognitive services account, you'll get a JSON response, which includes **provisioningState** property set to **Succeeded**.</span></span>

## <a name="get-an-access-key"></a><span data-ttu-id="4b5b6-185">获取访问键</span><span class="sxs-lookup"><span data-stu-id="4b5b6-185">Get an access key</span></span>

<span data-ttu-id="4b5b6-186">成功创建帐户后, 我们可以为此帐户检索订阅密钥或访问密钥。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-186">Once we have our account successfully created we can retrieve the subscription keys, or access keys, for this account.</span></span>

1. <span data-ttu-id="4b5b6-187">在 Azure 云命令行管理程序中执行以下命令:</span><span class="sxs-lookup"><span data-stu-id="4b5b6-187">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn>
    ```
    
    <span data-ttu-id="4b5b6-188">上面的命令返回与认知服务帐户 (名为**ComputerVisionService**) 相关联的键, 该帐户归给定资源组所有。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-188">The above command returns the keys associated with the cognitive services account called **ComputerVisionService**, which is owned by the given resource group.</span></span> <span data-ttu-id="4b5b6-189">它返回两个键: 一个是备用密钥。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-189">It returns two keys - one is a spare key.</span></span> <span data-ttu-id="4b5b6-190">这些项很难记住, 因此我们将把第一个关键字存储在一个变量中, 我们将使用此变量对 API 的所有调用。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-190">The keys are difficult to remember, so we'll store the first key in a variable that we'll use for all calls to the API.</span></span>

2.  <span data-ttu-id="4b5b6-191">在 Azure 云命令行管理程序中执行以下命令:</span><span class="sxs-lookup"><span data-stu-id="4b5b6-191">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    key=$(az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query key1 -o tsv)
    ```
    
    <span data-ttu-id="4b5b6-192">Azure CLI 2.0 使用`--query`参数对命令结果执行 JMESPath 查询。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-192">The Azure CLI 2.0 uses the `--query` argument to execute a JMESPath query on the results of commands.</span></span> <span data-ttu-id="4b5b6-193">JMESPath 是 JSON 的查询语言, 使您能够从 CLI 输出中选择和呈现数据。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-193">JMESPath is a query language for JSON, giving you the ability to select and present data from CLI output.</span></span> <span data-ttu-id="4b5b6-194">这些查询在 JSON 输出上对任何显示格式执行。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-194">These queries are executed on the JSON output before any display formatting.</span></span>
    <span data-ttu-id="4b5b6-195">Azure `--query` CLI 中的所有命令都支持该参数。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-195">The `--query` argument is supported by all commands in the Azure CLI.</span></span> 
    
    <span data-ttu-id="4b5b6-196">在我们的示例中, 我们将查询名为 "key1" 的项的键列表, 并将结果输出到**tsv**格式。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-196">In our example, we query the list of keys for an entry named "key1" and output the result to **tsv** format.</span></span> <span data-ttu-id="4b5b6-197">此格式将删除字符串值周围的引号。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-197">This format removes quotations around the string value.</span></span> <span data-ttu-id="4b5b6-198">我们将结果分配给一个变量**键**。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-198">We assign the result to a variable **key**.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="4b5b6-199">我们打算在整个模块中使用此项, 因此最好将其保存在变量中。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-199">We're going to use this key throughout the module, so saving it in a variable is a good idea.</span></span> <span data-ttu-id="4b5b6-200">如果丢失了值或变量变为未设置, 则再次运行该命令以进行设置。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-200">If you lose the value or the variable becomes unset, run the command again to set it.</span></span>  

3. <span data-ttu-id="4b5b6-201">若要查看我们的键的值, 请在 Azure 云命令行管理程序中执行以下命令:</span><span class="sxs-lookup"><span data-stu-id="4b5b6-201">To see the value of our key, execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    echo $key
    ```

<span data-ttu-id="4b5b6-202">现在我们已拥有帐户和密钥, 接下来是要对 API 进行一些调用。</span><span class="sxs-lookup"><span data-stu-id="4b5b6-202">Now that we have an account and a key, it's time to make some calls to the API.</span></span>