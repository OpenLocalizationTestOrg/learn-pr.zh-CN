<span data-ttu-id="787dd-101">请注意, 我们正在处理照片共享应用程序, 该应用程序将使用 Azure 存储来管理我们代表用户存储的图片和其他数据位。</span><span class="sxs-lookup"><span data-stu-id="787dd-101">Recall that we are working on a photo-sharing application that will use Azure Storage to manage pictures and other bits of data we store on behalf of our users.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

::: zone pivot="csharp"

<span data-ttu-id="787dd-102">为了简化我们的方案, 以便我们能够重点关注存储 api, 我们将创建一个新的 .net Core 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="787dd-102">To simplify our scenario so that we can focus on the Storage APIs, we will create a new .NET Core Console application.</span></span> <span data-ttu-id="787dd-103">我们还将假定它始终具有网络连接。</span><span class="sxs-lookup"><span data-stu-id="787dd-103">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="787dd-104">但是, 您应始终强化您的应用程序, 以确保网络故障不会影响用户体验或导致应用程序本身失败。</span><span class="sxs-lookup"><span data-stu-id="787dd-104">However, you should always harden your app to ensure network failures will not impact the user experience or result in a failure of the application itself.</span></span>

## <a name="create-a-net-core-application"></a><span data-ttu-id="787dd-105">创建 .net Core 应用程序</span><span class="sxs-lookup"><span data-stu-id="787dd-105">Create a .NET Core application</span></span>

<span data-ttu-id="787dd-106">.net Core 是在 macOS、Windows 和 Linux 上运行的 .net 的跨平台版本。</span><span class="sxs-lookup"><span data-stu-id="787dd-106">.NET Core is a cross-platform version of .NET that runs on macOS, Windows, and Linux.</span></span> <span data-ttu-id="787dd-107">您可以在本地安装这些工具, 也可以使用窗口右侧的云命令行管理程序执行下面的步骤。</span><span class="sxs-lookup"><span data-stu-id="787dd-107">You can install the tools locally or use the Cloud Shell on the right side of the window to execute the below steps below.</span></span>

1. <span data-ttu-id="787dd-108">登录云命令行管理程序或打开一个命令行会话, 并创建一个名为 "PhotoSharingApp" 的新 .net Core 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="787dd-108">Sign into the Cloud Shell or open a command-line session and create a new .NET Core Console application with the name "PhotoSharingApp".</span></span> <span data-ttu-id="787dd-109">您可以添加`-o`或`--output`标记以在特定文件夹中创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="787dd-109">You can add the `-o` or `--output` flag to create the app in a specific folder.</span></span>

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. <span data-ttu-id="787dd-110">运行应用程序以确保其生成和执行正确。</span><span class="sxs-lookup"><span data-stu-id="787dd-110">Run the app to make sure it builds and executes correctly.</span></span> <span data-ttu-id="787dd-111">它应显示 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="787dd-111">It should display "Hello World!"</span></span> <span data-ttu-id="787dd-112">到控制台。</span><span class="sxs-lookup"><span data-stu-id="787dd-112">to the console.</span></span>

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="787dd-113">为了简化我们的方案, 以便我们能够重点关注存储 api, 我们将创建可从控制台运行的新 node.js 应用程序。</span><span class="sxs-lookup"><span data-stu-id="787dd-113">To simplify our scenario so that we can focus on the Storage APIs, we will create a new Node.js application that can run from the console.</span></span> <span data-ttu-id="787dd-114">我们还将假定它始终具有网络连接。</span><span class="sxs-lookup"><span data-stu-id="787dd-114">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="787dd-115">但是, 您应始终强化您的应用程序, 以确保网络故障不会影响用户体验, 或导致应用程序本身失败。</span><span class="sxs-lookup"><span data-stu-id="787dd-115">However, you should always harden your app to ensure network failures will not impact the user experience, or result in a failure of the application itself.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="787dd-116">创建一个 node.js 应用程序</span><span class="sxs-lookup"><span data-stu-id="787dd-116">Create a Node.js application</span></span>

<span data-ttu-id="787dd-117">node.js 是运行 JavaScript 应用程序的流行框架。</span><span class="sxs-lookup"><span data-stu-id="787dd-117">Node.js is a popular framework for running JavaScript apps.</span></span> <span data-ttu-id="787dd-118">它通常用于 web 应用程序, 但也可以使用它从命令行运行逻辑。</span><span class="sxs-lookup"><span data-stu-id="787dd-118">It is most commonly used for web apps, but you can use it to run logic from the command line as well.</span></span> <span data-ttu-id="787dd-119">如果您已在本地安装这些工具, 则可以从命令行运行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="787dd-119">If you have the tools installed locally, you can run the following steps from a command line.</span></span> <span data-ttu-id="787dd-120">或者, 也可以使用窗口右侧的云命令行管理程序执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="787dd-120">Alternatively, you can use the Cloud Shell on the right side of the window to execute the below steps.</span></span>

1. <span data-ttu-id="787dd-121">登录云命令行管理程序或打开一个命令行会话, 并创建一个名为 "PhotoSharingApp" 的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="787dd-121">Sign into the Cloud Shell or open a command-line session and create a new folder named "PhotoSharingApp".</span></span>

    ```bash
    mkdir PhotoSharingApp
    ```

1. <span data-ttu-id="787dd-122">转到新文件夹, 并使用`npm`初始化新的 node.js 应用。</span><span class="sxs-lookup"><span data-stu-id="787dd-122">Change into the new folder and use `npm` to initialize a new Node.js app.</span></span> <span data-ttu-id="787dd-123">这将创建一个包含描述应用程序的元数据的**package. json**文件。</span><span class="sxs-lookup"><span data-stu-id="787dd-123">This will create a **package.json** file containing metadata that describes the app.</span></span>

    ```bash
    cd PhotoSharingApp
    npm init -y
    ```

1. <span data-ttu-id="787dd-124">创建一个新的源文件**索引 .js**, 即我们的代码将转到该文件的位置。</span><span class="sxs-lookup"><span data-stu-id="787dd-124">Create a new source file **index.js**, which is where our code will go.</span></span>

    ```bash
    touch index.js
    ```

1. <span data-ttu-id="787dd-125">使用编辑器打开**索引 .js**文件。</span><span class="sxs-lookup"><span data-stu-id="787dd-125">Open the **index.js** file with an editor.</span></span> <span data-ttu-id="787dd-126">如果使用的是云命令行管理程序, 则`code .`可以键入以打开编辑器。</span><span class="sxs-lookup"><span data-stu-id="787dd-126">If you are using the Cloud Shell, you can type `code .` to open an editor.</span></span>

1. <span data-ttu-id="787dd-127">将以下程序粘贴到**索引 .js**文件中。</span><span class="sxs-lookup"><span data-stu-id="787dd-127">Paste the following program into the **index.js** file.</span></span> <span data-ttu-id="787dd-128">您可以使用**Ctrl + V**键盘快捷方式, 或右键单击以粘贴。</span><span class="sxs-lookup"><span data-stu-id="787dd-128">You can use the **Ctrl+V** keyboard shortcut or right-click to paste.</span></span>

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. <span data-ttu-id="787dd-129">保存文件&mdash;您可以使用 "..."云命令行管理程序编辑器右上角的菜单。</span><span class="sxs-lookup"><span data-stu-id="787dd-129">Save the file&mdash;you can use the "..." menu on the top right corner of the Cloud Shell editor.</span></span>

1. <span data-ttu-id="787dd-130">运行应用程序以确保其正确执行。</span><span class="sxs-lookup"><span data-stu-id="787dd-130">Run the app to make sure it executes correctly.</span></span> <span data-ttu-id="787dd-131">它应显示 "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="787dd-131">It should display "Hello, World!"</span></span> <span data-ttu-id="787dd-132">到控制台。</span><span class="sxs-lookup"><span data-stu-id="787dd-132">to the console.</span></span>

    ```bash
    node index.js
    ```

::: zone-end