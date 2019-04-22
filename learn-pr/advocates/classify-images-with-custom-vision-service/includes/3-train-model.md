在此单位中, 您将使用上一练习中上传和标记的图像来训练模型。 在训练模型后, 可以通过上载其他标记图像并重新对其进行重新培训来优化模型。

1. 单击页面顶部的 "**培训**" 按钮以培训模型。 每次培训模型时, 都会创建一个新的小版本。 自定义远景服务维护多个迭代, 使您可以比较您在一段时间内的进度。

    ![突出显示了 "训练" 按钮的 Artworks 项目顶栏的屏幕截图](../media/2-portal-click-train.png)

1. 等待培训过程完成。 (只需几秒钟即可。)然后查看针对迭代1提供给您的培训统计信息。 

    结果显示了模型的精度、**精度**和**召回**的两个度量。 假设模型显示有三个 Picasso 图像, 三个来自 Van Gogh。 假设它正确地将两个 Picasso 示例标识为 "Picasso", 但将两个 Van Gogh 示例错误地标识为 Picasso。 在这种情况下,**精度**将为 50%, 因为它将正确地识别两个图像中的两个。 **撤回**得分为 67%, 因为它正确地确定了三个 Picasso 图像中的两个。

    ![显示对模型进行培训的结果的屏幕截图。 结果显示了总体 100% 精确度和 84.8% 撤回。](../media/2-portal-train-complete.png)

在下一个练习中, 我们将使用门户的快速测试功能测试模型, 该功能使您可以将图像提交到模型, 并查看它如何使用从培训图像获得的知识对其进行分类。

> [!TIP]
> 除了使用自定义远景门户 UI 培训模型之外, 还可以通过在[自定义远景培训 API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3)中调用[TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095bed)方法来对其进行训练。