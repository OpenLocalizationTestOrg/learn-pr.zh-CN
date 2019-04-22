<span data-ttu-id="e48d1-101">用户将连接到应用程序服务器, 以输入订单、更新其帐户并执行类似活动, 这将使用这些更改来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-101">Users will connect to our app server to enter orders, update their account, and perform similar activities, which will in turn update the database with these changes.</span></span> <span data-ttu-id="e48d1-102">由于我们在数据库中存储了个人数据, 因此确保仅允许来自受信任的和必要的资源的访问至关重要。</span><span class="sxs-lookup"><span data-stu-id="e48d1-102">Because we have personal data stored in the database it's critical to ensure that we only allow access from trusted and necessary resources.</span></span> <span data-ttu-id="e48d1-103">让我们来看一看通过网络控制对 SQL 数据库的访问的多种方法。</span><span class="sxs-lookup"><span data-stu-id="e48d1-103">Let's take a look at a number of ways you can control access to your SQL database over the network.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="e48d1-104">防火墙规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-104">Firewall rules</span></span>

<span data-ttu-id="e48d1-105">Azure SQL 数据库具有内置防火墙, 用于允许和拒绝对数据库服务器本身以及各个数据库的网络访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-105">Azure SQL Database has a built-in firewall that is used to allow and deny network access to both the database server itself, as well as individual databases.</span></span> <span data-ttu-id="e48d1-106">防火墙规则是在服务器和/或数据库级别配置的, 将明确声明允许哪些网络资源建立与数据库的连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-106">Firewall rules are configured at the server and/or database level, and will specifically state which network resources are allowed to establish a connection to the database.</span></span> <span data-ttu-id="e48d1-107">根据级别的不同, 您可以应用的规则如下所示:</span><span class="sxs-lookup"><span data-stu-id="e48d1-107">Depending on the level, the rules you can apply will be as follows:</span></span>

- <span data-ttu-id="e48d1-108">**服务器级别的防火墙规则**</span><span class="sxs-lookup"><span data-stu-id="e48d1-108">**Server-level firewall rules**</span></span>
  - <span data-ttu-id="e48d1-109">允许访问 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="e48d1-109">Allow access to Azure services</span></span>
  - <span data-ttu-id="e48d1-110">IP 地址规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-110">IP address rules</span></span>
  - <span data-ttu-id="e48d1-111">虚拟网络规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-111">Virtual network rules</span></span>
- <span data-ttu-id="e48d1-112">**数据库级别的防火墙规则**</span><span class="sxs-lookup"><span data-stu-id="e48d1-112">**Database-level firewall rules**</span></span>
  - <span data-ttu-id="e48d1-113">IP 地址规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-113">IP address rules</span></span>

<span data-ttu-id="e48d1-114">让我们进一步了解这些规则的工作原理。</span><span class="sxs-lookup"><span data-stu-id="e48d1-114">Let's take a closer look at how these rules work.</span></span>

### <a name="server-level-firewall-rules"></a><span data-ttu-id="e48d1-115">服务器级别的防火墙规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-115">Server-level firewall rules</span></span>

<span data-ttu-id="e48d1-116">这些规则使客户端可以访问您的整个 Azure SQL server, 即同一逻辑服务器中的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-116">These rules enable clients to access your entire Azure SQL server, that is, all the databases within the same logical server.</span></span> <span data-ttu-id="e48d1-117">可以在服务器级别应用以下三种类型的规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-117">There are three types of rules that can be applied at the server level.</span></span>

<span data-ttu-id="e48d1-118">"**允许访问 azure 服务**" 规则允许 azure 中的服务连接到 azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-118">The **Allow access to Azure services** rule allows services within Azure to connect to your Azure SQL Database.</span></span> <span data-ttu-id="e48d1-119">如果启用此设置, 则允许来自所有 Azure 公用 IP 地址的通信。</span><span class="sxs-lookup"><span data-stu-id="e48d1-119">When enabled, this setting allows communications from all Azure public IP addresses.</span></span> <span data-ttu-id="e48d1-120">这包括所有 azure 平台作为服务 (PaaS) 服务 (如 azure 应用服务和 azure 容器服务) 以及具有出站 internet 访问权限的 azure vm。</span><span class="sxs-lookup"><span data-stu-id="e48d1-120">This includes all Azure Platform as a Service (PaaS) services, such as Azure App Service and Azure Container Service, as well as Azure VMs that have outbound internet access.</span></span> <span data-ttu-id="e48d1-121">可以通过门户的 "防火墙" 窗格中的 "**开/关**" 选项或将0.0.0.0 作为开始和结束 ip 地址的 IP 规则配置此规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-121">This rule can be configured through the **ON/OFF** option in the firewall pane in the portal, or by an IP rule that has 0.0.0.0 as the start and end IP addresses.</span></span>

![允许访问 Azure 服务网络图](../media/2-allow-azure-services.png)

<span data-ttu-id="e48d1-123">当您的应用程序在 azure 中的 PaaS 服务 (如 azure 逻辑应用或 azure 函数) 中运行时, 需要访问 azure SQL 数据库, 则使用此规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-123">This rule is used when you have applications running on PaaS services in Azure, such as Azure Logic Apps or Azure Functions, that need to access your Azure SQL Database.</span></span> <span data-ttu-id="e48d1-124">其中许多服务没有静态 IP 地址, 因此需要此规则以确保它们能够连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-124">Many of these services don't have a static IP address, so this rule is needed to ensure they are able to connect to the database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e48d1-125">此选项将防火墙配置为允许来自 Azure 的所有连接, 包括来自其他客户的订阅的连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-125">This option configures the firewall to allow all connections from Azure including connections from the subscriptions of other customers.</span></span> <span data-ttu-id="e48d1-126">选择此选项时, 请确保您的登录和用户权限仅限制授权用户访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-126">When selecting this option, make sure your login and user permissions limit access to only authorized users.</span></span>

<span data-ttu-id="e48d1-127">**IP 地址规则**是基于特定公用 IP 地址范围的规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-127">**IP address rules** are rules that are based on specific public IP address ranges.</span></span> <span data-ttu-id="e48d1-128">将允许从允许的公共 IP 范围连接的 IP 地址连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-128">IP addresses connecting from an allowed public IP range will be permitted to connect to the database.</span></span>

![IP 地址规则网络图](../media/2-server-ip-rule-1.png)

<span data-ttu-id="e48d1-130">当您有需要访问您的数据库的静态公共 IP 地址时, 可以使用这些规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-130">These rules can be used when you have a static public IP address that needs to access your database.</span></span>

<span data-ttu-id="e48d1-131">**虚拟网络规则**允许你显式允许一个或多个 Azure 虚拟网络 (vnet) 内的指定子网中的连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-131">**Virtual network rules** allow you to explicitly allow connection from specified subnets inside one or more Azure virtual networks (VNets).</span></span> <span data-ttu-id="e48d1-132">虚拟网络规则可以对数据库提供更大的访问控制, 并且可以是首选选项, 具体取决于您的应用场景。</span><span class="sxs-lookup"><span data-stu-id="e48d1-132">Virtual network rules can provide greater access control to your databases and can be a preferred option depending on your scenario.</span></span> <span data-ttu-id="e48d1-133">由于 Azure VNet 地址空间是专用的, 因此您可以有效消除对公用 IP 地址的暴露和与您控制的那些地址的安全连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-133">Since Azure VNet address spaces are private, you can effectively eliminate exposure to public IP addresses and secure connectivity to those addresses you control.</span></span>

![VNet 规则网络图](../media/2-vnet-rule.png)

<span data-ttu-id="e48d1-135">当您的 Azure vm 需要访问您的数据库时, 将使用虚拟网络规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-135">Virtual network rules are used when you have Azure VMs that need to access your database.</span></span>

<span data-ttu-id="e48d1-136">对于服务器级别的规则, 可以通过门户、PowerShell、CLI 和 transact-sql (t-sql) 来创建和操作上述所有项。</span><span class="sxs-lookup"><span data-stu-id="e48d1-136">For server-level rules, all of the above can be created and manipulated through the portal, PowerShell, the CLI and through Transact-SQL (T-SQL).</span></span>

### <a name="database-level-firewall-rules"></a><span data-ttu-id="e48d1-137">数据库级别的防火墙规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-137">Database-level firewall rules</span></span>

<span data-ttu-id="e48d1-138">这些规则允许访问逻辑服务器上的单个数据库, 并存储在数据库本身中。</span><span class="sxs-lookup"><span data-stu-id="e48d1-138">These rules allow access to an individual database on a logical server and are stored in the database itself.</span></span> <span data-ttu-id="e48d1-139">对于数据库级别的规则, 只能配置**IP 地址规则**。</span><span class="sxs-lookup"><span data-stu-id="e48d1-139">For database-level rules, only **IP address rules** can be configured.</span></span> <span data-ttu-id="e48d1-140">它们的工作方式与在服务器级别应用时相同, 但范围仅限于数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-140">They function the same as when applied at the server-level, but are scoped to the database only.</span></span>

![数据库 IP 地址规则网络图](../media/2-db-ip-rule-1.png)

<span data-ttu-id="e48d1-142">数据库级规则的优势在于它们的可移植性。</span><span class="sxs-lookup"><span data-stu-id="e48d1-142">The benefits of database-level rules are their portability.</span></span> <span data-ttu-id="e48d1-143">将数据库复制到另一台服务器时, 数据库级别的规则将被复制, 因为它们存储在数据库本身中。</span><span class="sxs-lookup"><span data-stu-id="e48d1-143">When replicating a database to another server, the database-level rules will be replicated, since they are stored in the database itself.</span></span>

<span data-ttu-id="e48d1-144">数据库级规则的缺点是, 只能使用 IP 地址规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-144">The downside to database-level rules is that you can only use IP address rules.</span></span> <span data-ttu-id="e48d1-145">这可能会限制你拥有的灵活性, 并可能会增加管理开销。</span><span class="sxs-lookup"><span data-stu-id="e48d1-145">This may limit the flexibility you have and can increase administrative overhead.</span></span>

<span data-ttu-id="e48d1-146">最后, 只能通过 t-sql 创建和处理数据库级别的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-146">Lastly, database-level firewall rules can be created and manipulated only through T-SQL.</span></span>

## <a name="restricting-network-access-in-practice"></a><span data-ttu-id="e48d1-147">在实践中限制网络访问</span><span class="sxs-lookup"><span data-stu-id="e48d1-147">Restricting network access in practice</span></span>

<span data-ttu-id="e48d1-148">我们来看看这些工作在实践中的工作方式, 以及如何确保网络访问只允许必要。</span><span class="sxs-lookup"><span data-stu-id="e48d1-148">Let's take a look at how these work in practice, and how you can secure network access to only allow what is necessary.</span></span> <span data-ttu-id="e48d1-149">请记住, 我们创建了一个 Azure SQL 数据库逻辑服务器、一个数据库和一个作为应用程序服务器的_appServer_ Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="e48d1-149">Recall that we created an Azure SQL Database logical server, a database, and the _appServer_ Linux VM acting as an application server.</span></span> <span data-ttu-id="e48d1-150">当数据库迁移到 Azure SQL 数据库, 并且虚拟网络内部的资源需要访问它时, 通常会出现此情况。</span><span class="sxs-lookup"><span data-stu-id="e48d1-150">This scenario is often seen when a database has been migrated to Azure SQL Database and resources inside of a virtual network need to access it.</span></span> <span data-ttu-id="e48d1-151">Azure SQL Database 的防火墙功能可在许多方案中使用, 但这是一个具有实用适用性的示例, 并说明了每个规则的工作方式。</span><span class="sxs-lookup"><span data-stu-id="e48d1-151">The firewall feature of Azure SQL Database can be used in many scenarios, but this is an example that has practical applicability and demonstrates how each of the rules functions.</span></span>

<span data-ttu-id="e48d1-152">我们来看一下防火墙设置, 并查看它们的工作方式。</span><span class="sxs-lookup"><span data-stu-id="e48d1-152">Let's go through the firewall settings and see how they work.</span></span> <span data-ttu-id="e48d1-153">我们将使用云命令行管理程序和门户来实现这些练习。</span><span class="sxs-lookup"><span data-stu-id="e48d1-153">We'll use both the cloud shell and the portal for these exercises.</span></span>

<span data-ttu-id="e48d1-154">我们创建的数据库当前不允许从任何连接进行访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-154">The database we created currently does not allow access from any connections.</span></span> <span data-ttu-id="e48d1-155">这是根据我们为创建逻辑服务器和数据库而运行的命令设计的。</span><span class="sxs-lookup"><span data-stu-id="e48d1-155">This is by design based on the commands that we ran to create the logical server and database.</span></span> <span data-ttu-id="e48d1-156">让我们对此进行确认。</span><span class="sxs-lookup"><span data-stu-id="e48d1-156">Let's confirm this.</span></span>

1. <span data-ttu-id="e48d1-157">如果尚未连接, 则在云命令行管理程序中, SSH 加入你的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="e48d1-157">In the cloud shell, SSH into your Linux VM if you aren't already connected.</span></span>

    ```bash
    ssh <X.X.X.X>
    ```

1. <span data-ttu-id="e48d1-158">撤回我们`sqlcmd`之前检索的命令。</span><span class="sxs-lookup"><span data-stu-id="e48d1-158">Recall the `sqlcmd` command we retrieved earlier.</span></span> <span data-ttu-id="e48d1-159">继续执行并运行它以尝试连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-159">Go ahead and run it to attempt to connect to the database.</span></span> <span data-ttu-id="e48d1-160">请确保将和`<username>` `<password>`替换为您`ADMINUSER`在上一个设备中指定的凭据。</span><span class="sxs-lookup"><span data-stu-id="e48d1-160">Make sure you replace `<username>` and `<password>` with the `ADMINUSER` credentials you specified in the previous unit.</span></span> <span data-ttu-id="e48d1-161">请务必在用户名和密码周围保留单引号, 以便命令行管理程序不会错误地误解任何特殊字符。</span><span class="sxs-lookup"><span data-stu-id="e48d1-161">Make sure to keep the single quotes around the username and password so that any special characters aren't misinterpreted by the shell.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    <span data-ttu-id="e48d1-162">尝试连接时, 应会收到错误。</span><span class="sxs-lookup"><span data-stu-id="e48d1-162">You should receive an error when trying to connect.</span></span> <span data-ttu-id="e48d1-163">这是预期的原因, 因为我们不允许对数据库进行任何访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-163">This is expected since we've not allowed any access to the database.</span></span>

    ```output
    Sqlcmd: Error: Microsoft ODBC Driver 17 for SQL Server : Cannot open server 'securedb' requested by the login. Client with IP address '40.112.128.214' is not allowed to access the server.  To enable access, use the Windows Azure Management Portal or run sp_set_firewall_rule on the master database to create a firewall rule for this IP address or address range.  It may take up to five minutes for this change to take effect..
    ```

<span data-ttu-id="e48d1-164">让我们授予访问权限, 以便我们可以连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-164">Let's grant access so we can connect.</span></span>

### <a name="use-the-server-level-allow-access-to-azure-services-rule"></a><span data-ttu-id="e48d1-165">使用服务器级别的允许访问 Azure 服务规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-165">Use the server-level allow access to Azure services rule</span></span>

<span data-ttu-id="e48d1-166">由于我们的 VM 具有出站 internet 访问权限, 因此我们可以使用 "**允许访问 Azure 服务**" 规则来允许从我们的虚拟机访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-166">Since our VM has outbound internet access, we can use the **Allow access to Azure services** rule to allow access from our VM.</span></span>

1. <span data-ttu-id="e48d1-167">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="e48d1-167">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="e48d1-168">在顶部的 "**搜索资源、服务和文档**" 框中, 搜索您的数据库服务器名称`server<12345>`。</span><span class="sxs-lookup"><span data-stu-id="e48d1-168">In the **Search resources, services, and docs** box at the top, search for your database server name, `server<12345>`.</span></span> <span data-ttu-id="e48d1-169">选择 SQL server。</span><span class="sxs-lookup"><span data-stu-id="e48d1-169">Select the SQL server.</span></span>

1. <span data-ttu-id="e48d1-170">在 "SQL server" 面板中, 在左侧菜单的 "**安全性**" 部分, 选择 "**防火墙和虚拟网络**"。</span><span class="sxs-lookup"><span data-stu-id="e48d1-170">In the SQL server panel, in the **Security** section in the left menu, select **Firewalls and virtual networks**.</span></span>

1. <span data-ttu-id="e48d1-171">将 "**允许访问 Azure 服务**" 设置为 **"打开"** , 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="e48d1-171">Set **Allow access to Azure services** to **ON** and click **Save**.</span></span>

1. <span data-ttu-id="e48d1-172">回到 SSH 会话中, 让我们再次尝试连接到您的数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-172">Back in your SSH session, let's try to connect to your database again.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    <span data-ttu-id="e48d1-173">此时, 您应能够连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-173">At this point, you should be able to connect.</span></span> <span data-ttu-id="e48d1-174">如果成功, 您应该会看到 sqlcmd 提示。</span><span class="sxs-lookup"><span data-stu-id="e48d1-174">If it's successful, you should see a sqlcmd prompt.</span></span>

    ```sql
    1>
    ```

<span data-ttu-id="e48d1-175">因此, 我们打开了连接, 但此设置当前允许从_任何_Azure 资源 (包括我们的订阅之外的资源) 访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-175">So we've opened up connectivity, but this setting currently allows access from _any_ Azure resource, including resources outside of our subscription.</span></span> <span data-ttu-id="e48d1-176">让我们进一步限制此限制, 将网络访问限制为仅限控制范围内的资源。</span><span class="sxs-lookup"><span data-stu-id="e48d1-176">Let's restrict this further to limit network access to only resources that are within our control.</span></span>

### <a name="use-a-database-level-ip-address-rule"></a><span data-ttu-id="e48d1-177">使用数据库级别的 IP 地址规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-177">Use a database-level IP address rule</span></span>

<span data-ttu-id="e48d1-178">回想一下, 数据库级别的 IP 地址规则仅允许对逻辑服务器上的单个数据库的访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-178">Recall that database-level IP address rules allow only access to an individual database on a logical server.</span></span> <span data-ttu-id="e48d1-179">我们将在此处使用一个, 以向我们的_appServer_ VM 的静态 IP 授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="e48d1-179">We'll use one here to grant access to the static IP of our _appServer_ VM.</span></span>

<span data-ttu-id="e48d1-180">若要创建数据库级 IP 规则, 我们需要运行一些 t-sql 命令。</span><span class="sxs-lookup"><span data-stu-id="e48d1-180">To create a database-level IP rule, we'll need to run some T-SQL commands.</span></span> <span data-ttu-id="e48d1-181">您将使用以下约定创建数据库规则, 在该规则中传递规则名称、起始 ip 地址和结束 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="e48d1-181">You'll create a database rule using the following convention, where you pass in the rule name, the starting IP address, and the ending IP address.</span></span> <span data-ttu-id="e48d1-182">通过将起始和结束 IP 指定为相同, 我们将限制对单个 ip 的访问, 但如果我们有更大的地址块需要访问, 我们可以扩展该范围。</span><span class="sxs-lookup"><span data-stu-id="e48d1-182">By specifying the start and end IP to be the same, we're limiting access to a single IP, though we could expand the range if we had a larger block of addresses that required access.</span></span>

```sql
EXECUTE sp_set_database_firewall_rule N'My Firewall Rule', '40.112.128.214', '40.112.128.214'
```

1. <span data-ttu-id="e48d1-183">仍在 sqlcmd 提示符处, 运行以下命令, 在下面的两个位置替换您的_appServer_ VM 的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e48d1-183">While still at the sqlcmd prompt, run the following command, replacing the public IP address of your _appServer_ VM in both locations below.</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Allow appServer database level rule', '<From IP Address>', '<To IP Address>';
    GO
    ```

    <span data-ttu-id="e48d1-184">命令完成后, 键入`exit` exit sqlcmd。</span><span class="sxs-lookup"><span data-stu-id="e48d1-184">Once the command completes, type `exit` to exit sqlcmd.</span></span> <span data-ttu-id="e48d1-185">通过 SSH 保持连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-185">Remain connected via SSH.</span></span>

1. <span data-ttu-id="e48d1-186">在门户中, 在您的 SQL server 的 "**防火墙和虚拟网络**" 面板上, 将 "**允许访问 Azure 服务**" 设置为 "**关闭**", 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="e48d1-186">In the portal, on the **Firewalls and virtual networks** panel for your SQL server, set **Allow access to Azure services** to **OFF** and click **Save**.</span></span> <span data-ttu-id="e48d1-187">这将禁用来自所有 Azure 服务的访问, 但我们仍可以连接, 因为我们为我们的服务器提供了数据库级 IP 规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-187">This will disable access from all Azure services, but we'll still be able to connect since we have a database-level IP rule for our server.</span></span>

1. <span data-ttu-id="e48d1-188">在云命令行管理程序中, 在通过 SSH 连接到的 VM 中, 尝试再次连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-188">Back in cloud shell, in the VM you are connected via SSH to, try connecting to your database again.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    <span data-ttu-id="e48d1-189">此时, 您应能够连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-189">At this point, you should be able to connect.</span></span> <span data-ttu-id="e48d1-190">如果成功, 您应该会看到 sqlcmd 提示。</span><span class="sxs-lookup"><span data-stu-id="e48d1-190">If it's successful, you should see a sqlcmd prompt.</span></span>

    ```sql
    1>
    ```

<span data-ttu-id="e48d1-191">通过使用数据库级别的规则, 可以将访问特定于数据库进行隔离。</span><span class="sxs-lookup"><span data-stu-id="e48d1-191">Using a database-level rule allows access to be isolated specifically to the database.</span></span> <span data-ttu-id="e48d1-192">如果你想要为每个数据库配置网络访问, 这会非常有用。</span><span class="sxs-lookup"><span data-stu-id="e48d1-192">This can be useful if you'd like to keep your network access configured per database.</span></span> <span data-ttu-id="e48d1-193">如果多个数据库具有相同级别的网络访问权限, 则可以使用服务器级别的规则对服务器上的所有数据库应用相同的访问权限, 从而简化管理。</span><span class="sxs-lookup"><span data-stu-id="e48d1-193">If multiple databases share the same level of network access, you can simplify administration by using a server-level rule to apply the same access to all databases on the server.</span></span>

#### <a name="use-a-server-level-ip-address-rule"></a><span data-ttu-id="e48d1-194">使用服务器级别的 IP 地址规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-194">Use a server-level IP address rule</span></span>

<span data-ttu-id="e48d1-195">数据库级规则是一个很好的选择, 但如果我们在_appServer_ VM 需要连接到的同一台服务器上有多个数据库, 该怎么办？</span><span class="sxs-lookup"><span data-stu-id="e48d1-195">Database-level rules are a great option, but what if we had multiple databases on the same server that our _appServer_ VM needed to connect to?</span></span> <span data-ttu-id="e48d1-196">我们可以向每个数据库添加数据库级别的规则, 这会在我们添加更多数据库时执行更多的工作。</span><span class="sxs-lookup"><span data-stu-id="e48d1-196">We could add a database-level rule to each database, this can take more work as we add more databases.</span></span> <span data-ttu-id="e48d1-197">它会降低管理工作, 以允许访问服务器级别的规则, 这些规则将应用于服务器上的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-197">It would reduce our administration efforts to allow access with a server-level rule, which would apply to all databases on the server.</span></span>

<span data-ttu-id="e48d1-198">现在, 我们使用服务器级别的 IP 规则来限制可以连接的系统。</span><span class="sxs-lookup"><span data-stu-id="e48d1-198">Let's now use a server-level IP rule to restrict the systems that can connect.</span></span>

1. <span data-ttu-id="e48d1-199">仍在 sqlcmd 提示符处, 运行以下命令以删除数据库级别的 IP 地址规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-199">While still at the sqlcmd prompt, run the following command to delete the database-level IP address rule.</span></span>

    ```sql
    EXECUTE sp_delete_database_firewall_rule N'Allow appServer database level rule';
    GO
    ```

    <span data-ttu-id="e48d1-200">命令完成后, 键入`exit` exit sqlcmd。</span><span class="sxs-lookup"><span data-stu-id="e48d1-200">Once the command completes, type `exit` to exit sqlcmd.</span></span> <span data-ttu-id="e48d1-201">通过 SSH 保持连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-201">Remain connected via SSH.</span></span>

1. <span data-ttu-id="e48d1-202">返回到门户, 在您的 SQL server 的 "**防火墙和虚拟网络**" 面板中, 添加一个新规则, 其中包含**规则名称**"**允许 appServer** ", 并将 "**起始 ip** " 和 "**结束 ip** " 设置为 "appServer" 的公用 IP 地址。 __ VM。</span><span class="sxs-lookup"><span data-stu-id="e48d1-202">Back in the portal, on the **Firewalls and virtual networks** panel for your SQL server,  add a new rule with a **RULE NAME** of **Allow appServer** and with the **START IP** and **END IP** set to the public IP address of the _appServer_ VM.</span></span>

    <span data-ttu-id="e48d1-203">单击 "**保存**"</span><span class="sxs-lookup"><span data-stu-id="e48d1-203">Click **Save**</span></span>

    ![显示已添加的带有所述 IP 限制配置的服务器防火墙规则创建的 Azure 门户屏幕截图。](../media/2-ip-address-rule.png)

1. <span data-ttu-id="e48d1-205">在云命令行管理程序中的_appServer_虚拟机上, 尝试再次连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-205">Back in cloud shell, on your _appServer_ VM, try connecting to your database again.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    <span data-ttu-id="e48d1-206">此时, 您应该能够进行连接, 因为服务器级别规则允许基于_appServer_ VM 的公共 IP 地址进行访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-206">At this point you should be able to connect, since the server-level rule is allowing access based on the public IP address of the _appServer_ VM.</span></span> <span data-ttu-id="e48d1-207">如果成功, 您应该会看到 sqlcmd 提示。</span><span class="sxs-lookup"><span data-stu-id="e48d1-207">If it's successful, you should see a sqlcmd prompt.</span></span>

    ```sql
    1>
    ```

    <span data-ttu-id="e48d1-208">要`exit`退出 sqlcmd 的类型。</span><span class="sxs-lookup"><span data-stu-id="e48d1-208">Type `exit` to exit sqlcmd.</span></span> <span data-ttu-id="e48d1-209">通过 SSH 保持连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-209">Remain connected via SSH.</span></span>

<span data-ttu-id="e48d1-210">因此, 我们已将连接隔离到在规则中指定的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e48d1-210">So we've isolated connectivity to only the IP address we specified in the rule.</span></span> <span data-ttu-id="e48d1-211">这非常有用, 但在添加需要连接的更多系统时仍可能会遇到管理难题。</span><span class="sxs-lookup"><span data-stu-id="e48d1-211">This works great, but can still be an administrative challenge as you add more systems that need to connect.</span></span> <span data-ttu-id="e48d1-212">它还需要来自定义的 ip 地址范围的静态 ip 或 ip。如果 IP 是动态的且发生了更改, 则必须更新规则以确保连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-212">It also requires a static IP or an IP from a defined IP address range; if the IP is dynamic and changes, we'd have to update the rule to ensure connectivity.</span></span> <span data-ttu-id="e48d1-213">_appServer_ VM 当前已配置了动态 IP 地址, 因此此 IP 地址可能在某个时刻发生变化, 并在出现这种情况时中断我们的访问。</span><span class="sxs-lookup"><span data-stu-id="e48d1-213">The _appServer_ VM is currently configured with a dynamic IP address, so this IP address is likely to change at some point, breaking our access as soon as that happens.</span></span> <span data-ttu-id="e48d1-214">现在, 我们来看看虚拟网络规则在我们的配置中是如何有益的。</span><span class="sxs-lookup"><span data-stu-id="e48d1-214">Let's now look at how virtual network rules can be beneficial in our configuration.</span></span>

#### <a name="use-a-server-level-virtual-network-rule"></a><span data-ttu-id="e48d1-215">使用服务器级别的虚拟网络规则</span><span class="sxs-lookup"><span data-stu-id="e48d1-215">Use a server-level virtual network rule</span></span>

<span data-ttu-id="e48d1-216">在这种情况下, 由于我们的 VM 在 Azure 中运行, 因此我们可以使用服务器级别的虚拟网络规则来隔离访问权限, 并使将来的服务能够轻松地获取对数据库的访问权限。</span><span class="sxs-lookup"><span data-stu-id="e48d1-216">In this case, since our VM is running in Azure, we can use a server-level virtual network rule to isolate access and make it easy to enable future services to gain access to the database.</span></span>

1. <span data-ttu-id="e48d1-217">在 "**虚拟网络**" 部分的 "门户" 和 "仍在**防火墙和虚拟网络**" 面板中, 单击 " **+ 添加现有虚拟网络**" 选项。</span><span class="sxs-lookup"><span data-stu-id="e48d1-217">Back in the portal and still on the **Firewalls and virtual networks** panel, in the **Virtual networks** section click the **+ Add existing virtual network** option.</span></span>

1. <span data-ttu-id="e48d1-218">将显示 "创建/更新虚拟网络规则" 对话框。</span><span class="sxs-lookup"><span data-stu-id="e48d1-218">The Create/Update virtual network rule dialog will show.</span></span> <span data-ttu-id="e48d1-219">设置以下值:</span><span class="sxs-lookup"><span data-stu-id="e48d1-219">Set the following values:</span></span>

    | <span data-ttu-id="e48d1-220">_設定_</span><span class="sxs-lookup"><span data-stu-id="e48d1-220">_Setting_</span></span>                        | <span data-ttu-id="e48d1-221">_値_</span><span class="sxs-lookup"><span data-stu-id="e48d1-221">_Value_</span></span>                                  |
    | -------------------------------- | ---------------------------------------- |
    | <span data-ttu-id="e48d1-222">**名称**</span><span class="sxs-lookup"><span data-stu-id="e48d1-222">**Name**</span></span>                         | <span data-ttu-id="e48d1-223">保留默认值</span><span class="sxs-lookup"><span data-stu-id="e48d1-223">Leave the default value</span></span>                  |
    | <span data-ttu-id="e48d1-224">**订购**</span><span class="sxs-lookup"><span data-stu-id="e48d1-224">**Subscription**</span></span>                 | <span data-ttu-id="e48d1-225">Concierge 订阅</span><span class="sxs-lookup"><span data-stu-id="e48d1-225">Concierge Subscription</span></span>                   |
    | <span data-ttu-id="e48d1-226">**虚拟网络**</span><span class="sxs-lookup"><span data-stu-id="e48d1-226">**Virtual network**</span></span>              | <span data-ttu-id="e48d1-227">appServerVNET</span><span class="sxs-lookup"><span data-stu-id="e48d1-227">appServerVNET</span></span>                            |
    | <span data-ttu-id="e48d1-228">**子网名称/地址前缀**</span><span class="sxs-lookup"><span data-stu-id="e48d1-228">**Subnet name / Address prefix**</span></span> | <span data-ttu-id="e48d1-229">appServerSubnet/10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e48d1-229">appServerSubnet / 10.0.0.0/24</span></span>            |

    <span data-ttu-id="e48d1-230">单击 "**启用**" 以启用子网上的服务终结点, 然后在启用终结点以创建规则后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="e48d1-230">Click **Enable** to enable the service endpoint on the subnet, then **OK** once the endpoint is enabled to create the rule.</span></span>

1. <span data-ttu-id="e48d1-231">现在, 让我们删除 IP 地址规则。</span><span class="sxs-lookup"><span data-stu-id="e48d1-231">Now, let's remove the IP address rule.</span></span> <span data-ttu-id="e48d1-232">单击 "**允许 appServer** " 规则旁边的 " **...** ", 然后单击 "**删除**", 然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="e48d1-232">Click the **...** next to your **Allow appServer** rule and click **Delete**, then click **Save**.</span></span>

1. <span data-ttu-id="e48d1-233">在云命令行管理程序中的_appServer_虚拟机上, 尝试再次连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="e48d1-233">Back in cloud shell, on your _appServer_ VM, try connecting to your database again.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U '<username>' -P '<password>' -N -l 30
    ```

    <span data-ttu-id="e48d1-234">此时, 您应能够连接。</span><span class="sxs-lookup"><span data-stu-id="e48d1-234">At this point, you should be able to connect.</span></span> <span data-ttu-id="e48d1-235">如果成功, 您应该会看到 sqlcmd 提示。</span><span class="sxs-lookup"><span data-stu-id="e48d1-235">If it's successful, you should see a sqlcmd prompt.</span></span>

    ```sql
    1>
    ```

<span data-ttu-id="e48d1-236">我们在此处执行的操作将有效地删除对 SQL server 的任何公开访问, 并且仅允许来自我们定义的 Azure VNet 中的特定子网的访问权限。</span><span class="sxs-lookup"><span data-stu-id="e48d1-236">What we've done here effectively removes any public access to the SQL server, and only permits access from the specific subnet in the Azure VNet we defined.</span></span> <span data-ttu-id="e48d1-237">如果要在该子网中添加其他应用程序服务器, 则不需要进行其他配置, 因为该子网中的任何服务器都将能够连接到 SQL server。</span><span class="sxs-lookup"><span data-stu-id="e48d1-237">If we were to add additional app servers in that subnet, no additional configuration would be necessary, as any server in that subnet would have the ability to connect to the SQL server.</span></span> <span data-ttu-id="e48d1-238">这将限制我们对控制范围之外的服务的暴露, 并在我们添加其他服务器时简化管理。</span><span class="sxs-lookup"><span data-stu-id="e48d1-238">This limits our exposure to services outside of our scope of control, and eases administration if we were to add additional servers.</span></span> <span data-ttu-id="e48d1-239">这是保护对 Azure SQL 数据库的网络访问的有效方法。</span><span class="sxs-lookup"><span data-stu-id="e48d1-239">This is an effective method of securing network access to an Azure SQL Database.</span></span>