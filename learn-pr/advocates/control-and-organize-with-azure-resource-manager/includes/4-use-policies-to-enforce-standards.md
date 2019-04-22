<span data-ttu-id="1d95c-101">您要在资源组中更好地组织资源, 并已将标记应用于您的资源, 以便在帐单报告和监控解决方案中使用它们。</span><span class="sxs-lookup"><span data-stu-id="1d95c-101">You're organizing your resources better in resource groups, and you've applied tags to your resources to use them in billing reports and in your monitoring solution.</span></span> <span data-ttu-id="1d95c-102">资源分组和标记在现有资源中有差异, 但如何确保新资源遵循规则？</span><span class="sxs-lookup"><span data-stu-id="1d95c-102">Resource grouping and tagging have made a difference in the existing resources, but how do you ensure that new resources follow the rules?</span></span> <span data-ttu-id="1d95c-103">让我们来看看策略如何帮助您在 Azure 环境中强制实施标准。</span><span class="sxs-lookup"><span data-stu-id="1d95c-103">Let's take a look at how policies can help you enforce standards in your Azure environment.</span></span>

## <a name="what-is-azure-policy"></a><span data-ttu-id="1d95c-104">什么是 Azure 策略？</span><span class="sxs-lookup"><span data-stu-id="1d95c-104">What is Azure Policy?</span></span>

<span data-ttu-id="1d95c-105">Azure Policy 是一种可用于创建、分配和管理策略的服务。</span><span class="sxs-lookup"><span data-stu-id="1d95c-105">Azure Policy is a service you can use to create, assign, and manage policies.</span></span> <span data-ttu-id="1d95c-106">这些策略将应用并强制执行您的资源需要遵循的规则。</span><span class="sxs-lookup"><span data-stu-id="1d95c-106">These policies apply and enforce rules that your resources need to follow.</span></span> <span data-ttu-id="1d95c-107">这些策略可在创建资源时强制实施这些规则, 并且可以依据现有资源对其进行评估, 以提供符合性。</span><span class="sxs-lookup"><span data-stu-id="1d95c-107">These policies can enforce these rules when resources are created, and can be evaluated against existing resources to give visibility into compliance.</span></span>

<span data-ttu-id="1d95c-108">策略可以强制执行某些操作, 例如只允许创建特定类型的资源, 或仅允许特定 Azure 区域中的资源。</span><span class="sxs-lookup"><span data-stu-id="1d95c-108">Policies can enforce things such as only allowing specific types of resources to be created, or only allowing resources in specific Azure regions.</span></span> <span data-ttu-id="1d95c-109">您可以在您的 Azure 环境中强制实施命名约定。</span><span class="sxs-lookup"><span data-stu-id="1d95c-109">You can enforce naming conventions across your Azure environment.</span></span> <span data-ttu-id="1d95c-110">您还可以强制将特定标记应用于资源。</span><span class="sxs-lookup"><span data-stu-id="1d95c-110">You can also enforce that specific tags are applied to resources.</span></span> <span data-ttu-id="1d95c-111">让我们来看看策略的工作原理。</span><span class="sxs-lookup"><span data-stu-id="1d95c-111">Let's take a look at how policies work.</span></span>

## <a name="create-a-policy"></a><span data-ttu-id="1d95c-112">创建策略</span><span class="sxs-lookup"><span data-stu-id="1d95c-112">Create a policy</span></span>

<span data-ttu-id="1d95c-113">我们希望确保所有资源都有与其相关联的**部门**标签, 如果不存在, 则阻止创建。</span><span class="sxs-lookup"><span data-stu-id="1d95c-113">We'd like to ensure that all resources have the **Department** tag associated with them and block creation if it doesn't exist.</span></span> <span data-ttu-id="1d95c-114">我们需要创建一个新的策略定义, 然后将其分配给一个作用域;在这种情况下, 作用域将成为我们的**mslearn-rg**资源组。</span><span class="sxs-lookup"><span data-stu-id="1d95c-114">We'll need to create a new policy definition and then assign it to a scope; in this case the scope will be our **mslearn-core-infrastructure-rg** resource group.</span></span> <span data-ttu-id="1d95c-115">可以通过 azure 门户、azure PowerShell 或 azure CLI 创建和分配策略。</span><span class="sxs-lookup"><span data-stu-id="1d95c-115">Policies can be created and assigned through the Azure portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="1d95c-116">我们来演练一下如何在门户中创建策略。</span><span class="sxs-lookup"><span data-stu-id="1d95c-116">Let's walk through how to do create a policy in the portal.</span></span>

### <a name="create-the-policy-definition"></a><span data-ttu-id="1d95c-117">创建策略定义</span><span class="sxs-lookup"><span data-stu-id="1d95c-117">Create the policy definition</span></span>

1. <span data-ttu-id="1d95c-118">如果你还没有, 请继续在 web 浏览器中提取[Azure 门户](https://portal.azure.com/?azure-portal=true)(如果尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="1d95c-118">Go ahead and pull up the [Azure portal](https://portal.azure.com/?azure-portal=true) in a web browser if you haven't already.</span></span> <span data-ttu-id="1d95c-119">在顶部导航栏的搜索框中, 搜索**策略**并选择**策略**服务。</span><span class="sxs-lookup"><span data-stu-id="1d95c-119">In the search box in the top navigation bar, search for **Policy** and select the **Policy** service.</span></span>

1. <span data-ttu-id="1d95c-120">在 "**创作**" 部分的左侧菜单中, 选择 "**定义**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-120">In **Authoring** section in the left menu, select **Definitions**.</span></span>

1. <span data-ttu-id="1d95c-121">您应该会看到可使用的内置策略列表。</span><span class="sxs-lookup"><span data-stu-id="1d95c-121">You should see a list of built-in policies that you can use.</span></span> <span data-ttu-id="1d95c-122">在这种情况下, 我们将创建自己的自定义策略。</span><span class="sxs-lookup"><span data-stu-id="1d95c-122">In this case, we're going to create our own custom policy.</span></span> <span data-ttu-id="1d95c-123">在顶部菜单中单击 " **+ 策略定义**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-123">Click **+ Policy definition** in the top menu.</span></span>

1. <span data-ttu-id="1d95c-124">这将显示 "**新建策略定义**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="1d95c-124">This brings up the **New policy definition** dialog.</span></span> <span data-ttu-id="1d95c-125">若要设置**定义位置**, 请单击蓝色 **...**。选择要在其中存储策略的订阅, 它应与我们的资源组具有相同的订阅。</span><span class="sxs-lookup"><span data-stu-id="1d95c-125">To set the **Definition location**, click the blue **...**. Select the subscription for the policy to be stored in, which should be the same subscription as our resource group.</span></span> <span data-ttu-id="1d95c-126">单击 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-126">Click **Select**.</span></span>

1. <span data-ttu-id="1d95c-127">返回到 "**新建策略定义**" 对话框的 "**名称**" 为策略指定**资源上的 "强制" 标记**的名称。</span><span class="sxs-lookup"><span data-stu-id="1d95c-127">Back on the **New policy definition** dialog, for **Name** give your policy a name of **Enforce tag on resource**.</span></span>

1. <span data-ttu-id="1d95c-128">在 "**说明**" 中, 输入**此策略将强制存在对资源的标记。**</span><span class="sxs-lookup"><span data-stu-id="1d95c-128">For the **Description**, enter **This policy enforces the existence of a tag on a resource.**</span></span>

1. <span data-ttu-id="1d95c-129">对于 "**类别**", 选择 "**使用现有**", 然后选择 "**常规**" 类别。</span><span class="sxs-lookup"><span data-stu-id="1d95c-129">For **Category** select **Use existing** and then select the **General** category.</span></span>

1. <span data-ttu-id="1d95c-130">对于**策略规则**, 删除框中的所有文本, 并粘贴以下 JSON。</span><span class="sxs-lookup"><span data-stu-id="1d95c-130">For the **Policy rule**, delete all text in the box and paste in the following JSON.</span></span>

    ```json
    {
      "mode": "indexed",
      "policyRule": {
        "if": {
          "field": "[concat('tags[', parameters('tagName'), ']')]",
          "exists": "false"
        },
        "then": {
          "effect": "deny"
        }
      },
      "parameters": {
        "tagName": {
          "type": "String",
          "metadata": {
            "displayName": "Tag Name",
            "description": "Name of the tag, such as 'environment'"
          }
        }
      }
    }
    ```

    <span data-ttu-id="1d95c-131">您的策略定义应如下所示。</span><span class="sxs-lookup"><span data-stu-id="1d95c-131">Your policy definition should look like below.</span></span> <span data-ttu-id="1d95c-132">单击 "**保存**" 以保存策略定义。</span><span class="sxs-lookup"><span data-stu-id="1d95c-132">Click **Save** to save your policy definition.</span></span>

    ![显示 "新建策略定义" 对话框的门户的图像](../media/4-policy-definition.PNG)

### <a name="create-a-policy-assignment"></a><span data-ttu-id="1d95c-134">创建策略分配</span><span class="sxs-lookup"><span data-stu-id="1d95c-134">Create a policy assignment</span></span>

<span data-ttu-id="1d95c-135">我们已经创建了策略, 但实际上并不会使其生效。</span><span class="sxs-lookup"><span data-stu-id="1d95c-135">We've created the policy, but we haven't actually put it into effect yet.</span></span> <span data-ttu-id="1d95c-136">若要启用该策略, 我们需要创建一个工作分配。</span><span class="sxs-lookup"><span data-stu-id="1d95c-136">To enable the policy, we need to create an assignment.</span></span> <span data-ttu-id="1d95c-137">在这种情况下, 我们会将其分配给我们的**msftlearn-rg**资源组的范围, 以便它适用于资源组中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="1d95c-137">In this case, we'll assign it to the scope of our **msftlearn-core-infrastructure-rg** resource group, so that it applies to anything inside the resource group.</span></span>

1. <span data-ttu-id="1d95c-138">在策略窗格中, 在左侧的 "**创作**" 部分中, 选择 "**分配**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-138">In the policy pane, in the **Authoring** section on the left, select **Assignments**.</span></span>

1. <span data-ttu-id="1d95c-139">选择顶部的 "**分配策略**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-139">Select **Assign policy** at the top.</span></span>

1. <span data-ttu-id="1d95c-140">在 "**分配策略**" 窗格中, 我们会将策略分配给资源组。</span><span class="sxs-lookup"><span data-stu-id="1d95c-140">In the **Assign policy** pane, we'll assign our policy to our resource group.</span></span> <span data-ttu-id="1d95c-141">对于 "**范围**", 单击蓝色 **...**。选择您的订阅和**msftlearn-rg**资源组, 然后单击 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-141">For **Scope**, click the blue **...**. Select your subscription and the **msftlearn-core-infrastructure-rg** resource group, then click **Select**.</span></span>

1. <span data-ttu-id="1d95c-142">对于 "**策略定义**", 单击 "蓝色 **...**"。在 "**类型**" 下拉中, 选择 "**自定义**", 选择 "在您创建的**资源策略上强制标记**", 然后单击 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-142">For **Policy definition**, click the blue **...**. In the **Type** drop-down, select **Custom**, select the **Enforce tag on resource** policy you created, then click **Select**.</span></span>

1. <span data-ttu-id="1d95c-143">在 "**参数**" 部分的 "**标记名称**"**部门**中。</span><span class="sxs-lookup"><span data-stu-id="1d95c-143">In the **Parameters** section, for **Tag name** enter **Department**.</span></span> <span data-ttu-id="1d95c-144">单击 "**分配**" 以分配策略。</span><span class="sxs-lookup"><span data-stu-id="1d95c-144">Click **Assign** to assign the policy.</span></span>

### <a name="test-out-the-policy"></a><span data-ttu-id="1d95c-145">测试策略</span><span class="sxs-lookup"><span data-stu-id="1d95c-145">Test out the policy</span></span>

<span data-ttu-id="1d95c-146">至此, 我们已将策略分配给资源组, 任何创建没有**部门**标记的资源的尝试都将失败。</span><span class="sxs-lookup"><span data-stu-id="1d95c-146">Now that we have assigned the policy to our resource group, any attempts to create a resource without the **Department** tag should fail.</span></span> <span data-ttu-id="1d95c-147">让我们试一试。</span><span class="sxs-lookup"><span data-stu-id="1d95c-147">Let's try this out.</span></span>

1. <span data-ttu-id="1d95c-148">单击 "+ 在门户左上角**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-148">Click **+ Create a resource** in the top left of the portal.</span></span>

1. <span data-ttu-id="1d95c-149">搜索**存储帐户**并在结果中选择**存储帐户-blob、文件、表、队列**。</span><span class="sxs-lookup"><span data-stu-id="1d95c-149">Search for **Storage Account** and select **Storage account - blob, file, table, queue** in the results.</span></span> <span data-ttu-id="1d95c-150">单击"创建"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-150">Click **Create**.</span></span>

1. <span data-ttu-id="1d95c-151">选择您的订阅和**msftlearn-rg**资源组。</span><span class="sxs-lookup"><span data-stu-id="1d95c-151">Select your subscription, and the **msftlearn-core-infrastructure-rg** resource group.</span></span>

1. <span data-ttu-id="1d95c-152">对于**存储帐户名称**, 请为其指定您选择的任何名称, 但请注意, 它必须是一个全局唯一名称。</span><span class="sxs-lookup"><span data-stu-id="1d95c-152">For **Storage account name**, give it any name of your choice, but note that it does have to be a globally unique name.</span></span>

1. <span data-ttu-id="1d95c-153">保留其余选项的默认值, 请单击 "**审阅 + 创建**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-153">Leave the rest of the options at their default, click **Review + create**.</span></span>

    <span data-ttu-id="1d95c-154">对资源创建的验证将失败, 因为我们没有对该资源应用**部门**标记。</span><span class="sxs-lookup"><span data-stu-id="1d95c-154">Validation of your resource creation will fail because we don't have a **Department** tag applied to the resource.</span></span>

    ![显示违反策略的门户的图像](../media/4-policy-violation.PNG)

    <span data-ttu-id="1d95c-156">让我们修复冲突, 以便我们可以成功部署存储帐户。</span><span class="sxs-lookup"><span data-stu-id="1d95c-156">Let's fix the violation so we can successfully deploy the storage account.</span></span>

1. <span data-ttu-id="1d95c-157">在 tht 的 "**创建存储帐户**" 窗格顶部选择**标记**。</span><span class="sxs-lookup"><span data-stu-id="1d95c-157">Select **Tags** at tht top of the **Create storage account** pane.</span></span>

1. <span data-ttu-id="1d95c-158">将 "**部门: 财务**" 标记添加到列表中。</span><span class="sxs-lookup"><span data-stu-id="1d95c-158">Add a **Department:Finance** tag to the list.</span></span>

    ![显示新 "部门" 标记的门户的图像](../media/4-add-department-tag.PNG)

1. <span data-ttu-id="1d95c-160">现在, 单击 "**审阅 + 创建**"。</span><span class="sxs-lookup"><span data-stu-id="1d95c-160">Now click **Review + create**.</span></span> <span data-ttu-id="1d95c-161">验证现在应传递, 如果单击 "**创建**", 则将创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="1d95c-161">Validation should now pass, and if you click **Create** your storage account will be created.</span></span>

## <a name="use-policies-to-enforce-standards"></a><span data-ttu-id="1d95c-162">使用策略强制实施标准</span><span class="sxs-lookup"><span data-stu-id="1d95c-162">Use policies to enforce standards</span></span>

<span data-ttu-id="1d95c-163">我们已了解如何使用策略来确保我们的资源具有可组织我们的资源的标记。</span><span class="sxs-lookup"><span data-stu-id="1d95c-163">We've seen how we could use policies to ensure that our resources have the tags that organize our resources.</span></span> <span data-ttu-id="1d95c-164">有其他方法可用于我们的福利。</span><span class="sxs-lookup"><span data-stu-id="1d95c-164">There are other ways policies can be used to our benefit.</span></span>

<span data-ttu-id="1d95c-165">我们可以使用策略限制可将资源部署到的 Azure 区域。</span><span class="sxs-lookup"><span data-stu-id="1d95c-165">We could use policy to restrict which Azure regions we can deploy resources to.</span></span> <span data-ttu-id="1d95c-166">对于管控程度较高或对数据可以驻留的领域具有法律或法规限制的组织而言, 策略有助于确保不会在地理区域中预配不符合这些要求的资源。</span><span class="sxs-lookup"><span data-stu-id="1d95c-166">For organizations that are heavily regulated or have legal or regulatory restrictions on where data can reside, policies help to ensure that resources aren't provisioned in geographic areas that would go against these requirements.</span></span>

<span data-ttu-id="1d95c-167">我们可以使用策略来限制可部署的虚拟机大小的类型。</span><span class="sxs-lookup"><span data-stu-id="1d95c-167">We could use policy to restrict which types of virtual machine sizes can be deployed.</span></span> <span data-ttu-id="1d95c-168">您可能需要在生产订阅中允许较大的 VM 大小, 但也许您希望确保在开发订阅中保持最小化的成本。</span><span class="sxs-lookup"><span data-stu-id="1d95c-168">You may want to allow large VM sizes in your production subscriptions, but maybe you'd like to ensure that you keep costs minimized in your dev subscriptions.</span></span> <span data-ttu-id="1d95c-169">通过在 dev 订阅中通过策略拒绝大型 VM 大小, 可以确保它们不会在这些环境中部署。</span><span class="sxs-lookup"><span data-stu-id="1d95c-169">By denying the large VM sizes through policy in your dev subscriptions, you can ensure they don't get deployed in these environments.</span></span>

<span data-ttu-id="1d95c-170">我们还可以使用策略强制实施命名约定。</span><span class="sxs-lookup"><span data-stu-id="1d95c-170">We could also use policy to enforce naming conventions.</span></span> <span data-ttu-id="1d95c-171">如果我们的组织已根据特定的命名约定进行了标准化, 则使用策略强制实施约定可帮助我们在 Azure 资源中保持一致的命名标准。</span><span class="sxs-lookup"><span data-stu-id="1d95c-171">If our organization has standardized on specific naming conventions, using policy to enforce the conventions helps us to keep a consistent naming standard across our Azure resources.</span></span>
