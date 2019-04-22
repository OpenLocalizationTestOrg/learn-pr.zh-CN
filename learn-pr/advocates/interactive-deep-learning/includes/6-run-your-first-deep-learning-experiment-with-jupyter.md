![PyTorch 徽标](../media/5-image1.png) 

<span data-ttu-id="ccdb6-102">通常情况下, 深入学习的工程师不应手动实现矩阵代数运算。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-102">Typically deep learning engineers don't implement the matrix algebra operations all by hand.</span></span> <span data-ttu-id="ccdb6-103">而是使用框架 (如 PyTorch 或 TensorFlow)。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-103">Instead, they use frameworks such as PyTorch or TensorFlow.</span></span>  

<span data-ttu-id="ccdb6-104">PyTorch 是一个基于 python 的框架, 可提供作为深入学习开发平台的灵活性。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-104">PyTorch is a python-based framework that provides flexibility as a deep learning development platform.</span></span> <span data-ttu-id="ccdb6-105">它基于 Python 科学计算库 (NumPy) 构建。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-105">It's built on the Python scientific computing library, NumPy.</span></span> 

<span data-ttu-id="ccdb6-106">现在, 你可能会问, 为什么我们使用 PyTorch 构建深入学习模型？</span><span class="sxs-lookup"><span data-stu-id="ccdb6-106">Now you might ask, why would we use PyTorch to build deep learning models?</span></span>  

- <span data-ttu-id="ccdb6-107">易于使用 API –如果您知道 Python, 则可以快速向上提升。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-107">Easy to use API – If you know Python, you can ramp up quickly.</span></span>
- <span data-ttu-id="ccdb6-108">Python 支持– PyTorch 与科学计算堆栈顺利集成。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-108">Python support – PyTorch smoothly integrates with the scientific computing stack.</span></span>
- <span data-ttu-id="ccdb6-109">动态计算图–而不是具有特定功能的预定义关系图, PyTorch 可动态生成可在运行时修改的计算关系图。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-109">Dynamic computation graphs – Instead of predefined graphs with specific functionality, PyTorch builds computational graphs dynamically that can be modified during runtime.</span></span> <span data-ttu-id="ccdb6-110">动态计算图对于嵌套的批处理很有用, 并且当我们不知道创建给定网络所需的内存量时。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-110">Dynamic computation graphs are valuable for nested batching and when we do not know how much memory will be needed for creating a given network.</span></span>

<span data-ttu-id="ccdb6-111">有关 PyTorch 的详细信息, 请参阅[PyTorch.org 官方文档](https://pytorch.org/about/)。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-111">For more information about PyTorch, see [PyTorch.org official documentation](https://pytorch.org/about/).</span></span>

## <a name="run-your-first-pytorch-model"></a><span data-ttu-id="ccdb6-112">运行您的第一个 PyTorch 模型</span><span class="sxs-lookup"><span data-stu-id="ccdb6-112">Run your first PyTorch model</span></span>

<span data-ttu-id="ccdb6-113">现在, 您已从 PyTorch 映像预配了一个 Docker 容器, 现在是时候进行实验了。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-113">Now that you have a Docker container provisioned from a PyTorch image, it's time to experiment.</span></span> <span data-ttu-id="ccdb6-114">如果您记得, 我们从[python.org](https://python.org)下载了一个笔记本。该示例笔记本引导您完成网络的培训, 以便将图像分类为不同的类别。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-114">If you recall, we downloaded a notebook from [python.org](https://python.org). That sample notebook walks you through training a network to classify images  into different categories.</span></span> <span data-ttu-id="ccdb6-115">它定义了一个深度 Convolutional 神经网络 (CNN)。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-115">It defines a deep Convolutional Neural Network (CNN).</span></span>

1. <span data-ttu-id="ccdb6-116">在本地浏览器中导航到您在上一个练习中设置的 Jupyter 笔记本服务器。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-116">Navigate in your local browser to the Jupyter Notebook server that you set up in the last exercise.</span></span> <span data-ttu-id="ccdb6-117">URL 的格式为:</span><span class="sxs-lookup"><span data-stu-id="ccdb6-117">The URL will be of the form:</span></span>

    `<HOSTNAME>.<REGION>.cloudapp.azure.com:8888/?token={sometoken}`

1. <span data-ttu-id="ccdb6-118">在仪表`first_pytorch_classifier.ipynb`板中选择笔记本。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-118">Select the `first_pytorch_classifier.ipynb` notebook in the dashboard.</span></span>

    ![依次选择 "first_pytorch_classifier" 和 "ipynb"。](../media/5-image2.PNG)

    <span data-ttu-id="ccdb6-120">按照笔记本中的说明培训您的第一个 PyTorch 分类器。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-120">Follow the instructions in the notebook to train your first PyTorch classifier.</span></span>

    !["培训分类器笔记本" 的屏幕截图](../media/5-image3.PNG)

2. <span data-ttu-id="ccdb6-122">从笔记本顶部开始, 按顺序运行每个单元格。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-122">Start from the top of the notebook and run each cell in order.</span></span> <span data-ttu-id="ccdb6-123">请注意以下事项:</span><span class="sxs-lookup"><span data-stu-id="ccdb6-123">Note the following:</span></span>

    - <span data-ttu-id="ccdb6-124">某些单元格需要很长时间才能运行。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-124">Some of the cells take a long time to run.</span></span> <span data-ttu-id="ccdb6-125">观察笔记本右上部的小点, 旁边有 "Python 3" 字样。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-125">Observe the small dot in the top right of the notebook beside the words "Python 3".</span></span> <span data-ttu-id="ccdb6-126">当内核忙于操作时, 点将变成填充的、较深的圆形。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-126">When the kernel is busy with an operation, the dot becomes a filled, darker, circle.</span></span> <span data-ttu-id="ccdb6-127">在操作完成之前, 它将一直保持这种方式。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-127">It remains that way until the operation is complete.</span></span> 
    - <span data-ttu-id="ccdb6-128">您正在培训 CNN 对图像进行分类。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-128">You're training a CNN to classify images.</span></span> <span data-ttu-id="ccdb6-129">在网络经过培训之后, 笔记本将针对模型测试带标签的图像。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-129">Once the network is trained, the notebook will test labeled images against the model.</span></span> <span data-ttu-id="ccdb6-130">它记录为每个图像所做的预测, 并计算模型的准确性。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-130">It records the prediction made for each image and calculates the accuracy of the model.</span></span> <span data-ttu-id="ccdb6-131">你将看到以下格式的结果。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-131">You'll see results in the following format.</span></span>

    ![显示模型准确性的定型结果](../media/accuracy.png)
    
    - <span data-ttu-id="ccdb6-133">您可以在[PyTorch 教程文档](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html)中联机了解有关笔记本的更多信息。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-133">You can learn more about the notebook in the [PyTorch Tutorials documentation](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html) online.</span></span>
    
    - <span data-ttu-id="ccdb6-134">在笔记本的末尾, 笔记讨论了 GPU 上的培训。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-134">Towards the end of the notebook, the notes talk about training on a GPU.</span></span> <span data-ttu-id="ccdb6-135">如果您已按照本模块中的练习执行, 则您已设置了基于 CPU 的 VM。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-135">If you followed the exercises in this module, you have set up a CPU-based VM.</span></span> <span data-ttu-id="ccdb6-136">这对于模型而言很有意义, 在使用 GPU 时, 您可能无法在培训时间中看到任何重大改进。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-136">This is fine for a model this size and you may not see any significant improvements in training time with a GPU.</span></span> <span data-ttu-id="ccdb6-137">如果要使用具有 gpu 的虚拟机来试用模块, 则需要进行两项更改:</span><span class="sxs-lookup"><span data-stu-id="ccdb6-137">If you do want to try the module using a  virtual machine with GPUs, then there are two changes you need to make:</span></span>
    - <span data-ttu-id="ccdb6-138">在已启用 GPU 的 N 系列 VM 大小上设置 DSVM。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-138">Provision DSVM on a GPU enabled, N-series VM size.</span></span>
    - <span data-ttu-id="ccdb6-139">使用`nvidia-docker`而不是`docker`在上一个练习中创建容器。</span><span class="sxs-lookup"><span data-stu-id="ccdb6-139">Create a container using `nvidia-docker` instead of `docker` in the previous exercise.</span></span>