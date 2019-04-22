<span data-ttu-id="d3564-101">规划一致的云基础结构从设置策略开始。</span><span class="sxs-lookup"><span data-stu-id="d3564-101">Planning out a consistent cloud infrastructure starts with setting up policy.</span></span> <span data-ttu-id="d3564-102">您的策略将强制实施所创建资源的规则, 因此您的基础结构符合您与客户的公司标准、成本要求和服务级别协议 (sla)。</span><span class="sxs-lookup"><span data-stu-id="d3564-102">Your policies will enforce your rules for created resources, so your infrastructure stays compliant with your corporate standards, cost requirements, and service-level agreements (SLAs) you have with your customers.</span></span>

:::row:::
  :::column:::
    ![表示 Azure 蓝图的图标](../media/2-azurepolicy.png)
  :::column-end:::
    :::column span="3":::
<span data-ttu-id="d3564-104">**azure Policy**是 azure 中的一项服务, 可用于定义、分配和管理环境中资源的标准。</span><span class="sxs-lookup"><span data-stu-id="d3564-104">**Azure Policy** is a service in Azure that you use to define, assign, and, manage standards for resources in your environment.</span></span> <span data-ttu-id="d3564-105">它可以阻止创建不允许的资源, 确保新资源应用了特定设置, 并运行现有资源的评估以扫描不合规性。</span><span class="sxs-lookup"><span data-stu-id="d3564-105">It can prevent the creation of disallowed resources, ensure new resources have specific settings applied, and run evaluations of your existing resources to scan for non-compliance.</span></span> 

<span data-ttu-id="d3564-106">Azure 策略附带了许多内置策略和计划定义, 您可以在 "存储"、"网络"、"计算"、"安全中心" 和 "监视" 等类别下使用这些定义。</span><span class="sxs-lookup"><span data-stu-id="d3564-106">Azure Policy comes with many built-in policy and initiative definitions that you can use, under categories such as Storage, Networking, Compute, Security Center, and Monitoring.</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="d3564-107">设想我们允许组织中的任何人创建虚拟机 (vm)。</span><span class="sxs-lookup"><span data-stu-id="d3564-107">Imagine we allow anyone in our organization to create virtual machines (VMs).</span></span> <span data-ttu-id="d3564-108">我们想要控制开销, 因此 Azure 租户的管理员定义了一个策略, 该策略禁止创建超过4个 cpu 的任何 VM。</span><span class="sxs-lookup"><span data-stu-id="d3564-108">We want to control costs, so the administrator of our Azure tenant defines a policy that prohibits the creation of any VM with more than 4 CPUs.</span></span> <span data-ttu-id="d3564-109">一旦实施了策略, Azure 策略将阻止任何人在允许的 sku 列表之外创建新的 VM。</span><span class="sxs-lookup"><span data-stu-id="d3564-109">Once the policy is implemented, Azure Policy will stop anyone from creating a new VM outside the list of allowed SKUs.</span></span> <span data-ttu-id="d3564-110">此外, 如果您尝试_更新_现有 VM, 它将针对策略进行检查。</span><span class="sxs-lookup"><span data-stu-id="d3564-110">Also, if you try to _update_ an existing VM, it will be checked against policy.</span></span> <span data-ttu-id="d3564-111">最后, Azure 策略将审核组织中的所有现有虚拟机, 以确保实施策略。</span><span class="sxs-lookup"><span data-stu-id="d3564-111">Finally, Azure Policy will audit all the existing VMs in our organization to ensure our policy is enforced.</span></span> <span data-ttu-id="d3564-112">它可以审核不符合要求的资源、更改资源属性或停止创建资源。</span><span class="sxs-lookup"><span data-stu-id="d3564-112">It can audit non-compliant resources, alter the resource properties, or stop the resource from being created.</span></span>

> [!TIP]
> <span data-ttu-id="d3564-113">azure 策略可以与 azure DevOps 集成, 方法是应用任何持续的集成和传递管道策略, 这些策略会影响应用程序的预先部署和后期部署。</span><span class="sxs-lookup"><span data-stu-id="d3564-113">Azure Policy can integrate with Azure DevOps, by applying any continuous integration and delivery pipeline policies that affect the pre-deployment and post-deployment of your applications.</span></span>

## <a name="creating-a-policy"></a><span data-ttu-id="d3564-114">创建策略</span><span class="sxs-lookup"><span data-stu-id="d3564-114">Creating a policy</span></span>

<span data-ttu-id="d3564-115">创建和实现 Azure 策略的过程从创建_策略定义_开始。</span><span class="sxs-lookup"><span data-stu-id="d3564-115">The process of creating and implementing an Azure Policy begins with creating a _policy definition_.</span></span> <span data-ttu-id="d3564-116">每个策略定义都具有强制实施的条件。</span><span class="sxs-lookup"><span data-stu-id="d3564-116">Every policy definition has conditions under which it is enforced.</span></span> <span data-ttu-id="d3564-117">而且, 在满足条件时, 会产生相应的效果。</span><span class="sxs-lookup"><span data-stu-id="d3564-117">And, it has an accompanying effect that takes place if the conditions are met.</span></span> <span data-ttu-id="d3564-118">若要应用策略, 您将:</span><span class="sxs-lookup"><span data-stu-id="d3564-118">To apply a policy, you will:</span></span>

1. <span data-ttu-id="d3564-119">创建策略定义</span><span class="sxs-lookup"><span data-stu-id="d3564-119">Create a policy definition</span></span>
2. <span data-ttu-id="d3564-120">向资源范围分配定义</span><span class="sxs-lookup"><span data-stu-id="d3564-120">Assign a definition to a scope of resources</span></span>
3. <span data-ttu-id="d3564-121">查看策略评估结果</span><span class="sxs-lookup"><span data-stu-id="d3564-121">View policy evaluation results</span></span>

### <a name="what-is-a-policy-definition"></a><span data-ttu-id="d3564-122">什么是策略定义？</span><span class="sxs-lookup"><span data-stu-id="d3564-122">What is a policy definition?</span></span>

<span data-ttu-id="d3564-123">*策略定义*表示要评估的内容以及要采取的操作。</span><span class="sxs-lookup"><span data-stu-id="d3564-123">A *policy definition* expresses what to evaluate and what action to take.</span></span> <span data-ttu-id="d3564-124">例如, 可以确保所有公共网站都使用 HTTPS 进行保护、阻止创建特定存储类型或强制使用特定版本的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="d3564-124">For example, you could ensure all public websites are secured with HTTPS, prevent a particular storage type from being created, or force a specific version of SQL Server to be used.</span></span>

<span data-ttu-id="d3564-125">下面是您可以应用的一些最常见的策略定义。</span><span class="sxs-lookup"><span data-stu-id="d3564-125">Here are some of the most common policy definitions you can apply.</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="d3564-126">策略定义</span><span class="sxs-lookup"><span data-stu-id="d3564-126">Policy definition</span></span> | <span data-ttu-id="d3564-127">说明</span><span class="sxs-lookup"><span data-stu-id="d3564-127">Description</span></span> |
> |--------|-------------|
> | <span data-ttu-id="d3564-128">允许的存储帐户 sku</span><span class="sxs-lookup"><span data-stu-id="d3564-128">Allowed Storage Account SKUs</span></span> | <span data-ttu-id="d3564-129">此策略定义具有一组条件/规则, 用于确定要部署的存储帐户是否在 SKU 大小集中。</span><span class="sxs-lookup"><span data-stu-id="d3564-129">This policy definition has a set of conditions/rules that determine whether a storage account that is being deployed is within a set of SKU sizes.</span></span> <span data-ttu-id="d3564-130">其作用是拒绝不符合定义的 SKU 大小集的所有存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d3564-130">Its effect is to deny all storage accounts that do not adhere to the set of defined SKU sizes.</span></span> |
> | <span data-ttu-id="d3564-131">允许的资源类型</span><span class="sxs-lookup"><span data-stu-id="d3564-131">Allowed Resource Type</span></span> | <span data-ttu-id="d3564-132">此策略定义具有一组条件/规则, 用于指定您的组织可以部署的资源类型。</span><span class="sxs-lookup"><span data-stu-id="d3564-132">This policy definition has a set of conditions/rules to specify the resource types that your organization can deploy.</span></span> <span data-ttu-id="d3564-133">其作用是拒绝不属于此定义列表的所有资源。</span><span class="sxs-lookup"><span data-stu-id="d3564-133">Its effect is to deny all resources that are not part of this defined list.</span></span> |
> | <span data-ttu-id="d3564-134">允许的位置</span><span class="sxs-lookup"><span data-stu-id="d3564-134">Allowed Locations</span></span> | <span data-ttu-id="d3564-135">通过此策略, 您可以限制组织在部署资源时可以指定的位置。</span><span class="sxs-lookup"><span data-stu-id="d3564-135">This policy enables you to restrict the locations that your organization can specify when deploying resources.</span></span> <span data-ttu-id="d3564-136">其效果用于强制实施您的地理符合性要求。</span><span class="sxs-lookup"><span data-stu-id="d3564-136">Its effect is used to enforce your geographic compliance requirements.</span></span> |
> | <span data-ttu-id="d3564-137">允许的虚拟机 sku</span><span class="sxs-lookup"><span data-stu-id="d3564-137">Allowed Virtual Machine SKUs</span></span> | <span data-ttu-id="d3564-138">通过此策略, 您可以指定您的组织可以部署的一组 VM sku。</span><span class="sxs-lookup"><span data-stu-id="d3564-138">This policy enables you to specify a set of VM SKUs that your organization can deploy.</span></span> |
> | <span data-ttu-id="d3564-139">不允许的资源类型</span><span class="sxs-lookup"><span data-stu-id="d3564-139">Not allowed resource types</span></span> | <span data-ttu-id="d3564-140">阻止部署资源类型的列表。</span><span class="sxs-lookup"><span data-stu-id="d3564-140">Prevents a list of resource types from being deployed.</span></span> |

<span data-ttu-id="d3564-141">策略定义本身表示为 JSON 文件, 您可以在门户中使用预定义的定义, 也可以创建自己的定义 (修改现有定义或从头开始)。</span><span class="sxs-lookup"><span data-stu-id="d3564-141">The policy definition itself is represented as a JSON file - you can use one of the pre-defined definitions in the portal or create your own (either modifying an existing one or starting from scratch).</span></span> <span data-ttu-id="d3564-142">[GitHub 上提供了数百个示例](https://github.com/Azure/azure-policy)。</span><span class="sxs-lookup"><span data-stu-id="d3564-142">There are [hundreds of samples available on GitHub](https://github.com/Azure/azure-policy).</span></span>

<span data-ttu-id="d3564-143">下面的示例展示了仅允许特定虚拟机大小的计算策略:</span><span class="sxs-lookup"><span data-stu-id="d3564-143">Here is an example of a Compute policy that only allows specific virtual machine sizes:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Compute/virtualMachines"
      },
      {
        "not": {
          "field": "Microsoft.Compute/virtualMachines/sku.name",
          "in": "[parameters('listOfAllowedSKUs')]"
        }
      }
    ]
  },
  "then": {
    "effect": "Deny"
  }
}
```

<span data-ttu-id="d3564-144">请注意`[parameters('listofAllowedSKUs')]`值;这是在将策略定义应用于作用域时将填写的替换令牌。</span><span class="sxs-lookup"><span data-stu-id="d3564-144">Notice the `[parameters('listofAllowedSKUs')]` value; this is a replacement token that will be filled in when the policy definition is applied to a scope.</span></span> <span data-ttu-id="d3564-145">定义参数时, 将为其指定一个名称, 并根据需要提供一个值。</span><span class="sxs-lookup"><span data-stu-id="d3564-145">When a parameter is defined, it's given a name and optionally given a value.</span></span> 

### <a name="assign-a-definition-to-a-scope-of-resources"></a><span data-ttu-id="d3564-146">向资源范围分配定义</span><span class="sxs-lookup"><span data-stu-id="d3564-146">Assign a definition to a scope of resources</span></span>

<span data-ttu-id="d3564-147">定义了一个或多个策略定义后, 需要对其进行分配。</span><span class="sxs-lookup"><span data-stu-id="d3564-147">Once you've defined one or more policy definitions, you'll need to assign them.</span></span> <span data-ttu-id="d3564-148">_策略分配_是已分配为在特定范围内进行的策略定义。</span><span class="sxs-lookup"><span data-stu-id="d3564-148">A _policy assignment_ is a policy definition that has been assigned to take place within a specific scope.</span></span> 

<span data-ttu-id="d3564-149">此范围的范围可以从完整订阅到资源组。</span><span class="sxs-lookup"><span data-stu-id="d3564-149">This scope could range from a full subscription down to a resource group.</span></span> <span data-ttu-id="d3564-150">所有子资源都继承了策略分配。</span><span class="sxs-lookup"><span data-stu-id="d3564-150">Policy assignments are inherited by all child resources.</span></span> <span data-ttu-id="d3564-151">这意味着, 如果将策略应用于资源组, 则该策略将应用于该资源组中的所有资源。</span><span class="sxs-lookup"><span data-stu-id="d3564-151">This means that if a policy is applied to a resource group, it is applied to all the resources within that resource group.</span></span> <span data-ttu-id="d3564-152">但是, 您可以从策略分配中排除 subscope。</span><span class="sxs-lookup"><span data-stu-id="d3564-152">However, you can exclude a subscope from the policy assignment.</span></span> <span data-ttu-id="d3564-153">例如, 我们可以为整个订阅强制实施一个策略, 然后排除几个选择资源组。</span><span class="sxs-lookup"><span data-stu-id="d3564-153">For example, we could enforce a policy for an entire subscription and then exclude a few select resource groups.</span></span>

<span data-ttu-id="d3564-154">您可以通过 Azure 门户、PowerShell 或 azure CLI 分配这些策略中的任何一个。</span><span class="sxs-lookup"><span data-stu-id="d3564-154">You can assign any of these policies through the Azure portal, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="d3564-155">分配策略定义时, 将需要提供已定义的任何参数。</span><span class="sxs-lookup"><span data-stu-id="d3564-155">When you assign a policy definition, you will need to supply any parameters which are defined.</span></span>

![将策略分配给 Azure 门户中的作用域时显示参数的屏幕截图](../media/2-policy-parameters.png)

### <a name="policy-effects"></a><span data-ttu-id="d3564-157">策略效果</span><span class="sxs-lookup"><span data-stu-id="d3564-157">Policy effects</span></span>

<span data-ttu-id="d3564-158">通过 azure 策略首先评估通过 azure 资源管理器创建或更新资源的请求。</span><span class="sxs-lookup"><span data-stu-id="d3564-158">Requests to create or update a resource through Azure Resource Manager are evaluated by Azure Policy first.</span></span> <span data-ttu-id="d3564-159">Policy 创建所有适用于该资源的工作分配的列表, 然后根据每个定义评估该资源。</span><span class="sxs-lookup"><span data-stu-id="d3564-159">Policy creates a list of all assignments that apply to the resource and then evaluates the resource against each definition.</span></span> <span data-ttu-id="d3564-160">在将请求处理到相应的资源提供程序之前, 策略将处理几个影响, 以避免在资源违反策略时任何不必要的处理。</span><span class="sxs-lookup"><span data-stu-id="d3564-160">Policy processes several of the effects before handing the request to the appropriate Resource Provider to avoid any unnecessary processing if the resource violates policy.</span></span>

<span data-ttu-id="d3564-161">Azure 策略中的每个策略定义都有一个单一的效果。</span><span class="sxs-lookup"><span data-stu-id="d3564-161">Each policy definition in Azure Policy has a single effect.</span></span> <span data-ttu-id="d3564-162">该效果确定在关联的策略规则匹配时会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="d3564-162">That effect determines what happens when the associated policy rule is matched.</span></span> <span data-ttu-id="d3564-163">当发生这种情况时, Azure 策略将根据所分配的效果执行特定操作。</span><span class="sxs-lookup"><span data-stu-id="d3564-163">When that happens, Azure Policy will take a specific action based on the assigned effect.</span></span>

| <span data-ttu-id="d3564-164">策略效果</span><span class="sxs-lookup"><span data-stu-id="d3564-164">Policy Effect</span></span> | <span data-ttu-id="d3564-165">会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="d3564-165">What happens?</span></span> |
|---------------|---------------|
| <span data-ttu-id="d3564-166">他们</span><span class="sxs-lookup"><span data-stu-id="d3564-166">Deny</span></span> | <span data-ttu-id="d3564-167">由于策略, 资源创建/更新失败。</span><span class="sxs-lookup"><span data-stu-id="d3564-167">The resource creation/update fails due to policy.</span></span> |
| <span data-ttu-id="d3564-168">禁用</span><span class="sxs-lookup"><span data-stu-id="d3564-168">Disabled</span></span> | <span data-ttu-id="d3564-169">策略规则将被忽略 (已禁用)。</span><span class="sxs-lookup"><span data-stu-id="d3564-169">The policy rule is ignored (disabled).</span></span> <span data-ttu-id="d3564-170">通常用于测试。</span><span class="sxs-lookup"><span data-stu-id="d3564-170">Often used for testing.</span></span> |
| <span data-ttu-id="d3564-171">Append</span><span class="sxs-lookup"><span data-stu-id="d3564-171">Append</span></span> | <span data-ttu-id="d3564-172">在创建或更新过程中, 向请求的资源添加其他参数/字段。</span><span class="sxs-lookup"><span data-stu-id="d3564-172">Adds additional parameters/fields to the requested resource during creation or update.</span></span> <span data-ttu-id="d3564-173">一个常见的示例是添加标记, 如成本中心或为存储资源指定允许的 ip。</span><span class="sxs-lookup"><span data-stu-id="d3564-173">A common example is adding tags on resources such as Cost Center or specifying allowed IPs for a storage resource.</span></span> |
| <span data-ttu-id="d3564-174">Audit、AuditIfNotExists</span><span class="sxs-lookup"><span data-stu-id="d3564-174">Audit, AuditIfNotExists</span></span> | <span data-ttu-id="d3564-175">在评估不符合项的资源时, 在活动日志中创建一个警告事件, 但不会停止该请求。</span><span class="sxs-lookup"><span data-stu-id="d3564-175">Creates a warning event in the activity log when evaluating a non-compliant resource, but it doesn't stop the request.</span></span> |
| <span data-ttu-id="d3564-176">DeployIfNotExists</span><span class="sxs-lookup"><span data-stu-id="d3564-176">DeployIfNotExists</span></span> | <span data-ttu-id="d3564-177">满足特定条件时执行模板部署。</span><span class="sxs-lookup"><span data-stu-id="d3564-177">Executes a template deployment when a specific condition is met.</span></span> <span data-ttu-id="d3564-178">例如, 如果对数据库启用了 SQL 加密, 则它可以在创建数据库后运行一个模板, 以便以特定方式对其进行设置。</span><span class="sxs-lookup"><span data-stu-id="d3564-178">For example, if SQL encryption is enabled on a database, then it can run a template after the DB is created to set it up a specific way.</span></span> |

### <a name="view-policy-evaluation-results"></a><span data-ttu-id="d3564-179">查看策略评估结果</span><span class="sxs-lookup"><span data-stu-id="d3564-179">View policy evaluation results</span></span>

<span data-ttu-id="d3564-180">即使未通过验证, Azure 策略也可以允许创建资源。</span><span class="sxs-lookup"><span data-stu-id="d3564-180">Azure Policy can allow a resource to be created even if it doesn't pass validation.</span></span> <span data-ttu-id="d3564-181">在这些情况下, 可以让它触发可在 Azure 策略门户或命令行工具中查看的审核事件。</span><span class="sxs-lookup"><span data-stu-id="d3564-181">In these cases, you can have it trigger an audit event which can be viewed in the Azure Policy portal, or through command-line tools.</span></span> <span data-ttu-id="d3564-182">最简单的方法是在门户中, 因为它提供了一个直观的图形概述, 可供您浏览。</span><span class="sxs-lookup"><span data-stu-id="d3564-182">The easiest approach is in the portal as it provides a nice graphical overview which you can explore.</span></span> <span data-ttu-id="d3564-183">您可以通过 "搜索" 字段或 "_所有服务_" 找到 "Azure 策略" 部分。</span><span class="sxs-lookup"><span data-stu-id="d3564-183">You can find the Azure Policy section through the search field or _All Services_.</span></span>

![显示 azure 门户概述屏幕的 azure 门户](../media/2-policy-portal.png)

<span data-ttu-id="d3564-185">在此屏幕上, 您可以找出不合规的资源, 并采取措施纠正这些问题。</span><span class="sxs-lookup"><span data-stu-id="d3564-185">From this screen, you can spot resources which are not compliant and take action to correct them.</span></span> 

> [!TIP]
> <span data-ttu-id="d3564-186">如果你在 azure 基础学习路径中继续, 你将在控件中更详细地看到 azure 策略[, 并使用 azure 资源管理器模块组织 azure 资源](https://docs.microsoft.com/learn/modules/control-and-organize-with-azure-resource-manager/)。</span><span class="sxs-lookup"><span data-stu-id="d3564-186">If you continue in the Azure Fundamentals learning path, you'll see Azure Policy in more detail in the [Control and organize Azure resources with Azure Resource Manager](https://docs.microsoft.com/learn/modules/control-and-organize-with-azure-resource-manager/) module.</span></span>