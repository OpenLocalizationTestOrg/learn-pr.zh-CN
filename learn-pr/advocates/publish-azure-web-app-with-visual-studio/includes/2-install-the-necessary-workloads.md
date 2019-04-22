获取新网站准备工作的第一步是准备开发环境。 创建和部署 ASP.NET web 应用程序要求在本地计算机上安装必要的工具。 在这里, 我们将介绍你所需的工具以及如何安装它们。


Visual Studio 2017 有两个需要创建、发布网站并将其部署到 Azure 的工作负载。 这些工作负载包括 ASP.NET 网站的所有模板, 并提供将网站连接和部署到 Azure 的功能。

您需要确保已安装以下工作负荷:

- **ASP.NET 和 web 开发**: Visual Studio 2017 中的 web 开发工作负载旨在最大限度地提高使用 ASP.NET 的 web 应用程序开发的效率, 以及 HTML 和 JavaScript 等基于标准的技术。
- **azure 开发**: visual studio 2017 中的 azure 开发工作负载将安装最新的适用于 .net 的 azure SDK 和 tools for Visual studio。 安装这些项后, 可以在云资源管理器中查看资源, 使用 azure 资源管理器工具创建资源, 构建应用程序以使用 azure web 和云服务, 以及使用 Azure data Lake 工具执行大型数据操作。


您将使用 visual studio 安装程序修改作为 Visual studio 的一部分安装的组件。

1. 若要启动安装程序, 请从 Windows "开始" 菜单中向下滚动到 " **V**", 然后单击 " **Visual Studio 安装程序**"。 或者, 当 "开始" 菜单打开时, 只需键入```Visual Studio Installer```即可找到安装程序链接。 然后选择 " **Enter"。**

1. 将显示 "Visual Studio 安装程序" 窗口。 单击 "**修改**" 按钮。 如果看不到这种情况, 可以选择 "**更多**" 下拉菜单下的 "**修改**"。

    ![修改 Visual Studio](../media/2-visual-studio-installer-modify.PNG)

1. 确保在 "**工作负荷**" 选项卡的 " **web & 云**" 部分下选择了**ASP.NET 和 web 开发**和**Azure 开发**工作负载。 ![安装工作负载](../media/2-select-workloads.png)

1. 接下来, 单击安装程序右下角的 "**修改**" 按钮。 Visual Studio 安装程序将下载并安装必要的组件。

1. 单击 "**启动**" 以准备在下一个设备中创建 ASP.NET 应用程序。

您可以使用**ASP.NET 和 web 开发**和**Azure 开发**工作负载, 从 Visual Studio 2017 创建、管理和发布 ASP.NET 网站。
