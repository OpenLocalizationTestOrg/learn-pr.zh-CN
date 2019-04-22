<span data-ttu-id="f834c-101">现在, 你的网站已启动并在 Azure 上运行。</span><span class="sxs-lookup"><span data-stu-id="f834c-101">You now have your site up and running on Azure.</span></span> <span data-ttu-id="f834c-102">但如何帮助确保您的网站运行的是24/7？</span><span class="sxs-lookup"><span data-stu-id="f834c-102">But how can you help ensure your site is running 24/7?</span></span>

<span data-ttu-id="f834c-103">例如, 当您需要进行每周维护时, 会发生什么？</span><span class="sxs-lookup"><span data-stu-id="f834c-103">For instance, what happens when you need to do weekly maintenance?</span></span> <span data-ttu-id="f834c-104">在维护时段内, 你的服务仍将不可用。</span><span class="sxs-lookup"><span data-stu-id="f834c-104">Your service will still be unavailable during your maintenance window.</span></span> <span data-ttu-id="f834c-105">而且, 由于你的网站在全球范围内获得了用户, 因此没有合适的时间将系统用于维护。</span><span class="sxs-lookup"><span data-stu-id="f834c-105">And because your site reaches users all over the world, there's no good time to take down your systems for maintenance.</span></span> <span data-ttu-id="f834c-106">如果同时连接的用户太多, 也可能会遇到性能问题。</span><span class="sxs-lookup"><span data-stu-id="f834c-106">You may also run into performance issues if too many users connect at the same time.</span></span>

## <a name="what-are-availability-and-high-availability"></a><span data-ttu-id="f834c-107">什么是可用性和高可用性？</span><span class="sxs-lookup"><span data-stu-id="f834c-107">What are availability and high availability?</span></span>

:::row:::
  :::column:::
    ![表示高可用性的速度培训](../media/3-availability.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="f834c-109">_可用性_是指您的服务在不中断的情况下运行多长时间。</span><span class="sxs-lookup"><span data-stu-id="f834c-109">_Availability_ refers to how long your service is up and running without interruption.</span></span> <span data-ttu-id="f834c-110">_高可用性_或_高_可用性是指在很长一段时间内启动和运行的服务。</span><span class="sxs-lookup"><span data-stu-id="f834c-110">_High availability_, or _highly available_, refers to a service that's up and running for a long period of time.</span></span>

<span data-ttu-id="f834c-111">您知道当您无法访问所需信息时, 有什么麻烦。</span><span class="sxs-lookup"><span data-stu-id="f834c-111">You know how frustrating it is when you can't access the information you need.</span></span> <span data-ttu-id="f834c-112">试想一下你每天访问的社交媒体或新闻网站。</span><span class="sxs-lookup"><span data-stu-id="f834c-112">Think of a social media or news site that you visit daily.</span></span> <span data-ttu-id="f834c-113">您是否可以始终访问网站, 或者您是否经常看到类似于 "503 服务不可用" 的错误消息？</span><span class="sxs-lookup"><span data-stu-id="f834c-113">Can you always access the site, or do you often see error messages like "503 Service Unavailable"?</span></span>
  :::column-end:::
 :::row-end:::

<span data-ttu-id="f834c-114">您可能会听到类似 "五个9的可用性" 的术语。</span><span class="sxs-lookup"><span data-stu-id="f834c-114">You may have heard terms like "five nines availability."</span></span> <span data-ttu-id="f834c-115">"五个 9" 的可用性是指保证服务运行的是 99.999% 的时间。</span><span class="sxs-lookup"><span data-stu-id="f834c-115">Five nines availability means that the service is guaranteed to be running 99.999 percent of the time.</span></span> <span data-ttu-id="f834c-116">虽然很难实现 100% 的可用性, 但许多团队至少要努力5个九。</span><span class="sxs-lookup"><span data-stu-id="f834c-116">Although it's difficult to achieve 100 percent availability, many teams strive for at least five nines.</span></span>

## <a name="what-is-resiliency"></a><span data-ttu-id="f834c-117">什么是弹性？</span><span class="sxs-lookup"><span data-stu-id="f834c-117">What is resiliency?</span></span>

:::row:::
  :::column:::
    ![表示弹性的运行状况图](../media/3-resiliency.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="f834c-119">_复原_是指系统在异常情况中保持运行的功能。</span><span class="sxs-lookup"><span data-stu-id="f834c-119">_Resiliency_ refers to a system's ability to stay operational during abnormal conditions.</span></span>

<span data-ttu-id="f834c-120">这些条件包括:</span><span class="sxs-lookup"><span data-stu-id="f834c-120">These conditions include:</span></span>

- <span data-ttu-id="f834c-121">自然灾难</span><span class="sxs-lookup"><span data-stu-id="f834c-121">Natural disasters</span></span>
- <span data-ttu-id="f834c-122">系统维护, 包括计划的和未计划的, 包括软件更新和安全修补程序。</span><span class="sxs-lookup"><span data-stu-id="f834c-122">System maintenance, both planned and unplanned, including software updates and security patches.</span></span>
- <span data-ttu-id="f834c-123">网站流量中的峰值</span><span class="sxs-lookup"><span data-stu-id="f834c-123">Spikes in traffic to your site</span></span>
- <span data-ttu-id="f834c-124">由恶意方 (如分布式拒绝服务或 DDoS 攻击) 所做的威胁</span><span class="sxs-lookup"><span data-stu-id="f834c-124">Threats made by malicious parties, such as distributed denial of service, or DDoS, attacks</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="f834c-125">设想您的市场营销团队希望进行快速促销, 以促进新的 vitamin 补充行为。</span><span class="sxs-lookup"><span data-stu-id="f834c-125">Imagine your marketing team wants to have a flash sale to promote a new line of vitamin supplements.</span></span> <span data-ttu-id="f834c-126">在这段时间内, 您可能会期待流量大的峰值。</span><span class="sxs-lookup"><span data-stu-id="f834c-126">You might expect a huge spike in traffic during this time.</span></span> <span data-ttu-id="f834c-127">此峰值可能会严重影响您的处理系统, 导致用户 disappointing 速度下降或停止。</span><span class="sxs-lookup"><span data-stu-id="f834c-127">This spike could overwhelm your processing system, causing it to slow down or halt, disappointing your users.</span></span> <span data-ttu-id="f834c-128">您可能已经为自己体验了此 disappointment。</span><span class="sxs-lookup"><span data-stu-id="f834c-128">You may have experienced this disappointment for yourself.</span></span> <span data-ttu-id="f834c-129">您是否曾尝试仅访问在线销售以查找网站未响应？</span><span class="sxs-lookup"><span data-stu-id="f834c-129">Have you ever tried to access an online sale only to find the website wasn't responding?</span></span>

## <a name="what-is-a-load-balancer"></a><span data-ttu-id="f834c-130">什么是负载平衡器？</span><span class="sxs-lookup"><span data-stu-id="f834c-130">What is a load balancer?</span></span>

:::row:::
  :::column:::
    ![表示负载平衡的扩展](../media/3-lb.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="f834c-132">_负载平衡器_在池中的每个系统之间平均分布流量。</span><span class="sxs-lookup"><span data-stu-id="f834c-132">A _load balancer_ distributes traffic evenly among each system in a pool.</span></span> <span data-ttu-id="f834c-133">负载平衡器可帮助您实现高可用性和弹性。</span><span class="sxs-lookup"><span data-stu-id="f834c-133">A load balancer can help you achieve both high availability and resiliency.</span></span>

<span data-ttu-id="f834c-134">假设您首先向每个层添加其他 vm (每个配置相同)。</span><span class="sxs-lookup"><span data-stu-id="f834c-134">Say you start by adding additional VMs, each configured identically, to each tier.</span></span> <span data-ttu-id="f834c-135">其目的是让其他系统准备就绪, 以便在一段时间内或同时为太多用户提供服务。</span><span class="sxs-lookup"><span data-stu-id="f834c-135">The idea is to have additional systems ready, in case one goes down, or is serving too many users at the same time.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="f834c-136">此处的问题是每个虚拟机都有自己的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="f834c-136">The problem here is that each VM would have its own IP address.</span></span> <span data-ttu-id="f834c-137">此外, 在一个系统出现故障或繁忙的情况下, 你无法分配流量的方法。</span><span class="sxs-lookup"><span data-stu-id="f834c-137">Plus, you don't have a way to distribute traffic in case one system goes down or is busy.</span></span> <span data-ttu-id="f834c-138">如何连接你的 vm, 以使其作为一个系统显示给用户？</span><span class="sxs-lookup"><span data-stu-id="f834c-138">How do you connect your VMs so that they appear to the user as one system?</span></span>

<span data-ttu-id="f834c-139">答案是使用_负载平衡器_来分发流量。</span><span class="sxs-lookup"><span data-stu-id="f834c-139">The answer is to use a _load balancer_ to distribute traffic.</span></span> <span data-ttu-id="f834c-140">负载平衡器成为用户的入口点。</span><span class="sxs-lookup"><span data-stu-id="f834c-140">The load balancer becomes the entry point to the user.</span></span> <span data-ttu-id="f834c-141">用户不知道 (或需要知道) 负载平衡器选择接收请求的系统。</span><span class="sxs-lookup"><span data-stu-id="f834c-141">The user doesn't know (or need to know) which system the load balancer chooses to receive the request.</span></span>

<span data-ttu-id="f834c-142">下图显示了负载平衡器的角色。</span><span class="sxs-lookup"><span data-stu-id="f834c-142">The following illustration shows the role of a load balancer.</span></span>

![显示三层体系结构的 web 层的插图。](../media/3-load-balancer.png)

<span data-ttu-id="f834c-146">负载平衡器接收用户的请求, 并将请求定向到 web 层中的其中一个 vm。</span><span class="sxs-lookup"><span data-stu-id="f834c-146">The load balancer receives the user's request and directs the request to one of the VMs in the web tier.</span></span> <span data-ttu-id="f834c-147">如果 VM 不可用或停止响应, 则负载平衡器将停止向其发送流量。</span><span class="sxs-lookup"><span data-stu-id="f834c-147">If a VM is unavailable or stops responding, the load balancer stops sending traffic to it.</span></span> <span data-ttu-id="f834c-148">然后, 负载平衡器将通信定向到某个响应性服务器。</span><span class="sxs-lookup"><span data-stu-id="f834c-148">The load balancer then directs traffic to one of the responsive servers.</span></span>

<span data-ttu-id="f834c-149">负载平衡使您能够在不中断服务的情况下运行维护任务。</span><span class="sxs-lookup"><span data-stu-id="f834c-149">Load balancing enables you to run maintenance tasks without interrupting service.</span></span> <span data-ttu-id="f834c-150">例如, 可以错开每个 VM 的维护时段。</span><span class="sxs-lookup"><span data-stu-id="f834c-150">For example, you can stagger the maintenance window for each VM.</span></span> <span data-ttu-id="f834c-151">在维护时段内, 负载平衡器检测到 VM 无响应, 并将流量定向到池中的其他 vm。</span><span class="sxs-lookup"><span data-stu-id="f834c-151">During the maintenance window, the load balancer detects that the VM is unresponsive, and directs traffic to other VMs in the pool.</span></span>

<span data-ttu-id="f834c-152">对于您的电子商务站点, 应用层和数据层也可以具有负载平衡器。</span><span class="sxs-lookup"><span data-stu-id="f834c-152">For your e-commerce site, the app and data tiers can also have a load balancer.</span></span> <span data-ttu-id="f834c-153">这一切都取决于您的服务所需的内容。</span><span class="sxs-lookup"><span data-stu-id="f834c-153">It all depends on what your service requires.</span></span>

## <a name="what-is-azure-load-balancer"></a><span data-ttu-id="f834c-154">什么是 Azure 负载平衡器？</span><span class="sxs-lookup"><span data-stu-id="f834c-154">What is Azure Load Balancer?</span></span>

<span data-ttu-id="f834c-155">Azure 负载平衡器是 Microsoft 提供的一种负载平衡器服务, 可帮助您处理维护。</span><span class="sxs-lookup"><span data-stu-id="f834c-155">Azure Load Balancer is a load balancer service that Microsoft provides that helps take care of the maintenance for you.</span></span> <span data-ttu-id="f834c-156">负载平衡器支持入站和出站方案, 提供低延迟和高吞吐量, 并可扩展所有传输控制协议 (TCP) 和用户数据报协议 (UDP) 应用程序的流量。</span><span class="sxs-lookup"><span data-stu-id="f834c-156">Load Balancer supports inbound and outbound scenarios, provides low latency and high throughput, and scales up to millions of flows for all Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) applications.</span></span> <span data-ttu-id="f834c-157">可以将负载平衡器与传入 internet 流量、跨 Azure 服务的内部流量、特定流量的端口转发或虚拟网络中的 vm 的出站连接结合使用。</span><span class="sxs-lookup"><span data-stu-id="f834c-157">You can use Load Balancer with incoming internet traffic, internal traffic across Azure services, port forwarding for specific traffic, or outbound connectivity for VMs in your virtual network.</span></span>

<span data-ttu-id="f834c-158">在虚拟机上手动配置典型负载平衡器软件时, 存在一些缺点: 现在, 您有一个需要维护的额外系统。</span><span class="sxs-lookup"><span data-stu-id="f834c-158">When you manually configure typical load balancer software on a virtual machine, there's a downside: you now have an additional system that you need to maintain.</span></span> <span data-ttu-id="f834c-159">如果你的负载平衡器停机或需要例行维护, 你将回到原始问题。</span><span class="sxs-lookup"><span data-stu-id="f834c-159">If your load balancer goes down or needs routine maintenance, you're back to your original problem.</span></span>

<span data-ttu-id="f834c-160">然而, 如果使用的是 Azure 负载平衡器, 则不需要维护任何基础结构或软件。</span><span class="sxs-lookup"><span data-stu-id="f834c-160">If instead, however, you use Azure Load Balancer, there's no infrastructure or software for you to maintain.</span></span> <span data-ttu-id="f834c-161">将基于源 ip 和端口的转发规则定义到一组目标 ip/端口。</span><span class="sxs-lookup"><span data-stu-id="f834c-161">You define the forwarding rules based on the source IP and port to a set of destination IP/ports.</span></span>

<span data-ttu-id="f834c-162">下图显示了多层体系结构中的 Azure 负载平衡器的角色。</span><span class="sxs-lookup"><span data-stu-id="f834c-162">The following illustration shows  the role of Azure load balancers in a multi-tier architecture.</span></span>

![显示三层体系结构的 web 层的插图。](../media/3-azure-load-balancer.png)

## <a name="azure-application-gateway"></a><span data-ttu-id="f834c-166">Azure 应用程序网关</span><span class="sxs-lookup"><span data-stu-id="f834c-166">Azure Application Gateway</span></span>

<span data-ttu-id="f834c-167">如果你的所有流量都是 HTTP, 则一个可能更好的方法是使用 Azure 应用程序网关。</span><span class="sxs-lookup"><span data-stu-id="f834c-167">If all your traffic is HTTP, a potentially better option is to use Azure Application Gateway.</span></span> <span data-ttu-id="f834c-168">应用程序网关是为 web 应用程序设计的负载平衡器。</span><span class="sxs-lookup"><span data-stu-id="f834c-168">Application Gateway is a load balancer designed for web applications.</span></span> <span data-ttu-id="f834c-169">它在传输级别 (TCP) 使用 Azure 负载平衡器, 并应用基于 URL 的复杂路由规则来支持多种高级方案。</span><span class="sxs-lookup"><span data-stu-id="f834c-169">It uses Azure Load Balancer at the transport level (TCP) and applies sophisticated URL-based routing rules to support several advanced scenarios.</span></span>

![显示基于 URL 的服务器组之间的应用程序网关产品路由 HTTP 流量的概念性图像](../media/3-appgateway.png)

<span data-ttu-id="f834c-171">这种类型的路由称为应用程序层 (OSI 层 7) 负载平衡, 因为它了解 HTTP 消息的结构。</span><span class="sxs-lookup"><span data-stu-id="f834c-171">This type of routing is known as application layer (OSI layer 7) load balancing since it understands the structure of the HTTP message.</span></span> 

<span data-ttu-id="f834c-172">下面是在简单负载平衡器上使用 Azure 应用程序网关的一些好处:</span><span class="sxs-lookup"><span data-stu-id="f834c-172">Here are some of the benefits of using Azure Application Gateway over a simple load balancer:</span></span>

- <span data-ttu-id="f834c-173">**Cookie 关联**。</span><span class="sxs-lookup"><span data-stu-id="f834c-173">**Cookie affinity**.</span></span> <span data-ttu-id="f834c-174">当您想要在同一个后端服务器上保留用户会话时, 此方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="f834c-174">Useful when you want to keep a user session on the same backend server.</span></span>
- <span data-ttu-id="f834c-175">**SSL 终止**。</span><span class="sxs-lookup"><span data-stu-id="f834c-175">**SSL termination**.</span></span> <span data-ttu-id="f834c-176">应用程序网关可以管理 SSL 证书并将未加密的流量传递给后端服务器, 以避免加密/解密开销。</span><span class="sxs-lookup"><span data-stu-id="f834c-176">Application Gateway can manage your SSL certificates and pass unencrypted traffic to the backend servers to avoid encryption/decryption overhead.</span></span> <span data-ttu-id="f834c-177">它还支持对需要的应用程序的完整端到端加密。</span><span class="sxs-lookup"><span data-stu-id="f834c-177">It also supports full end-to-end encryption for applications that require that.</span></span>
- <span data-ttu-id="f834c-178">**Web 应用程序防火墙**。</span><span class="sxs-lookup"><span data-stu-id="f834c-178">**Web application firewall**.</span></span> <span data-ttu-id="f834c-179">应用程序网关支持具有详细监控和日志记录的高级防火墙 (WAF), 以检测对网络基础结构的恶意攻击。</span><span class="sxs-lookup"><span data-stu-id="f834c-179">Application gateway supports a sophisticated firewall (WAF) with detailed monitoring and logging to detect malicious attacks against your network infrastructure.</span></span>
- <span data-ttu-id="f834c-180">**基于 URL 规则的路由**。</span><span class="sxs-lookup"><span data-stu-id="f834c-180">**URL rule-based routes**.</span></span> <span data-ttu-id="f834c-181">应用程序网关允许您根据 URL 模式、源 ip 地址和端口到目标 ip 地址和端口路由流量。</span><span class="sxs-lookup"><span data-stu-id="f834c-181">Application Gateway allows you to route traffic based on URL patterns, source IP address and port to destination IP address and port.</span></span> <span data-ttu-id="f834c-182">这在设置_内容传递网络_时非常有用。</span><span class="sxs-lookup"><span data-stu-id="f834c-182">This is helpful when setting up a _content delivery network_.</span></span>
- <span data-ttu-id="f834c-183">**重写 HTTP 标头**。</span><span class="sxs-lookup"><span data-stu-id="f834c-183">**Rewrite HTTP headers**.</span></span> <span data-ttu-id="f834c-184">您可以在每个请求的入站和出站 HTTP 标头中添加或删除信息, 以启用重要的安全方案, 或清理敏感信息 (如服务器名称)。</span><span class="sxs-lookup"><span data-stu-id="f834c-184">You can add or remove information from the inbound and outbound HTTP headers of each request to enable important security scenarios, or scrub sensitive information such as server names.</span></span>

### <a name="what-is-a-content-delivery-network"></a><span data-ttu-id="f834c-185">什么是内容传递网络？</span><span class="sxs-lookup"><span data-stu-id="f834c-185">What is a Content Delivery Network?</span></span>

<span data-ttu-id="f834c-186">内容传递网络 (CDN) 是服务器的分布式网络, 可有效地向用户传递 web 内容。</span><span class="sxs-lookup"><span data-stu-id="f834c-186">A content delivery network (CDN) is a distributed network of servers that can efficiently deliver web content to users.</span></span> <span data-ttu-id="f834c-187">这是在本地区域中向用户获取内容以最大限度地减少延迟的一种方式。</span><span class="sxs-lookup"><span data-stu-id="f834c-187">It is a way to get content to users in their local region to minimize latency.</span></span> <span data-ttu-id="f834c-188">可以在 Azure 或任何其他位置托管 CDN。</span><span class="sxs-lookup"><span data-stu-id="f834c-188">CDN can be hosted in Azure or any other location.</span></span> <span data-ttu-id="f834c-189">您可以在世界上有战略放置的物理节点上缓存内容, 并为最终用户提供更好的性能。</span><span class="sxs-lookup"><span data-stu-id="f834c-189">You can cache content at strategically placed physical nodes across the world and provide better performance to end users.</span></span> <span data-ttu-id="f834c-190">典型的使用方案包括包含多媒体内容的 web 应用程序、特定区域中的产品启动事件或在某个区域中预计高带宽要求的任何事件。</span><span class="sxs-lookup"><span data-stu-id="f834c-190">Typical usage scenarios include web applications containing multimedia content, a product launch event in a particular region, or any event where you expect a high-bandwidth requirement in a region.</span></span>

## <a name="what-about-dns"></a><span data-ttu-id="f834c-191">DNS 的目标是什么？</span><span class="sxs-lookup"><span data-stu-id="f834c-191">What about DNS?</span></span>

:::row:::
  :::column:::
    ![代表 DNS 的地图上的 pin](../media/3-map-pin.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="f834c-193">DNS 或域名系统, 是一种将用户友好名称映射到其 IP 地址的方法。</span><span class="sxs-lookup"><span data-stu-id="f834c-193">DNS, or Domain Name System, is a way to map user-friendly names to their IP addresses.</span></span> <span data-ttu-id="f834c-194">你可以将 DNS 视为 internet 的电话簿。</span><span class="sxs-lookup"><span data-stu-id="f834c-194">You can think of DNS as the phonebook of the internet.</span></span>

<span data-ttu-id="f834c-195">例如, 您的域名 (contoso.com) 可能会映射到 web 层上的负载平衡器的 IP 地址, 40.65.106.192。</span><span class="sxs-lookup"><span data-stu-id="f834c-195">For example, your domain name, contoso.com, might map to the IP address of the load balancer at the web tier, 40.65.106.192.</span></span>

<span data-ttu-id="f834c-196">你可以将自己的 dns 服务器或使用 azure DNS 用于在 Azure 基础结构上运行的 DNS 域的托管服务。</span><span class="sxs-lookup"><span data-stu-id="f834c-196">You can bring your own DNS server or use Azure DNS, a hosting service for DNS domains that runs on Azure infrastructure.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="f834c-197">下图显示了 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="f834c-197">The following illustration shows Azure DNS.</span></span> <span data-ttu-id="f834c-198">当用户导航到**contoso.com**时, Azure DNS 会将流量路由到负载平衡器。</span><span class="sxs-lookup"><span data-stu-id="f834c-198">When the user navigates to **contoso.com**, Azure DNS routes traffic to the load balancer.</span></span>

![显示 Azure 域名系统位于负载平衡器前面的插图。](../media/3-dns.png)

## <a name="summary"></a><span data-ttu-id="f834c-200">摘要</span><span class="sxs-lookup"><span data-stu-id="f834c-200">Summary</span></span>

<span data-ttu-id="f834c-201">使用负载平衡时, 你的电子商务网站现在更具可用性和灵活性。</span><span class="sxs-lookup"><span data-stu-id="f834c-201">With load balancing in place, your e-commerce site is now more highly available and resilient.</span></span> <span data-ttu-id="f834c-202">当您在流量中执行维护或接收 uptick 时, 负载平衡器可以将流量分发到另一个可用系统。</span><span class="sxs-lookup"><span data-stu-id="f834c-202">When you perform maintenance or receive an uptick in traffic, your load balancer can distribute traffic to another available system.</span></span>

<span data-ttu-id="f834c-203">虽然您可以在虚拟机上配置自己的负载平衡器, 但 Azure 负载平衡器降低了维护, 因为没有要维护的基础结构或软件。</span><span class="sxs-lookup"><span data-stu-id="f834c-203">Although you can configure your own load balancer on a VM, Azure Load Balancer reduces upkeep because there's no infrastructure or software to maintain.</span></span>

<span data-ttu-id="f834c-204">DNS 将用户友好名称映射到其 IP 地址, 这与电话簿将人员或公司的名称映射到电话号码的方式非常相似。</span><span class="sxs-lookup"><span data-stu-id="f834c-204">DNS maps user-friendly names to their IP addresses, much like how a phonebook maps names of people or businesses to phone numbers.</span></span> <span data-ttu-id="f834c-205">你可以引入自己的 DNS 服务器, 也可以使用 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="f834c-205">You can bring your own DNS server, or use Azure DNS.</span></span>
