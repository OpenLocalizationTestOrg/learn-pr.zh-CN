到目前为止, 你的 Ubuntu VM 上安装了 MongoDB 和 node.js。 现在是时候创建基本 web 应用程序来查看操作中的内容。 同时, 你将看到 "AngularJS" 和 "Express" 的匹配方式。

例如, 学习的一种非常好的方法。 您将生成的 web 应用程序将实现基本书籍数据库。 通过 web 应用程序, 您可以列出有关书籍、添加新书籍和删除现有书籍的信息。

你将在此处看到的 web 应用程序演示了许多适用于大多数平均堆栈 web 应用程序的概念。 根据您的需求和兴趣, 您可以浏览构建自己的平均堆栈应用程序所需的功能。

本书 web 应用程序的外观如下所示。

![包含表单和提交按钮的网页。](../media/6-book-page.png)

下面介绍了每个平均堆栈的组件是如何适合的。

* MongoDB 存储书籍的相关信息。
* Express 将每个 HTTP 请求路由到相应的处理程序。
* AngularJS 将用户界面与程序的业务逻辑连接。
* node.js 承载服务器端应用程序。

> [!IMPORTANT]
> 出于学习目的, 您要构建基本的 web 应用程序。 其目的是测试您的 "均值" 堆栈, 并让您了解它的工作原理。 应用程序不够安全或已准备好用于生产用途。

## <a name="what-about-express"></a>什么是 Express？

到目前为止, 你已在你的 VM 上安装 MongoDB 和 node.js。 在平均首字母缩略词中, **E**是什么？

Express 是为 node.js 构建的 web 服务器框架, 简化了构建 web 应用程序的过程。

Express 的主要用途是处理请求路由。 _路由_指的是应用程序如何响应对特定终结点的请求。 终结点由路径或 URI 以及请求方法 (如 GET 或 POST) 组成。 例如, 您可以通过在数据库中提供所有书籍的`/book`列表来响应对终结点的 GET 请求。 您可以根据用户输入到 web 表单中的字段向数据库添加条目, 从而对同一终结点做出响应。

在您即将构建的 web 应用程序中, 您将使用 Express 路由 HTTP 请求, 并将 web 内容返回给您的用户。 Express 还可帮助 web 应用程序使用 HTTP cookie 和过程查询字符串。

Express 是 node.js 包。 您可以使用**npm**实用工具 (与 node.js 一起提供) 来安装和管理 node.js 包。 稍后将在此部分中创建一个名`package.json`为的文件, 以定义 Express 和其他依赖项, `npm install`然后运行该命令以安装这些依赖项。

## <a name="what-about-angularjs"></a>AngularJS？

与 Express 一样, 您尚未安装 AngularJS, 即 " **A" 作为**"平均值" 首字母缩写词。

AngularJS 使 web 应用程序更易于编写和测试, 因为它使您能够更好地将网页的_外观_(HTML 代码) 与网页的行为进行区分。 如果您熟悉模型– view – controller (MVC) 模式或数据绑定概念, 则 AngularJS 将对您很熟悉。

AngularJS 是所谓的前端 JavaScript 框架, 这意味着它只需要在访问应用程序的客户端上可用。 换言之, AngularJS 在用户的 web 浏览器中运行, 而不是在 web 服务器上运行。 由于 AngularJS 是 JavaScript, 因此您可以使用它轻松地从您的 web 服务器中获取数据, 以在页面上显示。

您无实际_安装_AngularJS。 而是在 HTML 页面中添加对 JavaScript 文件的引用, 就像对其他 JavaScript 库执行的操作一样。 有几种方法可在网页中添加 AngularJS。 在这里, 你将从内容传递网络或 CDN 加载 AngularJS。 CDN 是一种将图像、视频和其他内容分散在不同地理位置以提高下载速度的方法。

请勿同时添加此代码, 但下面的示例展示了如何从 CDN 加载 AngularJS。 通常将此代码添加到 HTML 页面`<head>`的部分。

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
```

> [!NOTE]
> 请勿将 AngularJS 与角混淆。 虽然其中的许多概念在两者之间相似, 但 AngularJS 是角度的前置任务。 AngularJS 仍通常用于构建 web 应用程序。 尽管 AngularJS 基于 JavaScript, 但角度是基于 TypeScript, 这种编程语言使编写 JavaScript 程序更为简单。

## <a name="how-will-i-build-the-application"></a>我将如何构建应用程序？

在这里, 你将使用一个基本过程。 你将从云命令行管理程序编写应用程序代码, 然后使用 SCP 或安全复制协议将文件复制到 VM。 然后, 启动 node.js 应用程序, 并在浏览器中查看结果。

在实践中, 通常会在更多的本地环境中编写和测试 web 应用程序, 例如从便携式计算机或本地运行的虚拟机。 然后, 您可以将代码存储在一个修订版控制系统 (如 Git) 中, 并使用连续集成和连续传递, 或者 CI/CD、系统 (如 Azure DevOps) 测试您的更改并将其上传到您的 VM。 我们将指向本模块结尾的更多资源。

## <a name="create-the-books-web-application"></a>创建书籍 web 应用程序

在这里, 你将创建构成 web 应用程序的所有代码、脚本和 HTML 文件。 为简洁起见, 我们将重点介绍每个文件的重要部分, 但不会深入了解全部详细信息。

如果仍通过 SSH 连接到 VM, 请运行`exit`以离开 ssh 会话并返回云命令行管理程序。

```bash
exit
```

你现在将回到云 Shell 会话。

### <a name="create-the-files"></a>创建文件

1. 从云命令行管理程序运行这些命令, 为 web 应用程序创建文件夹和文件。

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

    其中包括以下 what's:

    * `Books`&ndash;项目的根目录。
      * `server.js`定义 web 应用程序的入口点。 它加载所需的 node.js 包, 指定要侦听的端口, 并开始侦听传入的 HTTP 流量。
      * `package.json`提供有关应用程序的信息, 包括其名称、说明以及应用程序需要运行的 node.js 包。
    * `Books/app`&ndash;包含在服务器上运行的代码。
      * `model.js`定义数据库连接和架构。 将其视为应用程序的数据模型。
      * `routes.js`处理请求路由。 例如, 它通过提供数据库中所有书籍`/book`的列表来定义对终结点的 GET 请求。
    * `Books/public`&ndash;包含直接提供给客户端浏览器的文件。
      * `index.html`包含索引页。 它包含一个 web 表单, 用户可以通过它提交书籍的相关信息。 它还显示数据库中的所有书籍, 并使您可以从数据库中删除条目。
      * `script.js`包含在用户浏览器中运行的 JavaScript 代码。 它可以向服务器发送请求, 以列出书籍、向数据库添加书籍以及从数据库中删除书籍。

1. 运行`code`命令以通过云命令行管理程序编辑器打开文件。

    ```bash
    code Books
    ```

### <a name="create-the-data-model"></a>创建数据模型

1. 在编辑器中, 打开`app/model.js`并添加以下项。

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
    > 只要您将代码粘贴或更改为编辑器中的文件, 就一定要使用 "..." 进行保存。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Command + s</kbd> )。

    此代码使用 Mongoose 简化在 MongoDB 中传输数据的过程。 Mongoose 是一个基于架构的数据建模系统。

    此代码将连接到本地 MongoDB 服务器上名为 "书籍" 的数据库。 然后, 它使用提供的架构定义名为 "Book" 的数据库文档。 架构定义了四个字段, 用于描述一本书:

    * 书籍的名称或职务
    * 其国际标准书籍编号, 或可唯一标识书籍的 ISBN
    * 其作者
    * 它所包含的页面数

    接下来, 将创建用于将 GET、POST 和 DELETE 请求映射到数据库操作的 HTTP 处理程序。

### <a name="create-the-express-routes-that-handle-http-requests"></a>创建处理 HTTP 请求的 Express 路由

1. 在编辑器中, 打开`app/routes.js`并添加以下代码。

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

    此代码将为应用程序创建四个路由。 以下是每个主题的简要概述。

    | HTTP 谓词 | Endpoint      | 说明                                                                                                           |
    |-----------|---------------|-----------------------------------------------------------------------------------------------------------------------|
    | GET       | `/book`       | 检索数据库中的所有书籍。                                                                                |
    | POST      | `/book`       | 根据用户`Book`在 web 表单上提供的字段创建对象, 并将该对象写入数据库。 |
    | 删除    | `/book/:isbn` | 从数据库中删除由其 ISBN 标识的书籍。                                                         |
    | GET       | `*`           | 当没有匹配的其他路由时, 返回索引页。                                                                |

    Express 可以直接在路由处理代码中提供 HTTP 响应, 也可以提供来自文件的静态内容。 此代码显示了这两种情况。 前三个路由为 book API 请求返回 JSON 数据。 第四个路由 (默认情况下) 返回索引文件的内容`index.html`。

### <a name="create-the-client-side-javascript-application"></a>创建客户端 JavaScript 应用程序

1. 在编辑器中, 打开`public/script.js`并添加以下代码:

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

    请注意, 此代码如何定义名为 "myApp" 的模块和名为 "myCtrl" 的控制器。 我们不会详细介绍模块和控制器在这里如何工作, 但在下一步中将使用这些名称将用户界面 (HTML 代码) 与应用程序的业务逻辑绑定在一起。

    之前, 您创建了四个在服务器上处理各种 GET、POST 和 DELETE 操作的路由。 此代码类似于这些相同的操作, 但来自客户端 (用户的 web 浏览器)。

    例如`getData` , 函数将 GET 请求发送到`/book`终结点。 请记住, 服务器通过从数据库中检索有关所有书籍的信息并将该信息作为 JSON 数据返回来处理此请求。 请注意生成的 JSON 数据是如何分配给`$scope.books`变量的。 在下一步中, 您将了解到这会如何影响用户在网页上看到的内容。

    此代码在页面`getData`加载时调用函数。 您可以检查`del_book`和`add_book`函数, 以了解它们的工作方式。 您不需要客户端代码来匹配服务器的默认处理程序, 因为默认处理程序返回的是索引页而不是 JSON 数据。

### <a name="create-the-user-interface"></a>创建用户界面

1. 在编辑器中, 打开`public/index.html`并添加以下代码:

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

    此代码创建一个具有四个字段的基本 HTML 窗体, 用于提交书籍数据和一个显示存储在数据库中的所有书籍的表格。

    虽然这是标准 html 代码, 但`ng-` HTML 属性可能对您不熟悉。 这些 HTML 属性将 AngularJS 代码与用户界面线对齐。 例如, 当用户单击 "**添加**" 按钮时, AngularJS 将`add_book`调用函数, 该函数将表单数据发送到服务器。

    您可以查看此处的代码, 了解每个`ng-`属性与应用程序的业务逻辑的关系。

### <a name="create-the-express-server-to-host-the-application"></a>创建用于承载应用程序的 Express 服务器

1. 在编辑器中, 打开`server.js`并添加以下代码:

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

    此代码将创建 web 应用程序本身。 它提供目录中的`public`静态文件, 并使用您在之前定义的路由来处理请求。

### <a name="define-package-information-and-dependencies"></a>定义包信息和依赖项

召回, `package.json`提供有关应用程序的信息, 包括其名称、说明以及应用程序需要运行的 node.js 包。

1. 在编辑器中, 打开`package.json`并添加以下代码:

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

您将看到有关您的应用程序的信息或元数据, 包括其名称、说明和许可证。

该`repository`字段指定维护代码的位置。 若要进行参考, 可以稍后在 GitHub 上查看 GitHub 上的代码, 网址为此处显示的 URL。

`main`字段定义应用程序的入口点。 此处提供了完整的完整性, 但并不重要, 因为您不打算将应用程序作为 node.js 程序包发布, 以供其他人下载和使用。

`dependencies`字段很重要。 它定义您的应用程序需要的 node.js 包。 稍后, 你将很快连接到 VM 并运行`npm install`命令以安装这些程序包。

节点包通常使用[语义版本](https://semver.org?azure-portal=true)控制版本化方案。 版本号包含三个组件: 主要版本、次要版本和修补程序。 此处的`~`波形符表示法告诉 npm 在提供的主要版本和次要版本下安装最新的修补程序版本。 您在此处看到的版本是使用此模块测试的最新版本。 实际上, 在您更新和测试应用程序以使用每个相关包提供的最新功能时, 您可以随着时间的推移增加版本。

### <a name="copy-the-files-to-your-vm"></a>将文件复制到 VM

1. 你已完成编辑文件。 确保您已保存对每个文件的更改, 然后关闭编辑器。

    若要关闭编辑器, 请单击角上的省略号, 然后选择 "**关闭编辑器**"。

1. 运行以下`scp`命令, 将云命令行管理程序`~/Books`会话中目录的内容复制到 VM 上的相同目录名称中。

    ```bash
    scp -r ~/Books azureuser@$ipaddress:~/Books
    ```

## <a name="install-additional-node-packages"></a>安装其他节点程序包

假设在开发过程中, 您标识了要使用的其他节点包。 例如, 从该行开始`app/model.js`的回忆。

```javascript
var mongoose = require('mongoose');
```

请记住, 应用程序使用 Mongoose 帮助将数据传入和传出 MongoDB 数据库。

应用程序还需要 Express 和 body 分析器包。 body-parser 是一个插件, 它使 Express 能够使用客户端发送的 web 表单中的数据。

让我们连接到你的 VM 并安装你在中`package.json`指定的程序包。

1. 在连接到你的 vm 之前, 请确保你具有自己的 vm 的 IP 地址。 如果没有, 请从云命令行管理程序中运行这些命令以进行检索。

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

1. 正如您之前所做的那样, 请创建到你的 VM 的 SSH 连接。

    ```bash
    ssh azureuser@$ipaddress
    ```

1. 移动到主`Books`目录下的目录。

    ```bash
    cd ~/Books
    ```

1. 运行`npm install`以安装依赖程序包。

    ```bash
    npm install
    ```

将 SSH 连接保持打开状态, 以获取下一部分。

## <a name="test-the-application"></a>测试应用程序

现在准备测试 node.js web 应用程序!

1. 在`~/Books`目录中, 运行此命令以启动 web 应用程序。

    ```bash
    sudo node server.js
    ```

    此命令通过在端口80上侦听传入的 HTTP 请求来启动应用程序。

1. 从单独的浏览器选项卡中, 导航到 VM 的公共 IP 地址。

    您将看到 "索引" 页, 其中包含一个 web 表单。

    ![包含表单和提交按钮的网页。](../media/6-book-page.png)

    尝试将几本书添加到数据库中。 每次添加书籍时, 页面都会更新完整的书籍列表。

    ![](../media/6-book-sample-entries.png)

    您还可以单击 "**删除**" 按钮, 从数据库中删除书籍。