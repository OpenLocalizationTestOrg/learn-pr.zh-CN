<span data-ttu-id="bdd79-101">由于贵公司处理高度敏感的数据, 并拥有大量要存储在 Azure 中的信息, 因此对通过公共 Internet 连接的安全性和可靠性有一些顾虑。</span><span class="sxs-lookup"><span data-stu-id="bdd79-101">As your company deals with highly sensitive data and has large amounts of information it will store in Azure, there are some concerns about the security and reliability of connections over the public Internet.</span></span> <span data-ttu-id="bdd79-102">该公司不愿意将批发迁移到 Azure, 除非它可以演示更高级别的连接性、安全性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="bdd79-102">The company isn't willing to migrate wholesale to Azure unless it can demonstrate higher levels of connectivity, security, and reliability.</span></span>

<span data-ttu-id="bdd79-103">在这里, 我们将超越通过 Internet 运行的连接, 以直接转到 Azure 数据中心的专用线路。</span><span class="sxs-lookup"><span data-stu-id="bdd79-103">Here, we'll go beyond connections that run over the Internet to dedicated lines direct into the Azure datacenters.</span></span>

## <a name="azure-expressroute"></a><span data-ttu-id="bdd79-104">Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bdd79-104">Azure ExpressRoute</span></span>

<span data-ttu-id="bdd79-105">microsoft Azure ExpressRoute 使组织能够通过连接提供程序实现的专用连接将本地网络扩展到 Microsoft 云中。</span><span class="sxs-lookup"><span data-stu-id="bdd79-105">Microsoft Azure ExpressRoute enables organizations to extend their on-premises networks into the Microsoft Cloud over a private connection implemented by a connectivity provider.</span></span> <span data-ttu-id="bdd79-106">这种排列意味着, 与 Azure 数据中心的连接不会通过 Internet 进行, 而是通过专用链接进行。</span><span class="sxs-lookup"><span data-stu-id="bdd79-106">This arrangement means that the connectivity to the Azure datacenters doesn't go over the Internet but across a dedicated link.</span></span> <span data-ttu-id="bdd79-107">ExpressRoute 还促进了与其他 Microsoft 基于云的服务 (如 Office 365 和 Dynamics 365) 的有效连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-107">ExpressRoute also facilitates efficient connections with other Microsoft cloud-based services, such as Office 365 and Dynamics 365.</span></span>

<span data-ttu-id="bdd79-108">ExpressRoute 提供的优势包括:</span><span class="sxs-lookup"><span data-stu-id="bdd79-108">Advantages that ExpressRoute provides include:</span></span>

- <span data-ttu-id="bdd79-109">速度更快, 从 50 Mbps 到 10 Gbps, 使用动态带宽扩展</span><span class="sxs-lookup"><span data-stu-id="bdd79-109">Faster speeds, from 50 Mbps to 10 Gbps, with dynamic bandwidth scaling</span></span>

- <span data-ttu-id="bdd79-110">较低延迟</span><span class="sxs-lookup"><span data-stu-id="bdd79-110">Lower latency</span></span>

- <span data-ttu-id="bdd79-111">通过内置的对等更高的可靠性</span><span class="sxs-lookup"><span data-stu-id="bdd79-111">Greater reliability through built-in peering</span></span>

- <span data-ttu-id="bdd79-112">高度安全</span><span class="sxs-lookup"><span data-stu-id="bdd79-112">Highly secure</span></span>

<span data-ttu-id="bdd79-113">ExpressRoute 带来了许多进一步的好处, 例如:</span><span class="sxs-lookup"><span data-stu-id="bdd79-113">ExpressRoute brings a number of further benefits, such as:</span></span>

- <span data-ttu-id="bdd79-114">与所有受支持的 Azure 服务的连接</span><span class="sxs-lookup"><span data-stu-id="bdd79-114">Connectivity to all supported Azure services</span></span>

- <span data-ttu-id="bdd79-115">与所有区域的全局连接 (需要高级附加项)</span><span class="sxs-lookup"><span data-stu-id="bdd79-115">Global connectivity to all regions (requires premium add-on)</span></span>

- <span data-ttu-id="bdd79-116">动态路由边界网关协议</span><span class="sxs-lookup"><span data-stu-id="bdd79-116">Dynamic routing over Border Gateway Protocol</span></span>

- <span data-ttu-id="bdd79-117">连接正常运行时间的服务级别协议 (sla)</span><span class="sxs-lookup"><span data-stu-id="bdd79-117">Service-level agreements (SLAs) for connection uptime</span></span>

- <span data-ttu-id="bdd79-118">Skype for business 的服务质量 (QoS)</span><span class="sxs-lookup"><span data-stu-id="bdd79-118">Quality of Service (QoS) for Skype for Business</span></span>

<span data-ttu-id="bdd79-119">此外, 还提供了 ExpressRoute premium 加载项, 它提供了更多好处, 如增加路由限制、全局服务连接和每个电路增加的虚拟网络链路。</span><span class="sxs-lookup"><span data-stu-id="bdd79-119">Additionally, there's the ExpressRoute premium add-on, which offers benefits such as increased route limits, global service connectivity, and increased virtual network links per circuit.</span></span>

## <a name="expressroute-connectivity-models"></a><span data-ttu-id="bdd79-120">ExpressRoute 连接模型</span><span class="sxs-lookup"><span data-stu-id="bdd79-120">ExpressRoute connectivity models</span></span>

<span data-ttu-id="bdd79-121">可以通过以下机制连接到 ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="bdd79-121">Connections into ExpressRoute can be through the following mechanisms:</span></span>

- <span data-ttu-id="bdd79-122">IP VPN 网络 (任意对任意)</span><span class="sxs-lookup"><span data-stu-id="bdd79-122">IP VPN network (any-to-any)</span></span>

- <span data-ttu-id="bdd79-123">通过以太网交换的虚拟交叉连接</span><span class="sxs-lookup"><span data-stu-id="bdd79-123">Virtual cross-connection through an Ethernet exchange</span></span>

- <span data-ttu-id="bdd79-124">点到点以太网连接</span><span class="sxs-lookup"><span data-stu-id="bdd79-124">Point-to-point Ethernet connection</span></span>

 <span data-ttu-id="bdd79-125">ExpressRoute 功能和功能在上述所有连接模型中都完全相同。</span><span class="sxs-lookup"><span data-stu-id="bdd79-125">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span></span>

### <a name="what-is-layer-3-connectivity"></a><span data-ttu-id="bdd79-126">什么是第3层连接？</span><span class="sxs-lookup"><span data-stu-id="bdd79-126">What is layer 3 connectivity?</span></span>

<span data-ttu-id="bdd79-127">Microsoft 使用行业标准的动态路由协议 (BGP) 在你的本地网络、Azure 中的实例和 Microsoft 公用地址之间的 exchange 路由。</span><span class="sxs-lookup"><span data-stu-id="bdd79-127">Microsoft uses an industry-standard dynamic routing protocol (BGP) to exchange routes between your on-premises network, your instances in Azure, and Microsoft public addresses.</span></span> <span data-ttu-id="bdd79-128">我们为不同的流量配置文件为你的网络建立了多个 BGP 会话。</span><span class="sxs-lookup"><span data-stu-id="bdd79-128">We establish multiple BGP sessions with your network for different traffic profiles.</span></span>

### <a name="any-to-any-ipvpn-networks"></a><span data-ttu-id="bdd79-129">"任意对任意" (IPVPN) 网络</span><span class="sxs-lookup"><span data-stu-id="bdd79-129">Any-to-any (IPVPN) networks</span></span>

<span data-ttu-id="bdd79-130">IPVPN 提供程序通常在托管的第3层连接上提供分支机构和公司数据中心之间的连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-130">IPVPN providers typically provide connectivity between branch offices and your corporate datacenter over managed layer 3 connections.</span></span> <span data-ttu-id="bdd79-131">在 ExpressRoute 中, Azure 数据中心看起来好像是另一个分支机构。</span><span class="sxs-lookup"><span data-stu-id="bdd79-131">With ExpressRoute, the Azure datacenters appear as if they were another branch office.</span></span>

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a><span data-ttu-id="bdd79-132">通过以太网交换的虚拟交叉连接</span><span class="sxs-lookup"><span data-stu-id="bdd79-132">Virtual cross-connection through an Ethernet Exchange</span></span>

<span data-ttu-id="bdd79-133">如果你的组织与云 exchange 设施共同存在, 则你可以请求与 Microsoft 云的交叉连接, 但提供商的以太网交换。</span><span class="sxs-lookup"><span data-stu-id="bdd79-133">If your organization is co-located with a cloud exchange facility, you request cross-connections to the Microsoft Cloud though your provider's Ethernet exchange.</span></span> <span data-ttu-id="bdd79-134">与 Microsoft 云的这些跨连接可在第2层或第3层托管连接上运行, 如网络 OSI 模型中所示。</span><span class="sxs-lookup"><span data-stu-id="bdd79-134">These cross-connections to the Microsoft Cloud can operate at either layer 2 or layer 3 managed connections, as in the networking OSI model.</span></span>

### <a name="point-to-point-ethernet-connection"></a><span data-ttu-id="bdd79-135">点到点以太网连接</span><span class="sxs-lookup"><span data-stu-id="bdd79-135">Point-to-point Ethernet connection</span></span>

<span data-ttu-id="bdd79-136">点对点以太网链接可以在你的本地数据中心或分支之间为 Microsoft 云提供第2层或托管的第3层连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-136">Point-to-point Ethernet links can provide layer 2 or managed layer 3 connections between your on-premises datacenters or offices to the Microsoft Cloud.</span></span>

## <a name="how-expressroute-works"></a><span data-ttu-id="bdd79-137">ExpressRoute 的工作原理</span><span class="sxs-lookup"><span data-stu-id="bdd79-137">How ExpressRoute works</span></span>

<span data-ttu-id="bdd79-138">Azure ExpressRoute 使用 ExpressRoute 电路和路由域的组合来提供到 Microsoft 云的高带宽连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-138">Azure ExpressRoute uses a combination of ExpressRoute circuits and routing domains to provide high-bandwidth connectivity to the Microsoft Cloud.</span></span>

### <a name="what-are-expressroute-circuits"></a><span data-ttu-id="bdd79-139">什么是 ExpressRoute 电路</span><span class="sxs-lookup"><span data-stu-id="bdd79-139">What are ExpressRoute circuits</span></span>

<span data-ttu-id="bdd79-140">ExpressRoute 电路是你的本地基础结构与 Microsoft 云之间的逻辑连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-140">An ExpressRoute circuit is the logical connection between your on-premises infrastructure and the Microsoft Cloud.</span></span> <span data-ttu-id="bdd79-141">虽然某些组织出于冗余原因而使用多个连接提供程序, 但连接提供程序实现了该连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-141">A connectivity provider implements that connection, although some organizations use multiple connectivity providers for redundancy reasons.</span></span> <span data-ttu-id="bdd79-142">每个电路的固定带宽为50、100、200 Mbps 或 500 mbps 或 1 gbps 或 10 Gbps, 这些电路中的每一个都映射到一个连接提供程序和一个对等位置。</span><span class="sxs-lookup"><span data-stu-id="bdd79-142">Each circuit has a fixed bandwidth of either 50, 100, 200 Mbps or 500 Mbps, or 1 Gbps or 10 Gbps, and each of those circuits map to a connectivity provider and a peering location.</span></span> <span data-ttu-id="bdd79-143">此外, 每个 ExpressRoute 电路都具有默认配额和限制。</span><span class="sxs-lookup"><span data-stu-id="bdd79-143">In addition, each ExpressRoute circuit has default quotas and limits.</span></span>

<span data-ttu-id="bdd79-144">ExpressRoute 电路与网络连接或网络设备不等效。</span><span class="sxs-lookup"><span data-stu-id="bdd79-144">An ExpressRoute circuit isn't equivalent to a network connection or a network device.</span></span> <span data-ttu-id="bdd79-145">每个电路由 GUID (称为_服务_或_s 键_) 定义。</span><span class="sxs-lookup"><span data-stu-id="bdd79-145">Each circuit is defined by a GUID, called a _service_ or _s-key_.</span></span> <span data-ttu-id="bdd79-146">此密钥提供了 Microsoft、连接提供程序和组织之间的连接链接-它不是加密机密。</span><span class="sxs-lookup"><span data-stu-id="bdd79-146">This s-key provides the connectivity link between Microsoft, your connectivity provider, and your organization - it isn't a cryptographic secret.</span></span> <span data-ttu-id="bdd79-147">每个 s 键都具有到 Azure ExpressRoute 电路的一对一映射。</span><span class="sxs-lookup"><span data-stu-id="bdd79-147">Each s-key has a one-to-one mapping to an Azure ExpressRoute circuit.</span></span>

<span data-ttu-id="bdd79-148">每个电路最长可包含三个 peerings, 这是为实现冗余而配置的一对 BGP 会话。</span><span class="sxs-lookup"><span data-stu-id="bdd79-148">Each circuit can have up to three peerings, which are a pair of BGP sessions that are configured for redundancy.</span></span> <span data-ttu-id="bdd79-149">它们是:</span><span class="sxs-lookup"><span data-stu-id="bdd79-149">They are:</span></span>

- <span data-ttu-id="bdd79-150">Azure 专用</span><span class="sxs-lookup"><span data-stu-id="bdd79-150">Azure private</span></span>
- <span data-ttu-id="bdd79-151">Azure 公共</span><span class="sxs-lookup"><span data-stu-id="bdd79-151">Azure public</span></span>
- <span data-ttu-id="bdd79-152">word</span><span class="sxs-lookup"><span data-stu-id="bdd79-152">Microsoft</span></span>

### <a name="routing-domains"></a><span data-ttu-id="bdd79-153">路由域</span><span class="sxs-lookup"><span data-stu-id="bdd79-153">Routing domains</span></span>

<span data-ttu-id="bdd79-154">然后, expressroute 电路映射到路由域, 每个 expressroute 电路包含多个路由域。</span><span class="sxs-lookup"><span data-stu-id="bdd79-154">ExpressRoute circuits then map to routing domains, with each ExpressRoute circuit having multiple routing domains.</span></span> <span data-ttu-id="bdd79-155">这些域与上面列出的三个 peerings 相同。</span><span class="sxs-lookup"><span data-stu-id="bdd79-155">These domains are the same as the three peerings listed above.</span></span> <span data-ttu-id="bdd79-156">在主动-主动配置中, 每对路由器都具有相同的配置, 从而提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="bdd79-156">In an active-active configuration, each pair of routers would have each routing domain configured identically, thus providing high availability.</span></span> <span data-ttu-id="bdd79-157">azure public 和 azure 私有对等名称代表 IP 寻址方案。</span><span class="sxs-lookup"><span data-stu-id="bdd79-157">The Azure public and Azure private peering names represent the IP addressing schemes.</span></span>

#### <a name="azure-private-peering"></a><span data-ttu-id="bdd79-158">Azure 专用对等</span><span class="sxs-lookup"><span data-stu-id="bdd79-158">Azure private peering</span></span>

<span data-ttu-id="bdd79-159">azure 专用对连接到 azure 计算服务 (例如, 虚拟机和与虚拟网络一起部署的云服务)。</span><span class="sxs-lookup"><span data-stu-id="bdd79-159">Azure private peering connects to Azure compute services such as virtual machines and cloud services that are deployed with a virtual network.</span></span> <span data-ttu-id="bdd79-160">就安全性而言, 专用对等域只是将本地网络扩展到 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="bdd79-160">As far as security goes, the private peering domain is simply an extension of your on-premises network into Azure.</span></span> <span data-ttu-id="bdd79-161">然后, 在该网络和任何 Azure 虚拟网络之间启用双向连接, 使 azure VM IP 地址在内部网络中可见。</span><span class="sxs-lookup"><span data-stu-id="bdd79-161">You then enable bidirectional connectivity between that network and any Azure virtual networks, making the Azure VM IP addresses visible within your internal network.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd79-162">只能将一个虚拟网络连接到专用对等域。</span><span class="sxs-lookup"><span data-stu-id="bdd79-162">You can connect only one virtual network to the private peering domain.</span></span>

#### <a name="azure-public-peering"></a><span data-ttu-id="bdd79-163">Azure 公共对等</span><span class="sxs-lookup"><span data-stu-id="bdd79-163">Azure public peering</span></span>

<span data-ttu-id="bdd79-164">azure 公共对等启用与公用 IP 地址 (如 azure 存储、azure SQL 数据库和 azure web 服务) 上可用的服务的专用连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-164">Azure public peering enables private connections to services that are available on public IP addresses, such as Azure Storage, Azure SQL databases, and Azure web services.</span></span> <span data-ttu-id="bdd79-165">通过公共对等, 您可以连接到这些服务公用 IP 地址, 而无需通过 Internet 路由流量。</span><span class="sxs-lookup"><span data-stu-id="bdd79-165">With public peering, you can connect to those service public IP addresses without your traffic being routed over the Internet.</span></span> <span data-ttu-id="bdd79-166">连接始终从您的 WAN 连接到 Azure, 而不是其他方面。</span><span class="sxs-lookup"><span data-stu-id="bdd79-166">Connectivity is always from your WAN to Azure, not the other way around.</span></span> <span data-ttu-id="bdd79-167">这也是一种全或无方法, 因为您无法选择您想启用公共对等的服务。</span><span class="sxs-lookup"><span data-stu-id="bdd79-167">This is also an all-or-nothing approach, as you can't select the services for which you want public peering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd79-168">对于 Azure PaaS 服务, 建议使用 Microsoft 对等, 而不是公共对等。</span><span class="sxs-lookup"><span data-stu-id="bdd79-168">For Azure PaaS services, it's recommended to use Microsoft peering rather than public peering.</span></span>

#### <a name="microsoft-peering"></a><span data-ttu-id="bdd79-169">Microsoft 对等</span><span class="sxs-lookup"><span data-stu-id="bdd79-169">Microsoft peering</span></span>

<span data-ttu-id="bdd79-170">Microsoft 对等支持与基于云的 SaaS 产品 (如 Office 365 和 Dynamics 365) 的连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-170">Microsoft peering supports connections to cloud-based SaaS offerings, such as Office 365 and Dynamics 365.</span></span> <span data-ttu-id="bdd79-171">此对等选项在公司的 WAN 和 Microsoft 云服务之间提供双向连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-171">This peering option provides bi-directional connectivity between your company's WAN and Microsoft cloud services.</span></span>

### <a name="expressroute-health"></a><span data-ttu-id="bdd79-172">ExpressRoute 运行状况</span><span class="sxs-lookup"><span data-stu-id="bdd79-172">ExpressRoute health</span></span>

<span data-ttu-id="bdd79-173">与 Microsoft Azure 中的大多数功能一样, 您可以监视 ExpressRoute 连接以确保它们的执行满意。</span><span class="sxs-lookup"><span data-stu-id="bdd79-173">As with most features in Microsoft Azure, you can monitor ExpressRoute connections to ensure that they are performing satisfactorily.</span></span> <span data-ttu-id="bdd79-174">监视涵盖以下方面:</span><span class="sxs-lookup"><span data-stu-id="bdd79-174">Monitoring includes coverage of the following areas:</span></span>

- <span data-ttu-id="bdd79-175">可用率</span><span class="sxs-lookup"><span data-stu-id="bdd79-175">Availability</span></span>
- <span data-ttu-id="bdd79-176">与虚拟网络的连接</span><span class="sxs-lookup"><span data-stu-id="bdd79-176">Connectivity to virtual networks</span></span>
- <span data-ttu-id="bdd79-177">带宽利用率</span><span class="sxs-lookup"><span data-stu-id="bdd79-177">Bandwidth utilization</span></span>

<span data-ttu-id="bdd79-178">此监视活动的关键工具是网络性能监视器, 尤其是 ExpressRoute 的 NPM。</span><span class="sxs-lookup"><span data-stu-id="bdd79-178">The key tool for this monitoring activity is Network Performance Monitor, particularly NPM for ExpressRoute.</span></span>

<span data-ttu-id="bdd79-179">azure ExpressRoute 用于在你的内部部署中或在 colocation 环境中创建 azure 数据中心和基础结构之间的专用连接。</span><span class="sxs-lookup"><span data-stu-id="bdd79-179">Azure ExpressRoute is used to create private connections between Azure datacenters and infrastructure on your premises or in a colocation environment.</span></span> <span data-ttu-id="bdd79-180">ExpressRoute 连接不通过公共 internet, 它们提供更高的可靠性、更快的速度和比典型的 Internet 连接更低的延迟。</span><span class="sxs-lookup"><span data-stu-id="bdd79-180">ExpressRoute connections don't go over the public Internet, and they offer more reliability, faster speeds, and lower latencies than typical Internet connections.</span></span>
