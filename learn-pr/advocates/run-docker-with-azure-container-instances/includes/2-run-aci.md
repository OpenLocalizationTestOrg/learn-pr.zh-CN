<span data-ttu-id="2c3df-101">在这里, 你将在 Azure 中创建容器, 并使用完全限定的域名 (FQDN) 将其公开到 Internet。</span><span class="sxs-lookup"><span data-stu-id="2c3df-101">Here, you create a container in Azure and expose it to the Internet with a fully qualified domain name (FQDN).</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="why-use-azure-container-instances"></a><span data-ttu-id="2c3df-102">为什么要使用 Azure 容器实例？</span><span class="sxs-lookup"><span data-stu-id="2c3df-102">Why use Azure Container Instances?</span></span>

<span data-ttu-id="2c3df-103">Azure 容器实例适用于可在独立容器中运行的方案, 包括简单的应用程序、任务自动化和生成作业。</span><span class="sxs-lookup"><span data-stu-id="2c3df-103">Azure Container Instances is useful for scenarios that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="2c3df-104">以下是一些优点:</span><span class="sxs-lookup"><span data-stu-id="2c3df-104">Here are some of the benefits:</span></span>

- <span data-ttu-id="2c3df-105">**快速启动**: 以秒为单位启动容器。</span><span class="sxs-lookup"><span data-stu-id="2c3df-105">**Fast startup**: Launch containers in seconds.</span></span>
- <span data-ttu-id="2c3df-106">**每秒记帐**: 只有在运行容器时才会产生成本。</span><span class="sxs-lookup"><span data-stu-id="2c3df-106">**Per second billing**: Incur costs only while the container is running.</span></span>
- <span data-ttu-id="2c3df-107">**管理程序级安全性**: 将应用程序完全隔离为虚拟机中的。</span><span class="sxs-lookup"><span data-stu-id="2c3df-107">**Hypervisor-level security**: Isolate your application as completely as it would be in a VM.</span></span>
- <span data-ttu-id="2c3df-108">**自定义大小**: 指定 CPU 内核和内存的确切值。</span><span class="sxs-lookup"><span data-stu-id="2c3df-108">**Custom sizes**: Specify exact values for CPU cores and memory.</span></span>
- <span data-ttu-id="2c3df-109">**永久性存储**: 将 Azure 文件共享直接装载到容器以检索和保留状态。</span><span class="sxs-lookup"><span data-stu-id="2c3df-109">**Persistent storage**: Mount Azure Files shares directly to a container to retrieve and persist state.</span></span>
- <span data-ttu-id="2c3df-110">**Linux 和 Windows**: 使用相同的 API 计划 Windows 和 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="2c3df-110">**Linux and Windows**: Schedule both Windows and Linux containers using the same API.</span></span>

<span data-ttu-id="2c3df-111">对于需要完整容器业务流程的方案 (包括跨多个容器的服务发现、自动扩展和协调应用程序升级), 我们建议采用 Azure Kubernetes service (AKS)。</span><span class="sxs-lookup"><span data-stu-id="2c3df-111">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend Azure Kubernetes Service (AKS).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="2c3df-112">创建容器</span><span class="sxs-lookup"><span data-stu-id="2c3df-112">Create a container</span></span>

<span data-ttu-id="2c3df-113">您可以通过向`az container create`命令提供名称、Docker 图像和 Azure 资源组来创建容器。</span><span class="sxs-lookup"><span data-stu-id="2c3df-113">You create a container by providing a name, a Docker image, and an Azure resource group to the `az container create` command.</span></span> <span data-ttu-id="2c3df-114">您可以选择通过指定 DNS 名称标签将容器公开到 Internet。</span><span class="sxs-lookup"><span data-stu-id="2c3df-114">You can optionally expose the container to the Internet by specifying a DNS name label.</span></span> <span data-ttu-id="2c3df-115">在此示例中, 部署一个承载小型 web 应用程序的容器。</span><span class="sxs-lookup"><span data-stu-id="2c3df-115">In this example, you deploy a container that hosts a small web app.</span></span> <span data-ttu-id="2c3df-116">您还可以选择要放置图像的位置-你将使用**美国东部**地区, 但你可以从以下列表中将其更改为距你更近的位置。</span><span class="sxs-lookup"><span data-stu-id="2c3df-116">You can also select the location to place the image - you'll use the **East US** region, but you can change it to a location close to you from the following list.</span></span>

<!-- TODO: fix region list so it's not hardcoded here -->
<span data-ttu-id="2c3df-117">免费的沙盒允许您在 Azure 全局区域的子集内创建资源。</span><span class="sxs-lookup"><span data-stu-id="2c3df-117">The free sandbox allows you to create resources in a subset of Azure's global regions.</span></span> <span data-ttu-id="2c3df-118">创建任何资源时, 请从以下列表中选择一个区域:</span><span class="sxs-lookup"><span data-stu-id="2c3df-118">Select a region from the following list when creating any resources:</span></span>

:::row:::
    :::column:::
        - <span data-ttu-id="2c3df-119">westus2</span><span class="sxs-lookup"><span data-stu-id="2c3df-119">westus2</span></span>
        - <span data-ttu-id="2c3df-120">southcentralus</span><span class="sxs-lookup"><span data-stu-id="2c3df-120">southcentralus</span></span>
        - <span data-ttu-id="2c3df-121">centralus</span><span class="sxs-lookup"><span data-stu-id="2c3df-121">centralus</span></span>
        - <span data-ttu-id="2c3df-122">eastus</span><span class="sxs-lookup"><span data-stu-id="2c3df-122">eastus</span></span>
        - <span data-ttu-id="2c3df-123">westeurope</span><span class="sxs-lookup"><span data-stu-id="2c3df-123">westeurope</span></span>
        - <span data-ttu-id="2c3df-124">southeastasia</span><span class="sxs-lookup"><span data-stu-id="2c3df-124">southeastasia</span></span>
        - <span data-ttu-id="2c3df-125">centralindia</span><span class="sxs-lookup"><span data-stu-id="2c3df-125">centralindia</span></span>
    :::column-end:::
:::row-end:::

1. <span data-ttu-id="2c3df-126">提供一个 DNS 名称以将容器公开到 Internet。</span><span class="sxs-lookup"><span data-stu-id="2c3df-126">You provide a DNS name to expose your container to the Internet.</span></span> <span data-ttu-id="2c3df-127">您的 DNS 名称必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2c3df-127">Your DNS name must be unique.</span></span> <span data-ttu-id="2c3df-128">若要了解学习目的, 请从云命令行管理程序中运行此命令, 以创建保存唯一名称的 Bash 变量。</span><span class="sxs-lookup"><span data-stu-id="2c3df-128">For learning purposes, run this command from Cloud Shell to create a Bash variable that holds a unique name.</span></span>

    ```bash
    DNS_NAME_LABEL=aci-demo-$RANDOM
    ```

1. <span data-ttu-id="2c3df-129">运行以下`az container create`命令以启动容器实例。</span><span class="sxs-lookup"><span data-stu-id="2c3df-129">Run the following `az container create` command to start a container instance.</span></span>

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --image microsoft/aci-helloworld \
      --ports 80 \
      --dns-name-label $DNS_NAME_LABEL \
      --location eastus
    ```

    <span data-ttu-id="2c3df-130">`$DNS_NAME_LABEL`指定您的 DNS 名称。</span><span class="sxs-lookup"><span data-stu-id="2c3df-130">`$DNS_NAME_LABEL` specifies your DNS name.</span></span> <span data-ttu-id="2c3df-131">image name、 **microsoft/aci-helloworld**指的是承载在可运行基本 node.js web 应用程序的 docker 中心上的 docker 图像。</span><span class="sxs-lookup"><span data-stu-id="2c3df-131">The image name, **microsoft/aci-helloworld**, refers to a Docker image hosted on Docker Hub that runs a basic Node.js web application.</span></span>

1. <span data-ttu-id="2c3df-132">`az container create`命令完成后, 运行`az container show`以检查其状态。</span><span class="sxs-lookup"><span data-stu-id="2c3df-132">When the `az container create` command completes, run `az container show` to check its status.</span></span>

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
      --out table
    ```

    <span data-ttu-id="2c3df-133">你将看到容器的完全限定域名 (FQDN) 及其预配状态。</span><span class="sxs-lookup"><span data-stu-id="2c3df-133">You see your container's fully qualified domain name (FQDN) and its provisioning state.</span></span> <span data-ttu-id="2c3df-134">下面是一个示例。</span><span class="sxs-lookup"><span data-stu-id="2c3df-134">Here's an example.</span></span>

    ```output
    FQDN                                    ProvisioningState
    --------------------------------------  -------------------
    aci-demo.eastus.azurecontainer.io       Succeeded
    ````

    <span data-ttu-id="2c3df-135">如果你的容器处于 "**正在创建**" 状态, 请稍等几分钟, 然后再次运行该命令, 直到你看到 "**成功**" 状态。</span><span class="sxs-lookup"><span data-stu-id="2c3df-135">If your container is in the **Creating** state, wait a few moments and run the command again until you see the **Succeeded** state.</span></span>

1. <span data-ttu-id="2c3df-136">在浏览器中, 导航到容器的 FQDN 以查看它是否正在运行。</span><span class="sxs-lookup"><span data-stu-id="2c3df-136">From a browser, navigate to your container's FQDN to see it running.</span></span> <span data-ttu-id="2c3df-137">你会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="2c3df-137">You see this.</span></span>

    ![在浏览器中运行的示例 node.js 容器应用程序](../media/2-browser.png)

## <a name="summary"></a><span data-ttu-id="2c3df-139">摘要</span><span class="sxs-lookup"><span data-stu-id="2c3df-139">Summary</span></span>

<span data-ttu-id="2c3df-140">在这里, 您创建了一个 Azure 容器实例来运行 web 服务器和应用程序。</span><span class="sxs-lookup"><span data-stu-id="2c3df-140">Here, you created an Azure container instance to run a web server and application.</span></span> <span data-ttu-id="2c3df-141">你也可以使用容器实例的 FQDN 访问此应用程序。</span><span class="sxs-lookup"><span data-stu-id="2c3df-141">You also accessed this application using the FQDN of the container instance.</span></span>