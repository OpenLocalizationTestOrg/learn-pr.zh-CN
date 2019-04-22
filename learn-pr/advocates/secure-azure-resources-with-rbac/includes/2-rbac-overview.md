<span data-ttu-id="6f00e-101">假设您需要在 Azure 中管理对开发、工程和市场营销团队的资源的访问。</span><span class="sxs-lookup"><span data-stu-id="6f00e-101">Suppose you need to manage access to resources in Azure for the development, engineering, and marketing teams.</span></span> <span data-ttu-id="6f00e-102">您已开始接收访问请求, 您需要快速了解 access management 对 Azure 资源的工作方式。</span><span class="sxs-lookup"><span data-stu-id="6f00e-102">You’ve started to receive access requests, and you need to quickly learn how access management works for Azure resources.</span></span>

## <a name="what-is-rbac"></a><span data-ttu-id="6f00e-103">RBAC 是什么？</span><span class="sxs-lookup"><span data-stu-id="6f00e-103">What is RBAC?</span></span>

<span data-ttu-id="6f00e-104">基于角色的访问控制 (RBAC) 是一种基于 azure 资源管理器构建的授权系统, 可提供对 azure 中资源的细化访问管理。</span><span class="sxs-lookup"><span data-stu-id="6f00e-104">Role-based access control (RBAC) is an authorization system built on Azure Resource Manager that provides fine-grained access management of resources in Azure.</span></span> <span data-ttu-id="6f00e-105">Azure 有大量资源, 但有几个示例包括虚拟机、网站、网络和存储。</span><span class="sxs-lookup"><span data-stu-id="6f00e-105">Azure has lots of resources, but a few examples include virtual machines, websites, networks, and storage.</span></span>

#### <a name="what-is-role-based-access-control"></a><span data-ttu-id="6f00e-106">什么是基于角色的访问控制？</span><span class="sxs-lookup"><span data-stu-id="6f00e-106">What is role-based access control?</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvk]

## <a name="what-can-i-do-with-rbac"></a><span data-ttu-id="6f00e-107">我可以使用 RBAC 执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="6f00e-107">What can I do with RBAC?</span></span>

<span data-ttu-id="6f00e-108">RBAC 允许你授予对你控制的 Azure 资源的访问权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-108">RBAC allows you to grant access to Azure resources that you control.</span></span>

<span data-ttu-id="6f00e-109">下面是一些示例:</span><span class="sxs-lookup"><span data-stu-id="6f00e-109">Here are some examples:</span></span>

- <span data-ttu-id="6f00e-110">允许一个用户管理订阅中的虚拟机和另一个用户来管理虚拟网络</span><span class="sxs-lookup"><span data-stu-id="6f00e-110">Allow one user to manage virtual machines in a subscription and another user to manage virtual networks</span></span>
- <span data-ttu-id="6f00e-111">允许数据库管理员组在订阅中管理 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="6f00e-111">Allow a database administrator group to manage SQL databases in a subscription</span></span>
- <span data-ttu-id="6f00e-112">允许用户管理资源组中的所有资源, 如虚拟机、网站和子网</span><span class="sxs-lookup"><span data-stu-id="6f00e-112">Allow a user to manage all resources in a resource group, such as virtual machines, websites, and subnets</span></span>
- <span data-ttu-id="6f00e-113">允许应用程序访问资源组中的所有资源</span><span class="sxs-lookup"><span data-stu-id="6f00e-113">Allow an application to access all resources in a resource group</span></span>

## <a name="rbac-in-the-azure-portal"></a><span data-ttu-id="6f00e-114">Azure 门户中的 RBAC</span><span class="sxs-lookup"><span data-stu-id="6f00e-114">RBAC in the Azure portal</span></span>

<span data-ttu-id="6f00e-115">在 Azure 门户的多个区域中, 你将看到一个名为 "**访问控制 (IAM)**" 的刀片, 也称为 "标识和访问管理"。</span><span class="sxs-lookup"><span data-stu-id="6f00e-115">In several areas in the Azure portal, you'll see a blade named **Access control (IAM)**, also known as identity and access management.</span></span> <span data-ttu-id="6f00e-116">在此刀片式服务器上, 您可以看到谁有权访问该区域及其角色。</span><span class="sxs-lookup"><span data-stu-id="6f00e-116">On this blade, you can see who has access to that area and their role.</span></span> <span data-ttu-id="6f00e-117">使用这一相同的刀片, 可以授予或删除访问权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-117">Using this same blade, you can grant or remove access.</span></span>

<span data-ttu-id="6f00e-118">下面显示了资源组的访问控制 (IAM) 边栏示例。</span><span class="sxs-lookup"><span data-stu-id="6f00e-118">The following shows an example of the Access control (IAM) blade for a resource group.</span></span> <span data-ttu-id="6f00e-119">在此示例中, 已为 Alain Charon 分配了此资源组的备份操作员角色。</span><span class="sxs-lookup"><span data-stu-id="6f00e-119">In this example, Alain Charon has been assigned the Backup Operator role for this resource group.</span></span>

![显示具有 "备份操作员" 部分的 "访问控制角色分配" 边栏选项卡的 Azure 门户屏幕截图](../media/2-resource-group-access-control.png)

## <a name="how-does-rbac-work"></a><span data-ttu-id="6f00e-121">RBAC 的工作原理是什么？</span><span class="sxs-lookup"><span data-stu-id="6f00e-121">How does RBAC work?</span></span>

<span data-ttu-id="6f00e-122">您可以通过创建角色分配 (它控制如何强制实施权限), 使用 RBAC 控制对资源的访问。</span><span class="sxs-lookup"><span data-stu-id="6f00e-122">You control access to resources using RBAC by creating role assignments, which control how permissions are enforced.</span></span> <span data-ttu-id="6f00e-123">若要创建角色分配, 需要三个元素: 安全主体、角色定义和作用域。</span><span class="sxs-lookup"><span data-stu-id="6f00e-123">To create a role assignment, you need three elements: a security principal, a role definition, and a scope.</span></span> <span data-ttu-id="6f00e-124">可以将这些元素视为 "用户"、"内容" 和 "位置"。</span><span class="sxs-lookup"><span data-stu-id="6f00e-124">You can think of these elements as "who", "what", and "where".</span></span>

### <a name="1-security-principal-who"></a><span data-ttu-id="6f00e-125">1. 安全主体 (用户)</span><span class="sxs-lookup"><span data-stu-id="6f00e-125">1. Security principal (who)</span></span>

<span data-ttu-id="6f00e-126">*安全主体*只是要向其授予访问权限的用户、组或应用程序的别致名称。</span><span class="sxs-lookup"><span data-stu-id="6f00e-126">A *security principal* is just a fancy name for a user, group, or application that you want to grant access to.</span></span>

![显示安全主体 (包括用户、组和服务主体) 的说明。](../media/2-rbac-security-principal.png)

### <a name="2-role-definition-what-you-can-do"></a><span data-ttu-id="6f00e-128">2. 角色定义 (您可以执行的操作)</span><span class="sxs-lookup"><span data-stu-id="6f00e-128">2. Role definition (what you can do)</span></span>

<span data-ttu-id="6f00e-129">*角色定义*是权限的集合。</span><span class="sxs-lookup"><span data-stu-id="6f00e-129">A *role definition* is a collection of permissions.</span></span> <span data-ttu-id="6f00e-130">有时, 它只是称为角色。</span><span class="sxs-lookup"><span data-stu-id="6f00e-130">It's sometimes just called a role.</span></span> <span data-ttu-id="6f00e-131">角色定义列出了可以执行的权限, 如读取、写入和删除。</span><span class="sxs-lookup"><span data-stu-id="6f00e-131">A role definition lists the permissions that can be performed, such as read, write, and delete.</span></span> <span data-ttu-id="6f00e-132">角色可以是高级别的, 如所有者或特定的, 如虚拟机参与者。</span><span class="sxs-lookup"><span data-stu-id="6f00e-132">Roles can be high-level, like Owner, or specific, like Virtual Machine Contributor.</span></span>

![图中列出了不同的内置角色和自定义角色, 并在参与者角色的定义上进行了放大。](../media/2-rbac-role-definition.png)

<span data-ttu-id="6f00e-134">Azure 包括几个您可以使用的内置角色。</span><span class="sxs-lookup"><span data-stu-id="6f00e-134">Azure includes several built-in roles that you can use.</span></span> <span data-ttu-id="6f00e-135">下面列出了四个基本的内置角色:</span><span class="sxs-lookup"><span data-stu-id="6f00e-135">The following lists four fundamental built-in roles:</span></span>

- <span data-ttu-id="6f00e-136">Owner-具有对所有资源的完全访问权限, 包括向他人委派访问权限的权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-136">Owner - Has full access to all resources, including the right to delegate access to others.</span></span>
- <span data-ttu-id="6f00e-137">投稿人-可以创建和管理所有类型的 Azure 资源, 但不能向其他人授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-137">Contributor - Can create and manage all types of Azure resources, but can’t grant access to others.</span></span>
- <span data-ttu-id="6f00e-138">Reader-可以查看现有 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="6f00e-138">Reader - Can view existing Azure resources.</span></span>
- <span data-ttu-id="6f00e-139">用户访问管理员-允许您管理对 Azure 资源的用户访问。</span><span class="sxs-lookup"><span data-stu-id="6f00e-139">User Access Administrator - Lets you manage user access to Azure resources.</span></span>

<span data-ttu-id="6f00e-140">如果内置角色无法满足组织的特定需求, 您可以创建自己的自定义角色。</span><span class="sxs-lookup"><span data-stu-id="6f00e-140">If the built-in roles don't meet the specific needs of your organization, you can create your own custom roles.</span></span>

### <a name="3-scope-where"></a><span data-ttu-id="6f00e-141">3. Scope (其中)</span><span class="sxs-lookup"><span data-stu-id="6f00e-141">3. Scope (where)</span></span>

<span data-ttu-id="6f00e-142">*作用域*是指应用访问的位置。</span><span class="sxs-lookup"><span data-stu-id="6f00e-142">*Scope* is where the access applies to.</span></span> <span data-ttu-id="6f00e-143">如果您想让某人成为网站参与者, 但只针对一个资源组, 这将非常有用。</span><span class="sxs-lookup"><span data-stu-id="6f00e-143">This is helpful if you want to make someone a Website Contributor, but only for one resource group.</span></span>

<span data-ttu-id="6f00e-144">在 Azure 中, 可以在多个级别指定作用域: 管理组、订阅、资源组或资源。</span><span class="sxs-lookup"><span data-stu-id="6f00e-144">In Azure, you can specify a scope at multiple levels: management group, subscription, resource group, or resource.</span></span> <span data-ttu-id="6f00e-145">作用域在父-子关系中的结构。</span><span class="sxs-lookup"><span data-stu-id="6f00e-145">Scopes are structured in a parent-child relationship.</span></span> <span data-ttu-id="6f00e-146">当您在父作用域中授予访问权限时, 这些权限将由子作用域继承。</span><span class="sxs-lookup"><span data-stu-id="6f00e-146">When you grant access at a parent scope, those permissions are inherited by the child scopes.</span></span> <span data-ttu-id="6f00e-147">例如, 如果在订阅范围将参与者角色分配给一个组, 则该角色将由订阅中的所有资源组和资源继承。</span><span class="sxs-lookup"><span data-stu-id="6f00e-147">For example, if you assign the Contributor role to a group at the subscription scope, that role is inherited by all resource groups and resources in the subscription.</span></span>

![图中显示了要应用范围的不同 Azure 级别的层次结构表示形式。](../media/2-rbac-scope.png)

### <a name="role-assignment"></a><span data-ttu-id="6f00e-150">角色分配</span><span class="sxs-lookup"><span data-stu-id="6f00e-150">Role assignment</span></span>

<span data-ttu-id="6f00e-151">确定了用户、内容和位置之后, 可以将这些元素组合在一起, 以授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-151">Once you have determined the who, what, and where, you can combine those elements to grant access.</span></span> <span data-ttu-id="6f00e-152">*角色分配*是将角色绑定到特定作用域上的安全主体的过程, 目的是为了授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-152">A *role assignment* is the process of binding a role to a security principal at a particular scope, for the purpose of granting access.</span></span> <span data-ttu-id="6f00e-153">若要授予访问权限, 请创建角色分配。</span><span class="sxs-lookup"><span data-stu-id="6f00e-153">To grant access, you create a role assignment.</span></span> <span data-ttu-id="6f00e-154">若要撤消访问权限, 请删除角色分配。</span><span class="sxs-lookup"><span data-stu-id="6f00e-154">To revoke access, you remove a role assignment.</span></span>

<span data-ttu-id="6f00e-155">下面的示例演示如何为市场营销组分配 "销售资源" 组作用域的 "参与者" 角色。</span><span class="sxs-lookup"><span data-stu-id="6f00e-155">The following example shows how the Marketing group has been assigned the Contributor role at the sales resource group scope.</span></span>

![该图显示了市场营销组的示例角色分配过程, 它是安全主体、角色定义和范围的组合。](../media/2-rbac-overview.png)

## <a name="rbac-is-an-allow-model"></a><span data-ttu-id="6f00e-158">RBAC 是允许模型</span><span class="sxs-lookup"><span data-stu-id="6f00e-158">RBAC is an allow model</span></span>

<span data-ttu-id="6f00e-159">RBAC 是一个允许模型。</span><span class="sxs-lookup"><span data-stu-id="6f00e-159">RBAC is an allow model.</span></span> <span data-ttu-id="6f00e-160">这意味着, 在分配角色时, RBAC 允许您执行某些操作, 例如读取、写入或删除。</span><span class="sxs-lookup"><span data-stu-id="6f00e-160">What this means is that when you are assigned a role, RBAC allows you to perform certain actions, such as read, write, or delete.</span></span> <span data-ttu-id="6f00e-161">因此, 如果一个角色分配授予您对资源组的读取权限, 而另一个角色分配授予您对同一资源组的写入权限, 则您将拥有对该资源组的写入权限。</span><span class="sxs-lookup"><span data-stu-id="6f00e-161">So, if one role assignment grants you read permissions to a resource group and a different role assignment grants you write permissions to the same resource group, you will have write permissions on that resource group.</span></span>

<span data-ttu-id="6f00e-162">RBAC 有一些称为`NotActions` "权限" 的内容。</span><span class="sxs-lookup"><span data-stu-id="6f00e-162">RBAC has something called `NotActions` permissions.</span></span> <span data-ttu-id="6f00e-163">`NotActions`不是拒绝规则–它只是在需要排除特定权限时创建一组允许的权限的简便方法。</span><span class="sxs-lookup"><span data-stu-id="6f00e-163">`NotActions` is not a deny rule – it is simply a convenient way to create a set of allowed permissions when specific permissions need to be excluded.</span></span>

<span data-ttu-id="6f00e-164">在此单元中, 你学习了 RBAC 的工作原理的基础知识。</span><span class="sxs-lookup"><span data-stu-id="6f00e-164">In this unit, you learned the basics of how RBAC works.</span></span> <span data-ttu-id="6f00e-165">现在, 您已经了解了 RBAC 基础知识, 您可以通过开始使用 rbac 来获得您的手脏。</span><span class="sxs-lookup"><span data-stu-id="6f00e-165">Now that you have the RBAC fundamentals out of the way, you can get your hands dirty by starting to use RBAC.</span></span> <span data-ttu-id="6f00e-166">开始使用的最简单的方法是使用 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="6f00e-166">The easiest way to get started is to use the Azure portal.</span></span> <span data-ttu-id="6f00e-167">本模块的其余部分将为你执行与 RBAC 相关的实践练习。</span><span class="sxs-lookup"><span data-stu-id="6f00e-167">The rest of this module has you perform hands-on exercises related to RBAC.</span></span>