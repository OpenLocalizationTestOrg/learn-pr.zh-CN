> [!TIP]
> 登录到 VM 所需的用户名和密码位于 "**资源**" 选项卡上。

> [!NOTE]
> 如果您使用的是 Mac, 则在启动虚拟机后, 您可能需要使用工具栏上的闪电图标, 或从**** "资源" 选项卡上的 "**资源**" 选项卡中的 "资源" 选项卡旁边的 "打开", 以解除对 VM 的锁定。


在本模块中, 将创建具有无服务器后端的跨平台 Xamarin. 表单应用程序。 此应用将从其设备中获取用户的位置, 并将电话号码列表发送到 Azure 函数。 然后, 该函数将使用与第三方服务 (Twilio) 的绑定将您的位置作为短信发送给提供的所有电话号码。

此过程涉及以下步骤:

1. 应用程序使用 Xamarin 作为抽象来捕获您在特定于设备的位置 api 上的位置。

1. 位置和电话号码打包到 JSON 有效负载中并发送到 Azure 函数。

1. Azure 函数对 JSON 有效负载进行解码并创建 SMS 消息。

1. SMS 消息通过[Twilio](https://www.twilio.com/?azure-portal=true)发送。

下图显示了此过程的概述。

![该图显示了通过短信共享位置的过程的高级别体系结构。](../media/1-architecture.png)

## <a name="create-a-twilio-account"></a>创建 Twilio 帐户

若要能够从 Azure 函数发送短信消息, 您需要一个 Twilio 帐户。 免费帐户不足以开始。

1. 头到[twilio.com](https://www.twilio.com?azure-portal=true)。

1. 单击右上角的红色 "**注册**" 按钮。

1. 填写详细信息, 然后单击 "**开始**"。

1. 你需要验证你的电话号码。 Twilio 免费帐户允许您仅将邮件发送到已验证的电话号码, 以阻止它们用于垃圾邮件。 Twilio 将向您发送验证代码, 您需要输入该代码来验证您的电话。

1. 选择 "**产品**" 选项卡, 然后单击 "**可编程短信**", 然后单击 "**继续**"。

1. 为第一个项目 (如 "我在这里") 提供一个名称, 然后单击 "**继续**"。

1. 跳过要邀请团队配对的步骤。

1. 在 Twilio 消息仪表板中, 展开 "**项目信息**" 面板。

1. 请注意, 你的**帐户 SID**和**身份验证令牌**, 因为稍后将需要这些值。

    创建 Twilio 帐户时, 会向您分配一个可从其发送邮件的电话号码。 您可以在 "Twilio**电话号码**" 仪表板上找到此电话号码。

1. 在 Twilio 网站中, 选择左侧菜单底部的省略号。 然后, 选择 "*超级网络->Phone 号码*"。 您可以使用 pin 图标将此仪表板固定到左侧菜单。 您的 Twilio 号码将位于 "*管理号码->Active 号码*" 下。

    ![查找您的 Twilio 号码](../media/7-twilio-find-number.png)

    > [!TIP]
    > 如果还没有活动号码, 请选择 "活动**** 号码" 页中的 "开始", 开始创建号码的过程。

1. 记下您的活动电话号码。 本模块后面将会用到它。


> [!NOTE]
> 当你注册时, 你将被分配一个将用于发送短信的 Twilio 电话号码。 在某些国家/地区, 这些号码可能无法发送短信消息。 Twilio 文档列出[了哪些国家/地区有限制](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true), 并显示了使用[国际号码或字母数字发件人 Id](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true)发送短信的方法。

## <a name="launch-visual-studio"></a>启动 Visual Studio

对于本模块, 你将使用 Visual Studio 2017 (通过虚拟机提供) 开发移动应用和 Azure 函数应用。 [! 注意] 尽管可以构建用于在 iOS、Android 和通用 Windows 平台 (UWP) 上运行的 Xamarin 应用程序, 但此模块仅侧重于 UWP, 以便它可以在实验室虚拟机中运行。

从 VM 的 "开始" 菜单或从桌面快捷方式启动 Visual Studio 2017。

## <a name="summary"></a>摘要

在此单位中, 您创建了一个 Twilio 帐户, 用于发送短信并启动 Visual Studio。 接下来, 您将了解如何创建 xamarin 和添加 xamarin NuGet 包。

> [!IMPORTANT]
> 请记下您在此单元中收集的 Twilio**帐户 SID**和**AUTH TOKEN**以及**活动电话号码**值, 因为稍后将需要这些值。
