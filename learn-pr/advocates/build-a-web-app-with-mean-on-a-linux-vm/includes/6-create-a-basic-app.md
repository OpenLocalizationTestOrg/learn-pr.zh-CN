<span data-ttu-id="b667f-101">到目前为止, 你的 Ubuntu VM 上安装了 MongoDB 和 node.js。</span><span class="sxs-lookup"><span data-stu-id="b667f-101">So far, you have MongoDB and Node.js installed on your Ubuntu VM.</span></span> <span data-ttu-id="b667f-102">现在是时候创建基本 web 应用程序来查看操作中的内容。</span><span class="sxs-lookup"><span data-stu-id="b667f-102">Now it's time to create a basic web application to see things in action.</span></span> <span data-ttu-id="b667f-103">同时, 你将看到 "AngularJS" 和 "Express" 的匹配方式。</span><span class="sxs-lookup"><span data-stu-id="b667f-103">Along the way, you'll see how AngularJS and Express fit in.</span></span>

<span data-ttu-id="b667f-104">例如, 学习的一种非常好的方法。</span><span class="sxs-lookup"><span data-stu-id="b667f-104">A great way to learn is by example.</span></span> <span data-ttu-id="b667f-105">您将生成的 web 应用程序将实现基本书籍数据库。</span><span class="sxs-lookup"><span data-stu-id="b667f-105">The web application you'll build implements a basic book database.</span></span> <span data-ttu-id="b667f-106">通过 web 应用程序, 您可以列出有关书籍、添加新书籍和删除现有书籍的信息。</span><span class="sxs-lookup"><span data-stu-id="b667f-106">The web application enables you to list information about books, add new books, and delete existing books.</span></span>

<span data-ttu-id="b667f-107">你将在此处看到的 web 应用程序演示了许多适用于大多数平均堆栈 web 应用程序的概念。</span><span class="sxs-lookup"><span data-stu-id="b667f-107">The web application you'll see here demonstrates many concepts that apply to most MEAN stack web applications.</span></span> <span data-ttu-id="b667f-108">根据您的需求和兴趣, 您可以浏览构建自己的平均堆栈应用程序所需的功能。</span><span class="sxs-lookup"><span data-stu-id="b667f-108">Based on your needs and interests, you can explore the features you need to build your own MEAN stack applications.</span></span>

<span data-ttu-id="b667f-109">本书 web 应用程序的外观如下所示。</span><span class="sxs-lookup"><span data-stu-id="b667f-109">Here's what the Books web application will look like.</span></span>

![包含表单和提交按钮的网页。](../media/6-book-page.png)

<span data-ttu-id="b667f-111">下面介绍了每个平均堆栈的组件是如何适合的。</span><span class="sxs-lookup"><span data-stu-id="b667f-111">Here's how each component of the MEAN stack fits in.</span></span>

* <span data-ttu-id="b667f-112">MongoDB 存储书籍的相关信息。</span><span class="sxs-lookup"><span data-stu-id="b667f-112">MongoDB stores information about books.</span></span>
* <span data-ttu-id="b667f-113">Express 将每个 HTTP 请求路由到相应的处理程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-113">Express routes each HTTP request to the appropriate handler.</span></span>
* <span data-ttu-id="b667f-114">AngularJS 将用户界面与程序的业务逻辑连接。</span><span class="sxs-lookup"><span data-stu-id="b667f-114">AngularJS connects the user interface with the program's business logic.</span></span>
* <span data-ttu-id="b667f-115">node.js 承载服务器端应用程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-115">Node.js hosts the server-side application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b667f-116">出于学习目的, 您要构建基本的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-116">For learning purposes, here you're building a basic web application.</span></span> <span data-ttu-id="b667f-117">其目的是测试您的 "均值" 堆栈, 并让您了解它的工作原理。</span><span class="sxs-lookup"><span data-stu-id="b667f-117">Its purpose is to test out your MEAN stack and give you a sense of how it works.</span></span> <span data-ttu-id="b667f-118">应用程序不够安全或已准备好用于生产用途。</span><span class="sxs-lookup"><span data-stu-id="b667f-118">The application is not sufficiently secure or ready for production use.</span></span>

## <a name="what-about-express"></a><span data-ttu-id="b667f-119">什么是 Express？</span><span class="sxs-lookup"><span data-stu-id="b667f-119">What about Express?</span></span>

<span data-ttu-id="b667f-120">到目前为止, 你已在你的 VM 上安装 MongoDB 和 node.js。</span><span class="sxs-lookup"><span data-stu-id="b667f-120">So far, you've installed MongoDB and Node.js on your VM.</span></span> <span data-ttu-id="b667f-121">在平均首字母缩略词中, **E**是什么？</span><span class="sxs-lookup"><span data-stu-id="b667f-121">What about Express, the **E** in the MEAN acronym?</span></span>

<span data-ttu-id="b667f-122">Express 是为 node.js 构建的 web 服务器框架, 简化了构建 web 应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="b667f-122">Express is a web server framework that's built for Node.js that simplifies the process for building web applications.</span></span>

<span data-ttu-id="b667f-123">Express 的主要用途是处理请求路由。</span><span class="sxs-lookup"><span data-stu-id="b667f-123">The main purpose of Express is to handle request routing.</span></span> <span data-ttu-id="b667f-124">_路由_指的是应用程序如何响应对特定终结点的请求。</span><span class="sxs-lookup"><span data-stu-id="b667f-124">_Routing_ refers to how the application responds to a request to a specific endpoint.</span></span> <span data-ttu-id="b667f-125">终结点由路径或 URI 以及请求方法 (如 GET 或 POST) 组成。</span><span class="sxs-lookup"><span data-stu-id="b667f-125">An endpoint is made up of a path, or URI, and a request method, such as GET or POST.</span></span> <span data-ttu-id="b667f-126">例如, 您可以通过在数据库中提供所有书籍的`/book`列表来响应对终结点的 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="b667f-126">For example, you might respond to a GET request to the `/book` endpoint by providing the list of all books in the database.</span></span> <span data-ttu-id="b667f-127">您可以根据用户输入到 web 表单中的字段向数据库添加条目, 从而对同一终结点做出响应。</span><span class="sxs-lookup"><span data-stu-id="b667f-127">You might respond to a POST request to the same endpoint by adding an entry to the database based on fields the user entered into a web form.</span></span>

<span data-ttu-id="b667f-128">在您即将构建的 web 应用程序中, 您将使用 Express 路由 HTTP 请求, 并将 web 内容返回给您的用户。</span><span class="sxs-lookup"><span data-stu-id="b667f-128">In the web application you'll build shortly, you'll use Express to route HTTP requests and to return web content to your user.</span></span> <span data-ttu-id="b667f-129">Express 还可帮助 web 应用程序使用 HTTP cookie 和过程查询字符串。</span><span class="sxs-lookup"><span data-stu-id="b667f-129">Express can also help your web applications work with HTTP cookies and process query strings.</span></span>

<span data-ttu-id="b667f-130">Express 是 node.js 包。</span><span class="sxs-lookup"><span data-stu-id="b667f-130">Express is a Node.js package.</span></span> <span data-ttu-id="b667f-131">您可以使用**npm**实用工具 (与 node.js 一起提供) 来安装和管理 node.js 包。</span><span class="sxs-lookup"><span data-stu-id="b667f-131">You use the **npm** utility, which comes with Node.js, to install and manage Node.js packages.</span></span> <span data-ttu-id="b667f-132">稍后将在此部分中创建一个名`package.json`为的文件, 以定义 Express 和其他依赖项, `npm install`然后运行该命令以安装这些依赖项。</span><span class="sxs-lookup"><span data-stu-id="b667f-132">Later in this part, you'll create a file named `package.json` to define Express and other dependencies and then run the `npm install` command to install these dependencies.</span></span>

## <a name="what-about-angularjs"></a><span data-ttu-id="b667f-133">AngularJS？</span><span class="sxs-lookup"><span data-stu-id="b667f-133">What about AngularJS?</span></span>

<span data-ttu-id="b667f-134">与 Express 一样, 您尚未安装 AngularJS, 即 " **A" 作为**"平均值" 首字母缩写词。</span><span class="sxs-lookup"><span data-stu-id="b667f-134">Like Express, you haven't yet installed AngularJS, the **A** in the MEAN acronym.</span></span>

<span data-ttu-id="b667f-135">AngularJS 使 web 应用程序更易于编写和测试, 因为它使您能够更好地将网页的_外观_(HTML 代码) 与网页的行为进行区分。</span><span class="sxs-lookup"><span data-stu-id="b667f-135">AngularJS makes web applications easier to write and test because it enables you to better separate the _appearance_ of your web page, your HTML code, from how your web page behaves.</span></span> <span data-ttu-id="b667f-136">如果您熟悉模型– view – controller (MVC) 模式或数据绑定概念, 则 AngularJS 将对您很熟悉。</span><span class="sxs-lookup"><span data-stu-id="b667f-136">If you're familiar with the model–view–controller (MVC) pattern or the concept of data binding, AngularJS will be familiar to you.</span></span>

<span data-ttu-id="b667f-137">AngularJS 是所谓的前端 JavaScript 框架, 这意味着它只需要在访问应用程序的客户端上可用。</span><span class="sxs-lookup"><span data-stu-id="b667f-137">AngularJS is what's called a front-end JavaScript framework, which means it needs to only be available on the client that accesses the application.</span></span> <span data-ttu-id="b667f-138">换言之, AngularJS 在用户的 web 浏览器中运行, 而不是在 web 服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="b667f-138">In other words, AngularJS runs in your user's web browser, not on your web server.</span></span> <span data-ttu-id="b667f-139">由于 AngularJS 是 JavaScript, 因此您可以使用它轻松地从您的 web 服务器中获取数据, 以在页面上显示。</span><span class="sxs-lookup"><span data-stu-id="b667f-139">And because AngularJS is JavaScript, you can use it to easily fetch data from your web server to show on the page.</span></span>

<span data-ttu-id="b667f-140">您无实际_安装_AngularJS。</span><span class="sxs-lookup"><span data-stu-id="b667f-140">You don't really _install_ AngularJS.</span></span> <span data-ttu-id="b667f-141">而是在 HTML 页面中添加对 JavaScript 文件的引用, 就像对其他 JavaScript 库执行的操作一样。</span><span class="sxs-lookup"><span data-stu-id="b667f-141">Instead, you add a reference to the JavaScript file in your HTML page, just as you do with other JavaScript libraries.</span></span> <span data-ttu-id="b667f-142">有几种方法可在网页中添加 AngularJS。</span><span class="sxs-lookup"><span data-stu-id="b667f-142">There are several ways to include AngularJS in your web pages.</span></span> <span data-ttu-id="b667f-143">在这里, 你将从内容传递网络或 CDN 加载 AngularJS。</span><span class="sxs-lookup"><span data-stu-id="b667f-143">Here you'll load AngularJS from a content delivery network, or CDN.</span></span> <span data-ttu-id="b667f-144">CDN 是一种将图像、视频和其他内容分散在不同地理位置以提高下载速度的方法。</span><span class="sxs-lookup"><span data-stu-id="b667f-144">A CDN is a way to distribute images, video, and other content geographically to improve download speeds.</span></span>

<span data-ttu-id="b667f-145">请勿同时添加此代码, 但下面的示例展示了如何从 CDN 加载 AngularJS。</span><span class="sxs-lookup"><span data-stu-id="b667f-145">Don't add this code quite yet, but here's an example that loads AngularJS from a CDN.</span></span> <span data-ttu-id="b667f-146">通常将此代码添加到 HTML 页面`<head>`的部分。</span><span class="sxs-lookup"><span data-stu-id="b667f-146">You would typically add this code to the `<head>` section of your HTML page.</span></span>

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
```

> [!NOTE]
> <span data-ttu-id="b667f-147">请勿将 AngularJS 与角混淆。</span><span class="sxs-lookup"><span data-stu-id="b667f-147">Don't confuse AngularJS with Angular.</span></span> <span data-ttu-id="b667f-148">虽然其中的许多概念在两者之间相似, 但 AngularJS 是角度的前置任务。</span><span class="sxs-lookup"><span data-stu-id="b667f-148">While many of the concepts are similar between the two, AngularJS is the predecessor to Angular.</span></span> <span data-ttu-id="b667f-149">AngularJS 仍通常用于构建 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-149">AngularJS is still commonly used for building web applications.</span></span> <span data-ttu-id="b667f-150">尽管 AngularJS 基于 JavaScript, 但角度是基于 TypeScript, 这种编程语言使编写 JavaScript 程序更为简单。</span><span class="sxs-lookup"><span data-stu-id="b667f-150">While AngularJS is based on JavaScript, Angular is based on TypeScript, a programming language that makes it easier to write JavaScript programs.</span></span>

## <a name="how-will-i-build-the-application"></a><span data-ttu-id="b667f-151">我将如何构建应用程序？</span><span class="sxs-lookup"><span data-stu-id="b667f-151">How will I build the application?</span></span>

<span data-ttu-id="b667f-152">在这里, 你将使用一个基本过程。</span><span class="sxs-lookup"><span data-stu-id="b667f-152">Here you'll use a basic process.</span></span> <span data-ttu-id="b667f-153">你将从云命令行管理程序编写应用程序代码, 然后使用 SCP 或安全复制协议将文件复制到 VM。</span><span class="sxs-lookup"><span data-stu-id="b667f-153">You'll write application code from Cloud Shell and then use SCP, or secure copy protocol, to copy the files to your VM.</span></span> <span data-ttu-id="b667f-154">然后, 启动 node.js 应用程序, 并在浏览器中查看结果。</span><span class="sxs-lookup"><span data-stu-id="b667f-154">Then you'll start the Node.js application and see the results in your browser.</span></span>

<span data-ttu-id="b667f-155">在实践中, 通常会在更多的本地环境中编写和测试 web 应用程序, 例如从便携式计算机或本地运行的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b667f-155">In practice, you would typically write and test your web application in a more local environment, such as from your laptop or from a virtual machine you run locally.</span></span> <span data-ttu-id="b667f-156">然后, 您可以将代码存储在一个修订版控制系统 (如 Git) 中, 并使用连续集成和连续传递, 或者 CI/CD、系统 (如 Azure DevOps) 测试您的更改并将其上传到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="b667f-156">You might then store your code in a revision control system such as Git and use a continuous integration and continuous delivery, or CI/CD, system such as Azure DevOps to test your changes and upload them to your VM.</span></span> <span data-ttu-id="b667f-157">我们将指向本模块结尾的更多资源。</span><span class="sxs-lookup"><span data-stu-id="b667f-157">We'll point you to more resources at the end of this module.</span></span>

## <a name="create-the-books-web-application"></a><span data-ttu-id="b667f-158">创建书籍 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="b667f-158">Create the Books web application</span></span>

<span data-ttu-id="b667f-159">在这里, 你将创建构成 web 应用程序的所有代码、脚本和 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="b667f-159">Here you'll create all the code, script, and HTML files that make up your web application.</span></span> <span data-ttu-id="b667f-160">为简洁起见, 我们将重点介绍每个文件的重要部分, 但不会深入了解全部详细信息。</span><span class="sxs-lookup"><span data-stu-id="b667f-160">For brevity, we'll highlight the important parts of each file but won't go into complete details.</span></span>

<span data-ttu-id="b667f-161">如果仍通过 SSH 连接到 VM, 请运行`exit`以离开 ssh 会话并返回云命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-161">If you're still connected to your VM over SSH, run `exit` to leave the SSH session and return to Cloud Shell.</span></span>

```bash
exit
```

<span data-ttu-id="b667f-162">你现在将回到云 Shell 会话。</span><span class="sxs-lookup"><span data-stu-id="b667f-162">You're now back at your Cloud Shell session.</span></span>

### <a name="create-the-files"></a><span data-ttu-id="b667f-163">创建文件</span><span class="sxs-lookup"><span data-stu-id="b667f-163">Create the files</span></span>

1. <span data-ttu-id="b667f-164">从云命令行管理程序运行这些命令, 为 web 应用程序创建文件夹和文件。</span><span class="sxs-lookup"><span data-stu-id="b667f-164">From Cloud Shell, run these commands to create the folders and files for your web application.</span></span>

    ```bash
    cd ~
    mkdir Books
    touch Books/server.js
    touch Books/package.json
    mkdir Books/app
    touch Books/app/model.js
    touch Books/app/routes.js
    mkdir Books/public
    touch Books/public/script.js
    touch Books/public/index.html
    ```

    <span data-ttu-id="b667f-165">其中包括以下 what's:</span><span class="sxs-lookup"><span data-stu-id="b667f-165">Here's what's included:</span></span>

    * <span data-ttu-id="b667f-166">`Books`&ndash;项目的根目录。</span><span class="sxs-lookup"><span data-stu-id="b667f-166">`Books` &ndash; the project's root directory.</span></span>
      * <span data-ttu-id="b667f-167">`server.js`定义 web 应用程序的入口点。</span><span class="sxs-lookup"><span data-stu-id="b667f-167">`server.js` defines the entry point to the web application.</span></span> <span data-ttu-id="b667f-168">它加载所需的 node.js 包, 指定要侦听的端口, 并开始侦听传入的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="b667f-168">It loads the required Node.js packages, specifies the port to listen on, and begins listening for incoming HTTP traffic.</span></span>
      * <span data-ttu-id="b667f-169">`package.json`提供有关应用程序的信息, 包括其名称、说明以及应用程序需要运行的 node.js 包。</span><span class="sxs-lookup"><span data-stu-id="b667f-169">`package.json` provides information about your application, including its name, description, and what Node.js packages your application needs to run.</span></span>
    * <span data-ttu-id="b667f-170">`Books/app`&ndash;包含在服务器上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="b667f-170">`Books/app` &ndash; contains code that runs on the server.</span></span>
      * <span data-ttu-id="b667f-171">`model.js`定义数据库连接和架构。</span><span class="sxs-lookup"><span data-stu-id="b667f-171">`model.js` defines the database connection and schema.</span></span> <span data-ttu-id="b667f-172">将其视为应用程序的数据模型。</span><span class="sxs-lookup"><span data-stu-id="b667f-172">Think of it as the data model for your application.</span></span>
      * <span data-ttu-id="b667f-173">`routes.js`处理请求路由。</span><span class="sxs-lookup"><span data-stu-id="b667f-173">`routes.js` handles request routing.</span></span> <span data-ttu-id="b667f-174">例如, 它通过提供数据库中所有书籍`/book`的列表来定义对终结点的 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="b667f-174">For example, it defines GET requests to the `/book` endpoint by providing the list of all books in the database.</span></span>
    * <span data-ttu-id="b667f-175">`Books/public`&ndash;包含直接提供给客户端浏览器的文件。</span><span class="sxs-lookup"><span data-stu-id="b667f-175">`Books/public` &ndash; contains files that are served directly to the client's browser.</span></span>
      * <span data-ttu-id="b667f-176">`index.html`包含索引页。</span><span class="sxs-lookup"><span data-stu-id="b667f-176">`index.html` contains the index page.</span></span> <span data-ttu-id="b667f-177">它包含一个 web 表单, 用户可以通过它提交书籍的相关信息。</span><span class="sxs-lookup"><span data-stu-id="b667f-177">It contains a web form that enables the user to submit information about books.</span></span> <span data-ttu-id="b667f-178">它还显示数据库中的所有书籍, 并使您可以从数据库中删除条目。</span><span class="sxs-lookup"><span data-stu-id="b667f-178">It also displays all books in the database and enables you to delete entries from the database.</span></span>
      * <span data-ttu-id="b667f-179">`script.js`包含在用户浏览器中运行的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="b667f-179">`script.js` contains JavaScript code that runs in your user's browser.</span></span> <span data-ttu-id="b667f-180">它可以向服务器发送请求, 以列出书籍、向数据库添加书籍以及从数据库中删除书籍。</span><span class="sxs-lookup"><span data-stu-id="b667f-180">It can send requests to the server to list books, add books to the database, and delete books from the database.</span></span>

1. <span data-ttu-id="b667f-181">运行`code`命令以通过云命令行管理程序编辑器打开文件。</span><span class="sxs-lookup"><span data-stu-id="b667f-181">Run the `code` command to open your files through the Cloud Shell editor.</span></span>

    ```bash
    code Books
    ```

### <a name="create-the-data-model"></a><span data-ttu-id="b667f-182">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="b667f-182">Create the data model</span></span>

1. <span data-ttu-id="b667f-183">在编辑器中, 打开`app/model.js`并添加以下项。</span><span class="sxs-lookup"><span data-stu-id="b667f-183">From the editor, open `app/model.js` and add the following.</span></span>

    ```javascript
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/Books';
    mongoose.connect(dbHost, { useNewUrlParser: true } );
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
        name: String,
        isbn: {type: String, index: true},
        author: String,
        pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = Book;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b667f-184">只要您将代码粘贴或更改为编辑器中的文件, 就一定要使用 "..." 进行保存。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Command + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="b667f-184">Whenever you paste or change code into a file in the editor, make sure to save afterwards using the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Command+S</kbd> on macOS).</span></span>

    <span data-ttu-id="b667f-185">此代码使用 Mongoose 简化在 MongoDB 中传输数据的过程。</span><span class="sxs-lookup"><span data-stu-id="b667f-185">This code uses Mongoose to simplify the process of transferring data in and out of MongoDB.</span></span> <span data-ttu-id="b667f-186">Mongoose 是一个基于架构的数据建模系统。</span><span class="sxs-lookup"><span data-stu-id="b667f-186">Mongoose is a schema-based system for modeling data.</span></span>

    <span data-ttu-id="b667f-187">此代码将连接到本地 MongoDB 服务器上名为 "书籍" 的数据库。</span><span class="sxs-lookup"><span data-stu-id="b667f-187">This code connects to a database named "Books" on the local MongoDB server.</span></span> <span data-ttu-id="b667f-188">然后, 它使用提供的架构定义名为 "Book" 的数据库文档。</span><span class="sxs-lookup"><span data-stu-id="b667f-188">It then defines a database document called "Book" with the provided schema.</span></span> <span data-ttu-id="b667f-189">架构定义了四个字段, 用于描述一本书:</span><span class="sxs-lookup"><span data-stu-id="b667f-189">The schema defines four fields that describe a single book:</span></span>

    * <span data-ttu-id="b667f-190">书籍的名称或职务</span><span class="sxs-lookup"><span data-stu-id="b667f-190">The book's name, or title</span></span>
    * <span data-ttu-id="b667f-191">其国际标准书籍编号, 或可唯一标识书籍的 ISBN</span><span class="sxs-lookup"><span data-stu-id="b667f-191">Its International Standard Book Number, or ISBN, which uniquely identifies the book</span></span>
    * <span data-ttu-id="b667f-192">其作者</span><span class="sxs-lookup"><span data-stu-id="b667f-192">Its author</span></span>
    * <span data-ttu-id="b667f-193">它所包含的页面数</span><span class="sxs-lookup"><span data-stu-id="b667f-193">The number of pages it contains</span></span>

    <span data-ttu-id="b667f-194">接下来, 将创建用于将 GET、POST 和 DELETE 请求映射到数据库操作的 HTTP 处理程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-194">Next, you'll create HTTP handlers that map GET, POST, and DELETE requests to database operations.</span></span>

### <a name="create-the-express-routes-that-handle-http-requests"></a><span data-ttu-id="b667f-195">创建处理 HTTP 请求的 Express 路由</span><span class="sxs-lookup"><span data-stu-id="b667f-195">Create the Express routes that handle HTTP requests</span></span>

1. <span data-ttu-id="b667f-196">在编辑器中, 打开`app/routes.js`并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="b667f-196">From the editor, open `app/routes.js` and add the following code.</span></span>

    ```javascript
    var path = require('path');
    var Book = require('./model');
    var routes = function(app) {
        app.get('/book', function(req, res) {
            Book.find({}, function(err, result) {
                if ( err ) throw err;
                res.json(result);
            });
        });
        app.post('/book', function(req, res) {
            var book = new Book( {
                name:req.body.name,
                isbn:req.body.isbn,
                author:req.body.author,
                pages:req.body.pages
            });
            book.save(function(err, result) {
                if ( err ) throw err;
                res.json( {
                    message:"Successfully added book",
                    book:result
                });
            });
        });
        app.delete("/book/:isbn", function(req, res) {
            Book.findOneAndRemove(req.query, function(err, result) {
                if ( err ) throw err;
                res.json( {
                    message: "Successfully deleted the book",
                    book: result
                });
            });
        });
        app.get('*', function(req, res) {
            res.sendFile(path.join(__dirname + '/public', 'index.html'));
        });
    };
    module.exports = routes;
    ```

    <span data-ttu-id="b667f-197">此代码将为应用程序创建四个路由。</span><span class="sxs-lookup"><span data-stu-id="b667f-197">This code creates four routes for the application.</span></span> <span data-ttu-id="b667f-198">以下是每个主题的简要概述。</span><span class="sxs-lookup"><span data-stu-id="b667f-198">Here's a brief overview of each.</span></span>

    | <span data-ttu-id="b667f-199">HTTP 谓词</span><span class="sxs-lookup"><span data-stu-id="b667f-199">HTTP verb</span></span> | <span data-ttu-id="b667f-200">Endpoint</span><span class="sxs-lookup"><span data-stu-id="b667f-200">Endpoint</span></span>      | <span data-ttu-id="b667f-201">说明</span><span class="sxs-lookup"><span data-stu-id="b667f-201">Description</span></span>                                                                                                           |
    |-----------|---------------|-----------------------------------------------------------------------------------------------------------------------|
    | <span data-ttu-id="b667f-202">GET</span><span class="sxs-lookup"><span data-stu-id="b667f-202">GET</span></span>       | `/book`       | <span data-ttu-id="b667f-203">检索数据库中的所有书籍。</span><span class="sxs-lookup"><span data-stu-id="b667f-203">Retrieves all books from the database.</span></span>                                                                                |
    | <span data-ttu-id="b667f-204">POST</span><span class="sxs-lookup"><span data-stu-id="b667f-204">POST</span></span>      | `/book`       | <span data-ttu-id="b667f-205">根据用户`Book`在 web 表单上提供的字段创建对象, 并将该对象写入数据库。</span><span class="sxs-lookup"><span data-stu-id="b667f-205">Creates a `Book` object based on the fields the user provided on the web form and writes that object to the database.</span></span> |
    | <span data-ttu-id="b667f-206">删除</span><span class="sxs-lookup"><span data-stu-id="b667f-206">DELETE</span></span>    | `/book/:isbn` | <span data-ttu-id="b667f-207">从数据库中删除由其 ISBN 标识的书籍。</span><span class="sxs-lookup"><span data-stu-id="b667f-207">Deletes the book as identified by its ISBN from the database.</span></span>                                                         |
    | <span data-ttu-id="b667f-208">GET</span><span class="sxs-lookup"><span data-stu-id="b667f-208">GET</span></span>       | `*`           | <span data-ttu-id="b667f-209">当没有匹配的其他路由时, 返回索引页。</span><span class="sxs-lookup"><span data-stu-id="b667f-209">Returns the index page when no other route is matched.</span></span>                                                                |

    <span data-ttu-id="b667f-210">Express 可以直接在路由处理代码中提供 HTTP 响应, 也可以提供来自文件的静态内容。</span><span class="sxs-lookup"><span data-stu-id="b667f-210">Express can serve up HTTP responses directly in the route handling code or it can serve up static content from files.</span></span> <span data-ttu-id="b667f-211">此代码显示了这两种情况。</span><span class="sxs-lookup"><span data-stu-id="b667f-211">This code shows both.</span></span> <span data-ttu-id="b667f-212">前三个路由为 book API 请求返回 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="b667f-212">The first three routes return JSON data for book API requests.</span></span> <span data-ttu-id="b667f-213">第四个路由 (默认情况下) 返回索引文件的内容`index.html`。</span><span class="sxs-lookup"><span data-stu-id="b667f-213">The fourth route (the default case) returns the contents of the index file, `index.html`.</span></span>

### <a name="create-the-client-side-javascript-application"></a><span data-ttu-id="b667f-214">创建客户端 JavaScript 应用程序</span><span class="sxs-lookup"><span data-stu-id="b667f-214">Create the client-side JavaScript application</span></span>

1. <span data-ttu-id="b667f-215">在编辑器中, 打开`public/script.js`并添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="b667f-215">From the editor, open `public/script.js` and add this code:</span></span>

    ```javascript
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
        var getData = function() {
            return $http( {
                method: 'GET',
                url: '/book'
            }).then(function successCallback(response) {
                $scope.books = response.data;
            }, function errorCallback(response) {
                console.log('Error: ' + response);
            });
        };
        getData();
        $scope.del_book = function(book) {
            $http( {
                method: 'DELETE',
                url: '/book/:isbn',
                params: {'isbn': book.isbn}
            }).then(function successCallback(response) {
                console.log(response);
                return getData();
            }, function errorCallback(response) {
                console.log('Error: ' + response);
            });
        };
        $scope.add_book = function() {
            var body = '{ "name": "' + $scope.Name +
            '", "isbn": "' + $scope.Isbn +
            '", "author": "' + $scope.Author +
            '", "pages": "' + $scope.Pages + '" }';
            $http({
                method: 'POST',
                url: '/book',
                data: body
            }).then(function successCallback(response) {
                console.log(response);
                return getData();
            }, function errorCallback(response) {
                console.log('Error: ' + response);
            });
        };
    });
    ```

    <span data-ttu-id="b667f-216">请注意, 此代码如何定义名为 "myApp" 的模块和名为 "myCtrl" 的控制器。</span><span class="sxs-lookup"><span data-stu-id="b667f-216">Notice how this code defines a module named "myApp" and a controller named "myCtrl".</span></span> <span data-ttu-id="b667f-217">我们不会详细介绍模块和控制器在这里如何工作, 但在下一步中将使用这些名称将用户界面 (HTML 代码) 与应用程序的业务逻辑绑定在一起。</span><span class="sxs-lookup"><span data-stu-id="b667f-217">We won't go into full details about how module and controllers work here, but you'll use these names in the next step to bind the user interface (HTML code) with the application's business logic.</span></span>

    <span data-ttu-id="b667f-218">之前, 您创建了四个在服务器上处理各种 GET、POST 和 DELETE 操作的路由。</span><span class="sxs-lookup"><span data-stu-id="b667f-218">Earlier, you created four routes that handle various GET, POST, and DELETE operations on the server.</span></span> <span data-ttu-id="b667f-219">此代码类似于这些相同的操作, 但来自客户端 (用户的 web 浏览器)。</span><span class="sxs-lookup"><span data-stu-id="b667f-219">This code resembles those same operations, but from the client side (the user's web browser).</span></span>

    <span data-ttu-id="b667f-220">例如`getData` , 函数将 GET 请求发送到`/book`终结点。</span><span class="sxs-lookup"><span data-stu-id="b667f-220">The `getData` function, for example, sends a GET request to the `/book` endpoint.</span></span> <span data-ttu-id="b667f-221">请记住, 服务器通过从数据库中检索有关所有书籍的信息并将该信息作为 JSON 数据返回来处理此请求。</span><span class="sxs-lookup"><span data-stu-id="b667f-221">Recall that the server handles this request by retrieving information about all books from the database and returning that information as JSON data.</span></span> <span data-ttu-id="b667f-222">请注意生成的 JSON 数据是如何分配给`$scope.books`变量的。</span><span class="sxs-lookup"><span data-stu-id="b667f-222">Notice how the resulting JSON data is assigned to the `$scope.books` variable.</span></span> <span data-ttu-id="b667f-223">在下一步中, 您将了解到这会如何影响用户在网页上看到的内容。</span><span class="sxs-lookup"><span data-stu-id="b667f-223">You'll see how this affects what the user sees on the web page in the next step.</span></span>

    <span data-ttu-id="b667f-224">此代码在页面`getData`加载时调用函数。</span><span class="sxs-lookup"><span data-stu-id="b667f-224">This code calls the `getData` function when the page loads.</span></span> <span data-ttu-id="b667f-225">您可以检查`del_book`和`add_book`函数, 以了解它们的工作方式。</span><span class="sxs-lookup"><span data-stu-id="b667f-225">You can examine the `del_book` and `add_book` functions to get a sense for how they work.</span></span> <span data-ttu-id="b667f-226">您不需要客户端代码来匹配服务器的默认处理程序, 因为默认处理程序返回的是索引页而不是 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="b667f-226">You don't need client-side code to match the server's default handler because the default handler returns the index page and not JSON data.</span></span>

### <a name="create-the-user-interface"></a><span data-ttu-id="b667f-227">创建用户界面</span><span class="sxs-lookup"><span data-stu-id="b667f-227">Create the user interface</span></span>

1. <span data-ttu-id="b667f-228">在编辑器中, 打开`public/index.html`并添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="b667f-228">From the editor, open `public/index.html` and add this code:</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
        <script src="script.js"></script>
    </head>
    <body>
        <div>
        <table>
            <tr>
            <td>Name:</td>
            <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
            <td>Isbn:</td>
            <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
            <td>Author:</td>
            <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
            <td>Pages:</td>
            <td><input type="number" ng-model="Pages"></td>
            </tr>
        </table>
        <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
        <table>
            <tr>
            <th>Name</th>
            <th>Isbn</th>
            <th>Author</th>
            <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
            <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
            <td>{{book.name}}</td>
            <td>{{book.isbn}}</td>
            <td>{{book.author}}</td>
            <td>{{book.pages}}</td>
            </tr>
        </table>
        </div>
    </body>
    </html>
    ```

    <span data-ttu-id="b667f-229">此代码创建一个具有四个字段的基本 HTML 窗体, 用于提交书籍数据和一个显示存储在数据库中的所有书籍的表格。</span><span class="sxs-lookup"><span data-stu-id="b667f-229">This code creates a basic HTML form with four fields to submit book data and a table that displays all the books stored in the database.</span></span>

    <span data-ttu-id="b667f-230">虽然这是标准 html 代码, 但`ng-` HTML 属性可能对您不熟悉。</span><span class="sxs-lookup"><span data-stu-id="b667f-230">Although this is standard HTML code, the `ng-` HTML attributes may be unfamiliar to you.</span></span> <span data-ttu-id="b667f-231">这些 HTML 属性将 AngularJS 代码与用户界面线对齐。</span><span class="sxs-lookup"><span data-stu-id="b667f-231">These HTML attributes wire up the AngularJS code to the user interface.</span></span> <span data-ttu-id="b667f-232">例如, 当用户单击 "**添加**" 按钮时, AngularJS 将`add_book`调用函数, 该函数将表单数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="b667f-232">For example, when the user clicks the **Add** button, AngularJS calls the `add_book` function, which sends the form data to the server.</span></span>

    <span data-ttu-id="b667f-233">您可以查看此处的代码, 了解每个`ng-`属性与应用程序的业务逻辑的关系。</span><span class="sxs-lookup"><span data-stu-id="b667f-233">You can examine the code here to get a sense of how each of the `ng-` attributes relate to application's business logic.</span></span>

### <a name="create-the-express-server-to-host-the-application"></a><span data-ttu-id="b667f-234">创建用于承载应用程序的 Express 服务器</span><span class="sxs-lookup"><span data-stu-id="b667f-234">Create the Express server to host the application</span></span>

1. <span data-ttu-id="b667f-235">在编辑器中, 打开`server.js`并添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="b667f-235">From the editor, open `server.js` and add this code:</span></span>

    ```javascript
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./app/routes')(app);
    app.set('port', 80);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

    <span data-ttu-id="b667f-236">此代码将创建 web 应用程序本身。</span><span class="sxs-lookup"><span data-stu-id="b667f-236">This code creates the web application itself.</span></span> <span data-ttu-id="b667f-237">它提供目录中的`public`静态文件, 并使用您在之前定义的路由来处理请求。</span><span class="sxs-lookup"><span data-stu-id="b667f-237">It serves static files from the `public` directory and uses the routes you defined in previously to handle requests.</span></span>

### <a name="define-package-information-and-dependencies"></a><span data-ttu-id="b667f-238">定义包信息和依赖项</span><span class="sxs-lookup"><span data-stu-id="b667f-238">Define package information and dependencies</span></span>

<span data-ttu-id="b667f-239">召回, `package.json`提供有关应用程序的信息, 包括其名称、说明以及应用程序需要运行的 node.js 包。</span><span class="sxs-lookup"><span data-stu-id="b667f-239">Recall that `package.json` provides information about your application, including its name, description, and what Node.js packages your application needs to run.</span></span>

1. <span data-ttu-id="b667f-240">在编辑器中, 打开`package.json`并添加以下代码:</span><span class="sxs-lookup"><span data-stu-id="b667f-240">From the editor, open `package.json` and add this code:</span></span>

    ```json
    {
      "name": "books",
      "description": "Sample web app that manages book information.",
      "license": "MIT",
      "repository": {
        "type": "git",
        "url": "https://github.com/MicrosoftDocs/mslearn-build-a-web-app-with-mean-on-a-linux-vm"
      },
      "main": "server.js",
      "dependencies": {
        "express": "~4.16",
        "mongoose": "~5.3",
        "body-parser": "~1.18"
      }
    }
    ```

<span data-ttu-id="b667f-241">您将看到有关您的应用程序的信息或元数据, 包括其名称、说明和许可证。</span><span class="sxs-lookup"><span data-stu-id="b667f-241">You see information, or metadata, about your application including its name, description, and license.</span></span>

<span data-ttu-id="b667f-242">该`repository`字段指定维护代码的位置。</span><span class="sxs-lookup"><span data-stu-id="b667f-242">The `repository` field specifies where the code is maintained.</span></span> <span data-ttu-id="b667f-243">若要进行参考, 可以稍后在 GitHub 上查看 GitHub 上的代码, 网址为此处显示的 URL。</span><span class="sxs-lookup"><span data-stu-id="b667f-243">For reference, you can later review the code on GitHub at the URL shown here.</span></span>

<span data-ttu-id="b667f-244">`main`字段定义应用程序的入口点。</span><span class="sxs-lookup"><span data-stu-id="b667f-244">The `main` field defines the application's entry point.</span></span> <span data-ttu-id="b667f-245">此处提供了完整的完整性, 但并不重要, 因为您不打算将应用程序作为 node.js 程序包发布, 以供其他人下载和使用。</span><span class="sxs-lookup"><span data-stu-id="b667f-245">It's provided here for completeness but it's not important because you're not planning to publish your application as a Node.js package for others to download and use.</span></span>

<span data-ttu-id="b667f-246">`dependencies`字段很重要。</span><span class="sxs-lookup"><span data-stu-id="b667f-246">The `dependencies` field is important.</span></span> <span data-ttu-id="b667f-247">它定义您的应用程序需要的 node.js 包。</span><span class="sxs-lookup"><span data-stu-id="b667f-247">It defines the Node.js packages your application needs.</span></span> <span data-ttu-id="b667f-248">稍后, 你将很快连接到 VM 并运行`npm install`命令以安装这些程序包。</span><span class="sxs-lookup"><span data-stu-id="b667f-248">Shortly, you'll connect to your VM a second time and run the `npm install` command to install these packages.</span></span>

<span data-ttu-id="b667f-249">节点包通常使用[语义版本](https://semver.org?azure-portal=true)控制版本化方案。</span><span class="sxs-lookup"><span data-stu-id="b667f-249">Node packages typically use the [Semantic Versioning](https://semver.org?azure-portal=true) versioning scheme.</span></span> <span data-ttu-id="b667f-250">版本号包含三个组件: 主要版本、次要版本和修补程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-250">The version number contains three components: major version, minor version, and patch.</span></span> <span data-ttu-id="b667f-251">此处的`~`波形符表示法告诉 npm 在提供的主要版本和次要版本下安装最新的修补程序版本。</span><span class="sxs-lookup"><span data-stu-id="b667f-251">The tilde `~` notation here tells npm to install the latest patch version under the provided major and minor versions.</span></span> <span data-ttu-id="b667f-252">您在此处看到的版本是使用此模块测试的最新版本。</span><span class="sxs-lookup"><span data-stu-id="b667f-252">The versions you see here are the latest this module was tested with.</span></span> <span data-ttu-id="b667f-253">实际上, 在您更新和测试应用程序以使用每个相关包提供的最新功能时, 您可以随着时间的推移增加版本。</span><span class="sxs-lookup"><span data-stu-id="b667f-253">In practice, you can increment the version over time as you update and test your application to use the latest features each dependent package provides.</span></span>

### <a name="copy-the-files-to-your-vm"></a><span data-ttu-id="b667f-254">将文件复制到 VM</span><span class="sxs-lookup"><span data-stu-id="b667f-254">Copy the files to your VM</span></span>

1. <span data-ttu-id="b667f-255">你已完成编辑文件。</span><span class="sxs-lookup"><span data-stu-id="b667f-255">You're all done editing files.</span></span> <span data-ttu-id="b667f-256">确保您已保存对每个文件的更改, 然后关闭编辑器。</span><span class="sxs-lookup"><span data-stu-id="b667f-256">Ensure that you saved changes to each file and then close the editor.</span></span>

    <span data-ttu-id="b667f-257">若要关闭编辑器, 请单击角上的省略号, 然后选择 "**关闭编辑器**"。</span><span class="sxs-lookup"><span data-stu-id="b667f-257">To close the editor, click the ellipses in the corner and then select **Close Editor**.</span></span>

1. <span data-ttu-id="b667f-258">运行以下`scp`命令, 将云命令行管理程序`~/Books`会话中目录的内容复制到 VM 上的相同目录名称中。</span><span class="sxs-lookup"><span data-stu-id="b667f-258">Run the following `scp` command to copy the contents of the `~/Books` directory in your Cloud Shell session to the same directory name on your VM.</span></span>

    ```bash
    scp -r ~/Books azureuser@$ipaddress:~/Books
    ```

## <a name="install-additional-node-packages"></a><span data-ttu-id="b667f-259">安装其他节点程序包</span><span class="sxs-lookup"><span data-stu-id="b667f-259">Install additional Node packages</span></span>

<span data-ttu-id="b667f-260">假设在开发过程中, 您标识了要使用的其他节点包。</span><span class="sxs-lookup"><span data-stu-id="b667f-260">Let's say that during the development process, you identified additional Node packages that you want to use.</span></span> <span data-ttu-id="b667f-261">例如, 从该行开始`app/model.js`的回忆。</span><span class="sxs-lookup"><span data-stu-id="b667f-261">For example, recall that `app/model.js` starts with this line.</span></span>

```javascript
var mongoose = require('mongoose');
```

<span data-ttu-id="b667f-262">请记住, 应用程序使用 Mongoose 帮助将数据传入和传出 MongoDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="b667f-262">Recall that the application uses Mongoose to help transfer data in and out of your MongoDB database.</span></span>

<span data-ttu-id="b667f-263">应用程序还需要 Express 和 body 分析器包。</span><span class="sxs-lookup"><span data-stu-id="b667f-263">The application also requires Express and the body-parser packages.</span></span> <span data-ttu-id="b667f-264">body-parser 是一个插件, 它使 Express 能够使用客户端发送的 web 表单中的数据。</span><span class="sxs-lookup"><span data-stu-id="b667f-264">body-parser is a plugin that enables Express to work with data from the web form sent by the client.</span></span>

<span data-ttu-id="b667f-265">让我们连接到你的 VM 并安装你在中`package.json`指定的程序包。</span><span class="sxs-lookup"><span data-stu-id="b667f-265">Let's connect to your VM and install the packages you specified in `package.json`.</span></span>

1. <span data-ttu-id="b667f-266">在连接到你的 vm 之前, 请确保你具有自己的 vm 的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b667f-266">Before you connect to your VM, make sure you have your VM's IP address handy.</span></span> <span data-ttu-id="b667f-267">如果没有, 请从云命令行管理程序中运行这些命令以进行检索。</span><span class="sxs-lookup"><span data-stu-id="b667f-267">If you don't have it, run these commands from Cloud Shell to retrieve it.</span></span>

    ```azurecli
    ipaddress=$(az vm show \
      --name MeanStack \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --show-details \
      --query [publicIps] \
      --output tsv)
    ```

    ```bash
    echo $ipaddress
    ```

1. <span data-ttu-id="b667f-268">正如您之前所做的那样, 请创建到你的 VM 的 SSH 连接。</span><span class="sxs-lookup"><span data-stu-id="b667f-268">Like you did earlier, create an SSH connection to your VM.</span></span>

    ```bash
    ssh azureuser@$ipaddress
    ```

1. <span data-ttu-id="b667f-269">移动到主`Books`目录下的目录。</span><span class="sxs-lookup"><span data-stu-id="b667f-269">Move to the `Books` directory under the home directory.</span></span>

    ```bash
    cd ~/Books
    ```

1. <span data-ttu-id="b667f-270">运行`npm install`以安装依赖程序包。</span><span class="sxs-lookup"><span data-stu-id="b667f-270">Run `npm install` to install the dependent packages.</span></span>

    ```bash
    npm install
    ```

<span data-ttu-id="b667f-271">将 SSH 连接保持打开状态, 以获取下一部分。</span><span class="sxs-lookup"><span data-stu-id="b667f-271">Keep your SSH connection open for the next part.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="b667f-272">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="b667f-272">Test the application</span></span>

<span data-ttu-id="b667f-273">现在准备测试 node.js web 应用程序!</span><span class="sxs-lookup"><span data-stu-id="b667f-273">You're now ready to test out your Node.js web application!</span></span>

1. <span data-ttu-id="b667f-274">在`~/Books`目录中, 运行此命令以启动 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-274">From the `~/Books` directory, run this command to start the web application.</span></span>

    ```bash
    sudo node server.js
    ```

    <span data-ttu-id="b667f-275">此命令通过在端口80上侦听传入的 HTTP 请求来启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="b667f-275">This command starts the application by listening on port 80 for incoming HTTP requests.</span></span>

1. <span data-ttu-id="b667f-276">从单独的浏览器选项卡中, 导航到 VM 的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b667f-276">From a separate browser tab, navigate to your VM's public IP address.</span></span>

    <span data-ttu-id="b667f-277">您将看到 "索引" 页, 其中包含一个 web 表单。</span><span class="sxs-lookup"><span data-stu-id="b667f-277">You see the index page, which includes a web form.</span></span>

    ![包含表单和提交按钮的网页。](../media/6-book-page.png)

    <span data-ttu-id="b667f-279">尝试将几本书添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="b667f-279">Try adding a few books to the database.</span></span> <span data-ttu-id="b667f-280">每次添加书籍时, 页面都会更新完整的书籍列表。</span><span class="sxs-lookup"><span data-stu-id="b667f-280">Each time you add a book, the page updates the complete list of books.</span></span>

    ![](../media/6-book-sample-entries.png)

    <span data-ttu-id="b667f-281">您还可以单击 "**删除**" 按钮, 从数据库中删除书籍。</span><span class="sxs-lookup"><span data-stu-id="b667f-281">You can also click the **Delete** button to delete a book from the database.</span></span>