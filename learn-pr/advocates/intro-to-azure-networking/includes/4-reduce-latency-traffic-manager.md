<span data-ttu-id="157e1-101">以前, 你了解了**Azure 负载平衡器**如何帮助你实现高可用性并最大限度地减少停机时间。</span><span class="sxs-lookup"><span data-stu-id="157e1-101">Previously, you saw how **Azure Load Balancer** helps you achieve high availability and minimize downtime.</span></span>

<span data-ttu-id="157e1-102">虽然您的电子商务网站的可用性较高, 但它不会解决延迟的问题, 也不能跨地理区域创建弹性。</span><span class="sxs-lookup"><span data-stu-id="157e1-102">Although your e-commerce site is more highly available, it doesn't solve the issue of latency or create resiliency across geographic regions.</span></span>

<span data-ttu-id="157e1-103">如何使网站 (位于美国) 更快地以欧洲或亚洲用户的速度加载？</span><span class="sxs-lookup"><span data-stu-id="157e1-103">How can you make your site, which is located in the United States, load faster for users located in Europe or Asia?</span></span>

## <a name="what-is-network-latency"></a><span data-ttu-id="157e1-104">什么是网络延迟？</span><span class="sxs-lookup"><span data-stu-id="157e1-104">What is network latency?</span></span>

:::row:::
  :::column:::
    ![表示延迟的秒表](../media/4-latency.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="157e1-106">_延迟_是指数据通过网络传输所需的时间。</span><span class="sxs-lookup"><span data-stu-id="157e1-106">_Latency_ refers to the time it takes for data to travel over the network.</span></span> <span data-ttu-id="157e1-107">延迟通常以毫秒为单位。</span><span class="sxs-lookup"><span data-stu-id="157e1-107">Latency is typically measured in milliseconds.</span></span>

<span data-ttu-id="157e1-108">将延迟与带宽进行比较。</span><span class="sxs-lookup"><span data-stu-id="157e1-108">Compare latency to bandwidth.</span></span> <span data-ttu-id="157e1-109">"带宽" 指的是可以在连接上显示的数据量。</span><span class="sxs-lookup"><span data-stu-id="157e1-109">Bandwidth refers to the amount of data that can fit on the connection.</span></span> <span data-ttu-id="157e1-110">延迟是指数据到达其目标所需的时间。</span><span class="sxs-lookup"><span data-stu-id="157e1-110">Latency refers to the time it takes for that data to reach its destination.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="157e1-111">诸如您使用的连接类型和应用程序的设计方式可能会影响延迟的因素。</span><span class="sxs-lookup"><span data-stu-id="157e1-111">Factors such as the type of connection you use and how your application is designed can affect latency.</span></span> <span data-ttu-id="157e1-112">但最大的因素可能是距离。</span><span class="sxs-lookup"><span data-stu-id="157e1-112">But perhaps the biggest factor is distance.</span></span>

<span data-ttu-id="157e1-113">请考虑 Azure 上的电子商务网站 (美国东部地区)。</span><span class="sxs-lookup"><span data-stu-id="157e1-113">Think about your e-commerce site on Azure, which is in the East US region.</span></span> <span data-ttu-id="157e1-114">通常情况下, 将数据传输到亚特兰大 (距离400英里左右) 的时间要少得多, 而不是将数据传输到伦敦 (距离4000英里左右)。</span><span class="sxs-lookup"><span data-stu-id="157e1-114">It would typically take less time to transfer data to Atlanta (a distance of around 400 miles) than to transfer data to London (a distance of around 4,000 miles).</span></span>

<span data-ttu-id="157e1-115">您的电子商务网站提供标准的 HTML、CSS、JavaScript 和图像。</span><span class="sxs-lookup"><span data-stu-id="157e1-115">Your e-commerce site delivers standard HTML, CSS, JavaScript, and images.</span></span> <span data-ttu-id="157e1-116">许多文件的网络延迟可能会增加。</span><span class="sxs-lookup"><span data-stu-id="157e1-116">The network latency for many files can add up.</span></span> <span data-ttu-id="157e1-117">如何减少位于地理位置较远的用户的延迟？</span><span class="sxs-lookup"><span data-stu-id="157e1-117">How can you reduce latency for users located far away geographically?</span></span>

## <a name="scale-out-to-different-regions"></a><span data-ttu-id="157e1-118">向外扩展到不同区域</span><span class="sxs-lookup"><span data-stu-id="157e1-118">Scale out to different regions</span></span>

<span data-ttu-id="157e1-119">回想一下, Azure 在全球范围内提供了数据中心。</span><span class="sxs-lookup"><span data-stu-id="157e1-119">Recall that Azure provides data centers in regions across the globe.</span></span>

:::row:::
  :::column:::
    ![表示区域向外扩展的地球](../media/4-scale-out-regions.png) 
  :::column-end:::
  :::column span="3":::
<span data-ttu-id="157e1-121">考虑构建数据中心的成本。</span><span class="sxs-lookup"><span data-stu-id="157e1-121">Think about the cost of building a data center.</span></span> <span data-ttu-id="157e1-122">设备成本并不是唯一的因素。</span><span class="sxs-lookup"><span data-stu-id="157e1-122">Equipment costs aren't the only factor.</span></span> <span data-ttu-id="157e1-123">你需要提供电源、冷却和人员, 让你的系统在每个位置都能正常运行。</span><span class="sxs-lookup"><span data-stu-id="157e1-123">You need to provide the power, cooling, and personnel to keep your systems running at each location.</span></span> <span data-ttu-id="157e1-124">复制整个数据中心可能会花费大量的成本。</span><span class="sxs-lookup"><span data-stu-id="157e1-124">It might be prohibitively expensive to replicate your entire data center.</span></span> <span data-ttu-id="157e1-125">但在 azure 中执行此操作可能会花费更少的成本, 因为 azure 已经有设备和人员准备就绪。</span><span class="sxs-lookup"><span data-stu-id="157e1-125">But doing so with Azure can cost much less, because Azure already has the equipment and personnel in place.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="157e1-126">降低延迟的一种方法是在多个区域中提供服务的精确副本。</span><span class="sxs-lookup"><span data-stu-id="157e1-126">One way to reduce latency is to provide exact copies of your service in more than one region.</span></span> <span data-ttu-id="157e1-127">下图显示了全局部署的示例。</span><span class="sxs-lookup"><span data-stu-id="157e1-127">The following illustration shows an example of global deployment.</span></span>

![显示了一个突出显示了三个 Azure 数据中心的世界地图的插图。](../media/4-global-deployment.png)

<span data-ttu-id="157e1-130">图中显示了在三个 Azure 区域中运行的电子商务网站: 东美国、北欧和东亚。</span><span class="sxs-lookup"><span data-stu-id="157e1-130">The diagram shows your e-commerce site running in three Azure regions: East US, North Europe, and East Asia.</span></span> <span data-ttu-id="157e1-131">请注意每个的 DNS 名称。</span><span class="sxs-lookup"><span data-stu-id="157e1-131">Notice the DNS name for each.</span></span> <span data-ttu-id="157e1-132">如何将用户连接到距离地理位置最近的服务, 但在 contoso.com 域下？</span><span class="sxs-lookup"><span data-stu-id="157e1-132">How can you connect users to the service that's closest geographically, but under the contoso.com domain?</span></span>

## <a name="use-traffic-manager-to-route-users-to-the-closest-endpoint"></a><span data-ttu-id="157e1-133">使用流量管理器将用户路由到最近的终结点</span><span class="sxs-lookup"><span data-stu-id="157e1-133">Use Traffic Manager to route users to the closest endpoint</span></span>

:::row:::
  :::column:::
    ![代表 Azure 流量管理器的标记帖子](../media/4-sign-post.png) 
  :::column-end:::
  :::column span="3":::

<span data-ttu-id="157e1-135">一个答案是**Azure 流量管理器**。</span><span class="sxs-lookup"><span data-stu-id="157e1-135">One answer is **Azure Traffic Manager**.</span></span> <span data-ttu-id="157e1-136">流量管理器使用最接近用户的 DNS 服务器将用户流量定向到全局分布式终结点。</span><span class="sxs-lookup"><span data-stu-id="157e1-136">Traffic Manager uses the DNS server that's closest to the user to direct user traffic to a globally distributed endpoint.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="157e1-137">下图显示了流量管理器的角色。</span><span class="sxs-lookup"><span data-stu-id="157e1-137">The following illustration shows the role of the Traffic Manager.</span></span>

![<span data-ttu-id="157e1-138">显示 Azure 流量管理器将用户请求路由到最近的数据中心的插图。</span><span class="sxs-lookup"><span data-stu-id="157e1-138">An illustration showing Azure Traffic Manager routing a user request to the nearest data center.</span></span> ](../media/4-traffic-manager.png)

<span data-ttu-id="157e1-139">流量管理器看不到在客户端和服务器之间传递的流量。</span><span class="sxs-lookup"><span data-stu-id="157e1-139">Traffic Manager doesn't see the traffic that's passed between the client and server.</span></span> <span data-ttu-id="157e1-140">相反, 它会将客户端 web 浏览器定向到首选终结点。</span><span class="sxs-lookup"><span data-stu-id="157e1-140">Rather, it directs the client web browser to a preferred endpoint.</span></span> <span data-ttu-id="157e1-141">流量管理器可以通过几种不同的方式路由通信, 例如, 延迟为最低的终结点。</span><span class="sxs-lookup"><span data-stu-id="157e1-141">Traffic Manager can route traffic in a few different ways, such as to the endpoint with the lowest latency.</span></span>

<span data-ttu-id="157e1-142">虽然此处未显示, 但此安装程序还可能包括在加利福尼亚运行本地部署。</span><span class="sxs-lookup"><span data-stu-id="157e1-142">Although not shown here, this setup could also include your on-premises deployment running in California.</span></span> <span data-ttu-id="157e1-143">您可以将流量管理器连接到您自己的本地网络, 使您能够维护现有的数据中心投资。</span><span class="sxs-lookup"><span data-stu-id="157e1-143">You can connect Traffic Manager to your own on-premises networks, enabling you to maintain your existing data center investments.</span></span> <span data-ttu-id="157e1-144">你也可以将应用程序完全移动到云。</span><span class="sxs-lookup"><span data-stu-id="157e1-144">Or you can move your application entirely to the cloud.</span></span> <span data-ttu-id="157e1-145">是你的选择。</span><span class="sxs-lookup"><span data-stu-id="157e1-145">The choice is yours.</span></span>

## <a name="compare-load-balancer-to-traffic-manager"></a><span data-ttu-id="157e1-146">将负载平衡器与流量管理器进行比较</span><span class="sxs-lookup"><span data-stu-id="157e1-146">Compare Load Balancer to Traffic Manager</span></span>

:::row:::
  :::column:::
    ![放大镜](../media/4-magnifying-glass.png) 
  :::column-end:::
  :::column span="3":::
<span data-ttu-id="157e1-148">Azure 负载平衡器将通信分布在同一个区域中, 以使您的服务更高可用性和恢复能力更强。</span><span class="sxs-lookup"><span data-stu-id="157e1-148">Azure Load Balancer distributes traffic within the same region to make your services more highly available and resilient.</span></span> <span data-ttu-id="157e1-149">流量管理器在 DNS 级别工作, 并将客户端定向到首选终结点。</span><span class="sxs-lookup"><span data-stu-id="157e1-149">Traffic Manager works at the DNS level, and directs the client to a preferred endpoint.</span></span> <span data-ttu-id="157e1-150">此终结点可指向最接近你的用户的区域。</span><span class="sxs-lookup"><span data-stu-id="157e1-150">This endpoint can be to the region that's closest to your user.</span></span>

<span data-ttu-id="157e1-151">负载平衡器和流量管理器这两种方法都有助于使您的服务具有更好的可恢复性, 但采用略微</span><span class="sxs-lookup"><span data-stu-id="157e1-151">Load Balancer and Traffic Manager both help make your services more resilient, but in slightly different ways.</span></span> <span data-ttu-id="157e1-152">当负载平衡器检测到未响应的 vm 时, 它会将流量定向到池中的其他 vm。</span><span class="sxs-lookup"><span data-stu-id="157e1-152">When Load Balancer detects an unresponsive VM, it directs traffic to other VMs in the pool.</span></span> <span data-ttu-id="157e1-153">流量管理器监视终结点的运行状况。</span><span class="sxs-lookup"><span data-stu-id="157e1-153">Traffic Manager monitors the health of your endpoints.</span></span> <span data-ttu-id="157e1-154">相比之下, 当流量管理器发现没有响应的终结点时, 它会将流量定向到响应速度最接近的下一个终结点。</span><span class="sxs-lookup"><span data-stu-id="157e1-154">In contrast, when Traffic Manager finds an unresponsive endpoint, it directs traffic to the next closest endpoint that is responsive.</span></span>
  :::column-end:::
:::row-end:::

## <a name="summary"></a><span data-ttu-id="157e1-155">摘要</span><span class="sxs-lookup"><span data-stu-id="157e1-155">Summary</span></span>

<span data-ttu-id="157e1-156">地理距离是有助于延迟的最大因素之一。</span><span class="sxs-lookup"><span data-stu-id="157e1-156">Geographic distance is one of the biggest factors that contributes to latency.</span></span> <span data-ttu-id="157e1-157">使用流量管理器时, 您可以在多个地理区域中托管服务的精确副本。</span><span class="sxs-lookup"><span data-stu-id="157e1-157">With Traffic Manager in place, you can host exact copies of your service in multiple geographic regions.</span></span> <span data-ttu-id="157e1-158">这样一来, 美国、欧洲和亚洲的用户就可以使用电子商务网站。</span><span class="sxs-lookup"><span data-stu-id="157e1-158">That way, users in the United States, Europe, and Asia will all have a good experience using your e-commerce site.</span></span>
