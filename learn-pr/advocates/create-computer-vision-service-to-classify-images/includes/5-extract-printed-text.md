<span data-ttu-id="7150f-101">假设您现在想要阅读 frontline 分发服务器发布到您的服务器的股票图像中的文本。</span><span class="sxs-lookup"><span data-stu-id="7150f-101">Suppose you now want to read text from the stock images that your frontline distributors post to your server.</span></span> <span data-ttu-id="7150f-102">特别是, 您想要扫描产品, 查找包含销售价的促销不干胶标签。</span><span class="sxs-lookup"><span data-stu-id="7150f-102">In particular, you want to scan product looking for promotional stickers that containing sale prices.</span></span> <span data-ttu-id="7150f-103">现在是时候尝试计算机远景 API 的光学字符识别 (OCR) 功能。</span><span class="sxs-lookup"><span data-stu-id="7150f-103">It's time to try the optical character recognition (OCR) feature of the Computer Vision API.</span></span> 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a><span data-ttu-id="7150f-104">调用计算机远景 API 以提取打印文本</span><span class="sxs-lookup"><span data-stu-id="7150f-104">Calling the Computer Vision API to extract printed text</span></span>

<span data-ttu-id="7150f-105">该`ocr`操作检测图像中的文本, 并将识别的字符提取到计算机可用的字符流中。</span><span class="sxs-lookup"><span data-stu-id="7150f-105">The `ocr` operation detects text in an image and extracts the recognized characters into a machine-usable character stream.</span></span> <span data-ttu-id="7150f-106">请求 URL 的格式如下:</span><span class="sxs-lookup"><span data-stu-id="7150f-106">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr?language=<...>&detectOrientation=<...>`

<span data-ttu-id="7150f-107">与往常一样, 必须对创建帐户的区域进行所有呼叫。</span><span class="sxs-lookup"><span data-stu-id="7150f-107">As usual, all calls must be made to the region where the account was created.</span></span> <span data-ttu-id="7150f-108">该调用接受两个可选参数:</span><span class="sxs-lookup"><span data-stu-id="7150f-108">The call accepts two optional parameters:</span></span>

- <span data-ttu-id="7150f-109">**语言**: 要在图像中检测到的文本的语言代码。</span><span class="sxs-lookup"><span data-stu-id="7150f-109">**language**: The language code of the text to be detected in the image.</span></span> <span data-ttu-id="7150f-110">默认值为`unk`或未知。</span><span class="sxs-lookup"><span data-stu-id="7150f-110">The default value is `unk`,or unknown.</span></span> <span data-ttu-id="7150f-111">这让我们的服务自动检测图像中文本的语言。</span><span class="sxs-lookup"><span data-stu-id="7150f-111">This let's the service auto detect the language of the text in the image.</span></span>
- <span data-ttu-id="7150f-112">**detectOrientation**: 如果为 true, 服务将尝试检测图像方向并在进一步处理前对其进行更正, 例如, 是否颠倒了图像。</span><span class="sxs-lookup"><span data-stu-id="7150f-112">**detectOrientation**: When true, the service  tries to detect the image orientation and correct it before further processing, for example, whether the image is upside-down.</span></span> 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a><span data-ttu-id="7150f-113">使用 OCR 从图像中提取打印的文本</span><span class="sxs-lookup"><span data-stu-id="7150f-113">Extract printed text from an image using OCR</span></span>

<span data-ttu-id="7150f-114">我们要使用的图像是光学字符识别 (OCR) 的封面。 *.net Microservices: 体系结构适用于容器的 .net 应用程序*。</span><span class="sxs-lookup"><span data-stu-id="7150f-114">The image we're going to be using for Optical Character Recognition (OCR) is the cover from the book *.NET Microservices: Architecture for Containerized .NET Applications*.</span></span>

![电子书 .net Microservices 的封面的图片: 容器的 .net 应用程序的体系结构](../media/5-ebook.png)

1. <span data-ttu-id="7150f-116">在云命令行管理程序中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="7150f-116">Execute the following command in Cloud Shell.</span></span> <span data-ttu-id="7150f-117">将`<region>`命令中的替换为您的认知服务帐户所在的区域。</span><span class="sxs-lookup"><span data-stu-id="7150f-117">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

<span data-ttu-id="7150f-118">下面的 JSON 是我们从此调用获取的响应的示例。</span><span class="sxs-lookup"><span data-stu-id="7150f-118">The following JSON is an example of the response we get from this call.</span></span> <span data-ttu-id="7150f-119">已删除一些 JSON 行, 以使代码段更适合页面。</span><span class="sxs-lookup"><span data-stu-id="7150f-119">Some lines of JSON have been removed to make the snippet fit better on the page.</span></span>

```json
{
  "language": "en",
  "orientation": "Up",
  "textAngle": 0,
  "regions" : [
        /*... snipped*/
        {
          "boundingBox": "766,1419,302,33",
          "words": [
            {
              "boundingBox": "766,1419,126,25",
              "text": "Microsoft"
            },
            {
              "boundingBox": "903,1420,165,32",
              "text": "Corporation"
            }
          ]
        }]
}
```

<span data-ttu-id="7150f-120">让我们更详细地查看此响应。</span><span class="sxs-lookup"><span data-stu-id="7150f-120">Let's examine this response in more detail.</span></span> 

- <span data-ttu-id="7150f-121">服务将文本识别为英语。</span><span class="sxs-lookup"><span data-stu-id="7150f-121">The service identified the text as being English.</span></span> <span data-ttu-id="7150f-122">`language`字段的值包含图像中检测到的文本的 BCP-47 语言代码。</span><span class="sxs-lookup"><span data-stu-id="7150f-122">The value of the `language` field contains the BCP-47 language code of the text detected in the image.</span></span> <span data-ttu-id="7150f-123">在此示例中, 它是**en**或英语。</span><span class="sxs-lookup"><span data-stu-id="7150f-123">In this example it is **en**, or English.</span></span> 
- <span data-ttu-id="7150f-124">检测`orientation`为 " **up**"。</span><span class="sxs-lookup"><span data-stu-id="7150f-124">The `orientation` was detected as **up**.</span></span> <span data-ttu-id="7150f-125">此属性是在图像根据检测到的文本角度围绕其中心旋转后, 识别的文本的顶部方向。</span><span class="sxs-lookup"><span data-stu-id="7150f-125">This property is the direction that the top of the recognized text is facing, after the image has been rotated around its center according to the detected text angle.</span></span> 
- <span data-ttu-id="7150f-126">`textAngle`是要使文本变为水平方向或垂直方向而必须旋转的角度。</span><span class="sxs-lookup"><span data-stu-id="7150f-126">The `textAngle` is the angle by which the text must be rotated to become horizontal or vertical.</span></span> <span data-ttu-id="7150f-127">在此示例中, 文本是绝对水平的, 因此返回的值为**0**。</span><span class="sxs-lookup"><span data-stu-id="7150f-127">In this example, the text was perfectly horizontal, so the value returned is **0**.</span></span>  
- <span data-ttu-id="7150f-128">该`regions`属性包含一个值列表, 这些值用于显示文本的位置、其在图片中的位置以及在图像的该部分中找到的单词。</span><span class="sxs-lookup"><span data-stu-id="7150f-128">The `regions` property contains a list of values used to show where the text is, its position in the picture, and the word found in that part of the image.</span></span> 
- <span data-ttu-id="7150f-129">`boundingBox`值的四个整数为:</span><span class="sxs-lookup"><span data-stu-id="7150f-129">The four integers of the `boundingBox` value are:</span></span> 
    - <span data-ttu-id="7150f-130">左边缘的 x 坐标</span><span class="sxs-lookup"><span data-stu-id="7150f-130">the x-coordinate of the left edge</span></span> 
    - <span data-ttu-id="7150f-131">上边缘的 y 轴坐标值</span><span class="sxs-lookup"><span data-stu-id="7150f-131">the y-coordinate of the top edge</span></span>
    - <span data-ttu-id="7150f-132">边界框的宽度</span><span class="sxs-lookup"><span data-stu-id="7150f-132">the width of the bounding box</span></span>
    - <span data-ttu-id="7150f-133">边界框的高度,</span><span class="sxs-lookup"><span data-stu-id="7150f-133">the height of the bounding box,</span></span> 
   
    <span data-ttu-id="7150f-134">您可以使用这些值在图像中找到的每一段文本周围绘制框。</span><span class="sxs-lookup"><span data-stu-id="7150f-134">You can use these values to draw boxes around every piece of text found in the image.</span></span>

<span data-ttu-id="7150f-135">正如您在本练习中所看到`ocr`的, 该服务提供有关图像中打印文本的详细信息。</span><span class="sxs-lookup"><span data-stu-id="7150f-135">As you can see in this exercise, the `ocr` service gives detailed information about the printed text in an image.</span></span> 

<span data-ttu-id="7150f-136">有关此`ocr`操作的详细信息, 请参阅[OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc)参考文档。</span><span class="sxs-lookup"><span data-stu-id="7150f-136">For more information about the `ocr` operation, see the [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc) reference documentation.</span></span>