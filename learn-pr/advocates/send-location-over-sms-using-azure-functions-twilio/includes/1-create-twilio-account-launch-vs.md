## <a name="create-a-twilio-account"></a>创建 Twilio 帐户

若要能够从 Azure 函数发送短信消息, 您需要一个 Twilio 帐户。 免费帐户不足以开始。

1. 头到[twilio.com](https://www.twilio.com?azure-portal=true)。

1. 单击右上角的红色 "**注册**" 按钮。

1. 填写详细信息, 然后单击 "**开始**"。

1. 输入要验证的电话号码。 Twilio 免费帐户允许您仅将邮件发送到已验证的电话号码, 以阻止它们被用于垃圾邮件。 Twilio 将向您发送验证代码, 您需要输入该代码来验证您的电话。

    ![Twilio 注册中的电话验证步骤的屏幕截图](../media/twilio-verify-phone.png)
1. 登录到您的 Twilio 帐户, 然后单击您的帐户仪表板中**的 "获取试用号码**" 按钮。 Twilio 为您分配用于发送邮件的电话号码。

    > [!NOTE]
    > 这些分配的号码可能无法在某些国家/地区发送邮件。 Twilio 文档列出[了哪些国家/地区有限制](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), 并显示了使用[国际号码或字母数字发件人 Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true)发送短信的方法。

1. 记录新的 Twilio 试用号码;您将在本模块后面的部分中需要它。 您还可以随时单击左侧菜单底部的省略号, 然后导航到 "_超级网络_ > _电话号码_ > "_管理数字_ > _活动号码_。

## <a name="create-a-new-twilio-project"></a>创建新的 Twilio 项目

在开始使用 Twilio 向已验证的号码发送邮件之前, 请创建一个项目以发送 programable SMS。

1. 选择屏幕左上角的下拉框, 然后选择 "**新建项目**"。

    ![创建新项目](../media/twilio-new-project.png)

1. 选择 "**产品**" 选项卡, 然后单击 "**可编程短信**", 然后单击 "**继续**"。

1. 为第一个项目 (如 "我在这里") 提供一个名称, 然后单击 "**继续**"。

1. 跳过要邀请团队配对的步骤。

1. 在 Twilio 消息仪表板中, 展开 "**项目信息**" 面板。

    ![展开的 "项目信息" 面板的屏幕截图](../media/project-info.png)

1. 请注意, 你的**帐户 SID**和**身份验证令牌**, 因为稍后将需要这些值。

## <a name="launch-visual-studio"></a>启动 Visual Studio

对于本模块, 你将使用 Visual Studio 2017 开发移动应用和 Azure 函数应用。 [! 注意] 尽管可以构建用于在 iOS、Android 和通用 Windows 平台 (UWP) 上运行的 Xamarin 应用程序, 但本模块仅侧重于 UWP。

在系统上启动 Visual Studio 2017。

## <a name="summary"></a>摘要

在此单位中, 您创建了一个 Twilio 帐户, 用于发送短信并启动 Visual Studio。 接下来, 你将了解如何创建 xamarin 和添加 xamarin NuGet 包。

> [!IMPORTANT]
> 请记下您在此单元中收集的 Twilio**帐户 SID**和**AUTH TOKEN**以及**活动电话号码**值, 因为稍后将需要这些值。
