<span data-ttu-id="1abd7-101">在上一个练习中, 我们启用了试用许可证, 创建了一个目录, 创建了一个用户, 并创建了一个组来测试我们的解决方案。</span><span class="sxs-lookup"><span data-stu-id="1abd7-101">In the previous exercise, we enabled trial licenses, created a directory, created a user, and created a group to test our solution.</span></span> <span data-ttu-id="1abd7-102">在此单元中, 我们将创建条件访问规则, 以要求 azure 多因素身份验证 azure 门户。</span><span class="sxs-lookup"><span data-stu-id="1abd7-102">In this unit, we will create our conditional access rule to require Azure Multi-Factor Authentication for the Azure portal.</span></span>

## <a name="enable-conditional-access-based-multi-factor-authentication"></a><span data-ttu-id="1abd7-103">启用基于条件访问的多因素身份验证</span><span class="sxs-lookup"><span data-stu-id="1abd7-103">Enable conditional access-based Multi-Factor Authentication</span></span>

<span data-ttu-id="1abd7-104">条件访问允许管理员配置何时或不希望发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="1abd7-104">Conditional access allows administrators to configure when they do or do not want something to happen.</span></span> <span data-ttu-id="1abd7-105">他们可以同时使用多个规则来授予或拒绝对资源的访问权限。</span><span class="sxs-lookup"><span data-stu-id="1abd7-105">They can use multiple rules in parallel to grant or deny access to resources.</span></span> <span data-ttu-id="1abd7-106">下面是我们需要创建的规则:</span><span class="sxs-lookup"><span data-stu-id="1abd7-106">Here's the rule that we need to create:</span></span>

<span data-ttu-id="1abd7-107">**访问 Azure 门户时-要求进行多因素身份验证**</span><span class="sxs-lookup"><span data-stu-id="1abd7-107">**When accessing the Azure portal - Require multi-factor authentication**</span></span>

<span data-ttu-id="1abd7-108">下面的步骤将引导您完成创建条件访问规则的过程, 以要求用户在访问 Azure 门户时执行多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="1abd7-108">The steps that follow will walk you through the process to create a conditional access rule to require users to perform multi-factor authentication when they access the Azure portal.</span></span>

1. <span data-ttu-id="1abd7-109">浏览到**Azure Active Directory**, 并在生成的刀片中查找并选择 "**安全**" 子部分中的 "**条件访问**"。</span><span class="sxs-lookup"><span data-stu-id="1abd7-109">Browse to **Azure Active Directory**, and in the resulting blade locate and select **Conditional access** in the **Security** subsection.</span></span>

![显示带有选择框的 azure 门户导航项目的屏幕截图对 azure Active Directory 项目和条件访问项的关注](../media/4-portal-screenshot-1.png)

1. <span data-ttu-id="1abd7-111">单击 "**新建策略**"。</span><span class="sxs-lookup"><span data-stu-id="1abd7-111">Click **New policy**.</span></span> <span data-ttu-id="1abd7-112">这将打开一个新的刀片来创建新策略。</span><span class="sxs-lookup"><span data-stu-id="1abd7-112">This will open a new blade for creating the new policy.</span></span>

1. <span data-ttu-id="1abd7-113">Name 策略**需要对 Azure 门户进行 MFA**。</span><span class="sxs-lookup"><span data-stu-id="1abd7-113">Name the policy **Require MFA for Azure portal**.</span></span>

1. <span data-ttu-id="1abd7-114">在 "**分配**" 下, 选择 "**用户和组**" 打开下一个刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="1abd7-114">Under **Assignments** select **Users and groups** to open the next blade.</span></span>

1. <span data-ttu-id="1abd7-115">单击 "**选择用户和组**", 然后在其下方**选择**。</span><span class="sxs-lookup"><span data-stu-id="1abd7-115">Click **Select users and groups** and then **Select** below it.</span></span> <span data-ttu-id="1abd7-116">这将打开选择边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-116">This will open the selection blade.</span></span>

1. <span data-ttu-id="1abd7-117">选择我们在以前单位中创建的组 " **CA-MFA-AzurePortal**", 然后单击底部的 "**选择**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="1abd7-117">Select the group that we created in the previous unit, **CA-MFA-AzurePortal**, then click the **Select** button at the bottom.</span></span> <span data-ttu-id="1abd7-118">这将关闭选择边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-118">This will close the selection blade.</span></span>

1. <span data-ttu-id="1abd7-119">单击 "**完成**" 按钮完成此步骤并关闭刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="1abd7-119">Click the **Done** button to complete this step and close the blade.</span></span> <span data-ttu-id="1abd7-120">您应再次看到在上面的第二步中打开的新策略边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-120">You should once again see the new policy blade you opened in the second step above.</span></span>

1. <span data-ttu-id="1abd7-121">在 "**分配**" 下, 选择 "**云应用**" 打开下一个刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="1abd7-121">Under **Assignments** select **Cloud apps** to open the next blade.</span></span>

1. <span data-ttu-id="1abd7-122">单击 "**选择应用**", 然后在其下方**选择**。</span><span class="sxs-lookup"><span data-stu-id="1abd7-122">Click **Select apps** and then **Select** below it.</span></span> <span data-ttu-id="1abd7-123">这将打开选择边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-123">This will open the selection blade.</span></span>

1. <span data-ttu-id="1abd7-124">选择 " **Microsoft Azure 管理**", 然后选择底部的 "**选择**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="1abd7-124">Select **Microsoft Azure Management**, and then the **Select** button at the bottom.</span></span> <span data-ttu-id="1abd7-125">这将关闭选择边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-125">This will close the selection blade.</span></span>

1. <span data-ttu-id="1abd7-126">单击 "**完成**" 按钮完成此步骤并关闭刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="1abd7-126">Click the **Done** button to complete this step and close the blade.</span></span> <span data-ttu-id="1abd7-127">您应再次看到在上面的第二步中打开的新策略边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-127">You should once again see the new policy blade you opened in the second step above.</span></span>

1. <span data-ttu-id="1abd7-128">在 "**访问控制**" 下, 选择 "**授予**" 打开下一个刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="1abd7-128">Under **Access controls** select **Grant** to open the next blade.</span></span>

1. <span data-ttu-id="1abd7-129">单击 "**授予访问权限**", 然后**要求进行多因素身份验证**。</span><span class="sxs-lookup"><span data-stu-id="1abd7-129">Click **Grant access** and then **Require multi-factor authentication**.</span></span> <span data-ttu-id="1abd7-130">单击 "**选择**" 按钮完成此步骤并关闭刀片式服务器。</span><span class="sxs-lookup"><span data-stu-id="1abd7-130">Click the **Select** button to complete this step and close the blade.</span></span> <span data-ttu-id="1abd7-131">您应再次看到在上面的第二步中打开的新策略边栏。</span><span class="sxs-lookup"><span data-stu-id="1abd7-131">You should once again see the new policy blade you opened in the second step above.</span></span>

1. <span data-ttu-id="1abd7-132">将 "**启用策略**" 设置为 **"开"**。</span><span class="sxs-lookup"><span data-stu-id="1abd7-132">Set **Enable policy** to **On**.</span></span>

1. <span data-ttu-id="1abd7-133">单击"创建"。</span><span class="sxs-lookup"><span data-stu-id="1abd7-133">Click **Create**.</span></span> <span data-ttu-id="1abd7-134">如果未启用 "**创建**" 按钮, 请查看前面的步骤以确保已正确完成这些步骤。</span><span class="sxs-lookup"><span data-stu-id="1abd7-134">If the **Create** button is not enabled, review the previous steps to ensure you've completed them all correctly.</span></span>

<span data-ttu-id="1abd7-135">在此单元中, 你学习了如何为之前定义的组和/或用户创建条件访问规则。</span><span class="sxs-lookup"><span data-stu-id="1abd7-135">In this unit, you learned how to create a conditional access rule for a previously defined group and/or user(s).</span></span> <span data-ttu-id="1abd7-136">访问 Azure 门户时, 该规则需要多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="1abd7-136">The rule requires Multi-Factor Authentication when accessing the Azure portal.</span></span>