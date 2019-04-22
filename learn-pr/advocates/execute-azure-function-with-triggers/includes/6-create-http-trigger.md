<span data-ttu-id="df175-101">在此单元中, 我们将创建一个 Azure 函数, 它接受包含单个字符串的 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="df175-101">In this unit, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="df175-102">函数将返回返回给调用方的字符串, 以表示成功或失败。</span><span class="sxs-lookup"><span data-stu-id="df175-102">The function returns a string back to the caller to represent success or failure.</span></span> <span data-ttu-id="df175-103">我们将继续处理上一个练习中的函数。</span><span class="sxs-lookup"><span data-stu-id="df175-103">We'll continue working on the function from the previous exercise.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="df175-104">创建 HTTP 触发器</span><span class="sxs-lookup"><span data-stu-id="df175-104">Create an HTTP trigger</span></span>

<span data-ttu-id="df175-105">让我们继续使用现有的 Azure 函数应用程序, 并添加 HTTP 触发器。</span><span class="sxs-lookup"><span data-stu-id="df175-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="df175-106">请确保使用随激活沙盒的相同帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="df175-106">Make sure you are signed into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="df175-107">导航到 "**所有资源**" 屏幕, 然后选择您的函数应用程序。</span><span class="sxs-lookup"><span data-stu-id="df175-107">Navigate to the **All resources** screen and select your function app.</span></span>

1. <span data-ttu-id="df175-108">选择 "函数"**+** 旁边的 "添加\*\*\*\*" () 按钮。</span><span class="sxs-lookup"><span data-stu-id="df175-108">Select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="df175-109">此操作将启动函数创建过程。</span><span class="sxs-lookup"><span data-stu-id="df175-109">This action starts the function creation process.</span></span>

1. <span data-ttu-id="df175-110">在可用于此函数应用程序的所有模板的列表中, 选择 " **HTTP 触发器**"。</span><span class="sxs-lookup"><span data-stu-id="df175-110">In the list of all templates available to this function app, select **HTTP trigger** .</span></span>

1. <span data-ttu-id="df175-111">在 "**新建函数**" 对话框中, 选择函数的名称, 然后从 "**授权级别**" 下拉列表中选择 "*匿名*"。</span><span class="sxs-lookup"><span data-stu-id="df175-111">In the **New Function** dialog, choose a name for the function and select  *Anonymous* from the **Authorization level** dropdown.</span></span>
1. <span data-ttu-id="df175-112">选择 "**创建**" 以创建函数。</span><span class="sxs-lookup"><span data-stu-id="df175-112">Select **Create** to create the function.</span></span> 

1. <span data-ttu-id="df175-113">快速查看自动生成的代码, 以了解即将发生的情况。</span><span class="sxs-lookup"><span data-stu-id="df175-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="df175-114">*必需*参数表示传入请求并包含*name*参数。</span><span class="sxs-lookup"><span data-stu-id="df175-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="df175-115">我们检查*名称*是否具有值。</span><span class="sxs-lookup"><span data-stu-id="df175-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="df175-116">如果是这样, 我们将返回问候语。</span><span class="sxs-lookup"><span data-stu-id="df175-116">If it does, we return a greeting.</span></span> <span data-ttu-id="df175-117">否则, 我们将返回一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="df175-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="df175-118">获取您的函数 URL</span><span class="sxs-lookup"><span data-stu-id="df175-118">Get your function URL</span></span>

<span data-ttu-id="df175-119">现在, 我们已创建了 HTTP 触发器, 让我们获取函数 URL, 以便我们可以开始发出请求。</span><span class="sxs-lookup"><span data-stu-id="df175-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="df175-120">选择您的 HTTP 触发器以打开 "代码" 屏幕。</span><span class="sxs-lookup"><span data-stu-id="df175-120">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="df175-121">在 "**运行**" 的右侧, 选择 "**获取函数 URL**"。</span><span class="sxs-lookup"><span data-stu-id="df175-121">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="df175-122">选择 "**复制**", 然后关闭函数 URL 弹出菜单。</span><span class="sxs-lookup"><span data-stu-id="df175-122">Select **Copy**, then close the function URL popup.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="df175-123">向 HTTP 触发器发出 GET 请求</span><span class="sxs-lookup"><span data-stu-id="df175-123">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="df175-124">现在, 我们已将函数 URL 复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="df175-124">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="df175-125">让我们发出一个 get 请求, 以查看我们是否收到响应。</span><span class="sxs-lookup"><span data-stu-id="df175-125">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="df175-126">在 web 浏览器中打开新选项卡。</span><span class="sxs-lookup"><span data-stu-id="df175-126">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="df175-127">将 URL 粘贴到地址栏中。</span><span class="sxs-lookup"><span data-stu-id="df175-127">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="df175-128">使用您的名称添加名为*name*的查询字符串参数 (例如`.../api/HttpTriggerCSharp1?name=Jesse`</span><span class="sxs-lookup"><span data-stu-id="df175-128">Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`</span></span>

1. <span data-ttu-id="df175-129">按<kbd>enter</kbd>以提交请求。</span><span class="sxs-lookup"><span data-stu-id="df175-129">Press <kbd>ENTER</kbd> to submit the request.</span></span>
