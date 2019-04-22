请记住, 您的分析师的财务模型是在 Azure 虚拟机上运行的。 若要进一步自动化部署, 您需要从 Azure CLI 命令和脚本迁移到资源管理器模板。

在开始之前, 您可能首先想知道哪些现有模板存在, 您可以从中进行学习和构建。

在这里, 你将了解什么是 Azure 快速入门模板以及哪些预建模板可供你立即使用。

> [!TIP]
> 首选 Windows 或想要尝试一些新的内容吗？ 从此页面顶部选择 " **windows** " 以部署 windows Server 虚拟机。

## <a name="what-are-azure-quickstart-templates"></a>什么是 Azure 快速入门模板？

azure 快速入门模板是由 Azure 社区提供的资源管理器模板。 GitHub 上提供了快速启动模板。

许多模板都提供了部署解决方案所需的一切。 其他人可以作为你的模板的起始点。 无论哪种方式, 都可以研究这些模板, 以了解如何最大限度地创作和构造自己的模板。

## <a name="discover-whats-on-the-quickstart-template-gallery"></a>了解快速入门模板库中的内容

假设您要查找一个资源管理器模板, 该模板将提供一个包含 VM、 &ndash;基本网络设置和存储的基本 VM 配置。

1. 首先, 浏览到[快速入门模板库](https://azure.microsoft.com/resources/templates?azure-portal=true)以查看可用内容。

    你将看到许多受欢迎和最近更新的模板。 这些模板适用于 Azure 资源和受欢迎的软件包。

    ![Azure 快速入门模板库网页的一部分。](../../media/3-gallery-homepage.png)

1. 假设您在[部署简单的 Ubuntu Linux VM](https://azure.microsoft.com/resources/templates/101-vm-simple-linux/?azure-portal=true)模板中。

    ![Ubuntu VM 模板的库页面](../../media/3-gallery-page-linux.png)

    名称听起来像你所需的那样。 不过, 让我们进一步了解一下此模板的功能。

    使用 "**部署到 Azure** " 按钮, 可以直接通过 Azure 门户部署模板。 但此处不会执行此操作。 相反, 你将使用 Azure CLI 从云命令行管理程序部署模板。

1. 单击**github 上**的 "浏览" 以导航到 github 上的模板源代码。

    你会看到这一点。

    ![适用于资源管理器模板的 GitHub 自述文件](../../media/3-github-page-linux.png)

    使用 "**部署到 Azure** " 按钮, 可以直接通过 Azure 门户部署模板, 就像您在库页面上看到的那样。

1. 单击 "**可视化**" 以导航到 Azure 资源管理器可视化工具。

    你将看到构成部署的资源, 包括 VM、存储帐户和网络资源。

    您可以使用鼠标对资源进行排列。 您还可以使用鼠标的滚轮向外缩放。

    ![以可视化方式显示 azure 资源的 azure 资源管理器可视化工具](../../media/3-armviz-linux.png)

1. 单击标有 " **MyUbuntuVM**" 的**虚拟机**资源。

    您将看到定义 VM 资源的源代码。

    ![显示模板源代码的 Azure 资源管理器可视化工具](../../media/3-armviz-vm-linux.png)

    你将有更多的时间来检查源代码, 只需一位。 但现在, 请花些时间来简短地查看。

    您会发现:

    * 资源的类型为`Microsoft.Compute/virtualMachines`。
    * 它的位置 (或 Azure 区域) 来自名为`location`的模板参数。
    * VM 的大小来自模板变量`vmSize`。
    * 将从模板变量读取计算机名称, 并从模板参数中读取 VM 的用户名和密码。

在实践中, 您可能会查看 GitHub 上的**README.md**文件, 并进一步检查源代码以查看此模板是否符合您的需求。

但现在, 此模板看起来是有代表性的。 在下一部分中, 你将继续并部署此模板。
