假设您现在想要阅读 frontline 分发服务器发布到您的服务器的股票图像中的文本。 特别是, 您想要扫描产品, 查找包含销售价的促销不干胶标签。 现在是时候尝试计算机远景 API 的光学字符识别 (OCR) 功能。 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a>调用计算机远景 API 以提取打印文本

该`ocr`操作检测图像中的文本, 并将识别的字符提取到计算机可用的字符流中。 请求 URL 的格式如下:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr?language=<...>&detectOrientation=<...>`

与往常一样, 必须对创建帐户的区域进行所有呼叫。 该调用接受两个可选参数:

- **语言**: 要在图像中检测到的文本的语言代码。 默认值为`unk`或未知。 这让我们的服务自动检测图像中文本的语言。
- **detectOrientation**: 如果为 true, 服务将尝试检测图像方向并在进一步处理前对其进行更正, 例如, 是否颠倒了图像。 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a>使用 OCR 从图像中提取打印的文本

我们要使用的图像是光学字符识别 (OCR) 的封面。 *.net Microservices: 体系结构适用于容器的 .net 应用程序*。

![电子书 .net Microservices 的封面的图片: 容器的 .net 应用程序的体系结构](../media/5-ebook.png)

1. 在云命令行管理程序中执行以下命令。 将`<region>`命令中的替换为您的认知服务帐户所在的区域。

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

下面的 JSON 是我们从此调用获取的响应的示例。 已删除一些 JSON 行, 以使代码段更适合页面。

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

让我们更详细地查看此响应。 

- 服务将文本识别为英语。 `language`字段的值包含图像中检测到的文本的 BCP-47 语言代码。 在此示例中, 它是**en**或英语。 
- 检测`orientation`为 " **up**"。 此属性是在图像根据检测到的文本角度围绕其中心旋转后, 识别的文本的顶部方向。 
- `textAngle`是要使文本变为水平方向或垂直方向而必须旋转的角度。 在此示例中, 文本是绝对水平的, 因此返回的值为**0**。  
- 该`regions`属性包含一个值列表, 这些值用于显示文本的位置、其在图片中的位置以及在图像的该部分中找到的单词。 
- `boundingBox`值的四个整数为: 
    - 左边缘的 x 坐标 
    - 上边缘的 y 轴坐标值
    - 边界框的宽度
    - 边界框的高度, 
   
    您可以使用这些值在图像中找到的每一段文本周围绘制框。

正如您在本练习中所看到`ocr`的, 该服务提供有关图像中打印文本的详细信息。 

有关此`ocr`操作的详细信息, 请参阅[OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc)参考文档。