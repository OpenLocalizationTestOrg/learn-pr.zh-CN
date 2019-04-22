您要构建的应用程序是一个跨平台的移动应用程序, 它与 Azure 功能进行交互以共享您的位置。 在此单元中, 将使用 Visual Studio 创建空白移动应用程序, 并安装包含用于获取用户位置的 API 的 NuGet 包。

## <a name="create-the-xamarinforms-project"></a>创建 Xamarin. Forms 项目

1. 在 Visual Studio 中, 选择 "*文件"-">New->Project ...*"。

1. 从左侧的树中, 选择 " *Visual c #->Cross* ", 然后从中央面板中选择 "*移动应用程序 (Xamarin. Forms)* "。

1. 将解决方案命名为 "ImHere"。

1. 为解决方案选择适当的位置。

1. 单击"确定"。

    !["新建解决方案" 对话框](../media/2-new-solution-dialog.png)

1. 从 "**新建跨平台应用程序**" 对话框中, 选择 "*空白" 应用*程序模板。

1. 对于此模块, 您将构建一个 UWP 应用程序, 因此请取消选中 "iOS 和 Android" 并选中 "保留 UWP"。

1. 对于*代码共享策略*, 请选择 " **.net Standard**"。

1. 单击"确定"。

    !["配置新解决方案" 对话框](../media/2-configure-solution-dialog.png)

Visual Studio 将为您创建两个项目: 一个名`ImHere.UWP`为的 UWP 应用程序和一个`ImHere`.net 标准库。 Xamarin. Forms 应用程序由两部分组成-一个或多个平台特定的应用程序项目以及一个 (或多个) .net 标准库。 特定于平台的应用程序项目包含在相关平台上运行应用程序所需的特定于平台的代码。 然后, 这些项目启动跨平台 .net 标准库中定义的 Xamarin 应用程序。 在跨平台代码中构建应用程序, 在运行时, 您创建的任何用户界面都将转换为相关的特定于平台的 UI 组件。

## <a name="adding-xamarinessentials"></a>添加 Xamarin

UWP、Android 和 iOS 平台提供了很多类似的功能, 可充分利用操作系统和硬件。 尽管存在这些相似之处, 但 api 的差异很大。 从跨平台代码使用这些 api 需要在您向 .net 标准库公开的应用程序项目中编写特定于平台的代码。 [Xamarin](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true)是一个 NuGet 包, 它提供跨多个 api 的跨平台抽象, 因此您无需编写特定于平台的代码。 这包括将在应用程序中使用的地理位置 api, 以获取用户的位置。

1. 右键单击 Visual Studio " `ImHere`解决方案资源管理器" 中的 "解决方案`ImHere` (顶级解决方案, 而不是 .net 标准项目)", 然后选择 "*管理解决方案的 NuGet 包 ...*"。

1. 选择 "**浏览**" 选项卡, 然后搜索 "Xamarin"。 此包当前可用作预发布 NuGet 包, 请选中 "*包含 prelease* " 框。

    > [!TIP]
    > 如果看不到 Xamarin NuGet 包, 则选中 "*包含 prelease* " 的双重检查。 

1. 选择 " **Xamarin** NuGet 包"。

1. 在右侧的 "项目" 列表中检查所有项目。

1. 单击 "**安装**" 按钮以安装 NuGet 包。 你需要接受许可证才能继续。

    ![将 Xamarin NuGet 包添加到解决方案中的所有项目](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a>生成并运行应用程序

1. 右键单击 "解决方案资源`ImHere.UWP`管理器" 中的项目, 然后选择 "*设为启动项目*"。

1. 将 "生成配置" 设置为 "**调试**"、"用于**x86**的平台" 和 "要在**本地计算机**上运行的设备"。

    ![设置要在本地设备上运行的调试 x86 配置](../media/2-debug-configuration.png)

1. 开始调试应用程序。

    ![运行的应用程序](../media/2-debuging-app.png)

## <a name="summary"></a>摘要

在此单位中, 您创建了一个新的 Xamarin。 Forms 跨平台移动应用并添加了 xamarin NuGet 包。 接下来, 您将了解如何构建移动应用程序 UI 和逻辑。