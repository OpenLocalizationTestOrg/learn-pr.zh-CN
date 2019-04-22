<span data-ttu-id="9b557-101">随着计算环境从客户控制的数据中心移动到云数据中心, 安全性的责任也随之变化。</span><span class="sxs-lookup"><span data-stu-id="9b557-101">As computing environments move from customer-controlled data centers to cloud data centers, the responsibility of security also shifts.</span></span> <span data-ttu-id="9b557-102">现在, 安全性是由云提供商和客户共同关注的。</span><span class="sxs-lookup"><span data-stu-id="9b557-102">Security is now a concern shared both by cloud providers and customers.</span></span> <span data-ttu-id="9b557-103">对于每个应用程序和解决方案, 重要的是了解你的责任是什么以及什么 Azure's 责任。</span><span class="sxs-lookup"><span data-stu-id="9b557-103">For every application and solution, it's important to understand what's your responsibility and what's Azure's responsibility.</span></span>

#### <a name="understand-security-threats"></a><span data-ttu-id="9b557-104">了解安全威胁</span><span class="sxs-lookup"><span data-stu-id="9b557-104">Understand security threats</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWkotg]

#### <a name="azure-security-you-versus-the-cloud"></a><span data-ttu-id="9b557-105">Azure 安全性: 您与云的对比</span><span class="sxs-lookup"><span data-stu-id="9b557-105">Azure security: you versus the cloud</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvj]

## <a name="share-security-responsibility-with-azure"></a><span data-ttu-id="9b557-106">与 Azure 共享安全责任</span><span class="sxs-lookup"><span data-stu-id="9b557-106">Share security responsibility with Azure</span></span>

<span data-ttu-id="9b557-107">您首先要做的是从本地数据中心到作为服务 (IaaS) 的基础结构。</span><span class="sxs-lookup"><span data-stu-id="9b557-107">The first shift you’ll make is from on-premises data centers to infrastructure as a service (IaaS).</span></span> <span data-ttu-id="9b557-108">通过 IaaS, 你可以利用最低级别的服务, 并要求 Azure 创建虚拟机 (vm) 和虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="9b557-108">With IaaS, you are leveraging the lowest-level service and asking Azure to create virtual machines (VMs) and virtual networks.</span></span> <span data-ttu-id="9b557-109">在此级别, 仍有责任对操作系统和软件进行修补和保护, 并将您的网络配置为安全。</span><span class="sxs-lookup"><span data-stu-id="9b557-109">At this level, it's still your responsibility to patch and secure your operating systems and software, as well as configure your network to be secure.</span></span> <span data-ttu-id="9b557-110">在 Contoso 发货时, 在开始使用 Azure 虚拟机而不是本地物理服务器时, 利用 IaaS。</span><span class="sxs-lookup"><span data-stu-id="9b557-110">At Contoso Shipping, you are taking advantage of IaaS when you start using Azure VMs instead of your on-premises physical servers.</span></span> <span data-ttu-id="9b557-111">除了运营优势之外, 您还会收到在保护网络物理部分方面考虑外包问题的安全优势。</span><span class="sxs-lookup"><span data-stu-id="9b557-111">In addition to the operational advantages, you receive the security advantage of having outsourced concern over protecting the physical parts of the network.</span></span>

<span data-ttu-id="9b557-112">迁移到平台服务 (PaaS) outsources 有许多安全问题。</span><span class="sxs-lookup"><span data-stu-id="9b557-112">Moving to platform as a service (PaaS) outsources a lot of security concerns.</span></span> <span data-ttu-id="9b557-113">在此级别, Azure 将负责操作系统和大多数基础软件 (如数据库管理系统)。</span><span class="sxs-lookup"><span data-stu-id="9b557-113">At this level, Azure is taking care of the operating system and of most foundational software like database management systems.</span></span> <span data-ttu-id="9b557-114">所有内容都使用最新的安全修补程序进行更新, 并可与用于访问控制的 Azure Active Directory 集成。</span><span class="sxs-lookup"><span data-stu-id="9b557-114">Everything is updated with the latest security patches and can be integrated with Azure Active Directory for access controls.</span></span> <span data-ttu-id="9b557-115">PaaS 还具有许多操作优势。</span><span class="sxs-lookup"><span data-stu-id="9b557-115">PaaS also comes with a lot of operational advantages.</span></span> <span data-ttu-id="9b557-116">你可以通过手动为你的环境构建完整的基础结构和子网, 也可以在 Azure 门户内 "指向并单击", 或者运行自动化脚本以将复杂、受保护的系统放在一起, 并根据需要进行扩展。</span><span class="sxs-lookup"><span data-stu-id="9b557-116">Rather than building whole infrastructures and subnets for your environments by hand, you can "point and click" within the Azure portal or run automated scripts to bring complex, secured systems up and down, and scale them as needed.</span></span> <span data-ttu-id="9b557-117">Contoso 装运将 azure 事件中心用于来自 drones 和卡车&mdash;的 ingesting 遥测数据, 以及使用包含所有 PaaS 示例的移动应用&mdash;的 azure Cosmos DB 后端的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b557-117">Contoso Shipping uses Azure Event Hubs for ingesting telemetry data from drones and trucks &mdash; as well as a web app with an Azure Cosmos DB back end with its mobile apps &mdash; which are all examples of PaaS.</span></span>

<span data-ttu-id="9b557-118">通过软件即服务 (SaaS), 您几乎可以为所有内容提供外包。</span><span class="sxs-lookup"><span data-stu-id="9b557-118">With software as a service (SaaS), you outsource almost everything.</span></span> <span data-ttu-id="9b557-119">SaaS 是使用 internet 基础结构运行的软件。</span><span class="sxs-lookup"><span data-stu-id="9b557-119">SaaS is software that runs with an internet infrastructure.</span></span> <span data-ttu-id="9b557-120">代码由供应商控制, 但配置为供客户使用。</span><span class="sxs-lookup"><span data-stu-id="9b557-120">The code is controlled by the vendor but configured to be used by the customer.</span></span> <span data-ttu-id="9b557-121">就像许多公司一样, Contoso 发售使用 Office 365, 这是 SaaS 的一个很好的示例!</span><span class="sxs-lookup"><span data-stu-id="9b557-121">Like so many companies, Contoso Shipping uses Office 365, which is a great example of SaaS!</span></span>

![展示了云提供商和客户如何在不同类型的计算服务实施中共享安全职责的说明: 本地、基础结构作为服务、平台作为服务以及软件作为服务。](../media/shared_responsibilities.png)

## <a name="a-layered-approach-to-security"></a><span data-ttu-id="9b557-123">安全的分层方法</span><span class="sxs-lookup"><span data-stu-id="9b557-123">A layered approach to security</span></span>

<span data-ttu-id="9b557-124">*纵深防御*是一种策略, 它采用一系列机制来降低攻击的提前速度, 以获取对信息的未经授权的访问。</span><span class="sxs-lookup"><span data-stu-id="9b557-124">*Defense in depth* is a strategy that employs a series of mechanisms to slow the advance of an attack aimed at acquiring unauthorized access to information.</span></span> <span data-ttu-id="9b557-125">每个层都提供保护, 以便在一个层受到破坏时, 后续层已经准备就绪, 以防止进一步暴露。</span><span class="sxs-lookup"><span data-stu-id="9b557-125">Each layer provides protection so that if one layer is breached, a subsequent layer is already in place to prevent further exposure.</span></span> <span data-ttu-id="9b557-126">Microsoft 在物理数据中心和 Azure 服务中对安全性应用分层方法。</span><span class="sxs-lookup"><span data-stu-id="9b557-126">Microsoft applies a layered approach to security, both in physical data centers and across Azure services.</span></span> <span data-ttu-id="9b557-127">纵深防御的目标是保护和防止未经授权访问信息的个人盗取信息。</span><span class="sxs-lookup"><span data-stu-id="9b557-127">The objective of defense in depth is to protect and prevent information from being stolen by individuals who are not authorized to access it.</span></span>

<span data-ttu-id="9b557-128">纵深防御可以可视化为一组同心圆环, 并在中心对数据进行保护。</span><span class="sxs-lookup"><span data-stu-id="9b557-128">Defense in depth can be visualized as a set of concentric rings, with the data to be secured at the center.</span></span> <span data-ttu-id="9b557-129">每个环都围绕数据添加了一个额外的安全性层。</span><span class="sxs-lookup"><span data-stu-id="9b557-129">Each ring adds an additional layer of security around the data.</span></span> <span data-ttu-id="9b557-130">这种方法消除了对任何单个保护层的依赖, 并采取行动以降低攻击速度, 并提供可自动或手动操作的警报遥测。</span><span class="sxs-lookup"><span data-stu-id="9b557-130">This approach removes reliance on any single layer of protection and acts to slow down an attack and provide alert telemetry that can be acted upon, either automatically or manually.</span></span> <span data-ttu-id="9b557-131">我们来看看每个图层。</span><span class="sxs-lookup"><span data-stu-id="9b557-131">Let's take a look at each of the layers.</span></span>

![显示数据中心的深度纵深防御的插图。](../media/defense_in_depth_layers_small.PNG)

:::row:::
  :::column:::
    ![表示数据的图像](../media/2-data.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-135">**Data**</span><span class="sxs-lookup"><span data-stu-id="9b557-135">**Data**</span></span>

<span data-ttu-id="9b557-136">在几乎所有情况下, 攻击者都是在数据之后:</span><span class="sxs-lookup"><span data-stu-id="9b557-136">In almost all cases, attackers are after data:</span></span>

- <span data-ttu-id="9b557-137">存储在数据库中</span><span class="sxs-lookup"><span data-stu-id="9b557-137">Stored in a database</span></span>
- <span data-ttu-id="9b557-138">存储在虚拟机内的磁盘上</span><span class="sxs-lookup"><span data-stu-id="9b557-138">Stored on disk inside virtual machines</span></span>
- <span data-ttu-id="9b557-139">存储在 SaaS 应用程序 (如 Office 365) 上</span><span class="sxs-lookup"><span data-stu-id="9b557-139">Stored on a SaaS application such as Office 365</span></span>
- <span data-ttu-id="9b557-140">存储在云存储中</span><span class="sxs-lookup"><span data-stu-id="9b557-140">Stored in cloud storage</span></span>

<span data-ttu-id="9b557-141">他们负责存储和控制对数据的访问, 以确保它得到了适当的保护。</span><span class="sxs-lookup"><span data-stu-id="9b557-141">It's the responsibility of those storing and controlling access to data to ensure that it's properly secured.</span></span> <span data-ttu-id="9b557-142">通常, 有一些法规要求规定了必须实施的控制和过程, 以确保数据的机密性、完整性和可用性。</span><span class="sxs-lookup"><span data-stu-id="9b557-142">Often, there are regulatory requirements that dictate the controls and processes that must be in place to ensure the confidentiality, integrity, and availability of the data.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![网络上的文件的图像](../media/2-application.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-144">**Application**</span><span class="sxs-lookup"><span data-stu-id="9b557-144">**Application**</span></span>

- <span data-ttu-id="9b557-145">确保应用程序安全且没有漏洞。</span><span class="sxs-lookup"><span data-stu-id="9b557-145">Ensure applications are secure and free of vulnerabilities.</span></span>
- <span data-ttu-id="9b557-146">将敏感的应用程序机密存储在安全存储媒体中。</span><span class="sxs-lookup"><span data-stu-id="9b557-146">Store sensitive application secrets in a secure storage medium.</span></span>
- <span data-ttu-id="9b557-147">使安全性成为所有应用程序开发的设计要求。</span><span class="sxs-lookup"><span data-stu-id="9b557-147">Make security a design requirement for all application development.</span></span>

<span data-ttu-id="9b557-148">将安全性集成到应用程序开发生命周期中有助于减少代码中引入的漏洞的数量。</span><span class="sxs-lookup"><span data-stu-id="9b557-148">Integrating security into the application development life cycle will help reduce the number of vulnerabilities introduced in code.</span></span> <span data-ttu-id="9b557-149">我们鼓励所有开发团队确保其应用程序在默认情况下是安全的, 并且他们要使安全要求成为非流通的。</span><span class="sxs-lookup"><span data-stu-id="9b557-149">We encourage all development teams to ensure their applications are secure by default, and that they're making security requirements non-negotiable.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![表示计算的终端](../media/2-compute.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-151">**计算**</span><span class="sxs-lookup"><span data-stu-id="9b557-151">**Compute**</span></span>

- <span data-ttu-id="9b557-152">对虚拟机的安全访问。</span><span class="sxs-lookup"><span data-stu-id="9b557-152">Secure access to virtual machines.</span></span>
- <span data-ttu-id="9b557-153">实施 endpoint protection 并使系统保持修补并保持最新。</span><span class="sxs-lookup"><span data-stu-id="9b557-153">Implement endpoint protection and keep systems patched and current.</span></span>

<span data-ttu-id="9b557-154">恶意软件、未经修补的系统和不正确的安全系统将环境打开为攻击。</span><span class="sxs-lookup"><span data-stu-id="9b557-154">Malware, unpatched systems, and improperly secured systems open your environment to attacks.</span></span> <span data-ttu-id="9b557-155">此层中的重点是确保您的计算资源是安全的, 并且您有适当的控件来最大限度地减少安全问题。</span><span class="sxs-lookup"><span data-stu-id="9b557-155">The focus in this layer is on making sure your compute resources are secure, and that you have the proper controls in place to minimize security issues.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![三个代表网络的连接系统](../media/2-networking.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-157">**连接**</span><span class="sxs-lookup"><span data-stu-id="9b557-157">**Networking**</span></span>

- <span data-ttu-id="9b557-158">限制资源之间的通信。</span><span class="sxs-lookup"><span data-stu-id="9b557-158">Limit communication between resources.</span></span>
- <span data-ttu-id="9b557-159">默认为 "拒绝"。</span><span class="sxs-lookup"><span data-stu-id="9b557-159">Deny by default.</span></span>
- <span data-ttu-id="9b557-160">在适当的情况下限制入站 internet 访问并限制出站。</span><span class="sxs-lookup"><span data-stu-id="9b557-160">Restrict inbound internet access and limit outbound, where appropriate.</span></span>
- <span data-ttu-id="9b557-161">实现到本地网络的安全连接。</span><span class="sxs-lookup"><span data-stu-id="9b557-161">Implement secure connectivity to on-premises networks.</span></span>

<span data-ttu-id="9b557-162">在此层, 重点是限制所有资源的网络连接, 仅允许所需的内容。</span><span class="sxs-lookup"><span data-stu-id="9b557-162">At this layer, the focus is on limiting the network connectivity across all your resources to allow only what is required.</span></span> <span data-ttu-id="9b557-163">通过限制此通信, 可以降低在整个网络中横向移动的风险。</span><span class="sxs-lookup"><span data-stu-id="9b557-163">By limiting this communication, you reduce the risk of lateral movement throughout your network.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![表示网络外围的物理障碍](../media/2-perimeter.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-165">**周边**</span><span class="sxs-lookup"><span data-stu-id="9b557-165">**Perimeter**</span></span>

- <span data-ttu-id="9b557-166">使用分布式拒绝服务 (DDoS) 保护来筛选大规模攻击, 然后才会对最终用户造成拒绝服务。</span><span class="sxs-lookup"><span data-stu-id="9b557-166">Use distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for end users.</span></span>
- <span data-ttu-id="9b557-167">使用外围防火墙识别网络上的恶意攻击并对其发出警报。</span><span class="sxs-lookup"><span data-stu-id="9b557-167">Use perimeter firewalls to identify and alert on malicious attacks against your network.</span></span>

<span data-ttu-id="9b557-168">在网络外围, 将抵御针对您的资源的基于网络的攻击的保护。</span><span class="sxs-lookup"><span data-stu-id="9b557-168">At the network perimeter, it's about protecting from network-based attacks against your resources.</span></span> <span data-ttu-id="9b557-169">识别这些攻击, 消除其影响, 并在发生这些攻击时向您发出警报是保护网络安全的重要方法。</span><span class="sxs-lookup"><span data-stu-id="9b557-169">Identifying these attacks, eliminating their impact, and alerting you when they happen are important ways to keep your network secure.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![代表安全访问的徽章](../media/2-policies-and-access.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-171">**标识和访问**</span><span class="sxs-lookup"><span data-stu-id="9b557-171">**Identity and access**</span></span>

- <span data-ttu-id="9b557-172">控制对基础结构的访问和更改控制。</span><span class="sxs-lookup"><span data-stu-id="9b557-172">Control access to infrastructure and change control.</span></span>
- <span data-ttu-id="9b557-173">使用单一登录和多因素身份验证。</span><span class="sxs-lookup"><span data-stu-id="9b557-173">Use single sign-on and multi-factor authentication.</span></span>
- <span data-ttu-id="9b557-174">审核事件和更改。</span><span class="sxs-lookup"><span data-stu-id="9b557-174">Audit events and changes.</span></span>

<span data-ttu-id="9b557-175">标识和访问层都是为了确保标识是安全的, 因此授予的访问权限只是所需的, 并且会记录更改。</span><span class="sxs-lookup"><span data-stu-id="9b557-175">The identity and access layer is all about ensuring identities are secure, access granted is only what is needed, and changes are logged.</span></span>
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![表示物理安全性的安全相机](../media/2-physical-security.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="9b557-177">**物理安全性**</span><span class="sxs-lookup"><span data-stu-id="9b557-177">**Physical security**</span></span>

- <span data-ttu-id="9b557-178">物理构建安全性和控制对数据中心内的计算硬件的访问是第一防线。</span><span class="sxs-lookup"><span data-stu-id="9b557-178">Physical building security and controlling access to computing hardware within the data center is the first line of defense.</span></span>

<span data-ttu-id="9b557-179">使用物理安全, 目的是提供物理保护措施以防止对资产的访问。</span><span class="sxs-lookup"><span data-stu-id="9b557-179">With physical security, the intent is to provide physical safeguards against access to assets.</span></span> <span data-ttu-id="9b557-180">这可以确保不会绕过其他层, 并适当地处理丢失或被盗用的情况。</span><span class="sxs-lookup"><span data-stu-id="9b557-180">This ensures that other layers can't be bypassed, and loss or theft is handled appropriately.</span></span>
  :::column-end:::
:::row-end:::

## <a name="summary"></a><span data-ttu-id="9b557-181">摘要</span><span class="sxs-lookup"><span data-stu-id="9b557-181">Summary</span></span>

<span data-ttu-id="9b557-182">我们已在此处了解到, Azure 可帮助您进行更多的安全关注。</span><span class="sxs-lookup"><span data-stu-id="9b557-182">We've seen here that Azure helps a lot with your security concerns.</span></span> <span data-ttu-id="9b557-183">但安全性仍是一个**共同的责任**。</span><span class="sxs-lookup"><span data-stu-id="9b557-183">But security is still a **shared responsibility**.</span></span> <span data-ttu-id="9b557-184">此职责中有多少取决于我们与 Azure 结合使用的模型。</span><span class="sxs-lookup"><span data-stu-id="9b557-184">How much of that responsibility falls on us depends on which model we use with Azure.</span></span>

<span data-ttu-id="9b557-185">我们使用*纵深防御*环作为指导来考虑哪些保护对于我们的数据和环境是足够的。</span><span class="sxs-lookup"><span data-stu-id="9b557-185">We use the *defense in depth* rings as a guideline for considering what protections are adequate for our data and environments.</span></span>
