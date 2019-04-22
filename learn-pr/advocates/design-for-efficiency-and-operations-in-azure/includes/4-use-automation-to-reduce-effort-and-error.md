<span data-ttu-id="36823-101">管理任何类型的工作负荷的基础结构涉及配置任务。</span><span class="sxs-lookup"><span data-stu-id="36823-101">Managing the infrastructure of any type of workload involves configuration tasks.</span></span> <span data-ttu-id="36823-102">可以手动执行此配置, 但手动步骤可能会非常耗费人力、易出错且效率低下。</span><span class="sxs-lookup"><span data-stu-id="36823-102">This configuration can be done manually, but manual steps can be labor-intensive, error prone, and inefficient.</span></span> <span data-ttu-id="36823-103">如果分配给需要在 Azure 上部署数百个系统的项目, 该怎么办？</span><span class="sxs-lookup"><span data-stu-id="36823-103">What if you are assigned to lead a project that required the deployment of hundreds of systems on Azure?</span></span> <span data-ttu-id="36823-104">如何构建和配置这些资源？</span><span class="sxs-lookup"><span data-stu-id="36823-104">How would you build and configure these resources?</span></span> <span data-ttu-id="36823-105">此操作需要多长时间？</span><span class="sxs-lookup"><span data-stu-id="36823-105">How long would this take?</span></span> <span data-ttu-id="36823-106">您能否确保每个系统都已正确配置, 无差异？</span><span class="sxs-lookup"><span data-stu-id="36823-106">Could you ensure that each system was configured properly, with no variance between them?</span></span> <span data-ttu-id="36823-107">通过在体系结构设计中使用自动化功能, 您可以解决这些难题。</span><span class="sxs-lookup"><span data-stu-id="36823-107">By using automation in your architecture design, you can work past these challenges.</span></span> <span data-ttu-id="36823-108">让我们看一下你可以在 Azure 上实现自动化的一些方法。</span><span class="sxs-lookup"><span data-stu-id="36823-108">Let's take a look at some of the ways you can automate on Azure.</span></span>

## <a name="infrastructure-as-code"></a><span data-ttu-id="36823-109">作为代码的基础结构</span><span class="sxs-lookup"><span data-stu-id="36823-109">Infrastructure as code</span></span>

<span data-ttu-id="36823-110">作为代码的基础结构是一个描述性模型中的基础结构 (网络、虚拟机、负载平衡器和连接拓扑) 的管理, 使用的版本控制系统与用于源代码的版本类似。</span><span class="sxs-lookup"><span data-stu-id="36823-110">Infrastructure as code is the management of infrastructure (networks, virtual machines, load balancers, and connection topology) in a descriptive model, using a versioning system similar to what is used for source code.</span></span> <span data-ttu-id="36823-111">与相同的源代码生成相同二进制文件的原则一样, IaC 模型会在每次应用它时生成相同的环境。</span><span class="sxs-lookup"><span data-stu-id="36823-111">Like the principle that the same source code generates the same binary, an IaC model generates the same environment every time it is applied.</span></span> <span data-ttu-id="36823-112">IaC 是一项关键 DevOps 实践, 通常与连续交付一起使用。</span><span class="sxs-lookup"><span data-stu-id="36823-112">IaC is a key DevOps practice and is often used in conjunction with continuous delivery.</span></span>

<span data-ttu-id="36823-113">作为代码发展的基础结构, 以解决环境偏差问题。</span><span class="sxs-lookup"><span data-stu-id="36823-113">Infrastructure as code evolved to solve the problem of environment drift.</span></span> <span data-ttu-id="36823-114">如果没有 IaC, 团队必须维护各个部署环境的设置。</span><span class="sxs-lookup"><span data-stu-id="36823-114">Without IaC, teams must maintain the settings of individual deployment environments.</span></span> <span data-ttu-id="36823-115">随着时间的推移, 每个环境将成为雪花, 即不能自动重现的唯一配置。</span><span class="sxs-lookup"><span data-stu-id="36823-115">Over time, each environment becomes a snowflake, that is, a unique configuration that cannot be reproduced automatically.</span></span> <span data-ttu-id="36823-116">环境之间的不一致会导致部署过程中出现问题。</span><span class="sxs-lookup"><span data-stu-id="36823-116">Inconsistency among environments leads to issues during deployments.</span></span> <span data-ttu-id="36823-117">通过 snowflakes, 基础结构的管理和维护涉及难以跟踪和对错误进行贡献的手动过程。</span><span class="sxs-lookup"><span data-stu-id="36823-117">With snowflakes, administration and maintenance of infrastructure involves manual processes which were hard to track and contributed to errors.</span></span>

<span data-ttu-id="36823-118">自动化服务和基础结构的部署时, 可以采用两种不同的方法: 命令式和声明性。</span><span class="sxs-lookup"><span data-stu-id="36823-118">When automating the deployment of services and infrastructure, there are two different approaches you can take: imperative and declarative.</span></span> <span data-ttu-id="36823-119">在命令性方法中, 显式声明为生成要查找的结果所执行的命令。</span><span class="sxs-lookup"><span data-stu-id="36823-119">In an imperative approach, you explicitly state the commands that are executed to produce the outcome you are looking for.</span></span> <span data-ttu-id="36823-120">使用声明性方法, 可以指定您希望结果的结果, 而不是指定您希望的结果的完成方式。</span><span class="sxs-lookup"><span data-stu-id="36823-120">With a declarative approach, you specify what you want the outcome to be instead of specifying how you want it done.</span></span> <span data-ttu-id="36823-121">这两种方法都很有用, 因此没有任何错误的选择。</span><span class="sxs-lookup"><span data-stu-id="36823-121">Both approaches are valuable, so there's no wrong choice.</span></span> <span data-ttu-id="36823-122">在 Azure 上, 这些不同的方法看起来是什么, 以及如何使用它们呢？</span><span class="sxs-lookup"><span data-stu-id="36823-122">What do these different approaches look like on Azure, and how do you use them?</span></span>

### <a name="imperative-automation"></a><span data-ttu-id="36823-123">命令性自动化</span><span class="sxs-lookup"><span data-stu-id="36823-123">Imperative automation</span></span>

<span data-ttu-id="36823-124">让我们从命令性自动化开始。</span><span class="sxs-lookup"><span data-stu-id="36823-124">Let's start with imperative automation.</span></span> <span data-ttu-id="36823-125">使用命令性自动化时, 我们将指定_如何_完成操作。</span><span class="sxs-lookup"><span data-stu-id="36823-125">With imperative automation, we're specifying _how_ things are to be done.</span></span> <span data-ttu-id="36823-126">这通常通过脚本语言或 SDK 以编程方式完成。</span><span class="sxs-lookup"><span data-stu-id="36823-126">This is typically done programmatically through a scripting language or SDK.</span></span> <span data-ttu-id="36823-127">对于 azure 资源, 我们可以使用 azure CLI 或 azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="36823-127">For Azure resources, we could use the Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="36823-128">我们来看一个使用 Azure CLI 创建存储帐户的示例。</span><span class="sxs-lookup"><span data-stu-id="36823-128">Let's take a look at an example that uses the Azure CLI to create a storage account.</span></span>

```azure-cli
az group create --name storage-resource-group \
        --location eastus

az storage account create --name mystorageaccount \
        --resource-group storage-resource-group \
        --kind BlobStorage \
        --access-tier hot
```

<span data-ttu-id="36823-129">在此示例中, 我们要指定如何创建这些资源。</span><span class="sxs-lookup"><span data-stu-id="36823-129">In this example, we're specifying how to create these resources.</span></span> <span data-ttu-id="36823-130">执行命令以创建资源组。</span><span class="sxs-lookup"><span data-stu-id="36823-130">Execute a command to create a resource group.</span></span> <span data-ttu-id="36823-131">执行另一个命令来创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="36823-131">Execute another command to create a storage account.</span></span> <span data-ttu-id="36823-132">我们明确告诉 Azure 要运行哪些命令来生成所需的输出。</span><span class="sxs-lookup"><span data-stu-id="36823-132">We're explicitly telling Azure what commands to run to produce the output we need.</span></span>

<span data-ttu-id="36823-133">通过此方法, 我们能够完全自动化基础结构。</span><span class="sxs-lookup"><span data-stu-id="36823-133">With this approach, we're able to fully automate our infrastructure.</span></span> <span data-ttu-id="36823-134">我们可以提供输入和输出的区域, 并可确保每次执行相同的命令。</span><span class="sxs-lookup"><span data-stu-id="36823-134">We can provide areas for input and output, and can ensure that the same commands are executed every time.</span></span> <span data-ttu-id="36823-135">通过自动化我们的资源, 我们已将手动步骤从过程中移出, 使资源管理的工作效率更高。</span><span class="sxs-lookup"><span data-stu-id="36823-135">By automating our resources, we've taken the manual steps out of the process, making resource administration operationally more efficient.</span></span> <span data-ttu-id="36823-136">不过, 这种方法也有一些弊端。</span><span class="sxs-lookup"><span data-stu-id="36823-136">There are some downsides to this approach though.</span></span> <span data-ttu-id="36823-137">在体系结构变得越来越复杂的情况中, 创建资源的脚本可能会迅速变得复杂。</span><span class="sxs-lookup"><span data-stu-id="36823-137">Scripts to create resources can quickly become complex as the architecture becomes more complex.</span></span> <span data-ttu-id="36823-138">可能需要添加错误处理和输入验证, 以确保完全执行。</span><span class="sxs-lookup"><span data-stu-id="36823-138">Error handling and input validation may need to be added to ensure full execution.</span></span> <span data-ttu-id="36823-139">命令可能会更改, 需要持续的脚本维护。</span><span class="sxs-lookup"><span data-stu-id="36823-139">Commands may change, requiring ongoing maintenance of the scripts.</span></span>

### <a name="declarative-automation"></a><span data-ttu-id="36823-140">声明性自动化</span><span class="sxs-lookup"><span data-stu-id="36823-140">Declarative automation</span></span>

<span data-ttu-id="36823-141">通过声明性自动化, 我们将__ 指定我们希望得到的结果, 并提供有关如何对正在使用的系统执行的详细信息。</span><span class="sxs-lookup"><span data-stu-id="36823-141">With declarative automation, we're specifying _what_ we want our result to be, leaving the details of how it's done to the system we're using.</span></span> <span data-ttu-id="36823-142">在 azure 上, 声明性自动化通过使用 Azure 资源管理器模板来完成。</span><span class="sxs-lookup"><span data-stu-id="36823-142">On Azure, declarative automation is done through the use of Azure Resource Manager templates.</span></span>

<span data-ttu-id="36823-143">资源管理器模板是用于指定要创建的内容的 JSON 结构化文件。</span><span class="sxs-lookup"><span data-stu-id="36823-143">Resource Manager templates are JSON-structured files that specify what we want created.</span></span> <span data-ttu-id="36823-144">在下面的示例中, 我们正在告诉 Azure 创建包含我们指定的名称和属性的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="36823-144">In the example below, we're telling Azure to create a storage account with the names and properties that we specify.</span></span> <span data-ttu-id="36823-145">为创建此存储帐户而执行的实际步骤将保留给 Azure。</span><span class="sxs-lookup"><span data-stu-id="36823-145">The actual steps that are executed to create this storage account are left to Azure.</span></span> <span data-ttu-id="36823-146">模板包含四个部分: 参数、变量、资源和输出。</span><span class="sxs-lookup"><span data-stu-id="36823-146">Templates have four sections: parameters, variables, resources, and outputs.</span></span> <span data-ttu-id="36823-147">参数处理要在模板中使用的输入。</span><span class="sxs-lookup"><span data-stu-id="36823-147">Parameters handle input to be used within the template.</span></span> <span data-ttu-id="36823-148">变量提供了一种存储用于整个模板的值的方法。</span><span class="sxs-lookup"><span data-stu-id="36823-148">Variables provide a way to store values for use throughout the template.</span></span> <span data-ttu-id="36823-149">资源是要创建的内容, 而产出是向已创建内容的用户提供详细信息的一种方式。</span><span class="sxs-lookup"><span data-stu-id="36823-149">Resources are the things that are being created, and outputs are a way to provide details to the user of what was created.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "name": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "accountType": {
            "type": "string",
            "defaultValue": "Standard_RAGRS"
        },
        "kind": {
            "type": "string"
        },
        "accessTier": {
            "type": "string"
        },
        "httpsTrafficOnlyEnabled": {
            "type": "bool",
            "defaultValue": true
        }
    },
    "variables": {
    },
    "resources": [
        {
            "apiVersion": "2018-02-01",
            "name": "[parameters('name')]",
            "location": "[parameters('location')]",
            "type": "Microsoft.Storage/storageAccounts",
            "sku": {
                "name": "[parameters('accountType')]"
            },
            "kind": "[parameters('kind')]",
            "properties": {
                "supportsHttpsTrafficOnly": "[parameters('httpsTrafficOnlyEnabled')]",
                "accessTier": "[parameters('accessTier')]",
                "encryption": {
                    "services": {
                        "blob": {
                            "enabled": true
                        },
                        "file": {
                            "enabled": true
                        }
                    },
                    "keySource": "Microsoft.Storage"
                }
            },
            "dependsOn": []
        }
    ],
    "outputs": {
        "storageAccountName": {
            "type": "string",
            "value": "[parameters('name')]"
        }
    }
}
```

<span data-ttu-id="36823-150">模板可用于在 Azure 上创建和操作大多数服务。</span><span class="sxs-lookup"><span data-stu-id="36823-150">Templates can be used to create and manipulate most services on Azure.</span></span> <span data-ttu-id="36823-151">它们可以存储在代码库中并受源代码管理, 并在多个环境中共享, 以确保要开发的基础结构与实际生产中的内容相匹配。</span><span class="sxs-lookup"><span data-stu-id="36823-151">They can be stored in code repositories and source controlled, and shared across environments to ensure that the infrastructure being developed against matches what's actually in production.</span></span> <span data-ttu-id="36823-152">它们是自动化部署并帮助确保一致性、消除部署错误配置并可提高运营速度的极好的方法。</span><span class="sxs-lookup"><span data-stu-id="36823-152">They are a great way to automate deployments and help ensure consistency, eliminate deployment misconfigurations, and can increase operational speed.</span></span>

<span data-ttu-id="36823-153">自动化基础结构部署是一项极好的第一步, 但在部署虚拟机时, 仍有更多的工作要做。</span><span class="sxs-lookup"><span data-stu-id="36823-153">Automating your infrastructure deployment is a great first step, but when deploying virtual machines, there's still more work to do.</span></span> <span data-ttu-id="36823-154">我们来看看几种自动化配置部署的方法。</span><span class="sxs-lookup"><span data-stu-id="36823-154">Let's take a look at a couple of approaches to automating configuration post deployment.</span></span>

## <a name="vm-customization-images-vs-post-deployment-configuration"></a><span data-ttu-id="36823-155">VM 自定义: 图像与后期部署配置</span><span class="sxs-lookup"><span data-stu-id="36823-155">VM customization: images vs. post-deployment configuration</span></span>

<span data-ttu-id="36823-156">对于许多虚拟机部署, 该作业不是在计算机运行时执行的。</span><span class="sxs-lookup"><span data-stu-id="36823-156">For many virtual machine deployments, the job isn't done when the machine is running.</span></span> <span data-ttu-id="36823-157">在 VM 实际为其预期目的提供服务之前, 可能需要进行额外的配置。</span><span class="sxs-lookup"><span data-stu-id="36823-157">It's likely there's additional configuration that's needed before the VM can actually serve its intended purpose.</span></span> <span data-ttu-id="36823-158">其他磁盘可能需要格式化, VM 可能需要加入域, 或许需要安装管理软件的代理, 并且大多数情况下, 实际工作负载也需要安装和配置。</span><span class="sxs-lookup"><span data-stu-id="36823-158">Additional disks might need formatting, the VM might need to be joined to a domain, maybe an agent for a management software needs to be installed, and most likely the actual workload requires installation and configuration as well.</span></span>

<span data-ttu-id="36823-159">有两个通用策略适用于被认为是 VM 本身配置的配置工作, 这两者都有各自的优势和缺点:</span><span class="sxs-lookup"><span data-stu-id="36823-159">There are two common strategies applied for the configuration work considered to be part the configuration of the VM itself, both of which have advantages and disadvantages:</span></span>

- <span data-ttu-id="36823-160">自定义图像</span><span class="sxs-lookup"><span data-stu-id="36823-160">Custom images</span></span>
- <span data-ttu-id="36823-161">部署后脚本</span><span class="sxs-lookup"><span data-stu-id="36823-161">Post-deployment scripting</span></span>

<span data-ttu-id="36823-162">自定义图像是通过部署虚拟机, 然后在该运行实例上配置或安装软件生成的。</span><span class="sxs-lookup"><span data-stu-id="36823-162">Custom images are generated by deploying a virtual machine and then configuring or installing software on that running instance.</span></span> <span data-ttu-id="36823-163">当一切配置正确时, 可以关闭计算机, 并从 VM 创建映像。</span><span class="sxs-lookup"><span data-stu-id="36823-163">When everything is configured correctly, the machine can be shut down, and an image is created from the VM.</span></span> <span data-ttu-id="36823-164">然后, 可以将该映像用作其他新虚拟机的基础。</span><span class="sxs-lookup"><span data-stu-id="36823-164">The image can then be used as a base for other new virtual machines.</span></span> <span data-ttu-id="36823-165">使用自定义图像可以加快部署的总时间, 就像部署了虚拟机并运行后, 不需要其他配置。</span><span class="sxs-lookup"><span data-stu-id="36823-165">Working with custom images can speed up the overall time of your deployment as once the virtual machine is deployed and running, no additional configuration would be needed.</span></span> <span data-ttu-id="36823-166">如果部署速度是一个重要因素, 则自定义图像确实值得研究。</span><span class="sxs-lookup"><span data-stu-id="36823-166">If deployment speed is an important factor, custom images are definitely worth exploring.</span></span>

<span data-ttu-id="36823-167">部署后脚本通常利用基本的基本映像, 然后依赖脚本或配置管理平台在部署 VM 之后进行配置。</span><span class="sxs-lookup"><span data-stu-id="36823-167">Post-deployment scripting typically leverages a basic base image, then relies on scripting or a configuration management platform to do configuration after the VM is deployed.</span></span> <span data-ttu-id="36823-168">可以通过 Azure 脚本扩展在 VM 上执行脚本, 或利用更强健的解决方案 (如 Azure 自动化所需的状态配置 (DSC)) 来完成部署后脚本。</span><span class="sxs-lookup"><span data-stu-id="36823-168">The post-deployment scripting could be done by executing a script on the VM through the Azure Script Extension or by leveraging a more robust solution such as Azure Automation Desired State Configuration (DSC).</span></span>

<span data-ttu-id="36823-169">每种方法都有一些需要注意的事项。</span><span class="sxs-lookup"><span data-stu-id="36823-169">Each approach has some considerations to keep in mind.</span></span> <span data-ttu-id="36823-170">使用图像时, 需要确保有一个处理图像更新、安全修补程序和图像本身的库存管理的过程。</span><span class="sxs-lookup"><span data-stu-id="36823-170">When using images, you'll need to ensure there's a process to handle image updates, security patches, and inventory management of the images themselves.</span></span> <span data-ttu-id="36823-171">通过部署后脚本, 可以扩展生成时间, 因为在生成完成之前无法将 VM 添加到实时工作负荷。</span><span class="sxs-lookup"><span data-stu-id="36823-171">With post-deployment scripting, build times can be extended since the VM can't be added to live workloads until the build is complete.</span></span> <span data-ttu-id="36823-172">这可能不是独立系统的重要问题, 但在使用自动缩放 (如虚拟机扩展集) 的服务时, 这种扩展的生成时间可能会影响您可以扩展的速度。</span><span class="sxs-lookup"><span data-stu-id="36823-172">This may not be a significant issue for standalone systems, but when using services that autoscale (such as virtual machine scale sets), this extended build time can impact how quickly you can scale.</span></span> <span data-ttu-id="36823-173">对于这两种方法, 您都需要确保解决配置偏移;随着新配置的推出, 您需要确保现有系统会相应地进行更新。</span><span class="sxs-lookup"><span data-stu-id="36823-173">With both approaches, you'll want to ensure you address configuration drift; as new configuration is rolled out, you'll need to ensure that existing systems are updated accordingly.</span></span>

<span data-ttu-id="36823-174">自动化资源部署对您的环境来说可能是一个巨大的好处。</span><span class="sxs-lookup"><span data-stu-id="36823-174">Automating resource deployment can be a massive benefit to your environment.</span></span> <span data-ttu-id="36823-175">保存的时间量和减少的错误可以将操作功能移到另一个级别。</span><span class="sxs-lookup"><span data-stu-id="36823-175">The amount of time saved, and error reduced can move your operational capabilities to another level.</span></span>

## <a name="automation-of-operational-tasks"></a><span data-ttu-id="36823-176">操作任务的自动化</span><span class="sxs-lookup"><span data-stu-id="36823-176">Automation of operational tasks</span></span>

<span data-ttu-id="36823-177">在你的解决方案正常运行后, 还可以进行自动化的日常操作活动。</span><span class="sxs-lookup"><span data-stu-id="36823-177">Once your solutions are up and running, there are ongoing operational activities that can also be automated.</span></span> <span data-ttu-id="36823-178">使用 Azure 自动化自动执行这些任务可以减少手动工作负载, 启用对计算资源的配置和更新管理, 集中共享资源 (如计划、凭据和证书), 并提供用于运行任何Azure 任务的类型。</span><span class="sxs-lookup"><span data-stu-id="36823-178">Automating these tasks with Azure Automation reduces manual workloads, enables configuration and update management of compute resources, centralizes shared resources such as schedules, credentials, and certificates, and provides a framework for running any type of Azure task.</span></span>

<span data-ttu-id="36823-179">对于 Lamna 保健工作, 这可能包括:</span><span class="sxs-lookup"><span data-stu-id="36823-179">For your Lamna Healthcare work, this might include:</span></span>

- <span data-ttu-id="36823-180">定期搜索孤立磁盘。</span><span class="sxs-lookup"><span data-stu-id="36823-180">Periodically searching for orphaned disks.</span></span>
- <span data-ttu-id="36823-181">在 vm 上安装最新的安全修补程序。</span><span class="sxs-lookup"><span data-stu-id="36823-181">Installing the latest security patches on VMs.</span></span>
- <span data-ttu-id="36823-182">在非工作时间搜索和关闭虚拟机。</span><span class="sxs-lookup"><span data-stu-id="36823-182">Searching for and shutting down virtual machines in off-hours.</span></span>
- <span data-ttu-id="36823-183">运行每日报告并生成仪表板, 以向高级管理层报告。</span><span class="sxs-lookup"><span data-stu-id="36823-183">Running daily reports and producing a dashboard to report to senior management.</span></span>

<span data-ttu-id="36823-184">作为一个具体示例, 假设您只希望在营业时间运行虚拟机。</span><span class="sxs-lookup"><span data-stu-id="36823-184">As a concrete example, suppose you want to run a virtual machine only during business hours.</span></span> <span data-ttu-id="36823-185">您可以编写脚本以在上午启动 VM 并在晚间关闭它。</span><span class="sxs-lookup"><span data-stu-id="36823-185">You can write a script to start the VM in the morning and shut it down in the evening.</span></span> <span data-ttu-id="36823-186">您可以将 Azure 自动化配置为在设置时间运行脚本。</span><span class="sxs-lookup"><span data-stu-id="36823-186">You can configure Azure Automation to run the script at set times.</span></span> <span data-ttu-id="36823-187">下图显示了此过程中 Azure 自动化的角色。</span><span class="sxs-lookup"><span data-stu-id="36823-187">The following illustration shows the role of Azure Automation in this process.</span></span>

![展示了 Azure 自动化在管理重复业务流程中的角色的图示。](../media/automation-vm-power-state.png)

## <a name="automating-development-environments"></a><span data-ttu-id="36823-189">自动化开发环境</span><span class="sxs-lookup"><span data-stu-id="36823-189">Automating development environments</span></span>

<span data-ttu-id="36823-190">在云基础结构的管道的另一端, 开发人员使用开发计算机来编写作为业务核心的应用程序和服务。</span><span class="sxs-lookup"><span data-stu-id="36823-190">At the other end of the pipeline of your cloud infrastructure are the development machines used by developers to write the applications and services that are the core of your business.</span></span> <span data-ttu-id="36823-191">您可以使用 Azure DevTest 实验室, 通过所需的所有正确工具和存储库来标记虚拟机。</span><span class="sxs-lookup"><span data-stu-id="36823-191">You can use Azure DevTest Labs to stamp out VMs with all of the correct tools and repositories that they need.</span></span> <span data-ttu-id="36823-192">使用多个服务的开发人员可以在开发环境之间进行切换, 而无需自行预配一台新计算机。</span><span class="sxs-lookup"><span data-stu-id="36823-192">Developers working on multiple services can switch between development environments without having to provision a new machine themselves.</span></span> <span data-ttu-id="36823-193">这些开发环境可以在未使用时关闭, 并在需要时重新启动。</span><span class="sxs-lookup"><span data-stu-id="36823-193">These development environments can be shut down when not in use and restarted when they are required again.</span></span>

## <a name="automation-at-lamna-healthcare"></a><span data-ttu-id="36823-194">Lamna 保健中的自动化</span><span class="sxs-lookup"><span data-stu-id="36823-194">Automation at Lamna Healthcare</span></span>

<span data-ttu-id="36823-195">让我们来看看 Lamna 保健如何通过自动化进行改进。</span><span class="sxs-lookup"><span data-stu-id="36823-195">Let's take a look at how Lamna Healthcare has improved by using automation.</span></span> <span data-ttu-id="36823-196">当您开始旅程时, 基础结构部署和服务器生成都是完全手动完成的。</span><span class="sxs-lookup"><span data-stu-id="36823-196">When you started your journey, infrastructure deployment and server builds were entirely manual.</span></span> <span data-ttu-id="36823-197">工程师通过门户部署所有内容。</span><span class="sxs-lookup"><span data-stu-id="36823-197">Engineers were deploying everything through the portal.</span></span> <span data-ttu-id="36823-198">这就是在测试和生产环境之间引入差异和错误, 而不同之处在于无法在代码命中率前检测问题的能力。</span><span class="sxs-lookup"><span data-stu-id="36823-198">This was introducing variance and errors between test and production environments, and the differences were hindering their ability to detect problems before code hit production.</span></span>

<span data-ttu-id="36823-199">他们现在通过资源管理器模板部署所有基础结构。</span><span class="sxs-lookup"><span data-stu-id="36823-199">They now deploy all their infrastructure through Resource Manager templates.</span></span> <span data-ttu-id="36823-200">这些模板将签入 GitHub 存储库, 并在发布以进行部署之前发生代码评审。</span><span class="sxs-lookup"><span data-stu-id="36823-200">These templates are checked into a GitHub repository, and a code review happens before they are released for deployment.</span></span> <span data-ttu-id="36823-201">他们还可以在开发、测试和生产之间构建相同的基础结构, 以确保他们已在所有环境中验证其配置。</span><span class="sxs-lookup"><span data-stu-id="36823-201">They're also able to build the same infrastructure between dev, test, and production, ensuring they have validated their configuration across all environments.</span></span>

<span data-ttu-id="36823-202">对于使用虚拟机的大多数服务, 它们都有一个标准的基本映像, 并使用 DSC 配置部署后的系统。</span><span class="sxs-lookup"><span data-stu-id="36823-202">For most services using virtual machines, they have a standard base image and use DSC to configure the systems post deployment.</span></span> <span data-ttu-id="36823-203">对于需要虚拟机规模集的可伸缩性的 web 场, 它们具有一个完全自动化的过程, 可用于签入代码并使用内置的所有必需配置生成新图像, 然后使其在其规模集中可用。</span><span class="sxs-lookup"><span data-stu-id="36823-203">For web farms where they need the scalability of virtual machine scale sets, they have a fully automated process to check in code and build a new image with all required configuration built in before making it available in their scale sets.</span></span>

<span data-ttu-id="36823-204">他们有一个自动化作业, 用于在非工作时间内关闭已确定的虚拟机, 以降低成本并使其 VM 也自动进行修补。</span><span class="sxs-lookup"><span data-stu-id="36823-204">They have an Automation job to shut down identified virtual machines in off-hours to reduce costs and have automated their VM patching as well.</span></span>

<span data-ttu-id="36823-205">现在, 开发人员在 DevTest 实验室中有一个自助服务环境, 他们可以在其中针对最新的图像和配置进行开发, 以确保它们的开发内容与生产中的配置相匹配。</span><span class="sxs-lookup"><span data-stu-id="36823-205">Developers now have a self-service environment in DevTest Labs where they can develop against the latest images and configuration, ensuring that what they develop against matches the configuration in production.</span></span>

<span data-ttu-id="36823-206">所有这些都是提前完成的, 但在长期运行中, 这些好处已得到支付。</span><span class="sxs-lookup"><span data-stu-id="36823-206">All of this took some up-front effort, but the benefits have paid off in the long run.</span></span> <span data-ttu-id="36823-207">他们极大地减少了错误, 以及他们的运营团队在维护其环境时所需付出的努力。</span><span class="sxs-lookup"><span data-stu-id="36823-207">They've dramatically reduced error and the effort required by their operations teams to maintain their environments.</span></span> <span data-ttu-id="36823-208">开发人员喜欢他们可以轻松地设置要开发的资源, 从而消除前后的以获取所创建的环境。</span><span class="sxs-lookup"><span data-stu-id="36823-208">Developers love that they can easily go provision resources to develop against, eliminating the back and forth to get environments created.</span></span>

## <a name="summary"></a><span data-ttu-id="36823-209">摘要</span><span class="sxs-lookup"><span data-stu-id="36823-209">Summary</span></span>

<span data-ttu-id="36823-210">我们已经介绍了多种将自动化功能引入体系结构的方法。</span><span class="sxs-lookup"><span data-stu-id="36823-210">We've taken a look at a number of ways to bring automation capabilities into your architecture.</span></span> <span data-ttu-id="36823-211">从将基础结构部署为代码, 以使用实验室环境提高开发人员的工作效率, 可以利用大量的时间来自动执行环境。</span><span class="sxs-lookup"><span data-stu-id="36823-211">From deploying infrastructure as code, to improving developer productivity with lab environments, there's a ton of benefit from taking time to automate your environment.</span></span> <span data-ttu-id="36823-212">减少错误、降低差异并节省运营成本对组织而言是一项显著的好处, 可帮助将云环境转到下一级别。</span><span class="sxs-lookup"><span data-stu-id="36823-212">Reducing error, reducing variance, and saving operational costs can be a significant benefit to your organization and help take your cloud environment to the next level.</span></span>