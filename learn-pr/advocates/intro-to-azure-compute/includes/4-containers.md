:::row:::
  :::column:::
    ![表示 Azure 容器的图像](../media/4-azure-containers.png)
  :::column-end:::
  :::column span="3":::
<span data-ttu-id="c1346-102">如果要在单个虚拟机上运行应用程序的多个实例, 则容器是极好的选择。</span><span class="sxs-lookup"><span data-stu-id="c1346-102">If you wish to run multiple instances of an application on a single virtual machine, containers are an excellent choice.</span></span> <span data-ttu-id="c1346-103">容器 orchestrator 可以根据需要启动、停止和扩展应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="c1346-103">The container orchestrator can start, stop, and scale out application instances as needed.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="c1346-104">容器旨在进行轻型、创建、横向扩展和停止。</span><span class="sxs-lookup"><span data-stu-id="c1346-104">Containers are meant to be lightweight, created, scaled out, and stopped dynamically.</span></span> <span data-ttu-id="c1346-105">此设计允许您快速响应需求或失败的变化。</span><span class="sxs-lookup"><span data-stu-id="c1346-105">This design allows you to respond quickly to changes in demand or failure.</span></span>

<span data-ttu-id="c1346-106">容器的另一个优势是, 您可以在单个 VM 主机上运行多个独立的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c1346-106">Another benefit of containers is you can run multiple isolated applications on a single VM host.</span></span> <span data-ttu-id="c1346-107">由于容器受保护和隔离, 因此不需要每个应用程序都具有单独的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c1346-107">Since containers are secured and isolated, you don't need separate VMs for each app.</span></span>

#### <a name="vms-versus-containers"></a><span data-ttu-id="c1346-108">vm 与容器</span><span class="sxs-lookup"><span data-stu-id="c1346-108">VMs versus containers</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuaq]

## <a name="containers-in-azure"></a><span data-ttu-id="c1346-109">Azure 中的容器</span><span class="sxs-lookup"><span data-stu-id="c1346-109">Containers in Azure</span></span>

<span data-ttu-id="c1346-110">azure 支持 Docker 容器, 可以通过多种方式管理 azure 中的容器。</span><span class="sxs-lookup"><span data-stu-id="c1346-110">Azure supports Docker containers, and there are several ways to manage containers in Azure.</span></span>

- <span data-ttu-id="c1346-111">Azure 容器实例 (ACI)</span><span class="sxs-lookup"><span data-stu-id="c1346-111">Azure Container Instances (ACI)</span></span>
- <span data-ttu-id="c1346-112">Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="c1346-112">Azure Kubernetes Service (AKS)</span></span>

### <a name="azure-container-instances"></a><span data-ttu-id="c1346-113">Azure 容器实例</span><span class="sxs-lookup"><span data-stu-id="c1346-113">Azure Container Instances</span></span>

<span data-ttu-id="c1346-114">azure 容器实例 (ACI) 提供了在 Azure 中运行容器的速度最快且最简单的方法。</span><span class="sxs-lookup"><span data-stu-id="c1346-114">Azure Container Instances (ACI) offers the fastest and simplest way to run a container in Azure.</span></span> <span data-ttu-id="c1346-115">您无需管理任何虚拟机或配置任何其他服务。</span><span class="sxs-lookup"><span data-stu-id="c1346-115">You don't have to manage any virtual machines or configure any additional services.</span></span> <span data-ttu-id="c1346-116">它是一个 PaaS 产品, 允许您上载并直接执行容器。</span><span class="sxs-lookup"><span data-stu-id="c1346-116">It is a PaaS offering that allows you to upload your containers and execute them directly.</span></span> 

### <a name="azure-kubernetes-service"></a><span data-ttu-id="c1346-117">Azure Kubernetes 服务</span><span class="sxs-lookup"><span data-stu-id="c1346-117">Azure Kubernetes Service</span></span>

<span data-ttu-id="c1346-118">自动执行和管理大量容器以及与大量容器交互的任务称为 "业务流程"。</span><span class="sxs-lookup"><span data-stu-id="c1346-118">The task of automating and managing and interacting with a large number of containers is known as orchestration.</span></span> <span data-ttu-id="c1346-119">对于具有多个容器的分布式体系结构的容器, Azure Kubernetes Service (AKS) 是一个完整的业务流程服务。</span><span class="sxs-lookup"><span data-stu-id="c1346-119">Azure Kubernetes Service (AKS) is a complete orchestration service for containers with distributed architectures with multiple containers.</span></span> 

#### <a name="what-is-kubernetes"></a><span data-ttu-id="c1346-120">什么是 Kubernetes？</span><span class="sxs-lookup"><span data-stu-id="c1346-120">What is Kubernetes?</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuX]

### <a name="using-containers-in-your-solutions"></a><span data-ttu-id="c1346-121">在解决方案中使用容器</span><span class="sxs-lookup"><span data-stu-id="c1346-121">Using containers in your solutions</span></span>

<span data-ttu-id="c1346-122">容器通常用于创建使用_microservice 体系结构_的解决方案。</span><span class="sxs-lookup"><span data-stu-id="c1346-122">Containers are often used to create solutions using a _microservice architecture_.</span></span> <span data-ttu-id="c1346-123">这是将解决方案分解为较小的独立部分的位置。</span><span class="sxs-lookup"><span data-stu-id="c1346-123">This is where you break solutions into smaller, independent pieces.</span></span> <span data-ttu-id="c1346-124">例如, 您可以将网站拆分为承载前端的容器、另一个托管的后端和第三个存储。</span><span class="sxs-lookup"><span data-stu-id="c1346-124">For example, you may split a website into a container hosting your front end, another hosting your back end, and a third for storage.</span></span> <span data-ttu-id="c1346-125">这使您可以将应用程序的各个部分分隔成可独立进行维护、扩展或更新的逻辑部分。</span><span class="sxs-lookup"><span data-stu-id="c1346-125">This allows you to separate portions of your app into logical sections that can be maintained, scaled, or updated independently.</span></span>

#### <a name="what-is-a-microservice"></a><span data-ttu-id="c1346-126">什么是 microservice？</span><span class="sxs-lookup"><span data-stu-id="c1346-126">What is a microservice?</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yual]

<span data-ttu-id="c1346-127">设想你的网站后端已达到容量, 但前端和存储不会产生压力。</span><span class="sxs-lookup"><span data-stu-id="c1346-127">Imagine your website backend has reached capacity but the front end and storage aren't being stressed.</span></span> <span data-ttu-id="c1346-128">您可以单独扩展后端以提高性能, 也可以决定使用不同的存储服务。</span><span class="sxs-lookup"><span data-stu-id="c1346-128">You could scale the back end separately to improve performance, or you could decide to use a different storage service.</span></span> <span data-ttu-id="c1346-129">或者, 甚至可以替换存储容器, 而不会影响应用程序的其余部分。</span><span class="sxs-lookup"><span data-stu-id="c1346-129">Or you could even replace the storage container without affecting the rest of the application.</span></span>