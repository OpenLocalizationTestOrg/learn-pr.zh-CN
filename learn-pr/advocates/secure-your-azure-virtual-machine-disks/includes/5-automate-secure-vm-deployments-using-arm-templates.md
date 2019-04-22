<span data-ttu-id="44ef7-101">假设您的公司将多台服务器部署为其云转换的一部分。</span><span class="sxs-lookup"><span data-stu-id="44ef7-101">Suppose your company is deploying several servers as part of their cloud transition.</span></span> <span data-ttu-id="44ef7-102">在部署过程中, 必须对 VM 磁盘进行加密, 因此在磁盘易受攻击时没有任何时间。</span><span class="sxs-lookup"><span data-stu-id="44ef7-102">VM disks must be encrypted during the deployment, so there's no time when the disks are vulnerable.</span></span> <span data-ttu-id="44ef7-103">您希望自动执行此过程, 并且必须修改 Azure 资源管理器模板以自动启用加密。</span><span class="sxs-lookup"><span data-stu-id="44ef7-103">You want to automate this process, and have to modify the Azure Resource Manager templates to automatically enable encryption.</span></span>

<span data-ttu-id="44ef7-104">在这里, 我们将介绍如何使用 Azure 资源管理器模板自动为新的 Windows 虚拟机启用加密。</span><span class="sxs-lookup"><span data-stu-id="44ef7-104">Here, we'll look at how to use an Azure Resource Manager template to automatically enable encryption for new Windows VMs.</span></span>

## <a name="what-are-azure-resource-manager-templates"></a><span data-ttu-id="44ef7-105">什么是 Azure 资源管理器模板？</span><span class="sxs-lookup"><span data-stu-id="44ef7-105">What are Azure Resource Manager templates?</span></span>

<span data-ttu-id="44ef7-106">资源管理器模板是用于定义要部署到 Azure 的一组资源的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="44ef7-106">Resource Manager templates are JSON files used to define a set of resources to deploy to Azure.</span></span> <span data-ttu-id="44ef7-107">你可以从头开始编写它们, 对于某些 Azure 资源 (包括 vm), 你可以使用 azure 门户生成这些资源。</span><span class="sxs-lookup"><span data-stu-id="44ef7-107">You can write them from scratch, and for some Azure resources, including VMs, you can use the Azure portal to generate them.</span></span> <span data-ttu-id="44ef7-108">您需要完成手动 VM 部署所需的信息, 但不是将 VM 部署到 Azure, 而是保存该模板。</span><span class="sxs-lookup"><span data-stu-id="44ef7-108">You'll need to complete the required information for a manual VM deployment, but instead of deploying the VM to Azure, you save the template.</span></span> <span data-ttu-id="44ef7-109">然后, 您可以_重用_该模板来创建该特定的 VM 配置。</span><span class="sxs-lookup"><span data-stu-id="44ef7-109">You can then _reuse_ the template to create that specific VM configuration.</span></span>

<span data-ttu-id="44ef7-110">[文档中提供了一些示例模板](https://azure.microsoft.com/resources/templates), 可自动执行各种管理任务。</span><span class="sxs-lookup"><span data-stu-id="44ef7-110">There are [example templates available in docs](https://azure.microsoft.com/resources/templates) to automate all sorts of administrative tasks.</span></span> <span data-ttu-id="44ef7-111">事实上, 我们可以使用其中一个模板来加密我们刚才手动执行的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="44ef7-111">In fact, we could have used one of these templates to encrypt our VM that we just did manually!</span></span>

![显示 Azure 模板的屏幕截图](../media/5-browse-templates.png)

## <a name="using-github-templates"></a><span data-ttu-id="44ef7-113">使用 GitHub 模板</span><span class="sxs-lookup"><span data-stu-id="44ef7-113">Using GitHub templates</span></span>

<span data-ttu-id="44ef7-114">实际模板源存储在 GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="44ef7-114">The actual template source is stored in GitHub.</span></span> <span data-ttu-id="44ef7-115">您可以浏览 GitHub 中的模板并从页面向 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="44ef7-115">You can browse to a template in GitHub and deploy right to Azure from the page.</span></span>

![在突出显示了 "部署到 Azure" 按钮时显示 GitHub 模板的屏幕截图](../media/5-deploy-from-github.png)

<span data-ttu-id="44ef7-117">部署模板后, Azure 将显示所需输入域的列表。</span><span class="sxs-lookup"><span data-stu-id="44ef7-117">When the template is deployed, Azure will display a list of required input fields.</span></span>

![显示 Azure 门户中的模板的屏幕截图](../media/5-fill-in-template.png)

<span data-ttu-id="44ef7-119">然后, 您可以执行模板来创建、修改或删除资源。</span><span class="sxs-lookup"><span data-stu-id="44ef7-119">You can then execute the template to create, modify, or remove resources.</span></span>

### <a name="running-templates-in-the-azure-portal"></a><span data-ttu-id="44ef7-120">在 Azure 门户中运行模板</span><span class="sxs-lookup"><span data-stu-id="44ef7-120">Running templates in the Azure portal</span></span>

<span data-ttu-id="44ef7-121">如果您已经知道要使用的模板, 或者您已在 Azure 帐户中保存了模板, 则可以使用**创建资源** > **模板部署**资源在门户中查找和运行定义的模板。</span><span class="sxs-lookup"><span data-stu-id="44ef7-121">If you already know the template you want to use, or you have saved templates in your Azure account, you can use the **Create a resource** > **Template Deployment** resource to locate and run defined templates in the portal.</span></span> <span data-ttu-id="44ef7-122">您可以按名称搜索模板, 编辑模板以更改参数或行为, 并在 GUI 中执行模板权限。</span><span class="sxs-lookup"><span data-stu-id="44ef7-122">You can search through templates by name, edit a template to change the parameters or behavior, and execute the template right from the GUI.</span></span>

### <a name="running-templates-from-the-command-line"></a><span data-ttu-id="44ef7-123">从命令行运行模板</span><span class="sxs-lookup"><span data-stu-id="44ef7-123">Running templates from the command line</span></span>

<span data-ttu-id="44ef7-124">给定模板的 URL, 您可以使用 Azure PowerShell 执行它。</span><span class="sxs-lookup"><span data-stu-id="44ef7-124">Given a URL to a template, you can execute it with Azure PowerShell.</span></span> <span data-ttu-id="44ef7-125">例如, 我们可以使用以下 PowerShell 命令运行磁盘加密模板:</span><span class="sxs-lookup"><span data-stu-id="44ef7-125">For example, we could run the disk encryption template with the following PowerShell command:</span></span>

```powershell
New-AzResourceGroupDeployment `
    -Name encrypt-disk `
    -ResourceGroupName <resource-group-name> `
    -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

<span data-ttu-id="44ef7-126">或者, 如果您更喜欢使用该`group deployment create`命令, 也可以使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="44ef7-126">Or, if you prefer the Azure CLI, with the `group deployment create` command.</span></span>

```azurecli
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> \ 
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

