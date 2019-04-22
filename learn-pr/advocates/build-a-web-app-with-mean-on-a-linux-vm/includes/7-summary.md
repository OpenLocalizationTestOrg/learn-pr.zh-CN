均值是构建和承载 web 应用程序的开发堆栈。 回想一下, 均值是其组件部件的首字母缩略词: MongoDB、Express、AngularJS 和 node.js。

在本模块中, 您学习了当 "平均" 堆栈是理想的 web 开发选择以及您可能想要选择其他内容时。 您可能需要考虑的主要原因是您熟悉 JavaScript。

若要查看平均堆栈处于活动中, 您在 Azure 上创建了一个 Ubuntu 虚拟机, 并在其上安装了用于 web 开发的平均堆栈。

将 "均值" 堆栈放置后, 您创建了一个基本书籍清单 web 应用程序。 总而言之, web 应用程序使用:

* **MongoDB** , 用于存储书籍的相关信息。
* **Express**用于将每个 HTTP 请求路由到相应的处理程序。
* **AngularJS**将用户界面与程序的业务逻辑连接起来。
* 承载服务器端应用程序的**node.js** 。

你可以在 GitHub 上[查找 web 应用程序的源代码](https://github.com/MicrosoftDocs/mslearn-build-a-web-app-with-mean-on-a-linux-vm?azure-portal=true)。

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="learn-more"></a>了解更多信息

在本模块中, 您可以了解 "平均" 堆栈的工作方式, 并启动使用它的基本 web 应用程序。 下一步是开始构建可解决自己的业务难题的应用程序。 然后, 您可以将应用程序部署到 Azure, 并使用自动进程来监视应用程序并使其更好地使用。 下面是一些可了解详细信息的资源。

### <a name="learn-more-about-mean-stack-application-development"></a>了解有关平均堆栈应用程序开发的详细信息

详细了解在此模块中使用的 "平均" 堆栈组件和其他 node.js 包。

* [MongoDB](https://www.mongodb.com?azure-portal=true)
* [Express](http://expressjs.com?azure-portal=true)
* [AngularJS](https://angularjs.org?azure-portal=true)
* [node.js](https://nodejs.org?azure-portal=true)

* [npm](https://www.npmjs.com?azure-portal=true)
* [Mongoose](https://www.npmjs.com/package/mongoose?azure-portal=true)
* [body-分析程序](https://www.npmjs.com/package/body-parser?azure-portal=true)

### <a name="learn-about-the-azure-web-apps-service"></a>了解 Azure Web Apps 服务

在此模块中, 你使用了虚拟机来托管你的 web 应用程序。 VM 可让您更好地控制环境, 并且可能最适合当前管理您的部署的方式。 但还有其他方法可以托管 web 应用程序。 请查看[在 Azure 中创建 node.js web 应用](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs?azure-portal=true), 了解如何使用 azure web Apps 服务简化部署。

### <a name="automate-your-deployments"></a>自动化部署

此外, 在本模块中, 您使用主要的手动过程来配置您的 VM 并运行您的应用程序。 随着过程的成熟, 您可以使用更加自动化的过程来更快、更可靠地部署更改。 请参阅[Create a CI/CD 管道 for node.js with the azure DevOps 项目](https://docs.microsoft.com/azure/devops-project/azure-devops-project-nodejs?azure-portal=true), 了解如何使用 azure DevOps 将 node.js 应用程序部署为连续集成和连续传递 (CI/CD) 管道的一部分。