<span data-ttu-id="d0cf6-101">你有一个你计划保留的本地数据中心, 但你想要使用 azure 来使用 azure 中托管的虚拟机 (vm) 分担峰值流量。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-101">You have an on-premises datacenter that you plan to keep, but you want to use Azure to offload peak traffic using virtual machines (VMs) hosted in Azure.</span></span> <span data-ttu-id="d0cf6-102">您想要保留现有的 IP 寻址方案和网络设备, 同时确保任何数据传输是安全的。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-102">You want to keep your existing IP addressing scheme and network appliances, while ensuring that any data transfer is secure.</span></span>

## <a name="what-is-azure-virtual-networking"></a><span data-ttu-id="d0cf6-103">什么是 Azure 虚拟网络？</span><span class="sxs-lookup"><span data-stu-id="d0cf6-103">What is Azure virtual networking?</span></span>

<span data-ttu-id="d0cf6-104">**azure 虚拟网络**允许 azure 资源 (例如虚拟机、web 应用和数据库) 与 Internet 上的用户、Internet 上的用户以及本地客户端计算机进行通信。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-104">**Azure virtual networks** enable Azure resources, such as virtual machines, web apps, and databases, to communicate with: each other, users on the Internet, and on-premises client computers.</span></span> <span data-ttu-id="d0cf6-105">你可以将 Azure 网络视为一组链接到其他 Azure 资源的资源。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-105">You can think of an Azure network as a set of resources that links other Azure resources.</span></span>

<span data-ttu-id="d0cf6-106">Azure 虚拟网络提供了关键网络功能:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-106">Azure virtual networks provide key networking capabilities:</span></span>

- <span data-ttu-id="d0cf6-107">隔离和分段</span><span class="sxs-lookup"><span data-stu-id="d0cf6-107">Isolation and segmentation</span></span>
- <span data-ttu-id="d0cf6-108">Internet 通信</span><span class="sxs-lookup"><span data-stu-id="d0cf6-108">Internet communications</span></span>
- <span data-ttu-id="d0cf6-109">在 Azure 资源之间进行通信</span><span class="sxs-lookup"><span data-stu-id="d0cf6-109">Communicate between Azure resources</span></span>
- <span data-ttu-id="d0cf6-110">与本地资源进行通信</span><span class="sxs-lookup"><span data-stu-id="d0cf6-110">Communicate with on-premises resources</span></span>
- <span data-ttu-id="d0cf6-111">路由网络流量</span><span class="sxs-lookup"><span data-stu-id="d0cf6-111">Route network traffic</span></span>
- <span data-ttu-id="d0cf6-112">筛选网络流量</span><span class="sxs-lookup"><span data-stu-id="d0cf6-112">Filter network traffic</span></span>
- <span data-ttu-id="d0cf6-113">连接虚拟网络</span><span class="sxs-lookup"><span data-stu-id="d0cf6-113">Connect virtual networks</span></span>
 
#### <a name="network-configurations-for-virtual-machines"></a><span data-ttu-id="d0cf6-114">虚拟机的网络配置</span><span class="sxs-lookup"><span data-stu-id="d0cf6-114">Network configurations for virtual machines</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEve]

### <a name="isolation-and-segmentation"></a><span data-ttu-id="d0cf6-115">隔离和分段</span><span class="sxs-lookup"><span data-stu-id="d0cf6-115">Isolation and segmentation</span></span>

<span data-ttu-id="d0cf6-116">Azure 允许您创建多个独立的虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-116">Azure allows you to create multiple isolated virtual networks.</span></span> <span data-ttu-id="d0cf6-117">设置虚拟网络时, 可以使用公用或专用 IP 地址范围定义专用 Internet 协议 (IP) 地址空间。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-117">When you set up a virtual network, you define a private Internet Protocol (IP) address space, using either public or private IP address ranges.</span></span> <span data-ttu-id="d0cf6-118">然后, 可以将该 IP 地址空间划分为子网, 并将部分定义的地址空间分配给每个已命名的子网。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-118">You can then segment that IP address space into subnets, and allocate part of the defined address space to each named subnet.</span></span>

<span data-ttu-id="d0cf6-119">对于名称解析, 可以使用 Azure 中内置的名称解析服务, 也可以将虚拟网络配置为使用内部或外部域名系统 (DNS) 服务器。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-119">For name resolution, you can use the name resolution service that's built in to Azure, or you can configure the virtual network to use either an internal or an external Domain Name System (DNS) server.</span></span>

### <a name="internet-communications"></a><span data-ttu-id="d0cf6-120">Internet 通信</span><span class="sxs-lookup"><span data-stu-id="d0cf6-120">Internet communications</span></span>

<span data-ttu-id="d0cf6-121">默认情况下, Azure 中的 VM 可连接到 Internet。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-121">A VM in Azure can connect out to the Internet by default.</span></span> <span data-ttu-id="d0cf6-122">您可以通过定义公共 IP 地址或公用负载平衡器来启用来自 Internet 的传入连接。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-122">You can enable incoming connections from the Internet by defining a public IP address or a public load balancer.</span></span> <span data-ttu-id="d0cf6-123">对于虚拟机管理, 可以通过 Azure CLI、远程桌面协议 (RDP) 或安全命令行管理程序 (SSH) 进行连接。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-123">For VM management, you can connect via the Azure CLI, Remote Desktop Protocol (RDP), or Secure Shell (SSH).</span></span>

### <a name="communicate-between-azure-resources"></a><span data-ttu-id="d0cf6-124">在 Azure 资源之间进行通信</span><span class="sxs-lookup"><span data-stu-id="d0cf6-124">Communicate between Azure resources</span></span>

<span data-ttu-id="d0cf6-125">你将需要使 Azure 资源能够彼此安全地相互通信。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-125">You'll want to enable Azure resources to communicate securely with each other.</span></span> <span data-ttu-id="d0cf6-126">可以通过以下两种方式之一执行此操作:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-126">You can do that in one of two ways:</span></span>

- <span data-ttu-id="d0cf6-127">**虚拟网络**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-127">**Virtual networks**</span></span>

    <span data-ttu-id="d0cf6-128">虚拟网络不仅可以连接虚拟机, 还可以连接其他 Azure 资源, 如 App Service 环境、azure Kubernetes Service 和 azure 虚拟机规模集。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-128">Virtual networks can connect not only VMs, but other Azure resources, such as the App Service Environment, Azure Kubernetes Service, and Azure virtual machine scale sets.</span></span>

- <span data-ttu-id="d0cf6-129">**服务终结点**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-129">**Service endpoints**</span></span>

     <span data-ttu-id="d0cf6-130">您可以使用服务终结点连接到其他 azure 资源类型, 如 azure SQL 数据库和存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-130">You can use service endpoints to connect to other Azure resource types, such as Azure SQL databases and storage accounts.</span></span> <span data-ttu-id="d0cf6-131">利用此方法, 您可以将多个 Azure 资源链接到虚拟网络, 从而提高安全性并提供资源之间的最佳路由。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-131">This approach enables you to link multiple Azure resources to virtual networks, thereby improving security and providing optimal routing between resources.</span></span>

### <a name="communicate-with-on-premises-resources"></a><span data-ttu-id="d0cf6-132">与本地资源进行通信</span><span class="sxs-lookup"><span data-stu-id="d0cf6-132">Communicate with on-premises resources</span></span>

<span data-ttu-id="d0cf6-133">使用 azure 虚拟网络, 您可以将内部部署环境和 Azure 订阅中的资源链接在一起, 这实际上是创建一个同时跨越本地和云环境的网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-133">Azure virtual networks enable you to link resources together in your on-premises environment and within your Azure subscription, in effect creating a network that spans both your local and cloud environments.</span></span> <span data-ttu-id="d0cf6-134">您可以通过三种机制实现此连接:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-134">There are three mechanisms for you to achieve this connectivity:</span></span>

- <span data-ttu-id="d0cf6-135">**点到站点虚拟专用网络**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-135">**Point-to-site Virtual Private Networks**</span></span>

   <span data-ttu-id="d0cf6-136">此方法类似于虚拟专用网络 (VPN) 连接, 组织外部的计算机会将其返回到公司网络, 但它的工作方向相反。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-136">This approach is like a Virtual Private Network (VPN) connection that a computer outside your organization makes back into your corporate network, except that it's working in the opposite direction.</span></span> <span data-ttu-id="d0cf6-137">在这种情况下, 客户端计算机会启动到 azure 的加密 VPN 连接, 并将该计算机连接到 azure 虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-137">In this case, the client computer initiates an encrypted VPN connection to Azure, connecting that computer to the Azure virtual network.</span></span>

- <span data-ttu-id="d0cf6-138">**站点到站点虚拟专用网络**站点到站点 vpn 将本地 VPN 设备或网关链接到虚拟网络中的 Azure VPN 网关。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-138">**Site-to-site Virtual Private Networks** A site-to-site VPN links your on-premises VPN device or gateway to the Azure VPN gateway in a virtual network.</span></span> <span data-ttu-id="d0cf6-139">实际上, Azure 中的设备可能显示为位于本地网络上。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-139">In effect, the devices in Azure can appear as being on the local network.</span></span> <span data-ttu-id="d0cf6-140">该连接通过 Internet 进行加密和工作。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-140">The connection is encrypted and works over the Internet.</span></span>

- <span data-ttu-id="d0cf6-141">**Azure ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-141">**Azure ExpressRoute**</span></span>

    <span data-ttu-id="d0cf6-142">对于需要更大带宽甚至更高的安全性的环境, Azure ExpressRoute 是最佳方法。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-142">For environments where you need greater bandwidth and even higher levels of security, Azure ExpressRoute is the best approach.</span></span> <span data-ttu-id="d0cf6-143">azure ExpressRoute 提供到 azure 的专用专用连接, 不通过 Internet 传输。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-143">Azure ExpressRoute provides dedicated private connectivity to Azure that does not travel over the Internet.</span></span>

### <a name="route-network-traffic"></a><span data-ttu-id="d0cf6-144">路由网络流量</span><span class="sxs-lookup"><span data-stu-id="d0cf6-144">Route network traffic</span></span>

<span data-ttu-id="d0cf6-145">默认情况下, Azure 将路由任何连接的虚拟网络、本地网络和 Internet 上的子网之间的流量。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-145">By default, Azure will route traffic between subnets on any connected virtual networks, on-premises networks, and the Internet.</span></span> <span data-ttu-id="d0cf6-146">但是, 您可以控制路由和重写这些设置, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-146">However, you can control routing and override those settings as follows:</span></span>

- <span data-ttu-id="d0cf6-147">**路由表**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-147">**Route tables**</span></span>

    <span data-ttu-id="d0cf6-148">路由表允许您定义应如何定向流量的规则。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-148">A route table allows you to define rules as to how traffic should be directed.</span></span> <span data-ttu-id="d0cf6-149">您可以创建自定义路由表, 这些表控制如何在子网之间路由数据包。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-149">You can create custom route tables that control how packets are routed between subnets.</span></span>

- <span data-ttu-id="d0cf6-150">**边界网关协议**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-150">**Border Gateway Protocol**</span></span>

    <span data-ttu-id="d0cf6-151">边界网关协议 (BGP) 可与 azure VPN 网关或 ExpressRoute 配合使用, 以将本地 BGP 路由传播到 azure 虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-151">Border Gateway Protocol (BGP) works with Azure VPN gateways or ExpressRoute to propagate on-premises BGP routes to Azure virtual networks.</span></span>

### <a name="filter-network-traffic"></a><span data-ttu-id="d0cf6-152">筛选网络流量</span><span class="sxs-lookup"><span data-stu-id="d0cf6-152">Filter network traffic</span></span>

<span data-ttu-id="d0cf6-153">使用 Azure 虚拟网络, 可以通过以下方法来筛选子网之间的流量:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-153">Azure virtual networks enable you to filter traffic between subnets by using the following approaches:</span></span>

- <span data-ttu-id="d0cf6-154">**网络安全组**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-154">**Network security groups**</span></span>

    <span data-ttu-id="d0cf6-155">网络安全组是可以包含多个入站和出站安全规则的 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-155">A network security group is an Azure resource that can contain multiple inbound and outbound security rules.</span></span> <span data-ttu-id="d0cf6-156">您可以根据诸如源和目标 IP 地址、端口和协议等因素, 定义这些规则以允许或阻止流量。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-156">You can define these rules to allow or block traffic, based on factors such as source and destination IP address, port, and protocol.</span></span>

- <span data-ttu-id="d0cf6-157">**网络虚拟设备**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-157">**Network virtual appliances**</span></span>

    <span data-ttu-id="d0cf6-158">网络虚拟设备是一种专用的 VM, 可与强化的网络设备进行比较。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-158">A network virtual appliance is a specialized VM that can be compared to a hardened network appliance.</span></span> <span data-ttu-id="d0cf6-159">网络虚拟设备将执行特定的网络功能, 如运行防火墙或执行 WAN 优化。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-159">A network virtual appliance carries out a particular network function, such as running a firewall or performing WAN optimization.</span></span>

## <a name="connect-virtual-networks"></a><span data-ttu-id="d0cf6-160">连接虚拟网络</span><span class="sxs-lookup"><span data-stu-id="d0cf6-160">Connect virtual networks</span></span>

<span data-ttu-id="d0cf6-161">您可以使用虚拟网络对_等_链接将虚拟网络链接在一起。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-161">You can link virtual networks together using virtual network _peering_.</span></span> <span data-ttu-id="d0cf6-162">对等功能使每个虚拟网络中的资源能够相互通信。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-162">Peering enables resources in each virtual network to communicate with each other.</span></span> <span data-ttu-id="d0cf6-163">这些虚拟网络可以位于不同的区域, 从而使您可以通过 Azure 创建全局互联网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-163">These virtual networks can be in separate regions, allowing you to create a global interconnected network through Azure.</span></span>

## <a name="azure-virtual-network-settings"></a><span data-ttu-id="d0cf6-164">Azure 虚拟网络设置</span><span class="sxs-lookup"><span data-stu-id="d0cf6-164">Azure virtual network settings</span></span>

<span data-ttu-id="d0cf6-165">您可以从 azure 门户、本地计算机上的 azure PowerShell 或 azure 云命令行管理程序中创建和配置 azure 虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-165">You can create and configure Azure virtual networks from the Azure portal, Azure PowerShell on your local computer, or Azure Cloud Shell.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="d0cf6-166">创建虚拟网络</span><span class="sxs-lookup"><span data-stu-id="d0cf6-166">Create a virtual network</span></span>

<span data-ttu-id="d0cf6-167">创建 Azure 虚拟网络时, 可以配置许多基本设置。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-167">When you create an Azure virtual network, you configure a number of basic settings.</span></span> <span data-ttu-id="d0cf6-168">你可以选择配置高级设置, 如多个子网、分布式拒绝服务 (DDoS) 保护和服务终结点。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-168">You'll have the option to configure advanced settings, such as multiple subnets, distributed denial of service (DDoS) protection, and service endpoints.</span></span>

![显示创建虚拟网络刀片字段的示例的 Azure 门户屏幕截图。](../media/2-create-virtual-network.PNG)

<span data-ttu-id="d0cf6-170">你将为基本虚拟网络配置以下设置:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-170">You'll configure the following settings for a basic virtual network:</span></span>

- <span data-ttu-id="d0cf6-171">**网络名称**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-171">**Network name**</span></span>

    <span data-ttu-id="d0cf6-172">网络名称在订阅中必须是唯一的, 但不需要全局唯一。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-172">The network name must be unique in your subscription, but does not need to be globally unique.</span></span> <span data-ttu-id="d0cf6-173">使名称成为易于记忆的描述性的名称, 并可从其他虚拟网络进行识别。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-173">Make the name a descriptive one that is easy to remember and identified from other virtual networks.</span></span>

- <span data-ttu-id="d0cf6-174">**地址空间**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-174">**Address space**</span></span>

    <span data-ttu-id="d0cf6-175">设置虚拟网络时, 需要在无类别的域间路由 (CIDR) 格式中定义内部地址空间。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-175">When you set up a virtual network, you define the internal address space in Classless Inter-Domain Routing (CIDR) format.</span></span> <span data-ttu-id="d0cf6-176">此地址空间在你的订阅和你连接到的任何其他网络中都必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-176">This address space needs to be unique within your subscription and any other networks that you connect to.</span></span>

    <span data-ttu-id="d0cf6-177">假设您为第一个虚拟网络选择了 10.0.0.0/24 的地址空间。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-177">Let's assume, you choose an address space of 10.0.0.0/24 for your first virtual network.</span></span> <span data-ttu-id="d0cf6-178">此地址空间中定义的地址的范围为 10.0.0.1-10.0.0.254。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-178">The addresses defined in this address space ranges from 10.0.0.1 - 10.0.0.254.</span></span> <span data-ttu-id="d0cf6-179">然后, 创建第二个虚拟网络并选择10.1.0.0 的地址空间。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-179">You then create a second virtual network and choose an address space of 10.1.0.0./8.</span></span> <span data-ttu-id="d0cf6-180">此地址空间中的地址范围为 10.0.0.1-10.255.255.254。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-180">The address in this address space ranges from 10.0.0.1 - 10.255.255.254.</span></span> <span data-ttu-id="d0cf6-181">某些地址重叠, 不能用于两个虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-181">Some of the address overlap and can't be used for the two virtual networks.</span></span>

    <span data-ttu-id="d0cf6-182">但是, 可以使用 10.0.0.0/16, 地址范围为 10.0.0.1-10.0.255.254 和 10.1.0.0/16, 地址范围从 10.1.0.1-10.1.255.254。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-182">However, you can use 10.0.0.0/16, with addresses ranging from 10.0.0.1 - 10.0.255.254, and 10.1.0.0/16, with addresses ranging from 10.1.0.1 - 10.1.255.254.</span></span> <span data-ttu-id="d0cf6-183">你可以将这些地址空间分配给虚拟网络, 因为没有地址重叠。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-183">You can assign these address spaces to your virtual networks since there's no address overlap.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0cf6-184">可以在创建虚拟网络后添加地址空间。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-184">You can add address spaces after creating the virtual network.</span></span>

- <span data-ttu-id="d0cf6-185">**订购**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-185">**Subscription**</span></span>

    <span data-ttu-id="d0cf6-186">仅当您有多个订阅可供选择时才适用。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-186">Only applies if you have multiple subscriptions to choose from.</span></span>

- <span data-ttu-id="d0cf6-187">**资源组**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-187">**Resource group**</span></span>

    <span data-ttu-id="d0cf6-188">与任何其他 Azure 资源一样, 虚拟网络需要存在于资源组中。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-188">Like any other Azure resource, a virtual network needs to exist in a resource group.</span></span> <span data-ttu-id="d0cf6-189">您可以选择现有的资源组, 也可以创建一个新的资源组。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-189">You can either select an existing resource group or create a new one.</span></span>

- <span data-ttu-id="d0cf6-190">**Location**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-190">**Location**</span></span>

    <span data-ttu-id="d0cf6-191">选择您希望虚拟网络存在的位置。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-191">Select the location where you want the virtual network to exist.</span></span>

- <span data-ttu-id="d0cf6-192">**子网**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-192">**Subnet**</span></span>

    <span data-ttu-id="d0cf6-193">在每个虚拟网络地址范围内, 您可以创建一个或多个对虚拟网络的地址空间进行分区的子网。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-193">Within each virtual network address range, you can create one or more subnets that partition the virtual network's address space.</span></span> <span data-ttu-id="d0cf6-194">然后, 在子网之间路由将取决于默认流量路由, 也可以定义自定义路由。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-194">Routing between subnets will then depend on the default traffic routes, or you can define custom routes.</span></span> <span data-ttu-id="d0cf6-195">或者, 您可以定义一个包含所有虚拟网络地址范围的子网。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-195">Alternatively, you can define one subnet that encompasses all the virtual networks' address ranges.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0cf6-196">子网名称必须以字母或数字开头, 以字母、数字或下划线结尾, 并且只能包含字母、数字、下划线、句点或连字符。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-196">Subnet names must begin with a letter or number, end with a letter, number or underscore, and may contain only letters, numbers, underscores, periods, or hyphens.</span></span>

- <span data-ttu-id="d0cf6-197">**分布式拒绝服务 (DDoS) 保护**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-197">**Distributed Denial of Service (DDoS) protection**</span></span>

    <span data-ttu-id="d0cf6-198">您可以选择 "基本" 或 "标准" DDoS 保护。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-198">You can select either Basic or Standard DDoS protection.</span></span> <span data-ttu-id="d0cf6-199">标准 DDoS 保护是一项高级服务。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-199">Standard DDoS Protection is a premium service.</span></span> <span data-ttu-id="d0cf6-200">[Azure DDoS 保护标准](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview)提供了有关标准 DDoS 保护的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-200">The [Azure DDoS Protection Standard](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) provides for more information on Standard DDoS protection.</span></span>

- <span data-ttu-id="d0cf6-201">**服务终结点**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-201">**Service Endpoints**</span></span>

    <span data-ttu-id="d0cf6-202">在此处, 启用服务终结点, 然后从列表中选择您要启用的 Azure 服务终结点。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-202">Here, you enable service endpoints, and then select from the list which Azure service endpoints you want to enable.</span></span> <span data-ttu-id="d0cf6-203">选项包括 azure Cosmos DB、azure 服务总线、azure Key Vault 等。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-203">Options include Azure Cosmos DB, Azure Service Bus, Azure Key Vault, and so on.</span></span>

<span data-ttu-id="d0cf6-204">配置这些设置后, 单击 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-204">When you have configured these settings, click the **Create** button.</span></span>

### <a name="define-additional-settings"></a><span data-ttu-id="d0cf6-205">定义其他设置</span><span class="sxs-lookup"><span data-stu-id="d0cf6-205">Define additional settings</span></span>

<span data-ttu-id="d0cf6-206">创建虚拟网络后, 可以进一步定义设置。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-206">After creating a virtual network, you can then define further settings.</span></span> <span data-ttu-id="d0cf6-207">这些内容包括:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-207">These include:</span></span>

- <span data-ttu-id="d0cf6-208">**网络安全组**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-208">**Network security group**</span></span>

    <span data-ttu-id="d0cf6-209">网络安全组具有安全规则, 使您能够筛选出可以流入和传出虚拟网络子网和网络接口的网络通信的类型。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-209">Network security groups have security rules that enable you to filter the type of network traffic that can flow in and out of virtual network subnets and network interfaces.</span></span> <span data-ttu-id="d0cf6-210">您可以单独创建网络安全组, 然后将其与虚拟网络相关联。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-210">You create the network security group separately, and then associate it with the virtual network.</span></span>

- <span data-ttu-id="d0cf6-211">**路由表**</span><span class="sxs-lookup"><span data-stu-id="d0cf6-211">**Route table**</span></span>

    <span data-ttu-id="d0cf6-212">azure 自动为 Azure 虚拟网络中的每个子网创建路由表, 并将系统默认路由添加到表中。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-212">Azure automatically creates a route table for each subnet within an Azure virtual network and adds system default routes to the table.</span></span> <span data-ttu-id="d0cf6-213">但是, 可以添加自定义路由表以修改虚拟网络之间的流量。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-213">However, you can add custom route tables to modify traffic between virtual networks.</span></span>

<span data-ttu-id="d0cf6-214">您还可以修正服务终结点。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-214">You can also amend the service endpoints.</span></span>

![显示用于编辑虚拟网络设置的示例边栏的 Azure 门户的屏幕截图。](../media/2-virtual-network-additional-settings.PNG)

### <a name="configure-virtual-networks"></a><span data-ttu-id="d0cf6-216">配置虚拟网络</span><span class="sxs-lookup"><span data-stu-id="d0cf6-216">Configure virtual networks</span></span>

<span data-ttu-id="d0cf6-217">创建虚拟网络后, 可以在 Azure 门户中更改虚拟网络刀片中的任何其他设置。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-217">When you have created a virtual network, you can change any further settings from the Virtual Networks blade in the Azure portal.</span></span> <span data-ttu-id="d0cf6-218">或者, 也可以使用云命令行管理程序中的 PowerShell 命令或命令进行更改。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-218">Alternatively, you can use PowerShell commands or commands in Cloud Shell to make changes.</span></span>

![显示用于配置虚拟网络的示例边栏的 Azure 门户的屏幕截图。](../media/2-configure-virtual-network.PNG)

<span data-ttu-id="d0cf6-220">然后, 您可以查看和更改其他子刀片中的设置。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-220">You can then review and change settings in further sub-blades.</span></span>
<span data-ttu-id="d0cf6-221">这些设置包括:</span><span class="sxs-lookup"><span data-stu-id="d0cf6-221">These settings include:</span></span>

- <span data-ttu-id="d0cf6-222">地址空间: 可以向初始定义中添加更多地址空间</span><span class="sxs-lookup"><span data-stu-id="d0cf6-222">Address spaces: You can add further address spaces to the initial definition</span></span>

- <span data-ttu-id="d0cf6-223">连接的设备: 使用虚拟网络连接计算机</span><span class="sxs-lookup"><span data-stu-id="d0cf6-223">Connected devices: Use the virtual network to connect machines</span></span>

- <span data-ttu-id="d0cf6-224">子网: 添加更多子网</span><span class="sxs-lookup"><span data-stu-id="d0cf6-224">Subnets: Add further subnets</span></span>

- <span data-ttu-id="d0cf6-225">Peerings: 在对等排列中链接虚拟网络</span><span class="sxs-lookup"><span data-stu-id="d0cf6-225">Peerings: Link virtual networks in peering arrangements</span></span>

<span data-ttu-id="d0cf6-226">您还可以监视虚拟网络并对其进行故障排除, 或者创建一个自动化脚本来生成当前的虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-226">You can also monitor and troubleshoot virtual networks, or create an automation script to generate the current virtual network.</span></span>

<span data-ttu-id="d0cf6-227">虚拟网络是用于连接 Azure 中的实体的功能强大且高度可配置的机制。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-227">Virtual networks are powerful and highly configurable mechanisms for connecting entities in Azure.</span></span> <span data-ttu-id="d0cf6-228">你可以将 Azure 资源连接到另一台, 也可以将 Azure 资源连接到内部部署的资源。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-228">You can connect Azure resources to one another or to resources you have on-premises.</span></span> <span data-ttu-id="d0cf6-229">你可以隔离、筛选和路由你的网络流量, Azure 允许你在你认为需要它的情况下提高安全性。</span><span class="sxs-lookup"><span data-stu-id="d0cf6-229">You can isolate, filter and route your network traffic, and Azure allows you to increase security where you feel you need it.</span></span>
