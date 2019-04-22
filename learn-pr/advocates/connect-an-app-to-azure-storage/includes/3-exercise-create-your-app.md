请注意, 我们正在处理照片共享应用程序, 该应用程序将使用 Azure 存储来管理我们代表用户存储的图片和其他数据位。

[!include[](../../../includes/azure-sandbox-activate.md)]

::: zone pivot="csharp"

为了简化我们的方案, 以便我们能够重点关注存储 api, 我们将创建一个新的 .net Core 控制台应用程序。 我们还将假定它始终具有网络连接。 但是, 您应始终强化您的应用程序, 以确保网络故障不会影响用户体验或导致应用程序本身失败。

## <a name="create-a-net-core-application"></a>创建 .net Core 应用程序

.net Core 是在 macOS、Windows 和 Linux 上运行的 .net 的跨平台版本。 您可以在本地安装这些工具, 也可以使用窗口右侧的云命令行管理程序执行下面的步骤。

1. 登录云命令行管理程序或打开一个命令行会话, 并创建一个名为 "PhotoSharingApp" 的新 .net Core 控制台应用程序。 您可以添加`-o`或`--output`标记以在特定文件夹中创建应用程序。

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. 运行应用程序以确保其生成和执行正确。 它应显示 "Hello World!" 到控制台。

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
::: zone-end

::: zone pivot="javascript"

为了简化我们的方案, 以便我们能够重点关注存储 api, 我们将创建可从控制台运行的新 node.js 应用程序。 我们还将假定它始终具有网络连接。 但是, 您应始终强化您的应用程序, 以确保网络故障不会影响用户体验, 或导致应用程序本身失败。

## <a name="create-a-nodejs-application"></a>创建一个 node.js 应用程序

node.js 是运行 JavaScript 应用程序的流行框架。 它通常用于 web 应用程序, 但也可以使用它从命令行运行逻辑。 如果您已在本地安装这些工具, 则可以从命令行运行以下步骤。 或者, 也可以使用窗口右侧的云命令行管理程序执行以下步骤。

1. 登录云命令行管理程序或打开一个命令行会话, 并创建一个名为 "PhotoSharingApp" 的新文件夹。

    ```bash
    mkdir PhotoSharingApp
    ```

1. 转到新文件夹, 并使用`npm`初始化新的 node.js 应用。 这将创建一个包含描述应用程序的元数据的**package. json**文件。

    ```bash
    cd PhotoSharingApp
    npm init -y
    ```

1. 创建一个新的源文件**索引 .js**, 即我们的代码将转到该文件的位置。

    ```bash
    touch index.js
    ```

1. 使用编辑器打开**索引 .js**文件。 如果使用的是云命令行管理程序, 则`code .`可以键入以打开编辑器。

1. 将以下程序粘贴到**索引 .js**文件中。 您可以使用**Ctrl + V**键盘快捷方式, 或右键单击以粘贴。

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. 保存文件&mdash;您可以使用 "..."云命令行管理程序编辑器右上角的菜单。

1. 运行应用程序以确保其正确执行。 它应显示 "Hello, World!" 到控制台。

    ```bash
    node index.js
    ```

::: zone-end