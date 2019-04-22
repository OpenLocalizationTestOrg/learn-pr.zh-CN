<span data-ttu-id="33431-101">名为 Alain 的合作者在首次启动顾问时需要能够创建和管理正在处理的项目的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="33431-101">A co-worker named Alain at First Up Consultants needs the ability to create and manage virtual machines for a project he is working on.</span></span> <span data-ttu-id="33431-102">你的经理已要求你处理此请求。</span><span class="sxs-lookup"><span data-stu-id="33431-102">Your manager has asked that you handle this request.</span></span> <span data-ttu-id="33431-103">使用最佳实践向用户授予完成工作的最少权限, 您决定为资源组分配 Alain 的虚拟机参与者角色。</span><span class="sxs-lookup"><span data-stu-id="33431-103">Using the best practice to grant users the least privileges to get their work done, you decide to assign Alain the Virtual Machine Contributor role for a resource group.</span></span>

## <a name="grant-access"></a><span data-ttu-id="33431-104">授予访问权限</span><span class="sxs-lookup"><span data-stu-id="33431-104">Grant access</span></span>

<span data-ttu-id="33431-105">按照以下步骤操作, 将虚拟机参与者角色分配给资源组作用域上的用户。</span><span class="sxs-lookup"><span data-stu-id="33431-105">Follow these steps to assign the Virtual Machine Contributor role to a user at the resource group scope.</span></span>

1. <span data-ttu-id="33431-106">在导航列表中, 单击 "**资源组**"。</span><span class="sxs-lookup"><span data-stu-id="33431-106">In the navigation list, click **Resource groups**.</span></span>

1. <span data-ttu-id="33431-107">找到并单击 " \*\*FirstUpConsultantsRG1-_XXXXXXX_ \*\* " 资源组。</span><span class="sxs-lookup"><span data-stu-id="33431-107">Find and click the **FirstUpConsultantsRG1-_XXXXXXX_** resource group.</span></span>

1. <span data-ttu-id="33431-108">单击 "**访问控制 (IAM)**"。</span><span class="sxs-lookup"><span data-stu-id="33431-108">Click **Access control (IAM)**.</span></span>

1. <span data-ttu-id="33431-109">单击 "**角色分配**" 选项卡可查看当前角色分配列表。</span><span class="sxs-lookup"><span data-stu-id="33431-109">Click the **Role assignments** tab to see the current list of role assignments.</span></span>

   ![显示所选资源组的具有选定 "角色分配" 选项卡的 "访问控制" 的屏幕截图](../media/5-resource-group-role-assignment.png)

1. <span data-ttu-id="33431-111">在顶部, 单击 "**添加角色分配**"。</span><span class="sxs-lookup"><span data-stu-id="33431-111">At the top, click **Add role assignment**.</span></span>

   ![显示已突出显示 "添加角色分配" 按钮的访问控制的屏幕截图](../media/5-resource-group-add-role-assignment.png)

    <span data-ttu-id="33431-113">将打开 "**添加角色分配**" 窗格。</span><span class="sxs-lookup"><span data-stu-id="33431-113">The **Add role assignment** pane opens.</span></span>

   !["添加权限" 窗格的屏幕截图](../media/5-add-permissions.png)

1. <span data-ttu-id="33431-115">在 "**角色**" 下拉列表中, 选择 "**虚拟机参与者**"。</span><span class="sxs-lookup"><span data-stu-id="33431-115">In the **Role** drop-down list, select **Virtual Machine Contributor**.</span></span>

1. <span data-ttu-id="33431-116">在 "**选择**" 列表中, 选择 " **LabUser-_XXXXXXX_**"。</span><span class="sxs-lookup"><span data-stu-id="33431-116">In the **Select** list, select **LabUser-_XXXXXXX_**.</span></span>

    <span data-ttu-id="33431-117">您可以在 "**资源**" 选项卡上的说明旁边找到用户名。</span><span class="sxs-lookup"><span data-stu-id="33431-117">You can find the username on the **Resources** tab next to the instructions.</span></span>

   ![已完成所有字段的 "添加权限" 窗格的屏幕截图](../media/5-add-permissions-save.png)

1. <span data-ttu-id="33431-119">单击 "**保存**" 以创建角色分配。</span><span class="sxs-lookup"><span data-stu-id="33431-119">Click **Save** to create the role assignment.</span></span>

   <span data-ttu-id="33431-120">几分钟后, **LabUser-_XXXXXXX_ **用户将被分配到**__ FirstUpConsultantsRG1**资源组作用域的虚拟机参与者角色。</span><span class="sxs-lookup"><span data-stu-id="33431-120">After a few moments, the **LabUser-_XXXXXXX_** user is assigned the Virtual Machine Contributor role at the **FirstUpConsultantsRG1-_XXXXXXX_** resource group scope.</span></span> <span data-ttu-id="33431-121">用户现在可以在此资源组中创建和管理虚拟机。</span><span class="sxs-lookup"><span data-stu-id="33431-121">The user can now create and manage virtual machines just within this resource group.</span></span>

   ![<span data-ttu-id="33431-122">显示分配给用户的虚拟机参与者角色的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="33431-122">Screenshot showing the Virtual Machine Contributor role assigned to a user</span></span> ](../media/5-vm-contributor-assignment.png)

## <a name="remove-access"></a><span data-ttu-id="33431-123">删除访问权限</span><span class="sxs-lookup"><span data-stu-id="33431-123">Remove access</span></span>

<span data-ttu-id="33431-124">在 RBAC 中, 若要删除访问权限, 请删除角色分配。</span><span class="sxs-lookup"><span data-stu-id="33431-124">In RBAC, to remove access, you remove a role assignment.</span></span>

1. <span data-ttu-id="33431-125">在角色分配列表中, 选择具有虚拟机参与者角色的\*\*LabUser-_XXXXXXX_ \*\*用户。</span><span class="sxs-lookup"><span data-stu-id="33431-125">In the list of role assignments, select the **LabUser-_XXXXXXX_** user with the Virtual Machine Contributor role.</span></span>

1. <span data-ttu-id="33431-126">单击 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="33431-126">Click **Remove**.</span></span>

   ![显示 "删除角色分配" 消息的屏幕截图](../media/5-remove-role-assignment.png)

1. <span data-ttu-id="33431-128">在出现的 "**删除角色分配**" 消息中, 单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="33431-128">In the **Remove role assignments** message that appears, click **Yes**.</span></span>

<span data-ttu-id="33431-129">在此单元中, 你学习了如何使用 Azure 门户授予用户创建和管理资源组中的虚拟机的权限。</span><span class="sxs-lookup"><span data-stu-id="33431-129">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using the Azure portal.</span></span>