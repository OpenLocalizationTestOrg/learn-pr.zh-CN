我们打算使用 Azure 函数来托管此代码。 您将为每个函数创建一个`JavaScript` Azure Function App 和 HTTP 触发器, 然后在本地运行和调试这些函数。

## <a name="create-an-azure-function-project"></a>创建 Azure 函数项目

Azure 函数是在无需显式配置任何云基础结构的情况下执行的代码片段。

Azure Function 项目是多个函数的容器。 函数以不同的方式触发;你将通过发出 HTTP 请求来触发你的函数。

有多种方法可以创建 Azure 函数。 一种更简单的方法是使用 Visual Studio Code 和 Azure 函数扩展。

1. 打开 Visual Studio Code。

1. 在 Visual Studio Code 中, 打开 "克隆的 github 源代码" 文件夹。

    >[!IMPORTANT]
    > 此文件夹是您将在其中开发 Azure 函数的位置。 此处提供的代码提供了所需的基架。

1. 依次单击 "**查看**" 和 "**命令组件面板**", 然后搜索并选择 " **Azure 函数: 新建项目 ...**"。

   > [!NOTE]
   > 如果要求您覆盖文件 (如`.gitignore`), 请回答**no** all。

   !["新建 Azure 函数" 对话框将显示在 VS 代码屏幕的顶部。](../media/4.create-new-project.png)

1. 选择要在其中创建函数应用程序的文件夹。 选择当前文件夹 (在 Visual Studio code 中打开的文件夹)

   ![在 VS 代码顶部选择 "文件夹" 对话框。](../media/4.select-folder.png)

1. 选择 " **JavaScript** " 作为所需的语言。

   ![选择语言。 映像中的可用选项包括 JavaScript、Java 和 c #。](../media/4.select-language.png)

1. 在**** 要求覆盖`.gitignore`文件时选择 "否"

1. 您应看到在`host.json`项目`proxies.json`文件夹中`local.settings.json`创建的、和文件。

   ![使用前面所述文件的文件列表创建的应用程序。](../media/4.app-created.png)

## <a name="create-an-azure-function"></a>创建 Azure 函数

现在, 你将创建 Azure 函数本身。 这是响应 HTTP 请求的代码段。

同样, 您将使用 Visual Studio Code Extension。

1. 依次单击 "**查看**" 和 "**命令选项板**", 然后搜索并选择**Azure 函数: Create Function ...**

    ![在 VS 代码窗口顶部创建新的函数对话框。](../media/4.create-function.png)

1. 选择最初在其中创建 function 项目的文件夹。

    ![显示当前文件夹位置的 "选择文件夹" 对话框。](../media/4.select-current-project.png)

1. 选择 " **HTTP 触发器**" 选项。

    ![从可用触发器列表中选择 "HTTP 触发器", 包括 blob、队列和计时器触发器, 以及用于更改各种设置 (如 project runtime、project language 和 template filter) 的三个选项。](../media/4.select-trigger.png)

1. 键入`MojifyImage`作为函数的名称。

    ![使用文本字段中提供的 MojifyImage 选择 "名称" 对话框。](../media/4.choose-function-name.png)

1. 选择 "**匿名**" 作为身份验证级别。

    > [!NOTE]
    > 通过选择 "**匿名**", 函数在世界范围内开放且不安全。 如果将来创建其他函数, 则不建议使用此默认行为。 由于这是使用免费 Azure 学习资源的低风险操作, 因此目前尚不存在问题。

    !["选择授权级别" 对话框提供可供选择的匿名、功能和管理选项。](../media/4.choose-auth-level.png)

## <a name="run-the-function-locally"></a>在本地运行函数

完成这些命令后, 您将把初学者项目转换为具有调用`MojifyImage`的**HTTP trigger**函数的 function 项目。

1. 单击 "**终端**", 然后单击 "**新建终端**" 打开 Visual Studio 终端

2. 在本地的终端中运行函数应用程序

    ```bash
    func host start
    ```

    这将在本地启动函数的运行时。 如果工作正常, 则会看到打印有本地`MojifyImage` URL 的输出。

    ```output
    Http Functions:

            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

    > [!TIP]
    > 使用本地 Azure 函数运行时的优势之一是, 它允许我们使用在生产中运行函数时使用的相同基础技术运行函数。

3. 若要确认该函数是否正常工作, 请访问打印到控制台的 URL。

    ![在浏览器中工作的功能应用程序正常运行。 此函数应用程序显示文本 "请在查询字符串或请求正文中传递名称", 因为它请求传递到信息中。](../media/4.default-function-app-working.png)

## <a name="debug-the-function-locally"></a>在本地调试函数

> [!Important]
> 在尝试使用 Visual Studio `func host start` Code 调试命令之前, 请确保通过在终端中键入<kbd>ctrl-c</kbd>退出该命令。

您可以在 Visual Studio Code 中运行和调试应用程序。

1. 在 JavaScript 函数的顶部`index.js` , 向文件中添加一个断点。

    ![将断点添加到索引 .js。](../media/4.add-breakpoint.png)

1. 在调试模式下运行该函数, 方法是**** 单击 " ![调试" 图标 Visual Studio Code debug 图标, 该图标看起来像有一条线的错误)。](../media/4.debug.icon.png).

    选择 "从调试配置**附加到 JavaScript 函数**", 然后选择绿色三角形以启动调试会话。

    > [!Note]
    > 当您创建函数项目时, 将自动添加**附加到 JavaScript 函数**调试配置。

1. 为`func host start`您运行命令;终端应使用相同的输出打开。

    ```output
    Http Functions:
    
            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

1. 调试菜单栏会在调试后出现。

    ![Closeup 的调试菜单栏, 包含可用于调试的各种按钮。 屏幕还显示了索引 .js-demo 应用作为我们在标题栏中的位置。](../media/4.debug-menu-bar.png)

现在, 当您访问 URL 时, 它会在您指定的断点处断开, 并且您可以逐步完成该函数。
