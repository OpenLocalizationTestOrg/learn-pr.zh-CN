<span data-ttu-id="96794-101">如果你已使用 azure 一段时间, 你可能听说过 azure 资源管理器。</span><span class="sxs-lookup"><span data-stu-id="96794-101">If you've been using Azure for a while, you've likely heard about Azure Resource Manager.</span></span> <span data-ttu-id="96794-102">让我们查看资源管理器的角色并定义构成资源管理器模板的内容。</span><span class="sxs-lookup"><span data-stu-id="96794-102">Let's review Resource Manager's role and define what makes up a Resource Manager template.</span></span>

## <a name="whats-azure-resource-manager"></a><span data-ttu-id="96794-103">什么是 Azure 资源管理器？</span><span class="sxs-lookup"><span data-stu-id="96794-103">What's Azure Resource Manager?</span></span>

<span data-ttu-id="96794-104">Azure 资源管理器是用于管理和组织云资源的接口。</span><span class="sxs-lookup"><span data-stu-id="96794-104">Azure Resource Manager is the interface for managing and organizing cloud resources.</span></span> <span data-ttu-id="96794-105">请考虑使用资源管理器作为部署云资源的方法。</span><span class="sxs-lookup"><span data-stu-id="96794-105">Think of Resource Manager as a way to deploy cloud resources.</span></span>

<span data-ttu-id="96794-106">如果你熟悉 Azure 资源组, 则知道它们允许你将相关资源集视为一个单元。</span><span class="sxs-lookup"><span data-stu-id="96794-106">If you're familiar with Azure resource groups, you know that they enable you to treat sets of related resources as a single unit.</span></span> <span data-ttu-id="96794-107">资源管理器组织的资源组可让您在一次操作中部署、管理和删除所有资源。</span><span class="sxs-lookup"><span data-stu-id="96794-107">Resource Manager is what organizes the resource groups that let you deploy, manage, and delete all of the resources together in a single action.</span></span>

<span data-ttu-id="96794-108">考虑您为分析师运行的财务模型。</span><span class="sxs-lookup"><span data-stu-id="96794-108">Think about the financial models you run for your analysts.</span></span> <span data-ttu-id="96794-109">若要运行模型, 可能需要一个或多个虚拟机、存储数据的数据库和虚拟网络以在所有内容之间实现连接。</span><span class="sxs-lookup"><span data-stu-id="96794-109">To run a model, you might need one or more VMs, a database to store data, and a virtual network to enable connectivity between everything.</span></span> <span data-ttu-id="96794-110">使用资源管理器, 可以将这些资产部署到相同的资源组中, 并管理和监视它们。</span><span class="sxs-lookup"><span data-stu-id="96794-110">With Resource Manager, you deploy these assets into the same resource group and manage and monitor them together.</span></span> <span data-ttu-id="96794-111">完成后, 可以通过一次操作删除资源组中的所有资源。</span><span class="sxs-lookup"><span data-stu-id="96794-111">When you're done, you can delete all of the resources in a resource group in one operation.</span></span>

### <a name="what-are-resource-manager-templates"></a><span data-ttu-id="96794-112">什么是资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="96794-112">What are Resource Manager templates?</span></span>

<span data-ttu-id="96794-113">资源管理器_模板_精确定义部署中的所有资源管理器资源。</span><span class="sxs-lookup"><span data-stu-id="96794-113">A Resource Manager _template_ precisely defines all the Resource Manager resources in a deployment.</span></span> <span data-ttu-id="96794-114">您可以将资源管理器模板作为单个操作部署到资源组中。</span><span class="sxs-lookup"><span data-stu-id="96794-114">You can deploy a Resource Manager template into a resource group as a single operation.</span></span>

<span data-ttu-id="96794-115">资源管理器模板是一个 JSON 文件, 它成为_声明性自动化_的一种形式。</span><span class="sxs-lookup"><span data-stu-id="96794-115">A Resource Manager template is a JSON file, making it a form of _declarative automation_.</span></span> <span data-ttu-id="96794-116">声明性自动化意味着您可以定义所需的资源, 但不_是_创建_方式_。</span><span class="sxs-lookup"><span data-stu-id="96794-116">Declarative automation means that you define _what_ resources you need but not _how_ to create them.</span></span> <span data-ttu-id="96794-117">换句话说, 您可以定义所需的内容, 并且它是资源管理者的责任, 以确保正确部署资源。</span><span class="sxs-lookup"><span data-stu-id="96794-117">Put another way, you define what you need and it is Resource Manager's responsibility to ensure that resources are deployed correctly.</span></span>

<span data-ttu-id="96794-118">您可以将声明性自动化视为类似于 web 浏览器显示 HTML 文件的方式。</span><span class="sxs-lookup"><span data-stu-id="96794-118">You can think of declarative automation similar to how web browsers display HTML files.</span></span> <span data-ttu-id="96794-119">HTML 文件描述页面__ 上显示的元素, 但不说明_如何_显示这些元素。</span><span class="sxs-lookup"><span data-stu-id="96794-119">The HTML file describes _what_ elements appear on the page, but doesn't describe _how_ to display them.</span></span> <span data-ttu-id="96794-120">"如何" 是 web 浏览器的责任。</span><span class="sxs-lookup"><span data-stu-id="96794-120">The "how" is the web browser's responsibility.</span></span>

> [!NOTE]
> <span data-ttu-id="96794-121">你可能会听到其他人将资源管理器模板作为 "ARM 模板" 引用。</span><span class="sxs-lookup"><span data-stu-id="96794-121">You may hear others refer to Resource Manager templates as "ARM templates".</span></span> <span data-ttu-id="96794-122">我们更喜欢使用完整名称 "Azure 资源管理器模板" 或 "资源管理器模板"。</span><span class="sxs-lookup"><span data-stu-id="96794-122">We prefer the full names "Azure Resource Manager templates" or "Resource Manager templates".</span></span>

## <a name="why-use-resource-manager-templates"></a><span data-ttu-id="96794-123">为什么要使用资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="96794-123">Why use Resource Manager templates?</span></span>

<span data-ttu-id="96794-124">使用资源管理器模板可使部署速度更快且更具可重复。</span><span class="sxs-lookup"><span data-stu-id="96794-124">Using Resource Manager templates will make your deployments faster and more repeatable.</span></span> <span data-ttu-id="96794-125">例如, 您不再需要在门户中创建虚拟机, 请等待其完成, 然后创建下一个 vm, 依此类推。</span><span class="sxs-lookup"><span data-stu-id="96794-125">For example, you no longer have to create a VM in the portal, wait for it to finish, then create the next VM, and so on.</span></span> <span data-ttu-id="96794-126">资源管理器负责处理整个部署。</span><span class="sxs-lookup"><span data-stu-id="96794-126">Resource Manager takes care of the entire deployment for you.</span></span>

<span data-ttu-id="96794-127">以下是要考虑的其他一些好处。</span><span class="sxs-lookup"><span data-stu-id="96794-127">Here are some other benefits to consider.</span></span>

* <span data-ttu-id="96794-128">**模板提高一致性**</span><span class="sxs-lookup"><span data-stu-id="96794-128">**Templates improve consistency**</span></span>

    <span data-ttu-id="96794-129">资源管理器模板为您和其他人提供了一种用于描述您的部署的公共语言。</span><span class="sxs-lookup"><span data-stu-id="96794-129">Resource Manager templates provide a common language for you and others to describe your deployments.</span></span> <span data-ttu-id="96794-130">无论用于部署模板的工具或 SDK 是什么, 模板内的结构、格式和表达式都保持不变。</span><span class="sxs-lookup"><span data-stu-id="96794-130">Regardless of the tool or SDK used to deploy the template, the structure, format, and expressions inside the template remain the same.</span></span>

* <span data-ttu-id="96794-131">**模板可帮助快速进行复杂部署**</span><span class="sxs-lookup"><span data-stu-id="96794-131">**Templates help express complex deployments**</span></span>

    <span data-ttu-id="96794-132">使用模板, 可以按正确的顺序部署多个资源。</span><span class="sxs-lookup"><span data-stu-id="96794-132">Templates enable you to deploy multiple resources in the correct order.</span></span> <span data-ttu-id="96794-133">例如, 您不希望在创建 OS 磁盘或网络接口之前部署虚拟机。</span><span class="sxs-lookup"><span data-stu-id="96794-133">For example, you wouldn't want to deploy a virtual machine before creating OS disk or network interface.</span></span> <span data-ttu-id="96794-134">资源管理器将映射每个资源及其从属资源, 并首先创建从属资源。</span><span class="sxs-lookup"><span data-stu-id="96794-134">Resource Manager maps out each resource and its dependent resources and creates dependent resources first.</span></span> <span data-ttu-id="96794-135">依赖关系映射有助于确保按照正确的顺序执行部署。</span><span class="sxs-lookup"><span data-stu-id="96794-135">Dependency mapping helps ensure that the deployment is carried out in the correct order.</span></span>

* <span data-ttu-id="96794-136">**模板减少了手动且容易出错的任务**</span><span class="sxs-lookup"><span data-stu-id="96794-136">**Templates reduce manual, error-prone tasks**</span></span>

    <span data-ttu-id="96794-137">手动创建和连接资源可能需要很长时间, 同时也很容易出错。</span><span class="sxs-lookup"><span data-stu-id="96794-137">Manually creating and connecting resources can be time consuming, and it's easy to make mistakes along the way.</span></span> <span data-ttu-id="96794-138">资源管理器可确保每次都以相同的方式进行部署。</span><span class="sxs-lookup"><span data-stu-id="96794-138">Resource Manager ensures that the deployment happens the same way every time.</span></span>

* <span data-ttu-id="96794-139">**模板是代码**</span><span class="sxs-lookup"><span data-stu-id="96794-139">**Templates are code**</span></span>

    <span data-ttu-id="96794-140">模板通过代码表达你的要求。</span><span class="sxs-lookup"><span data-stu-id="96794-140">Templates express your requirements through code.</span></span> <span data-ttu-id="96794-141">将模板视为可像任何其他软件一样共享、测试和版本化的_代码的基础结构_类型。</span><span class="sxs-lookup"><span data-stu-id="96794-141">Think of a template as a type of _infrastructure as code_ that can be shared, tested, and versioned like any other piece of software.</span></span> <span data-ttu-id="96794-142">此外, 由于模板是代码, 因此您可以创建可遵循的 "纸张踪迹"。</span><span class="sxs-lookup"><span data-stu-id="96794-142">Also, because templates are code, you can create a "paper trail" that you can follow.</span></span> <span data-ttu-id="96794-143">模板代码记录部署。</span><span class="sxs-lookup"><span data-stu-id="96794-143">The template code documents the deployment.</span></span> <span data-ttu-id="96794-144">大多数用户在某种类型的修订控件 (如 Git) 下维护其模板。</span><span class="sxs-lookup"><span data-stu-id="96794-144">Most users maintain their templates under some kind of revision control, such as Git.</span></span> <span data-ttu-id="96794-145">更改模板时, 其修订历史记录还记录了模板 (和您的部署) 在一段时间内的发展方式。</span><span class="sxs-lookup"><span data-stu-id="96794-145">When you change the template, its revision history also documents how the template (and your deployment) has evolved over time.</span></span>

* <span data-ttu-id="96794-146">**模板促进重用**</span><span class="sxs-lookup"><span data-stu-id="96794-146">**Templates promote reuse**</span></span>

    <span data-ttu-id="96794-147">模板可以包含模板运行时填写的参数。</span><span class="sxs-lookup"><span data-stu-id="96794-147">Your template can contain parameters that are filled in when the template runs.</span></span> <span data-ttu-id="96794-148">参数可以定义用户名、密码、域名等。</span><span class="sxs-lookup"><span data-stu-id="96794-148">A parameter can define a username or password, a domain name, and so on.</span></span> <span data-ttu-id="96794-149">使用模板参数, 可以创建基础结构的多个版本, 如暂存和生产, 但仍能利用完全相同的模板。</span><span class="sxs-lookup"><span data-stu-id="96794-149">Template parameters enable you to create multiple versions of your infrastructure, such as staging and production, but still utilize the exact same template.</span></span>

* <span data-ttu-id="96794-150">**模板为 linkable**</span><span class="sxs-lookup"><span data-stu-id="96794-150">**Templates are linkable**</span></span>

    <span data-ttu-id="96794-151">可以将资源管理器模板链接在一起, 使模板本身成为模块式。</span><span class="sxs-lookup"><span data-stu-id="96794-151">Resource Manager templates can be linked together to make the templates themselves modular.</span></span> <span data-ttu-id="96794-152">您可以编写用于定义解决方案的一部分的小型模板, 并将它们组合起来以创建一个完整的系统。</span><span class="sxs-lookup"><span data-stu-id="96794-152">You can write small templates that each define a piece of a solution and combine them to create a complete system.</span></span>

<span data-ttu-id="96794-153">您的财务分析师运行的模型是唯一的, 但您可以在底层基础结构中看到模式。</span><span class="sxs-lookup"><span data-stu-id="96794-153">The models your financial analysts run are unique, but you see patterns in the underlying infrastructure.</span></span> <span data-ttu-id="96794-154">例如, 大多数模型都需要数据库来存储数据。</span><span class="sxs-lookup"><span data-stu-id="96794-154">For example, most models require a database to store data.</span></span> <span data-ttu-id="96794-155">许多模型都使用相同的编程语言、框架和操作系统来执行详细信息。</span><span class="sxs-lookup"><span data-stu-id="96794-155">Many models use the same programming languages, frameworks, and operating systems to carry out the details.</span></span> <span data-ttu-id="96794-156">您可以定义用于描述每个组件 (计算、存储、网络等) 的模板, 并将它们组合起来以满足每个分析者的特定需求。</span><span class="sxs-lookup"><span data-stu-id="96794-156">You can define templates that describe each individual component (compute, storage, networking, and so on), and combine them to meet each analyst's specific needs.</span></span>

## <a name="whats-in-a-resource-manager-template"></a><span data-ttu-id="96794-157">资源管理器模板中的内容有哪些？</span><span class="sxs-lookup"><span data-stu-id="96794-157">What's in a Resource Manager template?</span></span>

> [!NOTE]
> <span data-ttu-id="96794-158">在这里, 你将看到几个代码示例, 让你了解每个节的构造方式。</span><span class="sxs-lookup"><span data-stu-id="96794-158">Here you'll see a few code examples to give you a sense of how each section is structured.</span></span> <span data-ttu-id="96794-159">如果你看到的内容对你&mdash;不熟悉, 请不要担心, 你将能够阅读其他人的模板, 并在你获得与他们的实践体验时编写自己的体验。</span><span class="sxs-lookup"><span data-stu-id="96794-159">Don't worry if what you see is unfamiliar to you &mdash; you'll be able to read others' templates and write your own as you gain hands-on experience with them.</span></span>

<span data-ttu-id="96794-160">您可能已使用 JSON 或 JavaScript 对象表示法, 以在服务器和 web 应用程序之间发送数据。</span><span class="sxs-lookup"><span data-stu-id="96794-160">You may have used JSON, or JavaScript Object Notation, to send data between servers and web applications.</span></span> <span data-ttu-id="96794-161">JSON 也是描述如何配置应用程序和基础结构的常用方法。</span><span class="sxs-lookup"><span data-stu-id="96794-161">JSON is also a popular way to describe how applications and infrastructure are configured.</span></span> 

<span data-ttu-id="96794-162">JSON 使我们能够将存储为对象 (如虚拟机) 的数据表示为文本。</span><span class="sxs-lookup"><span data-stu-id="96794-162">JSON allows us to express data stored as an object (such as a virtual machine) in text.</span></span> <span data-ttu-id="96794-163">JSON 文档实质上是键值对的集合。</span><span class="sxs-lookup"><span data-stu-id="96794-163">A JSON document is essentially a collection of key-value pairs.</span></span> <span data-ttu-id="96794-164">每个键都是一个字符串;其值可以是字符串、数字、布尔表达式、值列表或对象 (是其他键值对的集合)。</span><span class="sxs-lookup"><span data-stu-id="96794-164">Each key is a string; its value can be a string, a number, a Boolean expression, a list of values, or an object (which is a collection of other key-value pairs).</span></span>

<span data-ttu-id="96794-165">资源管理器模板可包含以下部分。</span><span class="sxs-lookup"><span data-stu-id="96794-165">A Resource Manager template can contain the following sections.</span></span> <span data-ttu-id="96794-166">这些节使用 json 表示法表示, 但与 json 语言本身无关。</span><span class="sxs-lookup"><span data-stu-id="96794-166">These sections are expressed using JSON notation, but are not related to the JSON language itself.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "functions": [  ],
    "resources": [  ],
    "outputs": {  }
}
```
<span data-ttu-id="96794-167">让我们更详细了解一下其中的每个部分。</span><span class="sxs-lookup"><span data-stu-id="96794-167">Let's look at each of these sections in a little more detail.</span></span>

### <a name="parameters"></a><span data-ttu-id="96794-168">参数</span><span class="sxs-lookup"><span data-stu-id="96794-168">Parameters</span></span>

<span data-ttu-id="96794-169">您可以在此处指定模板运行时可配置的值。</span><span class="sxs-lookup"><span data-stu-id="96794-169">This is where you specify which values are configurable when the template runs.</span></span> <span data-ttu-id="96794-170">例如, 您可能允许模板的用户指定用户名、密码或域名。</span><span class="sxs-lookup"><span data-stu-id="96794-170">For example, you might allow users of your template to specify a username, password, or domain name.</span></span>

<span data-ttu-id="96794-171">下面的示例展示了一个 VM 的&ndash;用户名的两个参数, 一个用于其密码。</span><span class="sxs-lookup"><span data-stu-id="96794-171">Here's an example that illustrates two parameters &ndash; one for a VM's username and one for its password.</span></span>

```json
"parameters": {
  "adminUsername": {
    "type": "string",
    "metadata": {
      "description": "Username for the Virtual Machine."
    }
  },
  "adminPassword": {
    "type": "securestring",
    "metadata": {
      "description": "Password for the Virtual Machine."
    }
  }
}
```

### <a name="variables"></a><span data-ttu-id="96794-172">Variables</span><span class="sxs-lookup"><span data-stu-id="96794-172">Variables</span></span> 

<span data-ttu-id="96794-173">您可以在此处定义在整个模板中使用的值。</span><span class="sxs-lookup"><span data-stu-id="96794-173">This is where you define values that are used throughout the template.</span></span> <span data-ttu-id="96794-174">变量有助于使模板更易于维护。</span><span class="sxs-lookup"><span data-stu-id="96794-174">Variables can help make your templates easier to maintain.</span></span> <span data-ttu-id="96794-175">例如, 您可以将一个存储帐户名称定义一次作为变量, 并在整个模板中使用该变量。</span><span class="sxs-lookup"><span data-stu-id="96794-175">For example, you might define a storage account name one time as a variable and use that variable throughout the template.</span></span> <span data-ttu-id="96794-176">如果存储帐户名称发生更改, 则只需更新变量。</span><span class="sxs-lookup"><span data-stu-id="96794-176">If the storage account name changes, you need to only update the variable.</span></span>

<span data-ttu-id="96794-177">下面的示例展示了几个描述 VM 的网络功能的变量。</span><span class="sxs-lookup"><span data-stu-id="96794-177">Here's an example that illustrates a few variables that describe networking features for a VM.</span></span>

```json
"variables": {
  "nicName": "myVMNic",
  "addressPrefix": "10.0.0.0/16",
  "subnetName": "Subnet",
  "subnetPrefix": "10.0.0.0/24",
  "publicIPAddressName": "myPublicIP",
  "virtualNetworkName": "MyVNET"
}
```

### <a name="functions"></a><span data-ttu-id="96794-178">函数</span><span class="sxs-lookup"><span data-stu-id="96794-178">Functions</span></span>

<span data-ttu-id="96794-179">您可以在此处定义不希望在整个模板中重复的过程。</span><span class="sxs-lookup"><span data-stu-id="96794-179">This is where you define procedures that you don't want to repeat throughout the template.</span></span> <span data-ttu-id="96794-180">与变量一样, 函数可帮助使模板更易于维护。</span><span class="sxs-lookup"><span data-stu-id="96794-180">Like variables, functions can help make your templates easier to maintain.</span></span> <span data-ttu-id="96794-181">下面的示例创建一个函数, 以创建一个可在创建具有全局唯一命名要求的资源时使用的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="96794-181">Here's an example that creates a function to create a unique name that could be used when creating resources that have globally unique naming requirements.</span></span>

```json
"functions": [
  {
    "namespace": "contoso",
    "members": {
      "uniqueName": {
        "parameters": [
          {
            "name": "namePrefix",
            "type": "string"
          }
        ],
        "output": {
          "type": "string",
          "value": "[concat(toLower(parameters('namePrefix')), uniqueString(resourceGroup().id))]"
        }
      }
    }
  }
],
```

### <a name="resources"></a><span data-ttu-id="96794-182">中心</span><span class="sxs-lookup"><span data-stu-id="96794-182">Resources</span></span>

<span data-ttu-id="96794-183">在此部分中, 可以定义构成部署的 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="96794-183">This section is where you define the Azure resources that make up your deployment.</span></span>

<span data-ttu-id="96794-184">下面的示例展示了如何创建公用 IP 地址资源。</span><span class="sxs-lookup"><span data-stu-id="96794-184">Here's an example that creates a public IP address resource.</span></span>

```json
{
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIPAddressName')]",
  "location": "[parameters('location')]",
  "apiVersion": "2018-08-01",
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('dnsLabelPrefix')]"
    }
  }
}
```

<span data-ttu-id="96794-185">在这里, 资源的类型为`Microsoft.Network/publicIPAddresses`。</span><span class="sxs-lookup"><span data-stu-id="96794-185">Here, the type of resource is `Microsoft.Network/publicIPAddresses`.</span></span> <span data-ttu-id="96794-186">将从 "变量" 部分读取其名称, 并从 "参数" 部分读取其位置 (或 Azure 区域)。</span><span class="sxs-lookup"><span data-stu-id="96794-186">Its name is read from the variables section and its location, or Azure region, is read from the parameters section.</span></span>

<span data-ttu-id="96794-187">由于资源类型可以随着时间的推移`apiVersion`而更改, 因此请参考要使用的资源类型的版本。</span><span class="sxs-lookup"><span data-stu-id="96794-187">Because resource types can change over time, `apiVersion` refers to the version of the resource type you want to use.</span></span> <span data-ttu-id="96794-188">随着资源类型的演化和变化, 您可以修改模板以在准备就绪时使用最新的功能。</span><span class="sxs-lookup"><span data-stu-id="96794-188">As resource types evolve and change, you can modify your templates to work with the latest features when you're ready.</span></span>

### <a name="outputs"></a><span data-ttu-id="96794-189">产出</span><span class="sxs-lookup"><span data-stu-id="96794-189">Outputs</span></span>

<span data-ttu-id="96794-190">您可以在此处定义模板运行时想要接收的任何信息。</span><span class="sxs-lookup"><span data-stu-id="96794-190">This is where you define any information you'd like to receive when the template runs.</span></span> <span data-ttu-id="96794-191">例如, 你可能想要在部署运行之前接收你不知道的&ndash; VM 的 IP 地址或 FQDN 信息。</span><span class="sxs-lookup"><span data-stu-id="96794-191">For example, you might want to receive your VM's IP address or FQDN &ndash; information you do not know until the deployment runs.</span></span>

<span data-ttu-id="96794-192">下面的示例展示了一个名为 "hostname" 的输出。</span><span class="sxs-lookup"><span data-stu-id="96794-192">Here's an example that illustrates an output named "hostname".</span></span> <span data-ttu-id="96794-193">FQDN 值是从 VM 的公共 IP 地址设置中读取的。</span><span class="sxs-lookup"><span data-stu-id="96794-193">The FQDN value is read from the VM's public IP address settings.</span></span>

```json
"outputs": {
  "hostname": {
    "type": "string",
    "value": "[reference(variables('publicIPAddressName')).dnsSettings.fqdn]"
  }
}
```

## <a name="how-do-i-write-a-resource-manager-template"></a><span data-ttu-id="96794-194">如何编写资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="96794-194">How do I write a Resource Manager template?</span></span>

<span data-ttu-id="96794-195">编写资源管理器模板有多种方法。</span><span class="sxs-lookup"><span data-stu-id="96794-195">There are many approaches to writing Resource Manager templates.</span></span> <span data-ttu-id="96794-196">虽然您可以从头开始编写模板, 但从现有模板开始, 并根据您的需要对其进行修改是很常见的。</span><span class="sxs-lookup"><span data-stu-id="96794-196">Although you can write a template from scratch, it's common to start with an existing template and modify it to suit your needs.</span></span>

<span data-ttu-id="96794-197">下面是可以获取初学者模板的几种方法:</span><span class="sxs-lookup"><span data-stu-id="96794-197">Here are a few ways you can get a starter template:</span></span>

* <span data-ttu-id="96794-198">使用 Azure 门户创建基于现有资源组中的资源的模板。</span><span class="sxs-lookup"><span data-stu-id="96794-198">Use the Azure portal to create a template based on the resources in an existing resource group.</span></span>
* <span data-ttu-id="96794-199">从你或你的团队构建的用于类似用途的模板开始。</span><span class="sxs-lookup"><span data-stu-id="96794-199">Start with a template you or your team built that serves a similar purpose.</span></span>
* <span data-ttu-id="96794-200">从 Azure 快速入门模板开始。</span><span class="sxs-lookup"><span data-stu-id="96794-200">Start with an Azure Quickstart template.</span></span> <span data-ttu-id="96794-201">你将在下一部分中了解如何操作。</span><span class="sxs-lookup"><span data-stu-id="96794-201">You'll see how in the next part.</span></span>

<span data-ttu-id="96794-202">无论采用何种方法, 编写模板都涉及使用文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="96794-202">No matter your approach, writing a template involves working with a text editor.</span></span> <span data-ttu-id="96794-203">您可以引入常用编辑器, 但 Visual Studio Code 的[Azure 资源管理器工具扩展](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools&azure-portal=true)是专门为创建模板的任务而设计的。</span><span class="sxs-lookup"><span data-stu-id="96794-203">You can bring your favorite editor, but Visual Studio Code's [Azure Resource Manager Tools extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools&azure-portal=true) is specially designed for the task of creating templates.</span></span> <span data-ttu-id="96794-204">通过此扩展, 可以更轻松地导航模板代码并为许多常见任务提供自动完成。</span><span class="sxs-lookup"><span data-stu-id="96794-204">This extension makes it easier to navigate your template code and provides autocompletion for many common tasks.</span></span>

<span data-ttu-id="96794-205">在您浏览和编写模板时, 您将需要[参考文档](https://docs.microsoft.com/azure/templates?azure-portal=true), 以了解哪些资源类型可用以及如何使用它们。</span><span class="sxs-lookup"><span data-stu-id="96794-205">As you explore and write your templates, you'll want to [refer to the documentation](https://docs.microsoft.com/azure/templates?azure-portal=true) to understand what resource types are available and how to use them.</span></span>