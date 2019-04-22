[!INCLUDE [0-vm-note](0-vm-note.md)]

<span data-ttu-id="d3cb3-101">在此单元中, 你将机器人连接到您先前构建的 QnA Maker 知识库中, 以便机器人可以进行智能对话。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-101">In this unit, you will connect your bot to the QnA Maker knowledge base you built earlier so that the bot can carry on an intelligent conversation.</span></span> <span data-ttu-id="d3cb3-102">连接知识库的过程包括从 QnA Maker 门户检索一些信息, 将其复制到 Azure 门户, 更新 bot 代码, 然后将机器人重新部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-102">Connecting to the knowledge base involves retrieving some information from the QnA Maker portal, copying it into the Azure portal, updating the bot code, and then redeploying the bot to Azure.</span></span>

1. <span data-ttu-id="d3cb3-103">返回到 VM 浏览器https://www.qnamaker.ai中的 QnA Maker 门户, 然后选择右上角的 "帐户" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-103">Return to the QnA Maker portal at https://www.qnamaker.ai in the VM browser and select the account button in the upper-right corner.</span></span>
1. <span data-ttu-id="d3cb3-104">从下拉菜单中选择 "**管理终结点密钥**"。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-104">Select **Manage endpoint keys** from the menu that drops down.</span></span>
1. <span data-ttu-id="d3cb3-105">选择 "**显示**" 以显示**主**终结点键, 并**复制**以将其复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-105">Select **Show** to show the **Primary** endpoint key and **Copy** to copy it to the clipboard.</span></span> <span data-ttu-id="d3cb3-106">将其粘贴到文本文件中, 以便在一段时间内轻松地进行检索。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-106">Paste it into a text file, so you can easily retrieve it in a moment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3cb3-107">根据你的浏览器设置, 你可能需要允许第三方 cookie 完成此设备。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-107">Depending on your browser settings, you may need to allow third-party cookies to complete this unit.</span></span>

1. <span data-ttu-id="d3cb3-108">在页面顶部的菜单中选择 **"我的知识库**"。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-108">Select **My knowledge bases** in the menu at the top of the page.</span></span>
1. <span data-ttu-id="d3cb3-109">然后, 选择您之前创建的知识库的 "**查看代码**"。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-109">Then, select **View Code** for the knowledge base that you created earlier.</span></span>

1. <span data-ttu-id="d3cb3-110">复制第一行中的知识库 ID 和第二行中的主机名。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-110">Copy the knowledge base ID from the first line and the host name from the second line.</span></span> <span data-ttu-id="d3cb3-111">也将它们粘贴到文本文件中。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-111">Paste them into a text file, as well.</span></span> <span data-ttu-id="d3cb3-112">然后, 关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-112">Then, close the dialog.</span></span> <span data-ttu-id="d3cb3-113">**不要**在复制的主机名中包含 "https://" 前缀。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-113">**Do not** include the "https://" prefix in the host name that you copy.</span></span>

    ![显示示例 HTTP 请求的 QnA 生成器门户的屏幕截图, 其中突出显示了终结点知识库 ID 和主机名称。](../media/6-copy-endpoint-info.png)

1. <span data-ttu-id="d3cb3-115">返回到 Azure 门户中的 Web 应用程序 Bot。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-115">Return to the Web App Bot in the Azure portal.</span></span> <span data-ttu-id="d3cb3-116">在左侧菜单中选择 "**应用程序设置**", 然后向下滚动, 直到找到名为 "QnAKnowledgebaseId"、"QnAAuthKey" 和 "QnAEndpointHostName" 的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-116">Select **Application settings** in the menu on the left, and scroll down until you find application settings named "QnAKnowledgebaseId," "QnAAuthKey," and "QnAEndpointHostName."</span></span> <span data-ttu-id="d3cb3-117">将刚刚获取的知识库 ID 和主机名以及之前获取的终结点密钥粘贴到这些字段中。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-117">Paste the knowledge base ID and host name you just obtained and the endpoint key obtained previously into these fields.</span></span> <span data-ttu-id="d3cb3-118">然后, 选择顶部的 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-118">Then, select **Save** at the top.</span></span>

    ![在应用程序设置菜单项和相应的设置键突出显示的情况中显示 bot 边栏和应用程序设置详细信息的 Azure 门户屏幕截图。](../media/6-enter-app-settings.png)

1. <span data-ttu-id="d3cb3-120">返回到**Visual Studio Code**并将**app.config**的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-120">Return to **Visual Studio Code** and replace the contents of **app.js** with the code below.</span></span> <span data-ttu-id="d3cb3-121">然后, 保存该文件。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-121">Then, save the file.</span></span>

    ```JavaScript
    var restify = require('restify');
    var builder = require('botbuilder');
    var botbuilder_azure = require("botbuilder-azure");
    var builder_cognitiveservices = require("botbuilder-cognitiveservices");

    // Setup Restify Server
    var server = restify.createServer();
    server.listen(process.env.port || process.env.PORT || 3978, function () {
        console.log('%s listening to %s', server.name, server.url);
    });

    // Create chat connector for communicating with the Bot Framework Service
    var connector = new builder.ChatConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword,
        openIdMetadata: process.env.BotOpenIdMetadata
    });

    // Listen for messages from users
    server.post('/api/messages', connector.listen());

    var tableName = 'botdata';
    var azureTableClient = new botbuilder_azure.AzureTableClient(tableName, process.env['AzureWebJobsStorage']);
    var tableStorage = new botbuilder_azure.AzureBotStorage({ gzipData: false }, azureTableClient);

    // Create your bot with a function to receive messages from the user
    var bot = new builder.UniversalBot(connector);
    bot.set('storage', tableStorage);

    // Recognizer and and Dialog for preview QnAMaker service
    var previewRecognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId,
        authKey: process.env.QnAAuthKey || process.env.QnASubscriptionKey
    });

    var basicQnAMakerPreviewDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [previewRecognizer],
        defaultMessage: 'No match! Try changing the query terms!',
        qnaThreshold: 0.3
    }
    );

    bot.dialog('basicQnAMakerPreviewDialog', basicQnAMakerPreviewDialog);

    // Recognizer and and Dialog for GA QnAMaker service
    var recognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId,
        authKey: process.env.QnAAuthKey || process.env.QnASubscriptionKey, // Backward compatibility with QnAMaker (Preview)
        endpointHostName: process.env.QnAEndpointHostName
    });

    var basicQnAMakerDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [recognizer],
        defaultMessage: "I'm not quite sure what you're asking. Please ask your question again.",
        qnaThreshold: 0.3
    });

    bot.dialog('basicQnAMakerDialog', basicQnAMakerDialog);

    bot.dialog('/', //basicQnAMakerDialog);
        [
            function (session) {
                var qnaKnowledgebaseId = process.env.QnAKnowledgebaseId;
                var qnaAuthKey = process.env.QnAAuthKey || process.env.QnASubscriptionKey;
                var endpointHostName = process.env.QnAEndpointHostName;

                // QnA Subscription Key and KnowledgeBase Id null verification
                if ((qnaAuthKey == null || qnaAuthKey == '') || (qnaKnowledgebaseId == null || qnaKnowledgebaseId == ''))
                    session.send('Please set QnAKnowledgebaseId, QnAAuthKey and QnAEndpointHostName (if applicable) in App Settings. Learn how to get them at https://aka.ms/qnaabssetup.');
                else {
                    if (endpointHostName == null || endpointHostName == '')
                        // Replace with Preview QnAMakerDialog service
                        session.replaceDialog('basicQnAMakerPreviewDialog');
                    else
                        // Replace with GA QnAMakerDialog service
                        session.replaceDialog('basicQnAMakerDialog');
                }
            }
        ]);
    ```

    > [!NOTE]
    > <span data-ttu-id="d3cb3-122">在第30行创建`QnAMakerDialog`实例的调用。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-122">The call to create a `QnAMakerDialog` instance on line 30.</span></span> <span data-ttu-id="d3cb3-123">这将创建一个对话框, 该对话框将使用 Azure bot 服务生成的 bot 与通过 Microsoft QnA Maker 构建的知识库集成。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-123">This creates a dialog that integrates a bot built with the Azure Bot Service with a knowledge base built via Microsoft QnA Maker.</span></span>

1. <span data-ttu-id="d3cb3-124">在 Visual Studio Code 的活动栏中选择 "**源代码控制**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-124">Select the **Source Control** button in the activity bar in Visual Studio Code.</span></span>
1. <span data-ttu-id="d3cb3-125">将鼠标悬停在**app.config**文件上, 然后选择__+__ 该按钮以暂存该文件在下一次提交时所做的更改。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-125">Hover over the **app.js** file and select the __+__ button to stage that file's changes for the next commit.</span></span>
1. <span data-ttu-id="d3cb3-126">在消息框中键入 "已连接到知识库", 然后选中该复选标记以提交您所做的更改。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-126">Type "Connected to knowledge base" into the message box, and select the check mark to commit your changes.</span></span>

    > [!Warning]
    > <span data-ttu-id="d3cb3-127">如果您看到**package. json**文件的更改, 请确保您在提交时不包含这些更改。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-127">If you see changes to a **package.json** file ensure you do NOT include them in your commit.</span></span> <span data-ttu-id="d3cb3-128">您的提交应仅包含对**node.js**的更改。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-128">Your commit should only include your changes to **app.js**.</span></span>

1. <span data-ttu-id="d3cb3-129">然后, 选择省略号 (__...__) 按钮并使用 "**发布分支**" 命令将这些更改推送到远程存储库和 Azure Web 应用。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-129">Then, select the ellipsis (__...__) button and use the **Publish Branch** command to push these changes to the remote repository and the Azure Web App.</span></span>

1. <span data-ttu-id="d3cb3-130">返回到 Azure 门户中的 web 应用程序 bot, 然后选择左侧的 "**在 web 上聊天**" 中的 "测试" 以打开测试控制台。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-130">Return to the web app bot in the Azure portal, and select **Test in Web Chat** on the left to open the test console.</span></span> <span data-ttu-id="d3cb3-131">键入 "全球最受欢迎的软件编程语言是什么？"</span><span class="sxs-lookup"><span data-stu-id="d3cb3-131">Type "What's the most popular software programming language in the world?"</span></span> <span data-ttu-id="d3cb3-132">插入聊天窗口底部的框中, 然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-132">into the box at the bottom of the chat window and press **Enter**.</span></span> <span data-ttu-id="d3cb3-133">确认机器人是否响应。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-133">Confirm that the bot responds.</span></span>

<span data-ttu-id="d3cb3-134">!!</span><span class="sxs-lookup"><span data-stu-id="d3cb3-134">Congratulations!</span></span> <span data-ttu-id="d3cb3-135">你的 bot 已连接到知识库并可对问题做出响应。</span><span class="sxs-lookup"><span data-stu-id="d3cb3-135">Your bot is connected to the knowledge base and can respond to questions.</span></span>
