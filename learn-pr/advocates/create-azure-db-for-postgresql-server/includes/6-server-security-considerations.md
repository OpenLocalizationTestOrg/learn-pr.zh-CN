<span data-ttu-id="5919a-101">假设你使用的是本地 PostgreSQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="5919a-101">Let's assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="5919a-102">您正在管理所有安全方面, 并且已通过标准 PostgreSQL 服务器级别的防火墙规则锁定了对您的服务器的所有访问。</span><span class="sxs-lookup"><span data-stu-id="5919a-102">You're managing all security aspects and you've locked down all access to your servers using the standard PostgreSQL server-level firewall rules.</span></span> <span data-ttu-id="5919a-103">现在, 您需要确保您可以在 Azure 中配置相同的服务器级别防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-103">Now you want to make sure that you can configure the same server-level firewall rules in Azure.</span></span>

## <a name="server-security-considerations-and-connection-methods"></a><span data-ttu-id="5919a-104">服务器安全注意事项和连接方法</span><span class="sxs-lookup"><span data-stu-id="5919a-104">Server security considerations and connection methods</span></span>

<span data-ttu-id="5919a-105">您可以使用多种方法来限制对 PostgreSQL 服务器和数据库的 Azure 数据库的访问。</span><span class="sxs-lookup"><span data-stu-id="5919a-105">You have a number of options to restrict access to your Azure Database for PostgreSQL server and databases.</span></span> <span data-ttu-id="5919a-106">可以在网络、服务器或数据库级别限制网络访问。</span><span class="sxs-lookup"><span data-stu-id="5919a-106">Network access can be restricted at a network, server, or database level.</span></span> <span data-ttu-id="5919a-107">您可以使用以下任一选项:</span><span class="sxs-lookup"><span data-stu-id="5919a-107">You can use any of the following options:</span></span>

- <span data-ttu-id="5919a-108">限制数据库访问的用户帐户</span><span class="sxs-lookup"><span data-stu-id="5919a-108">User accounts to restrict database access</span></span>
- <span data-ttu-id="5919a-109">用于限制网络访问的虚拟网络</span><span class="sxs-lookup"><span data-stu-id="5919a-109">Virtual networks to restrict network access</span></span>
- <span data-ttu-id="5919a-110">限制服务器访问的防火墙规则</span><span class="sxs-lookup"><span data-stu-id="5919a-110">Firewall rules to restrict server access</span></span>

### <a name="authentication-and-authorization"></a><span data-ttu-id="5919a-111">身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="5919a-111">Authentication and authorization</span></span>

<span data-ttu-id="5919a-112">适用于 PostgreSQL 服务器的 Azure 数据库支持本机 PostgreSQL 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5919a-112">The Azure Database for PostgreSQL server supports native PostgreSQL authentication.</span></span> <span data-ttu-id="5919a-113">您可以通过服务器的管理员登录与服务器进行连接和身份验证。</span><span class="sxs-lookup"><span data-stu-id="5919a-113">You can connect and authenticate to the server with the server's admin login.</span></span> <span data-ttu-id="5919a-114">您还将创建用户以连接到特定数据库来限制访问。</span><span class="sxs-lookup"><span data-stu-id="5919a-114">You'll also create users to connect to specific databases to limit access.</span></span>

### <a name="what-is-a-virtual-network"></a><span data-ttu-id="5919a-115">什么是虚拟网络？</span><span class="sxs-lookup"><span data-stu-id="5919a-115">What is a virtual network?</span></span>

<span data-ttu-id="5919a-116">虚拟网络是在 Azure 网络中创建的逻辑隔离网络。</span><span class="sxs-lookup"><span data-stu-id="5919a-116">A virtual network is a logically isolated network that's created within the Azure network.</span></span> <span data-ttu-id="5919a-117">您可以使用虚拟网络控制哪些 Azure 资源可以连接到其他资源。</span><span class="sxs-lookup"><span data-stu-id="5919a-117">You can use a virtual network to control what Azure resources can connect to other resources.</span></span>

<span data-ttu-id="5919a-118">假设您正在运行连接到数据库的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5919a-118">Imagine you're running a web application that connects to a database.</span></span> <span data-ttu-id="5919a-119">你将使用子网隔离网络的不同部分。</span><span class="sxs-lookup"><span data-stu-id="5919a-119">You'll use subnets to isolate different parts of the network.</span></span> <span data-ttu-id="5919a-120">子网是基于 IP 地址范围的网络的一部分。</span><span class="sxs-lookup"><span data-stu-id="5919a-120">A subnet is a part of a network that's based on a range of IP addresses.</span></span>

<span data-ttu-id="5919a-121">若要配置这些子网, 您将创建一个虚拟网络, 然后将该网络细分为子网。</span><span class="sxs-lookup"><span data-stu-id="5919a-121">To configure these subnets, you'll create a virtual network and then subdivide the network into subnets.</span></span> <span data-ttu-id="5919a-122">web 应用程序将在一个子网和另一个子网上的数据库上运行。</span><span class="sxs-lookup"><span data-stu-id="5919a-122">The web application will operate on one subnet and the database on another subnet.</span></span> <span data-ttu-id="5919a-123">每个子网都有自己的规则, 用于与其他网络进行通信。</span><span class="sxs-lookup"><span data-stu-id="5919a-123">Each subnet will have its own rules for communicating to and from the other network.</span></span> <span data-ttu-id="5919a-124">这些规则使您能够限制从数据库到 web 应用程序的访问。</span><span class="sxs-lookup"><span data-stu-id="5919a-124">These rules give you the ability to restrict access from the database to the web application.</span></span>

### <a name="what-is-a-firewall"></a><span data-ttu-id="5919a-125">什么是防火墙？</span><span class="sxs-lookup"><span data-stu-id="5919a-125">What is a firewall?</span></span>

<span data-ttu-id="5919a-126">防火墙是一项服务, 它基于每个请求的原始 IP 地址授予服务器访问权限。</span><span class="sxs-lookup"><span data-stu-id="5919a-126">A firewall is a service that grants server access based on the originating IP address of each request.</span></span> <span data-ttu-id="5919a-127">创建用于指定 IP 地址范围的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-127">You create firewall rules that specify ranges of IP addresses.</span></span> <span data-ttu-id="5919a-128">仅允许来自这些已授予 IP 地址的客户端访问服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-128">Only clients from these granted IP addresses will be allowed to access the server.</span></span> <span data-ttu-id="5919a-129">通常情况下, 防火墙规则还包括特定网络协议和端口信息。</span><span class="sxs-lookup"><span data-stu-id="5919a-129">Firewall rules, generally speaking, also include specific network protocol and port information.</span></span> <span data-ttu-id="5919a-130">例如, 默认情况下, PostgreSQL 服务器侦听端口5432上的 TCP 请求。</span><span class="sxs-lookup"><span data-stu-id="5919a-130">For example, a PostgreSQL server by default listens to TCP requests on port 5432.</span></span>

### <a name="azure-database-for-postgresql-server-firewall"></a><span data-ttu-id="5919a-131">用于 PostgreSQL 服务器防火墙的 Azure 数据库</span><span class="sxs-lookup"><span data-stu-id="5919a-131">Azure Database for PostgreSQL server firewall</span></span>

<span data-ttu-id="5919a-132">PostgreSQL server 防火墙的 Azure 数据库将阻止对数据库服务器的所有访问, 直到您指定哪些计算机具有权限。</span><span class="sxs-lookup"><span data-stu-id="5919a-132">The Azure Database for PostgreSQL server firewall prevents all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="5919a-133">防火墙配置允许您指定允许连接到服务器的 IP 地址范围。</span><span class="sxs-lookup"><span data-stu-id="5919a-133">The firewall configuration allows you to specify a range of IP addresses that are allowed to connect to the server.</span></span> <span data-ttu-id="5919a-134">服务器始终使用默认的 PostgreSQL 连接信息。</span><span class="sxs-lookup"><span data-stu-id="5919a-134">The server always uses the default PostgreSQL connection information.</span></span>

![显示用于 PostgreSQL 服务器防火墙的 Azure 数据库扫描所有传入请求的 IP 地址的插图。](../media/6-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a><span data-ttu-id="5919a-137">用于 PostgreSQL server SSL 连接的 Azure 数据库</span><span class="sxs-lookup"><span data-stu-id="5919a-137">Azure Database for PostgreSQL server SSL connections</span></span>

<span data-ttu-id="5919a-138">适用于 PostgreSQL 的 Azure 数据库首选客户端应用程序使用安全套接字层 (SSL) 连接到 PostgreSQL 服务。</span><span class="sxs-lookup"><span data-stu-id="5919a-138">Azure Database for PostgreSQL prefers that your client applications connect to the PostgreSQL service using the Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="5919a-139">在数据库服务器和客户端应用程序之间实施 SSL 连接有助于通过加密服务器和客户端之间的数据来防止 "中间人" 和类似的攻击。</span><span class="sxs-lookup"><span data-stu-id="5919a-139">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" and similar attacks by encrypting the data between the server and client.</span></span> <span data-ttu-id="5919a-140">启用 SSL 需要在客户端和服务器之间交换密钥和严格的身份验证, 以便连接能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="5919a-140">Enabling SSL requires the exchange of keys and strict authentication between client and server for the connection to work.</span></span> <span data-ttu-id="5919a-141">有关使用 SSL 的详细信息不在本学习模块的范围之内。</span><span class="sxs-lookup"><span data-stu-id="5919a-141">Details about using SSL are beyond the scope of this learning module.</span></span>

## <a name="configure-connection-security"></a><span data-ttu-id="5919a-142">配置连接安全性</span><span class="sxs-lookup"><span data-stu-id="5919a-142">Configure connection security</span></span>

<span data-ttu-id="5919a-143">让我们来看一下为 PostgreSQL server 防火墙配置 Azure 数据库时所做的决策和步骤。</span><span class="sxs-lookup"><span data-stu-id="5919a-143">Let's look at the decisions and steps you make to configure an Azure Database for PostgreSQL server firewall.</span></span> <span data-ttu-id="5919a-144">此外, 您还将了解如何连接到之前创建的服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-144">You'll also see how to connect to the server that you created earlier.</span></span>

<span data-ttu-id="5919a-145">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="5919a-145">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span> <span data-ttu-id="5919a-146">导航到您要为其创建防火墙规则的服务器资源。</span><span class="sxs-lookup"><span data-stu-id="5919a-146">Navigate to the server resource for which you'd like to create a firewall rule.</span></span>

<span data-ttu-id="5919a-147">然后, 选择 "**连接安全**" 选项以打开右侧的 "连接安全" 边栏。</span><span class="sxs-lookup"><span data-stu-id="5919a-147">Then, you'll select the **Connection Security** option to open the connection security blade to the right.</span></span>

![显示 PostgreSQL 数据库资源边栏的 "连接安全" 部分的 Azure 门户屏幕截图](../media/6-db-security-settings.png)

<span data-ttu-id="5919a-149">在此屏幕上, 您有多个选项。</span><span class="sxs-lookup"><span data-stu-id="5919a-149">On this screen, you have several options.</span></span> <span data-ttu-id="5919a-150">您可以：</span><span class="sxs-lookup"><span data-stu-id="5919a-150">You can:</span></span>

- <span data-ttu-id="5919a-151">通过单击 "**添加客户端 IP** " 按钮, 添加用于将门户访问为防火墙条目的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="5919a-151">Add the IP address that you use to access the portal as a firewall entry by clicking on the **Add client IP** button.</span></span>
- <span data-ttu-id="5919a-152">允许访问 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="5919a-152">Allow access to Azure services.</span></span> <span data-ttu-id="5919a-153">默认情况下, 所有 Azure 服务都**无法**访问 PostgreSQL 服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-153">By default, all Azure services **don't** have access to the PostgreSQL server.</span></span>
- <span data-ttu-id="5919a-154">通过输入 IP 地址的范围来添加防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-154">Add firewall rules by entering ranges of IP addresses.</span></span>
- <span data-ttu-id="5919a-155">强制实施 SSL 连接。</span><span class="sxs-lookup"><span data-stu-id="5919a-155">Enforce SSL connections.</span></span> <span data-ttu-id="5919a-156">此选项将强制客户端使用 SSL 证书连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-156">This option forces your client to connect to the server using an SSL certificate.</span></span>

<span data-ttu-id="5919a-157">始终记得单击 "保存" 图标上方的 "**保存**" 图标, 以在进行更改后保存已更新的配置。</span><span class="sxs-lookup"><span data-stu-id="5919a-157">Always remember to click on the **Save** icon above the entry fields to save the updated configuration after you've made changes.</span></span>

### <a name="allow-access-to-azure-services"></a><span data-ttu-id="5919a-158">允许访问 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="5919a-158">Allow access to Azure services</span></span>

<span data-ttu-id="5919a-159">若要使用 Azure 云命令行管理程序访问或配置您的服务器, 请确保启用 "**允许访问 Azure 服务**"。</span><span class="sxs-lookup"><span data-stu-id="5919a-159">To use Azure Cloud Shell to access or configure your server, make sure to enable **Allow Access to Azure Services**.</span></span> <span data-ttu-id="5919a-160">此步骤将向服务器配置添加防火墙规则, 以允许从云命令行管理程序访问。</span><span class="sxs-lookup"><span data-stu-id="5919a-160">This step is going to add a firewall rule to the server configuration to allow access from Cloud Shell.</span></span> <span data-ttu-id="5919a-161">此规则不会显示为你添加的自定义规则之一。</span><span class="sxs-lookup"><span data-stu-id="5919a-161">This rule won't show as one of the custom rules that you add.</span></span>

<span data-ttu-id="5919a-162">此外, 还需要禁用**强制 SSL 连接**。</span><span class="sxs-lookup"><span data-stu-id="5919a-162">You also need to disable **Enforce SSL connection**.</span></span> <span data-ttu-id="5919a-163">如果客户端连接需要 SSL, PowerShell 将无法连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-163">PowerShell can't connect to the server if SSL is required for client connections.</span></span>

<span data-ttu-id="5919a-164">如果配置不正确, 这两个选项都将导致在命令行中显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="5919a-164">Both of these options will result in an error message that's displayed on the command line if not configured correctly.</span></span>

<span data-ttu-id="5919a-165">例如, 如果不允许访问 Azure 服务并强制实施 SSL 连接, 则当防火墙阻止访问时, 您会看到类似于此错误的内容:</span><span class="sxs-lookup"><span data-stu-id="5919a-165">For example, if access is not allowed to Azure services and enforce SSL connections is enabled, then you'll see something similar to this error when the firewall is blocking access:</span></span>

```output
psql: FATAL: no pg_hba.conf entry for host "123.45.67.89", user "adminuser", database "postgres", SSL on FATAL:  SSL connection is required. Please specify SSL options and retry.
```

### <a name="create-a-firewall-rule-using-the-portal"></a><span data-ttu-id="5919a-166">使用门户创建防火墙规则</span><span class="sxs-lookup"><span data-stu-id="5919a-166">Create a firewall rule using the portal</span></span>

<span data-ttu-id="5919a-167">假设您要创建提供来自任何 IP 地址的访问权限的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-167">Let's say you want to create a firewall rule that provides access from any IP address.</span></span>

> [!WARNING]
> <span data-ttu-id="5919a-168">创建此防火墙规则将允许 Internet 上的任何 IP 地址尝试连接到您的服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-168">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="5919a-169">即使客户端无法在不使用用户名和密码的情况下访问服务器, 也应谨慎启用此规则, 并确保了解安全含义。</span><span class="sxs-lookup"><span data-stu-id="5919a-169">Even though clients won't be able access the server without the username and password, enable this rule with caution and make sure you understand the security implications.</span></span>

<span data-ttu-id="5919a-170">您可以通过在标记的字段中输入以下数据来创建新的防火墙规则:</span><span class="sxs-lookup"><span data-stu-id="5919a-170">You create a new firewall rule by entering the following data in the labeled fields:</span></span>

- <span data-ttu-id="5919a-171">规则名称:`AllowAll`</span><span class="sxs-lookup"><span data-stu-id="5919a-171">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="5919a-172">起始 IP:`0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="5919a-172">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="5919a-173">结束 IP:`255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="5919a-173">End IP: `255.255.255.255`</span></span>

<span data-ttu-id="5919a-174">若要删除防火墙规则, 请单击要删除的规则末尾的省略号 (...)。</span><span class="sxs-lookup"><span data-stu-id="5919a-174">To remove a firewall rule, you'll click the ellipsis (...) at the end of the rule that you want to delete.</span></span> <span data-ttu-id="5919a-175">单击 "**删除**" 按钮以删除规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-175">Click the **Delete** button to delete the rule.</span></span>

<span data-ttu-id="5919a-176">单击 "**保存**" 图标上方的 "输入" 字段以提交规则的删除。</span><span class="sxs-lookup"><span data-stu-id="5919a-176">Click on the **Save** icon above the entry fields to commit the deletion of the rule.</span></span>

### <a name="create-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="5919a-177">使用 Azure CLI 创建防火墙规则</span><span class="sxs-lookup"><span data-stu-id="5919a-177">Create a firewall rule using the Azure CLI</span></span>

<span data-ttu-id="5919a-178">您可以使用 Azure CLI 将防火墙规则添加到您的服务器中的`az postgres server firewall-rule create`命令。</span><span class="sxs-lookup"><span data-stu-id="5919a-178">You can use the Azure CLI to add firewall rules to your server with the `az postgres server firewall-rule create` command.</span></span> <span data-ttu-id="5919a-179">下面的示例将根据上面的内容创建规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-179">Here's an example that creates the rule from above.</span></span>

```azurecli
az postgres server firewall-rule create \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --server <server-name> \
  --name AllowAll \
  --start-ip-address 0.0.0.0 \
  --end-ip-address 255.255.255.255
```

<span data-ttu-id="5919a-180">使用命令`az postgres server firewall-rule delete`删除服务器中的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="5919a-180">You remove firewall rules from your server with the command `az postgres server firewall-rule delete`.</span></span> <span data-ttu-id="5919a-181">下面是一个示例:</span><span class="sxs-lookup"><span data-stu-id="5919a-181">Here's an example:</span></span>

```azurecli
az postgres server firewall-rule delete \
  --name AllowAll \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --server-name <server-name>
```

## <a name="connecting-to-your-server"></a><span data-ttu-id="5919a-182">连接到服务器</span><span class="sxs-lookup"><span data-stu-id="5919a-182">Connecting to your server</span></span>

<span data-ttu-id="5919a-183">与任何新式数据库一样, PostgreSQL 需要进行定期服务器管理以实现最佳性能。</span><span class="sxs-lookup"><span data-stu-id="5919a-183">Like any modern database, PostgreSQL requires regular server administration to achieve best performance.</span></span> <span data-ttu-id="5919a-184">有许多选项可用于连接和管理 PostgreSQL 服务器的 Azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="5919a-184">You have a number of options to connect and manage your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="5919a-185">我们将使用`psql`连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-185">We'll use `psql` to connect to the server.</span></span>

### <a name="what-is-psql"></a><span data-ttu-id="5919a-186">什么是 psql？</span><span class="sxs-lookup"><span data-stu-id="5919a-186">What is psql?</span></span>

<span data-ttu-id="5919a-187">调用`psql`的命令行工具是用于使用 PostgreSQL 服务器和数据库的 PostgreSQL 分布式交互终端。</span><span class="sxs-lookup"><span data-stu-id="5919a-187">The command-line tool called `psql` is the PostgreSQL distributed interactive terminal for working with PostgreSQL servers and databases.</span></span> <span data-ttu-id="5919a-188">`psql`适用于 PostgreSQL 的 azure 数据库, 与任何其他 PostgreSQL 实现相同, 并且包含在 Azure 云命令行管理程序中。</span><span class="sxs-lookup"><span data-stu-id="5919a-188">`psql` works with Azure Database for PostgreSQL the same as with any other PostgreSQL implementation and is included with Azure Cloud Shell.</span></span> <span data-ttu-id="5919a-189">该`psql`工具允许您管理数据库以及对这些数据库执行结构查询。</span><span class="sxs-lookup"><span data-stu-id="5919a-189">The `psql` tool allows you to manage databases as well as execute structure queries against these databases.</span></span>

<span data-ttu-id="5919a-190">使用`psql`需要成功连接到 PostgreSQL 服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-190">Using `psql` requires a successful connection to a PostgreSQL server.</span></span> <span data-ttu-id="5919a-191">使用时, 有许多命令行参数可供使用`psql`。</span><span class="sxs-lookup"><span data-stu-id="5919a-191">There are a number of command-line parameters available for use when working with `psql`.</span></span>

- <span data-ttu-id="5919a-192">`--host`-要连接到的主机。</span><span class="sxs-lookup"><span data-stu-id="5919a-192">`--host` - The host to which you'd like to connect.</span></span>
- <span data-ttu-id="5919a-193">`--username`-连接所用的用户名/ID。</span><span class="sxs-lookup"><span data-stu-id="5919a-193">`--username` - The user name/ID with which to connect.</span></span>
- <span data-ttu-id="5919a-194">`--dbname`-要连接到的数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="5919a-194">`--dbname` - The name of the database to connect to.</span></span>

> [!TIP]
> <span data-ttu-id="5919a-195">在管理服务器访问和数据库`postgres`配置时, 通常会连接到管理数据库。</span><span class="sxs-lookup"><span data-stu-id="5919a-195">You'll typically connect to the `postgres` management database when managing your server access and database configurations.</span></span>

<span data-ttu-id="5919a-196">下面是完整的命令:</span><span class="sxs-lookup"><span data-stu-id="5919a-196">Here is the complete command:</span></span>

```bash
psql --host=<server-name>.postgres.database.azure.com \
  --username=<admin-user>@<server-name> \
  --dbname=<database>
```

<span data-ttu-id="5919a-197">连接后, 将显示命令提示符, 并可对服务器和数据库执行命令。</span><span class="sxs-lookup"><span data-stu-id="5919a-197">After you're connected, you'll be presented with a command prompt and can execute commands to your server and databases.</span></span>

<span data-ttu-id="5919a-198">现在, 您已看到为 PostgreSQL 安全设置配置 Azure 数据库所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="5919a-198">You've now seen the steps that you take to configure Azure Database for PostgreSQL security settings.</span></span> <span data-ttu-id="5919a-199">在下一个设备中, 您将为 PostgreSQL 安全设置配置 Azure 数据库。</span><span class="sxs-lookup"><span data-stu-id="5919a-199">In the next unit, you'll configure Azure Database for PostgreSQL security settings.</span></span> <span data-ttu-id="5919a-200">您还将使用云命令行管理程序连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="5919a-200">You'll also connect to the server using Cloud Shell.</span></span>
