<span data-ttu-id="3efa1-101">在这里, 你将部署在上一部分中研究过的快速入门模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-101">Here you'll deploy the Quickstart template you explored in the previous part.</span></span> <span data-ttu-id="3efa1-102">快速入门模板将显示基本的虚拟机配置。</span><span class="sxs-lookup"><span data-stu-id="3efa1-102">The Quickstart template brings up a basic virtual machine configuration.</span></span>

<span data-ttu-id="3efa1-103">在执行此操作之前, 让我们先简单回顾一下部署过程。</span><span class="sxs-lookup"><span data-stu-id="3efa1-103">Before you do that, let's briefly review the deployment process.</span></span>

[!include[](../../../../includes/azure-sandbox-activate.md)]

## <a name="how-do-i-deploy-a-resource-manager-template"></a><span data-ttu-id="3efa1-104">如何部署资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="3efa1-104">How do I deploy a Resource Manager template?</span></span>

<span data-ttu-id="3efa1-105">您可以使用自动化脚本工具 (例如 azure CLI、azure PowerShell) 甚至 azure REST api 和喜欢的编程语言从模板部署资源。</span><span class="sxs-lookup"><span data-stu-id="3efa1-105">You can use automation scripting tools such as the Azure CLI, Azure PowerShell, or even the Azure REST APIs with your favorite programming language to deploy resources from templates.</span></span> <span data-ttu-id="3efa1-106">您还可以通过 visual studio、visual studio Code 和 Azure 门户部署你的模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-106">You can also deploy your templates through Visual Studio, Visual Studio Code, and the Azure portal.</span></span> <span data-ttu-id="3efa1-107">很快, 你将使用云命令行管理程序中的 Azure CLI 部署资源管理器模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-107">Shortly, you'll deploy a Resource Manager template using the Azure CLI from Cloud Shell.</span></span>

### <a name="verifying-a-template"></a><span data-ttu-id="3efa1-108">验证模板</span><span class="sxs-lookup"><span data-stu-id="3efa1-108">Verifying a template</span></span>

<span data-ttu-id="3efa1-109">在运行模板之前, 您可能需要先验证它。</span><span class="sxs-lookup"><span data-stu-id="3efa1-109">Before you run your template, you might want to verify it first.</span></span>

<span data-ttu-id="3efa1-110">最好的第一步是使用_linter_处理模板, 这是一种验证模板的 JSON 语法是否正确的工具。</span><span class="sxs-lookup"><span data-stu-id="3efa1-110">A good first step is to process your template with a _linter_, a tool that verifies that the JSON syntax of your template is correct.</span></span> <span data-ttu-id="3efa1-111">您可以找到在命令行、浏览器或您喜爱的代码编辑器中运行的 JSON linting 工具。</span><span class="sxs-lookup"><span data-stu-id="3efa1-111">You can find JSON linting tools that run on the command line, in a browser, or in your favorite code editor.</span></span>

> [!TIP]
> <span data-ttu-id="3efa1-112">Visual Studio Code 提供了许多[内置功能](https://code.visualstudio.com/docs/languages/json?azure-portal=true), 使您可以更轻松地使用 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="3efa1-112">Visual Studio Code provides many [built-in features](https://code.visualstudio.com/docs/languages/json?azure-portal=true) that make it easier to work with JSON files.</span></span> <span data-ttu-id="3efa1-113">你的常用编辑器可能会提供类似的内置功能或插件。</span><span class="sxs-lookup"><span data-stu-id="3efa1-113">Your favorite editor may provide similar built-in features or plugins.</span></span>

<span data-ttu-id="3efa1-114">下一步是将模板可视化。</span><span class="sxs-lookup"><span data-stu-id="3efa1-114">The next step might be to visualize your template.</span></span> <span data-ttu-id="3efa1-115">通过[Azure 资源管理器可视化工具](http://armviz.io?azure-portal=true), 您可以上传资源管理器模板, 并以图形方式查看您的资源与其他项之间的关系。</span><span class="sxs-lookup"><span data-stu-id="3efa1-115">[Azure Resource Manager Visualizer](http://armviz.io?azure-portal=true) enables you to upload your Resource Manager template and graphically see how your resources relate to one another.</span></span> <span data-ttu-id="3efa1-116">您可以检查此可视化效果, 以验证是否正确设置了部署并满足您的要求。</span><span class="sxs-lookup"><span data-stu-id="3efa1-116">You can inspect this visualization to verify that the deployment is set up correctly and meets your requirements.</span></span>

<span data-ttu-id="3efa1-117">最后, 您可以从 azure CLI 或 azure PowerShell 执行测试部署。</span><span class="sxs-lookup"><span data-stu-id="3efa1-117">Finally, you can perform a test deployment from the Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="3efa1-118">测试部署不会创建任何资源, 但它会为您提供有关部署运行时所发生情况的反馈。</span><span class="sxs-lookup"><span data-stu-id="3efa1-118">A test deployment doesn't create any resources, but it provides you with feedback on what would happen when the deployment runs.</span></span> <span data-ttu-id="3efa1-119">你将很快执行测试部署, 以了解操作过程。</span><span class="sxs-lookup"><span data-stu-id="3efa1-119">You'll perform a test deployment shortly to see the process in action.</span></span>

## <a name="creating-resources-in-azure"></a><span data-ttu-id="3efa1-120">在 Azure 中创建资源</span><span class="sxs-lookup"><span data-stu-id="3efa1-120">Creating resources in Azure</span></span>

<span data-ttu-id="3efa1-121">通常, 我们要做的第一件事是创建一个_资源组_来保留我们需要创建的所有内容。</span><span class="sxs-lookup"><span data-stu-id="3efa1-121">Normally, the first thing we'd do is to create a _resource group_ to hold all the things that we need to create.</span></span> <span data-ttu-id="3efa1-122">这使我们能够管理所有虚拟机、磁盘、网络接口以及构成作为一个整体的解决方案的其他元素。</span><span class="sxs-lookup"><span data-stu-id="3efa1-122">This allows us to administer all the VMs, disks, network interfaces, and other elements that make up our solution as a unit.</span></span> <span data-ttu-id="3efa1-123">我们可以使用 Azure CLI 创建包含`az group create`命令的资源组。</span><span class="sxs-lookup"><span data-stu-id="3efa1-123">We can use the Azure CLI to create a resource group with the `az group create` command.</span></span> <span data-ttu-id="3efa1-124">`--name`在我们的订阅中让其具有唯一名称, 并`--location`告知 Azure 我们希望在默认情况下放置资源的世界领域。</span><span class="sxs-lookup"><span data-stu-id="3efa1-124">It takes a `--name` to give it a unique name in our subscription, and a `--location` to tell Azure what area of the world we want the resources to be located by default.</span></span>

<span data-ttu-id="3efa1-125">由于我们处于免费的 Azure 沙盒环境中, 因此您无需执行此步骤, 而是使用预创建的资源组**<rgn>[资源组名称]</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="3efa1-125">Since we are in the free Azure sandbox environment, you don't need to do this step, instead, you will use the pre-created resource group **<rgn>[Resource Group Name]</rgn>**.</span></span>

## <a name="create-template-parameters"></a><span data-ttu-id="3efa1-126">创建模板参数</span><span class="sxs-lookup"><span data-stu-id="3efa1-126">Create template parameters</span></span>

<span data-ttu-id="3efa1-127">回想一下, 资源管理器模板划分为多个部分, 其中一个是**参数**。</span><span class="sxs-lookup"><span data-stu-id="3efa1-127">Recall that a Resource Manager template is divided into sections, one of them being **Parameters**.</span></span>

<span data-ttu-id="3efa1-128">在模板的开头附近, 您会看到一个名为`parameters`的节。</span><span class="sxs-lookup"><span data-stu-id="3efa1-128">Near the start of the template, you see a section named `parameters`.</span></span> <span data-ttu-id="3efa1-129">本部分将定义这五个参数:</span><span class="sxs-lookup"><span data-stu-id="3efa1-129">This section defines these five parameters:</span></span>

* `adminUsername`
* `adminPassword`
* `dnsLabelPrefix`
* `windowsOSVersion`
* `location`

![模板的 parameters 部分的源代码, 突出显示每个参数名称](../../media/4-armviz-params-windows.png)

<span data-ttu-id="3efa1-131">这两个参数&ndash; `windowsOSVersion`中`location` &ndash;的两个, 它们都具有默认值。</span><span class="sxs-lookup"><span data-stu-id="3efa1-131">Two of these parameters &ndash; `windowsOSVersion` and `location` &ndash; have default values.</span></span> <span data-ttu-id="3efa1-132">的默认值`windowsOSVersion`为 "2016-Datacenter", 的默认`location`值为父资源组的位置。</span><span class="sxs-lookup"><span data-stu-id="3efa1-132">The default value for `windowsOSVersion` is "2016-Datacenter" and the default value for `location` is the parent resource group's location.</span></span>

<span data-ttu-id="3efa1-133">让我们将这些参数保留为其默认值。</span><span class="sxs-lookup"><span data-stu-id="3efa1-133">Let's keep these parameters at their default values.</span></span> <span data-ttu-id="3efa1-134">对于其余的三个参数, 您有两个选项:</span><span class="sxs-lookup"><span data-stu-id="3efa1-134">For the remaining three parameters, you have two options:</span></span>

1. <span data-ttu-id="3efa1-135">提供 JSON 文件中的值。</span><span class="sxs-lookup"><span data-stu-id="3efa1-135">Provide the values in a JSON file.</span></span>
1. <span data-ttu-id="3efa1-136">提供值作为命令行参数。</span><span class="sxs-lookup"><span data-stu-id="3efa1-136">Provide the values as command-line arguments.</span></span>

<span data-ttu-id="3efa1-137">为便于学习, 您将提供值作为命令行参数。</span><span class="sxs-lookup"><span data-stu-id="3efa1-137">For learning purposes, here you'll provide the values as command-line arguments.</span></span> <span data-ttu-id="3efa1-138">若要使模板易于部署, 首先需要将这些值存储为 Bash 变量。</span><span class="sxs-lookup"><span data-stu-id="3efa1-138">To make the template easy to deploy, you'll start by storing these values as Bash variables.</span></span>

1. <span data-ttu-id="3efa1-139">从云命令行管理程序创建用户名。</span><span class="sxs-lookup"><span data-stu-id="3efa1-139">From Cloud Shell, create a username.</span></span> <span data-ttu-id="3efa1-140">对于此示例, 我们使用**azureuser**。</span><span class="sxs-lookup"><span data-stu-id="3efa1-140">For this example, let's use **azureuser**.</span></span>

    ```bash
    USERNAME=azureuser
    ```

1. <span data-ttu-id="3efa1-141">运行**openssl**实用工具以生成随机密码。</span><span class="sxs-lookup"><span data-stu-id="3efa1-141">Run the **openssl** utility to generate a random password.</span></span>

    ```bash
    PASSWORD=$(openssl rand -base64 32)
    ```

    <span data-ttu-id="3efa1-142">生成随机密码的方式有很多种。</span><span class="sxs-lookup"><span data-stu-id="3efa1-142">There are many ways generate random passwords.</span></span> <span data-ttu-id="3efa1-143">您选择的方法取决于您的工作流和要求。</span><span class="sxs-lookup"><span data-stu-id="3efa1-143">The method you choose depends on your workflow and requirements.</span></span> <span data-ttu-id="3efa1-144">此方法使用**openssl**实用工具生成32随机字节, 而 base64 则对输出进行编码。</span><span class="sxs-lookup"><span data-stu-id="3efa1-144">This method uses the **openssl** utility to generate 32 random bytes and base64 encode the output.</span></span> <span data-ttu-id="3efa1-145">Base64 编码可确保结果仅包含可打印字符。</span><span class="sxs-lookup"><span data-stu-id="3efa1-145">Base64 encoding ensures that the result contains only printable characters.</span></span>

1. <span data-ttu-id="3efa1-146">生成唯一的 DNS 标签前缀。</span><span class="sxs-lookup"><span data-stu-id="3efa1-146">Generate a unique DNS label prefix.</span></span>

    ```bash
    DNS_LABEL_PREFIX=mydeployment-$RANDOM
    ```

    <span data-ttu-id="3efa1-147">DNS 标签前缀必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3efa1-147">The DNS label prefix must be unique.</span></span> <span data-ttu-id="3efa1-148">DNS 标签前缀以 "mydeployment" 开头, 后跟一个随机数字。</span><span class="sxs-lookup"><span data-stu-id="3efa1-148">The DNS label prefix begins with "mydeployment" followed by a random number.</span></span> <span data-ttu-id="3efa1-149">`$RANDOM`是一个 Bash 函数, 它生成随机正整数。</span><span class="sxs-lookup"><span data-stu-id="3efa1-149">`$RANDOM` is a Bash function that generates a random positive whole number.</span></span>

    <span data-ttu-id="3efa1-150">在实践中, 您将选择符合要求的 DNS 标签前缀。</span><span class="sxs-lookup"><span data-stu-id="3efa1-150">In practice, you would choose a DNS label prefix that fits your requirements.</span></span>

## <a name="validate-and-launch-the-template"></a><span data-ttu-id="3efa1-151">验证并启动模板</span><span class="sxs-lookup"><span data-stu-id="3efa1-151">Validate and launch the template</span></span>

<span data-ttu-id="3efa1-152">参数准备就绪后, 您就拥有启动模板所需的一切。</span><span class="sxs-lookup"><span data-stu-id="3efa1-152">With your parameters in place, you have everything you need to launch the template.</span></span>

<span data-ttu-id="3efa1-153">作为最后的验证步骤, 你将首先验证模板语法是否正确。</span><span class="sxs-lookup"><span data-stu-id="3efa1-153">As a final verification step, you'll begin by validating that the template is syntactically correct.</span></span>

1. <span data-ttu-id="3efa1-154">在云命令行管理`az group deployment validate`程序中, 运行以验证模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-154">From Cloud Shell, run `az group deployment validate` to validate the template.</span></span>

    ```azurecli
    az group deployment validate \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json" \
      --parameters adminUsername=$USERNAME \
      --parameters adminPassword=$PASSWORD \
      --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
    ```

    <span data-ttu-id="3efa1-155">`--template-uri`参数指向 GitHub 上的模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-155">The `--template-uri` argument points to the template on GitHub.</span></span> <span data-ttu-id="3efa1-156">模板的文件名为**azuredeploy.json**。</span><span class="sxs-lookup"><span data-stu-id="3efa1-156">The template's filename is **azuredeploy.json**.</span></span> <span data-ttu-id="3efa1-157">稍后, 您将了解如何在本地文件系统上验证和运行模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-157">Later, you'll see how to validate and run a template on your local filesystem.</span></span>

    <span data-ttu-id="3efa1-158">您看到一个较大的 JSON 块作为输出, 这会告知您模板已通过验证。</span><span class="sxs-lookup"><span data-stu-id="3efa1-158">You see a large JSON block as output, which tells you that the template passed validation.</span></span>

    <span data-ttu-id="3efa1-159">Azure 资源管理器填写模板参数, 并检查模板是否会在你的订阅中成功运行。</span><span class="sxs-lookup"><span data-stu-id="3efa1-159">Azure Resource Manager fills in the template parameters and checks whether the template would successfully run in your subscription.</span></span>

    <span data-ttu-id="3efa1-160">如果验证失败, 您将在输出中看到失败的详细说明。</span><span class="sxs-lookup"><span data-stu-id="3efa1-160">If validation failed, you would see a detailed description of the failure in the output.</span></span>

1. <span data-ttu-id="3efa1-161">运行`az group deployment create`以部署模板。</span><span class="sxs-lookup"><span data-stu-id="3efa1-161">Run `az group deployment create` to deploy the template.</span></span>

    ```azurecli
    az group deployment create \
      --name MyDeployment \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json" \
      --parameters adminUsername=$USERNAME \
      --parameters adminPassword=$PASSWORD \
      --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
    ```

    <span data-ttu-id="3efa1-162">此命令与前面的命令类似, 但还包含`--name`用于为您的部署指定名称的参数。</span><span class="sxs-lookup"><span data-stu-id="3efa1-162">This command resembles the previous command, but also includes the `--name` argument to give your deployment a name.</span></span>

    <span data-ttu-id="3efa1-163">此命令需要4-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="3efa1-163">This command takes 4-5 minutes to complete.</span></span> <span data-ttu-id="3efa1-164">在您等待时, 现在我们来[仔细看看此模板的源代码](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-simple-windows/azuredeploy.json?azure-portal=true)是个好的时间。</span><span class="sxs-lookup"><span data-stu-id="3efa1-164">While you wait, now's a great time to take a [closer look at the source code](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-simple-windows/azuredeploy.json?azure-portal=true) for this template.</span></span> <span data-ttu-id="3efa1-165">请记住, 在阅读现有模板和创建自己的模板时, 资源管理器模板的内容将变得越来越熟悉。</span><span class="sxs-lookup"><span data-stu-id="3efa1-165">Remember, the contents of a Resource Manager template will become more familiar to you as you read existing templates and create your own.</span></span>

    <span data-ttu-id="3efa1-166">部署完成后, 您会看到另一个较大的 JSON 块作为描述部署的输出。</span><span class="sxs-lookup"><span data-stu-id="3efa1-166">When the deployment completes, you see another large JSON block as output that describes the deployment.</span></span>

## <a name="verify-the-deployment"></a><span data-ttu-id="3efa1-167">验证部署</span><span class="sxs-lookup"><span data-stu-id="3efa1-167">Verify the deployment</span></span>

<span data-ttu-id="3efa1-168">部署成功。</span><span class="sxs-lookup"><span data-stu-id="3efa1-168">The deployment succeeded.</span></span> <span data-ttu-id="3efa1-169">但让我们仅运行几个命令来验证。</span><span class="sxs-lookup"><span data-stu-id="3efa1-169">But let's run a few commands just to verify.</span></span>

1. <span data-ttu-id="3efa1-170">运行`az group deployment show`以验证部署。</span><span class="sxs-lookup"><span data-stu-id="3efa1-170">Run `az group deployment show` to verify the deployment.</span></span>

    ```azurecli
    az group deployment show \
      --name MyDeployment \
      --resource-group <rgn>[sandbox resource group name]</rgn>
    ```

    <span data-ttu-id="3efa1-171">你将看到与之前相同的 JSON 块。</span><span class="sxs-lookup"><span data-stu-id="3efa1-171">You see the same JSON block as you did previously.</span></span> <span data-ttu-id="3efa1-172">如果你需要有关部署的这些详细信息, 你可以稍后再运行此命令。</span><span class="sxs-lookup"><span data-stu-id="3efa1-172">You can run this command later if you ever need these details about the deployment.</span></span> <span data-ttu-id="3efa1-173">输出的结构为 JSON, 以便更轻松地将其加入其他可用于跟踪部署和云使用的工具。</span><span class="sxs-lookup"><span data-stu-id="3efa1-173">The output is structured as JSON to make it easier to feed into other tools you might use to track your deployments and cloud usage.</span></span>

1. <span data-ttu-id="3efa1-174">运行`az vm list`以查看哪些虚拟机正在运行。</span><span class="sxs-lookup"><span data-stu-id="3efa1-174">Run `az vm list` to see which VMs are running.</span></span>

    ```azurecli
    az vm list \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --output table
    ```

    <span data-ttu-id="3efa1-175">您的输出与此类似。</span><span class="sxs-lookup"><span data-stu-id="3efa1-175">Your output resembles this.</span></span> <span data-ttu-id="3efa1-176">您的区域显示在 "**位置**" 列下。</span><span class="sxs-lookup"><span data-stu-id="3efa1-176">Your region is shown under the **Location** column.</span></span>

    ```bash
    Name         ResourceGroup                         Location        Zones
    -----------  ------------------------------------  --------------  -------
    SimpleWinVM  <rgn>[sandbox resource group name]</rgn>  southcentralus
    ```

    <span data-ttu-id="3efa1-177">请记住, 模板将名称命名为 VM "SimpleWinVM"。</span><span class="sxs-lookup"><span data-stu-id="3efa1-177">Recall that the template names the VM "SimpleWinVM".</span></span> <span data-ttu-id="3efa1-178">在这里, 你会看到你的资源组中存在此 VM。</span><span class="sxs-lookup"><span data-stu-id="3efa1-178">Here you see that this VM exists in your resource group.</span></span>