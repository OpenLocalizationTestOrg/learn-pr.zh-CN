<span data-ttu-id="9529e-101">你已成功创建 web 应用并将其发布到 Azure, 但如果你想要进行更改, 会发生什么？</span><span class="sxs-lookup"><span data-stu-id="9529e-101">You've successfully created your web app and published it to Azure, but what happens when you want to make changes?</span></span> <span data-ttu-id="9529e-102">Visual Studio 会记住应用程序的发布位置, 这将更新和更改应用程序一次单击过程。</span><span class="sxs-lookup"><span data-stu-id="9529e-102">Visual Studio will remember where the app is published, which makes updating and changing your app a two-click process.</span></span>

## <a name="explore-the-project-structure"></a><span data-ttu-id="9529e-103">浏览项目结构</span><span class="sxs-lookup"><span data-stu-id="9529e-103">Explore the project structure</span></span>

<span data-ttu-id="9529e-104">我们已在 Visual Studio 中创建了一个 ASP.NET web 应用程序, 现在您需要编辑和自定义您的网站。</span><span class="sxs-lookup"><span data-stu-id="9529e-104">We've created an ASP.NET web app in Visual Studio, and now you will need to edit and customize your website.</span></span> <span data-ttu-id="9529e-105">让我们浏览项目结构, 以查看 Visual Studio 为我们创建的内容。</span><span class="sxs-lookup"><span data-stu-id="9529e-105">Let's explore the project structure to see what Visual Studio has created for us.</span></span>

### <a name="dependencies"></a><span data-ttu-id="9529e-106">依</span><span class="sxs-lookup"><span data-stu-id="9529e-106">Dependencies</span></span>

<span data-ttu-id="9529e-107">依赖项包括 ASP.NET 内部应用程序, 以使您的应用程序正常运行。</span><span class="sxs-lookup"><span data-stu-id="9529e-107">Dependencies include the ASP.NET internals to get your app up and running.</span></span> <span data-ttu-id="9529e-108">除非要添加特定的第三方包, 否则不需要在此文件夹中花费大量时间。</span><span class="sxs-lookup"><span data-stu-id="9529e-108">Unless you are adding specific third-party packages, you won't need to spend much time in this folder.</span></span>

### <a name="properties"></a><span data-ttu-id="9529e-109">属性</span><span class="sxs-lookup"><span data-stu-id="9529e-109">Properties</span></span>

<span data-ttu-id="9529e-110">"属性" 文件夹包含用于承载 web 应用的位置的配置数据。</span><span class="sxs-lookup"><span data-stu-id="9529e-110">The properties folder contains configuration data for where you are hosting your web app.</span></span> <span data-ttu-id="9529e-111">如果现在展开 " **PublishProfiles** " 文件夹, 您应该会看到 Alpine 滑雪峰网站的 URL。</span><span class="sxs-lookup"><span data-stu-id="9529e-111">If you expand the **PublishProfiles** folder now, you should see the URL for the Alpine Ski Hill site.</span></span> <span data-ttu-id="9529e-112">每个发布配置文件都是一个 .xml 文件, 其中包含发布配置信息, 如 Visual Studio 用于上传文件的 Azure 地址。</span><span class="sxs-lookup"><span data-stu-id="9529e-112">Each publishing profile is an .xml file containing publishing configuration information, such as the Azure address that Visual Studio uses to upload your files.</span></span>

### <a name="wwwroot"></a><span data-ttu-id="9529e-113">wwwroot</span><span class="sxs-lookup"><span data-stu-id="9529e-113">wwwroot</span></span>

<span data-ttu-id="9529e-114">wwwroot 文件包含网站的所有静态资产, 如 .css、.js、图像和 .lib 文件。</span><span class="sxs-lookup"><span data-stu-id="9529e-114">The wwwroot file contains all of your static assets for your site, such as the .css, .js, images, and .lib files.</span></span> <span data-ttu-id="9529e-115">当您准备好样式并向网站添加更多功能时, 您将在此处工作。</span><span class="sxs-lookup"><span data-stu-id="9529e-115">When you are ready to style and add more functionality to your site, you will work in here.</span></span>

### <a name="pages"></a><span data-ttu-id="9529e-116">页面</span><span class="sxs-lookup"><span data-stu-id="9529e-116">Pages</span></span>

<span data-ttu-id="9529e-117">"**页面**" 文件夹包括您的网站页面的_**Razor**_ 模板。</span><span class="sxs-lookup"><span data-stu-id="9529e-117">The **Pages** folder includes _**Razor**_ templates for the pages of your site.</span></span>
<span data-ttu-id="9529e-118">Razor 是围绕 HTML 构建的一种语法, 它具有在网站上显示数据和执行逻辑的特殊约定。</span><span class="sxs-lookup"><span data-stu-id="9529e-118">Razor is a syntax that is built up around HTML, which has special conventions for displaying data and executing logic on your site.</span></span>

<span data-ttu-id="9529e-119">网站中的每个页面都用两个代码文件表示:</span><span class="sxs-lookup"><span data-stu-id="9529e-119">Each page in your site is represented with two code files:</span></span>

- <span data-ttu-id="9529e-120">第一个是`.cshtml`文件, 它是 Razor 标记文件。</span><span class="sxs-lookup"><span data-stu-id="9529e-120">The first is a `.cshtml` file, which is the Razor markup file.</span></span> <span data-ttu-id="9529e-121">此文件包括您的显示 HTML 和一些 c # 逻辑。</span><span class="sxs-lookup"><span data-stu-id="9529e-121">This file includes your display HTML and some C# logic.</span></span>

- <span data-ttu-id="9529e-122">第二个文件是`.cs`一个文件, 它是包含`PageModel`类的 c # 代码隐藏。</span><span class="sxs-lookup"><span data-stu-id="9529e-122">The second file is a `.cs` file, which is the C# code-behind that includes `PageModel` class.</span></span> <span data-ttu-id="9529e-123">通过此文件, 您可以在将任何数据传递到 Razor 文件之前截获 HTTP 请求并对该请求执行某些处理。</span><span class="sxs-lookup"><span data-stu-id="9529e-123">This file allows you to intercept HTTP requests and do some processing on that request before passing off any data to the Razor file.</span></span>

### <a name="appsettingjson"></a><span data-ttu-id="9529e-124">appsetting</span><span class="sxs-lookup"><span data-stu-id="9529e-124">appsetting.json</span></span>

<span data-ttu-id="9529e-125">这是 ASP.NET 的配置文件。</span><span class="sxs-lookup"><span data-stu-id="9529e-125">This is a configuration file for ASP.NET.</span></span>

### <a name="bundleconfigjson"></a><span data-ttu-id="9529e-126">bundleconfig</span><span class="sxs-lookup"><span data-stu-id="9529e-126">bundleconfig.json</span></span>

<span data-ttu-id="9529e-127">bundleconfig 正在进行预处理配置。</span><span class="sxs-lookup"><span data-stu-id="9529e-127">The bundleconfig.json is preprocessing configuration.</span></span> <span data-ttu-id="9529e-128">此文件将使您的 .css 和 .js 文件在发布时变小。</span><span class="sxs-lookup"><span data-stu-id="9529e-128">This file is making your .css and .js files smaller when they are published.</span></span>

### <a name="programcs-and-startupcs"></a><span data-ttu-id="9529e-129">Program.cs 和 Startup.cs</span><span class="sxs-lookup"><span data-stu-id="9529e-129">Program.cs and Startup.cs</span></span>

<span data-ttu-id="9529e-130">Program.cs 和 Startup.cs 为您的网站配置并启动您的 web 主机。</span><span class="sxs-lookup"><span data-stu-id="9529e-130">Program.cs and Startup.cs configure and launch your web host for your site.</span></span>

## <a name="introduction-to-razor-templates"></a><span data-ttu-id="9529e-131">Razor 模板简介</span><span class="sxs-lookup"><span data-stu-id="9529e-131">Introduction to Razor templates</span></span>

<span data-ttu-id="9529e-132">我们将需要对我们的网站进行一些基本的更改。</span><span class="sxs-lookup"><span data-stu-id="9529e-132">We will want to make some basic changes to our website.</span></span> <span data-ttu-id="9529e-133">若要执行此操作, 您需要对如何利用 Razor 模板来自定义 web 应用有一个基本的了解。</span><span class="sxs-lookup"><span data-stu-id="9529e-133">In order to do this, you will need to have a basic understanding of how to leverage the Razor templates to customize your web app.</span></span>

## <a name="what-is-razor"></a><span data-ttu-id="9529e-134">什么是 Razor？</span><span class="sxs-lookup"><span data-stu-id="9529e-134">What is Razor?</span></span>

<span data-ttu-id="9529e-135">Razor 是用于使用 c # 创建动态网页的 ASP.NET 语法。</span><span class="sxs-lookup"><span data-stu-id="9529e-135">Razor is an ASP.NET syntax used to create dynamic web pages with C#.</span></span> <span data-ttu-id="9529e-136">当服务器读取 Razor 页时, c # 代码在呈现 HTML 之前运行。</span><span class="sxs-lookup"><span data-stu-id="9529e-136">When a server reads a Razor page, the C# code is run before it renders the HTML.</span></span> <span data-ttu-id="9529e-137">这使您可以快速生成动态内容。</span><span class="sxs-lookup"><span data-stu-id="9529e-137">This allows you to generate dynamic content quickly.</span></span>

<span data-ttu-id="9529e-138">Razor 使用`@`指令告诉 ASP.NET 如何处理页面。</span><span class="sxs-lookup"><span data-stu-id="9529e-138">Razor uses `@` directives to tell ASP.NET how to process a page.</span></span>

<span data-ttu-id="9529e-139">例如, 查看`Contact.cshtml`页面中的代码:</span><span class="sxs-lookup"><span data-stu-id="9529e-139">For example, take a look at the code in the `Contact.cshtml` page:</span></span>

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

- <span data-ttu-id="9529e-140">该`@page`指令指示 ASP.NET 将此文件作为 Razor 页处理。</span><span class="sxs-lookup"><span data-stu-id="9529e-140">The `@page` directive is telling ASP.NET to process this file as a Razor page.</span></span>
- <span data-ttu-id="9529e-141">该`@model`指令指示 ASP.NET 将此 Razor 页与名`ContactModel`为的 c # 类关联。</span><span class="sxs-lookup"><span data-stu-id="9529e-141">The `@model` directive is telling ASP.NET to tie this Razor page with a C# class called `ContactModel`.</span></span>

<span data-ttu-id="9529e-142">Razor 还使用`@`符号在代码和 HTML 之间转换。</span><span class="sxs-lookup"><span data-stu-id="9529e-142">Razor also uses the `@` symbol to transition between code and HTML.</span></span> <span data-ttu-id="9529e-143">如果你查看上面的代码段, 你会注意`@{ ... }`到。</span><span class="sxs-lookup"><span data-stu-id="9529e-143">If you look at the snippet above, you'll notice `@{ ... }`.</span></span> <span data-ttu-id="9529e-144">这是一个**Razor 代码块**。</span><span class="sxs-lookup"><span data-stu-id="9529e-144">This is a **Razor code block**.</span></span> <span data-ttu-id="9529e-145">它是已_执行但不呈现_的代码。</span><span class="sxs-lookup"><span data-stu-id="9529e-145">It's code which is _executed but not rendered_.</span></span>

<span data-ttu-id="9529e-146">若要呈现代码语句的输出, 我们使用`@` c # 表达式之前的。</span><span class="sxs-lookup"><span data-stu-id="9529e-146">To render the output of a code statement, we use the `@` in front of a C# expression.</span></span> <span data-ttu-id="9529e-147">在上面的代码块中, `<h2>`和`<h3>`标记中有两个示例。</span><span class="sxs-lookup"><span data-stu-id="9529e-147">We have two examples of that in the code block above in the `<h2>` and `<h3>` tags.</span></span>

<span data-ttu-id="9529e-148">创建和发布网站只是创建优质网站的首要步骤。</span><span class="sxs-lookup"><span data-stu-id="9529e-148">Creating and publishing a website are just the first steps in creating a good website.</span></span> <span data-ttu-id="9529e-149">开始添加内容后, 需要更新网站。</span><span class="sxs-lookup"><span data-stu-id="9529e-149">Once you start to add content, you'll need to update your site.</span></span> <span data-ttu-id="9529e-150">在你最初将网站发布到 Azure 后, 你可以随时进行更新。</span><span class="sxs-lookup"><span data-stu-id="9529e-150">Once you've initially published your site to Azure, you can update at any time.</span></span>
