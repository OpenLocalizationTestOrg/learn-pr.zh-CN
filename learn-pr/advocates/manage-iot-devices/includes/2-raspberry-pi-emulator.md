Raspberry Pi 板在测试 theories 的过程中有 garnered 的更多兴趣, 甚至要做的事也更酷。 虽然此母板上的成本较低, 但有些人可能有兴趣在投资前测试 Raspberry Pi 的功能。

Microsoft 已构建了一个在线[Raspberry Pi Azure IoT 模拟器](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true), 允许用户通过代码控制模拟硬件。 仿真程序将 Raspberry Pi 的图形 portrays 连接到温度、湿度和压力传感器, 并通过 breadboard 允许电路连接到一个红色的 LED。 显示的侧面板允许用户输入 node.js JavaScript 代码, 以控制 LED 并从模拟传感器中收集虚拟数据。

![Raspberry Pi 模拟器](../media/RaspberryPiSimulator.png)

## <a name="raspberry-pi-azure-iot-online-simulator"></a>Raspberry Pi Azure IoT Online 模拟器

在首次运行时, 仿真程序将运行通过命令行显示的示例温度捕获程序。 同样的示例应用程序还可以在实际 Pi 上运行, 因为模拟器旨在允许用户在将代码转移到真正的设备之前对其进行测试。

web 模拟器中有三个区域:

1. **程序集区域**。 你可以在此处查看你的设备状态。 默认情况下, 这是一个与 BME280 传感器和 LED 指示灯连接的 Pi。 此配置现在不可自定义。
2. **编码区域**。 使用 node.js 在 Raspberry Pi 上创建应用程序的联机代码编辑器。 默认的示例应用程序可帮助收集 BME280 传感器中的传感器数据并将其发送到 Azure IoT 中心。
3. **集成控制台窗口**。 您可以在此处查看应用程序的输出。 在控制台中有三个函数:
    - `run`-运行示例代码 (当示例运行时, 代码为只读)。
    - `Stop`-停止运行示例代码。
    - `Reset`-重置代码。

现在您已经概述了 Raspberry Pi 模拟器, 我们将研究 Azure 中的 IoT 中心, 你将在其中创建新资源以从模拟器中捕获数据。

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>
-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->