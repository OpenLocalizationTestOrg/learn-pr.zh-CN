<span data-ttu-id="d669d-101">在为财务分析员创建 VM 时, 通常会包含一个 web 服务器, 该服务器为分析者提供仪表板以可视化和收集运行结果。</span><span class="sxs-lookup"><span data-stu-id="d669d-101">When you create a VM for your financial analysts, you typically include a web server that provides a dashboard for the analyst to visualize and collect the results of the run.</span></span> <span data-ttu-id="d669d-102">使用资源管理器模板来引入虚拟机是一个好的开端。</span><span class="sxs-lookup"><span data-stu-id="d669d-102">Using a Resource Manager template to bring up a VM is a good start.</span></span> <span data-ttu-id="d669d-103">但如何扩展模板以在 VM 中配置 web 服务器软件？</span><span class="sxs-lookup"><span data-stu-id="d669d-103">But how can you extend the template to configure web server software inside the VM?</span></span>

<span data-ttu-id="d669d-104">使用 Azure CLI 将虚拟机配置为运行 web 服务器只需要几个基本命令。</span><span class="sxs-lookup"><span data-stu-id="d669d-104">Using the Azure CLI to configure a VM to run a web server requires only a few basic commands.</span></span> <span data-ttu-id="d669d-105">但在以下情况下会发生什么情况:</span><span class="sxs-lookup"><span data-stu-id="d669d-105">But what happens when:</span></span>

* <span data-ttu-id="d669d-106">您需要连续创建和删除 vm？</span><span class="sxs-lookup"><span data-stu-id="d669d-106">You need to create and delete VMs continuously?</span></span>
* <span data-ttu-id="d669d-107">您的部署需要其他组件 (如存储和网络), 从而增加了复杂性？</span><span class="sxs-lookup"><span data-stu-id="d669d-107">Your deployments require additional components such as storage and networking, increasing their complexity?</span></span>

<span data-ttu-id="d669d-108">通过 Azure CLI 管理各个资源是一个很出色的开端。</span><span class="sxs-lookup"><span data-stu-id="d669d-108">Managing individual resources through the Azure CLI is a good start.</span></span> <span data-ttu-id="d669d-109">但它很快会变得单调乏味且容易出错, 因为您仍需要将资源正确地连接在一起。</span><span class="sxs-lookup"><span data-stu-id="d669d-109">But it quickly becomes tedious and error prone because you still need to correctly connect resources together.</span></span> <span data-ttu-id="d669d-110">您需要一个更自动化的解决方案。</span><span class="sxs-lookup"><span data-stu-id="d669d-110">You need a more automated solution.</span></span>

<span data-ttu-id="d669d-111">在这里, 你将检查 VM web 服务器的要求, 并了解如何生成可添加到模板中的资源。</span><span class="sxs-lookup"><span data-stu-id="d669d-111">Here you'll examine the requirements for your VM's web server and learn how to build resources you can add to your templates.</span></span>

> [!NOTE]
> <span data-ttu-id="d669d-112">您在此页面上看到的代码和命令用于说明。</span><span class="sxs-lookup"><span data-stu-id="d669d-112">The code and commands you see on this page are for illustration.</span></span> <span data-ttu-id="d669d-113">现在, 只需继续操作。</span><span class="sxs-lookup"><span data-stu-id="d669d-113">For now, just follow along.</span></span> <span data-ttu-id="d669d-114">您不需要修改任何文件或运行任何命令。</span><span class="sxs-lookup"><span data-stu-id="d669d-114">You don't need to modify any files or run any commands just yet.</span></span>

## <a name="whats-the-custom-script-extension"></a><span data-ttu-id="d669d-115">自定义脚本扩展名是什么？</span><span class="sxs-lookup"><span data-stu-id="d669d-115">What's the Custom Script Extension?</span></span>

<span data-ttu-id="d669d-116">自定义脚本扩展是在 Azure 虚拟机上下载和运行脚本的简单方法。</span><span class="sxs-lookup"><span data-stu-id="d669d-116">The Custom Script Extension is an easy way to download and run scripts on your Azure VMs.</span></span> <span data-ttu-id="d669d-117">它只是在虚拟机启动并运行后配置虚拟机的多种方法之一。</span><span class="sxs-lookup"><span data-stu-id="d669d-117">It's just one of the many ways you can configure a VM once it's up and running.</span></span>

<span data-ttu-id="d669d-118">你可以将脚本存储在 Azure 存储或公共位置 (如 GitHub) 中。</span><span class="sxs-lookup"><span data-stu-id="d669d-118">You can store your scripts in Azure storage or in a public location such as GitHub.</span></span> <span data-ttu-id="d669d-119">您可以手动运行脚本, 也可以将其作为更自动化的部署的一部分运行。</span><span class="sxs-lookup"><span data-stu-id="d669d-119">You can run scripts manually or as part of a more automated deployment.</span></span> <span data-ttu-id="d669d-120">在这里, 你将定义即将添加到资源管理器模板中的资源。</span><span class="sxs-lookup"><span data-stu-id="d669d-120">Here, you'll define a  resource that you'll soon add to your Resource Manager template.</span></span> <span data-ttu-id="d669d-121">资源将使用自定义脚本扩展从 GitHub 下载 Bash 脚本并在您的 VM 上执行该脚本。</span><span class="sxs-lookup"><span data-stu-id="d669d-121">The resource will use the Custom Script Extension to download a Bash script from GitHub and execute that script on your VM.</span></span> <span data-ttu-id="d669d-122">该脚本会安装和配置 Nginx web 服务器软件包并配置基本主页。</span><span class="sxs-lookup"><span data-stu-id="d669d-122">The script installs and configures the Nginx web server software package and configures a basic home page.</span></span>

## <a name="how-do-i-extend-a-resource-manager-template"></a><span data-ttu-id="d669d-123">如何扩展资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="d669d-123">How do I extend a Resource Manager template?</span></span>

<span data-ttu-id="d669d-124">您的资源管理器模板创建了 Ubuntu Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="d669d-124">Your Resource Manager template creates an Ubuntu Linux VM.</span></span> <span data-ttu-id="d669d-125">在 VM 启动时, 有几种方法可以扩展模板以安装 Nginx。</span><span class="sxs-lookup"><span data-stu-id="d669d-125">There are a few ways to extend the template to also install Nginx when the VM starts.</span></span>

<span data-ttu-id="d669d-126">扩展模板的一种方法是创建多个模板, 每个模板定义一段系统。</span><span class="sxs-lookup"><span data-stu-id="d669d-126">One way to extend your template is to create multiple templates, each defining one piece of the system.</span></span> <span data-ttu-id="d669d-127">然后, 将它们_链接_或_嵌套_在一起, 以生成更完整的系统。</span><span class="sxs-lookup"><span data-stu-id="d669d-127">You then _link_ or _nest_ them together to build a more complete system.</span></span> <span data-ttu-id="d669d-128">创建您自己的模板时, 可以构建一个较小、更精细的模板的库, 并将它们与您所需的方式相结合。</span><span class="sxs-lookup"><span data-stu-id="d669d-128">As you create your own templates, you can build a library of smaller, more granular templates and combine them how you need.</span></span>

<span data-ttu-id="d669d-129">另一种方法是修改现有模板以满足您的需求。</span><span class="sxs-lookup"><span data-stu-id="d669d-129">Another way is to modify an existing template to suit your needs.</span></span> <span data-ttu-id="d669d-130">你将在此模块中执行此操作, 因为这通常是开始编写你自己的模板的最快方法。</span><span class="sxs-lookup"><span data-stu-id="d669d-130">You'll do that in this module because that's often the fastest way to get started writing your own templates.</span></span>

## <a name="build-the-template-resource"></a><span data-ttu-id="d669d-131">生成模板资源</span><span class="sxs-lookup"><span data-stu-id="d669d-131">Build the template resource</span></span>

<span data-ttu-id="d669d-132">在这里, 你将了解如何使用自定义脚本扩展作为示例来构建模板资源。</span><span class="sxs-lookup"><span data-stu-id="d669d-132">Here you'll learn how to build template resources, using the Custom Script Extension as an example.</span></span> <span data-ttu-id="d669d-133">将参考文档用作起始点, 然后定义所需的资源属性。</span><span class="sxs-lookup"><span data-stu-id="d669d-133">You'll use the reference documentation as a starting point and then define the resource properties you need.</span></span>

<span data-ttu-id="d669d-134">让我们先查看你的要求。</span><span class="sxs-lookup"><span data-stu-id="d669d-134">Let's start by reviewing your requirements.</span></span>

### <a name="gather-requirements"></a><span data-ttu-id="d669d-135">收集要求</span><span class="sxs-lookup"><span data-stu-id="d669d-135">Gather requirements</span></span>

<span data-ttu-id="d669d-136">下面简要介绍了您希望通过模板实现的功能。</span><span class="sxs-lookup"><span data-stu-id="d669d-136">Here's a brief summary of what you want to accomplish through your template.</span></span>

1. <span data-ttu-id="d669d-137">创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="d669d-137">Create a VM.</span></span>
1. <span data-ttu-id="d669d-138">通过网络防火墙打开端口80。</span><span class="sxs-lookup"><span data-stu-id="d669d-138">Open port 80 through the network firewall.</span></span>
1. <span data-ttu-id="d669d-139">在 VM 上安装和配置 web 服务器软件。</span><span class="sxs-lookup"><span data-stu-id="d669d-139">Install and configure web server software on your VM.</span></span>

<span data-ttu-id="d669d-140">上一部件中使用的资源管理器模板已涵盖前两个要求。</span><span class="sxs-lookup"><span data-stu-id="d669d-140">The Resource Manager template you used in the previous part already covers the first two requirements.</span></span> <span data-ttu-id="d669d-141">第三个是, 让我们先看一看 Azure CLI 命令, 我们可以从命令行手动运行, 使用自定义脚本扩展在你的 VM 上安装和配置 Nginx。</span><span class="sxs-lookup"><span data-stu-id="d669d-141">For the third, let's start by taking a look at an Azure CLI command we could run manually from the command line to install and configure Nginx on your VM using the Custom Script Extension.</span></span>

```azurecli
az vm extension set \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --vm-name MyUbuntuVM \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --version 2.0 \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```

<span data-ttu-id="d669d-142">此命令使用自定义脚本扩展在你的 VM 上运行可安装 Nginx 的 Bash 脚本。</span><span class="sxs-lookup"><span data-stu-id="d669d-142">This command uses the Custom Script Extension to run a Bash script on your VM that installs Nginx.</span></span> <span data-ttu-id="d669d-143">如果你愿意, 可以从单独的浏览器选项卡[检查 Bash 脚本](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="d669d-143">You can [examine the Bash script](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh?azure-portal=true) from a separate browser tab if you'd like.</span></span>

<span data-ttu-id="d669d-144">您需要一种方法来映射此命令以使用资源管理器模板语法。</span><span class="sxs-lookup"><span data-stu-id="d669d-144">You need a way to map this command to use the Resource Manager template syntax.</span></span> <span data-ttu-id="d669d-145">上面`az vm extension set`显示的示例是您在命令行中输入的命令。</span><span class="sxs-lookup"><span data-stu-id="d669d-145">The `az vm extension set` example shown above is a command you'd enter on the command line.</span></span> <span data-ttu-id="d669d-146">您需要的是模板格式的声明性 JSON。</span><span class="sxs-lookup"><span data-stu-id="d669d-146">What you need is the declarative JSON in template format.</span></span>

### <a name="locate-the-resource-schema"></a><span data-ttu-id="d669d-147">查找资源架构</span><span class="sxs-lookup"><span data-stu-id="d669d-147">Locate the resource schema</span></span>

<span data-ttu-id="d669d-148">若要了解如何在模板中使用自定义脚本扩展, 一种方法是按示例学习。</span><span class="sxs-lookup"><span data-stu-id="d669d-148">To discover how to use the Custom Script Extension in your template, one approach is to learn by example.</span></span> <span data-ttu-id="d669d-149">例如, 你可能会发现一个 Azure 快速入门模板执行类似操作, 并根据你的需要对其进行调整。</span><span class="sxs-lookup"><span data-stu-id="d669d-149">For example, you might find an Azure Quickstart template that does something similar and adapt it to your needs.</span></span>

<span data-ttu-id="d669d-150">另一种方法是在[参考文档](https://docs.microsoft.com/azure/templates?azure-portal=true)中查找所需的资源。</span><span class="sxs-lookup"><span data-stu-id="d669d-150">Another approach is to look up the resource you need in the [reference documentation](https://docs.microsoft.com/azure/templates?azure-portal=true).</span></span> <span data-ttu-id="d669d-151">在这种情况下, 搜索文档会显示[Microsoft。计算 virtualMachines/extension 模板参考](https://docs.microsoft.com/azure/templates/Microsoft.Compute/2018-10-01/virtualMachines/extensions?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="d669d-151">In this case, searching the documentation would reveal [Microsoft.Compute virtualMachines/extensions template reference](https://docs.microsoft.com/azure/templates/Microsoft.Compute/2018-10-01/virtualMachines/extensions?azure-portal=true).</span></span>

<span data-ttu-id="d669d-152">您可以先将架构复制到临时文档, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="d669d-152">You can start by copying the schema to a temporary document, like this.</span></span>

```json
{
  "name": "string",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-10-01",
  "location": "string",
  "tags": {},
  "properties": {
    "publisher": "string",
    "type": "string",
    "typeHandlerVersion": "string",
    "autoUpgradeMinorVersion": boolean,
    "settings": {},
    "protectedSettings": {},
    "instanceView": {
      "name": "string",
      "type": "string",
      "typeHandlerVersion": "string",
      "substatuses": [
        {
          "code": "string",
          "level": "string",
          "displayStatus": "string",
          "message": "string",
          "time": "string"
        }
      ],
      "statuses": [
        {
          "code": "string",
          "level": "string",
          "displayStatus": "string",
          "message": "string",
          "time": "string"
        }
      ]
    }
  }
}
```

### <a name="specify-required-properties"></a><span data-ttu-id="d669d-153">指定所需属性</span><span class="sxs-lookup"><span data-stu-id="d669d-153">Specify required properties</span></span>

<span data-ttu-id="d669d-154">架构显示您可以提供的所有属性。</span><span class="sxs-lookup"><span data-stu-id="d669d-154">The schema shows all of the properties you can provide.</span></span> <span data-ttu-id="d669d-155">有些属性是必需的。其他选项是可选的。</span><span class="sxs-lookup"><span data-stu-id="d669d-155">Some properties are required; others are optional.</span></span> <span data-ttu-id="d669d-156">您可以从确定所有必需属性开始。</span><span class="sxs-lookup"><span data-stu-id="d669d-156">You might start by identifying all of the required properties.</span></span> <span data-ttu-id="d669d-157">请在 "参考" 页面上的架构定义下找到这些。</span><span class="sxs-lookup"><span data-stu-id="d669d-157">Locate these below the schema definition on the reference page.</span></span>

<span data-ttu-id="d669d-158">下面是必需的参数。</span><span class="sxs-lookup"><span data-stu-id="d669d-158">Here are the required parameters.</span></span>

* `name`
* `type`
* `apiVersion`
* `location`
* `properties`

<span data-ttu-id="d669d-159">删除所有不需要的参数后, 资源定义可能如下所示。</span><span class="sxs-lookup"><span data-stu-id="d669d-159">After you remove all the parameters that aren't required, your resource definition might look like this.</span></span>

```json
{
  "name": "[concat(variables('vmName'), '/', 'ConfigureNginx')]",
  "type": "Microsoft.Azure.Extensions/virtualMachines/extensions",
  "apiVersion": "2018-06-01",
  "location": "[parameters('location')]",
  "properties": { }
}
```

<span data-ttu-id="d669d-160">`type`和`apiVersion`属性的值直接来自文档。</span><span class="sxs-lookup"><span data-stu-id="d669d-160">The values for the `type` and `apiVersion` properties come directly from the documentation.</span></span> <span data-ttu-id="d669d-161">`properties`是必需的, 但现在可以是空的。</span><span class="sxs-lookup"><span data-stu-id="d669d-161">`properties` is required but for now can be empty.</span></span>

<span data-ttu-id="d669d-162">您知道现有 VM 模板具有一个名为`location`的参数。</span><span class="sxs-lookup"><span data-stu-id="d669d-162">You know that your existing VM template has a parameter named `location`.</span></span> <span data-ttu-id="d669d-163">本示例使用内置`parameters`函数来读取该值。</span><span class="sxs-lookup"><span data-stu-id="d669d-163">This example uses the built-in `parameters` function to read that value.</span></span>

<span data-ttu-id="d669d-164">该`name`属性遵循特殊约定。</span><span class="sxs-lookup"><span data-stu-id="d669d-164">The `name` property follows a special convention.</span></span> <span data-ttu-id="d669d-165">此示例使用内置`concat`函数连接或组合多个字符串。</span><span class="sxs-lookup"><span data-stu-id="d669d-165">This example uses the built-in `concat` function to concatenate, or combine, multiple strings.</span></span> <span data-ttu-id="d669d-166">完整的字符串包含 VM 名称, 后跟一个斜杠`/`字符, 后跟您选择的名称 (这里是 "ConfigureNginx")。</span><span class="sxs-lookup"><span data-stu-id="d669d-166">The complete string contains the VM name followed by a slash `/` character followed by a name you choose (here, it's "ConfigureNginx").</span></span> <span data-ttu-id="d669d-167">VM 名称可帮助模板标识要在其上运行脚本的 VM 资源。</span><span class="sxs-lookup"><span data-stu-id="d669d-167">The VM name helps the template identify which VM resource to run the script on.</span></span>

### <a name="specify-additional-properties"></a><span data-ttu-id="d669d-168">指定其他属性</span><span class="sxs-lookup"><span data-stu-id="d669d-168">Specify additional properties</span></span>

<span data-ttu-id="d669d-169">接下来, 您可以添加所需的任何其他属性。</span><span class="sxs-lookup"><span data-stu-id="d669d-169">Next, you might add in any additional properties that you need.</span></span> <span data-ttu-id="d669d-170">重新引用 CLI 示例之前, 您需要脚本文件的位置或 URI, 以及要在 VM 上执行以运行该脚本的 Bash 命令。</span><span class="sxs-lookup"><span data-stu-id="d669d-170">Referring back to the CLI example earlier, you need the location, or URI, of the script file and the Bash command to execute on the VM to run that script.</span></span> <span data-ttu-id="d669d-171">作为建议的做法, 还可以包含资源的发布者名称、类型和版本。</span><span class="sxs-lookup"><span data-stu-id="d669d-171">As a recommended practice, you might also include the resource's publisher name, its type, and version.</span></span>

<span data-ttu-id="d669d-172">参考本文档, 您需要使用 "点" 表示法中显示的这些值。</span><span class="sxs-lookup"><span data-stu-id="d669d-172">Referring back to the documentation, you need these values, shown here using "dot" notation.</span></span>

* `properties.publisher`
* `properties.type`
* `properties.typeHandlerVersion`
* `properties.autoUpgradeMinorVersion`
* `properties.settings.fileUris`
* `properties.protectedSettings.commandToExecute`

<span data-ttu-id="d669d-173">现在, 您的自定义脚本扩展资源如下所示。</span><span class="sxs-lookup"><span data-stu-id="d669d-173">Your Custom Script Extension resource now looks like this.</span></span>

```json
{
  "name": "[concat(variables('vmName'), '/', 'ConfigureNginx')]",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-06-01",
  "location": "[parameters('location')]",
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "customScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "./configure-nginx.sh"
    }
  }
}
```

### <a name="specify-dependent-resources"></a><span data-ttu-id="d669d-174">指定依存资源</span><span class="sxs-lookup"><span data-stu-id="d669d-174">Specify dependent resources</span></span>

<span data-ttu-id="d669d-175">在虚拟机可用之前, 不能运行自定义脚本扩展。</span><span class="sxs-lookup"><span data-stu-id="d669d-175">You can't run the Custom Script Extension until the VM is available.</span></span> <span data-ttu-id="d669d-176">所有模板资源都提供`dependsOn`属性。</span><span class="sxs-lookup"><span data-stu-id="d669d-176">All template resources provide a `dependsOn` property.</span></span> <span data-ttu-id="d669d-177">此属性可帮助资源管理器确定应用资源的正确顺序。</span><span class="sxs-lookup"><span data-stu-id="d669d-177">This property helps Resource Manager determine the correct order to apply resources.</span></span>

<span data-ttu-id="d669d-178">下面是添加`dependsOn`属性后模板资源可能的外观。</span><span class="sxs-lookup"><span data-stu-id="d669d-178">Here's what your template resource might look like after you add the `dependsOn` property.</span></span>

```json
{
  "name": "[concat(variables('vmName'), '/', 'ConfigureNginx')]",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-06-01",
  "location": "[parameters('location')]",
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "customScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "./configure-nginx.sh"
    }
  },
  "dependsOn": [
    "[resourceId('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ]
}
```

<span data-ttu-id="d669d-179">括号`[ ]`语法意味着可以提供在应用此资源之前必须存在的资源列表 (一个或一组)。</span><span class="sxs-lookup"><span data-stu-id="d669d-179">The bracket `[ ]` syntax means that you can provide an array, or list, of resources that must exist before applying this resource.</span></span>

<span data-ttu-id="d669d-180">有多种方法可以定义资源相关性。</span><span class="sxs-lookup"><span data-stu-id="d669d-180">There are multiple ways to define a resource dependency.</span></span> <span data-ttu-id="d669d-181">您可以提供它的名称, 如 "MyUbuntuVM"、全名 (包括其命名空间、类型和名称), 例如 "MyUbuntuVM/virtualMachines/", 或按其资源 ID。</span><span class="sxs-lookup"><span data-stu-id="d669d-181">You can provide its name, such as "MyUbuntuVM", it's full name (including its namespace, type, and name), such as "Microsoft.Compute/virtualMachines/MyUbuntuVM", or by its resource ID.</span></span>

<span data-ttu-id="d669d-182">此示例使用内置`resourceId`函数获取虚拟机的资源 ID (使用其完整名称)。</span><span class="sxs-lookup"><span data-stu-id="d669d-182">This example uses the built-in `resourceId` function to get the VM's resource ID using its full name.</span></span> <span data-ttu-id="d669d-183">这有助于阐明所引用的资源, 并有助于避免在多个资源具有相似名称时出现歧义。</span><span class="sxs-lookup"><span data-stu-id="d669d-183">This helps clarify which resource you're referring to and can help avoid ambiguity when more than one resource has a similar name.</span></span>

<span data-ttu-id="d669d-184">现有模板提供了一个`vmName`定义 VM 名称的变量。</span><span class="sxs-lookup"><span data-stu-id="d669d-184">The existing template provides a `vmName` variable that defines the VM's name.</span></span> <span data-ttu-id="d669d-185">本示例使用内置`variables`函数进行读取。</span><span class="sxs-lookup"><span data-stu-id="d669d-185">This example uses the built-in `variables` function to read it.</span></span>

## <a name="summary"></a><span data-ttu-id="d669d-186">摘要</span><span class="sxs-lookup"><span data-stu-id="d669d-186">Summary</span></span>

<span data-ttu-id="d669d-187">现在, 你已拥有在模板中定义自定义脚本扩展资源所需的一切。</span><span class="sxs-lookup"><span data-stu-id="d669d-187">You now have everything you need to define the Custom Script Extension resource in your template.</span></span> <span data-ttu-id="d669d-188">在下一部分中, 你将扩展模板以使用它。</span><span class="sxs-lookup"><span data-stu-id="d669d-188">In the next part, you'll extend your template to use it.</span></span>
