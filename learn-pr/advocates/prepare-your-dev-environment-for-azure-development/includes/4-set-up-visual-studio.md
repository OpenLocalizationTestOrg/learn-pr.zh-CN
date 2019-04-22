Visual Studio 是用于多种编程应用程序类型和语言的功能全面的集成开发环境 (IDE)。 Visual Studio 有一套完整的工具和功能, 专门针对使用 Microsoft Azure 开发应用程序。 这意味着 Azure 开发、调试和部署工具与 IDE 紧密集成在一起。

## <a name="visual-studio-2017"></a>Visual Studio 2017

Visual Studio 2017 是一个功能齐全的 IDE, 用于在包括 Windows、Android、iOS、web 和 Azure 的各种应用程序类型的应用程序中开发应用程序。

安装 Visual Studio 时, 您将看到多个可用的*工作负载*。 工作负荷是用于定义可安装的功能区域的库和组件的集合。 您可以使用工作负荷来执行 "主题" 安装, 而不是安装您必须知道并记住每个组件之间的依赖关系的单个组件。 这可确保包含所有必需的组件。

Visual Studio 的基本安装附带没有用于 Azure 开发的工具或库。 为此, 你需要包含 azure 开发工作负载, 其中包括 azure sdk、工具和模板项目。

若要安装 Visual Studio, 请[下载安装程序](https://visualstudio.microsoft.com/)。 安装程序将要求安装哪些工作负荷;你将指定 Azure 开发工作负载。 如果需要其他功能, 则通常通过 NuGet 包或 Visual Studio 扩展进行添加。

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

Visual Studio for Mac 是一个本机设计和开发的用于 macOS 的 IDE。 它允许您为 Android 和 iOS、web 和 .net Core 中的移动应用程序构建解决方案。

Visual Studio for Mac 的基本安装附带有 Azure 工具的上下文集成。 例如, 如果您要构建适用于 Android 的 Xamarin 应用程序, 则所包含的连接的服务模板将提供一个链接, 用于创建与 Azure 应用服务的移动后端。 如果要创建 Azure 函数, 则在云类别下有一个项目模板。

如果需要不在基本安装中的 Azure 功能和功能的工具, 您可能需要添加 NuGet 包或 Visual Studio for Mac 扩展。

若要安装 Visual Studio for Mac, 请[下载安装程序](https://visualstudio.microsoft.com/)。 安装程序将检查您的系统, 以确定需要更新的组件或需要更新的组件。

> [!NOTE]
> 系统可能会提示您在计算机上安装管理员凭据以安装某些组件。