<span data-ttu-id="efcca-101">接下来, 我们将使用 Azure CLI 创建资源组, 然后将 web 应用程序部署到此资源组中。</span><span class="sxs-lookup"><span data-stu-id="efcca-101">Next, let's use the Azure CLI to create a resource group, and then to deploy a web app into this resource group.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="using-a-resource-group"></a><span data-ttu-id="efcca-102">使用资源组</span><span class="sxs-lookup"><span data-stu-id="efcca-102">Using a resource group</span></span>

<span data-ttu-id="efcca-103">当您使用自己的计算机和 Azure 订阅时, 您需要使用`az login`命令首次登录 Azure。</span><span class="sxs-lookup"><span data-stu-id="efcca-103">When you are working with your own machine and Azure subscription you will need to first login to Azure using the `az login` command.</span></span> <span data-ttu-id="efcca-104">这在云命令行管理程序环境中是不必要的。</span><span class="sxs-lookup"><span data-stu-id="efcca-104">This is unnecessary with the Cloud Shell environment.</span></span>

<span data-ttu-id="efcca-105">接下来, 通常使用`az group create`命令为所有相关的 Azure 资源创建资源组, 但这些练习已为您创建了一个资源组。</span><span class="sxs-lookup"><span data-stu-id="efcca-105">Next, you would normally create a resource group for all your related Azure resources with an `az group create` command, but for these exercises one has been created for you.</span></span> <span data-ttu-id="efcca-106">为您的资源组使用**<rgn>[沙盒资源组名称]</rgn>** 。</span><span class="sxs-lookup"><span data-stu-id="efcca-106">Use **<rgn>[sandbox resource group name]</rgn>** for your resource group.</span></span>

1. <span data-ttu-id="efcca-107">您可以请求 Azure CLI 列出表中的所有资源组。</span><span class="sxs-lookup"><span data-stu-id="efcca-107">You can ask the Azure CLI to list all your resource groups in a table.</span></span> <span data-ttu-id="efcca-108">在免费的 Azure 沙箱中应该只有一台。</span><span class="sxs-lookup"><span data-stu-id="efcca-108">There should just be one while you are in the free Azure sandbox.</span></span>

    ```azurecli
    az group list --output table
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="efcca-109">在执行更多 Azure 开发的过程中, 您可以最终处理几个资源组。</span><span class="sxs-lookup"><span data-stu-id="efcca-109">As you do more Azure development, you can end up with several resource groups.</span></span> <span data-ttu-id="efcca-110">如果组列表中有多个项, 则可以通过添加一个`--query`选项来筛选返回值。</span><span class="sxs-lookup"><span data-stu-id="efcca-110">If you have several items in the group list, you can filter the return values by adding a `--query` option.</span></span> <span data-ttu-id="efcca-111">尝试此命令:</span><span class="sxs-lookup"><span data-stu-id="efcca-111">Try this command:</span></span>

    ```azurecli
    az group list --query "[?name == '<rgn>[sandbox resource group name]</rgn>']"
    ```

    <span data-ttu-id="efcca-112">使用**JMESPath** (它是用于 JSON 请求的标准查询语言) 对查询进行了格式化。</span><span class="sxs-lookup"><span data-stu-id="efcca-112">The query is formated using **JMESPath** which is a standard query language for JSON requests.</span></span> <span data-ttu-id="efcca-113">您可以在中了解有关此强大的筛选<http://jmespath.org/>器语言的详细信息。</span><span class="sxs-lookup"><span data-stu-id="efcca-113">You can learn more about this powerful filter language at <http://jmespath.org/>.</span></span> <span data-ttu-id="efcca-114">我们还将更深入地介绍了如何在**Azure CLI 模块中管理虚拟机**的查询。</span><span class="sxs-lookup"><span data-stu-id="efcca-114">We also cover queries in more depth in the **Manage VMs with the Azure CLI** module.</span></span>

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="efcca-115">创建服务计划的步骤</span><span class="sxs-lookup"><span data-stu-id="efcca-115">Steps to create a service plan</span></span>

<span data-ttu-id="efcca-116">在运行使用 azure 应用服务的 Web 应用程序时, 会为应用使用的 azure 计算资源付费, 这取决于与 Web 应用关联的应用服务计划。</span><span class="sxs-lookup"><span data-stu-id="efcca-116">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="efcca-117">服务计划确定用于应用数据中心的区域、使用的 vm 数量和定价层。</span><span class="sxs-lookup"><span data-stu-id="efcca-117">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="efcca-118">创建应用服务计划以运行您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="efcca-118">Create an App Service plan to run your app.</span></span> <span data-ttu-id="efcca-119">以下命令未指定定价层或 VM 实例详细信息, 因此默认情况下, 你将获得具有1个**小型**VM 实例的**基本**计划。</span><span class="sxs-lookup"><span data-stu-id="efcca-119">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    > [!WARNING]
    > <span data-ttu-id="efcca-120">app 和 plan 的名称必须是_唯一_的, 因此, 请将后缀添加到名称中, 并`<unique>`将以下命令中的文本替换为一组数字、缩写或其他文本段, 以确保它在所有 Azure 中都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="efcca-120">The name of the app and plan must be _unique_, so add a suffix to the name and replace the `<unique>` text in the command below with a set of numbers, your initials, or some other piece of text to make sure it's unique in all of Azure.</span></span>

    <span data-ttu-id="efcca-121">对于`--location`参数, 请使用以下位置值之一。</span><span class="sxs-lookup"><span data-stu-id="efcca-121">For the `--location` parameter, use one of the below location values.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --location <location>
    ```

    <span data-ttu-id="efcca-122">此命令可能需要几分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="efcca-122">This command can take several minutes to complete.</span></span>

1. <span data-ttu-id="efcca-123">通过在表中列出所有计划, 确认已成功创建服务计划。</span><span class="sxs-lookup"><span data-stu-id="efcca-123">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="efcca-124">创建 web 应用程序的步骤</span><span class="sxs-lookup"><span data-stu-id="efcca-124">Steps to create a web app</span></span>

<span data-ttu-id="efcca-125">接下来, 您将在服务计划中创建 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="efcca-125">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="efcca-126">您可以同时部署代码, 但对于我们的示例, 我们将以单独的步骤执行此操作。</span><span class="sxs-lookup"><span data-stu-id="efcca-126">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="efcca-127">创建 web 应用程序, 提供上面创建的计划的名称。</span><span class="sxs-lookup"><span data-stu-id="efcca-127">Create the web app, supply the name of the plan you created above.</span></span> <span data-ttu-id="efcca-128">**就像计划一样, 应用名称必须是唯一**的, 将`<unique>`标记替换为一些文本, 使名称在全局范围内是唯一的。</span><span class="sxs-lookup"><span data-stu-id="efcca-128">**Just like the plan, the app name must be unique**, replace the `<unique>` marker with some text to make the name globally unique.</span></span>

    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --plan popupappplan-<unique>
    ```

1. <span data-ttu-id="efcca-129">通过在表中列出所有应用来验证是否已成功创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="efcca-129">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```azurecli
    az webapp list --output table
    ```

1. <span data-ttu-id="efcca-130">记下表中列出的**DefaultHostName** , 然后将其记录。这是新网站可访问的 web 地址。</span><span class="sxs-lookup"><span data-stu-id="efcca-130">Make a note of the **DefaultHostName** listed in the table; this is the reachable web address for the new website.</span></span> <span data-ttu-id="efcca-131">Azure 将使你的网站通过`azurewebsites.net`域中的唯一应用程序名称提供。</span><span class="sxs-lookup"><span data-stu-id="efcca-131">Azure will make your website available through the unique app name in the `azurewebsites.net` domain.</span></span> <span data-ttu-id="efcca-132">例如, 如果我的应用程序名称是 "popupwebapp-mslearn123", 则我的网站 URL 将`http://popupwebapp-mslearn123.azurewebsites.net`为:。</span><span class="sxs-lookup"><span data-stu-id="efcca-132">For example, if my app name was "popupwebapp-mslearn123", then my website URL would be: `http://popupwebapp-mslearn123.azurewebsites.net`.</span></span>

1. <span data-ttu-id="efcca-133">您的网站有一个由 Azure 创建的 "快速入门" 页面, 您可以在浏览器中或通过卷查看, 只需使用**DefaultHostName**:</span><span class="sxs-lookup"><span data-stu-id="efcca-133">Your site has a "QuickStart" page created by Azure that you can see either in a browser, or with CURL, just use the **DefaultHostName**:</span></span>

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="efcca-134">部署 GitHub 中的代码的步骤</span><span class="sxs-lookup"><span data-stu-id="efcca-134">Steps to deploy code from GitHub</span></span>

1. <span data-ttu-id="efcca-135">最后一步是将 GitHub 存储库中的代码部署到 web 应用。</span><span class="sxs-lookup"><span data-stu-id="efcca-135">The final step is to deploy code from a GitHub repository to the web app.</span></span> <span data-ttu-id="efcca-136">让我们使用一个显示 "HelloWorld!" 的 Azure 示例 Github 存储库中提供的简单 PHP 页面。</span><span class="sxs-lookup"><span data-stu-id="efcca-136">Let's use a simple PHP page available in the Azure Samples Github repository that displays "HelloWorld!"</span></span> <span data-ttu-id="efcca-137">执行时。</span><span class="sxs-lookup"><span data-stu-id="efcca-137">when it executes.</span></span> <span data-ttu-id="efcca-138">请确保使用您创建的 web 应用名称。</span><span class="sxs-lookup"><span data-stu-id="efcca-138">Make sure to use the web app name you created.</span></span>

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="efcca-139">部署后, 通过浏览器或卷再次进入您的网站。</span><span class="sxs-lookup"><span data-stu-id="efcca-139">Once it's deployed, hit your site again with a browser or CURL.</span></span>

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
    <span data-ttu-id="efcca-140">页面显示 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="efcca-140">The page displays "Hello World!"</span></span>

    ```output
    Hello World!
    ```

<span data-ttu-id="efcca-141">本练习演示了交互式 Azure CLI 会话的典型模式。</span><span class="sxs-lookup"><span data-stu-id="efcca-141">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="efcca-142">您首先使用标准命令创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="efcca-142">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="efcca-143">然后, 使用一组命令将资源 (在此示例中为 web 应用) 部署到此资源组中。</span><span class="sxs-lookup"><span data-stu-id="efcca-143">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="efcca-144">这组命令可以轻松地组合到命令行管理程序脚本中, 并在每次需要创建相同的资源时执行。</span><span class="sxs-lookup"><span data-stu-id="efcca-144">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>