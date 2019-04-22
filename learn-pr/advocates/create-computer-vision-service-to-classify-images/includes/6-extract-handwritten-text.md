我们看到了计算机远景 API 如何从图像中提取打印出来的文本。 在本练习中, 我们将使用该服务来检测手写文本。

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a>调用计算机远景 API 以提取手写文本

该`recognizeText`操作检测并提取来自注释、字母、essays、白板、窗体和其他源的手写文本。 请求 URL 的格式如下:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=<...>`

必须对创建帐户的区域进行所有呼叫。

如果存在此参数`mode` , 则必须将该`Handwritten`参数`Printed`设置为或且区分大小写。 如果此参数设置为`Handwritten`或未指定, 则执行手写识别。 如果将参数设置为`Printed`, 则执行打印的文本识别。 从此调用获取结果所需的时间取决于图像中的书写量。

在此示例中, 我们将:

- 使用卷曲的`-D`选项将响应标头打印到控制台
- 复制我们`Operation-Location`在响应中收到的标头中的标头值
- 几秒钟后, 请检查针对结果指定的`Operation-Location` URL。

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a>检测并从图像中提取手写文本

我们将在此示例中使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。

![备注上的手写示例的图片](../media/6-handwriting.jpg)

1. 在 Azure 云命令行管理程序中执行以下命令。 将`<region>`命令中的替换为您的认知服务帐户所在的区域。

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

上面将此操作的标头转储到控制台。 下面是一个示例:

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

`Operation-Location`标头是在完成后将发布结果的位置。

2. 复制`Operation-Location`标头值。
1. 在 Azure 云命令行管理程序中执行`"<Operation-Location>"`以下命令, 将替换为您在上一步中复制的**操作位置**标头的值。

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

如果操作已完成, 则会收到包含手写识别请求结果的 JSON 文件。

有关此`recognizeText`操作的详细信息, 请参阅[识别手写文本](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200)参考文档。