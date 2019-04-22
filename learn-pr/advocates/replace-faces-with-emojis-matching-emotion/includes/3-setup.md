## <a name="face-api-registration"></a><span data-ttu-id="5d0c2-101">面孔 API 注册</span><span class="sxs-lookup"><span data-stu-id="5d0c2-101">Face API registration</span></span>

<span data-ttu-id="5d0c2-102">拥有 Azure 沙盒订阅后, 可以添加面孔 api 资源并获取连接到此 API 所需的面孔 api URL 和密钥。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-102">Once you have your Azure sandbox subscription, you can add a Face API resource and obtain the Face API URL and key needed to connect to this API.</span></span>

1. <span data-ttu-id="5d0c2-103">转到[Azure 认知服务面孔服务](https://azure.microsoft.com/en-us/services/cognitive-services/face?azure-portal=true)并单击 " **Try 面孔**"。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-103">Go to the [Azure Cognitive Services Face Service](https://azure.microsoft.com/en-us/services/cognitive-services/face?azure-portal=true) and click on **Try Face**.</span></span> <span data-ttu-id="5d0c2-104">单击 "**现有 Azure 帐户**" 框中的 "**登录**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-104">Click on the **Sign In** button in the **Existing Azure Account** box.</span></span> <span data-ttu-id="5d0c2-105">这将转到 Azure 门户, 并打开 "**创建表面**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-105">This will take you to the Azure Portal and open the **Create Face** dialog box.</span></span> <span data-ttu-id="5d0c2-106">输入以下信息:</span><span class="sxs-lookup"><span data-stu-id="5d0c2-106">Enter the following information:</span></span>

    - <span data-ttu-id="5d0c2-107">Azure 面孔资源的名称</span><span class="sxs-lookup"><span data-stu-id="5d0c2-107">a name for the Azure Face resource</span></span>
    - <span data-ttu-id="5d0c2-108">`Concierge Subscription`订阅的</span><span class="sxs-lookup"><span data-stu-id="5d0c2-108">`Concierge Subscription` for the subscription</span></span>
    - <span data-ttu-id="5d0c2-109">保留其默认值的位置</span><span class="sxs-lookup"><span data-stu-id="5d0c2-109">leave the location at its default value</span></span>
    - <span data-ttu-id="5d0c2-110">`F0`对于定价层</span><span class="sxs-lookup"><span data-stu-id="5d0c2-110">`F0` for pricing tier</span></span>
    - <span data-ttu-id="5d0c2-111">资源组的**<rgn>沙盒资源组</rgn>**</span><span class="sxs-lookup"><span data-stu-id="5d0c2-111">**<rgn>Sandbox Resource Group</rgn>** for the Resource Group</span></span>

1. <span data-ttu-id="5d0c2-112">成功部署 Azure 资源后, 请转到此资源并记录 API**终结点**和**注册表项**。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-112">Once the Azure resource has been deployed successfully, go to this resource and make a note of the API **Endpoint** and **keys**.</span></span> <span data-ttu-id="5d0c2-113">你将需要其中一个密钥来调用面孔 API。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-113">You will need one of the keys to call the Face API.</span></span> <span data-ttu-id="5d0c2-114">您可以使用任一键。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-114">You can use either of the keys.</span></span>

## <a name="slack-workspace"></a><span data-ttu-id="5d0c2-115">可宽延时间工作区</span><span class="sxs-lookup"><span data-stu-id="5d0c2-115">Slack workspace</span></span>

<span data-ttu-id="5d0c2-116">若要创建可宽延时间命令, 您需要具有可宽延时间的工作区的管理员权限。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-116">To create a Slack command, you need administrator privileges for a Slack workspace.</span></span>

1. <span data-ttu-id="5d0c2-117">如果您有一个可宽延时间工作区, 并且您具有管理员权限, 则可以使用该工作区。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-117">If you already have a Slack workspace where you have admin privileges, you can use that.</span></span> <span data-ttu-id="5d0c2-118">您还可以[创建新的 "全新可宽延时间" 工作区](https://slack.com/create?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-118">You can also [create a brand new Slack workspace](https://slack.com/create?azure-portal=true).</span></span>

## <a name="local-setup"></a><span data-ttu-id="5d0c2-119">本地安装</span><span class="sxs-lookup"><span data-stu-id="5d0c2-119">Local setup</span></span>

<span data-ttu-id="5d0c2-120">你可以在本地计算机上执行此模块中的大多数练习, 并将其部署到 Azure 沙盒作为最后一步。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-120">You do most of the exercises in this module on your local machine, deploying to your Azure sandbox as the final step.</span></span>

1. <span data-ttu-id="5d0c2-121">安装 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5d0c2-121">Install Visual Studio Code</span></span>

    <span data-ttu-id="5d0c2-122">如果尚未安装, 请下载并安装[Visual Studio Code](https://code.visualstudio.com?azure-portal=true)</span><span class="sxs-lookup"><span data-stu-id="5d0c2-122">If you don't have it already, download and install [Visual Studio Code](https://code.visualstudio.com?azure-portal=true)</span></span>

1. <span data-ttu-id="5d0c2-123">向 Visual Studio Code 中添加 Azure 扩展</span><span class="sxs-lookup"><span data-stu-id="5d0c2-123">Add Azure Extensions to Visual Studio Code</span></span>

    <span data-ttu-id="5d0c2-124">如果尚未安装这些扩展, 请安装以下 VS 代码扩展:</span><span class="sxs-lookup"><span data-stu-id="5d0c2-124">If you don't have them already, install these VS Code extensions:</span></span>
    - [<span data-ttu-id="5d0c2-125">Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="5d0c2-125">Azure Account</span></span>](https://marketplace.visualstudio.com/items?azure-portal=true&itemName=ms-vscode.azure-account)
    - [<span data-ttu-id="5d0c2-126">Azure 函数</span><span class="sxs-lookup"><span data-stu-id="5d0c2-126">Azure Functions</span></span>](https://marketplace.visualstudio.com/items?azure-portal=true&itemName=ms-azuretools.vscode-azurefunctions)

1. <span data-ttu-id="5d0c2-127">安装节点和 npm</span><span class="sxs-lookup"><span data-stu-id="5d0c2-127">Install node and npm</span></span>

   <span data-ttu-id="5d0c2-128">如果尚未在计算机上本地安装它们, 请为您的操作系统安装[node 和 npm](https://nodejs.org/en/download?azure-portal=true) 。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-128">If you don't already have them installed locally on your machine, Install [node and npm](https://nodejs.org/en/download?azure-portal=true) for your operating system.</span></span>

1. <span data-ttu-id="5d0c2-129">克隆起始代码</span><span class="sxs-lookup"><span data-stu-id="5d0c2-129">Clone the starter code</span></span>

    <span data-ttu-id="5d0c2-130">克隆起始代码可帮助您充分利用本模块。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-130">Cloning the starter code will help you get the most out of this module.</span></span> <span data-ttu-id="5d0c2-131">完成应用程序所需的所有代码和一些初始的引导代码都可免费开始。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-131">All of the code you need to complete the app, and some initial bootstrap code, is available for free to get you started.</span></span>

    ```bash
    git clone https://github.com/MicrosoftDocs/mslearn-the-mojifier.git
    ```

    <span data-ttu-id="5d0c2-132">您应该能够使用所提供的代码完成项目, 但如果您无法确定事情, 则可以在`completed`分支中找到已完成的代码。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-132">You should be able to complete the project using the code provided, but if you can't figure something out, then you can find the completed code in the `completed` branch.</span></span>

1. <span data-ttu-id="5d0c2-133">转到包含克隆的源存储库的目录中, 然后安装所需的程序包:</span><span class="sxs-lookup"><span data-stu-id="5d0c2-133">Change into the directory containing the cloned source repository, then install the required packages:</span></span>

    ```bash
    cd mslearn-the-mojifier
    npm install
    ```

1. <span data-ttu-id="5d0c2-134">将 TypeScript 代码编译为 JavaScript</span><span class="sxs-lookup"><span data-stu-id="5d0c2-134">Compile the TypeScript code into JavaScript</span></span>

    <span data-ttu-id="5d0c2-135">您将使用 TypeScript 编写应用程序。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-135">You are going to write your app using TypeScript.</span></span> <span data-ttu-id="5d0c2-136">TypeScript 支持类型检查和类定义, 我们将在我们的 Mojifier 代码中使用它们。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-136">TypeScript has support for type-checking and class definitions, which we will make use of in our Mojifier code.</span></span> <span data-ttu-id="5d0c2-137">node.js 不知道如何运行 typescript, 因此在开发时, 需要将 TypeScript 代码转换为 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-137">Node.js does not know how to run TypeScript, so as you develop, you'll need to convert your TypeScript code to JavaScript.</span></span> <span data-ttu-id="5d0c2-138">在运行上面`tsc`的`npm install`命令时, 将`package.json`会安装 TypeScript 编译器, 并将配置为在生成阶段运行它。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-138">The TypeScript compiler `tsc` is installed when you run the `npm install` command above, and the `package.json` is configured to run it in the build stage.</span></span> <span data-ttu-id="5d0c2-139">运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="5d0c2-139">Run the following command:</span></span>

    ```bash
    npm run build
    ```

    <span data-ttu-id="5d0c2-140">保持此命令在终端命令行管理程序中运行。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-140">Keep this command running in a terminal shell.</span></span> <span data-ttu-id="5d0c2-141">这将监视对 TypeScript 文件所做的任何更改, 并将其转换为 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-141">This watches for any changes to the TypeScript files and converts them to JavaScript files.</span></span> <span data-ttu-id="5d0c2-142">如果您在练习中看不到所需的行为, 请检查 "终端" 窗口中的控制台输出, 因为您的 TypeScript 代码中可能存在错误。</span><span class="sxs-lookup"><span data-stu-id="5d0c2-142">If you aren't seeing the behavior you expect in the exercises, check the console output in the terminal window as there may be errors in your TypeScript code.</span></span>
