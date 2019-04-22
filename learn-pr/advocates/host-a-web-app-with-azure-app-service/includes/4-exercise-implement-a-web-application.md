<span data-ttu-id="16dc8-101">在此单元中, 你将使用开发人员工具为初学者 web 应用程序创建代码。</span><span class="sxs-lookup"><span data-stu-id="16dc8-101">In this unit, you will use developer tools to create the code for a starter web application.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="16dc8-102">创建新的 web 项目</span><span class="sxs-lookup"><span data-stu-id="16dc8-102">Create a new web project</span></span>

::: zone pivot="csharp"

<span data-ttu-id="16dc8-103">.net CLI 工具的核心是`dotnet`命令行工具。</span><span class="sxs-lookup"><span data-stu-id="16dc8-103">The heart of the .NET CLI tools is the `dotnet` command line tool.</span></span> <span data-ttu-id="16dc8-104">使用此命令, 您将创建一个新的 ASP.NET Core web 项目。</span><span class="sxs-lookup"><span data-stu-id="16dc8-104">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="16dc8-105">在右侧的云命令行管理程序中, 创建一个新的 ASP.NET Core MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="16dc8-105">In the Cloud Shell on the right, create a new ASP.NET Core MVC application.</span></span> <span data-ttu-id="16dc8-106">将其命名为 "BestBikeApp"。</span><span class="sxs-lookup"><span data-stu-id="16dc8-106">Name it "BestBikeApp".</span></span>

```bash
dotnet new mvc --name BestBikeApp
```

<span data-ttu-id="16dc8-107">该命令将创建一个名为 "BestBikeApp" 的新文件夹来保存您的项目。</span><span class="sxs-lookup"><span data-stu-id="16dc8-107">The command will create a new folder named "BestBikeApp" to hold your project.</span></span> <span data-ttu-id="16dc8-108">`cd`然后, 生成并运行应用程序以验证它是否已完成。</span><span class="sxs-lookup"><span data-stu-id="16dc8-108">`cd` there, then build and run the application to verify it is complete.</span></span>

```bash
cd BestBikeApp
dotnet run
```

<span data-ttu-id="16dc8-109">您应该会看到类似这样的内容:</span><span class="sxs-lookup"><span data-stu-id="16dc8-109">You should get something like:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

<span data-ttu-id="16dc8-110">输出描述了启动应用后的情况: 应用程序正在运行, 并在端口5000处侦听。</span><span class="sxs-lookup"><span data-stu-id="16dc8-110">The output describes the situation after starting your app: the application is running and listening at port 5000.</span></span>

<span data-ttu-id="16dc8-111">如果我们在自己的计算机上运行应用程序, 我们将能够打开浏览器http://localhost:5000。</span><span class="sxs-lookup"><span data-stu-id="16dc8-111">If we were running the app on our own machine, we'd be able to open a browser to http://localhost:5000.</span></span> <span data-ttu-id="16dc8-112">若要从我们自己的计算机外部对此进行访问, 我们需要将应用部署到公共终结点所在的某个位置。</span><span class="sxs-lookup"><span data-stu-id="16dc8-112">To make this accessible from outside of our own machine, we'll need to deploy the app to somewhere with a public endpoint.</span></span> <span data-ttu-id="16dc8-113">我们之前创建的 App Service 实例非常理想。</span><span class="sxs-lookup"><span data-stu-id="16dc8-113">The App Service instance we created earlier is perfect for that.</span></span>

::: zone-end

::: zone pivot="node"

<span data-ttu-id="16dc8-114">若要创建初学者 node.js web 应用程序, 我们将使用节点包管理器 (NPM) 和一些基本 JavaScript 代码来运行实际的网页处理。</span><span class="sxs-lookup"><span data-stu-id="16dc8-114">To create a starter Node.js web application, we'll use the Node Package Manager (NPM) along with some basic JavaScript code to run the actual web page processing.</span></span>

<span data-ttu-id="16dc8-115">立即在云命令行管理程序中运行这些命令, `package.json`以创建将描述 node.js 应用程序的新命令。</span><span class="sxs-lookup"><span data-stu-id="16dc8-115">Run these commands in the Cloud Shell now to create a new `package.json` which will describe our Node.js application.</span></span>

```console
cd ~
mkdir helloworld
cd helloworld
npm init
```

<span data-ttu-id="16dc8-116">NPM 将提示您提供一系列答案, 请使用以下响应。</span><span class="sxs-lookup"><span data-stu-id="16dc8-116">NPM will prompt you for a series of answers, use the following responses.</span></span> <span data-ttu-id="16dc8-117">按 ENTER 以接受默认响应。</span><span class="sxs-lookup"><span data-stu-id="16dc8-117">Hit ENTER to accept the default response.</span></span>

| <span data-ttu-id="16dc8-118">问题</span><span class="sxs-lookup"><span data-stu-id="16dc8-118">Question</span></span> | <span data-ttu-id="16dc8-119">答案</span><span class="sxs-lookup"><span data-stu-id="16dc8-119">Answer</span></span> |
|----------|--------|
| <span data-ttu-id="16dc8-120">包名称</span><span class="sxs-lookup"><span data-stu-id="16dc8-120">package name</span></span> | <span data-ttu-id="16dc8-121">helloworld</span><span class="sxs-lookup"><span data-stu-id="16dc8-121">helloworld</span></span> |
| <span data-ttu-id="16dc8-122">版本</span><span class="sxs-lookup"><span data-stu-id="16dc8-122">version</span></span> | <span data-ttu-id="16dc8-123">_设置_</span><span class="sxs-lookup"><span data-stu-id="16dc8-123">_default_</span></span> |
| <span data-ttu-id="16dc8-124">产品介绍</span><span class="sxs-lookup"><span data-stu-id="16dc8-124">description</span></span> | <span data-ttu-id="16dc8-125">简单的 Hello World 应用程序</span><span class="sxs-lookup"><span data-stu-id="16dc8-125">A simple Hello World app</span></span> |
| <span data-ttu-id="16dc8-126">入口点</span><span class="sxs-lookup"><span data-stu-id="16dc8-126">entry point</span></span> | <span data-ttu-id="16dc8-127">_设置_</span><span class="sxs-lookup"><span data-stu-id="16dc8-127">_default_</span></span> |
| <span data-ttu-id="16dc8-128">测试命令</span><span class="sxs-lookup"><span data-stu-id="16dc8-128">test command</span></span> | <span data-ttu-id="16dc8-129">_设置_</span><span class="sxs-lookup"><span data-stu-id="16dc8-129">_default_</span></span> |
| <span data-ttu-id="16dc8-130">git 存储库</span><span class="sxs-lookup"><span data-stu-id="16dc8-130">git repository</span></span> | <span data-ttu-id="16dc8-131">_设置_</span><span class="sxs-lookup"><span data-stu-id="16dc8-131">_default_</span></span> |
| <span data-ttu-id="16dc8-132">关键字</span><span class="sxs-lookup"><span data-stu-id="16dc8-132">keywords</span></span> | <span data-ttu-id="16dc8-133">_设置_</span><span class="sxs-lookup"><span data-stu-id="16dc8-133">_default_</span></span> |
| <span data-ttu-id="16dc8-134">编写</span><span class="sxs-lookup"><span data-stu-id="16dc8-134">author</span></span> | <span data-ttu-id="16dc8-135">您的姓名</span><span class="sxs-lookup"><span data-stu-id="16dc8-135">your name</span></span> |
| <span data-ttu-id="16dc8-136">license</span><span class="sxs-lookup"><span data-stu-id="16dc8-136">license</span></span> | <span data-ttu-id="16dc8-137">无论您想要的是什么, MIT, ISC, 等等。</span><span class="sxs-lookup"><span data-stu-id="16dc8-137">whatever you want, MIT, ISC, etc.</span></span> |

<span data-ttu-id="16dc8-138">这将在当前文件夹`package.json`中创建一个新文件-如果您在 "终端" 窗口中键入`ls` , 您应该会在当前文件夹中看到它。</span><span class="sxs-lookup"><span data-stu-id="16dc8-138">This will create a new `package.json` file in the current folder - you should see it in the current folder if you type `ls` in the terminal window.</span></span> <span data-ttu-id="16dc8-139">我们将需要一个 JavaScript 文件来运行我们的网站逻辑-因为这只是一个基本示例, 所以我们只需要一个文件`index.js`。</span><span class="sxs-lookup"><span data-stu-id="16dc8-139">We will need a JavaScript file to run our website logic - since this is just a basic example, we will only need one file - `index.js`.</span></span> <span data-ttu-id="16dc8-140">在终端中使用以下命令来创建文件:</span><span class="sxs-lookup"><span data-stu-id="16dc8-140">Use the following command in the terminal to create the file:</span></span>

```bash
touch index.js
``` 

<span data-ttu-id="16dc8-141">现在, 我们必须对这两个文件进行一些编辑。</span><span class="sxs-lookup"><span data-stu-id="16dc8-141">Now we have to make a few edits to both of our files.</span></span> <span data-ttu-id="16dc8-142">在 "终端" 中键入以下命令, 以打开交互式编辑器。</span><span class="sxs-lookup"><span data-stu-id="16dc8-142">Type the following command into the terminal to open an interactive editor.</span></span>

```console
code .
```

<span data-ttu-id="16dc8-143">选择`package.json`文件并对`scripts`节进行以下编辑, 以使用 node.js 启动 web 应用。</span><span class="sxs-lookup"><span data-stu-id="16dc8-143">Select the `package.json` file and make the following edits to the `scripts` section to use Node.js to launch the web app.</span></span> <span data-ttu-id="16dc8-144">您也可以删除该`main`条目。</span><span class="sxs-lookup"><span data-stu-id="16dc8-144">You can also remove the `main` entry.</span></span>

```json
{
  "name": "helloworld",
  ...
  "scripts": {
    "start": "node index.js"
  },
  ...
}
```

<span data-ttu-id="16dc8-145">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="16dc8-145">Save the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16dc8-146">只要您将代码粘贴或更改为编辑器中的文件, 就一定要使用 "..." 进行保存。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Command + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="16dc8-146">Whenever you paste or change code into a file in the editor, make sure to save afterwards using the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Command+S</kbd> on macOS).</span></span>

<span data-ttu-id="16dc8-147">切换到该`index.js`文件并向其添加以下内容。</span><span class="sxs-lookup"><span data-stu-id="16dc8-147">Switch to the `index.js` file and add the following contents to it.</span></span> <span data-ttu-id="16dc8-148">这是一个简单的节点程序, 可始终使用 "Hello World!" 进行响应</span><span class="sxs-lookup"><span data-stu-id="16dc8-148">This is a simple node program to always respond with "Hello World!"</span></span> <span data-ttu-id="16dc8-149">对服务器发出任何 GET 请求时。</span><span class="sxs-lookup"><span data-stu-id="16dc8-149">when any GET request is made to the server.</span></span>

```javascript
var http = require('http');

var server = http.createServer(function(request, response) {

    response.writeHead(200, { "Content-Type": "text/html" });
    response.end("<html><h1>Hello World!</h1></html>");

});

var port = process.env.PORT || 1337;
server.listen(port);

console.log("Server running at http://localhost:%d", port);
```

<span data-ttu-id="16dc8-150">保存文件并退出编辑器。</span><span class="sxs-lookup"><span data-stu-id="16dc8-150">Save the file and exit the editor.</span></span> <span data-ttu-id="16dc8-151">您可以通过 "..." 退出编辑器。右上部菜单或通过<kbd>Ctrl + Q</kbd>。</span><span class="sxs-lookup"><span data-stu-id="16dc8-151">You can exit the editor through the "..." menu on the top right or through <kbd>Ctrl+Q</kbd>.</span></span>

<span data-ttu-id="16dc8-152">现在, 我们已准备好打包要部署到 Azure 的文件。</span><span class="sxs-lookup"><span data-stu-id="16dc8-152">Now we are ready to package up the files to deploy to Azure.</span></span> <span data-ttu-id="16dc8-153">我们需要为项目中的所有内容创建 ZIP 存档。</span><span class="sxs-lookup"><span data-stu-id="16dc8-153">We need to create a ZIP archive of everything in the project.</span></span> <span data-ttu-id="16dc8-154">在 "终端" 窗口中键入以下命令, 以创建 ZIP 文件:</span><span class="sxs-lookup"><span data-stu-id="16dc8-154">Type the following commands into the terminal window to create a ZIP file:</span></span>

```bash
zip -r helloworld.zip .
```

<span data-ttu-id="16dc8-155">命令运行完毕后, 请键入`ls`, 您将看到一个名为`helloworld.zip`的文件。</span><span class="sxs-lookup"><span data-stu-id="16dc8-155">When the command finishes running, type `ls`, you'll see a file named `helloworld.zip`.</span></span> <span data-ttu-id="16dc8-156">这是我们将部署到应用服务的 web 应用程序包。</span><span class="sxs-lookup"><span data-stu-id="16dc8-156">This is the web application package that we will deploy to App Service.</span></span>

::: zone-end

::: zone pivot="java"

<span data-ttu-id="16dc8-157">若要创建初学者 web 应用程序, 我们将使用 Maven, 它是一种常用的 Java 应用程序项目管理和生成工具。</span><span class="sxs-lookup"><span data-stu-id="16dc8-157">To create a starter web application, we'll use Maven, a commonly-used project management and build tool for Java apps.</span></span> <span data-ttu-id="16dc8-158">Maven 包含一个名为*archetypes*的功能, 可为不同类型的应用程序快速创建起始代码。</span><span class="sxs-lookup"><span data-stu-id="16dc8-158">Maven includes a feature called *archetypes* that can quickly create starter code for different kinds of applications.</span></span> <span data-ttu-id="16dc8-159">我们可以使用该`maven-archetype-webapp`模板为显示 "Hello World!" 的简单 web 应用程序生成代码。</span><span class="sxs-lookup"><span data-stu-id="16dc8-159">We can use the `maven-archetype-webapp` template to generate the code for a simple web app that displays "Hello World!"</span></span> <span data-ttu-id="16dc8-160">在其主页上。</span><span class="sxs-lookup"><span data-stu-id="16dc8-160">on its homepage.</span></span>

<span data-ttu-id="16dc8-161">立即在云命令行管理程序中运行这些命令, 以创建新的 web 应用程序:</span><span class="sxs-lookup"><span data-stu-id="16dc8-161">Run these commands in the Cloud Shell now to create a new web app:</span></span>

```console
cd ~
mvn archetype:generate -DgroupId=example.demo -DartifactId=helloworld -DinteractiveMode=false -DarchetypeArtifactId=maven-archetype-webapp
```

<span data-ttu-id="16dc8-162">现在, 运行这些命令以更改为新的 "helloworld" 应用程序目录, 并打包应用程序以进行部署:</span><span class="sxs-lookup"><span data-stu-id="16dc8-162">Now, run these commands to change to the new "helloworld" application directory and package the application for deployment:</span></span>

```console
cd helloworld
mvn package
```

<span data-ttu-id="16dc8-163">命令完成运行后, 如果您更改为`target`目录并运行`ls`, 将看到一个名为的文件被`helloworld.war`列出。</span><span class="sxs-lookup"><span data-stu-id="16dc8-163">When the command finishes running, if you change to the `target` directory and run `ls`, you'll see one file listed called `helloworld.war`.</span></span> <span data-ttu-id="16dc8-164">这是我们将部署到应用服务的 web 应用程序包。</span><span class="sxs-lookup"><span data-stu-id="16dc8-164">This is the web application package that we will deploy to App Service.</span></span>

::: zone-end