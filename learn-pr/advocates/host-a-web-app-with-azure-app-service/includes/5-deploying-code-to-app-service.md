<span data-ttu-id="81deb-101">现在, 我们来看看如何将应用程序部署到应用服务。</span><span class="sxs-lookup"><span data-stu-id="81deb-101">Now, let's see how we can deploy our application to App Service.</span></span>

## <a name="what-is-automated-deployment"></a><span data-ttu-id="81deb-102">什么是自动部署？</span><span class="sxs-lookup"><span data-stu-id="81deb-102">What is automated deployment?</span></span>

<span data-ttu-id="81deb-103">自动部署或持续集成是一种以快速重复模式推送新功能和 bug 修复的过程, 对最终用户影响最小。</span><span class="sxs-lookup"><span data-stu-id="81deb-103">Automated deployment, or continuous integration, is a process used to push out new features and bug fixes in a fast and repetitive pattern with minimal impact on end users.</span></span>

<span data-ttu-id="81deb-104">Azure 支持直接从多个源进行自动部署。</span><span class="sxs-lookup"><span data-stu-id="81deb-104">Azure supports automated deployment directly from several sources.</span></span> <span data-ttu-id="81deb-105">可以使用以下选项:</span><span class="sxs-lookup"><span data-stu-id="81deb-105">The following options are available:</span></span>

- <span data-ttu-id="81deb-106">**Visual Studio Team Services (VSTS)**: 可以将您的代码推送到 VSTS、在云中生成代码、运行测试、从代码中生成版本, 最后将代码推送到 Azure Web 应用。</span><span class="sxs-lookup"><span data-stu-id="81deb-106">**Visual Studio Team Services (VSTS)**: You can push your code to VSTS, build your code in the cloud, run the tests, generate a release from the code, and finally, push your code to an Azure Web App.</span></span>

- <span data-ttu-id="81deb-107">**GitHub**: Azure 支持直接从 GitHub 进行自动部署。</span><span class="sxs-lookup"><span data-stu-id="81deb-107">**GitHub**: Azure supports automated deployment directly from GitHub.</span></span> <span data-ttu-id="81deb-108">将 GitHub 存储库连接到 Azure 以实现自动部署时, 将自动为您部署在 GitHub 上推送到生产分支的任何更改。</span><span class="sxs-lookup"><span data-stu-id="81deb-108">When you connect your GitHub repository to Azure for automated deployment, any changes you push to your production branch on GitHub will be automatically deployed for you.</span></span>

- <span data-ttu-id="81deb-109">**Bitbucket**: 在其与 GitHub 的相似之处, 您可以使用 Bitbucket 配置自动部署。</span><span class="sxs-lookup"><span data-stu-id="81deb-109">**Bitbucket**: With its similarities to GitHub, you can configure an automated deployment with Bitbucket.</span></span>

- <span data-ttu-id="81deb-110">**OneDrive**: 您可以使用应用服务连接 onedrive 帐户, 以便在您更改 OneDrive 帐户上的任何文件时, Azure 将自动检测它并在 web 应用程序文件中提取任何更改。</span><span class="sxs-lookup"><span data-stu-id="81deb-110">**OneDrive**: You can connect your OneDrive account with App Service so that when you change any file on your OneDrive account, Azure will automatically detect it and pull in any changes on the web app files.</span></span> <span data-ttu-id="81deb-111">对于静态网站, 这是一个很好的选择。</span><span class="sxs-lookup"><span data-stu-id="81deb-111">This is a great option for static websites.</span></span> <span data-ttu-id="81deb-112">这将使你感觉你正在处理的本地文件系统在 Azure 上平稳且即时地反映所有更改。</span><span class="sxs-lookup"><span data-stu-id="81deb-112">It will give you the feeling that you are dealing with a local file system that reflects any changes on Azure, smoothly and instantly.</span></span>

- <span data-ttu-id="81deb-113">**收存箱**: 类似于 OneDrive, 您可以将 web 应用程序文件托管在 Dropbox 帐户中, 并让它们自动推送并通过 web 应用进行部署。</span><span class="sxs-lookup"><span data-stu-id="81deb-113">**Dropbox**: Similar to OneDrive, you can host your web app files in a Dropbox account and have them automatically push and be deployed over a web app.</span></span>

- <span data-ttu-id="81deb-114">**外部存储库**: 可以使用任何外部 Git 存储库配置自动部署。</span><span class="sxs-lookup"><span data-stu-id="81deb-114">**External repository**: You can configure automated deployment with any external Git repository.</span></span>

### <a name="non-automated-deployment-to-azure"></a><span data-ttu-id="81deb-115">到 Azure 的非自动部署</span><span class="sxs-lookup"><span data-stu-id="81deb-115">Non-automated deployment to Azure</span></span>

<span data-ttu-id="81deb-116">您可以使用几个选项手动将您的代码推送到 Azure:</span><span class="sxs-lookup"><span data-stu-id="81deb-116">There are a few options that you can use to manually push your code to Azure:</span></span>

- <span data-ttu-id="81deb-117">**ftp/S**: ftp 或 FTPS 是将代码推送到任何宿主环境的传统方法。</span><span class="sxs-lookup"><span data-stu-id="81deb-117">**FTP/S**: FTP or FTPS is a traditional way of pushing your code to any hosting environment.</span></span> <span data-ttu-id="81deb-118">尽管不建议再这样做, 但仍可以使用它。</span><span class="sxs-lookup"><span data-stu-id="81deb-118">Despite the fact that it is not recommended anymore, you can still make use of it.</span></span>

- <span data-ttu-id="81deb-119">**Web Deploy/IDE**: 您可以使用 Visual Studio IDE 将 Web 应用发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="81deb-119">**Web Deploy/IDE**: You can use the Visual Studio IDE to publish your web app to Azure.</span></span> <span data-ttu-id="81deb-120">Visual Studio 发布机制可以利用 Web Deploy 技术将您的代码推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="81deb-120">The Visual Studio publishing mechanism can make use of Web Deploy technology to push your code to Azure.</span></span>

- <span data-ttu-id="81deb-121">**Git**: Azure 为你的应用程序维护**本地 Git 存储库**。</span><span class="sxs-lookup"><span data-stu-id="81deb-121">**Git**: Azure maintains a **local Git repository** for your application.</span></span> <span data-ttu-id="81deb-122">您可以将您的代码直接**提交**给它。</span><span class="sxs-lookup"><span data-stu-id="81deb-122">You can **commit** your code directly to it.</span></span>

## <a name="summary"></a><span data-ttu-id="81deb-123">摘要</span><span class="sxs-lookup"><span data-stu-id="81deb-123">Summary</span></span>

<span data-ttu-id="81deb-124">Azure 提供了多种方法来上传代码, 以帮助它更好地满足当前工作流的需要。</span><span class="sxs-lookup"><span data-stu-id="81deb-124">Azure provides multiple ways to upload your code to help it better fit in with your current workflow.</span></span>