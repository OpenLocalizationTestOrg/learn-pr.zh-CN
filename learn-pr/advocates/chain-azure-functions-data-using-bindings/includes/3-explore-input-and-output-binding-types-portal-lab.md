<span data-ttu-id="dd325-101">以下是我们将在本练习中构建的内容的高级别说明。</span><span class="sxs-lookup"><span data-stu-id="dd325-101">The following is a high-level illustration of what we're going to build in this exercise.</span></span>

![显示 http 请求和响应以及各自的请求和反应绑定参数的默认 http 触发器的说明](../media/3-default-http-trigger-visual-small.PNG)

<span data-ttu-id="dd325-103">我们将创建一个函数, 该函数将在收到 HTTP 请求时启动, 并通过发送回邮件来响应每个请求。</span><span class="sxs-lookup"><span data-stu-id="dd325-103">We'll create a function that will start when it receives an HTTP request and will respond to each request by sending back a message.</span></span> <span data-ttu-id="dd325-104">参数`req` , 分别`res`是触发器绑定和输出绑定。</span><span class="sxs-lookup"><span data-stu-id="dd325-104">The parameters `req` and `res` are the trigger binding and output binding, respectively.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-function-app"></a><span data-ttu-id="dd325-105">创建函数应用程序</span><span class="sxs-lookup"><span data-stu-id="dd325-105">Create a function app</span></span>

<span data-ttu-id="dd325-106">我们来创建一个函数应用程序, 我们将在整个模块中使用它。</span><span class="sxs-lookup"><span data-stu-id="dd325-106">Let's create a function app that we'll use throughout this entire module.</span></span> <span data-ttu-id="dd325-107">使用函数应用程序, 您可以将函数分组为逻辑单元, 以便更轻松地管理、部署和共享资源。</span><span class="sxs-lookup"><span data-stu-id="dd325-107">A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources.</span></span>

1. <span data-ttu-id="dd325-108">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="dd325-108">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="dd325-109">选择 "**创建资源**" 按钮 (位于 Azure 门户的左上角), 然后选择 "**计算** > **函数应用**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-109">Select the **Create a resource** button found on the upper left-hand corner of the Azure portal, then select **Compute** > **Function App**.</span></span>

1. <span data-ttu-id="dd325-110">按如下所示设置 function app 属性:</span><span class="sxs-lookup"><span data-stu-id="dd325-110">Set the function app properties as follows:</span></span>

    | <span data-ttu-id="dd325-111">属性</span><span class="sxs-lookup"><span data-stu-id="dd325-111">Property</span></span>     | <span data-ttu-id="dd325-112">建议值</span><span class="sxs-lookup"><span data-stu-id="dd325-112">Suggested value</span></span>  | <span data-ttu-id="dd325-113">说明</span><span class="sxs-lookup"><span data-stu-id="dd325-113">Description</span></span>  |
    |--------------|------------------|--------------|
    | <span data-ttu-id="dd325-114">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="dd325-114">**App name**</span></span> | <span data-ttu-id="dd325-115">全局唯一名称</span><span class="sxs-lookup"><span data-stu-id="dd325-115">Globally unique name</span></span> | <span data-ttu-id="dd325-116">标识新的函数应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="dd325-116">Name that identifies your new function app.</span></span> <span data-ttu-id="dd325-117">有效的字符`a-z`为`0-9`、和`-`。</span><span class="sxs-lookup"><span data-stu-id="dd325-117">Valid characters are `a-z`, `0-9`, and `-`.</span></span>  |
    | <span data-ttu-id="dd325-118">**订购**</span><span class="sxs-lookup"><span data-stu-id="dd325-118">**Subscription**</span></span> | <span data-ttu-id="dd325-119">你的订阅</span><span class="sxs-lookup"><span data-stu-id="dd325-119">Your subscription</span></span> | <span data-ttu-id="dd325-120">在其下创建此新的函数应用程序的订阅。</span><span class="sxs-lookup"><span data-stu-id="dd325-120">The subscription under which this new function app is created.</span></span> |
    | <span data-ttu-id="dd325-121">**资源组**</span><span class="sxs-lookup"><span data-stu-id="dd325-121">**Resource Group**</span></span>|  <span data-ttu-id="dd325-122">选择 "**使用现有**" 并选择 " _<rgn>[沙盒资源组名称]</rgn>_ "</span><span class="sxs-lookup"><span data-stu-id="dd325-122">Select **Use existing** and choose _<rgn>[sandbox resource group name]</rgn>_</span></span> | <span data-ttu-id="dd325-123">要在其中创建函数应用程序的资源组的名称。</span><span class="sxs-lookup"><span data-stu-id="dd325-123">Name of the resource group in which to create your function app.</span></span> |
    | <span data-ttu-id="dd325-124">**OS**</span><span class="sxs-lookup"><span data-stu-id="dd325-124">**OS**</span></span> | <span data-ttu-id="dd325-125">Windows</span><span class="sxs-lookup"><span data-stu-id="dd325-125">Windows</span></span> | <span data-ttu-id="dd325-126">承载函数应用程序的操作系统。</span><span class="sxs-lookup"><span data-stu-id="dd325-126">The operating system that hosts the function app.</span></span>  |
    | <span data-ttu-id="dd325-127">**托管计划**</span><span class="sxs-lookup"><span data-stu-id="dd325-127">**Hosting Plan**</span></span> |   <span data-ttu-id="dd325-128">消耗量计划</span><span class="sxs-lookup"><span data-stu-id="dd325-128">Consumption plan</span></span> | <span data-ttu-id="dd325-129">定义如何将资源分配给函数应用程序的托管计划。</span><span class="sxs-lookup"><span data-stu-id="dd325-129">Hosting plan that defines how resources are allocated to your function app.</span></span> <span data-ttu-id="dd325-130">在默认**消耗计划**中, 资源是根据所需的函数动态添加的。</span><span class="sxs-lookup"><span data-stu-id="dd325-130">In the default **Consumption Plan**, resources are added dynamically as required by your functions.</span></span> <span data-ttu-id="dd325-131">在此无服务器托管模型中, 只需支付函数运行时间。</span><span class="sxs-lookup"><span data-stu-id="dd325-131">In this serverless hosting model, you only pay for the time your functions run.</span></span>   |
    | <span data-ttu-id="dd325-132">**Location**</span><span class="sxs-lookup"><span data-stu-id="dd325-132">**Location**</span></span> | <span data-ttu-id="dd325-133">从列表中选择</span><span class="sxs-lookup"><span data-stu-id="dd325-133">Select from the list</span></span> | <span data-ttu-id="dd325-134">选择最接近的一个, 也可以是下面列出的允许的*沙盒区域*之一。</span><span class="sxs-lookup"><span data-stu-id="dd325-134">Choose the nearest one to you that is also one of the allowed *Sandbox regions* listed below.</span></span> |
    | <span data-ttu-id="dd325-135">**运行时堆栈**</span><span class="sxs-lookup"><span data-stu-id="dd325-135">**Runtime Stack**</span></span> | <span data-ttu-id="dd325-136">JavaScript</span><span class="sxs-lookup"><span data-stu-id="dd325-136">JavaScript</span></span> | <span data-ttu-id="dd325-137">此模块中的示例代码是用 JavaScript 编写的。</span><span class="sxs-lookup"><span data-stu-id="dd325-137">The sample code in this module is written in JavaScript.</span></span>  |
    | <span data-ttu-id="dd325-138">**Storage**</span><span class="sxs-lookup"><span data-stu-id="dd325-138">**Storage**</span></span> |  <span data-ttu-id="dd325-139">全局唯一名称</span><span class="sxs-lookup"><span data-stu-id="dd325-139">Globally unique name</span></span> |  <span data-ttu-id="dd325-140">您的函数应用程序使用的新存储帐户的名称。</span><span class="sxs-lookup"><span data-stu-id="dd325-140">Name of the new storage account used by your function app.</span></span> <span data-ttu-id="dd325-141">存储帐户名称的长度必须介于3到24个字符之间, 并且可以仅包含数字和小写字母。</span><span class="sxs-lookup"><span data-stu-id="dd325-141">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="dd325-142">此对话框使用唯一名称填充字段, 该名称派生自您赋予应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="dd325-142">This dialog populates the field with a unique name that is derived from the name you gave the app.</span></span> <span data-ttu-id="dd325-143">但是, 可以随意使用其他名称, 甚至可以使用现有帐户。</span><span class="sxs-lookup"><span data-stu-id="dd325-143">However, feel free to use a different name or even an existing account.</span></span> |

    ### <a name="sandbox-regions"></a><span data-ttu-id="dd325-144">沙盒区域</span><span class="sxs-lookup"><span data-stu-id="dd325-144">Sandbox regions</span></span>
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="dd325-145">选择 "**创建**" 以设置和部署函数应用。</span><span class="sxs-lookup"><span data-stu-id="dd325-145">Select **Create** to provision and deploy the function app.</span></span>

1. <span data-ttu-id="dd325-146">选择门户右上角的通知图标, 并监视**正在进行**的、类似于以下消息的部署消息。</span><span class="sxs-lookup"><span data-stu-id="dd325-146">Select the Notification icon in the upper-right corner of the portal and watch for a **Deployment in progress** message similar to the following message.</span></span>

    ![正在进行函数应用部署的通知](../media/3-func-app-deploy-progress-small.PNG)

1. <span data-ttu-id="dd325-148">部署可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="dd325-148">Deployment can take some time.</span></span> <span data-ttu-id="dd325-149">因此, 请停留在通知中心并监视 "**部署已成功**" 消息 (类似于以下消息)。</span><span class="sxs-lookup"><span data-stu-id="dd325-149">So, stay in the notification hub and  watch for a **Deployment succeeded** message similar to the following message.</span></span>

    ![函数应用部署已完成的通知](../media/3-func-app-deploy-success-small.PNG)

 1. <span data-ttu-id="dd325-151">部署函数应用后, 请转到门户中的**所有资源**。</span><span class="sxs-lookup"><span data-stu-id="dd325-151">Once the function app is deployed, go to **All resources** in the portal.</span></span> <span data-ttu-id="dd325-152">将使用 type **app Service**列出函数应用程序, 并为其赋予名称。</span><span class="sxs-lookup"><span data-stu-id="dd325-152">The function app will be listed with type **App Service** and has the name you gave it.</span></span> <span data-ttu-id="dd325-153">从列表中选择函数应用程序以将其打开。</span><span class="sxs-lookup"><span data-stu-id="dd325-153">Select the function app from the list to open it.</span></span>

    >[!TIP]
    ><span data-ttu-id="dd325-154">如果在门户中查找函数应用程序时遇到问题, 请了解如何[将 function 应用程序添加到门户中的收藏夹中](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite)。</span><span class="sxs-lookup"><span data-stu-id="dd325-154">If you are having trouble finding your function apps in the portal, find out how to [add function apps to your favorites in the portal](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).</span></span>

## <a name="create-a-function"></a><span data-ttu-id="dd325-155">创建函数</span><span class="sxs-lookup"><span data-stu-id="dd325-155">Create a function</span></span>

<span data-ttu-id="dd325-156">现在我们有了函数应用程序, 现在是时候创建函数了。</span><span class="sxs-lookup"><span data-stu-id="dd325-156">Now that we have a function app, it's time to create a function.</span></span> <span data-ttu-id="dd325-157">通过触发器激活函数。</span><span class="sxs-lookup"><span data-stu-id="dd325-157">A function is activated through a trigger.</span></span> <span data-ttu-id="dd325-158">在本模块中, 我们将使用 HTTP 触发器。</span><span class="sxs-lookup"><span data-stu-id="dd325-158">In this module, we'll use an HTTP trigger.</span></span>

1. <span data-ttu-id="dd325-159">选择 "函数"**+** 旁边的 "添加\*\*\*\*" () 按钮。</span><span class="sxs-lookup"><span data-stu-id="dd325-159">Select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="dd325-160">此操作将启动函数创建过程。</span><span class="sxs-lookup"><span data-stu-id="dd325-160">This action starts the function creation process.</span></span>

1. <span data-ttu-id="dd325-161">在 "**适用于 JavaScript 的 Azure 函数-入门**" 页上, 选择 "**在门户中**", 然后选择 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-161">On the **Azure Functions for JavaScript - getting started** page, select **In-portal** and then select **continue**.</span></span>

1. <span data-ttu-id="dd325-162">在 "**创建函数**" 步骤中, 选择 "**更多模板 ...** ", 然后选择 "完成", 然后单击 "**查看模板**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-162">In the **Create a function** step, select **More templates...** and then select **Finish and view templates**.</span></span>

1. <span data-ttu-id="dd325-163">在可用于此函数应用程序的所有模板的列表中, 选择 " **HTTP 触发器**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-163">In the list of all templates available to this function app, select **HTTP Trigger** .</span></span>

1. <span data-ttu-id="dd325-164">在 "**新建函数**" 屏幕上, 更改名称 (如果需要), 将 "**授权级别**" 保留为 "_函数_", 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-164">On the **New Function** screen, change the name if you want, leave the **Authorization level** as _Function_, and click **Create**.</span></span>

1. <span data-ttu-id="dd325-165">在您的新函数中, 单击右上角的 " **</> Get 函数 URL** " 链接, 选择 " **default (功能键)**", 然后选择 "**复制**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-165">In your new function, click the **</> Get function URL** link at the top right, select **default (Function key)**, and then select **Copy**.</span></span>

1. <span data-ttu-id="dd325-166">将复制的函数 URL 粘贴到浏览器的新选项卡的地址栏中。</span><span class="sxs-lookup"><span data-stu-id="dd325-166">Paste the function URL you copied into the address bar of a new tab in your browser.</span></span>

1. <span data-ttu-id="dd325-167">将查询字符串值`&name=Azure`添加到此 URL 的末尾, 然后按键盘上的 enter 键以执行请求。</span><span class="sxs-lookup"><span data-stu-id="dd325-167">Add the query string value `&name=Azure` to the end of this URL, and then press Enter on your keyboard to execute the request.</span></span> <span data-ttu-id="dd325-168">您应该会看到类似于浏览器中显示的函数返回的以下响应。</span><span class="sxs-lookup"><span data-stu-id="dd325-168">You should see a response similar to the following response returned by the function displayed in your browser.</span></span>

    ```output
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Hello Azure</string>
    ```

<span data-ttu-id="dd325-169">正如您在此练习中可以看到的, 在创建函数时, 您必须选择触发器类型。</span><span class="sxs-lookup"><span data-stu-id="dd325-169">As you can see from this exercise so far, you have to select a trigger type when you create a function.</span></span> <span data-ttu-id="dd325-170">每个函数都有一个且只有一个触发器。</span><span class="sxs-lookup"><span data-stu-id="dd325-170">Every function has one and only one trigger.</span></span> <span data-ttu-id="dd325-171">在此示例中, 我们使用的是 http 触发器, 这意味着我们的函数将在收到 HTTP 请求时启动。</span><span class="sxs-lookup"><span data-stu-id="dd325-171">In this example, we're using an HTTP trigger, which means that our function starts when it receives an HTTP request.</span></span> <span data-ttu-id="dd325-172">默认实现 (如 JavaScript 中的以下屏幕截图所示) 使用在请求的查询字符串或正文中收到的参数*名称*的值做出响应。</span><span class="sxs-lookup"><span data-stu-id="dd325-172">The default implementation, shown in the following screenshot in JavaScript, responds with the value of the parameter *name* it received in the query string or body of the request.</span></span> <span data-ttu-id="dd325-173">如果未提供任何字符串, 则函数将使用一条消息进行响应, 该消息会询问负责提供名称值的人的电话。</span><span class="sxs-lookup"><span data-stu-id="dd325-173">If no string was provided, the function responds with a message that asks whomever is calling to supply a name value.</span></span>

![HTTP 触发 Azure 函数的默认 JavaScript 实现](../media/3-default-http-trigger-implementation-small.PNG)

<span data-ttu-id="dd325-175">所有这些代码都位于此函数的文件夹中的**node.js**文件中。</span><span class="sxs-lookup"><span data-stu-id="dd325-175">All of this code is in the **index.js** file in this function's folder.</span></span> <span data-ttu-id="dd325-176">让我们简单了解一下函数的其他文件 (即**函数 json**配置文件)。</span><span class="sxs-lookup"><span data-stu-id="dd325-176">Let's look briefly at the function's other file, the **function.json** config file.</span></span> <span data-ttu-id="dd325-177">以下 JSON 列表中显示了此配置数据。</span><span class="sxs-lookup"><span data-stu-id="dd325-177">This configuration data is shown in the following JSON listing.</span></span>

```json
{
    "bindings": [
    {
        "authLevel": "function",
        "type": "httpTrigger",
        "direction": "in",
        "name": "req",
        "methods": [
        "get",
        "post"
        ]
    },
    {
        "type": "http",
        "direction": "out",
        "name": "res"
    }
    ],
    "disabled": false
}
```

<span data-ttu-id="dd325-178">正如您所看到的, 此函数具有一个名\*\*\*\* 为 "必需`httpTrigger` " 类型的触发器绑定和名为`HTTP`"类型" **res**的输出绑定。</span><span class="sxs-lookup"><span data-stu-id="dd325-178">As you can see, this function has a trigger binding named **req** of type `httpTrigger` and an output binding named **res**  of type `HTTP`.</span></span> <span data-ttu-id="dd325-179">在我们的函数的上述代码中, 我们看到我们如何通过我们的请求参数访问传入 HTTP 请求\*\*\*\* 的有效负载。</span><span class="sxs-lookup"><span data-stu-id="dd325-179">In the preceding code for our function, we saw how we accessed the payload of the incoming HTTP request through our **req** parameter.</span></span> <span data-ttu-id="dd325-180">同样, 我们仅通过设置**res**参数发送了一个 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="dd325-180">Similarly, we sent an HTTP response simply by setting our **res** parameter.</span></span> <span data-ttu-id="dd325-181">绑定实际上确实会为我们做一些繁重的提升。</span><span class="sxs-lookup"><span data-stu-id="dd325-181">Bindings really do take care of some of the heavy lifting for us.</span></span>

>[!TIP]
><span data-ttu-id="dd325-182">您可以通过展开 "**查看文件**" 菜单来查看**index .js**和**函数 json**文件, 当您选择了函数时, 将在屏幕右侧看到该菜单。</span><span class="sxs-lookup"><span data-stu-id="dd325-182">You can see the **index.js** and **function.json** files by expanding the **View Files** menu that you'll see on the right hand side of the screen when you have your function selected.</span></span> <span data-ttu-id="dd325-183">您可能需要向右滚动才能看到此菜单。</span><span class="sxs-lookup"><span data-stu-id="dd325-183">You might have to scroll to the right to see this menu.</span></span>

### <a name="explore-binding-types"></a><span data-ttu-id="dd325-184">浏览绑定类型</span><span class="sxs-lookup"><span data-stu-id="dd325-184">Explore binding types</span></span>

1. <span data-ttu-id="dd325-185">请注意, 在函数条目下有一组菜单项, 如以下屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="dd325-185">Notice under the function entry there is a set of menu items as shown in the following screenshot.</span></span>

    ![显示函数应用程序边栏中的函数下的菜单项的屏幕截图。](../media/3-func-menu-small.PNG)

1. <span data-ttu-id="dd325-187">选择 "**集成**" 菜单项, 打开函数的 "集成" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="dd325-187">Select the **Integrate** menu item to open the integration tab for our function.</span></span> <span data-ttu-id="dd325-188">如果你已与此设备一起关注, "集成" 选项卡应类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="dd325-188">If you've been following along with this unit, the integrate tab should look very similar to the following screenshot.</span></span>

    ![显示集成 UI 或选项卡的屏幕截图。](../media/3-func-integrate-tab-small.PNG)

    > [!NOTE]
    > <span data-ttu-id="dd325-190">我们已经定义了触发器和输出绑定, 如屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="dd325-190">We have already defined a trigger and an output binding, as shown in the screenshot.</span></span> <span data-ttu-id="dd325-191">您可以看到, 我们无法添加多个__ 触发器。</span><span class="sxs-lookup"><span data-stu-id="dd325-191">You can see that we can't add more than _one_ trigger.</span></span> <span data-ttu-id="dd325-192">事实上, 若要更改函数的触发器, 我们必须先删除触发器并创建一个新触发器。</span><span class="sxs-lookup"><span data-stu-id="dd325-192">In fact, to change the trigger for our function we would have to first delete the trigger and create a new one.</span></span> <span data-ttu-id="dd325-193">但是, 此 UI 的**输入**和**输出**部分显示一个加号 (+) 以添加更多绑定, 因此我们可以接受多个输入值并发出多个输出值。</span><span class="sxs-lookup"><span data-stu-id="dd325-193">However, the **Inputs** and **Outputs** sections of this UI display a plus sign (+) to add more bindings so we can accept more than one input value and emit more than one output value.</span></span>

1. <span data-ttu-id="dd325-194">在 "**输入**" 列下选择 " **+ 新建输入**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-194">Select **+ New Input** under the **Inputs** column.</span></span> <span data-ttu-id="dd325-195">将显示所有可能的输入绑定类型的列表, 如下面的屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="dd325-195">A list of all possible input binding types is displayed as shown in the following screenshot.</span></span>

    ![显示可能的输入绑定列表的屏幕截图。](../media/3-func-input-bindings-selector-small.PNG)

   <span data-ttu-id="dd325-197">请花点时间考虑一下每个输入绑定以及如何在解决方案中使用它们。</span><span class="sxs-lookup"><span data-stu-id="dd325-197">Take a moment to consider each of these input bindings and how you might use them in a solution.</span></span> <span data-ttu-id="dd325-198">有很多可供选择。</span><span class="sxs-lookup"><span data-stu-id="dd325-198">There are a lot to choose from.</span></span> <span data-ttu-id="dd325-199">此列表甚至可能在你阅读此模块时已发生更改, 因为我们继续支持更多数据源。</span><span class="sxs-lookup"><span data-stu-id="dd325-199">This list might even have changed by the time you read this module, as we continue to support more data sources.</span></span>

1. <span data-ttu-id="dd325-200">我们将返回稍后在模块中添加输入绑定, 但现在, 请选择 "**取消**" 关闭此列表。</span><span class="sxs-lookup"><span data-stu-id="dd325-200">We'll get back to adding input bindings later in the module but, for now, select **Cancel** to dismiss this list.</span></span>

1. <span data-ttu-id="dd325-201">在 "**输出**" 列下选择 " **+ 新输出**"。</span><span class="sxs-lookup"><span data-stu-id="dd325-201">Select **+ New Output** under the **Outputs** column.</span></span> <span data-ttu-id="dd325-202">将显示所有可能的输出绑定类型的列表, 如下面的屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="dd325-202">A list of all possible output binding types is displayed as shown in the following screenshot.\\</span></span>

    ![显示可能的输出绑定列表的屏幕截图。](../media/3-func-output-bindings-selector-small.PNG)

   <span data-ttu-id="dd325-204">正如您所看到的, 有几种输出绑定类型可供您处置。</span><span class="sxs-lookup"><span data-stu-id="dd325-204">As you can see, there are several output binding types at your disposal.</span></span> <span data-ttu-id="dd325-205">我们将返回稍后在模块中添加输出绑定, 但现在, 请选择 "**取消**" 关闭此列表。</span><span class="sxs-lookup"><span data-stu-id="dd325-205">We'll get back to adding output bindings later in the module but, for now, select **Cancel** to dismiss this list.</span></span>

<span data-ttu-id="dd325-206">到目前为止, 我们已经学习了如何创建函数应用程序并向其添加函数。</span><span class="sxs-lookup"><span data-stu-id="dd325-206">So far, we've learned how to create a function app and add a function to it.</span></span> <span data-ttu-id="dd325-207">我们在操作中看到了一个简单的函数, 即在向其发出 HTTP 请求时运行的函数。</span><span class="sxs-lookup"><span data-stu-id="dd325-207">We've seen a simple function in action, one that runs when an HTTP request is made to it.</span></span> <span data-ttu-id="dd325-208">我们还探索了 Azure 门户 UI 以及可用于我们的函数的输入和输出绑定的类型。</span><span class="sxs-lookup"><span data-stu-id="dd325-208">We've also explored the Azure portal UI and types of input and output binding that are available to our functions.</span></span> <span data-ttu-id="dd325-209">在下一个单元中, 我们将使用输入绑定从数据库中读取文本。</span><span class="sxs-lookup"><span data-stu-id="dd325-209">In the next unit, we'll use an input binding to read text from a database.</span></span>