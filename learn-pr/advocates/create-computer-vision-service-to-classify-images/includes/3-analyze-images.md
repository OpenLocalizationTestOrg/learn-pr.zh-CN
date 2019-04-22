作为 Contoso 饮料分布的开发人员, 您负责构建和维护业务线应用程序, 让您的 frontline 分销商扫描和上传商店货位的图像以进行重新进货。 

您想要验证用户发布的任何图像是否遵循贵公司设置的内容规则。 公司不希望将不良内容发布到公司网站。 鉴于人工智能中的进步, 你决定在应用中使用计算机远景 API。 

若要开始, 请在 Azure 订阅中创建计算机远景帐户, 并开始测试 "**分析**" 功能。

## <a name="calling-the-computer-vision-api-to-analyze-images"></a>调用计算机远景 API 以分析图像

该`analyze`操作将根据图像内容提取一组丰富的视觉功能。 请求 URL 的格式如下:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=<...>&details=<...>&language=<...>`

发送到服务的参数为`visualFeatures`、 `details`和。 `languages` 将`details`参数设置为`Landmarks`或`Celebrities`可帮助您识别使或 celebrities。 `visualFeatures`确定您希望服务返回的信息类型。 该`Categories`选项将对图像内容 (如树、建筑物等) 进行分类。 `Faces`将识别人员的面孔并为你提供其性别和年龄。

当遇到计算机远景 API 上的所有操作时, 都将对您要求其处理的图像进行以下限制:

- 支持的图像格式: JPEG、PNG、GIF、BMP。 
- 图像文件大小必须小于 4 MB。
- 图像尺寸必须至少为 50 x 50。

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a>确定图像中的使

让我们首先调用在图像中查找使。 在此示例中, 我们将使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。 

![在有 skies 的 mountains 上方具有蓝色的山地区间的图片。](../media/3-mountains.jpg)

在 Azure 云命令行管理程序中执行以下命令。 将`<region>`命令中的替换为您的认知服务帐户所在的区域。

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

- 此调用在图像 URL 指定的图像中查找使。 我们正在分析的映像存储在此练习的 GitHub 存储库中。 
- 该调用还会要求服务返回类别信息和图像说明。 该说明以完整的英文句子的形式返回。 
- 如你所知, 对 API 的每个调用都需要一个访问密钥。 这是在请求的`Ocp-Apim-Subscription-Key`标头中设置的。 

> [!TIP]
> 请求的结果是原始 JSON, 描述中的图片`url`。 我们在` | jq '.'`命令的末尾添加了 prettify JSON 输出。

此调用的 JSON 响应将返回以下内容:

- 列出`categories`检测到的所有图像类别的数组, 以及介于0和1之间的分数, 表示该映像属于指定类别的服务的置信度。
- 包含`description`与图像相关的标记或词语的数组的条目。
- 带有`captions`文本字段的条目, 该字段以英语描述图像中的内容。 请注意, 文本也有确定性的分数。 此分数可帮助您通过此分析来决定下一步操作。


## <a name="check-for-inappropriate-content-in-an-image"></a>检查图像中是否有不适当的内容

在此示例中, 我们将分析成人内容的图像。 置信度分数表示图像包含成人或 racy 内容的可能性。 

在此示例中, 我们将使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。 

![微笑的家庭的图片。](../media/3-people.png)

1. 在 Azure 云命令行管理程序中执行以下`<region>`命令, 在 URL 中进行替换。

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

在此示例中, 我们将`visualFeatures`设置`Adult,Description`为。 

响应为我们提供了两个置信分数, 一个用于 racy 内容, 一个用于成人内容。 使用这些分数加上图像说明和其他可视功能, 您可以开始标记发送到服务器的图像。

本练习中我们尝试的示例为您提供了可使用该`analyze`操作执行的分析类型的概念。 尝试使用不同的图像进行分析, 并尝试使用不同的 visualFeatures、details 和语言参数组合。

有关此`analyze`操作的详细信息, 请参阅[分析图像](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa)参考文档。