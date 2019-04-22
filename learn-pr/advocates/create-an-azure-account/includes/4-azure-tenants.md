<span data-ttu-id="989cd-101">如你所见, 你的 azure 帐户是一个全局唯一实体, 可让你访问 Azure 订阅和服务。</span><span class="sxs-lookup"><span data-stu-id="989cd-101">As you've seen, your Azure account is a globally unique entity that gives you access to your Azure subscriptions and services.</span></span> <span data-ttu-id="989cd-102">使用 azure Active Directory (azure AD) 对你的帐户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="989cd-102">Authentication for your account is performed using Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="989cd-103">Azure AD 是一种新式标识提供程序, 它支持多个身份验证协议, 以保护云中的应用程序和服务。</span><span class="sxs-lookup"><span data-stu-id="989cd-103">Azure AD is a modern identity provider that supports multiple authentication protocols to secure applications and services in the cloud.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="989cd-104">Azure AD 与__ Windows Active Directory 不同。</span><span class="sxs-lookup"><span data-stu-id="989cd-104">Azure AD is _not_ the same as Windows Active Directory.</span></span> <span data-ttu-id="989cd-105">windows Active Directory 重点关注 Windows 桌面和服务器的安全。</span><span class="sxs-lookup"><span data-stu-id="989cd-105">Windows Active Directory is focused on securing Windows desktops and servers.</span></span> <span data-ttu-id="989cd-106">相比之下, Azure AD 都是关于基于 web 的身份验证标准 (如 OpenID 和 OAuth) 的。</span><span class="sxs-lookup"><span data-stu-id="989cd-106">In contrast, Azure AD is all about web-based authentication standards such as OpenID and OAuth.</span></span>

<span data-ttu-id="989cd-107">在 Azure AD 中注册的用户、应用程序和其他实体并不都是 lumped 一个全局服务。</span><span class="sxs-lookup"><span data-stu-id="989cd-107">Users, applications, and other entities registered in Azure AD aren't all lumped into a single global service.</span></span> <span data-ttu-id="989cd-108">而是将 Azure AD 划分为单独的_租户_。</span><span class="sxs-lookup"><span data-stu-id="989cd-108">Instead, Azure AD is partitioned into separate _tenants_.</span></span> <span data-ttu-id="989cd-109">租户是一个专用的、独立的 Azure Active Directory 服务实例, 由组织拥有和管理。</span><span class="sxs-lookup"><span data-stu-id="989cd-109">A tenant is a dedicated, isolated instance of the Azure Active Directory service, owned and managed by an organization.</span></span> <span data-ttu-id="989cd-110">当你注册 microsoft 云服务订阅 (如 microsoft Azure、microsoft Intune 或 Office 365) 时, 将自动为你的组织创建 Azure AD 的专用实例。</span><span class="sxs-lookup"><span data-stu-id="989cd-110">When you sign up for a Microsoft cloud service subscription such as Microsoft Azure, Microsoft Intune, or Office 365, a dedicated instance of Azure AD is automatically created for your organization.</span></span>

<span data-ttu-id="989cd-111">当遇到 Azure AD 租户时, 个人、团队、公司或任何其他人员组&mdash;不会拥有 "组织" 租户的具体定义。</span><span class="sxs-lookup"><span data-stu-id="989cd-111">When it comes to Azure AD tenants, there is no concrete definition of "organization" &mdash; tenants can be owned by individuals, teams, companies, or any other group of people.</span></span> <span data-ttu-id="989cd-112">租户通常与公司相关联。</span><span class="sxs-lookup"><span data-stu-id="989cd-112">Tenants are commonly associated with companies.</span></span> <span data-ttu-id="989cd-113">如果使用与现有租户不关联的电子邮件地址注册 Azure, 注册过程将引导您完成创建由您完全拥有的租户的过程。</span><span class="sxs-lookup"><span data-stu-id="989cd-113">If you sign up for Azure with an email address that's not associated with an existing tenant, the sign-up process will walk you through creating a tenant, owned entirely by you.</span></span>

> [!TIP]
> <span data-ttu-id="989cd-114">你用于登录 Azure 的电子邮件地址可与多个租户关联。</span><span class="sxs-lookup"><span data-stu-id="989cd-114">The email address you use to sign in to Azure can be associated with more than one tenant.</span></span> <span data-ttu-id="989cd-115">如果你有 Azure 帐户, 并且使用 Microsoft 学习的 azure 沙盒来完成练习, 你可能会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="989cd-115">You might see this if you have an Azure account and you use Microsoft Learn's Azure Sandbox to complete exercises.</span></span> <span data-ttu-id="989cd-116">在 Azure 门户中, 一次只能查看属于一个租户的资源。</span><span class="sxs-lookup"><span data-stu-id="989cd-116">In the Azure portal, you can only view resources belonging to one tenant at a time.</span></span> <span data-ttu-id="989cd-117">若要切换租户, 请查看门户顶部的 "**书籍和筛选器**" 图标的资源, 并在 "**切换目录**" 部分中选择一个不同的租户。</span><span class="sxs-lookup"><span data-stu-id="989cd-117">To switch the tenant, you're viewing resources for select the **Book and filter** icon at the top of the portal and choose a different tenant in the **Switch directory** section.</span></span>

<span data-ttu-id="989cd-118">Azure AD 租户和订阅具有多对一的信任关系: 租户可与多个 Azure 订阅关联, 但每个订阅仅与一个租户关联。</span><span class="sxs-lookup"><span data-stu-id="989cd-118">Azure AD tenants and subscriptions have a many-to-one trust relationship: A tenant can be associated with multiple Azure subscriptions, but every subscription is associated with only one tenant.</span></span> <span data-ttu-id="989cd-119">此结构允许组织管理多个订阅并在其包含的所有资源中设置安全规则。</span><span class="sxs-lookup"><span data-stu-id="989cd-119">This structure allows organizations to manage multiple subscriptions and set security rules across all the resources contained within them.</span></span>

<span data-ttu-id="989cd-120">下面是有关帐户、订阅、租户和资源如何协同工作的简单表示。</span><span class="sxs-lookup"><span data-stu-id="989cd-120">Here's a simple representation of how accounts, subscriptions, tenants, and resources work together.</span></span>

![显示两个不同的 Azure AD 租户的插图。](../media/4-azure-ad-tenant.png)

<span data-ttu-id="989cd-124">请注意, 每个 Azure AD 租户都有一个_帐户所有者_。</span><span class="sxs-lookup"><span data-stu-id="989cd-124">Notice that each Azure AD tenant has an _account owner_.</span></span> <span data-ttu-id="989cd-125">这是负责计费的原始 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="989cd-125">This is the original Azure account that is responsible for billing.</span></span> <span data-ttu-id="989cd-126">你可以将其他用户添加到租户, 甚至邀请来自其他 Azure AD 租户的来宾访问订阅中的资源。</span><span class="sxs-lookup"><span data-stu-id="989cd-126">You can add additional users to the tenant, and even invite guests from other Azure AD tenants to access resources in subscriptions.</span></span>