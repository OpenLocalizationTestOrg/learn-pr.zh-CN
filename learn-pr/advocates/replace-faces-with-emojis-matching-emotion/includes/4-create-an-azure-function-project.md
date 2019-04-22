<span data-ttu-id="e86f2-101">我们打算使用 Azure 函数来托管此代码。</span><span class="sxs-lookup"><span data-stu-id="e86f2-101">We're going to use Azure Functions to host this code.</span></span> <span data-ttu-id="e86f2-102">您将为每个函数创建一个`JavaScript` Azure Function App 和 HTTP 触发器, 然后在本地运行和调试这些函数。</span><span class="sxs-lookup"><span data-stu-id="e86f2-102">You'll create an Azure Function App and `JavaScript` HTTP triggers for each function, then locally run and debug these functions.</span></span>

## <a name="create-an-azure-function-project"></a><span data-ttu-id="e86f2-103">创建 Azure 函数项目</span><span class="sxs-lookup"><span data-stu-id="e86f2-103">Create an Azure Function project</span></span>

<span data-ttu-id="e86f2-104">Azure 函数是在无需显式配置任何云基础结构的情况下执行的代码片段。</span><span class="sxs-lookup"><span data-stu-id="e86f2-104">An Azure Function is a snippet of code that is executed without you having to explicitly configure any cloud infrastructure.</span></span>

<span data-ttu-id="e86f2-105">Azure Function 项目是多个函数的容器。</span><span class="sxs-lookup"><span data-stu-id="e86f2-105">An Azure Function project is a container for multiple functions.</span></span> <span data-ttu-id="e86f2-106">函数以不同的方式触发;你将通过发出 HTTP 请求来触发你的函数。</span><span class="sxs-lookup"><span data-stu-id="e86f2-106">Functions are triggered in different ways; you'll be triggering your functions by making an HTTP request.</span></span>

<span data-ttu-id="e86f2-107">有多种方法可以创建 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="e86f2-107">There are many ways to create Azure Functions.</span></span> <span data-ttu-id="e86f2-108">一种更简单的方法是使用 Visual Studio Code 和 Azure 函数扩展。</span><span class="sxs-lookup"><span data-stu-id="e86f2-108">One of the easier ways is with Visual Studio Code and the Azure Functions extension.</span></span>

1. <span data-ttu-id="e86f2-109">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="e86f2-109">Open Visual Studio Code.</span></span>

1. <span data-ttu-id="e86f2-110">在 Visual Studio Code 中, 打开 "克隆的 github 源代码" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e86f2-110">In Visual Studio Code, open the cloned github source code folder.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="e86f2-111">此文件夹是您将在其中开发 Azure 函数的位置。</span><span class="sxs-lookup"><span data-stu-id="e86f2-111">This folder is where you will develop your Azure functions.</span></span> <span data-ttu-id="e86f2-112">此处提供的代码提供了所需的基架。</span><span class="sxs-lookup"><span data-stu-id="e86f2-112">The code provided in here provides the scaffolding you need.</span></span>

1. <span data-ttu-id="e86f2-113">依次单击 "**查看**" 和 "**命令组件面板**", 然后搜索并选择 " **Azure 函数: 新建项目 ...**"。</span><span class="sxs-lookup"><span data-stu-id="e86f2-113">Click on **View** then **Command Palette**, then search for and select **Azure Functions: Create New Project...**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e86f2-114">如果要求您覆盖文件 (如`.gitignore`), 请回答**no** all。</span><span class="sxs-lookup"><span data-stu-id="e86f2-114">If you're asked to overwrite files, like `.gitignore`, answer **no** to all.</span></span>

   !["新建 Azure 函数" 对话框将显示在 VS 代码屏幕的顶部。](../media/4.create-new-project.png)

1. <span data-ttu-id="e86f2-116">选择要在其中创建函数应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e86f2-116">Select the folder where you want to create the function app.</span></span> <span data-ttu-id="e86f2-117">选择当前文件夹 (在 Visual Studio code 中打开的文件夹)</span><span class="sxs-lookup"><span data-stu-id="e86f2-117">Select the current folder (the folder that you opened in Visual Studio code)</span></span>

   ![在 VS 代码顶部选择 "文件夹" 对话框。](../media/4.select-folder.png)

1. <span data-ttu-id="e86f2-119">选择 " **JavaScript** " 作为所需的语言。</span><span class="sxs-lookup"><span data-stu-id="e86f2-119">Choose **JavaScript** as the desired language.</span></span>

   ![选择语言。](../media/4.select-language.png)

1. <span data-ttu-id="e86f2-122">在\*\*\*\* 要求覆盖`.gitignore`文件时选择 "否"</span><span class="sxs-lookup"><span data-stu-id="e86f2-122">Choose **No** when asked to overwrite the `.gitignore` file</span></span>

1. <span data-ttu-id="e86f2-123">您应看到在`host.json`项目`proxies.json`文件夹中`local.settings.json`创建的、和文件。</span><span class="sxs-lookup"><span data-stu-id="e86f2-123">You should see the `host.json`,`proxies.json`, and `local.settings.json` files created in the project folder.</span></span>

   ![使用前面所述文件的文件列表创建的应用程序。](../media/4.app-created.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="e86f2-125">创建 Azure 函数</span><span class="sxs-lookup"><span data-stu-id="e86f2-125">Create an Azure Function</span></span>

<span data-ttu-id="e86f2-126">现在, 你将创建 Azure 函数本身。</span><span class="sxs-lookup"><span data-stu-id="e86f2-126">You're now going to create the Azure Function itself.</span></span> <span data-ttu-id="e86f2-127">这是响应 HTTP 请求的代码段。</span><span class="sxs-lookup"><span data-stu-id="e86f2-127">This is the piece of code that responds to an HTTP request.</span></span>

<span data-ttu-id="e86f2-128">同样, 您将使用 Visual Studio Code Extension。</span><span class="sxs-lookup"><span data-stu-id="e86f2-128">Again, you're going to use the Visual Studio Code Extension.</span></span>

1. <span data-ttu-id="e86f2-129">依次单击 "**查看**" 和 "**命令选项板**", 然后搜索并选择**Azure 函数: Create Function ...**</span><span class="sxs-lookup"><span data-stu-id="e86f2-129">Click on **View** then **Command Palette**, then search for and select **Azure Functions: Create Function...**</span></span>

    ![在 VS 代码窗口顶部创建新的函数对话框。](../media/4.create-function.png)

1. <span data-ttu-id="e86f2-131">选择最初在其中创建 function 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e86f2-131">Select the folder where you originally created the function project.</span></span>

    ![显示当前文件夹位置的 "选择文件夹" 对话框。](../media/4.select-current-project.png)

1. <span data-ttu-id="e86f2-133">选择 " **HTTP 触发器**" 选项。</span><span class="sxs-lookup"><span data-stu-id="e86f2-133">Select the **HTTP Trigger** option.</span></span>

    ![从可用触发器列表中选择 "HTTP 触发器", 包括 blob、队列和计时器触发器, 以及用于更改各种设置 (如 project runtime、project language 和 template filter) 的三个选项。](../media/4.select-trigger.png)

1. <span data-ttu-id="e86f2-135">键入`MojifyImage`作为函数的名称。</span><span class="sxs-lookup"><span data-stu-id="e86f2-135">Type `MojifyImage` as the name of your function.</span></span>

    ![使用文本字段中提供的 MojifyImage 选择 "名称" 对话框。](../media/4.choose-function-name.png)

1. <span data-ttu-id="e86f2-137">选择 "**匿名**" 作为身份验证级别。</span><span class="sxs-lookup"><span data-stu-id="e86f2-137">Choose **Anonymous** as the authentication level.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e86f2-138">通过选择 "**匿名**", 函数在世界范围内开放且不安全。</span><span class="sxs-lookup"><span data-stu-id="e86f2-138">By choosing **Anonymous**, the function is open to the world and insecure.</span></span> <span data-ttu-id="e86f2-139">如果将来创建其他函数, 则不建议使用此默认行为。</span><span class="sxs-lookup"><span data-stu-id="e86f2-139">If you create other functions in the future, this isn't the recommended default behavior.</span></span> <span data-ttu-id="e86f2-140">由于这是使用免费 Azure 学习资源的低风险操作, 因此目前尚不存在问题。</span><span class="sxs-lookup"><span data-stu-id="e86f2-140">Since this is a low-risk exercise with free Azure learning resources, it's not a problem for now.</span></span>

    !["选择授权级别" 对话框提供可供选择的匿名、功能和管理选项。](../media/4.choose-auth-level.png)

## <a name="run-the-function-locally"></a><span data-ttu-id="e86f2-142">在本地运行函数</span><span class="sxs-lookup"><span data-stu-id="e86f2-142">Run the function locally</span></span>

<span data-ttu-id="e86f2-143">完成这些命令后, 您将把初学者项目转换为具有调用`MojifyImage`的**HTTP trigger**函数的 function 项目。</span><span class="sxs-lookup"><span data-stu-id="e86f2-143">Once these commands complete, you'll have converted the starter project to a function project with an **HTTP trigger** function called `MojifyImage`.</span></span>

1. <span data-ttu-id="e86f2-144">单击 "**终端**", 然后单击 "**新建终端**" 打开 Visual Studio 终端</span><span class="sxs-lookup"><span data-stu-id="e86f2-144">Click on **Terminal** then **New Terminal** to open a Visual Studio terminal</span></span>

2. <span data-ttu-id="e86f2-145">在本地的终端中运行函数应用程序</span><span class="sxs-lookup"><span data-stu-id="e86f2-145">Run the function app locally, in the terminal</span></span>

    ```bash
    func host start
    ```

    <span data-ttu-id="e86f2-146">这将在本地启动函数的运行时。</span><span class="sxs-lookup"><span data-stu-id="e86f2-146">This starts the function's runtime locally.</span></span> <span data-ttu-id="e86f2-147">如果工作正常, 则会看到打印有本地`MojifyImage` URL 的输出。</span><span class="sxs-lookup"><span data-stu-id="e86f2-147">If it works, you should see an output printed with a local `MojifyImage` URL.</span></span>

    ```output
    Http Functions:

            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

    > [!TIP]
    > <span data-ttu-id="e86f2-148">使用本地 Azure 函数运行时的优势之一是, 它允许我们使用在生产中运行函数时使用的相同基础技术运行函数。</span><span class="sxs-lookup"><span data-stu-id="e86f2-148">One of the advantages of using the local Azure Functions runtime is that it allows us to run the function using the same underlying technology that would be used to run the function in production.</span></span>

3. <span data-ttu-id="e86f2-149">若要确认该函数是否正常工作, 请访问打印到控制台的 URL。</span><span class="sxs-lookup"><span data-stu-id="e86f2-149">To confirm the function is working correctly, visit the URL printed to the console.</span></span>

    ![在浏览器中工作的功能应用程序正常运行。](../media/4.default-function-app-working.png)

## <a name="debug-the-function-locally"></a><span data-ttu-id="e86f2-152">在本地调试函数</span><span class="sxs-lookup"><span data-stu-id="e86f2-152">Debug the function locally</span></span>

> [!Important]
> <span data-ttu-id="e86f2-153">在尝试使用 Visual Studio `func host start` Code 调试命令之前, 请确保通过在终端中键入<kbd>ctrl-c</kbd>退出该命令。</span><span class="sxs-lookup"><span data-stu-id="e86f2-153">Make sure you exit the `func host start` command by typing <kbd>CTRL-C</kbd> in the terminal, before trying to debug it using Visual Studio Code.</span></span>

<span data-ttu-id="e86f2-154">您可以在 Visual Studio Code 中运行和调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="e86f2-154">You can run and debug the app inside Visual Studio Code.</span></span>

1. <span data-ttu-id="e86f2-155">在 JavaScript 函数的顶部`index.js` , 向文件中添加一个断点。</span><span class="sxs-lookup"><span data-stu-id="e86f2-155">Add a breakpoint to the `index.js` file, at the top of the JavaScript function.</span></span>

    ![将断点添加到索引 .js。](../media/4.add-breakpoint.png)

1. <span data-ttu-id="e86f2-157">在调试模式下运行该函数, 方法是\*\*\*\* 单击 " ![调试" 图标 Visual Studio Code debug 图标, 该图标看起来像有一条线的错误)。](../media/4.debug.icon.png).</span><span class="sxs-lookup"><span data-stu-id="e86f2-157">Run the function in debug mode by clicking on the **Debug** icon ![Visual Studio Code Debug icon which looks like a bug with a line through it).](../media/4.debug.icon.png).</span></span>

    <span data-ttu-id="e86f2-158">选择 "从调试配置**附加到 JavaScript 函数**", 然后选择绿色三角形以启动调试会话。</span><span class="sxs-lookup"><span data-stu-id="e86f2-158">Select **Attach to JavaScript Functions** from the debug configuration before you select the green triangle to start the debug session.</span></span>

    > [!Note]
    > <span data-ttu-id="e86f2-159">当您创建函数项目时, 将自动添加**附加到 JavaScript 函数**调试配置。</span><span class="sxs-lookup"><span data-stu-id="e86f2-159">The **Attach to JavaScript Functions** debug configuration is automatically added when you created the function project.</span></span>

1. <span data-ttu-id="e86f2-160">为`func host start`您运行命令;终端应使用相同的输出打开。</span><span class="sxs-lookup"><span data-stu-id="e86f2-160">The `func host start` command is run for you; a terminal should open with the same output.</span></span>

    ```output
    Http Functions:
    
            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

1. <span data-ttu-id="e86f2-161">调试菜单栏会在调试后出现。</span><span class="sxs-lookup"><span data-stu-id="e86f2-161">The debug menu bar should appear since you're debugging.</span></span>

    ![Closeup 的调试菜单栏, 包含可用于调试的各种按钮。](../media/4.debug-menu-bar.png)

<span data-ttu-id="e86f2-164">现在, 当您访问 URL 时, 它会在您指定的断点处断开, 并且您可以逐步完成该函数。</span><span class="sxs-lookup"><span data-stu-id="e86f2-164">Now when you visit the URL, it breaks at your specified breakpoint, and you can step through through the function.</span></span>
