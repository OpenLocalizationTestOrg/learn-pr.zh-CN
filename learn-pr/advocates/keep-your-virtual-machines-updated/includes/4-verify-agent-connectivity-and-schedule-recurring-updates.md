除了面向公众的网站之外, 该部门还使用网站进行内部内容 (如派遣和患者护理记录)。 这些网站必须尽可能安全。

在这里, 你将了解如何评估代理连接并安排定期更新。

## <a name="components-used-by-update-management"></a>更新管理使用的组件

以下配置用于执行评估和更新部署:

- 适用于 Windows 或 Linux 的 Microsoft Monitoring Agent (MMA)。
- 适用于 Linux 的 PowerShell Desired State Configuration (DSC)。
- 自动化混合 Runbook 辅助角色。
- 适用于 windows 计算机的 Microsoft update 或 windows Server Update Services (WSUS)。

## <a name="compliance-scan"></a>合规性扫描

更新管理将执行对更新合规性的扫描。 默认情况下, 合规性扫描在 Windows 计算机上每12小时执行一次, 在 Linux 计算机上每3小时执行一次。 除了扫描计划之外, 如果重新启动 MMA 时, 将在15分钟内启动合规性扫描, 并在安装更新安装之前和安装更新后启动。 在计算机执行对更新合规性的扫描后, 代理会将信息批量转发到 Azure 日志分析。

除了扫描计划之外, 在15分钟内启动更新合规性扫描, 如果重新启动了 MMA, 则在安装更新之前和安装更新之后。

仪表板可能需要30分钟到6小时的时间, 才能显示托管计算机中更新的数据。

## <a name="recurring-updates"></a>定期更新

您可以创建更新的计划和定期部署。 通过计划的部署, 您可以通过明确指定计算机或选择基于一组特定计算机的日志搜索的计算机组来定义哪些目标计算机接收更新。 此外, 还可以指定计划以供审批并指定在一段时间内安装更新。

更新由 Azure 自动化中的 runbook 安装。 您无法查看这些 runbook, 且 runbook 不需要任何配置。 在创建更新部署后, 更新部署将创建一个计划, 以在指定的时间为所包括的计算机启动一个主更新 runbook。 主 runbook 将在每个代理上启动子 runbook, 以执行所需更新的安装。
