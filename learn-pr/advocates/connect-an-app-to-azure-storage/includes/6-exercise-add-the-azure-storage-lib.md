::: zone pivot="csharp"
<span data-ttu-id="a7ad3-101">让我们将 Azure 存储客户端库集成到 .net Core 控制台应用程序中。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-101">Let's integrate the Azure Storage client library into your .NET Core console application.</span></span>

<span data-ttu-id="a7ad3-102">适用于 .net 的 Azure 存储客户端库是通过 NuGet 分发的。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-102">The Azure storage client library for .NET is distributed with NuGet.</span></span> <span data-ttu-id="a7ad3-103">您需要将**WindowsAzure**包添加到 .net 或 .net Core 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-103">You will want to add the **WindowsAzure.Storage** package to your .NET or .NET Core applications.</span></span>

## <a name="add-the-azure-storage-nuget-package"></a><span data-ttu-id="a7ad3-104">添加 Azure 存储 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a7ad3-104">Add the Azure Storage NuGet package</span></span>

1. <span data-ttu-id="a7ad3-105">在终端中, `cd`如果尚不存在, 则为 PhotoSharingApp 目录。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-105">In the terminal, `cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="a7ad3-106">将**WindowsAzure**包添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-106">Add the **WindowsAzure.Storage** package to the application.</span></span>

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. <span data-ttu-id="a7ad3-107">这会导致在客户端库和所有必需的依赖项下载时出现一些控制台活动。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-107">This should result in some console activity while the client library and all the required dependencies are downloaded.</span></span> <span data-ttu-id="a7ad3-108">完成后, 继续操作并再次生成并运行应用程序, 以确保一切就绪即可开始进行。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-108">Once it's done, go ahead and build and run the app again to make sure everything is ready to go.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="a7ad3-109">与之前一样, 它应输出 "Hello World!"。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-109">As before, it should output "Hello World!".</span></span>

::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="a7ad3-110">让将**node.js 和 JavaScript 的 Microsoft Azure 存储客户端库**集成到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-110">Let's integrate the **Microsoft Azure Storage Client Library for Node.js and JavaScript** into your application.</span></span>

<span data-ttu-id="a7ad3-111">可通过节点包管理器 (NPM) 获取 node.js 的客户端库。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-111">The client library for Node.js is available through the Node Package manager (NPM).</span></span> <span data-ttu-id="a7ad3-112">你需要将**azure 存储**包添加到你的**程序包 json**文件中。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-112">You will want to add the **azure-storage** package to your **packages.json** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a7ad3-113">用于**node.js 和 JavaScript 的 Microsoft Azure 存储客户端库**适用于服务器应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-113">The **Microsoft Azure Storage Client Library for Node.js and JavaScript** is intended for server applications.</span></span> <span data-ttu-id="a7ad3-114">如果要执行客户端 JavaScript, 则需要使用**适用于 JavaScript 的 Azure 存储客户端库**, 以提供与在浏览器中运行的功能相同但功能更好的功能。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-114">If you are doing client-side JavaScript, you will want to use the **Azure Storage Client Library for JavaScript**, which provides the same functionality but is tailored to running in a browser.</span></span>

## <a name="add-the-azure-storage-package"></a><span data-ttu-id="a7ad3-115">添加 Azure 存储包</span><span class="sxs-lookup"><span data-stu-id="a7ad3-115">Add the Azure Storage package</span></span>

1. <span data-ttu-id="a7ad3-116">如果尚不存在`cd` , 请在云命令行管理程序中的 PhotoSharingApp 目录。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-116">In Cloud Shell, `cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="a7ad3-117">将**azure 存储**包添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-117">Add the **azure-storage** package to the application.</span></span> <span data-ttu-id="a7ad3-118">请务必提供此`--save`选项, 使其与**包 json**保持不变。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-118">Make sure to supply the `--save` option so it persists to **packages.json**.</span></span>

    ```bash
    npm install azure-storage --save
    ```

1. <span data-ttu-id="a7ad3-119">这会导致在客户端库和所有必需的依赖项下载时出现一些控制台活动。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-119">This should result in some console activity while the client library and all the required dependencies are downloaded.</span></span> <span data-ttu-id="a7ad3-120">完成后, 继续操作并再次生成并运行应用程序, 以确保一切就绪即可开始进行。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-120">Once it's done, go ahead and build and run the app again to make sure everything is ready to go.</span></span>

    ```bash
    node index.js
    ```

1. <span data-ttu-id="a7ad3-121">与之前一样, 它应输出 "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="a7ad3-121">As before, it should output "Hello, World!"</span></span>

::: zone-end

<span data-ttu-id="a7ad3-122">现在, 我们已准备好了必要的库, 我们来看看您在代码中使用 Azure 存储时要执行的常见任务。</span><span class="sxs-lookup"><span data-stu-id="a7ad3-122">Now that we have the necessary libraries in place, let's look at the common tasks you'll do in your code to work with Azure storage.</span></span>
