**Azure 高级威胁防护**(Azure ATP) 是一种基于云的安全解决方案, 用于识别、检测和帮助您调查组织中的高级威胁、已泄露身份和恶意内幕活动。

Azure ATP 能够检测已知的恶意攻击和技术、安全问题以及针对网络的风险。

## <a name="azure-atp-components"></a>Azure ATP 组件

Azure ATP 由多个组件组成。

**Azure ATP 门户** 

Azure ATP 有自己的门户, 您可以通过它监视和响应可疑活动。 azure atp 门户允许您创建 azure atp 实例, 并查看从 Azure atp 传感器收到的数据。 您还可以使用门户监视、管理和调查网络环境中的威胁。 你可以在上[https://portal.atp.azure.com](https://portal.atp.azure.com)登录到 Azure ATP 门户。 您必须使用分配给可访问 azure ATP 门户的 azure AD 安全组的用户帐户登录。

**Azure ATP 传感器** 

Azure ATP 传感器直接安装在域控制器上。 传感器监控域控制器流量, 而不需要专用服务器或配置端口镜像。

**Azure ATP 云服务** 

azure ATP 云服务在 azure 基础结构上运行, 目前部署在美国、欧洲和亚洲。 Azure ATP 云服务已连接到 Microsoft 的智能安全图形。

![Azure 高级威胁防护仪表板和事件时间线的屏幕截图, 显示安全事件, 如 HoneyToken 活动、检测到远程执行尝试和可疑服务创建](../media/7-atp-sa-timeline.png)

## <a name="purchasing-azure-advanced-threat-protection"></a>购买 Azure 高级威胁防护

Azure ATP 可作为企业移动性 + Security 5 套件 (EMS E5) 的一部分和作为独立许可证。 您可以直接从 "[企业移动性 + 安全性定价选项](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)" 页或通过云解决方案提供商 (CSP) 许可模型获取许可证。 它不适用于通过 Azure 门户购买。