你已成功创建 web 应用并将其发布到 Azure, 但如果你想要进行更改, 会发生什么？ Visual Studio 会记住应用程序的发布位置, 这将更新和更改应用程序一次单击过程。

## <a name="explore-the-project-structure"></a>浏览项目结构

我们已在 Visual Studio 中创建了一个 ASP.NET web 应用程序, 现在您需要编辑和自定义您的网站。 让我们浏览项目结构, 以查看 Visual Studio 为我们创建的内容。

### <a name="dependencies"></a>依

依赖项包括 ASP.NET 内部应用程序, 以使您的应用程序正常运行。 除非要添加特定的第三方包, 否则不需要在此文件夹中花费大量时间。

### <a name="properties"></a>属性

"属性" 文件夹包含用于承载 web 应用的位置的配置数据。 如果现在展开 " **PublishProfiles** " 文件夹, 您应该会看到 Alpine 滑雪峰网站的 URL。 每个发布配置文件都是一个 .xml 文件, 其中包含发布配置信息, 如 Visual Studio 用于上传文件的 Azure 地址。

### <a name="wwwroot"></a>wwwroot

wwwroot 文件包含网站的所有静态资产, 如 .css、.js、图像和 .lib 文件。 当您准备好样式并向网站添加更多功能时, 您将在此处工作。

### <a name="pages"></a>页面

"**页面**" 文件夹包括您的网站页面的_**Razor**_ 模板。
Razor 是围绕 HTML 构建的一种语法, 它具有在网站上显示数据和执行逻辑的特殊约定。

网站中的每个页面都用两个代码文件表示:

- 第一个是`.cshtml`文件, 它是 Razor 标记文件。 此文件包括您的显示 HTML 和一些 c # 逻辑。

- 第二个文件是`.cs`一个文件, 它是包含`PageModel`类的 c # 代码隐藏。 通过此文件, 您可以在将任何数据传递到 Razor 文件之前截获 HTTP 请求并对该请求执行某些处理。

### <a name="appsettingjson"></a>appsetting

这是 ASP.NET 的配置文件。

### <a name="bundleconfigjson"></a>bundleconfig

bundleconfig 正在进行预处理配置。 此文件将使您的 .css 和 .js 文件在发布时变小。

### <a name="programcs-and-startupcs"></a>Program.cs 和 Startup.cs

Program.cs 和 Startup.cs 为您的网站配置并启动您的 web 主机。

## <a name="introduction-to-razor-templates"></a>Razor 模板简介

我们将需要对我们的网站进行一些基本的更改。 若要执行此操作, 您需要对如何利用 Razor 模板来自定义 web 应用有一个基本的了解。

## <a name="what-is-razor"></a>什么是 Razor？

Razor 是用于使用 c # 创建动态网页的 ASP.NET 语法。 当服务器读取 Razor 页时, c # 代码在呈现 HTML 之前运行。 这使您可以快速生成动态内容。

Razor 使用`@`指令告诉 ASP.NET 如何处理页面。

例如, 查看`Contact.cshtml`页面中的代码:

```aspx-csharp
@page
@model ContactModel
@{
    ViewData["Title"] = "Contact";
}
<h2>@ViewData["Title"]</h2>
<h3>@Model.Message</h3>
...
```

- 该`@page`指令指示 ASP.NET 将此文件作为 Razor 页处理。
- 该`@model`指令指示 ASP.NET 将此 Razor 页与名`ContactModel`为的 c # 类关联。

Razor 还使用`@`符号在代码和 HTML 之间转换。 如果你查看上面的代码段, 你会注意`@{ ... }`到。 这是一个**Razor 代码块**。 它是已_执行但不呈现_的代码。

若要呈现代码语句的输出, 我们使用`@` c # 表达式之前的。 在上面的代码块中, `<h2>`和`<h3>`标记中有两个示例。

创建和发布网站只是创建优质网站的首要步骤。 开始添加内容后, 需要更新网站。 在你最初将网站发布到 Azure 后, 你可以随时进行更新。
