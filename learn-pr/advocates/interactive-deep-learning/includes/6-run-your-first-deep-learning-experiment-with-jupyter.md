![PyTorch 徽标](../media/5-image1.png) 

通常情况下, 深入学习的工程师不应手动实现矩阵代数运算。 而是使用框架 (如 PyTorch 或 TensorFlow)。  

PyTorch 是一个基于 python 的框架, 可提供作为深入学习开发平台的灵活性。 它基于 Python 科学计算库 (NumPy) 构建。 

现在, 你可能会问, 为什么我们使用 PyTorch 构建深入学习模型？  

- 易于使用 API –如果您知道 Python, 则可以快速向上提升。
- Python 支持– PyTorch 与科学计算堆栈顺利集成。
- 动态计算图–而不是具有特定功能的预定义关系图, PyTorch 可动态生成可在运行时修改的计算关系图。 动态计算图对于嵌套的批处理很有用, 并且当我们不知道创建给定网络所需的内存量时。

有关 PyTorch 的详细信息, 请参阅[PyTorch.org 官方文档](https://pytorch.org/about/)。

## <a name="run-your-first-pytorch-model"></a>运行您的第一个 PyTorch 模型

现在, 您已从 PyTorch 映像预配了一个 Docker 容器, 现在是时候进行实验了。 如果您记得, 我们从[python.org](https://python.org)下载了一个笔记本。该示例笔记本引导您完成网络的培训, 以便将图像分类为不同的类别。 它定义了一个深度 Convolutional 神经网络 (CNN)。

1. 在本地浏览器中导航到您在上一个练习中设置的 Jupyter 笔记本服务器。 URL 的格式为:

    `<HOSTNAME>.<REGION>.cloudapp.azure.com:8888/?token={sometoken}`

1. 在仪表`first_pytorch_classifier.ipynb`板中选择笔记本。

    ![依次选择 "first_pytorch_classifier" 和 "ipynb"。](../media/5-image2.PNG)

    按照笔记本中的说明培训您的第一个 PyTorch 分类器。

    !["培训分类器笔记本" 的屏幕截图](../media/5-image3.PNG)

2. 从笔记本顶部开始, 按顺序运行每个单元格。 请注意以下事项:

    - 某些单元格需要很长时间才能运行。 观察笔记本右上部的小点, 旁边有 "Python 3" 字样。 当内核忙于操作时, 点将变成填充的、较深的圆形。 在操作完成之前, 它将一直保持这种方式。 
    - 您正在培训 CNN 对图像进行分类。 在网络经过培训之后, 笔记本将针对模型测试带标签的图像。 它记录为每个图像所做的预测, 并计算模型的准确性。 你将看到以下格式的结果。

    ![显示模型准确性的定型结果](../media/accuracy.png)
    
    - 您可以在[PyTorch 教程文档](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html)中联机了解有关笔记本的更多信息。
    
    - 在笔记本的末尾, 笔记讨论了 GPU 上的培训。 如果您已按照本模块中的练习执行, 则您已设置了基于 CPU 的 VM。 这对于模型而言很有意义, 在使用 GPU 时, 您可能无法在培训时间中看到任何重大改进。 如果要使用具有 gpu 的虚拟机来试用模块, 则需要进行两项更改:
    - 在已启用 GPU 的 N 系列 VM 大小上设置 DSVM。
    - 使用`nvidia-docker`而不是`docker`在上一个练习中创建容器。