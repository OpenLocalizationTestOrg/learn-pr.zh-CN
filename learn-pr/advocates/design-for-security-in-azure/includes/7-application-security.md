<span data-ttu-id="83e8b-101">与传统的本地部署相比, 在云平台上托管应用程序可提供多种优势。</span><span class="sxs-lookup"><span data-stu-id="83e8b-101">Hosting applications on a cloud platform provides a number of advantages when compared to traditional on-premises deployments.</span></span> <span data-ttu-id="83e8b-102">云的共享责任模型将安全性移动到物理网络、生成和主机级别下, 在云提供程序的控制之下。</span><span class="sxs-lookup"><span data-stu-id="83e8b-102">The cloud's shared-responsibility model moves security at the physical network, building, and host levels under the control of the cloud provider.</span></span> <span data-ttu-id="83e8b-103">试图在此级别危害平台的攻击者将看到不断发生的返回, 而不是大量的投资和洞察力提供商在保护和监视其基础结构方面做出的努力。</span><span class="sxs-lookup"><span data-stu-id="83e8b-103">An attacker trying to compromise the platform at this level would see diminishing returns versus the considerable investment and insight providers make in securing and monitoring their infrastructure.</span></span>

<span data-ttu-id="83e8b-104">因此, 攻击者可以更有效地实现云平台客户在应用程序级别引入的漏洞。</span><span class="sxs-lookup"><span data-stu-id="83e8b-104">It's therefore far more effective for attackers to pursue vulnerabilities introduced at the application level by cloud-platform customers.</span></span> <span data-ttu-id="83e8b-105">此外, 通过采用 Platform for Service (PaaS) 托管其应用程序, 客户可以从管理操作系统安全中释放资源, 并将其部署为加强应用程序代码并监视应用程序周围的标识外围环境。</span><span class="sxs-lookup"><span data-stu-id="83e8b-105">Furthermore, by adopting Platform as a Service (PaaS) to host their applications, customers are able to free resources from managing operating system security and deploy them to harden application code and monitor the identity perimeter around the application.</span></span> <span data-ttu-id="83e8b-106">在此单元中, 我们将讨论一些通过设计改进应用程序安全性的方法。</span><span class="sxs-lookup"><span data-stu-id="83e8b-106">In this unit we will discuss some of the ways application security can be improved through design.</span></span>

## <a name="scenario"></a><span data-ttu-id="83e8b-107">方案</span><span class="sxs-lookup"><span data-stu-id="83e8b-107">Scenario</span></span>

<span data-ttu-id="83e8b-108">Lamna 医疗保健客户需要通过联机 web 门户访问其个人医疗记录。</span><span class="sxs-lookup"><span data-stu-id="83e8b-108">Lamna Healthcare customers require access to their personal medical records through an online web portal.</span></span> <span data-ttu-id="83e8b-109">遵守健康保险便携性和责任法案 (HIPAA) 是必需的, 如果发生个人数据泄露, 则会将公司的财务处罚降低为严重风险。因此, 将与之交互的应用程序和个人数据的安全是极其重要的。</span><span class="sxs-lookup"><span data-stu-id="83e8b-109">Compliance with the Health Insurance Portability and Accountability Act (HIPAA) is mandatory and puts the company at significant risk of financial penalties if a breach of personal data occurs; therefore, securing the application and personal data it interacts with is paramount.</span></span>

<span data-ttu-id="83e8b-110">客户应用程序关注的主要方面是:</span><span class="sxs-lookup"><span data-stu-id="83e8b-110">The primary areas that concern customer applications are:</span></span>

- <span data-ttu-id="83e8b-111">安全应用程序设计</span><span class="sxs-lookup"><span data-stu-id="83e8b-111">Secure application design</span></span>
- <span data-ttu-id="83e8b-112">数据安全性</span><span class="sxs-lookup"><span data-stu-id="83e8b-112">Data security</span></span>
- <span data-ttu-id="83e8b-113">标识和访问管理</span><span class="sxs-lookup"><span data-stu-id="83e8b-113">Identity and access management</span></span>
- <span data-ttu-id="83e8b-114">终结点安全性</span><span class="sxs-lookup"><span data-stu-id="83e8b-114">Endpoint security</span></span>

## <a name="security-development-lifecycle"></a><span data-ttu-id="83e8b-115">安全开发生命周期</span><span class="sxs-lookup"><span data-stu-id="83e8b-115">Security Development Lifecycle</span></span>

<span data-ttu-id="83e8b-116">可以在应用程序设计阶段使用 Microsoft[安全开发生命周期](https://www.microsoft.com/sdl)(SDL) 流程, 以确保在软件开发生命周期中加入安全问题。</span><span class="sxs-lookup"><span data-stu-id="83e8b-116">Microsoft's [Security Development Lifecycle](https://www.microsoft.com/sdl) (SDL) process can be used during the application design stage to ensure security concerns are incorporated in the software development lifecycle.</span></span> <span data-ttu-id="83e8b-117">设计应用程序时, 安全性和合规性问题更易于解决, 并且可以减少可能导致最终产品的安全缺陷的许多常见错误。</span><span class="sxs-lookup"><span data-stu-id="83e8b-117">Security and compliance issues are far easier to address when designing an application and can mitigate many common errors that can lead to security flaws in the final product.</span></span> <span data-ttu-id="83e8b-118">在软件开发旅程早期修复问题也远远低于成本。</span><span class="sxs-lookup"><span data-stu-id="83e8b-118">Fixing issues early in the software development journey is also far less costly.</span></span> <span data-ttu-id="83e8b-119">软件项目可使用的 SDL SDL 步骤的典型顺序如下所示:</span><span class="sxs-lookup"><span data-stu-id="83e8b-119">The typical sequence of SDL steps a software project can use are as follows:</span></span>

1. <span data-ttu-id="83e8b-120">方面</span><span class="sxs-lookup"><span data-stu-id="83e8b-120">Training</span></span>

    - <span data-ttu-id="83e8b-121">核心安全培训</span><span class="sxs-lookup"><span data-stu-id="83e8b-121">Core security training</span></span>

1. <span data-ttu-id="83e8b-122">要求</span><span class="sxs-lookup"><span data-stu-id="83e8b-122">Requirements</span></span>

    - <span data-ttu-id="83e8b-123">定义要求和质量关口</span><span class="sxs-lookup"><span data-stu-id="83e8b-123">Define requirements and quality gates</span></span>
    - <span data-ttu-id="83e8b-124">分析安全和隐私风险</span><span class="sxs-lookup"><span data-stu-id="83e8b-124">Analyze security and privacy risks</span></span>
 
1. <span data-ttu-id="83e8b-125">Design</span><span class="sxs-lookup"><span data-stu-id="83e8b-125">Design</span></span>

    - <span data-ttu-id="83e8b-126">攻击面分析</span><span class="sxs-lookup"><span data-stu-id="83e8b-126">Attack surface analysis</span></span>
    - <span data-ttu-id="83e8b-127">威胁建模</span><span class="sxs-lookup"><span data-stu-id="83e8b-127">Threat modeling</span></span>
 
1. <span data-ttu-id="83e8b-128">实现</span><span class="sxs-lookup"><span data-stu-id="83e8b-128">Implementation</span></span>

    - <span data-ttu-id="83e8b-129">指定工具以确保可以测量代码质量</span><span class="sxs-lookup"><span data-stu-id="83e8b-129">Specify tools to ensure code quality can be measured</span></span>
    - <span data-ttu-id="83e8b-130">强制实施禁止的 api 和函数</span><span class="sxs-lookup"><span data-stu-id="83e8b-130">Enforce banned APIs and functions</span></span>
    - <span data-ttu-id="83e8b-131">执行静态代码分析</span><span class="sxs-lookup"><span data-stu-id="83e8b-131">Perform static code analysis</span></span>
    - <span data-ttu-id="83e8b-132">扫描存储的机密存储库</span><span class="sxs-lookup"><span data-stu-id="83e8b-132">Scan repositories for stored secrets</span></span>
 
1. <span data-ttu-id="83e8b-133">校验</span><span class="sxs-lookup"><span data-stu-id="83e8b-133">Verification</span></span>

    - <span data-ttu-id="83e8b-134">动态/Fuzz 测试</span><span class="sxs-lookup"><span data-stu-id="83e8b-134">Dynamic/Fuzz testing</span></span>
    - <span data-ttu-id="83e8b-135">验证威胁模型/攻击面</span><span class="sxs-lookup"><span data-stu-id="83e8b-135">Verify threat models/attack surface</span></span>
 
1. <span data-ttu-id="83e8b-136">7。2</span><span class="sxs-lookup"><span data-stu-id="83e8b-136">Release</span></span>

    - <span data-ttu-id="83e8b-137">表单安全响应计划</span><span class="sxs-lookup"><span data-stu-id="83e8b-137">Form security response plan</span></span>
    - <span data-ttu-id="83e8b-138">执行最终安全评审</span><span class="sxs-lookup"><span data-stu-id="83e8b-138">Perform a final security review</span></span>
    - <span data-ttu-id="83e8b-139">发布存档</span><span class="sxs-lookup"><span data-stu-id="83e8b-139">Release archive</span></span>
 
1. <span data-ttu-id="83e8b-140">响应</span><span class="sxs-lookup"><span data-stu-id="83e8b-140">Response</span></span> 

    - <span data-ttu-id="83e8b-141">执行威胁响应执行</span><span class="sxs-lookup"><span data-stu-id="83e8b-141">Execute threat response execution</span></span>

![显示安全开发生命周期的 illustraton](../media/sdl.png)

<span data-ttu-id="83e8b-143">SDL 的文化方面相当于一个过程或一组工具。</span><span class="sxs-lookup"><span data-stu-id="83e8b-143">The SDL is as much a cultural aspect as it is a process or set of tools.</span></span> <span data-ttu-id="83e8b-144">构建一个区域性, 其中安全是任何应用程序开发的主要焦点和要求会对组织在安全方面的能力的发展产生极大的努力。</span><span class="sxs-lookup"><span data-stu-id="83e8b-144">Building a culture where security is a primary focus and requirement of any application development can make great strides in evolving an organization's capabilities around security.</span></span>

<!-- Bear in mind that the migration of un-modified applications (especially COTS procured software systems) will not be able to perform many of the steps listed above.
 -->

## <a name="operational-security-assessment"></a><span data-ttu-id="83e8b-145">操作安全评估</span><span class="sxs-lookup"><span data-stu-id="83e8b-145">Operational security assessment</span></span>

<span data-ttu-id="83e8b-146">部署应用程序后, 必须不断评估其安全状态, 确定如何缓解发现的任何问题, 并将知识反馈回软件开发周期。</span><span class="sxs-lookup"><span data-stu-id="83e8b-146">Once an application has been deployed, it's essential to continually evaluate its security posture, determine how to mitigate any issues that are discovered, and feed the knowledge back into the software development cycle.</span></span> <span data-ttu-id="83e8b-147">执行此操作的深度是软件开发和运营团队的成熟度级别以及数据隐私要求的因素。</span><span class="sxs-lookup"><span data-stu-id="83e8b-147">The depth to which this is performed is a factor of the maturity level of the software development and operational teams as well as the data privacy requirements.</span></span>

<span data-ttu-id="83e8b-148">安全漏洞扫描软件服务可用于帮助自动化此过程并在定期节奏上评估安全问题, 而无需为团队带来成本高昂的手动过程 (如渗透测试)。</span><span class="sxs-lookup"><span data-stu-id="83e8b-148">Security vulnerability scanning software services are available to help automate this process and assess security concerns on a regular cadence, without burdening teams with costly manual processes, such as penetration testing.</span></span>

<span data-ttu-id="83e8b-149">azure 安全中心是在默认情况下为所有 azure 订阅启用的免费服务, 与其他 azure 应用程序级别的服务 (如 Azure 应用程序网关和 azure Web 应用程序防火墙) 紧密集成。</span><span class="sxs-lookup"><span data-stu-id="83e8b-149">Azure Security Center is a free service, now enabled by default for all Azure subscriptions, that is tightly integrated with other Azure application level services, such as Azure Application Gateway and Azure Web Application Firewall.</span></span> <span data-ttu-id="83e8b-150">通过分析这些服务中的日志, ASC 可以实时报告已知漏洞, 建议对其进行缓解, 甚至将其配置为在响应攻击时自动执行行动手册。</span><span class="sxs-lookup"><span data-stu-id="83e8b-150">By analyzing logs from these services, ASC can report on known vulnerabilities in real time, recommend responses to mitigate them, and even be configured to automatically execute playbooks in response to attacks.</span></span>

<!-- SDL culture
Key Vault / MSI
CSE = App  -> DB & App Storage
Mention approach of code scanning & SDL
Scanning for passwords - Git
 -->

## <a name="identity-as-the-perimeter"></a><span data-ttu-id="83e8b-151">标识作为外围设备</span><span class="sxs-lookup"><span data-stu-id="83e8b-151">Identity as the perimeter</span></span>

<span data-ttu-id="83e8b-152">身份验证成为应用程序防御的第一行。</span><span class="sxs-lookup"><span data-stu-id="83e8b-152">Identity validation is becoming the first line in defense for applications.</span></span> <span data-ttu-id="83e8b-153">通过对会话进行身份验证和授权, 限制对 web 应用程序的访问可以大大减少受攻击面。</span><span class="sxs-lookup"><span data-stu-id="83e8b-153">Restricting access to a web application by authenticating and authorizing sessions can drastically reduce the attack surface area.</span></span> <span data-ttu-id="83e8b-154">azure ad 和 azure ad B2C 提供了一种有效的方法来分担身份和访问完全管理的服务的责任。</span><span class="sxs-lookup"><span data-stu-id="83e8b-154">Azure AD and Azure AD B2C offer an effective way to offload the responsibility of identity and access to a fully managed service.</span></span> <span data-ttu-id="83e8b-155">Azure AD 条件访问策略、特权标识管理和标识保护控件进一步增强了客户阻止未经授权的访问和审核更改的能力。</span><span class="sxs-lookup"><span data-stu-id="83e8b-155">Azure AD conditional access policies, privileged identity management, and Identity Protection controls further enhance a customer's ability to prevent unauthorized access and audit changes.</span></span>

## <a name="data-protection"></a><span data-ttu-id="83e8b-156">数据保护</span><span class="sxs-lookup"><span data-stu-id="83e8b-156">Data protection</span></span>

<span data-ttu-id="83e8b-157">如果不是针对 web 应用程序的所有攻击, 则客户数据是大多数情况下的目标。</span><span class="sxs-lookup"><span data-stu-id="83e8b-157">Customer data is the target for most, if not all attacks against web applications.</span></span> <span data-ttu-id="83e8b-158">在应用程序与其数据存储层之间, 数据的安全存储和传输是极其重要的。</span><span class="sxs-lookup"><span data-stu-id="83e8b-158">The secure storage and transport of data between an application and its data storage layer is paramount.</span></span>

<span data-ttu-id="83e8b-159">Lamna 保健存储和访问特别敏感的患者医疗记录数据。</span><span class="sxs-lookup"><span data-stu-id="83e8b-159">Lamna Healthcare stores and accesses particularly sensitive patient medical record data.</span></span> <span data-ttu-id="83e8b-160">由美国国会在1996中代理的 HIPAA, 用于定义医疗保健提供商和雇主的电子医疗保健交易的国家标准。</span><span class="sxs-lookup"><span data-stu-id="83e8b-160">HIPAA, enacted by the United States Congress in 1996, among other controls, defines the national standards for electronic healthcare transactions by healthcare providers and employers.</span></span> <span data-ttu-id="83e8b-161">Lamna 必须确保患者和授权方 (如其医生) 可以安全地访问医疗数据。</span><span class="sxs-lookup"><span data-stu-id="83e8b-161">Lamna must ensure patients and authorized parties, such as their physicians, have secure access to medical data.</span></span>

<span data-ttu-id="83e8b-162">为了符合这些要求, Lamna 医疗保健已修改其应用程序, 以在 rest 和运输中对所有患者数据进行加密。</span><span class="sxs-lookup"><span data-stu-id="83e8b-162">To comply with these requirements, Lamna Healthcare has modified their applications to encrypt all patient data at rest and in transit.</span></span> <span data-ttu-id="83e8b-163">例如, 传输层安全性 (TLS) 用于对 web 应用程序和后端 SQL 数据库之间交换的数据进行加密。</span><span class="sxs-lookup"><span data-stu-id="83e8b-163">For example, Transport Layer Security (TLS) is used to encrypt data exchanged between the web application and back-end SQL databases.</span></span> <span data-ttu-id="83e8b-164">在 SQL Server 中, 数据也使用透明数据加密 (TDE) 进行加密, 以确保即使环境受到威胁, 在没有正确解密密钥的情况下, 任何人都将无法使用数据。</span><span class="sxs-lookup"><span data-stu-id="83e8b-164">Data is also encrypted at rest in SQL Server using Transparent Data Encryption (TDE), ensuring that even if the environment is compromised, data is effectively useless to anyone without the correct decryption keys.</span></span>

<span data-ttu-id="83e8b-165">若要加密存储在 blob 存储中的数据, 可以使用客户端加密来加密内存中的数据, 然后再将其写入存储服务。</span><span class="sxs-lookup"><span data-stu-id="83e8b-165">To encrypt data stored in blob storage, client-side encryption can be used to encrypt the data in memory before it's written to the storage service.</span></span> <span data-ttu-id="83e8b-166">支持此加密的库适用于 .net、Java 和 Python, 并支持将数据加密直接集成到应用程序中, 以增强数据完整性。</span><span class="sxs-lookup"><span data-stu-id="83e8b-166">Libraries supporting this encryption are available for .NET, Java, and Python, and enable the integration of data encryption directly into applications to enhance data integrity.</span></span>

### <a name="secure-key-and-secret-storage"></a><span data-ttu-id="83e8b-167">安全密钥和密钥存储</span><span class="sxs-lookup"><span data-stu-id="83e8b-167">Secure key and secret storage</span></span>

<span data-ttu-id="83e8b-168">将应用程序机密 (连接字符串、密码等) 和用于访问数据的应用程序中的加密密钥隔开是至关重要的。</span><span class="sxs-lookup"><span data-stu-id="83e8b-168">Separating application secrets (connection strings, passwords, etc.) and encryption keys from the application used to access data is vital.</span></span> <span data-ttu-id="83e8b-169">加密密钥和应用程序机密永远不应存储在配置文件的应用程序代码中。</span><span class="sxs-lookup"><span data-stu-id="83e8b-169">Encryption keys and application secrets should never be stored in the application code of configuration files.</span></span> <span data-ttu-id="83e8b-170">相反, 应使用一个安全存储 (如 Azure Key Vault)。</span><span class="sxs-lookup"><span data-stu-id="83e8b-170">Instead, a secure store such as Azure Key Vault should be used.</span></span> <span data-ttu-id="83e8b-171">然后, 可以通过托管服务标识将对此敏感数据的访问限制为应用程序标识, 并且可以定期轮换密钥以限制加密密钥泄露情况的暴露。</span><span class="sxs-lookup"><span data-stu-id="83e8b-171">Access to this sensitive data can then be limited to application identities through Managed Service Identities, and keys can be rotated on a regular basis to limit exposure in the case of encryption key leakage.</span></span> <span data-ttu-id="83e8b-172">客户还可以选择使用本地硬件安全模块 (HSM) 生成的自己的加密密钥, 甚至强制在单租户的离散 hsm 中实施 Azure Key Vault 实例。</span><span class="sxs-lookup"><span data-stu-id="83e8b-172">Customers can also choose to use their own encryption keys generated by on-premises Hardware Security Modules (HSM) and even mandate that Azure Key Vault instances are implemented in single-tenant, discrete HSMs.</span></span>

<!-- ### Secure and immutable file storage

All Azure storage accounts are encrypted by default using Microsoft managed keys. Azure customers also have the ability to use their own encryption keys (BYOK) to encrypt blob, file and queue data so that even the hosting provider has no access to unencrypted data. Data immutability is often required for auditing purposes or when legal disputes call for data to be effectively frozen for a determined amount of time. Azure has recently introduced an [immutable data storage](https://docs.microsoft.com/azure/storage/blobs/storage-blob-immutable-storage) option known as Write-Once, Read many (WORM) for this scenario. -->
