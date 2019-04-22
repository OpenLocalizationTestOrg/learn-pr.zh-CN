<span data-ttu-id="ba425-101">现在我们已对模型进行了培训, 现在可以对其进行测试了。</span><span class="sxs-lookup"><span data-stu-id="ba425-101">Now that we've trained our model, it's time to test it.</span></span> <span data-ttu-id="ba425-102">我们将为模型提供新图像, 并查看它对其进行分类的效果。</span><span class="sxs-lookup"><span data-stu-id="ba425-102">We'll give the model new images and see how well it classifies it.</span></span>

1. <span data-ttu-id="ba425-103">单击页面顶部的 "**快速测试**"。</span><span class="sxs-lookup"><span data-stu-id="ba425-103">Click **Quick Test** at the top of the page.</span></span>

    ![突出显示了快速测试按钮的 Artworks 项目顶栏的屏幕截图](../media/4-portal-click-quick-test.png)

1. <span data-ttu-id="ba425-105">单击 "**浏览本地文件**", 然后浏览到之前下载的 "模块资源" 文件夹中的 "快速测试" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="ba425-105">Click **Browse local files**, and then browse to the "Quick Tests" folder in the module resources folder you download previously.</span></span> <span data-ttu-id="ba425-106">选择 " **PicassoTest_01**", 然后单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="ba425-106">Select **PicassoTest_01.jpg**, and click **Open**.</span></span>

    ![选定了 Picasso 测试图像并突出显示了 "打开" 按钮的 QuickTests 文件夹的屏幕截图](../media/4-portal-select-test-01.png)

1. <span data-ttu-id="ba425-108">在 "快速测试" 对话框中检查测试结果。</span><span class="sxs-lookup"><span data-stu-id="ba425-108">Examine the results of the test in the "Quick Test" dialog.</span></span> <span data-ttu-id="ba425-109">绘图是 Picasso 的概率是多少？</span><span class="sxs-lookup"><span data-stu-id="ba425-109">What is the probability that the painting is a Picasso?</span></span> <span data-ttu-id="ba425-110">Rembrandt 或 Pollock 的概率是多少？</span><span class="sxs-lookup"><span data-stu-id="ba425-110">What is the probability that it's a Rembrandt or Pollock?</span></span>

    ![显示所选图像的 "QuickTest" 对话框的屏幕截图](../media/4-quick-test-result.png)

1. <span data-ttu-id="ba425-112">关闭 "快速测试" 对话框。</span><span class="sxs-lookup"><span data-stu-id="ba425-112">Close the "Quick Test" dialog.</span></span> <span data-ttu-id="ba425-113">然后单击页面顶部的 "**预测**"。</span><span class="sxs-lookup"><span data-stu-id="ba425-113">Then click **Predictions** at the top of the page.</span></span>

    ![突出显示了 "预测" 选项卡的 Artworks 项目顶栏的屏幕截图](../media/4-portal-select-predictions.png)

1. <span data-ttu-id="ba425-115">单击您上载的测试映像以显示它的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ba425-115">Click the test image that you uploaded to show a detail of it.</span></span> <span data-ttu-id="ba425-116">然后, 通过从下拉列表中选择**Picasso**并单击 "**保存并关闭**", 将图像标记为 "Picasso"。</span><span class="sxs-lookup"><span data-stu-id="ba425-116">Then tag the image as a "Picasso" by selecting **Picasso** from the drop-down list and clicking **Save and close**.</span></span>

    > <span data-ttu-id="ba425-117">通过这种方式标记测试图像, 可以优化模型, 而无需上载其他培训图像。</span><span class="sxs-lookup"><span data-stu-id="ba425-117">By tagging test images this way, you can refine the model without uploading additional training images.</span></span>

    ![显示为使用 Picasso 标记进行预测而选择的图像的屏幕截图, 并突出显示 "保存并关闭" 按钮](../media/4-tag-test-image.png)

1. <span data-ttu-id="ba425-119">运行另一个快速测试, 这次使用 "快速测试" 文件夹中名为**FlowersTest**的文件。</span><span class="sxs-lookup"><span data-stu-id="ba425-119">Run another quick test, this time using the file named **FlowersTest.jpg** in the "Quick Test" folder.</span></span> <span data-ttu-id="ba425-120">确认分配给此图像的可能性较低, 即 Picasso、Rembrandt 或 Pollock。</span><span class="sxs-lookup"><span data-stu-id="ba425-120">Confirm that this image is assigned a low probability of being a Picasso, a Rembrandt, or a Pollock.</span></span>

<span data-ttu-id="ba425-121">该模型经过培训并准备就绪, 并在识别特定艺术家的 paintings 时似乎非常熟练。</span><span class="sxs-lookup"><span data-stu-id="ba425-121">The model is trained and ready to go and appears to be skilled at identifying paintings by certain artists.</span></span> <span data-ttu-id="ba425-122">让我们通过 HTTP 调用预测终结点, 并查看发生的情况。</span><span class="sxs-lookup"><span data-stu-id="ba425-122">Let's call the prediction endpoint over HTTP and see what happens.</span></span>