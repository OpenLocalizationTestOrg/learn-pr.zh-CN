<span data-ttu-id="d8623-101">您的第一步可能是在云中重新创建本地配置。</span><span class="sxs-lookup"><span data-stu-id="d8623-101">Your first step will likely be to re-create your on-premises configuration in the cloud.</span></span>

<span data-ttu-id="d8623-102">这一基本配置将让你了解如何配置网络, 以及网络流量在 Azure 中的移动方式。</span><span class="sxs-lookup"><span data-stu-id="d8623-102">This basic configuration will give you a sense of how networks are configured, and how network traffic moves in and out of Azure.</span></span>

## <a name="your-e-commerce-site-at-a-glance"></a><span data-ttu-id="d8623-103">你的电子商务网站概览</span><span class="sxs-lookup"><span data-stu-id="d8623-103">Your e-commerce site at a glance</span></span>

<span data-ttu-id="d8623-104">较大的企业系统通常由多个相互连接的应用程序和可协同工作的服务组成。</span><span class="sxs-lookup"><span data-stu-id="d8623-104">Larger enterprise systems are often composed of multiple inter-connected applications and services that work together.</span></span> <span data-ttu-id="d8623-105">您可能有一个显示清单的前端 web 系统, 并允许客户创建订单。</span><span class="sxs-lookup"><span data-stu-id="d8623-105">You might have a front-end web system that displays inventory and allows customers to create an order.</span></span> <span data-ttu-id="d8623-106">这可能会与各种 web 服务通信, 以提供库存数据、管理用户配置文件、处理信用卡以及请求执行已处理的订单。</span><span class="sxs-lookup"><span data-stu-id="d8623-106">That might talk to a variety of web services to provide the inventory data, manage user profiles, process credit cards, and request fulfillment of processed orders.</span></span>

<span data-ttu-id="d8623-107">软件架构师和设计人员采用几种策略和模式, 使这些复杂系统更易于设计、构建、管理和维护。</span><span class="sxs-lookup"><span data-stu-id="d8623-107">There are several strategies and patterns employed by software architects and designers to make these complex systems easier to design, build, manage, and maintain.</span></span> <span data-ttu-id="d8623-108">让我们来看看其中的几个问题, 从_松散结合的体系结构_开始。</span><span class="sxs-lookup"><span data-stu-id="d8623-108">Let's look at a few of them, starting with _loosely coupled architectures_.</span></span>

### <a name="benefits-of-loosely-coupled-architectures"></a><span data-ttu-id="d8623-109">松散耦合体系结构的好处</span><span class="sxs-lookup"><span data-stu-id="d8623-109">Benefits of Loosely Coupled Architectures</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yHrc]

### <a name="using-an-n-tier-architecture"></a><span data-ttu-id="d8623-110">使用 N 层体系结构</span><span class="sxs-lookup"><span data-stu-id="d8623-110">Using an N-tier architecture</span></span>

<span data-ttu-id="d8623-111">可用于构建松散耦合系统的体系结构模式为_N 层_。</span><span class="sxs-lookup"><span data-stu-id="d8623-111">An architectural pattern that can be used to build loosely coupled systems is _N-tier_.</span></span>

<span data-ttu-id="d8623-112">[N 层体系结构](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier)将应用程序划分为两个或更多个逻辑层。</span><span class="sxs-lookup"><span data-stu-id="d8623-112">An [N-tier architecture](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) divides an application into two or more logical tiers.</span></span> <span data-ttu-id="d8623-113">在体系结构上, 更高的层可以从较低层访问服务, 但较低层不应访问更高的层。</span><span class="sxs-lookup"><span data-stu-id="d8623-113">Architecturally, a higher tier can access services from a lower tier, but a lower tier should never access a higher tier.</span></span>

<span data-ttu-id="d8623-114">层帮助分离问题, 并理想设计为可重用。</span><span class="sxs-lookup"><span data-stu-id="d8623-114">Tiers help separate concerns and are ideally designed to be reusable.</span></span> <span data-ttu-id="d8623-115">使用分层体系结构还可以简化维护。</span><span class="sxs-lookup"><span data-stu-id="d8623-115">Using a tiered architecture also simplifies maintenance.</span></span> <span data-ttu-id="d8623-116">层可以独立进行更新或替换, 并且可以根据需要插入新的层。</span><span class="sxs-lookup"><span data-stu-id="d8623-116">Tiers can be updated or replaced independently, and new tiers can be inserted if needed.</span></span>

<span data-ttu-id="d8623-117">_三层_指具有三个层的 n 层应用程序。</span><span class="sxs-lookup"><span data-stu-id="d8623-117">_Three-tier_ refers to an n-tier application that has three tiers.</span></span> <span data-ttu-id="d8623-118">您的电子商务 web 应用程序遵循以下三层体系结构:</span><span class="sxs-lookup"><span data-stu-id="d8623-118">Your e-commerce web application follows this three-tier architecture:</span></span>

* <span data-ttu-id="d8623-119">**web 层**通过浏览器向你的用户提供 web 界面。</span><span class="sxs-lookup"><span data-stu-id="d8623-119">The **web tier** provides the web interface to your users through a browser.</span></span>
* <span data-ttu-id="d8623-120">**应用程序层**运行业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="d8623-120">The **application tier** runs business logic.</span></span>
* <span data-ttu-id="d8623-121">**数据层**包括保存产品信息和客户订单的数据库和其他存储。</span><span class="sxs-lookup"><span data-stu-id="d8623-121">The **data tier** includes databases and other storage that hold product information and customer orders.</span></span>

<span data-ttu-id="d8623-122">下图显示了从用户到数据层的请求流。</span><span class="sxs-lookup"><span data-stu-id="d8623-122">The following illustration shows the flow of a request from the user to the data tier.</span></span>

![图中显示了三层体系结构, 其中每个层都托管在专用虚拟机中。](../media/2-three-tier.png)

<span data-ttu-id="d8623-124">当用户单击按钮来下订单时, 请求将发送到 web 层, 以及用户的地址和付款信息。</span><span class="sxs-lookup"><span data-stu-id="d8623-124">When the user clicks the button to place the order, the request is sent to the web tier, along with the user's address and payment information.</span></span> <span data-ttu-id="d8623-125">web 层将此信息传递到应用程序层, 这将验证付款信息和检查库存。</span><span class="sxs-lookup"><span data-stu-id="d8623-125">The web tier passes this information to the application tier, which would validate payment information and check inventory.</span></span> <span data-ttu-id="d8623-126">然后, 应用程序层可能会将订单存储在数据层中, 以便稍后将其用于履单。</span><span class="sxs-lookup"><span data-stu-id="d8623-126">The application tier might then store the order in the data tier, to be picked up later for fulfillment.</span></span>

## <a name="your-e-commerce-site-running-on-azure"></a><span data-ttu-id="d8623-127">在 Azure 上运行的电子商务网站</span><span class="sxs-lookup"><span data-stu-id="d8623-127">Your e-commerce site running on Azure</span></span>

<span data-ttu-id="d8623-128">Azure 提供了多种不同的方式来托管您的 web 应用程序, 从托管您的代码的完全预配置环境到您配置、自定义和管理的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="d8623-128">Azure provides many different ways to host your web applications, from fully pre-configured environments that host your code, to virtual machines that you configure, customize, and manage.</span></span>

<span data-ttu-id="d8623-129">假设你选择在虚拟机上运行你的电子商务网站。</span><span class="sxs-lookup"><span data-stu-id="d8623-129">Let's say you choose to run your e-commerce site on virtual machines.</span></span> <span data-ttu-id="d8623-130">以下是在 Azure 上运行的测试环境中可能的外观。</span><span class="sxs-lookup"><span data-stu-id="d8623-130">Here's what that might look like in your test environment running on Azure.</span></span> <span data-ttu-id="d8623-131">下图显示了在启用了安全功能的虚拟机上运行的三层体系结构来限制入站请求。</span><span class="sxs-lookup"><span data-stu-id="d8623-131">The following illustration shows a three-tier architecture running on virtual machines with security features enabled to restrict inbound requests.</span></span> 

![图中显示了三层体系结构, 其中每个层在单独的虚拟机上运行。](../media/2-test-deployment.png)

<span data-ttu-id="d8623-135">让我们将其断开。</span><span class="sxs-lookup"><span data-stu-id="d8623-135">Let's break this down.</span></span>

:::row:::
  :::column:::
    ![代表 Azure 区域的地球上的固定位置](../media/2-azure-region.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="d8623-137">**什么是 Azure 区域？**</span><span class="sxs-lookup"><span data-stu-id="d8623-137">**What's an Azure region?**</span></span>

<span data-ttu-id="d8623-138">_区域_是特定地理位置中的 Azure 数据中心。</span><span class="sxs-lookup"><span data-stu-id="d8623-138">A _region_ is an Azure data center within a specific geographic location.</span></span> <span data-ttu-id="d8623-139">美国东部、美国西部和北欧是区域的示例。</span><span class="sxs-lookup"><span data-stu-id="d8623-139">East US, West US, and North Europe are examples of regions.</span></span> <span data-ttu-id="d8623-140">在此示例中, 您将看到应用程序正在美国东部地区运行。</span><span class="sxs-lookup"><span data-stu-id="d8623-140">In this instance, you see that the application is running in the East US region.</span></span>

  :::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![在虚拟网络上运行的两个虚拟机](../media/2-azure-vnet.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="d8623-142">**什么是虚拟网络？**</span><span class="sxs-lookup"><span data-stu-id="d8623-142">**What's a virtual network?**</span></span>

<span data-ttu-id="d8623-143">_虚拟网络_是 Azure 上逻辑隔离的网络。</span><span class="sxs-lookup"><span data-stu-id="d8623-143">A _virtual network_ is a logically isolated network on Azure.</span></span> <span data-ttu-id="d8623-144">如果你已在 hyper-v、VMware 甚至其他公共云上设置了网络, 则 Azure 虚拟网络将非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="d8623-144">Azure virtual networks will be familiar to you if you've set up networks on Hyper-V, VMware, or even on other public clouds.</span></span> <span data-ttu-id="d8623-145">虚拟网络允许 Azure 资源与彼此、internet 和本地网络之间的安全通信。</span><span class="sxs-lookup"><span data-stu-id="d8623-145">A virtual network allows Azure resources to securely communicate with each other, the internet, and on-premises networks.</span></span> <span data-ttu-id="d8623-146">虚拟网络的范围限定为单个区域;但是, 可以使用虚拟网络对等连接将不同区域中的多个虚拟网络连接在一起。</span><span class="sxs-lookup"><span data-stu-id="d8623-146">A virtual network is scoped to a single region; however, multiple virtual networks from different regions can be connected together using virtual network peering.</span></span> 

<span data-ttu-id="d8623-147">可以将虚拟网络分成一个或多_个子网_。</span><span class="sxs-lookup"><span data-stu-id="d8623-147">Virtual networks can be segmented into one or more _subnets_.</span></span> <span data-ttu-id="d8623-148">子网可帮助您在不连续的分区中组织和保护资源。</span><span class="sxs-lookup"><span data-stu-id="d8623-148">Subnets help you organize and secure your resources in discrete sections.</span></span> <span data-ttu-id="d8623-149">web、应用程序和数据层都有一个虚拟机。</span><span class="sxs-lookup"><span data-stu-id="d8623-149">The web, application, and data tiers each have a single VM.</span></span> <span data-ttu-id="d8623-150">所有三个虚拟机都位于同一个虚拟网络中, 但位于不同的子网中。</span><span class="sxs-lookup"><span data-stu-id="d8623-150">All three VMs are in the same virtual network but are in separate subnets.</span></span>

<span data-ttu-id="d8623-151">用户直接与 web 层交互, 因此虚拟机具有一个公用 ip 地址和一个专用 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="d8623-151">Users interact with the web tier directly, so that VM has a public IP address along with a private IP address.</span></span> <span data-ttu-id="d8623-152">用户不会与应用程序或数据层进行交互, 因此, 每个虚拟机都仅具有专用 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="d8623-152">Users don't interact with the application or data tiers, so these VMs each have a private IP address only.</span></span>

<span data-ttu-id="d8623-153">您还可以将您的服务或数据层保留在本地网络中, 将您的 web 层放入云中, 但保持对应用程序的其他方面的严格控制。</span><span class="sxs-lookup"><span data-stu-id="d8623-153">You can also keep your service or data tiers in your on-premises network, placing your web tier into the cloud, but keeping tight control over other aspects of your application.</span></span> <span data-ttu-id="d8623-154">_VPN 网关_(或虚拟网络网关) 启用此方案。</span><span class="sxs-lookup"><span data-stu-id="d8623-154">A _VPN gateway_ (or virtual network gateway), enables this scenario.</span></span> <span data-ttu-id="d8623-155">它可以提供 internet 上的 Azure 虚拟网络和本地位置的安全连接。</span><span class="sxs-lookup"><span data-stu-id="d8623-155">It can provide a secure connection an Azure Virtual Network and an on-premises location over the internet.</span></span>

<span data-ttu-id="d8623-156">Azure 为你管理物理硬件。</span><span class="sxs-lookup"><span data-stu-id="d8623-156">Azure manages the physical hardware for you.</span></span> <span data-ttu-id="d8623-157">通过软件配置虚拟网络和网关, 这使您可以像对待自己的网络那样对待虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="d8623-157">You configure virtual networks and gateways through software, which enables you to treat a virtual network just like your own network.</span></span> <span data-ttu-id="d8623-158">您可以选择您的虚拟网络可以连接到的网络, 而不管它是公用 internet 还是专用 IP 地址空间中的其他网络。</span><span class="sxs-lookup"><span data-stu-id="d8623-158">You choose which networks your virtual network can reach, whether that's the public internet or other networks in the private IP address space.</span></span>

  :::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![具有共享网络安全组的两台虚拟机](../media/2-azure-nsg.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="d8623-160">**什么是网络安全组？**</span><span class="sxs-lookup"><span data-stu-id="d8623-160">**What's a network security group?**</span></span>

<span data-ttu-id="d8623-161">_网络安全组_(或 NSG) 允许或拒绝到 Azure 资源的入站网络流量。</span><span class="sxs-lookup"><span data-stu-id="d8623-161">A _network security group_, or NSG, allows or denies inbound network traffic to your Azure resources.</span></span> <span data-ttu-id="d8623-162">将网络安全组视为网络的云级防火墙。</span><span class="sxs-lookup"><span data-stu-id="d8623-162">Think of a network security group as a cloud-level firewall for your network.</span></span>

<span data-ttu-id="d8623-163">例如, 请注意, web 层中的 VM 允许端口 22 (SSH) 和 80 (HTTP) 上的入站流量。</span><span class="sxs-lookup"><span data-stu-id="d8623-163">For example, notice that the VM in the web tier allows inbound traffic on ports 22 (SSH) and 80 (HTTP).</span></span> <span data-ttu-id="d8623-164">此 VM 的网络安全组允许来自所有源的来自这些端口的入站流量。</span><span class="sxs-lookup"><span data-stu-id="d8623-164">This VM's network security group allows inbound traffic over these ports from all sources.</span></span> <span data-ttu-id="d8623-165">可以将网络安全组配置为仅接受来自已知源 (如您信任的 IP 地址) 的通信。</span><span class="sxs-lookup"><span data-stu-id="d8623-165">You can configure a network security group to accept traffic only from known sources, such as IP addresses that you trust.</span></span>

> [!NOTE]
> <span data-ttu-id="d8623-166">端口22使你能够通过 SSH 直接连接到 Linux 系统。</span><span class="sxs-lookup"><span data-stu-id="d8623-166">Port 22 enables you to connect directly to Linux systems over SSH.</span></span> <span data-ttu-id="d8623-167">此处显示了端口22打开以供学习之用。</span><span class="sxs-lookup"><span data-stu-id="d8623-167">Here we show port 22 open for learning purposes.</span></span> <span data-ttu-id="d8623-168">在实践中, 您可以配置对虚拟网络的 VPN 访问以提高安全性。</span><span class="sxs-lookup"><span data-stu-id="d8623-168">In practice, you might configure VPN access to your virtual network to increase security.</span></span>

  :::column-end:::
:::row-end:::

## <a name="summary"></a><span data-ttu-id="d8623-169">摘要</span><span class="sxs-lookup"><span data-stu-id="d8623-169">Summary</span></span>

<span data-ttu-id="d8623-170">现在, 你的三层应用程序在美国东部地区的 Azure 上运行。</span><span class="sxs-lookup"><span data-stu-id="d8623-170">Your three-tier application is now running on Azure in the East US region.</span></span> <span data-ttu-id="d8623-171">_区域_是特定地理位置中的 Azure 数据中心。</span><span class="sxs-lookup"><span data-stu-id="d8623-171">A _region_ is an Azure data center within a specific geographic location.</span></span>

<span data-ttu-id="d8623-172">每个层只能从较低层访问服务。</span><span class="sxs-lookup"><span data-stu-id="d8623-172">Each tier can access services only from a lower tier.</span></span> <span data-ttu-id="d8623-173">在 web 层中运行的虚拟机具有公共 IP 地址, 因为它接收来自 internet 的流量。</span><span class="sxs-lookup"><span data-stu-id="d8623-173">The VM running in the web tier has a public IP address because it receives traffic from the internet.</span></span> <span data-ttu-id="d8623-174">较低层 (即应用程序和数据层) 中的 vm 都具有专用 IP 地址, 因为它们不会直接通过 internet 进行通信。</span><span class="sxs-lookup"><span data-stu-id="d8623-174">The VMs in the lower tiers, the application and data tiers, each have private IP addresses because they don't communicate directly over the internet.</span></span>

<span data-ttu-id="d8623-175">_虚拟网络_使您能够对相关系统进行分组和隔离。</span><span class="sxs-lookup"><span data-stu-id="d8623-175">_Virtual networks_ enable you to group and isolate related systems.</span></span> <span data-ttu-id="d8623-176">您可以定义_网络安全组_, 以控制哪些流量可以通过虚拟网络流动。</span><span class="sxs-lookup"><span data-stu-id="d8623-176">You define _network security groups_ to control what traffic can flow through a virtual network.</span></span>

<span data-ttu-id="d8623-177">您在此处看到的配置是一个很棒的开端。</span><span class="sxs-lookup"><span data-stu-id="d8623-177">The configuration you saw here is a good start.</span></span> <span data-ttu-id="d8623-178">但是, 当您将电子商务网站部署到云中的生产环境中时, 可能会遇到与您在本地部署中所做的相同问题。</span><span class="sxs-lookup"><span data-stu-id="d8623-178">But when you deploy your e-commerce site to production in the cloud, you'll likely run into the same problems as you did in your on-premises deployment.</span></span>    