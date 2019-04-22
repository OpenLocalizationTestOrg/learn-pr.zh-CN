![Docker 徽标](../media/3-image1.PNG)

Docker 是一种工具, 允许您在沙盒中部署应用程序, 以在所选的主机操作系统上运行。 它允许您使用标准化单元打包您的应用程序的所有依赖项。 但是, 如果 DSVM 基本图像附带了已预安装的最热门的深入学习框架, 为什么要使用 Docker？

尝试运行深入学习任务时, 开发人员会发现自己面临的依赖项问题。 例如： 

- 必须构建自定义程序包-深入学习研究人员在将代码发布到 GitHub 时, 会更少地考虑生产。 如果他们能够获取在自己的开发环境中工作的包, 则通常只假定其他人也可以执行此操作。
- GPU 驱动程序版本控制-CUDA 是由 NVIDIA 开发的并行计算平台和应用程序编程接口 (API)。 它允许开发人员使用 CUDA 的图形处理单元 (GPU) 进行常规用途的处理。 某些版本的 Tensorflow 将无法与高于9.1 的 CUDA 版本一起使用。 其他框架 (如 PyTorch) 似乎更好地在更高版本的 CUDA 中运行。

若要解决这些问题并提高代码的可用性, 可以使用 Docker 或其 GPU 型 NVIDIA Docker 来管理和运行深入学习项目。 

<!--Quiz 
What is CUDA? 
What versioning issues do deep learning engineers deal with? -->