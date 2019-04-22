<span data-ttu-id="7c13c-101">请记住将应用程序从本地迁移到 Azure 的方案。</span><span class="sxs-lookup"><span data-stu-id="7c13c-101">Remember our scenario of migrating an application from on-premises to Azure.</span></span> <span data-ttu-id="7c13c-102">此体系结构可能类似于什么？</span><span class="sxs-lookup"><span data-stu-id="7c13c-102">What might this architecture look like?</span></span> <span data-ttu-id="7c13c-103">您的组织有一个不重要的应用程序, 这是一个不错的候选人试用。它是一种编写的应用程序, 用于解决在挑选午餐时遇到的常见问题。</span><span class="sxs-lookup"><span data-stu-id="7c13c-103">Your organization has a non-critical application that is a good candidate try out. It's an application written to solve the all-too-common problem of picking what's for lunch.</span></span>

<span data-ttu-id="7c13c-104">试想一下, 一组朋友或同事最后一次进入午餐。</span><span class="sxs-lookup"><span data-stu-id="7c13c-104">Think of the last time you went out to lunch with a group of friends or colleagues.</span></span> <span data-ttu-id="7c13c-105">你是否发现很容易做出决定, 或者你是否需要花费大量时间来尝试了解每个人在说 "我喜欢所有内容" 时的真正意义？</span><span class="sxs-lookup"><span data-stu-id="7c13c-105">Did you find it easy to make a decision or did you spend a lot of time trying to figure out what everyone really meant when they said "I like everything"?</span></span> <span data-ttu-id="7c13c-106">让我们根据可帮助您解决此问题的三层体系结构来部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c13c-106">Let's deploy an application based on a three-tier architecture that might help you solve this problem.</span></span> <span data-ttu-id="7c13c-107">此应用程序允许你提供午餐建议, 每个人都可以对其首选选择进行投票。</span><span class="sxs-lookup"><span data-stu-id="7c13c-107">This application that lets you make lunch suggestions and everyone can vote for their preferred choice.</span></span>

<span data-ttu-id="7c13c-108">我们为此应用程序创建了一个模板, 该模板将每个层部署为 Azure 资源, 然后部署实际代码。</span><span class="sxs-lookup"><span data-stu-id="7c13c-108">We've created a template for this application that deploys each tier as Azure resources, then deploys the actual code.</span></span> <span data-ttu-id="7c13c-109">这是在 Linux 服务器上部署的 ASP.NET 核心 MVC 应用程序, 但无论底层操作系统平台或 SDK 如何, 都可以使用此体系结构样式。</span><span class="sxs-lookup"><span data-stu-id="7c13c-109">This is an ASP.NET Core MVC application deployed on Linux servers, but this architectural style can be used regardless of the underlying OS platforms or SDK.</span></span>

<span data-ttu-id="7c13c-110">下面是对使用此模板部署的内容的高级别可视化。</span><span class="sxs-lookup"><span data-stu-id="7c13c-110">Here's a high-level visualization of what is deployed with this template.</span></span>

![要在此单位中部署的 N 层体系结构的可视化效果](../media/3-n-tier-simple.svg)

## <a name="deploy-an-n-tier-architecture"></a><span data-ttu-id="7c13c-112">部署 N 层体系结构</span><span class="sxs-lookup"><span data-stu-id="7c13c-112">Deploy an N-tier architecture</span></span>

1. <span data-ttu-id="7c13c-113">运行以下命令以启动部署。</span><span class="sxs-lookup"><span data-stu-id="7c13c-113">Run the following command to start the deployment.</span></span> <span data-ttu-id="7c13c-114">该`az group deployment create`命令将使用所指定的模板文件和参数将部署启动到沙盒资源组中。</span><span class="sxs-lookup"><span data-stu-id="7c13c-114">The `az group deployment create` command starts a deployment into our sandbox resource group using the template file and parameters we specify.</span></span> <span data-ttu-id="7c13c-115">此外, 还可以指定从`head /dev/urandom | tr -dc A-Za-z0-9 | head -c 32`命令生成的随机32字符字符串作为 password 参数。</span><span class="sxs-lookup"><span data-stu-id="7c13c-115">We also specify a random 32 character string generated from the `head /dev/urandom | tr -dc A-Za-z0-9 | head -c 32` command as the password parameter.</span></span>

    <span data-ttu-id="7c13c-116">完成部署大约需要5分钟。</span><span class="sxs-lookup"><span data-stu-id="7c13c-116">The deployment takes approximately 5 minutes to complete.</span></span>

    ```azurecli
    az group deployment create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --template-uri  https://raw.githubusercontent.com/MicrosoftDocs/mslearn-n-tier-architecture/master/Deployment/azuredeploy.json \
      --parameters password="$(head /dev/urandom | tr -dc A-Za-z0-9 | head -c 32)"
    ```

## <a name="view-deployed-resources-and-test-the-application"></a><span data-ttu-id="7c13c-117">查看已部署的资源并测试应用程序</span><span class="sxs-lookup"><span data-stu-id="7c13c-117">View deployed resources and test the application</span></span>

<span data-ttu-id="7c13c-118">部署完成后, 测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c13c-118">Once the deployment has completed, test the application.</span></span> <span data-ttu-id="7c13c-119">运行以下命令, 该命令将返回应用程序的 URL。</span><span class="sxs-lookup"><span data-stu-id="7c13c-119">Run the following command, which will return the URL for the app.</span></span>

```azurecli
az group deployment show \
  --output table \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name azuredeploy \
  --query properties.outputs.webSiteUrl
```

<span data-ttu-id="7c13c-120">打开 web 浏览器并访问网站。</span><span class="sxs-lookup"><span data-stu-id="7c13c-120">Open a web browser and visit the site.</span></span> <span data-ttu-id="7c13c-121">您会看到一个框, 可在其中添加食物选项。</span><span class="sxs-lookup"><span data-stu-id="7c13c-121">You see a box where you can add food choices.</span></span> <span data-ttu-id="7c13c-122">添加选项后, 单击它即可添加投票。</span><span class="sxs-lookup"><span data-stu-id="7c13c-122">Once an option is added, clicking it adds a vote.</span></span>

![示例投票应用程序的屏幕截图](../media/3-lunch.png)

## <a name="three-tiers-of-whats-for-lunch"></a><span data-ttu-id="7c13c-124">三层 "午餐的用途是什么？"</span><span class="sxs-lookup"><span data-stu-id="7c13c-124">Three tiers of "What's For Lunch?"</span></span>

<span data-ttu-id="7c13c-125">此应用程序以其复杂性为单位特意精简。</span><span class="sxs-lookup"><span data-stu-id="7c13c-125">This application is intentionally minimal in its complexity.</span></span> <span data-ttu-id="7c13c-126">它是一个有趣的应用程序, 但仍说明了三层体系结构。</span><span class="sxs-lookup"><span data-stu-id="7c13c-126">It's a fun application, but still demonstrates a three-tier architecture.</span></span> <span data-ttu-id="7c13c-127">该模板创建两台虚拟机 (vm)、Azure SQL 数据库以及支持这些资源所需的资源, 如磁盘、nic 和虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="7c13c-127">The template creates two Virtual Machines (VMs), an Azure SQL database, and the resources needed to support these resources, such as disks, NICs, and virtual networks.</span></span> <span data-ttu-id="7c13c-128">它还部署代码以在每个层上运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c13c-128">It also deploys the code to run the application on each tier.</span></span> <span data-ttu-id="7c13c-129">我们部署的虚拟网络具有两个子网, 一个用于表示层, 一个用于应用层, 为每个层提供一个安全边界。</span><span class="sxs-lookup"><span data-stu-id="7c13c-129">The virtual network we've deployed has two subnets, one for the presentation tier and one for the application tier, providing a security boundary for each tier.</span></span> 

<span data-ttu-id="7c13c-130">我们还将标记作为部署的一部分应用于资源, 以反映该资源支持的层 (`tier:presentation`、 `tier:application`、 `tier:data`)。</span><span class="sxs-lookup"><span data-stu-id="7c13c-130">We also applied tags to the resources as part of the deployment to reflect the tier the resource is supporting (`tier:presentation`, `tier:application`, `tier:data`).</span></span> <span data-ttu-id="7c13c-131">标记是一种将元数据应用于 Azure 资源的方法, 在这种情况下, 我们可以轻松筛选每个层的资源。</span><span class="sxs-lookup"><span data-stu-id="7c13c-131">Tags are a method of applying metadata to Azure resources, and in this case they allow us to easily filter the resources for each tier.</span></span>

<span data-ttu-id="7c13c-132">让我们深入了解一下每一层。</span><span class="sxs-lookup"><span data-stu-id="7c13c-132">Let's look closer at each tier.</span></span> <span data-ttu-id="7c13c-133">下面是我们刚刚部署的资源的详细可视化。</span><span class="sxs-lookup"><span data-stu-id="7c13c-133">Here's a detailed visualization of the resources we just deployed.</span></span>

![要在此单位中部署的 N 层体系结构的可视化效果](../media/3-n-tier-deployment.svg)

### <a name="presentation-tier"></a><span data-ttu-id="7c13c-135">表示层</span><span class="sxs-lookup"><span data-stu-id="7c13c-135">Presentation tier</span></span>

<span data-ttu-id="7c13c-136">运行以下命令以列出表示层资源。</span><span class="sxs-lookup"><span data-stu-id="7c13c-136">Run the following command to list out the presentation tier resources.</span></span>

```azurecli
az resource list --tag tier=presentation --output table
```

<span data-ttu-id="7c13c-137">在我们引用的三层体系结构中, 这表示的是表示层。</span><span class="sxs-lookup"><span data-stu-id="7c13c-137">In the three-tier architecture we've been referencing, this represents the presentation tier.</span></span> <span data-ttu-id="7c13c-138">负责 web 界面的代码已部署在此层上, 它提供 UI 并直接处理用户请求。</span><span class="sxs-lookup"><span data-stu-id="7c13c-138">The code responsible for the web interface was deployed on this tier, it presents the UI and directly handles user requests.</span></span> <span data-ttu-id="7c13c-139">此层仅与用户的网站的演示文稿相关。</span><span class="sxs-lookup"><span data-stu-id="7c13c-139">This tier is only concerned with the presentation of the web site to the user.</span></span> <span data-ttu-id="7c13c-140">它不具有对数据的直接访问权限, 并且不包含业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="7c13c-140">It doesn't have direct access to the data, and doesn't include business logic.</span></span>

<span data-ttu-id="7c13c-141">我们部署了一个名为 " **demo-web 虚拟机**" 的 web 服务器, 该服务器运行的是正在访问的网站。</span><span class="sxs-lookup"><span data-stu-id="7c13c-141">We've deployed a web server called **demo-web-vm** that is running the web site we're accessing.</span></span> <span data-ttu-id="7c13c-142">服务器具有一个带有公用 IP 地址的网络接口, 即 " **demo**-web-vm-nic **-pip**", 这是我们之前检索到的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="7c13c-142">The server has a network interface, **demo-web-vm-nic**, that has a public IP address, **demo-web-vm-nic-pip**, associated with it, that being the IP address we retrieved earlier.</span></span> <span data-ttu-id="7c13c-143">它还有一个网络安全组**演示-nsg**, 仅允许从 internet 入站端口 80 (HTTP) 流量。</span><span class="sxs-lookup"><span data-stu-id="7c13c-143">It also has a network security group **demo-web-nsg**, that allows only port 80 (HTTP) traffic inbound from the internet.</span></span> <span data-ttu-id="7c13c-144">这将限制仅对网站的访问权限, 并阻止通过恶意使用的不必要的端口进行访问。</span><span class="sxs-lookup"><span data-stu-id="7c13c-144">This restricts access to only the web site, and prevents access via unnecessary ports that could be used maliciously.</span></span> <span data-ttu-id="7c13c-145">此层通过 HTTP 与表示层通信, 以满足对用户的请求。</span><span class="sxs-lookup"><span data-stu-id="7c13c-145">This tier communicates with the presentation tier over HTTP to fulfill the request for the user.</span></span>

### <a name="application-tier"></a><span data-ttu-id="7c13c-146">应用层</span><span class="sxs-lookup"><span data-stu-id="7c13c-146">Application tier</span></span>

<span data-ttu-id="7c13c-147">运行以下命令以列出应用层资源。</span><span class="sxs-lookup"><span data-stu-id="7c13c-147">Run the following command to list the application tier resources.</span></span>

```azurecli
az resource list --tag tier=application --output table
```

<span data-ttu-id="7c13c-148">应用程序层已部署在一个名为 **.biz-vm**的虚拟机上, 该虚拟机正在运行业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="7c13c-148">The application tier has been deployed on a virtual machine called **demo-biz-vm** that is running the business logic.</span></span> <span data-ttu-id="7c13c-149">它还具有网络接口 .biz- **nic**, 但此网络接口仅具有专用 IP 地址, 而不提供到服务器的直接入站连接的任何机制。</span><span class="sxs-lookup"><span data-stu-id="7c13c-149">It also has a network interface, **demo-biz-vm-nic**, but this network interface only has a private IP address, providing no mechanism for direct inbound connectivity to the server.</span></span> <span data-ttu-id="7c13c-150">它还具有网络安全组 **.biz-nsg**, 仅允许从表示层的子网访问。</span><span class="sxs-lookup"><span data-stu-id="7c13c-150">It also has a network security group, **demo-biz-nsg**, that only allows access from the subnet of the presentation tier.</span></span>

<span data-ttu-id="7c13c-151">该层是应用程序访问数据的管道。</span><span class="sxs-lookup"><span data-stu-id="7c13c-151">This tier is the conduit for the application to access the data.</span></span> <span data-ttu-id="7c13c-152">公开在此服务器上部署表示层调用的 API 的代码。</span><span class="sxs-lookup"><span data-stu-id="7c13c-152">The code that exposes the API that the presentation tier calls is deployed on this server.</span></span> <span data-ttu-id="7c13c-153">此处不存储任何数据, 用户无法直接访问此服务器。</span><span class="sxs-lookup"><span data-stu-id="7c13c-153">No data is stored here, and users are not able to access this server directly.</span></span> <span data-ttu-id="7c13c-154">若要访问数据并满足用户请求, 此层通过 t-sql 命令与数据层进行通信。</span><span class="sxs-lookup"><span data-stu-id="7c13c-154">To access data and fulfill user requests, this tier communicates with the data tier through T-SQL commands.</span></span>

<span data-ttu-id="7c13c-155">在此层的应用程序中, 有一个简单的业务逻辑示例。</span><span class="sxs-lookup"><span data-stu-id="7c13c-155">There is a simple example of business logic incorporated in the application at this tier.</span></span> <span data-ttu-id="7c13c-156">有对午餐建议的服务器端验证, 将它们与可接受的值列表进行比较。</span><span class="sxs-lookup"><span data-stu-id="7c13c-156">There is server-side validation of the lunch suggestions, comparing them to a list of acceptable values.</span></span> <span data-ttu-id="7c13c-157">如果您尝试在此列表中添加未包含的内容, 则不会接受该列表, 并将使用有效的午餐选项返回一条消息。</span><span class="sxs-lookup"><span data-stu-id="7c13c-157">If you try to add something that isn't on this list, it's not accepted, and a message is returned with the valid lunch options.</span></span>

### <a name="data-tier"></a><span data-ttu-id="7c13c-158">数据层</span><span class="sxs-lookup"><span data-stu-id="7c13c-158">Data tier</span></span>

<span data-ttu-id="7c13c-159">运行以下命令以列出数据层资源。</span><span class="sxs-lookup"><span data-stu-id="7c13c-159">Run the following command to list out the data tier resources.</span></span>

```azurecli
az resource list --tag tier=data --output table
```

<span data-ttu-id="7c13c-160">数据层是一个 Azure SQL 数据库服务器, **dbserver-abc123** (我们为全局唯一性的服务器名称添加一个随机字符串)。</span><span class="sxs-lookup"><span data-stu-id="7c13c-160">The data tier is an Azure SQL Database server, **demo-dbserver-abc123** (we add a random string to the server name for global uniqueness).</span></span> <span data-ttu-id="7c13c-161">此服务器将应用程序的数据存储在名为**demo-sqldb**的数据库中。</span><span class="sxs-lookup"><span data-stu-id="7c13c-161">This server stores the data for the application in a database called **demo-sqldb**.</span></span> <span data-ttu-id="7c13c-162">此应用程序层仅关注数据存储, 并提供访问它的方法, 在此示例中, 应用程序对数据库执行 t-sql。</span><span class="sxs-lookup"><span data-stu-id="7c13c-162">This tier of the application is solely concerned with the storage of data, and providing a method to access it, in this case through T-SQL the application executes against the database.</span></span> <span data-ttu-id="7c13c-163">我们不会在此层处理任何业务逻辑, 也不会对用户进行任何数据呈现。</span><span class="sxs-lookup"><span data-stu-id="7c13c-163">We're not handling any business logic at this tier, nor are we doing any presentation of data back to the user.</span></span>

<span data-ttu-id="7c13c-164">此层通过 VNet 服务终结点公开端口1433之间的连接。</span><span class="sxs-lookup"><span data-stu-id="7c13c-164">This tier exposes connectivity over port 1433 through a VNet service endpoint.</span></span> <span data-ttu-id="7c13c-165">VNet 服务终结点是一种将 PaaS 服务 (如 Azure SQL Database) 连接到子网并限制仅连接到该子网中的资源的机制。</span><span class="sxs-lookup"><span data-stu-id="7c13c-165">VNet service endpoints are a mechanism to connect PaaS services (such as Azure SQL Database) to a subnet and restrict connectivity to only the resources within that subnet.</span></span>

<span data-ttu-id="7c13c-166">这也是使用 Platform as 服务 (PaaS) 服务取代基础结构作为服务 (IaaS) 虚拟机以运行应用程序层的示例。</span><span class="sxs-lookup"><span data-stu-id="7c13c-166">This is also an example of using Platform as a Service (PaaS) services in place of Infrastructure as a Service (IaaS) virtual machines to run a tier of an application.</span></span> <span data-ttu-id="7c13c-167">N 层应用程序通常被认为是基于 VM 的应用程序, 但这并不是必需的。</span><span class="sxs-lookup"><span data-stu-id="7c13c-167">N-tier applications are often thought of as VM-based applications, but that is not a requirement.</span></span> <span data-ttu-id="7c13c-168">通过使用 PaaS 服务取代虚拟机, 您将降低成本、提高安全性并降低管理要求。</span><span class="sxs-lookup"><span data-stu-id="7c13c-168">By using PaaS services in place of VMs, you will lower your costs, increase security, and reduce administration requirements.</span></span>