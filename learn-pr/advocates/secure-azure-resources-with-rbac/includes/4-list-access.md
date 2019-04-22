> [!NOTE]
> <span data-ttu-id="d6d72-101">启动实验室后, 您所需的用户名和密码位于说明旁边的 "**资源**" 选项卡上。</span><span class="sxs-lookup"><span data-stu-id="d6d72-101">After launching the lab, the username and password you need is located on the **Resources** tab next to the instructions.</span></span>

<span data-ttu-id="d6d72-102">在首次运行顾问时, 您已向市场营销团队授予了对资源组的访问权限。</span><span class="sxs-lookup"><span data-stu-id="d6d72-102">At First Up Consultants, you've been granted access to a resource group for the marketing team.</span></span> <span data-ttu-id="d6d72-103">您想要熟悉 Azure 门户, 并查看当前分配了哪些角色。</span><span class="sxs-lookup"><span data-stu-id="d6d72-103">You want to familiarize yourself with the Azure portal and see what roles are currently assigned.</span></span>

## <a name="list-role-assignments-for-yourself"></a><span data-ttu-id="d6d72-104">为自己列出角色分配</span><span class="sxs-lookup"><span data-stu-id="d6d72-104">List role assignments for yourself</span></span>

<span data-ttu-id="d6d72-105">按照以下步骤查看当前分配给您的角色。</span><span class="sxs-lookup"><span data-stu-id="d6d72-105">Follow these steps to see what roles are currently assigned to you.</span></span>

1. <span data-ttu-id="d6d72-106">在 Azure 门户的右上角, 单击您的用户名打开菜单。</span><span class="sxs-lookup"><span data-stu-id="d6d72-106">In the upper-right corner of the Azure portal, click your username to open the menu.</span></span>

1. <span data-ttu-id="d6d72-107">请确保您已登录为**LabAdmin-_XXXXXXX_**。</span><span class="sxs-lookup"><span data-stu-id="d6d72-107">Make sure you are signed in as **LabAdmin-_XXXXXXX_**.</span></span> <span data-ttu-id="d6d72-108">如果不是, 请使用 "**资源**" 选项卡上的用户名和密码注销并登录。</span><span class="sxs-lookup"><span data-stu-id="d6d72-108">If not, sign out and sign in using the username and password on the **Resources** tab.</span></span>

1. <span data-ttu-id="d6d72-109">单击省略号 (**...**) 以查看更多链接。</span><span class="sxs-lookup"><span data-stu-id="d6d72-109">Click the ellipsis (**...**) to see more links.</span></span>

    ![突出显示了我的权限的用户菜单屏幕截图](../media/4-my-permissions-menu.png)

1. <span data-ttu-id="d6d72-111">单击 "**我的权限**" 打开 "我的权限" 窗格。</span><span class="sxs-lookup"><span data-stu-id="d6d72-111">Click **My permissions** to open the My permissions pane.</span></span>

    !["我的权限" 窗格的屏幕截图](../media/4-my-permissions-pane.png)

    <span data-ttu-id="d6d72-113">在 "我的权限" 窗格中, 您可以看到您已分配的角色和作用域。</span><span class="sxs-lookup"><span data-stu-id="d6d72-113">On the My permissions pane, you can see the roles that you have been assigned and the scope.</span></span> <span data-ttu-id="d6d72-114">您的列表看上去会有所不同。</span><span class="sxs-lookup"><span data-stu-id="d6d72-114">Your list will look different.</span></span>

## <a name="list-role-assignments-for-a-resource-group"></a><span data-ttu-id="d6d72-115">列出资源组的角色分配</span><span class="sxs-lookup"><span data-stu-id="d6d72-115">List role assignments for a resource group</span></span>

<span data-ttu-id="d6d72-116">按照以下步骤查看在资源组作用域中分配的角色。</span><span class="sxs-lookup"><span data-stu-id="d6d72-116">Follow these steps to see what roles are assigned at the resource group scope.</span></span>

1. <span data-ttu-id="d6d72-117">在导航列表中, 单击 "**资源组**"。</span><span class="sxs-lookup"><span data-stu-id="d6d72-117">In the navigation list, click **Resource groups**.</span></span>

   ![显示资源组叶片的 Azure 门户屏幕截图](../media/4-resource-groups.png)

1. <span data-ttu-id="d6d72-119">查找并单击名为**FirstUpConsultantsRG1-_XXXXXXX_** 的资源组。</span><span class="sxs-lookup"><span data-stu-id="d6d72-119">Find and click the resource group named **FirstUpConsultantsRG1-_XXXXXXX_**.</span></span>

1. <span data-ttu-id="d6d72-120">单击 "**访问控制 (IAM)**"。</span><span class="sxs-lookup"><span data-stu-id="d6d72-120">Click **Access control (IAM)**.</span></span>

   ![显示所选资源组边栏中的访问控制 (IAM) 选项的位置的屏幕截图](../media/4-resource-group-access-control.png)

1. <span data-ttu-id="d6d72-122">单击 "**角色分配**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="d6d72-122">Click the **Role assignments** tab.</span></span>

    <span data-ttu-id="d6d72-123">您可以查看哪些用户有权访问此资源组。</span><span class="sxs-lookup"><span data-stu-id="d6d72-123">You can see who has access to this resource group.</span></span> <span data-ttu-id="d6d72-124">请注意, 某些角色的作用范围为**此资源**, 而其他角色则从父作用域进行 **(继承)** 。</span><span class="sxs-lookup"><span data-stu-id="d6d72-124">Notice that some roles are scoped to **This resource** while others are **(Inherited)** from a parent scope.</span></span>

   ![显示所选资源组的具有选定 "角色分配" 选项卡的 "访问控制" 的屏幕截图](../media/4-resource-group-role-assignment.png)

## <a name="list-roles"></a><span data-ttu-id="d6d72-126">列出角色</span><span class="sxs-lookup"><span data-stu-id="d6d72-126">List roles</span></span>

<span data-ttu-id="d6d72-127">正如您在上一个单元中学习的那样, 角色是权限的集合。</span><span class="sxs-lookup"><span data-stu-id="d6d72-127">As you learned in the previous unit, a role is a collection of permissions.</span></span> <span data-ttu-id="d6d72-128">Azure 具有超过70个内置角色, 您可以在角色分配中使用这些角色。</span><span class="sxs-lookup"><span data-stu-id="d6d72-128">Azure has over 70 built-in roles that you can use in your role assignments.</span></span> <span data-ttu-id="d6d72-129">按照此步骤列出角色。</span><span class="sxs-lookup"><span data-stu-id="d6d72-129">Follow this step to list the roles.</span></span>

- <span data-ttu-id="d6d72-130">在窗格顶部, 单击 "**角色**" 选项卡以查看所有内置角色和自定义角色的列表。</span><span class="sxs-lookup"><span data-stu-id="d6d72-130">At the top of the pane, click the **Roles** tab to see a list of all the built-in and custom roles.</span></span>

   <span data-ttu-id="d6d72-131">您可以看到分配给每个角色的用户和组的数量。</span><span class="sxs-lookup"><span data-stu-id="d6d72-131">You can see the number of users and groups that are assigned to each role.</span></span>

   ![显示分配给每个角色的角色、用户和组的列表的屏幕截图。](../media/4-roles-list.png)

<span data-ttu-id="d6d72-133">在此单元中, 你学习了如何在 Azure 门户中列出自己的角色分配。</span><span class="sxs-lookup"><span data-stu-id="d6d72-133">In this unit, you learned how to list the role assignments for yourself in the Azure portal.</span></span> <span data-ttu-id="d6d72-134">此外, 还学习了如何列出资源组的角色分配。</span><span class="sxs-lookup"><span data-stu-id="d6d72-134">You also learned how to list the role assignments for a resource group.</span></span>