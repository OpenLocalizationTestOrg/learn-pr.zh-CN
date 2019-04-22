<span data-ttu-id="d82b8-101">首先, 顾问会检查基于角色的访问控制 (RBAC) 更改了季度, 以供审核和故障排除之用。</span><span class="sxs-lookup"><span data-stu-id="d82b8-101">First Up Consultants reviews role-based access control (RBAC) changes quarterly for auditing and troubleshooting purposes.</span></span> <span data-ttu-id="d82b8-102">您知道更改已记录在[Azure 活动日志](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)中。</span><span class="sxs-lookup"><span data-stu-id="d82b8-102">You know that changes get logged in [Azure Activity Log](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</span></span> <span data-ttu-id="d82b8-103">你的经理已询问你是否可以生成上个月的角色分配和自定义角色更改的报告。</span><span class="sxs-lookup"><span data-stu-id="d82b8-103">Your manager has asked if you can generate a report of the role assignment and custom role changes for the last month.</span></span>

## <a name="view-activity-logs"></a><span data-ttu-id="d82b8-104">查看活动日志</span><span class="sxs-lookup"><span data-stu-id="d82b8-104">View activity logs</span></span>

<span data-ttu-id="d82b8-105">开始时最简单的方法是使用 Azure 门户查看活动日志。</span><span class="sxs-lookup"><span data-stu-id="d82b8-105">The easiest way to get started is to view the activity logs with the Azure portal.</span></span>

1. <span data-ttu-id="d82b8-106">单击 "**所有服务**", 然后找到 "**活动日志**"。</span><span class="sxs-lookup"><span data-stu-id="d82b8-106">Click **All services** and then find **Activity log**.</span></span>

    ![显示 "活动日志位置" 选项的 Azure 门户屏幕截图](../media/6-all-services-activity-log.png)

1. <span data-ttu-id="d82b8-108">单击 "**活动日志**" 以打开 "活动日志"。</span><span class="sxs-lookup"><span data-stu-id="d82b8-108">Click **Activity log** to open the activity log.</span></span>

    ![显示活动日志的 Azure 门户屏幕截图](../media/6-activity-log-portal.png)

1. <span data-ttu-id="d82b8-110">将时间**跨度**筛选器设置为 "**上个月**"。</span><span class="sxs-lookup"><span data-stu-id="d82b8-110">Set the **Timespan** filter to **Last month**.</span></span>

1. <span data-ttu-id="d82b8-111">添加**操作**筛选器和类型**角色**以筛选列表。</span><span class="sxs-lookup"><span data-stu-id="d82b8-111">Add an **Operation** filter and type **role** to filter the list.</span></span>

1. <span data-ttu-id="d82b8-112">选择以下 RBAC 操作:</span><span class="sxs-lookup"><span data-stu-id="d82b8-112">Select the following RBAC operations:</span></span>

    - <span data-ttu-id="d82b8-113">创建角色分配 (roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="d82b8-113">Create role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="d82b8-114">删除角色分配 (roleAssignments)</span><span class="sxs-lookup"><span data-stu-id="d82b8-114">Delete role assignment (roleAssignments)</span></span>
    - <span data-ttu-id="d82b8-115">创建或更新自定义角色定义 (roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="d82b8-115">Create or update custom role definition (roleDefinitions)</span></span>
    - <span data-ttu-id="d82b8-116">删除自定义角色定义 (roleDefinitions)</span><span class="sxs-lookup"><span data-stu-id="d82b8-116">Delete custom role definition (roleDefinitions)</span></span>

    ![显示选择了四个筛选器的操作筛选器列表的屏幕截图](../media/6-operation-filter.png)

    <span data-ttu-id="d82b8-118">几分钟后, 你将看到上个月的所有角色分配和角色定义操作。</span><span class="sxs-lookup"><span data-stu-id="d82b8-118">After a few moments, you'll see all the role assignment and role definition operations for the last month.</span></span> <span data-ttu-id="d82b8-119">它还包括将活动日志下载为 CSV 文件的链接。</span><span class="sxs-lookup"><span data-stu-id="d82b8-119">It also includes a link to download the activity log as a CSV file.</span></span>

1. <span data-ttu-id="d82b8-120">单击其中一个操作以查看活动日志详细信息。</span><span class="sxs-lookup"><span data-stu-id="d82b8-120">Click one of the operations to see the activity log details.</span></span>

    ![屏幕截图显示活动日志的详细信息](../media/6-activity-log-details.png)

<span data-ttu-id="d82b8-122">在此单元中, 您学习了如何使用 Azure 活动日志列出门户中的 RBAC 更改并生成简单报告。</span><span class="sxs-lookup"><span data-stu-id="d82b8-122">In this unit, you learned how to use Azure Activity Log to list RBAC changes in the portal and generate a simple report.</span></span>