捕获天气数据是一项重要任务, 因为天气可能会影响流量模式与零售商店中的加热、通风和空气调节 (HVAC) 系统的运营方式之间的所有内容。 在本练习中, 你将与在线 Raspberry Pi 模拟器进行交互, 你学习了如何在上一个单元中捕获模拟的天气数据, 并通过 Azure IoT 中心进行操作。

[!include[](../../../includes/azure-sandbox-activate.md)]

虽然在模拟环境中执行此操作, 但在模拟设备上运行的应用程序可以在将来转移到实际设备。

## <a name="create-an-iot-hub"></a>创建 IoT 中心
Azure IoT 中心提供了功能和可扩展性模型, 使设备和后端开发人员能够构建强大的设备管理解决方案。 设备的范围从受约束的传感器和单一目的 microcontrollers, 到路由设备组通信的功能强大的网关。 此外, IoT 运算符的用例和要求在各行业中的变化显著不同。 尽管这种变化, 但使用 IoT 中心的设备管理还提供了可适应各种设备和最终用户的功能、模式和代码库。

若要从 Raspberry Pi 模拟器开始收集数据, 需要先创建 IoT 中心。

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

2. 选择 "在 Azure 门户的左上角**创建资源**"。

3. 选择 " **Internet 内容**", 然后选择 " **IoT 中心**"。

![指向 IoT 中心的 Azure 门户导航的屏幕截图](../media/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. 在**iot 中心**窗格中, 输入你的 iot 中心的以下信息:

   - **订阅**: 使用此示例的默认订阅。
   - **资源组**: 使用现有的资源组。 通过将所有相关资源放在同一个组中, 可以将它们全部管理在一起。 例如, 删除资源组将删除该组中包含的所有资源。
   - **名称**: 为 IoT 中心创建唯一名称。 如果输入的名称可用, 则会出现一个绿色的复选标记。
   - **区域**: 从以下列表中选择最接近你的位置。

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    > [!IMPORTANT]
    > IoT 中心将公开为 DNS 终结点, 因此在对其命名时, 请务必避免任何敏感信息。

    ![IoT 中心基础知识窗口](./../media/dbb7319388673b8ee0e0b407536156c0.png)

1. 选择 "**下一步: 大小和缩放**" 以继续创建 IoT 中心。
2. 选择**定价和扩展层**。 对于此示例, 请选择**无 F1**的层。

    ![IoT 中心大小和缩放窗口](../media/b506eb3293fa4aa9d4785ad498fc476c.png)

3. 选择 "**审阅 + 创建**"。

4. 查看 IoT 中心信息, 然后单击 "**创建**"。 你的 IoT 中心可能需要几分钟的时间才能创建。 您可以在 "**通知**" 窗格中监视进度。

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up exercise. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a>注册设备
在可以连接之前, 必须向你的 IoT 中心注册设备。

1. 在 iot 中心导航菜单中, 打开**iot 设备**, 然后单击 "**添加**" 以在 IoT 中心中注册设备。

   ![在 iot 中心的 iot 设备中添加设备](../media/ee5f177abcf06b86dd007fce3b8448ad.png)

2. 为新设备输入**设备 ID** 。 选择一个有意义的 ID 来表示设备。 设备 id 区分大小写。

    > [!IMPORTANT]
    > 设备 ID 可能在为客户支持和故障排除收集的日志中可见, 因此, 请务必在对其命名时避免任何敏感信息。

3. 单击"保存"。
4. 创建设备后, 从 " **IoT 设备**" 窗格的列表中打开该设备。
5. 将 **---主键的连接字符串**复制到稍后使用。

   ![获取设备连接字符串](../media/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a>发送模拟遥测

1. 打开[Raspberry Pi Azure IoT 模拟器](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true)。
1. 将第15行中的占位符替换为您刚复制的 Azure IoT 中心设备连接字符串。
1. 单击 " `Run`控制台" 窗口`npm start`中的按钮或键入以运行应用程序。

    ![替换设备连接字符串](../media/Line15.png)

1. 您应该会看到以下输出, 其中显示传感器数据和发送到 IoT 中心的邮件。

    ![从 Raspberry Pi 发送到 IoT 中心的输出传感器数据](../media/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a>从你的中心读取遥测
那么, 会发生什么情况呢？ IoT 中心正在接收从模拟设备发送的设备到云消息。 为了了解这一点, 让我们快速了解 Azure IoT 中心处理传入数据的方式。 在 IoT 中心中的 "**监视**" 下, 选择 "**指标**"。 等待数据进入图片时, 请等待几分钟, 然后重试。

![IoT 中心指标](../media/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
