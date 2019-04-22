[!INCLUDE [0-vm-note](0-vm-note.md)]

在此单元中, 你将机器人连接到您先前构建的 QnA Maker 知识库中, 以便机器人可以进行智能对话。 连接知识库的过程包括从 QnA Maker 门户检索一些信息, 将其复制到 Azure 门户, 更新 bot 代码, 然后将机器人重新部署到 Azure。

1. 返回到 VM 浏览器https://www.qnamaker.ai中的 QnA Maker 门户, 然后选择右上角的 "帐户" 按钮。
1. 从下拉菜单中选择 "**管理终结点密钥**"。
1. 选择 "**显示**" 以显示**主**终结点键, 并**复制**以将其复制到剪贴板。 将其粘贴到文本文件中, 以便在一段时间内轻松地进行检索。

    > [!NOTE]
    > 根据你的浏览器设置, 你可能需要允许第三方 cookie 完成此设备。

1. 在页面顶部的菜单中选择 **"我的知识库**"。
1. 然后, 选择您之前创建的知识库的 "**查看代码**"。

1. 复制第一行中的知识库 ID 和第二行中的主机名。 也将它们粘贴到文本文件中。 然后, 关闭对话框。 **不要**在复制的主机名中包含 "https://" 前缀。

    ![显示示例 HTTP 请求的 QnA 生成器门户的屏幕截图, 其中突出显示了终结点知识库 ID 和主机名称。](../media/6-copy-endpoint-info.png)

1. 返回到 Azure 门户中的 Web 应用程序 Bot。 在左侧菜单中选择 "**应用程序设置**", 然后向下滚动, 直到找到名为 "QnAKnowledgebaseId"、"QnAAuthKey" 和 "QnAEndpointHostName" 的应用程序设置。 将刚刚获取的知识库 ID 和主机名以及之前获取的终结点密钥粘贴到这些字段中。 然后, 选择顶部的 "**保存**"。

    ![在应用程序设置菜单项和相应的设置键突出显示的情况中显示 bot 边栏和应用程序设置详细信息的 Azure 门户屏幕截图。](../media/6-enter-app-settings.png)

1. 返回到**Visual Studio Code**并将**app.config**的内容替换为以下代码。 然后, 保存该文件。

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
    > 在第30行创建`QnAMakerDialog`实例的调用。 这将创建一个对话框, 该对话框将使用 Azure bot 服务生成的 bot 与通过 Microsoft QnA Maker 构建的知识库集成。

1. 在 Visual Studio Code 的活动栏中选择 "**源代码控制**" 按钮。
1. 将鼠标悬停在**app.config**文件上, 然后选择__+__ 该按钮以暂存该文件在下一次提交时所做的更改。
1. 在消息框中键入 "已连接到知识库", 然后选中该复选标记以提交您所做的更改。

    > [!Warning]
    > 如果您看到**package. json**文件的更改, 请确保您在提交时不包含这些更改。 您的提交应仅包含对**node.js**的更改。

1. 然后, 选择省略号 (__...__) 按钮并使用 "**发布分支**" 命令将这些更改推送到远程存储库和 Azure Web 应用。

1. 返回到 Azure 门户中的 web 应用程序 bot, 然后选择左侧的 "**在 web 上聊天**" 中的 "测试" 以打开测试控制台。 键入 "全球最受欢迎的软件编程语言是什么？" 插入聊天窗口底部的框中, 然后按**enter**。 确认机器人是否响应。

!! 你的 bot 已连接到知识库并可对问题做出响应。
