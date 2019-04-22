你的部门中的公共信息官 (PIO) 维护非公开网站, 以供本地媒体使用。 你的 PIO 使用移动设备更新媒体网站上的内容, 以便本地媒体插座可以随时了解当前事件。 若要防止向媒体显示未经授权或不正确的信息, 此网站必须尽可能安全。 作为管理员, 为提高安全性, 您可以采取的一种方法是让网站保持最新的更新。

在这里, 我们将介绍 Azure 的更新管理解决方案。

## <a name="update-management-overview"></a>更新管理概述

 通过更新管理解决方案, 可以管理和安装在 Azure、内部部署中甚至在其他云提供程序中部署的 Windows 和 Linux 虚拟机的操作系统更新和修补程序。 您可以评估计算机上可用更新的状态, 并管理安装服务器所需更新的过程。  

 更新管理解决方案具有以下几个优点:
  1. 虚拟机中没有代理或其他配置。
  1. 你可以在不登录到 VM 的情况下运行更新。 此外, 您还无需创建用于安装更新的密码。
  1. 更新管理解决方案列出缺少的更新, 并提供有关在易于阅读的格式中失败的部署的信息。

更新管理可用于在同一租户的多个订阅中的本机板载计算机。 若要管理不同租户中的计算机, 必须将其作为非 Azure 计算机进行集成。

## <a name="supported-operating-systems"></a>支持的操作系统

Update Management 解决方案支持 Windows 和 Linux, 具体说就是:
 - Windows Server (2008 和更高版本)
 - CentOS 6 (x86/X64) 和 CentOS 7
 - Red Hat Enterprise 6 (x86/x64) 和 7 (x64)
 - SUSE Linux Enterprise Server 11 (x86/x64) 和 12 (x64)
 - Ubuntu 14.04 LTS、16.04 LTS 和 18.04 (x86/x64)

在本模块中, 我们将使用在 Azure 中部署的 Windows Server 2016 虚拟机。
 
## <a name="components-used-by-update-management"></a>更新管理使用的组件

以下配置用于执行评估和更新部署:

- 适用于 Windows 或 Linux 的 Microsoft Monitoring Agent (MMA)。
- 适用于 Linux 的 PowerShell Desired State Configuration (DSC)。
- 自动化混合 Runbook 辅助角色。
- 适用于 windows 计算机的 Microsoft update 或 windows Server Update Services (WSUS)。

下图显示了行为和数据流的概念视图, 以及解决方案如何评估并将安全更新应用到工作区中所有连接的 Windows Server 和 Linux 计算机。

![数据流的概念视图](../media/2-conceptual-view-data-flow50.png "数据流的概念视图")

### <a name="hybrid-worker-groups"></a>混合辅助角色组

 直接连接到 Log Analytics 工作区的 Windows 计算机将自动配置为混合 Runbook 辅助角色, 以支持此解决方案中包含的 runbook。 由解决方案管理的每台 Windows 计算机在 "混合工作器组" 窗格中列出为自动化帐户的系统混合辅助角色组。 这些解决方案使用命名约定 Hostname FQDN_GUID。

## <a name="operations-manager-management-packs"></a>Operations Manager 管理包

如果 System Center Operations Manager 管理组已连接到 Log Analytics 工作区, 则会在 Operations Manager 中安装以下管理包。 在添加解决方案之后, 这些管理包也会安装在直接连接的 Windows 计算机上。 您无需配置或管理这些管理包。
- Microsoft System Center Advisor 更新评估智能包 
- IntelligencePack UpdateAssessment
- 更新部署 MP
