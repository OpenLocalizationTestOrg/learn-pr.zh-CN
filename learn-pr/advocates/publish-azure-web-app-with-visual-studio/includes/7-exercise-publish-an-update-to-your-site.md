<span data-ttu-id="06148-101">你的 Alpine 滑雪房子 web 应用已准备好并在运行, 但现在你需要将其显示给老板。</span><span class="sxs-lookup"><span data-stu-id="06148-101">Your Alpine Ski House web app is up and running, but now you need to show it to your boss.</span></span> <span data-ttu-id="06148-102">您需要更新网站并将这些更新发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="06148-102">You are going to have to update the site and publish those updates to Azure.</span></span>

## <a name="update-your-web-app"></a><span data-ttu-id="06148-103">更新 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="06148-103">Update your web app</span></span>

### <a name="replace-the-boilerplate-code"></a><span data-ttu-id="06148-104">替换样本代码</span><span class="sxs-lookup"><span data-stu-id="06148-104">Replace the boilerplate code</span></span>

1. <span data-ttu-id="06148-105">在 "**页面**" 文件夹中, 打开 "**关于. cshtml** " 文件。</span><span class="sxs-lookup"><span data-stu-id="06148-105">In the **Pages** folder, open the **About.cshtml** file.</span></span>

1. <span data-ttu-id="06148-106">在代码的底部, 找到`<p> Use this area to provide additional information. </p>`。</span><span class="sxs-lookup"><span data-stu-id="06148-106">At the bottom of the code, locate  `<p> Use this area to provide additional information. </p>`.</span></span>

1. <span data-ttu-id="06148-107">将此样本文字替换`<p>Welcome to the Alpine Ski House!</p>`为。</span><span class="sxs-lookup"><span data-stu-id="06148-107">Replace this boilerplate text with  `<p>Welcome to the Alpine Ski House!</p>`.</span></span>

1. <span data-ttu-id="06148-108">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="06148-108">Save the file.</span></span>

1. <span data-ttu-id="06148-109">打开**About.cshtml.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="06148-109">Open the **About.cshtml.cs** file.</span></span>

1. <span data-ttu-id="06148-110">将`Message`字符串替换为说**Alpine 滑雪房子是东北的首要滑雪峰。**</span><span class="sxs-lookup"><span data-stu-id="06148-110">Replace the `Message` string to say  **Alpine Ski House is the premier ski hill in Northeast.**</span></span>

1. <span data-ttu-id="06148-111">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="06148-111">Save the file.</span></span>

### <a name="publish-your-updates"></a><span data-ttu-id="06148-112">发布更新</span><span class="sxs-lookup"><span data-stu-id="06148-112">Publish your updates</span></span>

1. <span data-ttu-id="06148-113">在 "解决方案资源管理器" 中, 右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="06148-113">In Solution Explorer, right-click the project.</span></span>

1. <span data-ttu-id="06148-114">选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="06148-114">Select **Publish**.</span></span> <span data-ttu-id="06148-115">应具有包含 [网站]-web deploy 的选项。</span><span class="sxs-lookup"><span data-stu-id="06148-115">You should have an option that includes your [website]-web deploy.</span></span>

1. <span data-ttu-id="06148-116">选择您的网站, Visual Studio 会将您所做的更改发送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="06148-116">Select your site, and Visual Studio will send your changes to Azure.</span></span>

### <a name="view-your-changes"></a><span data-ttu-id="06148-117">查看所做的更改</span><span class="sxs-lookup"><span data-stu-id="06148-117">View your changes</span></span>

<span data-ttu-id="06148-118">发布所做的更改后, Visual Studio 将在浏览器中打开该网站。</span><span class="sxs-lookup"><span data-stu-id="06148-118">Once you've published your changes, Visual Studio will open the site in your browser.</span></span> <span data-ttu-id="06148-119">导航到 "**关于**" 页, 并查看您所做的更改已反映出来。</span><span class="sxs-lookup"><span data-stu-id="06148-119">Navigate to the **About** page, and see that your changes are reflected.</span></span>

## <a name="congrats"></a><span data-ttu-id="06148-120">Congrats!</span><span class="sxs-lookup"><span data-stu-id="06148-120">Congrats!</span></span>

<span data-ttu-id="06148-121">您已成功使用 Visual Studio 2017 更新 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="06148-121">You have successfully updated your web app using Visual Studio 2017.</span></span>
