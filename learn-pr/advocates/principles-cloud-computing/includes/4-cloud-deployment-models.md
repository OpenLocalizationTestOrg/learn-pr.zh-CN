<span data-ttu-id="93f73-101">共有三种不同的云部署模型。</span><span class="sxs-lookup"><span data-stu-id="93f73-101">There are three different cloud deployment models.</span></span> <span data-ttu-id="93f73-102">云部署模型定义数据的存储位置以及客户与之交互的方式–如何访问数据以及应用程序在哪里运行？</span><span class="sxs-lookup"><span data-stu-id="93f73-102">A cloud deployment model defines where your data is stored and how your customers interact with it – how do they get to it, and where do the applications run?</span></span> <span data-ttu-id="93f73-103">它还取决于您想要或需要管理的您自己的基础结构的多少。</span><span class="sxs-lookup"><span data-stu-id="93f73-103">It also depends on how much of your own infrastructure you want or need to manage.</span></span>

## <a name="explore-the-three-deployment-methods-of-cloud-computing"></a><span data-ttu-id="93f73-104">探索云计算的三种部署方法</span><span class="sxs-lookup"><span data-stu-id="93f73-104">Explore the three deployment methods of cloud computing</span></span>

#### <a name="public-versus-private-versus-hybrid"></a><span data-ttu-id="93f73-105">公用与专用与混合</span><span class="sxs-lookup"><span data-stu-id="93f73-105">Public versus Private versus Hybrid</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEv7]

:::row:::
  :::column span="3":::
### <a name="public-cloud"></a><span data-ttu-id="93f73-106">公共云</span><span class="sxs-lookup"><span data-stu-id="93f73-106">Public cloud</span></span>

<span data-ttu-id="93f73-107">这是最常见的部署模型。</span><span class="sxs-lookup"><span data-stu-id="93f73-107">This is the most common deployment model.</span></span> <span data-ttu-id="93f73-108">在这种情况下, 无需本地硬件即可管理或保持最新状态-一切都在云提供商的硬件上运行。</span><span class="sxs-lookup"><span data-stu-id="93f73-108">In this case, you have no local hardware to manage or keep up-to-date – everything runs on your cloud provider’s hardware.</span></span> <span data-ttu-id="93f73-109">在某些情况下, 您可以通过与其他云用户共享计算资源来节省额外的成本。</span><span class="sxs-lookup"><span data-stu-id="93f73-109">In some cases, you can save additional costs by sharing computing resources with other cloud users.</span></span>

<span data-ttu-id="93f73-110">企业可以使用不同规模的多个公共云提供商。</span><span class="sxs-lookup"><span data-stu-id="93f73-110">Businesses can use multiple public cloud providers of varying scale.</span></span> <span data-ttu-id="93f73-111">Microsoft Azure 是公共云提供商的一个示例。</span><span class="sxs-lookup"><span data-stu-id="93f73-111">Microsoft Azure is an example of a public cloud provider.</span></span>
  :::column-end:::
  :::column:::
![公共云图标](../media/4-public-cloud.png)
  :::column-end:::
:::row-end:::

#### <a name="advantages"></a><span data-ttu-id="93f73-113">在于</span><span class="sxs-lookup"><span data-stu-id="93f73-113">Advantages</span></span>
- <span data-ttu-id="93f73-114">高可扩展性/灵活性–无需购买新服务器即可扩展</span><span class="sxs-lookup"><span data-stu-id="93f73-114">High scalability/agility – you don’t have to buy a new server in order to scale</span></span>
- <span data-ttu-id="93f73-115">随价格付费–仅为您使用的内容付费, 无 CapEx 成本</span><span class="sxs-lookup"><span data-stu-id="93f73-115">Pay-as-you-go pricing – you pay only for what you use, no CapEx costs</span></span>
- <span data-ttu-id="93f73-116">你不负责维护或更新硬件</span><span class="sxs-lookup"><span data-stu-id="93f73-116">You’re not responsible for maintenance or updates of the hardware</span></span>
- <span data-ttu-id="93f73-117">设置和使用的技术知识最少-您可以利用云提供商的技能和专业知识来确保工作负载是安全、安全和高可用性</span><span class="sxs-lookup"><span data-stu-id="93f73-117">Minimal technical knowledge to set up and use - you can leverage the skills and expertise of the cloud provider to ensure workloads are secure, safe, and highly available</span></span>

<span data-ttu-id="93f73-118">一个常见的用例方案是在由云提供商拥有的硬件和资源上部署 web 应用程序或博客网站。</span><span class="sxs-lookup"><span data-stu-id="93f73-118">A common use case scenario is deploying a web application or a blog site on hardware and resources that are owned by a cloud provider.</span></span> <span data-ttu-id="93f73-119">通过在此方案中使用公共云, 云用户可以快速获取其网站或博客, 并将重点放在维护网站的同时, 而无需担心购买、管理或维护其运行的硬件。</span><span class="sxs-lookup"><span data-stu-id="93f73-119">Using a public cloud in this scenario allows cloud users to get their website or blog up quickly, and then focus on maintaining the site without having to worry about purchasing, managing or maintaining the hardware on which it runs.</span></span>

#### <a name="disadvantages"></a><span data-ttu-id="93f73-120">在于</span><span class="sxs-lookup"><span data-stu-id="93f73-120">Disadvantages</span></span>
<span data-ttu-id="93f73-121">并非所有方案都适用于公共云。</span><span class="sxs-lookup"><span data-stu-id="93f73-121">Not all scenarios fit the public cloud.</span></span> <span data-ttu-id="93f73-122">以下是一些需要考虑的缺点:</span><span class="sxs-lookup"><span data-stu-id="93f73-122">Here are some disadvantages to think about:</span></span>

- <span data-ttu-id="93f73-123">可能存在使用公共云无法满足的特定安全要求</span><span class="sxs-lookup"><span data-stu-id="93f73-123">There may be specific security requirements that cannot be met by using public cloud</span></span>
- <span data-ttu-id="93f73-124">可能存在公共云无法满足的政府策略、行业标准或法律要求</span><span class="sxs-lookup"><span data-stu-id="93f73-124">There may be government policies, industry standards, or legal requirements which public clouds cannot meet</span></span>
- <span data-ttu-id="93f73-125">你不拥有硬件或服务, 无法根据需要进行管理</span><span class="sxs-lookup"><span data-stu-id="93f73-125">You don't own the hardware or services and cannot manage them as they may wish</span></span>
- <span data-ttu-id="93f73-126">独特的业务要求, 例如维护旧版应用程序可能难以满足</span><span class="sxs-lookup"><span data-stu-id="93f73-126">Unique business requirements, such as having to maintain a legacy application might be hard to meet</span></span>

:::row:::
  :::column span="3":::
### <a name="private-cloud"></a><span data-ttu-id="93f73-127">私有云</span><span class="sxs-lookup"><span data-stu-id="93f73-127">Private cloud</span></span>

<span data-ttu-id="93f73-128">在私有云中, 您在自己的数据中心中创建云环境, 并提供自助服务访问权限, 以向组织中的用户计算资源。</span><span class="sxs-lookup"><span data-stu-id="93f73-128">In a private cloud, you create a cloud environment in your own datacenter and provide self-service access to compute resources to users in your organization.</span></span> <span data-ttu-id="93f73-129">这为你的用户提供了一个公共云模拟, 但你完全负责购买和维护你提供的硬件和软件服务。</span><span class="sxs-lookup"><span data-stu-id="93f73-129">This offers a simulation of a public cloud to your users, but you remain completely responsible for the purchase and maintenance of the hardware and software services you provide.</span></span>
  :::column-end:::
  :::column:::
![私有云图标](../media/4-private-cloud.png)
  :::column-end:::
:::row-end:::

#### <a name="advantages"></a><span data-ttu-id="93f73-131">在于</span><span class="sxs-lookup"><span data-stu-id="93f73-131">Advantages</span></span>
<span data-ttu-id="93f73-132">此方法有以下几个优点:</span><span class="sxs-lookup"><span data-stu-id="93f73-132">This approach has several advantages:</span></span>

- <span data-ttu-id="93f73-133">您可以完全控制资源并确保配置能够支持任何方案或旧版应用程序</span><span class="sxs-lookup"><span data-stu-id="93f73-133">You have complete control over the resources and can ensure the configuration can support any scenario or legacy application</span></span>
- <span data-ttu-id="93f73-134">你对安全具有完全控制 (和责任)</span><span class="sxs-lookup"><span data-stu-id="93f73-134">You have complete control (and responsibility) over security</span></span>
- <span data-ttu-id="93f73-135">私有云可以在公共云可能无法进行的方式下满足严格的安全性、合规性或法律要求</span><span class="sxs-lookup"><span data-stu-id="93f73-135">Private clouds can meet strict security, compliance, or legal requirements in ways a public cloud might not be able to</span></span>

#### <a name="disadvantages"></a><span data-ttu-id="93f73-136">在于</span><span class="sxs-lookup"><span data-stu-id="93f73-136">Disadvantages</span></span>
<span data-ttu-id="93f73-137">团队从私有云移开的一些原因是:</span><span class="sxs-lookup"><span data-stu-id="93f73-137">Some reasons teams move away from the private cloud are:</span></span>

- <span data-ttu-id="93f73-138">您有前期 CapEx 成本, 并且必须购买硬件以供启动和维护</span><span class="sxs-lookup"><span data-stu-id="93f73-138">You have upfront CapEx costs and must purchase the hardware for startup and maintenance</span></span>
- <span data-ttu-id="93f73-139">拥有的设备限制灵活性与规模必须购买、安装和安装新硬件</span><span class="sxs-lookup"><span data-stu-id="93f73-139">Owning the equipment limits the agility - to scale you must buy, install, and setup new hardware</span></span>
- <span data-ttu-id="93f73-140">私有云需要 IT 技能和专业技能, 这很难做到</span><span class="sxs-lookup"><span data-stu-id="93f73-140">Private clouds require IT skills and expertise that's hard to come by</span></span>

<span data-ttu-id="93f73-141">如果组织具有无法加入公共云的数据 (可能出于法律原因), 则私有云的用例方案。</span><span class="sxs-lookup"><span data-stu-id="93f73-141">A use case scenario for a private cloud would be when an organization has data that cannot be put in the public cloud, perhaps for legal reasons.</span></span> <span data-ttu-id="93f73-142">例如, 他们可能具有无法公开公开的医疗数据。</span><span class="sxs-lookup"><span data-stu-id="93f73-142">For example, they may have medical data that cannot be exposed publicly.</span></span> <span data-ttu-id="93f73-143">另一种情况可能是政府策略要求将特定数据保留在国家/地区内, 也可能是秘密的。</span><span class="sxs-lookup"><span data-stu-id="93f73-143">Another scenario may be where government policy requires specific data to be kept in-country or privately.</span></span>

<span data-ttu-id="93f73-144">私有云可以向外部客户提供云功能, 也可以为特定内部部门 (如会计或人力资源) 提供云功能。</span><span class="sxs-lookup"><span data-stu-id="93f73-144">A private cloud can provide cloud functionality to external customers as well, or to specific internal departments such as Accounting or Human Resources.</span></span>

:::row:::
  :::column span="3":::
### <a name="hybrid-cloud"></a><span data-ttu-id="93f73-145">混合云</span><span class="sxs-lookup"><span data-stu-id="93f73-145">Hybrid cloud</span></span>

<span data-ttu-id="93f73-146">混合云将公共和私有云结合在一起, 使您可以在最合适的位置运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="93f73-146">A hybrid cloud combines public and private clouds, allowing you to run your applications in the most appropriate location.</span></span> <span data-ttu-id="93f73-147">例如, 您可以在公共云中托管一个网站, 并将其链接到私有云 (或内部部署数据中心) 中托管的高度安全的数据库。</span><span class="sxs-lookup"><span data-stu-id="93f73-147">For example, you could host a website in the public cloud and link it to a highly secure database hosted in your private cloud (or on-premises datacenter).</span></span>
  :::column-end:::
  :::column:::
![混合云图标](../media/4-hybrid-cloud.png)
  :::column-end:::
:::row-end:::

<span data-ttu-id="93f73-149">如果你有一些无法加入云中的东西, 这很有帮助, 原因可能是法律原因。</span><span class="sxs-lookup"><span data-stu-id="93f73-149">This is helpful when you have some things that cannot be put in the cloud, maybe for legal reasons.</span></span> <span data-ttu-id="93f73-150">例如, 您可能有一些特定的数据部分无法公开 (例如医疗数据), 需要在您的专用数据中心内进行公开。</span><span class="sxs-lookup"><span data-stu-id="93f73-150">For example, you may have some specific pieces of data that cannot be exposed publicly (such as medical data) which needs to be held in your private datacenter.</span></span> <span data-ttu-id="93f73-151">另一个示例是在不能更新的旧硬件上运行的一个或多个应用程序。</span><span class="sxs-lookup"><span data-stu-id="93f73-151">Another example is one or more applications that run on old hardware that can’t be updated.</span></span> <span data-ttu-id="93f73-152">在这种情况下, 您可以让旧系统在本地运行, 并将其连接到公共云以进行授权或存储。</span><span class="sxs-lookup"><span data-stu-id="93f73-152">In this case, you can keep the old system running locally, and connect it to the public cloud for authorization or storage.</span></span>

#### <a name="advantages"></a><span data-ttu-id="93f73-153">在于</span><span class="sxs-lookup"><span data-stu-id="93f73-153">Advantages</span></span>
<span data-ttu-id="93f73-154">混合云与私有云的一些优势如下:</span><span class="sxs-lookup"><span data-stu-id="93f73-154">Some advantages of a hybrid cloud versus a private cloud are:</span></span>

- <span data-ttu-id="93f73-155">您可以保留任何运行和可访问的、使用过时硬件或过期操作系统的系统</span><span class="sxs-lookup"><span data-stu-id="93f73-155">You can keep any systems running and accessible that use out-of-date hardware or an out-of-date operating system</span></span>
- <span data-ttu-id="93f73-156">您可以在本地运行的与在云中运行的内容具有灵活性</span><span class="sxs-lookup"><span data-stu-id="93f73-156">You have flexibility with what you run locally versus in the cloud</span></span>
- <span data-ttu-id="93f73-157">您可以利用来自公共云提供商的服务和资源, 使其价格更便宜, 并在不存在的情况下补充自己的设备</span><span class="sxs-lookup"><span data-stu-id="93f73-157">You can take advantage of economies of scale from public cloud providers for services and resources where it's cheaper, and then supplement with your own equipment when it's not</span></span>
- <span data-ttu-id="93f73-158">您可以使用自己的设备来满足需要完全控制环境的安全性、合规性或旧方案</span><span class="sxs-lookup"><span data-stu-id="93f73-158">You can use your own equipment to meet security, compliance, or legacy scenarios where you need to completely control the environment</span></span>

#### <a name="disadvantages"></a><span data-ttu-id="93f73-159">在于</span><span class="sxs-lookup"><span data-stu-id="93f73-159">Disadvantages</span></span>
<span data-ttu-id="93f73-160">需要注意的问题包括:</span><span class="sxs-lookup"><span data-stu-id="93f73-160">Some concerns you'll need to watch out for are:</span></span>

- <span data-ttu-id="93f73-161">它比选择一个部署模型成本更高, 因为它涉及一些 CapEx 的提前成本</span><span class="sxs-lookup"><span data-stu-id="93f73-161">It can be more expensive than selecting one deployment model since it involves some CapEx cost up front</span></span>
- <span data-ttu-id="93f73-162">设置和管理可能更复杂</span><span class="sxs-lookup"><span data-stu-id="93f73-162">It can be more complicated to set up and manage</span></span>

## <a name="summary"></a><span data-ttu-id="93f73-163">摘要</span><span class="sxs-lookup"><span data-stu-id="93f73-163">Summary</span></span>

<span data-ttu-id="93f73-164">云计算是灵活的, 使您能够选择部署它的方式。</span><span class="sxs-lookup"><span data-stu-id="93f73-164">Cloud computing is flexible and gives you the ability to choose how you want to deploy it.</span></span> <span data-ttu-id="93f73-165">你选择的云部署模型取决于你的预算以及你的安全、可伸缩性和维护需求。</span><span class="sxs-lookup"><span data-stu-id="93f73-165">The cloud deployment model you choose depends on your budget, and on your security, scalability, and maintenance needs.</span></span>
