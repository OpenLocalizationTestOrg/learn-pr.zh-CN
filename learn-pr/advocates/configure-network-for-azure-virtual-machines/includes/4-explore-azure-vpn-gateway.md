<span data-ttu-id="4c368-101">若要将您的本地环境与 Azure 集成, 您需要能够创建加密连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-101">To integrate your on-premises environment with Azure, you need the ability to create an encrypted connection.</span></span> <span data-ttu-id="4c368-102">您可以通过 Internet 或通过专用链接进行连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-102">You can connect over the Internet or over a dedicated link.</span></span> <span data-ttu-id="4c368-103">在这里, 我们将查看 Azure VPN 网关, 该网关提供来自本地环境的传入连接的终结点。</span><span class="sxs-lookup"><span data-stu-id="4c368-103">Here, we'll look at Azure VPN Gateway, which provides an endpoint for incoming connections from on-premises environments.</span></span>

<span data-ttu-id="4c368-104">你已设置 azure 虚拟网络, 并需要确保从 azure 到你的网站以及在 azure 虚拟网络之间的任何数据传输均已加密。</span><span class="sxs-lookup"><span data-stu-id="4c368-104">You have set up an Azure virtual network and need to ensure that any data transfers from Azure to your site and between Azure virtual networks are encrypted.</span></span> <span data-ttu-id="4c368-105">此外, 还需要了解如何在区域和订阅之间连接虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="4c368-105">You also need to know how to connect virtual networks between regions and subscriptions.</span></span>

## <a name="what-is-a-vpn-gateway"></a><span data-ttu-id="4c368-106">什么是 VPN 网关？</span><span class="sxs-lookup"><span data-stu-id="4c368-106">What is a VPN gateway?</span></span>

<span data-ttu-id="4c368-107">azure VPN 网关提供了一个终结点, 用于从内部部署位置到 Azure 通过 Internet 传入加密连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-107">An Azure VPN gateway provides an endpoint for incoming encrypted connections from on-premises locations to Azure over the Internet.</span></span> <span data-ttu-id="4c368-108">它还可以在 Microsoft 专用网络上的 azure 虚拟网络之间发送加密的流量, 该网络在不同区域中链接 azure 数据中心。</span><span class="sxs-lookup"><span data-stu-id="4c368-108">It can also send encrypted traffic between Azure virtual networks over Microsoft's dedicated network that links Azure datacenters in different regions.</span></span> <span data-ttu-id="4c368-109">此配置使您可以安全地链接不同区域中的虚拟机和服务。</span><span class="sxs-lookup"><span data-stu-id="4c368-109">This configuration allows you to link virtual machines and services in different regions securely.</span></span>

<span data-ttu-id="4c368-110">每个虚拟网络只能有一个 VPN 网关。</span><span class="sxs-lookup"><span data-stu-id="4c368-110">Each virtual network can have only one VPN gateway.</span></span> <span data-ttu-id="4c368-111">与该 VPN 网关的所有连接都共享可用的网络带宽。</span><span class="sxs-lookup"><span data-stu-id="4c368-111">All connections to that VPN gateway share the available network bandwidth.</span></span>

<span data-ttu-id="4c368-112">在每个虚拟网络网关中有两个或多个虚拟机 (vm)。</span><span class="sxs-lookup"><span data-stu-id="4c368-112">Within each virtual network gateway there are two or more virtual machines (VMs).</span></span> <span data-ttu-id="4c368-113">这些虚拟机已部署到您指定的特殊子网, 称为_网关子网_。</span><span class="sxs-lookup"><span data-stu-id="4c368-113">These VMs have been deployed to a special subnet that you specify, called the _gateway subnet_.</span></span> <span data-ttu-id="4c368-114">它们包含与其他网络的连接的路由表, 以及特定的网关服务。</span><span class="sxs-lookup"><span data-stu-id="4c368-114">They contain routing tables for connections to other networks, along with specific gateway services.</span></span> <span data-ttu-id="4c368-115">这些虚拟机和网关子网类似于强化的网络设备。</span><span class="sxs-lookup"><span data-stu-id="4c368-115">These VMs and the gateway subnet are similar to a hardened network device.</span></span> <span data-ttu-id="4c368-116">您无需直接配置这些虚拟机, 也不应将任何其他资源部署到网关子网中。</span><span class="sxs-lookup"><span data-stu-id="4c368-116">You don't need to configure these VMs directly and should not deploy any additional resources into the gateway subnet.</span></span>

<span data-ttu-id="4c368-117">创建虚拟网络网关可能需要一些时间才能完成, 因此您必须进行适当的规划, 这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="4c368-117">Creating a virtual network gateway can take some time to complete, so it's vital that you plan appropriately.</span></span> <span data-ttu-id="4c368-118">创建虚拟网络网关时, 设置过程将生成网关虚拟机并将其部署到网关子网。</span><span class="sxs-lookup"><span data-stu-id="4c368-118">When you create a virtual network gateway, the provisioning process generates the gateway VMs and deploys them to the gateway subnet.</span></span> <span data-ttu-id="4c368-119">这些虚拟机将具有您在网关上配置的设置。</span><span class="sxs-lookup"><span data-stu-id="4c368-119">These VMs will have the settings that you configure on the gateway.</span></span>

<span data-ttu-id="4c368-120">"密钥" 设置是**_网关类型_**, vpn 网关的类型为 "vpn"。</span><span class="sxs-lookup"><span data-stu-id="4c368-120">A key setting is the **_gateway type_**, which for a VPN gateway will be of type "vpn".</span></span> <span data-ttu-id="4c368-121">VPN 网关的选项包括:</span><span class="sxs-lookup"><span data-stu-id="4c368-121">Options for VPN gateways include:</span></span>

- <span data-ttu-id="4c368-122">通过 IPsec/IKE VPN 隧道的网络到网络连接, 将 VPN 网关链接到其他 vpn 网关。</span><span class="sxs-lookup"><span data-stu-id="4c368-122">Network-to-network connections over IPsec/IKE VPN tunneling, linking VPN gateways to other VPN gateways.</span></span>

- <span data-ttu-id="4c368-123">跨界 IPsec/IKE VPN 隧道, 用于通过专用的 VPN 设备将本地网络连接到 Azure, 以创建站点到站点连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-123">Cross-premises IPsec/IKE VPN tunneling, for connecting on-premises networks to Azure through dedicated VPN devices to create site-to-site connections.</span></span>

- <span data-ttu-id="4c368-124">通过 IKEv2 或 SSTP 的点到站点连接, 可将客户端计算机链接到 Azure 中的资源。</span><span class="sxs-lookup"><span data-stu-id="4c368-124">Point-to-site connections over IKEv2 or SSTP, to link client computers to resources in Azure.</span></span>

<span data-ttu-id="4c368-125">现在, 让我们来看看您在规划 VPN 网关时需要考虑的因素。</span><span class="sxs-lookup"><span data-stu-id="4c368-125">Now, let's look at the factors you need to consider for planning your VPN gateway.</span></span>

## <a name="plan-a-vpn-gateway"></a><span data-ttu-id="4c368-126">规划 VPN 网关</span><span class="sxs-lookup"><span data-stu-id="4c368-126">Plan a VPN gateway</span></span>

<span data-ttu-id="4c368-127">在规划 VPN 网关时, 需要考虑以下三个体系结构:</span><span class="sxs-lookup"><span data-stu-id="4c368-127">When you're planning a VPN gateway, there are three architectures to consider:</span></span>

- <span data-ttu-id="4c368-128">通过 Internet 指向网站</span><span class="sxs-lookup"><span data-stu-id="4c368-128">Point to site over the Internet</span></span>
- <span data-ttu-id="4c368-129">通过 Internet 的网站</span><span class="sxs-lookup"><span data-stu-id="4c368-129">Site to site over the Internet</span></span>
- <span data-ttu-id="4c368-130">通过专用网络的站点到站点, 如 Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4c368-130">Site to site over a dedicated network, such as Azure ExpressRoute</span></span>

### <a name="planning-factors"></a><span data-ttu-id="4c368-131">规划因素</span><span class="sxs-lookup"><span data-stu-id="4c368-131">Planning factors</span></span>

<span data-ttu-id="4c368-132">在规划过程中需要满足的因素包括:</span><span class="sxs-lookup"><span data-stu-id="4c368-132">Factors that you need to cover during your planning process include:</span></span>

- <span data-ttu-id="4c368-133">吞吐量-Mbps 或 Gbps</span><span class="sxs-lookup"><span data-stu-id="4c368-133">Throughput - Mbps or Gbps</span></span>
- <span data-ttu-id="4c368-134">主干-Internet 或专用？</span><span class="sxs-lookup"><span data-stu-id="4c368-134">Backbone - Internet or private?</span></span>
- <span data-ttu-id="4c368-135">公用 (静态) IP 地址的可用性</span><span class="sxs-lookup"><span data-stu-id="4c368-135">Availability of a public (static) IP address</span></span>
- <span data-ttu-id="4c368-136">VPN 设备兼容性</span><span class="sxs-lookup"><span data-stu-id="4c368-136">VPN device compatibility</span></span>
- <span data-ttu-id="4c368-137">多个客户端连接或站点到站点链接？</span><span class="sxs-lookup"><span data-stu-id="4c368-137">Multiple client connections or a site-to-site link?</span></span>
- <span data-ttu-id="4c368-138">VPN 网关类型</span><span class="sxs-lookup"><span data-stu-id="4c368-138">VPN gateway type</span></span>
- <span data-ttu-id="4c368-139">Azure VPN 网关 SKU</span><span class="sxs-lookup"><span data-stu-id="4c368-139">Azure VPN Gateway SKU</span></span>

<span data-ttu-id="4c368-140">下表汇总了其中一些规划问题。</span><span class="sxs-lookup"><span data-stu-id="4c368-140">The following table summarizes some of these planning issues.</span></span> <span data-ttu-id="4c368-141">后面将对其余部分进行讨论。</span><span class="sxs-lookup"><span data-stu-id="4c368-141">The remainder are discussed later.</span></span>

|                           |  <span data-ttu-id="4c368-142">指向 "网站"</span><span class="sxs-lookup"><span data-stu-id="4c368-142">Point to site</span></span>            | <span data-ttu-id="4c368-143">站点到站点</span><span class="sxs-lookup"><span data-stu-id="4c368-143">Site to site</span></span>                          |  <span data-ttu-id="4c368-144">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4c368-144">ExpressRoute</span></span>                 |
| -------------             | -------------             | -------------                         | ---------                     |
| <span data-ttu-id="4c368-145">Azure 支持的服务</span><span class="sxs-lookup"><span data-stu-id="4c368-145">Azure supported services</span></span>  | <span data-ttu-id="4c368-146">云服务和虚拟机</span><span class="sxs-lookup"><span data-stu-id="4c368-146">Cloud services and VMs</span></span>    | <span data-ttu-id="4c368-147">云服务和虚拟机</span><span class="sxs-lookup"><span data-stu-id="4c368-147">Cloud services and VMs</span></span>                | <span data-ttu-id="4c368-148">所有受支持的服务</span><span class="sxs-lookup"><span data-stu-id="4c368-148">All supported services</span></span>        |
| <span data-ttu-id="4c368-149">典型带宽</span><span class="sxs-lookup"><span data-stu-id="4c368-149">Typical bandwidth</span></span>         | <span data-ttu-id="4c368-150">取决于 VPN 网关 SKU</span><span class="sxs-lookup"><span data-stu-id="4c368-150">Depends on VPN Gateway SKU</span></span>    | <span data-ttu-id="4c368-151">最高配置 1 Gbps 和聚合</span><span class="sxs-lookup"><span data-stu-id="4c368-151">Up to 1 Gbps with aggregation</span></span>         | <span data-ttu-id="4c368-152">从 50 Mbps 到 10 Gbps</span><span class="sxs-lookup"><span data-stu-id="4c368-152">From 50 Mbps to 10 Gbps</span></span>       |
| <span data-ttu-id="4c368-153">支持的协议</span><span class="sxs-lookup"><span data-stu-id="4c368-153">Protocols supported</span></span>       | <span data-ttu-id="4c368-154">SSTP 和 IPsec</span><span class="sxs-lookup"><span data-stu-id="4c368-154">SSTP and IPsec</span></span>            | <span data-ttu-id="4c368-155">IPsec</span><span class="sxs-lookup"><span data-stu-id="4c368-155">IPsec</span></span>                                 | <span data-ttu-id="4c368-156">直接连接、vlan</span><span class="sxs-lookup"><span data-stu-id="4c368-156">Direct connection, VLANs</span></span>      |
| <span data-ttu-id="4c368-157">路径</span><span class="sxs-lookup"><span data-stu-id="4c368-157">Routing</span></span>                   | <span data-ttu-id="4c368-158">RouteBased (动态)</span><span class="sxs-lookup"><span data-stu-id="4c368-158">RouteBased (dynamic)</span></span>      | <span data-ttu-id="4c368-159">PolicyBased (静态) 和 RouteBased</span><span class="sxs-lookup"><span data-stu-id="4c368-159">PolicyBased (static) and RouteBased</span></span>   | <span data-ttu-id="4c368-160">BGP</span><span class="sxs-lookup"><span data-stu-id="4c368-160">BGP</span></span>                           |
| <span data-ttu-id="4c368-161">连接弹性</span><span class="sxs-lookup"><span data-stu-id="4c368-161">Connection resiliency</span></span>     | <span data-ttu-id="4c368-162">主动-被动</span><span class="sxs-lookup"><span data-stu-id="4c368-162">Active-passive</span></span>            | <span data-ttu-id="4c368-163">主动-被动或主动-主动</span><span class="sxs-lookup"><span data-stu-id="4c368-163">Active-passive or active-active</span></span>       | <span data-ttu-id="4c368-164">主动-主动</span><span class="sxs-lookup"><span data-stu-id="4c368-164">Active-active</span></span>                 |
| <span data-ttu-id="4c368-165">用例</span><span class="sxs-lookup"><span data-stu-id="4c368-165">Use case</span></span>                  | <span data-ttu-id="4c368-166">测试和原型设计</span><span class="sxs-lookup"><span data-stu-id="4c368-166">Testing and prototyping</span></span>   | <span data-ttu-id="4c368-167">开发、测试和小型生产</span><span class="sxs-lookup"><span data-stu-id="4c368-167">Dev, test and small-scale production</span></span>  | <span data-ttu-id="4c368-168">企业/任务关键型</span><span class="sxs-lookup"><span data-stu-id="4c368-168">Enterprise/mission critical</span></span>   |

### <a name="gateway-skus"></a><span data-ttu-id="4c368-169">网关 sku</span><span class="sxs-lookup"><span data-stu-id="4c368-169">Gateway SKUs</span></span>

<span data-ttu-id="4c368-170">Azure 为网关服务提供以下 sku:</span><span class="sxs-lookup"><span data-stu-id="4c368-170">Azure offers the following SKUs for gateway services:</span></span>

| <span data-ttu-id="4c368-171">SKU</span><span class="sxs-lookup"><span data-stu-id="4c368-171">SKU</span></span>              |  <span data-ttu-id="4c368-172">S2S/网络到网络隧道</span><span class="sxs-lookup"><span data-stu-id="4c368-172">S2S/network-to-network tunnels</span></span> | <span data-ttu-id="4c368-173">P2S 连接</span><span class="sxs-lookup"><span data-stu-id="4c368-173">P2S connections</span></span>  |  <span data-ttu-id="4c368-174">聚合吞吐量基准</span><span class="sxs-lookup"><span data-stu-id="4c368-174">Aggregate throughput benchmark</span></span>   | <span data-ttu-id="4c368-175">用于</span><span class="sxs-lookup"><span data-stu-id="4c368-175">Use for</span></span>                         |
| -------------    | -------------             | -------------    | ---------                         | ---------                       |
| <span data-ttu-id="4c368-176">vba</span><span class="sxs-lookup"><span data-stu-id="4c368-176">Basic</span></span>            | <span data-ttu-id="4c368-177">最多10</span><span class="sxs-lookup"><span data-stu-id="4c368-177">Max 10</span></span>                    | <span data-ttu-id="4c368-178">最大128</span><span class="sxs-lookup"><span data-stu-id="4c368-178">Max 128</span></span>          | <span data-ttu-id="4c368-179">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="4c368-179">100 Mbps</span></span>                          | <span data-ttu-id="4c368-180">开发/测试/POC</span><span class="sxs-lookup"><span data-stu-id="4c368-180">Dev/test/POC</span></span>                    |
| <span data-ttu-id="4c368-181">VpnGw1</span><span class="sxs-lookup"><span data-stu-id="4c368-181">VpnGw1</span></span>           | <span data-ttu-id="4c368-182">最多30</span><span class="sxs-lookup"><span data-stu-id="4c368-182">Max 30</span></span>                    | <span data-ttu-id="4c368-183">最大128</span><span class="sxs-lookup"><span data-stu-id="4c368-183">Max 128</span></span>          | <span data-ttu-id="4c368-184">650 Mbps</span><span class="sxs-lookup"><span data-stu-id="4c368-184">650 Mbps</span></span>                          | <span data-ttu-id="4c368-185">生产/关键工作负载</span><span class="sxs-lookup"><span data-stu-id="4c368-185">Production/critical workloads</span></span>   |
| <span data-ttu-id="4c368-186">VpnGw2</span><span class="sxs-lookup"><span data-stu-id="4c368-186">VpnGw2</span></span>           | <span data-ttu-id="4c368-187">最多30</span><span class="sxs-lookup"><span data-stu-id="4c368-187">Max 30</span></span>                    | <span data-ttu-id="4c368-188">最大128</span><span class="sxs-lookup"><span data-stu-id="4c368-188">Max 128</span></span>          | <span data-ttu-id="4c368-189">1 Gbps</span><span class="sxs-lookup"><span data-stu-id="4c368-189">1 Gbps</span></span>                            | <span data-ttu-id="4c368-190">生产/关键工作负载</span><span class="sxs-lookup"><span data-stu-id="4c368-190">Production/critical workloads</span></span>   |
| <span data-ttu-id="4c368-191">VpnGw3</span><span class="sxs-lookup"><span data-stu-id="4c368-191">VpnGw3</span></span>           | <span data-ttu-id="4c368-192">最多30</span><span class="sxs-lookup"><span data-stu-id="4c368-192">Max 30</span></span>                    | <span data-ttu-id="4c368-193">最大128</span><span class="sxs-lookup"><span data-stu-id="4c368-193">Max 128</span></span>          | <span data-ttu-id="4c368-194">1.25 Gbps</span><span class="sxs-lookup"><span data-stu-id="4c368-194">1.25 Gbps</span></span>                          | <span data-ttu-id="4c368-195">生产/关键工作负载</span><span class="sxs-lookup"><span data-stu-id="4c368-195">Production/critical workloads</span></span>   |

> [!Note]
> <span data-ttu-id="4c368-196">请务必选择正确的 SKU。</span><span class="sxs-lookup"><span data-stu-id="4c368-196">It's important that you choose the right SKU.</span></span> <span data-ttu-id="4c368-197">如果您设置了不正确的 VPN 网关, 则必须将其关闭并重新生成网关, 这可能需要很长时间。</span><span class="sxs-lookup"><span data-stu-id="4c368-197">If you have set up your VPN gateway with the wrong one, you'll have to take it down and rebuild the gateway, which can be time consuming.</span></span>

## <a name="workflow"></a><span data-ttu-id="4c368-198">工作流</span><span class="sxs-lookup"><span data-stu-id="4c368-198">Workflow</span></span>

<span data-ttu-id="4c368-199">在使用 Azure 上的虚拟专用网络设计云连接策略时, 应应用以下工作流:</span><span class="sxs-lookup"><span data-stu-id="4c368-199">When designing a cloud connectivity strategy using virtual private networking on Azure, you should apply the following workflow:</span></span>

1. <span data-ttu-id="4c368-200">设计连接拓扑, 并列出所有连接网络的地址空间。</span><span class="sxs-lookup"><span data-stu-id="4c368-200">Design your connectivity topology, listing the address spaces for all connecting networks.</span></span>

1. <span data-ttu-id="4c368-201">创建 Azure 虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="4c368-201">Create an Azure virtual network.</span></span>

1. <span data-ttu-id="4c368-202">为虚拟网络创建 VPN 网关。</span><span class="sxs-lookup"><span data-stu-id="4c368-202">Create a VPN gateway for the virtual network.</span></span>

1. <span data-ttu-id="4c368-203">根据需要, 创建并配置到本地网络或其他虚拟网络的连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-203">Create and configure connections to on-premises networks or other virtual networks, as required.</span></span>

1. <span data-ttu-id="4c368-204">如果需要, 为 Azure VPN 网关创建和配置点到站点连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-204">If required, create and configure a point-to-site connection for your Azure VPN gateway.</span></span>

### <a name="design-considerations"></a><span data-ttu-id="4c368-205">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="4c368-205">Design considerations</span></span>

<span data-ttu-id="4c368-206">在设计 VPN 网关以连接虚拟网络时, 必须考虑以下因素:</span><span class="sxs-lookup"><span data-stu-id="4c368-206">When you design your VPN gateways to connect virtual networks, you must consider the following factors:</span></span>

- <span data-ttu-id="4c368-207">子网不能重叠</span><span class="sxs-lookup"><span data-stu-id="4c368-207">Subnets cannot overlap</span></span>

    <span data-ttu-id="4c368-208">一个位置中的子网不包含与另一个位置相同的地址空间, 这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="4c368-208">It is vital that a subnet in one location does not contain the same address space as in another location.</span></span>

- <span data-ttu-id="4c368-209">IP 地址必须是唯一的</span><span class="sxs-lookup"><span data-stu-id="4c368-209">IP addresses must be unique</span></span>

    <span data-ttu-id="4c368-210">在不同位置不能有两个具有相同 IP 地址的主机, 因为这两个主机之间的通信无法路由, 网络到网络连接将会失败。</span><span class="sxs-lookup"><span data-stu-id="4c368-210">You cannot have two hosts with the same IP address in different locations, as it will be impossible to route traffic between those two hosts and the network-to-network connection will fail.</span></span>

- <span data-ttu-id="4c368-211">VPN 网关需要一个名为**GatewaySubnet**的网关子网</span><span class="sxs-lookup"><span data-stu-id="4c368-211">VPN gateways need a gateway subnet called **GatewaySubnet**</span></span>

    <span data-ttu-id="4c368-212">它必须具有此名称, 网关才能正常工作, 并且它不应包含任何其他资源。</span><span class="sxs-lookup"><span data-stu-id="4c368-212">It must have this name for the gateway to work, and it should not contain any other resources.</span></span>

### <a name="create-an-azure-virtual-network"></a><span data-ttu-id="4c368-213">创建 Azure 虚拟网络</span><span class="sxs-lookup"><span data-stu-id="4c368-213">Create an Azure virtual network</span></span>

<span data-ttu-id="4c368-214">在创建 VPN 网关之前, 需要创建 Azure 虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="4c368-214">Before you create a VPN gateway, you need to create the Azure virtual network.</span></span>

### <a name="create-a-vpn-gateway"></a><span data-ttu-id="4c368-215">创建 VPN 网关</span><span class="sxs-lookup"><span data-stu-id="4c368-215">Create a VPN gateway</span></span>

<span data-ttu-id="4c368-216">您创建的 VPN 网关的类型将取决于您的体系结构。</span><span class="sxs-lookup"><span data-stu-id="4c368-216">The type of VPN gateway you create will depend on your architecture.</span></span> <span data-ttu-id="4c368-217">选项包括:</span><span class="sxs-lookup"><span data-stu-id="4c368-217">Options are:</span></span>

- <span data-ttu-id="4c368-218">RouteBased</span><span class="sxs-lookup"><span data-stu-id="4c368-218">RouteBased</span></span>

    <span data-ttu-id="4c368-219">基于路由的 VPN 设备使用任意对任意 (通配符) 流量选择器, 并允许路由/转发表将通信定向到不同的 IPsec 隧道。</span><span class="sxs-lookup"><span data-stu-id="4c368-219">Route-based VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="4c368-220">基于路由的连接通常建立在路由器平台上, 其中每个 IPsec 隧道都作为网络接口或 VTI (虚拟隧道接口) 进行建模。</span><span class="sxs-lookup"><span data-stu-id="4c368-220">Route-based connections are typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

- <span data-ttu-id="4c368-221">PolicyBased</span><span class="sxs-lookup"><span data-stu-id="4c368-221">PolicyBased</span></span>

    <span data-ttu-id="4c368-222">基于策略的 VPN 设备使用这两个网络中的前缀的组合来定义如何通过 IPsec 隧道对流量进行加密/解密。</span><span class="sxs-lookup"><span data-stu-id="4c368-222">Policy-based VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="4c368-223">基于策略的连接通常建立在执行数据包筛选的防火墙设备上。</span><span class="sxs-lookup"><span data-stu-id="4c368-223">A policy-based connection is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="4c368-224">IPsec 隧道加密和解密将添加到数据包筛选和处理引擎中。</span><span class="sxs-lookup"><span data-stu-id="4c368-224">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>

## <a name="set-up-a-vpn-gateway"></a><span data-ttu-id="4c368-225">设置 VPN 网关</span><span class="sxs-lookup"><span data-stu-id="4c368-225">Set up a VPN gateway</span></span>

<span data-ttu-id="4c368-226">您需要执行的步骤取决于要安装的 VPN 网关的类型。</span><span class="sxs-lookup"><span data-stu-id="4c368-226">The steps you need to take will depend on the type of VPN gateway that you are installing.</span></span> <span data-ttu-id="4c368-227">例如, 若要使用 Azure 门户创建点到站点 VPN 网关, 请执行以下步骤:</span><span class="sxs-lookup"><span data-stu-id="4c368-227">For example, to create a point-to-site VPN gateway by using the Azure portal, you would carry out the following steps:</span></span>

1. <span data-ttu-id="4c368-228">创建虚拟网络</span><span class="sxs-lookup"><span data-stu-id="4c368-228">Create a virtual network</span></span>

2. <span data-ttu-id="4c368-229">添加网关子网</span><span class="sxs-lookup"><span data-stu-id="4c368-229">Add a gateway subnet</span></span>

3. <span data-ttu-id="4c368-230">指定 DNS 服务器 (可选)</span><span class="sxs-lookup"><span data-stu-id="4c368-230">Specify a DNS server (optional)</span></span>

4. <span data-ttu-id="4c368-231">创建虚拟网络网关</span><span class="sxs-lookup"><span data-stu-id="4c368-231">Create a virtual network gateway</span></span>

5. <span data-ttu-id="4c368-232">生成证书</span><span class="sxs-lookup"><span data-stu-id="4c368-232">Generate certificates</span></span>

6. <span data-ttu-id="4c368-233">添加客户端地址池</span><span class="sxs-lookup"><span data-stu-id="4c368-233">Add the client address pool</span></span>

7. <span data-ttu-id="4c368-234">配置隧道类型</span><span class="sxs-lookup"><span data-stu-id="4c368-234">Configure the tunnel type</span></span>

8. <span data-ttu-id="4c368-235">配置身份验证类型</span><span class="sxs-lookup"><span data-stu-id="4c368-235">Configure the authentication type</span></span>

9. <span data-ttu-id="4c368-236">上传根证书公共证书数据</span><span class="sxs-lookup"><span data-stu-id="4c368-236">Upload the root certificate public certificate data</span></span>

10. <span data-ttu-id="4c368-237">安装导出的客户端证书</span><span class="sxs-lookup"><span data-stu-id="4c368-237">Install an exported client certificate</span></span>

11. <span data-ttu-id="4c368-238">生成并安装 VPN 客户端配置包</span><span class="sxs-lookup"><span data-stu-id="4c368-238">Generate and install the VPN client configuration package</span></span>

12. <span data-ttu-id="4c368-239">连接到 Azure</span><span class="sxs-lookup"><span data-stu-id="4c368-239">Connect to Azure</span></span>

<span data-ttu-id="4c368-240">由于存在多个具有多个选项的 Azure VPN 网关的配置路径, 因此不可能在此课程中涵盖每个设置。</span><span class="sxs-lookup"><span data-stu-id="4c368-240">As there are several configuration paths with Azure VPN gateways, each with multiple options, it is not possible to cover every setup in this course.</span></span> <span data-ttu-id="4c368-241">有关详细信息, 请参阅 "其他资源" 部分。</span><span class="sxs-lookup"><span data-stu-id="4c368-241">For more information, see the Additional Resources section.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="4c368-242">配置网关</span><span class="sxs-lookup"><span data-stu-id="4c368-242">Configure the gateway</span></span>

<span data-ttu-id="4c368-243">创建网关后, 你需要对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="4c368-243">Once your gateway is created, you'll need to configure it.</span></span>  <span data-ttu-id="4c368-244">需要提供几个配置设置, 如名称、位置、DNS 服务器等。在练习中, 我们将更详细地介绍这些内容。</span><span class="sxs-lookup"><span data-stu-id="4c368-244">There are several configuration settings you will need to provide, such as the name, location, DNS server, etc. We will go into these in more detail in the exercise.</span></span>

<span data-ttu-id="4c368-245">azure VPN 网关是 azure 虚拟网络中的一个组件, 可启用点到站点、站点到站点或网络到网络的连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-245">Azure VPN gateways are a component in Azure virtual networks that enable point-to-site, site-to-site, or network-to-network connections.</span></span> <span data-ttu-id="4c368-246">azure VPN 网关使单个客户端计算机能够连接到 azure 中的资源, 将本地网络扩展到 azure, 或者促进不同区域和订阅中的虚拟网络之间的连接。</span><span class="sxs-lookup"><span data-stu-id="4c368-246">Azure VPN gateways enable individual client computers to connect to resources in Azure, extend on-premises networks into Azure, or facilitate connections between virtual networks in different regions and subscriptions.</span></span>
