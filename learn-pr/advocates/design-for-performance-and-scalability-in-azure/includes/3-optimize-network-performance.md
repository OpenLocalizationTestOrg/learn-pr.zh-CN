<span data-ttu-id="6248e-101">网络性能会对用户体验产生显著影响。</span><span class="sxs-lookup"><span data-stu-id="6248e-101">Network performance can have a dramatic impact on a user's experience.</span></span> <span data-ttu-id="6248e-102">在具有多种不同服务的复杂体系结构中, 最大程度地减少每个跃点的延迟可能会对整体性能产生重大影响。</span><span class="sxs-lookup"><span data-stu-id="6248e-102">In complex architectures with many different services, minimizing the latency at each hop can have a huge impact on the overall performance.</span></span> <span data-ttu-id="6248e-103">在此单元中, 我们将讨论网络延迟的重要性以及如何在体系结构中对其进行减少。</span><span class="sxs-lookup"><span data-stu-id="6248e-103">In this unit, we'll talk about the importance of network latency and how to reduce it within your architecture.</span></span> <span data-ttu-id="6248e-104">我们还将讨论 Lamna 保健采用的策略如何最大限度地减少 Azure 资源之间以及用户和 Azure 之间的网络延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-104">We'll also discuss how Lamna Healthcare adopted strategies to minimize network latency between their Azure resources as well as between their users and Azure.</span></span>

## <a name="the-importance-of-network-latency"></a><span data-ttu-id="6248e-105">网络延迟的重要性</span><span class="sxs-lookup"><span data-stu-id="6248e-105">The importance of network latency</span></span>

<span data-ttu-id="6248e-106">延迟是一种延迟指标。</span><span class="sxs-lookup"><span data-stu-id="6248e-106">Latency is a measure of delay.</span></span> <span data-ttu-id="6248e-107">网络延迟是在某个网络基础结构中从一个源到达目标所需的时间。</span><span class="sxs-lookup"><span data-stu-id="6248e-107">Network latency is the time needed to get from a source to a destination across some network infrastructure.</span></span> <span data-ttu-id="6248e-108">此时间段通常称为往返延迟, 或从源恢复到目标并再次返回时所需的时间。</span><span class="sxs-lookup"><span data-stu-id="6248e-108">This time period is commonly known as a round-trip delay, or the time taken to get from the source to destination and back again.</span></span>

<span data-ttu-id="6248e-109">在传统数据中心环境中, 延迟可能会很小, 因为资源通常共享相同的位置和一组通用的基础结构。</span><span class="sxs-lookup"><span data-stu-id="6248e-109">In a traditional datacenter environment, latency may be minimal since resources often share the same location and a common set of infrastructure.</span></span> <span data-ttu-id="6248e-110">当资源在物理上断开时, 从源获取到目标所需的时间较低。</span><span class="sxs-lookup"><span data-stu-id="6248e-110">The time taken to get from source to destination is lower when resources are physically close together.</span></span>

<span data-ttu-id="6248e-111">相比之下, 云环境是针对规模而构建的。</span><span class="sxs-lookup"><span data-stu-id="6248e-111">In comparison, a cloud environment is built for scale.</span></span> <span data-ttu-id="6248e-112">云托管的资源可能不在同一机架、数据中心, 甚至地区。</span><span class="sxs-lookup"><span data-stu-id="6248e-112">Cloud-hosted resources may not be in the same rack, datacenter, or even region.</span></span> <span data-ttu-id="6248e-113">这种分布式方法可能会影响网络通信的往返时间。</span><span class="sxs-lookup"><span data-stu-id="6248e-113">This distributed approach can have an impact on the round-trip time of your network communications.</span></span> <span data-ttu-id="6248e-114">虽然所有 Azure 区域都是通过高速光纤主干网互连的, 但光的速度仍是物理限制。</span><span class="sxs-lookup"><span data-stu-id="6248e-114">While all Azure regions are interconnected by a high-speed fiber backbone, the speed of light is still a physical limitation.</span></span> <span data-ttu-id="6248e-115">不同物理位置中的服务之间的呼叫将仍具有与它们之间的距离直接相关的网络延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-115">Calls between services in different physical locations will still have network latency directly correlated to the distance between them.</span></span>

<span data-ttu-id="6248e-116">在此之上, chattier 应用程序, 需要的往返行程越多。</span><span class="sxs-lookup"><span data-stu-id="6248e-116">On top of this, the chattier an application, the more round trips that are required.</span></span> <span data-ttu-id="6248e-117">每个往返行程都带有延迟税, 每个往返行程都添加到整体延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-117">Each round trip comes with a latency tax, with each round trip adding to the overall latency.</span></span> <span data-ttu-id="6248e-118">下图显示了用户可检测到的延迟的组合, 以及为请求提供服务所需的往返次数。</span><span class="sxs-lookup"><span data-stu-id="6248e-118">The following illustration shows how the latency perceived by the user is the combination of the roundtrips required to service the request.</span></span>

![该图显示了位于云中不同地理位置的资源之间的网络延迟。](../media/3-networkLatency.png)

<span data-ttu-id="6248e-120">现在, 我们来看看如何提高 azure 资源和最终用户与 azure 资源之间的性能。</span><span class="sxs-lookup"><span data-stu-id="6248e-120">Now let's take a look at how to improve performance between Azure resources and from your end users to your Azure resources.</span></span>

## <a name="latency-between-azure-resources"></a><span data-ttu-id="6248e-121">Azure 资源之间的延迟</span><span class="sxs-lookup"><span data-stu-id="6248e-121">Latency between Azure resources</span></span>

<span data-ttu-id="6248e-122">假设 Lamna 保健正在试验在多台 web 服务器上运行新的患者预订系统, 以及西欧 Azure 区域中的数据库。</span><span class="sxs-lookup"><span data-stu-id="6248e-122">Imagine that Lamna Healthcare is piloting a new patient booking system running on several web servers and a database in the West Europe Azure region.</span></span> <span data-ttu-id="6248e-123">此体系结构可将网络上的数据时间减至最少, 因为资源在 Azure 区域中有共同的位置。</span><span class="sxs-lookup"><span data-stu-id="6248e-123">This architecture minimizes the data time on the wire as resources are co-located inside an Azure region.</span></span>

<span data-ttu-id="6248e-124">假定系统的试用版已顺利完成, 并已扩展到澳大利亚用户。</span><span class="sxs-lookup"><span data-stu-id="6248e-124">Suppose that the pilot of the system went well and has been expanded to users in Australia.</span></span> <span data-ttu-id="6248e-125">澳大利亚的用户将发生到欧洲西部的资源的往返时间, 以查看网站, 最终用户体验将因网络延迟而变差。</span><span class="sxs-lookup"><span data-stu-id="6248e-125">Users in Australia will incur the round-trip time to the resources in West Europe to view the website, and their end-user experience will be poor due to the network latency.</span></span>

<span data-ttu-id="6248e-126">Lamna 保健团队决定在澳大利亚东部地区托管另一个前端实例, 以减少用户延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-126">The Lamna Healthcare team decide to host another front-end instance in the Australia East region to reduce user latency.</span></span> <span data-ttu-id="6248e-127">虽然此设计有助于缩短 web 服务器将内容返回给最终用户的时间, 但由于澳大利亚东部的前端 web 服务器和西欧的数据库中的前端 web 服务器之间的通信发生重大延迟, 因此其体验仍很差。</span><span class="sxs-lookup"><span data-stu-id="6248e-127">While this design helps reduce the time for the web server to return content to end users, their experience is still poor since there's significant latency communicating between the front-end web servers in Australia East and the database in West Europe.</span></span>

<span data-ttu-id="6248e-128">可以通过几种方法来减少剩余的延迟:</span><span class="sxs-lookup"><span data-stu-id="6248e-128">There are a few ways we could reduce the remaining latency:</span></span>

- <span data-ttu-id="6248e-129">在澳大利亚东部中创建数据库的读取副本。</span><span class="sxs-lookup"><span data-stu-id="6248e-129">Create a read-replica of the database in Australia East.</span></span> <span data-ttu-id="6248e-130">这将允许读取正常运行, 但写入仍会导致延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-130">This would allow reads to perform well, but writes would still incur latency.</span></span> <span data-ttu-id="6248e-131">Azure SQL 数据库异地复制允许读取副本。</span><span class="sxs-lookup"><span data-stu-id="6248e-131">Azure SQL Database geo-replication allows for read-replicas.</span></span>
- <span data-ttu-id="6248e-132">在具有 Azure SQL 数据同步的区域之间同步你的数据。</span><span class="sxs-lookup"><span data-stu-id="6248e-132">Sync your data between regions with Azure SQL Data Sync.</span></span>
- <span data-ttu-id="6248e-133">使用全局分布式数据库, 如 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="6248e-133">Use a globally distributed database such as Azure Cosmos DB.</span></span> <span data-ttu-id="6248e-134">这将允许读取和写入操作, 而不考虑位置, 但可能需要对应用程序存储和引用数据的方式进行更改。</span><span class="sxs-lookup"><span data-stu-id="6248e-134">This would allow both reads and writes to occur regardless of location, but may require changes to the way your application stores and references data.</span></span>
- <span data-ttu-id="6248e-135">使用缓存技术 (如 Redis 的 Azure 缓存) 将对频繁访问的数据的远程数据库的高延迟调用降至最低。</span><span class="sxs-lookup"><span data-stu-id="6248e-135">Use caching technology such as Azure Cache for Redis to minimize high-latency calls to remote databases for frequently accessed data.</span></span>

<span data-ttu-id="6248e-136">此处的目标是最大限度地减少应用程序的每个层之间的网络延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-136">The goal here is to minimize the network latency between each layer of the application.</span></span> <span data-ttu-id="6248e-137">此解决方案的解决方式取决于您的应用程序和数据体系结构, 但 Azure 提供了在多个服务上解决这一情况的机制。</span><span class="sxs-lookup"><span data-stu-id="6248e-137">How this is solved depends on your application and data architecture, but Azure provides mechanisms to solve this on several services.</span></span>

## <a name="latency-between-users-and-azure-resources"></a><span data-ttu-id="6248e-138">用户和 Azure 资源之间的延迟</span><span class="sxs-lookup"><span data-stu-id="6248e-138">Latency between users and Azure resources</span></span>

<span data-ttu-id="6248e-139">我们查看了 Azure 资源之间的延迟, 但我们还应考虑用户与我们的云应用程序之间的延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-139">We've looked at the latency between our Azure resources, but we should also consider the latency between users and our cloud application.</span></span> <span data-ttu-id="6248e-140">我们希望优化对用户的前端用户界面的交付。</span><span class="sxs-lookup"><span data-stu-id="6248e-140">We're looking to optimize delivery of the front end-user interface to our users.</span></span> <span data-ttu-id="6248e-141">让我们来看看在最终用户和应用程序之间提高网络性能的一些方法。</span><span class="sxs-lookup"><span data-stu-id="6248e-141">Let's take a look at some ways to improve the network performance between end users and the application.</span></span>

### <a name="use-a-dns-load-balancer-for-endpoint-path-optimization"></a><span data-ttu-id="6248e-142">使用 DNS 负载平衡器进行终结点路径优化</span><span class="sxs-lookup"><span data-stu-id="6248e-142">Use a DNS load balancer for endpoint path optimization</span></span>

<span data-ttu-id="6248e-143">在 Lamna 保健示例中, 我们看到团队在澳大利亚东部中创建了其他 web 前端节点。</span><span class="sxs-lookup"><span data-stu-id="6248e-143">In the Lamna Healthcare example, we saw that the team created an additional web front-end node in Australia East.</span></span> <span data-ttu-id="6248e-144">但是, 最终用户必须明确指定要使用的前端终结点。</span><span class="sxs-lookup"><span data-stu-id="6248e-144">However, end users have to explicitly specify which front-end endpoint they want to use.</span></span> <span data-ttu-id="6248e-145">作为解决方案的设计者, Lamna 医疗保健希望为其用户提供尽可能平滑的体验。</span><span class="sxs-lookup"><span data-stu-id="6248e-145">As the designer of a solution, Lamna Healthcare wants to make the experience as smooth as possible for their users.</span></span>

<span data-ttu-id="6248e-146">Azure 流量管理器可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="6248e-146">Azure Traffic Manager could help.</span></span> <span data-ttu-id="6248e-147">流量管理器是基于 DNS 的负载平衡器, 它使您能够在 Azure 区域内以及在 Azure 区域之间分布流量。</span><span class="sxs-lookup"><span data-stu-id="6248e-147">Traffic Manager is a DNS-based load balancer that enables you to distribute traffic within and across Azure regions.</span></span> <span data-ttu-id="6248e-148">流量管理器可根据一组特征路由用户, 而不是让用户浏览到 web 前端的特定实例:</span><span class="sxs-lookup"><span data-stu-id="6248e-148">Rather than having the user browse to a specific instance of our web front end, Traffic Manager can route users based upon a set of characteristics:</span></span>

- <span data-ttu-id="6248e-149">**优先级**-指定前端实例的已排序列表。</span><span class="sxs-lookup"><span data-stu-id="6248e-149">**Priority** - You specify an ordered list of front-end instances.</span></span> <span data-ttu-id="6248e-150">如果具有最高优先级的用户不可用, 流量管理器会将用户路由到下一个可用的实例。</span><span class="sxs-lookup"><span data-stu-id="6248e-150">If the one with the highest priority is unavailable, Traffic Manager will route the user to the next available instance.</span></span>
- <span data-ttu-id="6248e-151">**加权**-将为每个前端实例设置权重。</span><span class="sxs-lookup"><span data-stu-id="6248e-151">**Weighted** - You would set a weight against each front-end instance.</span></span> <span data-ttu-id="6248e-152">然后, 流量管理器根据已定义的比率来分配流量。</span><span class="sxs-lookup"><span data-stu-id="6248e-152">Traffic Manager then distributes traffic according to those defined ratios.</span></span>
- <span data-ttu-id="6248e-153">**性能**流量管理器根据网络延迟将用户路由到最近的前端实例。</span><span class="sxs-lookup"><span data-stu-id="6248e-153">**Performance** - Traffic Manager routes users to the closest front-end instance based on network latency.</span></span>
- <span data-ttu-id="6248e-154">**地理**位置-您可以为前端部署设置地理区域, 并根据数据主权的要求或本地化内容来路由您的用户。</span><span class="sxs-lookup"><span data-stu-id="6248e-154">**Geographic** - You could set up geographical regions for front-end deployments, routing your users based upon data sovereignty mandates or localization of content.</span></span>

<span data-ttu-id="6248e-155">此外, 还可以嵌套流量管理器配置文件。</span><span class="sxs-lookup"><span data-stu-id="6248e-155">Traffic Manager profiles can also be nested.</span></span> <span data-ttu-id="6248e-156">您可以先使用地理路由在不同地理位置 (例如, 欧洲和澳大利亚) 路由用户, 然后使用性能路由方法将它们路由到本地前端部署。</span><span class="sxs-lookup"><span data-stu-id="6248e-156">You could first route your users across different geographies (for example, Europe and Australia) using geographic routing and then route them to local front-end deployments using the performance routing method.</span></span>

<span data-ttu-id="6248e-157">请注意, Lamna 保健已在西欧和澳大利亚部署了 web 前端。</span><span class="sxs-lookup"><span data-stu-id="6248e-157">Consider that Lamna Healthcare has deployed a web front end in West Europe and Australia.</span></span> <span data-ttu-id="6248e-158">假定他们已在西欧的主要部署中部署了 Azure SQL 数据库以及在澳大利亚东部的读取副本。</span><span class="sxs-lookup"><span data-stu-id="6248e-158">Assume they have deployed Azure SQL Database with their primary deployment in West Europe, and a read replica in Australia East.</span></span> <span data-ttu-id="6248e-159">我们还假设应用程序可以连接到本地 SQL 实例以进行读取查询。</span><span class="sxs-lookup"><span data-stu-id="6248e-159">Let's also assume the application can connect to the local SQL instance for read queries.</span></span>

<span data-ttu-id="6248e-160">团队在性能模式中部署流量管理器实例, 并将这两个前端实例添加为流量管理器配置文件。</span><span class="sxs-lookup"><span data-stu-id="6248e-160">The team deploy a Traffic Manager instance in performance mode and add the two front-end instances as Traffic Manager profiles.</span></span> <span data-ttu-id="6248e-161">作为最终用户, 您可以导航到流量管理器路由到的自定义域名 (例如, lamnahealthcare.com)。</span><span class="sxs-lookup"><span data-stu-id="6248e-161">As an end user, you navigate to a custom domain name (for example, lamnahealthcare.com) which routes to Traffic Manager.</span></span> <span data-ttu-id="6248e-162">然后, 流量管理器将基于最佳网络延迟性能返回西欧或澳大利亚东前端的 DNS 名称。</span><span class="sxs-lookup"><span data-stu-id="6248e-162">Traffic Manager then returns the DNS name of the West Europe or Australia East front end based on the best network latency performance.</span></span>

<span data-ttu-id="6248e-163">请务必注意, 此负载平衡仅通过 DNS 处理, 没有内嵌负载平衡或缓存在此处发生, 而流量管理器只是向用户返回最近前端的 DNS 名称。</span><span class="sxs-lookup"><span data-stu-id="6248e-163">It's important to note that this load balancing is only handled via DNS, there's no inline load balancing or caching that's happening here, Traffic Manager is simply returning the DNS name of the closest front end to the user.</span></span>

### <a name="use-cdn-to-cache-content-close-to-users"></a><span data-ttu-id="6248e-164">使用 CDN 将内容缓存到用户附近</span><span class="sxs-lookup"><span data-stu-id="6248e-164">Use CDN to cache content close to users</span></span>

<span data-ttu-id="6248e-165">该网站可能会使用某种形式的静态内容 (整页或资产, 如图像和视频)。</span><span class="sxs-lookup"><span data-stu-id="6248e-165">The website will likely be using some form of static content (either whole pages or assets such as images and videos).</span></span> <span data-ttu-id="6248e-166">此内容可以通过使用内容传递网络 (CDN) (如 Azure CDN) 更快地传递给用户。</span><span class="sxs-lookup"><span data-stu-id="6248e-166">This content could be delivered to users faster by using a content delivery network (CDN) such as Azure CDN.</span></span> 

<span data-ttu-id="6248e-167">当 Lamna 将内容部署到 Azure CDN 时, 会将这些项目复制到全球范围内的多台服务器上。</span><span class="sxs-lookup"><span data-stu-id="6248e-167">When Lamna deploys content to Azure CDN, those items are copied to multiple servers around the globe.</span></span> <span data-ttu-id="6248e-168">假设其中一项是从 blob 存储提供的视频: `HowToCompleteYourBillingForms.MP4`。</span><span class="sxs-lookup"><span data-stu-id="6248e-168">Let's say one of those items is a video served from blob storage: `HowToCompleteYourBillingForms.MP4`.</span></span> <span data-ttu-id="6248e-169">然后, 团队将网站配置为, 使每个用户的视频链接实际引用最接近它们的 CDN 边缘服务器, 而不是引用 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="6248e-169">The team then configure the website so that each user's link to the video will actually reference the CDN edge server nearest them, rather than referencing blob storage.</span></span> <span data-ttu-id="6248e-170">此方法将内容放在更接近目标的位置, 从而减少延迟和改善用户体验。</span><span class="sxs-lookup"><span data-stu-id="6248e-170">This approach puts content closer to the destination, reducing latency and improving user experience.</span></span> <span data-ttu-id="6248e-171">下图显示了如何使用 Azure CDN 将内容放在更接近目标的位置, 从而减少延迟并改善用户体验。</span><span class="sxs-lookup"><span data-stu-id="6248e-171">The following illustration shows how using Azure CDN puts content closer to the destination which reduces latency and improves the user experience.</span></span>

![该图显示了如何使用 Azure 内容传送网络来减少延迟。](../media/3-cdnSketch.png)

<span data-ttu-id="6248e-173">内容传递网络也_可_用于承载缓存的动态内容。</span><span class="sxs-lookup"><span data-stu-id="6248e-173">Content delivery networks _can_ also be used to host cached dynamic content.</span></span> <span data-ttu-id="6248e-174">但需要额外考虑, 因为缓存的内容与源相比可能已过期。</span><span class="sxs-lookup"><span data-stu-id="6248e-174">Extra consideration is required, though, since cached content may be out of date compared with the source.</span></span> <span data-ttu-id="6248e-175">可以通过将时间设置为生存时间 (TTL) 来控制上下文过期。</span><span class="sxs-lookup"><span data-stu-id="6248e-175">Context expiration can be controlled by setting a time to live (TTL).</span></span> <span data-ttu-id="6248e-176">如果 TTL 过高, 则可能会显示过时的内容, 并且需要清除缓存。</span><span class="sxs-lookup"><span data-stu-id="6248e-176">If the TTL is too high, out-of-date content may be displayed and the cache would need to be purged.</span></span>

<span data-ttu-id="6248e-177">处理缓存内容的一种方法是一个称为 "**动态网站加速**" 的功能, 它可以提高使用动态内容的网页的性能。</span><span class="sxs-lookup"><span data-stu-id="6248e-177">One way to handle cached content is with a feature called **dynamic site acceleration**, which can increase performance of webpages with dynamic content.</span></span> <span data-ttu-id="6248e-178">动态网站加速还可以提供到解决方案中的其他服务的低延迟路径 (例如 API 终结点)。</span><span class="sxs-lookup"><span data-stu-id="6248e-178">Dynamic site acceleration can also provide a low-latency path to additional services in your solution (for example, an API endpoint).</span></span>

### <a name="use-expressroute-for-connectivity-from-on-premises-to-azure"></a><span data-ttu-id="6248e-179">将 ExpressRoute 用于从本地到 Azure 的连接</span><span class="sxs-lookup"><span data-stu-id="6248e-179">Use ExpressRoute for connectivity from on-premises to Azure</span></span>

<span data-ttu-id="6248e-180">优化从本地环境到 Azure 的网络连接也很重要。</span><span class="sxs-lookup"><span data-stu-id="6248e-180">Optimizing network connectivity from your on-premises environment to Azure is also important.</span></span> <span data-ttu-id="6248e-181">对于连接到应用程序的用户, 无论是在虚拟机上还是在与 Azure 应用服务类似的 PaaS 产品上托管, 您都需要确保它们可以与应用程序建立最佳连接。</span><span class="sxs-lookup"><span data-stu-id="6248e-181">For users connecting to applications, whether they're hosted on virtual machines or on PaaS offerings like Azure App Service, you'll want to ensure they have the best connection to your applications.</span></span> 

<span data-ttu-id="6248e-182">您始终可以使用公共 internet 将用户连接到您的服务, 但 internet 性能可能会有所不同, 并且可能会受到外部问题的影响。</span><span class="sxs-lookup"><span data-stu-id="6248e-182">You can always use the public internet to connect users to your services, but internet performance can vary and may be impacted by outside issues.</span></span> <span data-ttu-id="6248e-183">在此之上, 你可能不希望通过 internet 公开你的所有服务, 你可能需要与 Azure 资源的专用连接。</span><span class="sxs-lookup"><span data-stu-id="6248e-183">On top of that, you may not want to expose all of your services over the internet, and you may want a private connection to your Azure resources.</span></span>

<span data-ttu-id="6248e-184">internet 上的站点到站点 VPN 也是一个选项, 但对于高吞吐量体系结构, VPN 开销和 internet 可变性可能会显著增加延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-184">Site-to-site VPN over the internet is also an option, but for high throughput architectures, VPN overhead and internet variability can increase latency noticeably.</span></span>

<span data-ttu-id="6248e-185">Azure ExpressRoute 可帮助。</span><span class="sxs-lookup"><span data-stu-id="6248e-185">Azure ExpressRoute can help.</span></span> <span data-ttu-id="6248e-186">ExpressRoute 是你的网络与 Azure 之间的专用专用连接, 它为你提供了保证的性能, 并确保最终用户具有你的所有 Azure 资源的最佳路径。</span><span class="sxs-lookup"><span data-stu-id="6248e-186">ExpressRoute is a private, dedicated connection between your network and Azure, giving you guaranteed performance and ensuring that your end users have the best path to all of your Azure resources.</span></span> <span data-ttu-id="6248e-187">下图显示了 ExpressRoute 电路如何在本地应用程序和 Azure 资源之间提供连接。</span><span class="sxs-lookup"><span data-stu-id="6248e-187">The following illustration shows how ExpressRoute Circuit provides connectivity between on-premises applications and Azure resources.</span></span>

![显示与 Azure 资源连接客户网络的 ExpressRoute 电路的体系结构图。](../media/3-expressroute-connection-overview.png)

<span data-ttu-id="6248e-189">再次查看 Lamna 的方案后, 他们决定通过在澳大利亚东部和西欧中预配的 ExpressRoute 电路来进一步改进其设施中用户的最终用户体验。</span><span class="sxs-lookup"><span data-stu-id="6248e-189">Once again looking at Lamna's scenario, they decide to further improve end-user experience for users who are in their facilities by provisioning an ExpressRoute circuit in both Australia East and West Europe.</span></span> <span data-ttu-id="6248e-190">这使他们的最终用户能够直接连接到其预订系统, 并确保其应用程序可能具有最低延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-190">This gives their end users a direct connection to their booking system and ensures the lowest latency possible for their application.</span></span>

<span data-ttu-id="6248e-191">考虑到对体系结构的网络延迟的影响对于确保最终用户可能获得最佳性能非常重要。</span><span class="sxs-lookup"><span data-stu-id="6248e-191">Considering the impact of network latency on your architecture is important to ensure the best possible performance for your end users.</span></span> <span data-ttu-id="6248e-192">我们查看了一些选项, 以降低最终用户和 azure 之间和 azure 资源之间的网络延迟。</span><span class="sxs-lookup"><span data-stu-id="6248e-192">We've taken a look at some options to lower network latency between end users and Azure and between Azure resources.</span></span>