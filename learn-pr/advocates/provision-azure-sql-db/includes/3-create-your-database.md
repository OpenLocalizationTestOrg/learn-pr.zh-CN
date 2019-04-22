<span data-ttu-id="22ff8-101">您的运输公司想要将其设置为与其他公司分开, 但不会损坏银行。</span><span class="sxs-lookup"><span data-stu-id="22ff8-101">Your transportation company wants to set themselves apart from other companies but without breaking the bank.</span></span> <span data-ttu-id="22ff8-102">您必须有一个很好的句柄来设置数据库, 以提供最佳服务, 同时控制成本。</span><span class="sxs-lookup"><span data-stu-id="22ff8-102">You must have a good handle on how to set up the database to provide the best service while controlling costs.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="22ff8-103">在这里, 你将了解:</span><span class="sxs-lookup"><span data-stu-id="22ff8-103">Here, you'll learn:</span></span>

- <span data-ttu-id="22ff8-104">创建 Azure SQL 数据库时需要考虑的注意事项, 其中包括:</span><span class="sxs-lookup"><span data-stu-id="22ff8-104">What considerations you need to make when creating an Azure SQL database, including:</span></span>
  - <span data-ttu-id="22ff8-105">逻辑服务器如何充当数据库的管理容器。</span><span class="sxs-lookup"><span data-stu-id="22ff8-105">How a logical server acts as an administrative container for your databases.</span></span>
  - <span data-ttu-id="22ff8-106">采购模型之间的差异。</span><span class="sxs-lookup"><span data-stu-id="22ff8-106">The differences between purchasing models.</span></span>
  - <span data-ttu-id="22ff8-107">弹性池如何使您能够在数据库之间共享处理能力。</span><span class="sxs-lookup"><span data-stu-id="22ff8-107">How elastic pools enable you to share processing power among databases.</span></span>
  - <span data-ttu-id="22ff8-108">排序规则如何影响数据的比较和排序方式。</span><span class="sxs-lookup"><span data-stu-id="22ff8-108">How collation rules affect how data is compared and sorted.</span></span>
- <span data-ttu-id="22ff8-109">如何从门户中引入 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-109">How to bring up Azure SQL Database from the portal.</span></span>
- <span data-ttu-id="22ff8-110">如何添加防火墙规则, 以便仅可从受信任的源访问数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-110">How to add firewall rules so that your database is accessible from only trusted sources.</span></span>

<span data-ttu-id="22ff8-111">让我们快速看一下创建 Azure SQL 数据库时需要考虑的一些事项。</span><span class="sxs-lookup"><span data-stu-id="22ff8-111">Let's take a quick look at some things you need to consider when you create an Azure SQL database.</span></span>

## <a name="one-server-many-databases"></a><span data-ttu-id="22ff8-112">一台服务器, 多个数据库</span><span class="sxs-lookup"><span data-stu-id="22ff8-112">One server, many databases</span></span>

<span data-ttu-id="22ff8-113">当您创建第一个 azure sql 数据库时, 还会创建一个_azure sql 逻辑服务器_。</span><span class="sxs-lookup"><span data-stu-id="22ff8-113">When you create your first Azure SQL database, you also create an _Azure SQL logical server_.</span></span> <span data-ttu-id="22ff8-114">将逻辑服务器视为数据库的管理容器。</span><span class="sxs-lookup"><span data-stu-id="22ff8-114">Think of a logical server as an administrative container for your databases.</span></span> <span data-ttu-id="22ff8-115">您可以通过逻辑服务器控制登录、防火墙规则和安全策略。</span><span class="sxs-lookup"><span data-stu-id="22ff8-115">You can control logins, firewall rules, and security policies through the logical server.</span></span> <span data-ttu-id="22ff8-116">您还可以在逻辑服务器中的每个数据库上覆盖这些策略。</span><span class="sxs-lookup"><span data-stu-id="22ff8-116">You can also override these policies on each database within the logical server.</span></span>

<span data-ttu-id="22ff8-117">目前, 只需要一个数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-117">For now, you need just one database.</span></span> <span data-ttu-id="22ff8-118">但逻辑服务器使您能够在更高的更高版本中添加更多和优化所有数据库的性能。</span><span class="sxs-lookup"><span data-stu-id="22ff8-118">But a logical server enables you to add more later and tune performance among all your databases.</span></span>

## <a name="choose-performance-dtus-versus-vcores"></a><span data-ttu-id="22ff8-119">选择性能: dtu 和 vCores</span><span class="sxs-lookup"><span data-stu-id="22ff8-119">Choose performance: DTUs versus vCores</span></span>

<span data-ttu-id="22ff8-120">Azure SQL 数据库有两个购买模型: DTU 和 vCore。</span><span class="sxs-lookup"><span data-stu-id="22ff8-120">Azure SQL Database has two purchasing models: DTU and vCore.</span></span>

### <a name="what-are-dtus"></a><span data-ttu-id="22ff8-121">什么是 dtu？</span><span class="sxs-lookup"><span data-stu-id="22ff8-121">What are DTUs?</span></span>

<span data-ttu-id="22ff8-122">DTU 代表数据库事务单元, 是计算、存储和 IO 资源的组合指标。</span><span class="sxs-lookup"><span data-stu-id="22ff8-122">DTU stands for Database Transaction Unit and is a combined measure of compute, storage, and IO resources.</span></span> <span data-ttu-id="22ff8-123">将 DTU 模型视为一个简单的预配置的 "购买" 选项。</span><span class="sxs-lookup"><span data-stu-id="22ff8-123">Think of the DTU model as a simple, preconfigured purchase option.</span></span>

<span data-ttu-id="22ff8-124">由于您的逻辑服务器可以包含多个数据库, 因此也有 eDTUs 或弹性数据库事务单元的概念。</span><span class="sxs-lookup"><span data-stu-id="22ff8-124">Because your logical server can hold more than one database, there's also the idea of eDTUs, or elastic Database Transaction Units.</span></span> <span data-ttu-id="22ff8-125">此选项使您能够选择一个价格, 但允许池中的每个数据库消耗较少或更多的资源, 具体取决于当前负载。</span><span class="sxs-lookup"><span data-stu-id="22ff8-125">This option enables you to choose one price, but allow each database in the pool to consume fewer or greater resources depending on current load.</span></span>

### <a name="what-are-vcores"></a><span data-ttu-id="22ff8-126">什么是 vCores？</span><span class="sxs-lookup"><span data-stu-id="22ff8-126">What are vCores?</span></span>

<span data-ttu-id="22ff8-127">vCore 使您可以更好地控制您为其创建和支付的计算和存储资源。</span><span class="sxs-lookup"><span data-stu-id="22ff8-127">vCore gives you greater control over what compute and storage resources you create and pay for.</span></span>

<span data-ttu-id="22ff8-128">当 DTU 模型提供计算、存储和 IO 资源的固定组合时, vCore 模型使您能够单独配置资源。</span><span class="sxs-lookup"><span data-stu-id="22ff8-128">While the DTU model provides fixed combinations of compute, storage, and IO resources, the vCore model enables you to configure resources independently.</span></span> <span data-ttu-id="22ff8-129">例如, 使用 vCore 模型, 可以增加存储容量, 但可以保留现有的计算量和 IO 吞吐量。</span><span class="sxs-lookup"><span data-stu-id="22ff8-129">For example, with the vCore model you can increase storage capacity but keep the existing amount of compute and IO throughput.</span></span>

<span data-ttu-id="22ff8-130">您的运输和物流原型只需要一个 Azure SQL 数据库实例。</span><span class="sxs-lookup"><span data-stu-id="22ff8-130">Your transportation and logistics prototype only needs one Azure SQL Database instance.</span></span> <span data-ttu-id="22ff8-131">你可以决定使用 DTU 选项, 因为它能为计算、存储和 IO 性能提供很好的平衡, 并且入门成本较低。</span><span class="sxs-lookup"><span data-stu-id="22ff8-131">You decide on the DTU option because it provides a good balance of compute, storage, and IO performance and is less expensive to get started.</span></span>

## <a name="what-are-sql-elastic-pools"></a><span data-ttu-id="22ff8-132">什么是 SQL 弹性池？</span><span class="sxs-lookup"><span data-stu-id="22ff8-132">What are SQL elastic pools?</span></span>

<span data-ttu-id="22ff8-133">创建 Azure sql 数据库时, 可以创建_SQL 弹性池_。</span><span class="sxs-lookup"><span data-stu-id="22ff8-133">When you create your Azure SQL database, you can create a _SQL elastic pool_.</span></span>

<span data-ttu-id="22ff8-134">SQL 弹性池与 eDTUs 相关。</span><span class="sxs-lookup"><span data-stu-id="22ff8-134">SQL elastic pools relate to eDTUs.</span></span> <span data-ttu-id="22ff8-135">它们使您能够购买在池中的所有数据库之间共享的一组计算和存储资源。</span><span class="sxs-lookup"><span data-stu-id="22ff8-135">They enable you to buy a set of compute and storage resources that are shared among all the databases in the pool.</span></span> <span data-ttu-id="22ff8-136">每个数据库都可以使用所需的资源, 在设置的限制内, 具体取决于当前负载。</span><span class="sxs-lookup"><span data-stu-id="22ff8-136">Each database can use the resources they need, within the limits you set, depending on current load.</span></span>

<span data-ttu-id="22ff8-137">对于原型, 不需要 sql 弹性池, 因为只需要一个 sql 数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-137">For your prototype, you won't need a SQL elastic pool because you need only one SQL database.</span></span>

## <a name="what-is-collation"></a><span data-ttu-id="22ff8-138">排序规则是什么？</span><span class="sxs-lookup"><span data-stu-id="22ff8-138">What is collation?</span></span>

<span data-ttu-id="22ff8-139">排序规则是指对数据进行排序和比较的规则。</span><span class="sxs-lookup"><span data-stu-id="22ff8-139">Collation refers to the rules that sort and compare data.</span></span> <span data-ttu-id="22ff8-140">当区分大小写、重音标记和其他语言特征很重要时, 排序规则可帮助您定义排序规则。</span><span class="sxs-lookup"><span data-stu-id="22ff8-140">Collation helps you define sorting rules when case sensitivity, accent marks, and other language characteristics are important.</span></span>

<span data-ttu-id="22ff8-141">现在, 我们来思考一下默认的排序规则 ( **SQL_Latin1_General_CP1_CI_AS**) 的含义。</span><span class="sxs-lookup"><span data-stu-id="22ff8-141">Let's take a moment to consider what the default collation, **SQL_Latin1_General_CP1_CI_AS**, means.</span></span>

- <span data-ttu-id="22ff8-142">**Latin1_General**是指西方欧洲语言系列。</span><span class="sxs-lookup"><span data-stu-id="22ff8-142">**Latin1_General** refers to the family of Western European languages.</span></span>
- <span data-ttu-id="22ff8-143">**CP1**是指代码页 1252, 即拉丁字母的常见字符编码。</span><span class="sxs-lookup"><span data-stu-id="22ff8-143">**CP1** refers to code page 1252, a popular character encoding of the Latin alphabet.</span></span>
- <span data-ttu-id="22ff8-144">**CI**意味着比较不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="22ff8-144">**CI** means that comparisons are case insensitive.</span></span> <span data-ttu-id="22ff8-145">例如, "hello" 与 "hello" 比较相等。</span><span class="sxs-lookup"><span data-stu-id="22ff8-145">For example, "HELLO" compares equally to "hello".</span></span>
- <span data-ttu-id="22ff8-146">**这**意味着比较区分重音。</span><span class="sxs-lookup"><span data-stu-id="22ff8-146">**AS** means that comparisons are accent sensitive.</span></span> <span data-ttu-id="22ff8-147">例如, "简历" 不会平均比较为 "resume"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-147">For example, "résumé" doesn't compare equally to "resume".</span></span>

<span data-ttu-id="22ff8-148">由于在如何对数据进行排序和比较方面没有具体的要求, 因此, 您可以选择默认的排序规则。</span><span class="sxs-lookup"><span data-stu-id="22ff8-148">Because you don't have specific requirements around how data is sorted and compared, you choose the default collation.</span></span>

## <a name="create-your-azure-sql-database"></a><span data-ttu-id="22ff8-149">创建 Azure SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="22ff8-149">Create your Azure SQL database</span></span>

<span data-ttu-id="22ff8-150">在这里, 你将设置数据库, 其中包括创建逻辑服务器。</span><span class="sxs-lookup"><span data-stu-id="22ff8-150">Here you'll set up your database, which includes creating your logical server.</span></span> <span data-ttu-id="22ff8-151">您将选择支持您的运输物流应用程序的设置。</span><span class="sxs-lookup"><span data-stu-id="22ff8-151">You'll choose settings that support your transportation logistics application.</span></span> <span data-ttu-id="22ff8-152">在实践中, 您将选择支持您正在构建的应用程序类型的设置。</span><span class="sxs-lookup"><span data-stu-id="22ff8-152">In practice, you would choose settings that support the kind of app you're building.</span></span>

<span data-ttu-id="22ff8-153">随着时间的推移, 如果您意识到需要额外的计算能力来满足需求, 则可以调整性能选项, 甚至可以在 DTU 和 vCore 性能模型之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="22ff8-153">Over time if you realize you need additional compute power to keep up with demand, you can adjust performance options or even switch between the DTU and vCore performance models.</span></span>

1. <span data-ttu-id="22ff8-154">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="22ff8-154">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="22ff8-155">从门户中, 单击 "从左上角**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-155">From the portal, click **Create a resource** from the upper left-hand corner.</span></span> <span data-ttu-id="22ff8-156">选择 "**数据库**", 然后选择 " **SQL 数据库**"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-156">Select **Databases**, then select **SQL Database**.</span></span>

   ![显示 "创建具有所选数据库的资源边栏" 部分并突出显示 "创建资源"、"数据库" 和 "SQL 数据库" 按钮的 Azure 门户屏幕截图。](../media/3-create-db.png)

1. <span data-ttu-id="22ff8-158">在 "**服务器**" 下, 单击 "**配置必需设置**", 填写表单, 然后单击 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-158">Under **Server**, click **Configure required settings**, fill out the form, then click **Select**.</span></span> <span data-ttu-id="22ff8-159">以下是有关如何填写表单的详细信息:</span><span class="sxs-lookup"><span data-stu-id="22ff8-159">Here's more information on how to fill out the form:</span></span>

    | <span data-ttu-id="22ff8-160">设置</span><span class="sxs-lookup"><span data-stu-id="22ff8-160">Setting</span></span>      | <span data-ttu-id="22ff8-161">值</span><span class="sxs-lookup"><span data-stu-id="22ff8-161">Value</span></span> |
    | ------------ | ----- |
    | <span data-ttu-id="22ff8-162">**服务器名称**</span><span class="sxs-lookup"><span data-stu-id="22ff8-162">**Server name**</span></span> | <span data-ttu-id="22ff8-163">一个全局唯一的[服务器名称](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。</span><span class="sxs-lookup"><span data-stu-id="22ff8-163">A globally unique [server name](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
    | <span data-ttu-id="22ff8-164">**服务器管理员登录**</span><span class="sxs-lookup"><span data-stu-id="22ff8-164">**Server admin login**</span></span> | <span data-ttu-id="22ff8-165">充当主管理员登录名的[数据库标识符](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。</span><span class="sxs-lookup"><span data-stu-id="22ff8-165">A [database identifier](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) that serves as your primary administrator login name.</span></span> |
    | <span data-ttu-id="22ff8-166">**Password**</span><span class="sxs-lookup"><span data-stu-id="22ff8-166">**Password**</span></span> | <span data-ttu-id="22ff8-167">至少包含八个字符并包含三个类别中的字符的任何有效密码: 大写字符、小写字符、数字和非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="22ff8-167">Any valid password that has at least eight characters and contains characters from three of these categories: uppercase characters, lowercase characters, numbers, and non-alphanumeric characters.</span></span> |
    | <span data-ttu-id="22ff8-168">**Location**</span><span class="sxs-lookup"><span data-stu-id="22ff8-168">**Location**</span></span> | <span data-ttu-id="22ff8-169">下面可用列表中的任何有效位置。</span><span class="sxs-lookup"><span data-stu-id="22ff8-169">Any valid location from the available list below.</span></span> |

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="22ff8-170">单击 "**定价层**" 以指定服务层。</span><span class="sxs-lookup"><span data-stu-id="22ff8-170">Click **Pricing tier** to specify the service tier.</span></span> <span data-ttu-id="22ff8-171">选择 "**基本**服务层", 然后单击 "**应用**"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-171">Select the **Basic** service tier, then click **Apply**.</span></span>

1. <span data-ttu-id="22ff8-172">使用这些值来填写表单的其余部分。</span><span class="sxs-lookup"><span data-stu-id="22ff8-172">Use these values to fill out the rest of the form.</span></span>

    | <span data-ttu-id="22ff8-173">设置</span><span class="sxs-lookup"><span data-stu-id="22ff8-173">Setting</span></span>      | <span data-ttu-id="22ff8-174">值</span><span class="sxs-lookup"><span data-stu-id="22ff8-174">Value</span></span> |
    | ------------ | ----- |
    | <span data-ttu-id="22ff8-175">**数据库名称**</span><span class="sxs-lookup"><span data-stu-id="22ff8-175">**Database name**</span></span> | <span data-ttu-id="22ff8-176">**事务**</span><span class="sxs-lookup"><span data-stu-id="22ff8-176">**Logistics**</span></span> |
    | <span data-ttu-id="22ff8-177">**订购**</span><span class="sxs-lookup"><span data-stu-id="22ff8-177">**Subscription**</span></span> | <span data-ttu-id="22ff8-178">你的订阅</span><span class="sxs-lookup"><span data-stu-id="22ff8-178">Your subscription</span></span> |
    | <span data-ttu-id="22ff8-179">**资源组**</span><span class="sxs-lookup"><span data-stu-id="22ff8-179">**Resource group**</span></span> | <span data-ttu-id="22ff8-180"> 使用现有组<rgn>[沙盒资源组名称]</rgn></span><span class="sxs-lookup"><span data-stu-id="22ff8-180"> Use the existing group <rgn>[sandbox resource group name]</rgn></span></span> |
    | <span data-ttu-id="22ff8-181">**选择源**</span><span class="sxs-lookup"><span data-stu-id="22ff8-181">**Select source**</span></span> | <span data-ttu-id="22ff8-182">**空数据库**</span><span class="sxs-lookup"><span data-stu-id="22ff8-182">**Blank database**</span></span> |
    | <span data-ttu-id="22ff8-183">**想要使用 SQL 弹性池吗？**</span><span class="sxs-lookup"><span data-stu-id="22ff8-183">**Want to use SQL elastic pool?**</span></span> | <span data-ttu-id="22ff8-184">**不是现在**</span><span class="sxs-lookup"><span data-stu-id="22ff8-184">**Not now**</span></span> |
    | <span data-ttu-id="22ff8-185">**排序**</span><span class="sxs-lookup"><span data-stu-id="22ff8-185">**Collation**</span></span> | <span data-ttu-id="22ff8-186">**SQL_Latin1_General_CP1_CI_AS**</span><span class="sxs-lookup"><span data-stu-id="22ff8-186">**SQL_Latin1_General_CP1_CI_AS**</span></span> |

1. <span data-ttu-id="22ff8-187">单击 "**创建**" 以创建 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-187">Click **Create** to create your Azure SQL database.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="22ff8-188">稍后请记住您的服务器名称、管理员登录名和密码。</span><span class="sxs-lookup"><span data-stu-id="22ff8-188">Remember your server name, admin login, and password for later.</span></span>

1. <span data-ttu-id="22ff8-189">在工具栏上, 单击 "**通知**" 以监视部署过程。</span><span class="sxs-lookup"><span data-stu-id="22ff8-189">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

<span data-ttu-id="22ff8-190">在此过程完成后, 单击 "**固定到仪表板**" 将数据库服务器固定到仪表板, 以便您可以在以后需要时快速访问。</span><span class="sxs-lookup"><span data-stu-id="22ff8-190">When the process completes, click **Pin to dashboard** to pin your database server to the dashboard so that you have quick access when you need it later.</span></span>

   ![显示 "通知" 菜单的 Azure 门户屏幕截图, 其中突出显示了最近一次部署成功消息中的 "Pin 到仪表板" 按钮。](../media/3-notifications-complete.png)

## <a name="set-the-server-firewall"></a><span data-ttu-id="22ff8-192">设置服务器防火墙</span><span class="sxs-lookup"><span data-stu-id="22ff8-192">Set the server firewall</span></span>

<span data-ttu-id="22ff8-193">你的 Azure SQL 数据库现已启动并正在运行。</span><span class="sxs-lookup"><span data-stu-id="22ff8-193">Your Azure SQL database is now up and running.</span></span> <span data-ttu-id="22ff8-194">您可以通过多种方式来进一步配置、保护、监视和排除新数据库的故障。</span><span class="sxs-lookup"><span data-stu-id="22ff8-194">You have many options to further configure, secure, monitor, and troubleshoot your new database.</span></span>

<span data-ttu-id="22ff8-195">您还可以指定哪些系统可以通过防火墙访问您的数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-195">You can also specify which systems can access your database through the firewall.</span></span> <span data-ttu-id="22ff8-196">最初, 防火墙会阻止从 Azure 外部访问您的数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="22ff8-196">Initially, the firewall prevents all access to your database server from outside of Azure.</span></span>

<span data-ttu-id="22ff8-197">对于原型, 只需从便携式计算机访问数据库即可。</span><span class="sxs-lookup"><span data-stu-id="22ff8-197">For your prototype, you only need to access the database from your laptop.</span></span> <span data-ttu-id="22ff8-198">稍后, 您可以对其他系统 (如移动应用程序) 进行白名单。</span><span class="sxs-lookup"><span data-stu-id="22ff8-198">Later, you can whitelist additional systems, such as your mobile app.</span></span>

<span data-ttu-id="22ff8-199">让你的开发计算机立即通过防火墙访问数据库。</span><span class="sxs-lookup"><span data-stu-id="22ff8-199">Let's enable your development computer to access the database through the firewall now.</span></span>

1. <span data-ttu-id="22ff8-200">转到后勤数据库的概述边栏。</span><span class="sxs-lookup"><span data-stu-id="22ff8-200">Go to the overview blade of the Logistics database.</span></span> <span data-ttu-id="22ff8-201">如果先前已固定数据库, 则可以单击仪表板上的**物流**磁贴以转到此处。</span><span class="sxs-lookup"><span data-stu-id="22ff8-201">If you pinned the database earlier, you can click the **Logistics** tile on the dashboard to get there.</span></span>

1. <span data-ttu-id="22ff8-202">单击 "**设置服务器防火墙**"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-202">Click **Set server firewall**.</span></span>

    ![显示 SQL 数据库概述刀片的 Azure 门户屏幕截图, 其中突出显示了 "设置服务器防火墙" 按钮。](../media/3-set-server-firewall.png)

1. <span data-ttu-id="22ff8-204">单击 "**添加客户端 IP**"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-204">Click **Add client IP**.</span></span>

    ![显示 SQL 数据库防火墙设置刀片的 Azure 门户屏幕截图, 其中突出显示了 "添加客户端 IP" 按钮。](../media/3-add-client-ip.png)

1. <span data-ttu-id="22ff8-206">单击"保存"。</span><span class="sxs-lookup"><span data-stu-id="22ff8-206">Click **Save**.</span></span>

<span data-ttu-id="22ff8-207">在下一部分中, 你将通过新数据库和 Azure 云命令行管理程序实现一些实际操作实践。</span><span class="sxs-lookup"><span data-stu-id="22ff8-207">In the next part, you'll get some hands-on practice with your new database and with Azure Cloud Shell.</span></span> <span data-ttu-id="22ff8-208">您将连接到数据库, 创建一个表, 添加一些示例数据, 并执行几个 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="22ff8-208">You'll connect to the database, create a table, add some sample data, and execute a few SQL statements.</span></span>