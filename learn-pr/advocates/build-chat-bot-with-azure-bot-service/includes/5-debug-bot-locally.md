[!INCLUDE [0-vm-note](0-vm-note.md)]

与您编写的任何应用程序代码一样, 在部署到生产环境之前, 需要在本地测试和调试对 bot 代码所做的更改。 为了帮助调试 bot, Microsoft 提供了 bot 框架模拟器。 在此单元中, 你将了解如何使用 Visual Studio Code 和模拟器调试你的 bot。

1. 在 Visual Studio Code 的集成终端中执行以下命令, 以安装[Restify](http://restify.com/), 用于构建和使用 RESTful web 服务的受欢迎的 node.js 包:

    ```bash
    npm install restify
    ```

1. 对以下命令重复此步骤, 以安装[适用于 node.js 的 Microsoft Bot 框架自动程序生成器 SDK](https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-quickstart):

    ```bash
    npm install botbuilder
    npm install botbuilder-azure
    npm install botbuilder-cognitiveservices
    ```

1. 在 Visual Studio Code 的活动栏中选择 "**浏览器**" 按钮。 
1. 选择**app.config**以在代码编辑器中打开它。 此文件包含驱动机器人的代码 (由 Azure bot 服务生成的代码和从 azure 门户下载的代码)。

1. 将**app.config**的内容替换为以下代码, 然后保存文件。

    ```JavaScript
    "use strict";
    var builder = require("botbuilder");
    var botbuilder_azure = require("botbuilder-azure");

    var useEmulator = true;
    var userName = "";
    var yearsCoding = "";
    var selectedLanguage = "";

    var connector = useEmulator ? new builder.ChatConnector() : new botbuilder_azure.BotServiceConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword
    });

    var bot = new builder.UniversalBot(connector);

    bot.dialog('/', [

    function (session) {
        builder.Prompts.text(session, "Hello, and welcome to QnA Factbot! What's your name?");
    },

    function (session, results) {
        userName = results.response;
        builder.Prompts.number(session, "Hi " + userName + ", how many years have you been writing code?");
    },

    function (session, results) {
        yearsCoding = results.response;
        builder.Prompts.choice(session, "What language do you love the most?", ["C#", "Python", "Node.js", "Visual FoxPro"]);
    },

    function (session, results) {
        selectedLanguage = results.response.entity;

        session.send("Okay, " + userName + ", I think I've got it:" +
            " You've been writing code for " + yearsCoding + " years," +
            " and prefer to use " + selectedLanguage + ".");
    }]);

    var restify = require('restify');
    var server = restify.createServer();

    server.listen(3978, function() {
        console.log('test bot endpoint at http://localhost:3978/api/messages');
    });

    server.post('/api/messages', connector.listen());
    ```

1. 通过在左侧的边距中进行选择, 在行`builder.Prompts...` 20、25和 30 (调用) 上设置断点。

1. 在活动栏中选择 "**调试**" 按钮, 然后选择绿色的 "**启动调试**" 按钮以启动调试会话。 确认 "测试机器人终结点http://localhost:3978/api/messages" 出现在调试控制台中。

    ![显示具有调试导航项的调试系统的 Visual Studio 代码的屏幕截图和用于启动突出显示的调试会话的调试播放按钮。](../media/5-vs-launch-debugger.png)

    你的 bot 代码现在正在本地运行。

1. 从 "开始" 菜单启动**Bot 框架模拟器**。

1. 选择 "**输入您的终结点 URL** " 字段。 输入在上一步的调试控制台中显示的 bot 名称和 bot URL。

1. 将 microsoft app ID、microsoft app 密码和区域设置字段保留为空, 然后选择 "**连接**"。

1. 然后, 选择 "**保存并连接**", 并将配置文件保存在您选择的位置。

    >[!NOTE]
    > 以后, 您只需选择 "我的 bot" 下的 bot 名称即可重新连接到 bot。

    ![Bot 框架仿真程序的屏幕截图, 显示新的 bot 配置屏幕, 其中突出显示了 "保存并连接" 按钮。](../media/5-new-bot-configuration.png)

1. 在仿真程序底部的框中键入 "hi", 然后按**enter**。 确认 Visual Studio Code 在**应用 .js**的第20行中断。 然后, 在 Visual Studio Code 的调试工具栏中选择 "**继续**" 按钮, 然后返回到仿真程序以查看 bot 的响应。

1. bot 将向你询问一系列问题。 回答这些问题, 并在每次命中断点时选择 "在 Visual Studio Code 中**继续**"。 完成后, 选择 "调试" 工具栏中的 "**停止**" 按钮以结束调试会话。

在这种情况下, 你有一个功能完全正常的 bot, 并了解如何通过在 Microsoft bot 框架仿真器中本地运行它来调试它。 下一步是将 bot 连接到您发布的知识库, 使其更加智能化。