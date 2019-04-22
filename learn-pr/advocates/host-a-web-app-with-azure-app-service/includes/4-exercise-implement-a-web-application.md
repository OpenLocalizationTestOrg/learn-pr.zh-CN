在此单元中, 你将使用开发人员工具为初学者 web 应用程序创建代码。

## <a name="create-a-new-web-project"></a>创建新的 web 项目

::: zone pivot="csharp"

.net CLI 工具的核心是`dotnet`命令行工具。 使用此命令, 您将创建一个新的 ASP.NET Core web 项目。

在右侧的云命令行管理程序中, 创建一个新的 ASP.NET Core MVC 应用程序。 将其命名为 "BestBikeApp"。

```bash
dotnet new mvc --name BestBikeApp
```

该命令将创建一个名为 "BestBikeApp" 的新文件夹来保存您的项目。 `cd`然后, 生成并运行应用程序以验证它是否已完成。

```bash
cd BestBikeApp
dotnet run
```

您应该会看到类似这样的内容:

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

输出描述了启动应用后的情况: 应用程序正在运行, 并在端口5000处侦听。

如果我们在自己的计算机上运行应用程序, 我们将能够打开浏览器http://localhost:5000。 若要从我们自己的计算机外部对此进行访问, 我们需要将应用部署到公共终结点所在的某个位置。 我们之前创建的 App Service 实例非常理想。

::: zone-end

::: zone pivot="node"

若要创建初学者 node.js web 应用程序, 我们将使用节点包管理器 (NPM) 和一些基本 JavaScript 代码来运行实际的网页处理。

立即在云命令行管理程序中运行这些命令, `package.json`以创建将描述 node.js 应用程序的新命令。

```console
cd ~
mkdir helloworld
cd helloworld
npm init
```

NPM 将提示您提供一系列答案, 请使用以下响应。 按 ENTER 以接受默认响应。

| 问题 | 答案 |
|----------|--------|
| 包名称 | helloworld |
| 版本 | _设置_ |
| 产品介绍 | 简单的 Hello World 应用程序 |
| 入口点 | _设置_ |
| 测试命令 | _设置_ |
| git 存储库 | _设置_ |
| 关键字 | _设置_ |
| 编写 | 您的姓名 |
| license | 无论您想要的是什么, MIT, ISC, 等等。 |

这将在当前文件夹`package.json`中创建一个新文件-如果您在 "终端" 窗口中键入`ls` , 您应该会在当前文件夹中看到它。 我们将需要一个 JavaScript 文件来运行我们的网站逻辑-因为这只是一个基本示例, 所以我们只需要一个文件`index.js`。 在终端中使用以下命令来创建文件:

```bash
touch index.js
``` 

现在, 我们必须对这两个文件进行一些编辑。 在 "终端" 中键入以下命令, 以打开交互式编辑器。

```console
code .
```

选择`package.json`文件并对`scripts`节进行以下编辑, 以使用 node.js 启动 web 应用。 您也可以删除该`main`条目。

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

保存该文件。

> [!IMPORTANT]
> 只要您将代码粘贴或更改为编辑器中的文件, 就一定要使用 "..." 进行保存。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Command + s</kbd> )。

切换到该`index.js`文件并向其添加以下内容。 这是一个简单的节点程序, 可始终使用 "Hello World!" 进行响应 对服务器发出任何 GET 请求时。

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

保存文件并退出编辑器。 您可以通过 "..." 退出编辑器。右上部菜单或通过<kbd>Ctrl + Q</kbd>。

现在, 我们已准备好打包要部署到 Azure 的文件。 我们需要为项目中的所有内容创建 ZIP 存档。 在 "终端" 窗口中键入以下命令, 以创建 ZIP 文件:

```bash
zip -r helloworld.zip .
```

命令运行完毕后, 请键入`ls`, 您将看到一个名为`helloworld.zip`的文件。 这是我们将部署到应用服务的 web 应用程序包。

::: zone-end

::: zone pivot="java"

若要创建初学者 web 应用程序, 我们将使用 Maven, 它是一种常用的 Java 应用程序项目管理和生成工具。 Maven 包含一个名为*archetypes*的功能, 可为不同类型的应用程序快速创建起始代码。 我们可以使用该`maven-archetype-webapp`模板为显示 "Hello World!" 的简单 web 应用程序生成代码。 在其主页上。

立即在云命令行管理程序中运行这些命令, 以创建新的 web 应用程序:

```console
cd ~
mvn archetype:generate -DgroupId=example.demo -DartifactId=helloworld -DinteractiveMode=false -DarchetypeArtifactId=maven-archetype-webapp
```

现在, 运行这些命令以更改为新的 "helloworld" 应用程序目录, 并打包应用程序以进行部署:

```console
cd helloworld
mvn package
```

命令完成运行后, 如果您更改为`target`目录并运行`ls`, 将看到一个名为的文件被`helloworld.war`列出。 这是我们将部署到应用服务的 web 应用程序包。

::: zone-end