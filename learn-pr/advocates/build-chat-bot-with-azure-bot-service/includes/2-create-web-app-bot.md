> [!NOTE]
> 启动 VM 后, 您需要登录的用户名和密码位于说明旁边的 "**资源**" 选项卡上。

创建 bot 的第一步是为要在 Azure 中托管的 bot 提供一个位置。 azure 应用服务的 Web 应用功能非常适合承载机器人应用程序, azure bot 服务旨在为你进行预配。 在此单元中, 你将使用 azure 门户预配 azure web 应用程序 bot。

1. 通过在 VM 浏览器中打开https://portal.azure.com登录到 Azure 门户。

1. 依次选择 " **+ 创建资源**" 和 " **AI + 机器学习**", 然后选择 " **Web 应用程序机器人**"。

    ![显示 "创建具有 Web 应用程序机器人资源类型的资源" 边栏的 Azure 门户屏幕截图。](../media/2-new-bot-service.png)

1. 在 "**应用程序名称**" 框中输入一个名称, 如 "factbot"。 *此名称在 Azure 中必须是唯一的, 因此请确保旁边出现绿色的复选标记。*

1. 在 "**订阅**和**资源组**" 下, 选择预先存在的资源。

1. 从以下选项之一中选择**位置**:
    - 美国中部
    - 美国东部
    - 美国东部2
    - 美国中北部
    - 美国中南部
    - 美国西部
    - 美国西部2

    > [!NOTE]
    > 如果您在创建 Web 应用程序的 Bot 时看到资源策略错误, 请检查其位置是否设置为上述选项之一。

1. 选择**S1**定价层。

1. 然后, 选择 " **Bot 模板**"。 选择 " **sdk v3** " 作为版本, **node.js**作为 SDK 语言, 并将**问题和答案**作为模板类型。 然后, 选择刀片式服务器底部的 "**选择**"。

    ![Azure 门户的屏幕截图, 其中显示了使用 node.js SDK 语言的 bot 创建进程的 bot 模板边栏和突出显示的问题和答案模板选项。](../media/2-portal-select-template.png)

1. 现在, 依次选择 " **app service plan/Location**" 和 "**新建**", 然后创建名为 "qa-服务-计划" 的应用程序服务计划, 或在上一步中选择的相同区域中的类似内容。 完成后, 选择 "Web 应用程序 Bot" 边栏底部的 "**创建**" 以启动部署。

    ![显示一个新 Web 应用程序的示例配置刀片的 Azure 门户屏幕截图。](../media/2-portal-start-bot-creation.png)

    > [!NOTE]
    > 部署通常需要两分钟或更短时间。

1. 部署完成后, 在门户左侧的功能区中选择 "**资源组**"。
1. 选择 "为此组预先创建的资源组", 打开部署了 Azure web app bot 的资源组。

您现在应该会看到为您的 Azure web 应用程序机器人创建的几个资源。 在幕后, 部署 Azure web 应用程序 bot 时会发生很大的情况。 已经创建并注册了一个 bot, 创建了一个[Azure web 应用程序](https://azure.microsoft.com/services/app-service/web/), 并将该 bot 配置为与[Microsoft QnA Maker](https://www.qnamaker.ai/)配合使用。 下一步是使用 QnA Maker 创建包含智能的兼顾的问题和答案的知识库。
