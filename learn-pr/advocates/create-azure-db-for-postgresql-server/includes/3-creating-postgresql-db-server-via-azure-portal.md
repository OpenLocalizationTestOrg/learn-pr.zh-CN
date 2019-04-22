<span data-ttu-id="85ef3-101">假设您当前正在使用灵活的数据类型和地理空间支持的本地 PostgreSQL 关系数据库。</span><span class="sxs-lookup"><span data-stu-id="85ef3-101">Let's assume that you're currently using an on-premises PostgreSQL relational database using flexible data types and geospatial support.</span></span> <span data-ttu-id="85ef3-102">您的公司正在寻找扩展, 这需要数据库进行扩展。</span><span class="sxs-lookup"><span data-stu-id="85ef3-102">Your company is looking at expanding, which requires the database to scale.</span></span> <span data-ttu-id="85ef3-103">作为额外硬件投资的替代方案, 您需要找到最佳的云托管数据库服务。</span><span class="sxs-lookup"><span data-stu-id="85ef3-103">As an alternative to investing in additional hardware, you're tasked with finding an optimal cloud-hosted database offering.</span></span> <span data-ttu-id="85ef3-104">您已决定对 PostgreSQL 服务器使用 Azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="85ef3-104">You've decided to use an Azure Database for PostgreSQL server.</span></span>

## <a name="what-is-an-azure-database-for-postgresql-server"></a><span data-ttu-id="85ef3-105">什么是 PostgreSQL 服务器的 Azure 数据库？</span><span class="sxs-lookup"><span data-stu-id="85ef3-105">What is an Azure Database for PostgreSQL server?</span></span>

<span data-ttu-id="85ef3-106">PostgreSQL 服务器是一个或多个数据库的中心管理点。</span><span class="sxs-lookup"><span data-stu-id="85ef3-106">The PostgreSQL server is a central administration point for one or more databases.</span></span> <span data-ttu-id="85ef3-107">Azure 中的 PostgreSQL 服务是一种可提供性能保证的托管资源, 它提供了服务器级别的访问和功能。</span><span class="sxs-lookup"><span data-stu-id="85ef3-107">The PostgreSQL service in Azure is a managed resource that provides performance guarantees, and provides access and features at the server level.</span></span>

<span data-ttu-id="85ef3-108">PostgreSQL server 的**Azure 数据库**是数据库的父_资源_。</span><span class="sxs-lookup"><span data-stu-id="85ef3-108">An **Azure Database for PostgreSQL** server is the parent _resource_ for a database.</span></span> <span data-ttu-id="85ef3-109">_资源_是通过 Azure 提供的可管理项。</span><span class="sxs-lookup"><span data-stu-id="85ef3-109">A _resource_ is a manageable item that's available through Azure.</span></span> <span data-ttu-id="85ef3-110">通过创建此资源, 您可以配置服务器实例。</span><span class="sxs-lookup"><span data-stu-id="85ef3-110">Creating this resource allows you to configure your server instance.</span></span>

### <a name="what-is-an-azure-database-for-postgresql-server-resource"></a><span data-ttu-id="85ef3-111">什么是 PostgreSQL 服务器资源的 Azure 数据库？</span><span class="sxs-lookup"><span data-stu-id="85ef3-111">What is an Azure Database for PostgreSQL server resource?</span></span>

<span data-ttu-id="85ef3-112">PostgreSQL server 资源的 Azure 数据库是对服务器和数据库具有极高生存期影响的容器。</span><span class="sxs-lookup"><span data-stu-id="85ef3-112">An Azure Database for PostgreSQL server resource is a container with strong lifetime implications for your server and databases.</span></span> <span data-ttu-id="85ef3-113">如果删除了服务器资源, 则还会删除所有数据库。</span><span class="sxs-lookup"><span data-stu-id="85ef3-113">If the server resource is deleted, all databases are also deleted.</span></span> <span data-ttu-id="85ef3-114">请注意, 属于父代的所有资源都托管在同一个区域中。</span><span class="sxs-lookup"><span data-stu-id="85ef3-114">Keep in mind that all resources belonging to the parent are hosted in the same region.</span></span>

<span data-ttu-id="85ef3-115">服务器资源名称用于定义服务器终结点名称。</span><span class="sxs-lookup"><span data-stu-id="85ef3-115">The server resource name is used to define the server endpoint name.</span></span> <span data-ttu-id="85ef3-116">例如, 如果资源名称为**mypgsqlserver**, 则服务器名称将变为**mypgsqlserver.postgres.database.azure.com**。</span><span class="sxs-lookup"><span data-stu-id="85ef3-116">For example, if the resource name is **mypgsqlserver**, then the server name becomes **mypgsqlserver.postgres.database.azure.com**.</span></span>

<span data-ttu-id="85ef3-117">服务器资源还为应用到其数据库的管理策略提供__连接作用域__。</span><span class="sxs-lookup"><span data-stu-id="85ef3-117">The server resource also provides the __connection scope__ for management policies that apply to its database.</span></span> <span data-ttu-id="85ef3-118">例如: 登录、防火墙、用户、角色和配置。</span><span class="sxs-lookup"><span data-stu-id="85ef3-118">For example: login, firewall, users, roles, and configuration.</span></span>

<span data-ttu-id="85ef3-119">就像 PostgreSQL 的开放源代码版本一样, 服务器可在多个版本中使用, 并允许安装扩展。</span><span class="sxs-lookup"><span data-stu-id="85ef3-119">Just like the open-source version of PostgreSQL, the server is available in several versions and allows for the installation of extensions.</span></span> <span data-ttu-id="85ef3-120">你将选择要安装的服务器版本。</span><span class="sxs-lookup"><span data-stu-id="85ef3-120">You'll choose which server version to install.</span></span>

> [!NOTE]
> <span data-ttu-id="85ef3-121">扩展允许将多个 SQL 对象捆绑在一起, 在可以使用单个命令加载或删除的单个包中。</span><span class="sxs-lookup"><span data-stu-id="85ef3-121">Extensions allow for bundling multiple SQL objects together in a single package that can be loaded or removed with a single command.</span></span> <span data-ttu-id="85ef3-122">扩展的一个示例是`chkpass`, 它提供自动加密密码的数据类型。</span><span class="sxs-lookup"><span data-stu-id="85ef3-122">An example of an extension is `chkpass`, which provides a data type for auto-encrypted passwords.</span></span>

## <a name="pricing-tiers"></a><span data-ttu-id="85ef3-123">定价层</span><span class="sxs-lookup"><span data-stu-id="85ef3-123">Pricing tiers</span></span>

<span data-ttu-id="85ef3-124">PostgreSQL 的 Azure 数据库提供了根据参数 (如计算功率和存储) 选择定价层的选项。</span><span class="sxs-lookup"><span data-stu-id="85ef3-124">Azure Database for PostgreSQL provides you with the option to choose pricing tiers based on parameters like compute power and storage.</span></span> <span data-ttu-id="85ef3-125">有关更多详细信息, 请参阅[Azure Database for PostgreSQL 定价层](https://docs.microsoft.com/azure/postgresql/concepts-pricing-tiers?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="85ef3-125">For more details, see [Azure Database for PostgreSQL pricing tiers](https://docs.microsoft.com/azure/postgresql/concepts-pricing-tiers?azure-portal=true).</span></span>

## <a name="steps-to-create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="85ef3-126">为 PostgreSQL 服务器创建 Azure 数据库的步骤</span><span class="sxs-lookup"><span data-stu-id="85ef3-126">Steps to create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="85ef3-127">通常, 您将使用 azure 门户为 PostgreSQL 服务器创建 azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="85ef3-127">You'll typically create an Azure Database for PostgreSQL server using the Azure portal.</span></span> <span data-ttu-id="85ef3-128">我们来看看您需要执行的步骤。</span><span class="sxs-lookup"><span data-stu-id="85ef3-128">Let's look at the steps you'd take.</span></span> <span data-ttu-id="85ef3-129">这不是一个练习, 但如果选择使用 Azure 门户, 则可以熟悉这些步骤。</span><span class="sxs-lookup"><span data-stu-id="85ef3-129">This is not an exercise, but serves to familiarize you with the steps if you choose to use the Azure portal.</span></span>

<span data-ttu-id="85ef3-130">首先, 你将登录到 Azure 门户, 然后单击 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="85ef3-130">First, you'll sign in to the Azure portal, and then you'll click **Create a resource**.</span></span>

<span data-ttu-id="85ef3-131">您将选择 PostgreSQL 的**数据库**和**Azure 数据库**。</span><span class="sxs-lookup"><span data-stu-id="85ef3-131">You'll select **Databases** and **Azure Database for PostgreSQL**.</span></span> <span data-ttu-id="85ef3-132">您还可以使用**搜索**功能查找此类别。</span><span class="sxs-lookup"><span data-stu-id="85ef3-132">You can also use the **Search** functionality to find this category.</span></span>

<span data-ttu-id="85ef3-133">门户将显示 "PostgreSQL 服务器配置" 屏幕 (也称为 "边栏"), 并进行选择。</span><span class="sxs-lookup"><span data-stu-id="85ef3-133">The portal will display a PostgreSQL server configuration screen, also called a blade, and you make your selection.</span></span>

<span data-ttu-id="85ef3-134">您需要为刀片中的所有项目提供值, 因此, 让我们看一下每个项目。</span><span class="sxs-lookup"><span data-stu-id="85ef3-134">You'll need to give a value to all the items in the blade, so let's have a look at each.</span></span>

### <a name="server-name"></a><span data-ttu-id="85ef3-135">服务器名称</span><span class="sxs-lookup"><span data-stu-id="85ef3-135">Server name</span></span>

<span data-ttu-id="85ef3-136">之前我们提到过, 您将创建服务器资源。</span><span class="sxs-lookup"><span data-stu-id="85ef3-136">Earlier we mentioned that you'll create a server resource.</span></span> <span data-ttu-id="85ef3-137">服务器名称是指定该资源的项。</span><span class="sxs-lookup"><span data-stu-id="85ef3-137">The server name is the item that specifies this resource.</span></span> <span data-ttu-id="85ef3-138">因此, 您必须为服务器选择唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="85ef3-138">As a result, you'll have to choose a unique name for the server.</span></span> <span data-ttu-id="85ef3-139">服务器名称必须全部为小写字母, 并且可以包含数字和连字符。</span><span class="sxs-lookup"><span data-stu-id="85ef3-139">The server name must be all lowercase and can have numbers and hyphens.</span></span>

<span data-ttu-id="85ef3-140">假设您要为服务器_艾德公司的工作跟踪_命名。</span><span class="sxs-lookup"><span data-stu-id="85ef3-140">Let's say you want to name the server _Adventure Works Tracking_.</span></span> <span data-ttu-id="85ef3-141">然后, 将 "名称" 设置为`adventure-works-tracking`。</span><span class="sxs-lookup"><span data-stu-id="85ef3-141">You would then set up the name as `adventure-works-tracking`.</span></span> <span data-ttu-id="85ef3-142">如果尝试使用已经存在的名称创建服务器, 则会对此产生错误。</span><span class="sxs-lookup"><span data-stu-id="85ef3-142">If you try to create a server with a name that already exists, you'll get an error to that effect.</span></span>

### <a name="subscription"></a><span data-ttu-id="85ef3-143">订购</span><span class="sxs-lookup"><span data-stu-id="85ef3-143">Subscription</span></span>

<span data-ttu-id="85ef3-144">"订阅" 字段用于帐单。</span><span class="sxs-lookup"><span data-stu-id="85ef3-144">The subscription field is used for billing.</span></span> <span data-ttu-id="85ef3-145">如果你有多个订阅, 你将选择特定订阅。</span><span class="sxs-lookup"><span data-stu-id="85ef3-145">You'll pick a specific subscription in case you have more than one subscription available.</span></span>

### <a name="resource-group"></a><span data-ttu-id="85ef3-146">资源组</span><span class="sxs-lookup"><span data-stu-id="85ef3-146">Resource group</span></span>

<span data-ttu-id="85ef3-147">您将使用资源组来管理与服务器相关的所有资源。</span><span class="sxs-lookup"><span data-stu-id="85ef3-147">You'll use a resource group to manage all the resources related to your server.</span></span> <span data-ttu-id="85ef3-148">您可以创建新的资源组或重用现有的资源组。</span><span class="sxs-lookup"><span data-stu-id="85ef3-148">You can create a new resource group or reuse an existing resource group.</span></span>

### <a name="source"></a><span data-ttu-id="85ef3-149">源</span><span class="sxs-lookup"><span data-stu-id="85ef3-149">Source</span></span>

<span data-ttu-id="85ef3-150">您可以通过选择_空白_默认选项或现有备份来从头开始创建服务器。</span><span class="sxs-lookup"><span data-stu-id="85ef3-150">You can create a server either from scratch by choosing the _Blank_ default option or from an existing backup.</span></span> <span data-ttu-id="85ef3-151">**备份**选项将为您提供恢复 PostgreSQL 服务器现有 Azure 数据库的地域备份的机会。</span><span class="sxs-lookup"><span data-stu-id="85ef3-151">The **Backup** option will give you the opportunity restore a geo-backup of an existing Azure Database for PostgreSQL server.</span></span>

### <a name="server-admin-login-name"></a><span data-ttu-id="85ef3-152">服务器管理员登录名</span><span class="sxs-lookup"><span data-stu-id="85ef3-152">Server admin login name</span></span>

<span data-ttu-id="85ef3-153">创建服务器管理员用户。</span><span class="sxs-lookup"><span data-stu-id="85ef3-153">You create the server admin user.</span></span> <span data-ttu-id="85ef3-154">选择要用作新服务器的管理员登录名的登录名。</span><span class="sxs-lookup"><span data-stu-id="85ef3-154">Choose a login name to use as an administrator login for the new server.</span></span> <span data-ttu-id="85ef3-155">管理员登录名不能为 azure_superuser、azure_pg_admin、admin、administrator、root、guest 或 public。</span><span class="sxs-lookup"><span data-stu-id="85ef3-155">The admin login name can't be azure_superuser, azure_pg_admin, admin, administrator, root, guest, or public.</span></span> <span data-ttu-id="85ef3-156">它不能以 pg_ 开头。</span><span class="sxs-lookup"><span data-stu-id="85ef3-156">It can't start with pg_.</span></span> <span data-ttu-id="85ef3-157">请记住或记下此名称以供将来使用。</span><span class="sxs-lookup"><span data-stu-id="85ef3-157">Remember or write down this name for future use.</span></span>

### <a name="password"></a><span data-ttu-id="85ef3-158">Password</span><span class="sxs-lookup"><span data-stu-id="85ef3-158">Password</span></span>

<span data-ttu-id="85ef3-159">选择与上述管理员登录名一起使用的密码。</span><span class="sxs-lookup"><span data-stu-id="85ef3-159">You choose a password to use with the above administrator login name.</span></span> <span data-ttu-id="85ef3-160">您的密码必须包含以下三种类别中的字符:</span><span class="sxs-lookup"><span data-stu-id="85ef3-160">Your password must include characters from three of the following categories:</span></span>

- <span data-ttu-id="85ef3-161">英文大写字母</span><span class="sxs-lookup"><span data-stu-id="85ef3-161">English uppercase letters</span></span>
- <span data-ttu-id="85ef3-162">英文小写字母</span><span class="sxs-lookup"><span data-stu-id="85ef3-162">English lowercase letters</span></span>
- <span data-ttu-id="85ef3-163">数字 (0 到 9)</span><span class="sxs-lookup"><span data-stu-id="85ef3-163">Numbers (0 through 9)</span></span>
- <span data-ttu-id="85ef3-164">非字母数字字符 (!、$、#、% 等)</span><span class="sxs-lookup"><span data-stu-id="85ef3-164">Non-alphanumeric characters (!, $, #, %, and so on)</span></span>

<span data-ttu-id="85ef3-165">请记住或记下此密码以供将来使用。</span><span class="sxs-lookup"><span data-stu-id="85ef3-165">Remember or write down this password for future use.</span></span>

### <a name="confirm-password"></a><span data-ttu-id="85ef3-166">确认密码</span><span class="sxs-lookup"><span data-stu-id="85ef3-166">Confirm password</span></span>

<span data-ttu-id="85ef3-167">重新键入密码进行确认。</span><span class="sxs-lookup"><span data-stu-id="85ef3-167">Retype the password to confirmation.</span></span>

### <a name="location"></a><span data-ttu-id="85ef3-168">位置</span><span class="sxs-lookup"><span data-stu-id="85ef3-168">Location</span></span>

<span data-ttu-id="85ef3-169">"位置" 选项允许您指定在物理上创建服务器的位置。</span><span class="sxs-lookup"><span data-stu-id="85ef3-169">The location option allows you to specify where the server is created physically.</span></span> <span data-ttu-id="85ef3-170">选择离你最近的地理位置。</span><span class="sxs-lookup"><span data-stu-id="85ef3-170">Choose the geographic location closest to you.</span></span> <span data-ttu-id="85ef3-171">在实际方案中, 该位置应是最接近用户大部分的位置。</span><span class="sxs-lookup"><span data-stu-id="85ef3-171">In a real-world scenario, the location should be the location closest to the majority of your users.</span></span>

### <a name="version"></a><span data-ttu-id="85ef3-172">Version</span><span class="sxs-lookup"><span data-stu-id="85ef3-172">Version</span></span>

<span data-ttu-id="85ef3-173">您可以指定要使用的 PostgreSQL 版本。</span><span class="sxs-lookup"><span data-stu-id="85ef3-173">You can specify the version of PostgreSQL to use.</span></span> <span data-ttu-id="85ef3-174">Microsoft 旨在支持当前版本和两个早期版本的 PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="85ef3-174">Microsoft aims to support the current version and two previous versions of PostgreSQL.</span></span> <span data-ttu-id="85ef3-175">你将选择与你的生产环境相匹配的版本。</span><span class="sxs-lookup"><span data-stu-id="85ef3-175">You'll choose a version that matches your production environment.</span></span>

> [!NOTE]
> <span data-ttu-id="85ef3-176">有关详细信息, 请参阅以下资源:</span><span class="sxs-lookup"><span data-stu-id="85ef3-176">For more information, see the following sources:</span></span>
> - [<span data-ttu-id="85ef3-177">支持的 PostgreSQL 数据库版本</span><span class="sxs-lookup"><span data-stu-id="85ef3-177">Supported PostgreSQL database versions</span></span>](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions?azure-portal=true)
> - [<span data-ttu-id="85ef3-178">版本控制策略</span><span class="sxs-lookup"><span data-stu-id="85ef3-178">Versioning policy</span></span>](https://www.postgresql.org/support/versioning/?azure-portal=true)

### <a name="pricing-tier"></a><span data-ttu-id="85ef3-179">定价层</span><span class="sxs-lookup"><span data-stu-id="85ef3-179">Pricing tier</span></span>

<span data-ttu-id="85ef3-180">你将选择支持你的服务器工作负载的定价层。</span><span class="sxs-lookup"><span data-stu-id="85ef3-180">You'll choose a pricing tier that will support your server's workload.</span></span> <span data-ttu-id="85ef3-181">请记住, 您有不同的层可供选择。</span><span class="sxs-lookup"><span data-stu-id="85ef3-181">Recall that you have different tiers to choose from.</span></span> <span data-ttu-id="85ef3-182">如前文所述, 这些层中的每一层都允许您配置计算和存储选项。</span><span class="sxs-lookup"><span data-stu-id="85ef3-182">As we saw earlier, each of these tiers allows you to configure the compute and storage options.</span></span> 

<span data-ttu-id="85ef3-183">现在, 剩下的只是查看您输入的值, 以后您可能需要的任何说明, 然后单击 "**创建**" 以创建服务器。</span><span class="sxs-lookup"><span data-stu-id="85ef3-183">All that's left now is to review the values that you entered, make any notes you may need for later, and click **Create** to create the server.</span></span>

<span data-ttu-id="85ef3-184">部署服务器需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="85ef3-184">Deploying the server takes a couple of minutes.</span></span> <span data-ttu-id="85ef3-185">部署完成后, 你将收到通知。</span><span class="sxs-lookup"><span data-stu-id="85ef3-185">You'll receive a notification when the deployment is complete.</span></span> <span data-ttu-id="85ef3-186">从通知中, 您可以导航到新创建的服务器。</span><span class="sxs-lookup"><span data-stu-id="85ef3-186">From the notification, you can navigate to the newly created server.</span></span>

