<span data-ttu-id="cf65c-101">我们看到了计算机远景 API 如何从图像中提取打印出来的文本。</span><span class="sxs-lookup"><span data-stu-id="cf65c-101">We saw how the Computer Vision API can extract printed text from images.</span></span> <span data-ttu-id="cf65c-102">在本练习中, 我们将使用该服务来检测手写文本。</span><span class="sxs-lookup"><span data-stu-id="cf65c-102">In this exercise, we'll use the service to detect handwritten text.</span></span>

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a><span data-ttu-id="cf65c-103">调用计算机远景 API 以提取手写文本</span><span class="sxs-lookup"><span data-stu-id="cf65c-103">Calling the Computer Vision API to extract handwritten text</span></span>

<span data-ttu-id="cf65c-104">该`recognizeText`操作检测并提取来自注释、字母、essays、白板、窗体和其他源的手写文本。</span><span class="sxs-lookup"><span data-stu-id="cf65c-104">The `recognizeText` operation detects and extracts handwritten text from notes, letters, essays, whiteboards, forms, and other sources.</span></span> <span data-ttu-id="cf65c-105">请求 URL 的格式如下:</span><span class="sxs-lookup"><span data-stu-id="cf65c-105">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=<...>`

<span data-ttu-id="cf65c-106">必须对创建帐户的区域进行所有呼叫。</span><span class="sxs-lookup"><span data-stu-id="cf65c-106">All calls must be made to the region where the account was created.</span></span>

<span data-ttu-id="cf65c-107">如果存在此参数`mode` , 则必须将该`Handwritten`参数`Printed`设置为或且区分大小写。</span><span class="sxs-lookup"><span data-stu-id="cf65c-107">If present, the `mode` parameter must be set to `Handwritten` or `Printed` and is case-sensitive.</span></span> <span data-ttu-id="cf65c-108">如果此参数设置为`Handwritten`或未指定, 则执行手写识别。</span><span class="sxs-lookup"><span data-stu-id="cf65c-108">If the parameter is set to `Handwritten` or is not specified, handwriting recognition is performed.</span></span> <span data-ttu-id="cf65c-109">如果将参数设置为`Printed`, 则执行打印的文本识别。</span><span class="sxs-lookup"><span data-stu-id="cf65c-109">If the parameter is set to `Printed`, then printed text recognition is performed.</span></span> <span data-ttu-id="cf65c-110">从此调用获取结果所需的时间取决于图像中的书写量。</span><span class="sxs-lookup"><span data-stu-id="cf65c-110">The time it takes to get a result from this call depends on the amount of writing in the image.</span></span>

<span data-ttu-id="cf65c-111">在此示例中, 我们将:</span><span class="sxs-lookup"><span data-stu-id="cf65c-111">In this example, we'll:</span></span>

- <span data-ttu-id="cf65c-112">使用卷曲的`-D`选项将响应标头打印到控制台</span><span class="sxs-lookup"><span data-stu-id="cf65c-112">Print the response headers to the console using cUrl's `-D` option</span></span>
- <span data-ttu-id="cf65c-113">复制我们`Operation-Location`在响应中收到的标头中的标头值</span><span class="sxs-lookup"><span data-stu-id="cf65c-113">Copy the `Operation-Location` header value from the headers we receive in the response</span></span>
- <span data-ttu-id="cf65c-114">几秒钟后, 请检查针对结果指定的`Operation-Location` URL。</span><span class="sxs-lookup"><span data-stu-id="cf65c-114">After a few seconds, check the URL specified by the `Operation-Location` for the results</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a><span data-ttu-id="cf65c-115">检测并从图像中提取手写文本</span><span class="sxs-lookup"><span data-stu-id="cf65c-115">Detect and extract handwritten text from an image</span></span>

<span data-ttu-id="cf65c-116">我们将在此示例中使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。</span><span class="sxs-lookup"><span data-stu-id="cf65c-116">We'll use the following image in this example, but you're free to try the same command with URLs to other images.</span></span>

![备注上的手写示例的图片](../media/6-handwriting.jpg)

1. <span data-ttu-id="cf65c-118">在 Azure 云命令行管理程序中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="cf65c-118">Execute the following commands in Azure Cloud Shell.</span></span> <span data-ttu-id="cf65c-119">将`<region>`命令中的替换为您的认知服务帐户所在的区域。</span><span class="sxs-lookup"><span data-stu-id="cf65c-119">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

<span data-ttu-id="cf65c-120">上面将此操作的标头转储到控制台。</span><span class="sxs-lookup"><span data-stu-id="cf65c-120">The above dumps the headers of this operation to the console.</span></span> <span data-ttu-id="cf65c-121">下面是一个示例:</span><span class="sxs-lookup"><span data-stu-id="cf65c-121">Here's an example:</span></span>

```azurecli
HTTP/1.1 202 Accepted
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Expires: -1
Operation-Location: https://westus2.api.cognitive.microsoft.com/vision/v2.0/textOperations/d0e9b397-4072-471c-ae61-7490bec8f077
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
apim-request-id: f5663487-03c6-4760-9be7-c9157fac10a1
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
x-content-type-options: nosniff
Date: Wed, 12 Sep 2018 19:22:00 GMT
```

<span data-ttu-id="cf65c-122">`Operation-Location`标头是在完成后将发布结果的位置。</span><span class="sxs-lookup"><span data-stu-id="cf65c-122">The `Operation-Location` header is where the results will be posted once complete.</span></span>

2. <span data-ttu-id="cf65c-123">复制`Operation-Location`标头值。</span><span class="sxs-lookup"><span data-stu-id="cf65c-123">Copy the `Operation-Location` header value.</span></span>
1. <span data-ttu-id="cf65c-124">在 Azure 云命令行管理程序中执行`"<Operation-Location>"`以下命令, 将替换为您在上一步中复制的**操作位置**标头的值。</span><span class="sxs-lookup"><span data-stu-id="cf65c-124">Execute the following command in Azure Cloud Shell replacing `"<Operation-Location>"` with the value for the **Operation-Location** header you copied from the preceding step.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

<span data-ttu-id="cf65c-125">如果操作已完成, 则会收到包含手写识别请求结果的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="cf65c-125">If the operation has completed, you'll receive a JSON file containing the result of the handwriting recognition request.</span></span>

<span data-ttu-id="cf65c-126">有关此`recognizeText`操作的详细信息, 请参阅[识别手写文本](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200)参考文档。</span><span class="sxs-lookup"><span data-stu-id="cf65c-126">For more information about the `recognizeText` operation, see the [Recognize Handwritten Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) reference documentation.</span></span>