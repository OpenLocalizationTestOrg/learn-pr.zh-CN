Mojifier 是一个宽延时间 bot, 它会检测并将图像中的图符替换为与其情感相匹配的表情符号。 例如：  

![示例 Mojified 脸。 中间人的图片位于左侧, 其中有一个箭头指向右侧的表情符号, 并将其置于其正面。](../media/example-mojify-image.png)

它旨在作为自定义命令在可宽延时间中工作。 虽然您可以将命令命名为您喜欢的命令, 但本模块将把`mojify`它称为。 若要执行命令, 请`/mojify <image to mojify>`输入。

然后, Mojifier 将:

  1. 计算图像中任何人员的情感
  2. 将感受与表情符号匹配
  3. 将图像中的面孔替换为表情符号
  4. 将更新后的图像作为答复投递到可宽延时间

这将导致新 mojified 图像显示在可宽延时间中, 如下所示: 

![调用可宽延时间 Mojifier 应用将表情符号添加到 URL 上的图像。 Mojifier 已使用图像对 URL 做出响应。](../media/8.slack-type-mojify.png)

Mojifier 是使用 TypeScript、 [azure 函数](https://azure.microsoft.com/services/functions?azure-portal=true)和[azure 认知服务](https://azure.microsoft.com/services/cognitive-services?azure-portal=true)编写而成。 您可以使用这些程序制作自己的 Mojifier 版本。

## <a name="learning-objectives"></a>学习目标

在本模块中, 您将:

- 对图像中任何人员的情感进行分类
- 将感受与表情符号匹配
- 将图像中的面孔替换为表情符号
- 将更新后的图像作为答复投递到可宽延时间

## <a name="tools-youll-use"></a>您将使用的工具

### <a name="azure-cognitive-services"></a>Azure 认知服务

Azure 认知服务是一组高级 api, 可用于将高级人工智能 (AI) 功能快速添加到应用程序中。 如果您知道如何发出 HTTP 请求, 那么您应该能够使用认知服务。

### <a name="azure-functions"></a>Azure 函数

通过 Azure 函数, 可以托管可响应事件或 HTTP 请求的代码段。 Azure 会自动处理缩放问题, 您只需付费即可使用。 与 Microsoft 学习的任何内容一样, 我们都会在学习环境中向你介绍任何成本。

> [!NOTE]
> [GitHub](https://github.com/MicrosoftDocs/mslearn-the-mojifier?azure-portal=true)上提供了 Mojifier 的所有代码。
