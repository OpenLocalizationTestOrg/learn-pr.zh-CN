产品的 Frontline 分销商扫描和上载商店货位的图像。 作为贵公司的开发人员主管, 您负责创建图像的缩略图。 缩略图在您为销售团队创建的联机报告中使用。 最近, 销售经理说, 报告中的图像模糊, 并且通常没有产品的前端和中心, 使扫描大型报告变得困难。 你将由你来改进这种情况。

您决定尝试计算机远景 API 的缩略图生成功能。 或许它可以执行比您编写的调整大小函数更好的工作。

计算机远景首先生成高质量的缩略图, 然后分析图像中的对象以确定感兴趣的区域 (ROI)。 计算机远景然后裁剪图像以满足感兴趣的区域的要求。 根据您的需要, 可以使用与原始图像的纵横比不同的高宽比显示生成的缩略图。 让我们看看它在操作中。

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a>调用计算机远景 API 以生成缩略图

该`generateThumbnail`操作将创建具有用户指定的宽度和高度的缩略图图像。 默认情况下, 该服务会分析图像, 标识感兴趣的区域 (ROI), 并基于 ROI 生成智能裁剪坐标。 当您指定与输入图像的纵横比不同的纵横比时, 智能裁剪将会有所帮助。 请求 URL 的格式如下:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=<...>&height=<...>&smartCropping=<...>`

可以向 API 提供不同的参数, 以生成适当的缩略图来满足您的需求。 和`width` `height`参数是必需的。 它们告诉 API 您需要用于特定图像的大小。 `smartCropping`参数通过分析图像中感兴趣的区域以将其保留在缩略图中, 从而生成更智能的裁剪。 例如, 在启用智能裁剪的情况下, 裁剪的配置文件图片会使某人在图片框架中的表面保持不被使用, 即使该图片的纵横比较不同也是如此。

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a>生成缩略图

我们将在此示例中使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。

![一种可爱的白色狗坐在绿色草地中的图片。](../media/4-dog.png)

1. 在 Azure 云命令行管理程序中执行以下命令。 在`<region>`命令中使用您的认知服务帐户的区域进行替换

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

在此示例中, 我们要求服务创建一个100x100 的缩略图。 启用智能裁剪。 成功的响应包含缩略图图像二进制, 我们会将其写入到名为 ".jpg" 的文件中。

> [!CAUTION]
> `-o`参数将输出重定向到文件。 始终会覆盖该文件, 因此, 如果您想要在尝试此命令时保留多个缩略图, 请更改文件名。

## <a name="view-the-generated-thumbnail"></a>查看生成的缩略图

将在你的 Azure 云 Shell 存储帐户中找到生成的缩略图。 已将文件**缩略图**命名为 .jpg。

Microsoft 学习中的云命令行管理程序无法下载文件, 但您可以按照这些说明操作, 通过 Azure 门户下载缩略图。

1. 在 Azure 云命令行管理程序中执行以下命令, 以确认您的主文件夹中存在文件**缩略图。**

    ```azurecli
    cd ~
    ls -l
    ```



1. 执行以下命令以移动`thumbnail.jpg`到 clouddrive 文件夹中。

    ```azurecli
    mv ~/thumbnail.jpg ~/clouddrive
    ```
1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。
1. 在 "门户" 仪表板的 "**所有资源**" 面板中, 选择名称以开头`cloudshell`的存储帐户。
1. 在 "存储帐户" 面板中, 依次选择 "**存储资源管理器**"、"**文件共享**" 和该集合中的文件共享 (以**cloudshellfiles**开头的名称)。
1. 选择 " *thunbnail* " 文件, 然后从顶部菜单中进行**下载**以查看图像。

该`generateThumbnail`操作是功能强大的缩略图生成器, 能够在缩略图中保持图像的感兴趣 (ROI)。

有关此`generateThumbnails`操作的详细信息, 请参阅[获取缩略图](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb)参考文档。
