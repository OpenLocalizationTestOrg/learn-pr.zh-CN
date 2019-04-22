在这里, 你将在 Windows 或 macOS 开发计算机上安装 Visual Studio。

## <a name="exercise-steps"></a>练习步骤

::: zone pivot="windows"

### <a name="windows"></a>Windows

1. 从https://visualstudio.microsoft.com/downloads/下载 Visual Studio 安装程序。

1. 运行安装程序。

1. 在 "**工作负荷**" 选项卡上, 选择**Azure 开发**工作负载。

    下面的屏幕截图显示了在 visual studio 中选择允许 Azure 开发的 visual studio 安装程序工作负荷。

    ![突出显示了 Azure 开发工作负载的 Visual Studio 安装程序的屏幕截图。](../media/5-select-azure-workload.png)

1. Optional安装 ASP.NET 和 web 开发工作负载, 准备好创建适用于 Azure 的 web 应用程序。

1. 单击 "**安装**", 等待 Visual Studio 安装。 对于已安装 Visual Studio 的系统, 此按钮可能会显示 "**修改**"。

1. 安装完成后, 打开 Visual Studio。

1. 转到 Visual Studio 中的 "视图" 菜单, 确保您具有 "**云资源管理器**" 选项。

    下面的屏幕截图显示了在安装了 Azure 开发工作负载时将显示的云浏览器菜单选项。

    ![突出显示了 "云浏览器" 菜单选项的 Visual Studio "视图" 菜单屏幕截图。](../media/5-verify-cloud-explorer.png)

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a>macOS

1. 转到https://visualstudio.microsoft.com/并下载 Visual Studio for Mac 安装程序。

1. 单击 VisualStudioInstaller 文件以装入安装程序, 然后通过双击徽标运行它。

1. 在出现时确认隐私和许可条款。

1. 安装程序将询问您要安装哪些组件。 Azure 组件已经是 Visual Studio for Mac 的一部分, 但建议安装 **.net Core** platform 以开发适用于 Azure 的 web 体验。

    下面的屏幕截图显示了向 Visual Studio for Mac 添加 Azure 开发功能所需的 .net 核心平台。

    ![突出显示了选定的 .net Core platform 选项的 Visual Studio for Mac 安装程序的屏幕截图。](../media/5-vsmac-install-net-core.png)

1. 选择好选择后, 单击 "**安装并更新**", 并等待安装程序完成。

1. 如果系统提示你提升所需的权限, 请使用管理员凭据执行此操作。

1. 安装程序完成后, 启动 Visual Studio for Mac。

::: zone-end