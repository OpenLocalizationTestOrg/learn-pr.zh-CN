首先, 顾问会检查基于角色的访问控制 (RBAC) 更改了季度, 以供审核和故障排除之用。 您知道更改已记录在[Azure 活动日志](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)中。 你的经理已询问你是否可以生成上个月的角色分配和自定义角色更改的报告。

## <a name="view-activity-logs"></a>查看活动日志

开始时最简单的方法是使用 Azure 门户查看活动日志。

1. 单击 "**所有服务**", 然后找到 "**活动日志**"。

    ![显示 "活动日志位置" 选项的 Azure 门户屏幕截图](../media/6-all-services-activity-log.png)

1. 单击 "**活动日志**" 以打开 "活动日志"。

    ![显示活动日志的 Azure 门户屏幕截图](../media/6-activity-log-portal.png)

1. 将时间**跨度**筛选器设置为 "**上个月**"。

1. 添加**操作**筛选器和类型**角色**以筛选列表。

1. 选择以下 RBAC 操作:

    - 创建角色分配 (roleAssignments)
    - 删除角色分配 (roleAssignments)
    - 创建或更新自定义角色定义 (roleDefinitions)
    - 删除自定义角色定义 (roleDefinitions)

    ![显示选择了四个筛选器的操作筛选器列表的屏幕截图](../media/6-operation-filter.png)

    几分钟后, 你将看到上个月的所有角色分配和角色定义操作。 它还包括将活动日志下载为 CSV 文件的链接。

1. 单击其中一个操作以查看活动日志详细信息。

    ![屏幕截图显示活动日志的详细信息](../media/6-activity-log-details.png)

在此单元中, 您学习了如何使用 Azure 活动日志列出门户中的 RBAC 更改并生成简单报告。