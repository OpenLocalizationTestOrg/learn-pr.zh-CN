## <a name="face-api-registration"></a>面孔 API 注册

拥有 Azure 沙盒订阅后, 可以添加面孔 api 资源并获取连接到此 API 所需的面孔 api URL 和密钥。

1. 转到[Azure 认知服务面孔服务](https://azure.microsoft.com/en-us/services/cognitive-services/face?azure-portal=true)并单击 " **Try 面孔**"。 单击 "**现有 Azure 帐户**" 框中的 "**登录**" 按钮。 这将转到 Azure 门户, 并打开 "**创建表面**" 对话框。 输入以下信息:

    - Azure 面孔资源的名称
    - `Concierge Subscription`订阅的
    - 保留其默认值的位置
    - `F0`对于定价层
    - 资源组的**<rgn>沙盒资源组</rgn>**

1. 成功部署 Azure 资源后, 请转到此资源并记录 API**终结点**和**注册表项**。 你将需要其中一个密钥来调用面孔 API。 您可以使用任一键。

## <a name="slack-workspace"></a>可宽延时间工作区

若要创建可宽延时间命令, 您需要具有可宽延时间的工作区的管理员权限。

1. 如果您有一个可宽延时间工作区, 并且您具有管理员权限, 则可以使用该工作区。 您还可以[创建新的 "全新可宽延时间" 工作区](https://slack.com/create?azure-portal=true)。

## <a name="local-setup"></a>本地安装

你可以在本地计算机上执行此模块中的大多数练习, 并将其部署到 Azure 沙盒作为最后一步。

1. 安装 Visual Studio Code

    如果尚未安装, 请下载并安装[Visual Studio Code](https://code.visualstudio.com?azure-portal=true)

1. 向 Visual Studio Code 中添加 Azure 扩展

    如果尚未安装这些扩展, 请安装以下 VS 代码扩展:
    - [Azure 帐户](https://marketplace.visualstudio.com/items?azure-portal=true&itemName=ms-vscode.azure-account)
    - [Azure 函数](https://marketplace.visualstudio.com/items?azure-portal=true&itemName=ms-azuretools.vscode-azurefunctions)

1. 安装节点和 npm

   如果尚未在计算机上本地安装它们, 请为您的操作系统安装[node 和 npm](https://nodejs.org/en/download?azure-portal=true) 。

1. 克隆起始代码

    克隆起始代码可帮助您充分利用本模块。 完成应用程序所需的所有代码和一些初始的引导代码都可免费开始。

    ```bash
    git clone https://github.com/MicrosoftDocs/mslearn-the-mojifier.git
    ```

    您应该能够使用所提供的代码完成项目, 但如果您无法确定事情, 则可以在`completed`分支中找到已完成的代码。

1. 转到包含克隆的源存储库的目录中, 然后安装所需的程序包:

    ```bash
    cd mslearn-the-mojifier
    npm install
    ```

1. 将 TypeScript 代码编译为 JavaScript

    您将使用 TypeScript 编写应用程序。 TypeScript 支持类型检查和类定义, 我们将在我们的 Mojifier 代码中使用它们。 node.js 不知道如何运行 typescript, 因此在开发时, 需要将 TypeScript 代码转换为 JavaScript。 在运行上面`tsc`的`npm install`命令时, 将`package.json`会安装 TypeScript 编译器, 并将配置为在生成阶段运行它。 运行以下命令:

    ```bash
    npm run build
    ```

    保持此命令在终端命令行管理程序中运行。 这将监视对 TypeScript 文件所做的任何更改, 并将其转换为 JavaScript 文件。 如果您在练习中看不到所需的行为, 请检查 "终端" 窗口中的控制台输出, 因为您的 TypeScript 代码中可能存在错误。
