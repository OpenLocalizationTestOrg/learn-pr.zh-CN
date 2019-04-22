应用和 Azure 函数现在已完成并在本地运行。 在此单元中, 你将把函数发布到 Azure 以在云中运行。

你将从 Visual Studio 发布函数。 这是开始使用概念证明、原型和学习的好方法, 但对于生产质量的应用程序,**不**应使用此方法。 您应使用某种形式的基于 CI 的部署。 您可以在[Azure 函数部署文档](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true)中阅读有关此操作的详细信息。

## <a name="publishing-your-app-to-azure"></a>将应用程序发布到 Azure

azure 函数可从 Visual Studio 内部发布到 azure。

1. 如果本地 Azure 函数运行时仍从上一个单元运行, 请停止运行时。

1. 右键单击 "解决方案资源`ImHere.Functions`管理器" 中的应用程序, 然后选择 "*发布 ...*"。

    ![右键单击 "函数" 应用程序上的 "发布"](../media/8-right-click-publish.png)

1. 从 "**选择发布目标**" 对话框中, 选择 " *azure 函数应用*", 并选择 " **azure 应用服务**", 然后选择 "*新建*"。 单击 "**发布**"。

    ![创建要发布到的新 Azure 应用服务](../media/8-pick-publish-target.png)

1. 登录到你的 Azure 帐户。

1. 为你的应用程序输入一个名称。

1. 选择你的_订阅_、_资源组_、_托管计划_和_存储帐户_。

1. 单击 "**创建**" 以设置 azure 上的所有资源并发布 azure 函数应用。

    ![创建应用服务](../media/8-create-app-service.png)

1. 系统可能会询问您是否要更新 Azure 上的函数版本。 如果显示此对话框, 请选择 **"是"** 以确保您的 function app 使用最新的 Azure 函数运行时版本进行发布。
    !["更新 Azure 函数" 对话框](../media/8-update-functions-on-azure.png)

预配将需要几分钟时间才能完成。 将预配以下资源:

- 一个存储帐户, 用于存储 Azure 函数应用所需的文件
- 用于管理 Azure 函数应用所需的计算资源的应用程序服务计划
- 运行 Azure 函数的应用程序服务

函数现在将发布, 并可在**https://\<\>** 上进行调用。 azurewebsites.net/api/SendLocation。

## <a name="configuring-your-app"></a>配置应用程序

当 Azure 函数在本地运行时, 它使用的是存储在`local.settings.json`文件中的 Twilio 凭据。 顾名思义, 此文件适用于本地设置, 不适用于 Azure 设置。 在 azure 函数可以在 azure 中调用之前, 需要`TwilioAccountSid`配置`TwilioAuthToken`和设置。

1. 从 "发布" 选项卡中, 单击 "**管理应用程序设置**" 选项。

    !["管理应用程序设置" 选项](../media/8-application-settings-option.png)

1. "**应用程序设置**" 对话框将显示带有本地和远程值的应用程序设置-本地来自您`local.settings.json`的文件, 远程值是在 Azure 中托管时, 您的函数将使用的应用程序设置。 将 " **TwilioAccountSid** " 和 " **TwilioAuthToken** " 值的*本地*框中的值复制到*远程*框中。

    ![在应用程序设置中设置 Twilio 凭据](../media/8-set-creds-in-app-settings.png)

1. 单击"确定"。 这会将值发布到 Azure 函数应用。

## <a name="pointing-the-mobile-app-to-azure"></a>将移动应用程序指向 Azure

1. 从 "发布" 选项卡中, 使用值旁边的 "**复制到剪贴板**" 按钮复制**网站 URL** 。

    ![从 "发布" 选项卡复制网站 URL](../media/8-copy-site-url.png)

1. `MainViewModel`从`ImHere`项目中打开。

1. 将`baseUrl`字段的值更新为从 "发布" 选项卡复制的网站 URL。

## <a name="test-it-out"></a>测试

1. 将`ImHere.UWP`应用程序设置为启动应用程序并运行它。

1. 输入电话号码, 然后单击 "**发送位置**" 按钮。

1. 您应以 SMS 消息的形式收到该位置。

1. 如果您收到一项*服务不可用*错误, 请检查您的函数应用程序使用的是哪个版本的 "Twilio" NuGet 包, 它应为 3.0.0-rc1, 而不是3.0.0。
1. 如果您收到一项*服务不可用*错误, 请检查您的函数应用程序使用的是哪个版本的 "Twilio" NuGet 包, 它应为 3.0.0-rc1,**而不**是3.0.0。

## <a name="summary"></a>摘要

在此单元中, 你学习了如何在 Visual Studio 中将 azure 函数项目发布到 azure, 并配置应用程序设置。