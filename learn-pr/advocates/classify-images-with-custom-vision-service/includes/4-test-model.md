现在我们已对模型进行了培训, 现在可以对其进行测试了。 我们将为模型提供新图像, 并查看它对其进行分类的效果。

1. 单击页面顶部的 "**快速测试**"。

    ![突出显示了快速测试按钮的 Artworks 项目顶栏的屏幕截图](../media/4-portal-click-quick-test.png)

1. 单击 "**浏览本地文件**", 然后浏览到之前下载的 "模块资源" 文件夹中的 "快速测试" 文件夹。 选择 " **PicassoTest_01**", 然后单击 "**打开**"。

    ![选定了 Picasso 测试图像并突出显示了 "打开" 按钮的 QuickTests 文件夹的屏幕截图](../media/4-portal-select-test-01.png)

1. 在 "快速测试" 对话框中检查测试结果。 绘图是 Picasso 的概率是多少？ Rembrandt 或 Pollock 的概率是多少？

    ![显示所选图像的 "QuickTest" 对话框的屏幕截图](../media/4-quick-test-result.png)

1. 关闭 "快速测试" 对话框。 然后单击页面顶部的 "**预测**"。

    ![突出显示了 "预测" 选项卡的 Artworks 项目顶栏的屏幕截图](../media/4-portal-select-predictions.png)

1. 单击您上载的测试映像以显示它的详细信息。 然后, 通过从下拉列表中选择**Picasso**并单击 "**保存并关闭**", 将图像标记为 "Picasso"。

    > 通过这种方式标记测试图像, 可以优化模型, 而无需上载其他培训图像。

    ![显示为使用 Picasso 标记进行预测而选择的图像的屏幕截图, 并突出显示 "保存并关闭" 按钮](../media/4-tag-test-image.png)

1. 运行另一个快速测试, 这次使用 "快速测试" 文件夹中名为**FlowersTest**的文件。 确认分配给此图像的可能性较低, 即 Picasso、Rembrandt 或 Pollock。

该模型经过培训并准备就绪, 并在识别特定艺术家的 paintings 时似乎非常熟练。 让我们通过 HTTP 调用预测终结点, 并查看发生的情况。