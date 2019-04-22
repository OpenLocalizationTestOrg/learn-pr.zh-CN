<span data-ttu-id="48687-101">你已创建所有必需的 Azure 函数, 并已将其部署!</span><span class="sxs-lookup"><span data-stu-id="48687-101">You've created all the required Azure Functions, and deployed them!</span></span> <span data-ttu-id="48687-102">让我们将 Azure 函数与可宽延时间连接, 并创建一个可宽延的斜杠命令以调用 Azure 函数, 并在可宽延时间窗口中显示生成的 mojified 图像。</span><span class="sxs-lookup"><span data-stu-id="48687-102">Let's connect the Azure Functions with Slack and create a Slack slash command to calls the Azure Function and displays the resulting mojified image in the Slack window.</span></span> 

## <a name="create-a-slack-app"></a><span data-ttu-id="48687-103">创建可宽延时间应用</span><span class="sxs-lookup"><span data-stu-id="48687-103">Create a Slack app</span></span>

<span data-ttu-id="48687-104">斜杠命令作为可宽延时间应用 (也称为 "可宽延时间" bot) 的一部分存在。</span><span class="sxs-lookup"><span data-stu-id="48687-104">A slash command exists as part of a Slack app, also known as a Slack bot.</span></span> 

1. <span data-ttu-id="48687-105">[创建可宽延时间应用](https://api.slack.com/apps/new?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="48687-105">[Create a Slack app](https://api.slack.com/apps/new?azure-portal=true).</span></span>
2. <span data-ttu-id="48687-106">选择一个**应用程序名称**, 并将其与您在此模块开始时创建的**工作区**相关联, 然后选择 "**创建应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="48687-106">Choose an **App Name** and associate it with the **Workspace** you created at the start of this module, then select **Create App**.</span></span>

    ![创建可宽延时间应用。](../media/8.create-slack-app.png)

3. <span data-ttu-id="48687-108">转到 "可宽延时间" 应用, 并创建一个斜杠命令。</span><span class="sxs-lookup"><span data-stu-id="48687-108">Go to your Slack app and create a slash command.</span></span> <span data-ttu-id="48687-109">在`slash Commands`菜单项上选择。</span><span class="sxs-lookup"><span data-stu-id="48687-109">Select on the `slash Commands` menu item.</span></span>

    ![创建可宽延时间应用程序屏幕。](../media/8.slash-commands.png)

4. <span data-ttu-id="48687-112">选择 "**新建命令**"。</span><span class="sxs-lookup"><span data-stu-id="48687-112">Select **Create New Command**.</span></span>

    - <span data-ttu-id="48687-113">在 "**命令**" 字段中为您的斜杠命令提供所需的任何名称。</span><span class="sxs-lookup"><span data-stu-id="48687-113">Provide whatever name you want for your slash command in the **command** field.</span></span>
    - <span data-ttu-id="48687-114">在 "**请求 URL** " 字段中输入 Azure function app 公共 URL。</span><span class="sxs-lookup"><span data-stu-id="48687-114">Enter the Azure function app public URL into the **Request URL** field.</span></span> <span data-ttu-id="48687-115">对于在`mojifier-slack-function-app`上一个单元中使用的, 我们的函数应用程序公共`https://mojifier-slack-function-app.azurewebsites.net`URL 为。</span><span class="sxs-lookup"><span data-stu-id="48687-115">For our `mojifier-slack-function-app` used in the previous unit, our function app public URL would be `https://mojifier-slack-function-app.azurewebsites.net`.</span></span> <span data-ttu-id="48687-116">追加`/api/RespondToSlackCommand`到 URL。</span><span class="sxs-lookup"><span data-stu-id="48687-116">Append `/api/RespondToSlackCommand` to the URL.</span></span>
    - <span data-ttu-id="48687-117">添加**简短说明**和**用法提示**。</span><span class="sxs-lookup"><span data-stu-id="48687-117">Add a **Short Description** and **Usage Hint**.</span></span>

    <span data-ttu-id="48687-118">选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="48687-118">Select **Save**.</span></span>

    ![斜杠命令](../media/8.create-slash-command.png)

5. <span data-ttu-id="48687-120">如果成功, 您应该会看到斜线命令显示在**斜线命令**列表中。</span><span class="sxs-lookup"><span data-stu-id="48687-120">If successful, you should see the slash command appear in your list of **Slash Commands**.</span></span>

    ![斜杠命令显示在所有斜杠命令的列表中。](../media/8.create-slash-commands-success.png)

6. <span data-ttu-id="48687-123">若要实现此操作, 需要在工作区中安装可宽延时间应用。</span><span class="sxs-lookup"><span data-stu-id="48687-123">To get this working, you need to install the Slack app in the workspace.</span></span> <span data-ttu-id="48687-124">在菜单中选择 "**基本信息**"。</span><span class="sxs-lookup"><span data-stu-id="48687-124">Select **Basic Information** in the menu.</span></span>

7. <span data-ttu-id="48687-125">展开 "**将应用安装到工作区**", 然后选择 "**将应用程序安装到工作区**"。</span><span class="sxs-lookup"><span data-stu-id="48687-125">Expand **Install your app to your workspace** and select **Install app to workspace**.</span></span>

   ![将应用程序安装到工作区在可宽延 API 页中的 "可宽延时间的应用程序" 菜单下列出。](../media/8.install-app-to-workspace.png)

8. <span data-ttu-id="48687-127">如果需要, 请**授权**你的应用。</span><span class="sxs-lookup"><span data-stu-id="48687-127">If asked, **Authorize** your app.</span></span>

   ![将应用程序身份验证到工作区间隙屏幕将显示 "授权" 或 "取消" 选项。](../media/8.authenticate-slack-app.png)

## <a name="try-it-out"></a><span data-ttu-id="48687-129">试用</span><span class="sxs-lookup"><span data-stu-id="48687-129">Try it out</span></span>

<span data-ttu-id="48687-130">你已经创建了斜杠命令并将其连接到部署的 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="48687-130">You've created and connected your slash command to your deployed Azure Functions.</span></span> <span data-ttu-id="48687-131">现在, 您可以对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="48687-131">Now, you can test it.</span></span>

1. <span data-ttu-id="48687-132">打开 "可宽延时间" 工作区。</span><span class="sxs-lookup"><span data-stu-id="48687-132">Open your Slack workspace.</span></span>
2. <span data-ttu-id="48687-133">打开聊天窗口并键入`/mojify`。</span><span class="sxs-lookup"><span data-stu-id="48687-133">Open a chat window and type `/mojify`.</span></span> <span data-ttu-id="48687-134">如果你已将应用程序命名为其他内容, 请改为输入该命令。</span><span class="sxs-lookup"><span data-stu-id="48687-134">If you named the app something else, enter that command instead.</span></span>
3. <span data-ttu-id="48687-135">如果一切正常, 您应看到`mojify`一个选项。</span><span class="sxs-lookup"><span data-stu-id="48687-135">If everything has worked correctly, you should see `mojify` as an option.</span></span>

   ![在文本上方弹出斜杠命令菜单。](../media/8.slack-check-mojify.png)

4. <span data-ttu-id="48687-138">输入`/mojify`并添加图像 URL。</span><span class="sxs-lookup"><span data-stu-id="48687-138">Enter `/mojify` and add an image URL.</span></span>

   ![可宽延时间命令正在运行并 mojified 提供的图像 URL。](../media/8.slack-type-mojify.png)
