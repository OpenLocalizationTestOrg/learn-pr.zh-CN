<span data-ttu-id="dd8f1-101">让我们将网络安全组应用到我们的网络, 以便我们只允许通过我们的服务器进行 HTTP 通信。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-101">Let's apply a network security group to our network, so that we only allow HTTP traffic through our server.</span></span>

## <a name="create-a-network-security-group"></a><span data-ttu-id="dd8f1-102">创建网络安全组</span><span class="sxs-lookup"><span data-stu-id="dd8f1-102">Create a network security group</span></span>

<span data-ttu-id="dd8f1-103">Azure 应为我们创建了一个安全组, 因为我们指出我们需要 SSH 访问。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-103">Azure should have created a security group for us because we indicated we wanted SSH access.</span></span> <span data-ttu-id="dd8f1-104">但让我们创建一个新的安全组, 以便您可以完成整个过程。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-104">But let's create a new security group, so you can walk through the entire process.</span></span> <span data-ttu-id="dd8f1-105">如果决定在 vm_之前_创建虚拟网络, 这一点尤其重要。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-105">This is particularly important if you decide to create your virtual network _before_ your VMs.</span></span> <span data-ttu-id="dd8f1-106">如前面所述, 安全组是_可选_的, 并且不一定是通过网络创建的。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-106">As mentioned earlier, security groups are _optional_ and not necessarily created with the network.</span></span>

1. <span data-ttu-id="dd8f1-107">在[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)中, 单击左角边栏中的 "**创建资源**" 按钮以启动新的资源创建。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-107">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), click the **Create a resource** button in the left-corner sidebar to start a new resource creation.</span></span>

1. <span data-ttu-id="dd8f1-108">在 "筛选器" 框中键入**网络安全组**, 然后选择列表中的匹配项。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-108">Type **Network security group** into the filter box and select the matching item in the list.</span></span>

1. <span data-ttu-id="dd8f1-109">确保选择了 "**资源管理器**" 部署模型, 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-109">Make sure the **Resource Manager** deployment model is selected and click **Create**.</span></span>

1. <span data-ttu-id="dd8f1-110">为安全组提供**名称**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-110">Provide a **Name** for your security group.</span></span> <span data-ttu-id="dd8f1-111">同样, 在这里, 命名约定是一个好主意。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-111">Again, naming conventions are a good idea here.</span></span> <span data-ttu-id="dd8f1-112">我们来使用**eus-nsg1**为**测试 web 网络安全组 #1 美国东部**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-112">Let's use **test-web-eus-nsg1** for **Test Web Network Security Group #1 in East US**.</span></span> <span data-ttu-id="dd8f1-113">您可能需要更改名称的位置部分, 以反映放置安全组的位置。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-113">You'll likely want to change the location portion of the name to reflect where you put the security group.</span></span>

1. <span data-ttu-id="dd8f1-114">选择正确的**订阅**并使用现有的**资源组**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-114">Select the proper **Subscription** and use your existing **Resource group**.</span></span>

1. <span data-ttu-id="dd8f1-115">最后, 将其置于 VM/虚拟网络所在的**位置**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-115">Finally, put it into the same **Location** as the VM / virtual network.</span></span> <span data-ttu-id="dd8f1-116">这一点很重要;如果此资源位于不同的位置, 则不能应用该资源。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-116">This is important; you won't be able to apply this resource if it's in a different location.</span></span>

1. <span data-ttu-id="dd8f1-117">单击 "**创建**" 以创建组。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-117">Click **Create** to create the group.</span></span>

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a><span data-ttu-id="dd8f1-118">将新的入站规则添加到我们的网络安全组</span><span class="sxs-lookup"><span data-stu-id="dd8f1-118">Add a new inbound rule to our network security group</span></span>

<span data-ttu-id="dd8f1-119">部署应很快完成。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-119">Deployment should complete quickly.</span></span> <span data-ttu-id="dd8f1-120">完成后, 我们可以将新规则添加到安全组:</span><span class="sxs-lookup"><span data-stu-id="dd8f1-120">When it's finished, we can add new rules to our security group:</span></span>

1. <span data-ttu-id="dd8f1-121">查找新的安全组资源并在 Azure 门户中选择它。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-121">Find the new security group resource and select it in the Azure portal.</span></span>

1. <span data-ttu-id="dd8f1-122">在 "概述" 页上, 您会发现它有一些创建的用于锁定网络的默认规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-122">On the overview page, you'll find that it has some default rules created to lock down the network.</span></span>

    <span data-ttu-id="dd8f1-123">在入站端:</span><span class="sxs-lookup"><span data-stu-id="dd8f1-123">On the inbound side:</span></span>

    - <span data-ttu-id="dd8f1-124">允许从一个 VNet 到另一个 VNet 的所有传入流量。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-124">All incoming traffic from one VNet to another is allowed.</span></span> <span data-ttu-id="dd8f1-125">这样, VNet 中的资源可以相互对话。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-125">This lets resources on the VNet talk to each other.</span></span>
    - <span data-ttu-id="dd8f1-126">Azure 负载平衡器**探测**请求, 以确保 VM 处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-126">Azure Load Balancer **probe** requests to ensure the VM is alive.</span></span>
    - <span data-ttu-id="dd8f1-127">其他所有入站流量将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-127">All other inbound traffic is denied.</span></span>

    <span data-ttu-id="dd8f1-128">在出站端:</span><span class="sxs-lookup"><span data-stu-id="dd8f1-128">On the outbound side:</span></span>
    - <span data-ttu-id="dd8f1-129">VNet 中的所有网络通信都是允许的。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-129">All in-network traffic on the VNet is allowed.</span></span>
    - <span data-ttu-id="dd8f1-130">允许到 internet 的所有出站流量。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-130">All outbound traffic to the internet is permitted.</span></span>
    - <span data-ttu-id="dd8f1-131">其他所有出站通信都将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-131">All other outbound traffic is denied.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd8f1-132">这些默认规则是使用高优先级值设置的, 这意味着它们_最后_得到评估。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-132">These default rules are set with high-priority values, which means that they get evaluated _last_.</span></span> <span data-ttu-id="dd8f1-133">不能更改或删除它们, 但可以通过创建更具体的规则来将您的流量与优先级较低的值相匹配来_覆盖_它们。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-133">They cannot be changed or deleted, but you can _override_ them by creating more specific rules to match your traffic with a lower priority value.</span></span>

1. <span data-ttu-id="dd8f1-134">在安全组的 "**设置**" 面板中, 单击 "**入站安全规则**" 部分。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-134">Click the **Inbound security rules** section in the **Settings** panel for the security group.</span></span>

1. <span data-ttu-id="dd8f1-135">单击 " **+ 添加**" 以添加新的安全规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-135">Click **+ Add** to add a new security rule.</span></span>

    ![显示入站安全规则设置的 Azure 门户屏幕截图, 其中突出显示了 "添加" 按钮。](../media/8-add-rule.png)

    <span data-ttu-id="dd8f1-137">有两种方法可输入安全规则所需的信息: 基本和高级。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-137">There are two ways to enter the information necessary for a security rule: basic and advanced.</span></span> <span data-ttu-id="dd8f1-138">您可以通过单击 "**添加**" 面板顶部的按钮在它们之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-138">You can switch between them by clicking the button at the top of the **add** panel.</span></span>

    ![Azure 门户的一对显示基本和高级规则输入之间切换的屏幕截图, 其中突出显示了切换按钮的两种状态之间的箭头链接。](../media/8-advanced-create-rule.png)

    <span data-ttu-id="dd8f1-140">高级模式提供了完全自定义规则的功能。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-140">The advanced mode provides the ability to customize the rule completely.</span></span> <span data-ttu-id="dd8f1-141">但是, 如果您需要配置已知协议, 则使用基本模式要容易得多。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-141">However, if you need to configure a known protocol, the basic mode is a bit easier to work with.</span></span>

1. <span data-ttu-id="dd8f1-142">切换到基本模式。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-142">Switch to the basic mode.</span></span>

1. <span data-ttu-id="dd8f1-143">添加有关我们的 HTTP 规则的信息:</span><span class="sxs-lookup"><span data-stu-id="dd8f1-143">Add the information for our HTTP rule:</span></span>

    - <span data-ttu-id="dd8f1-144">将**服务**设置为 HTTP。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-144">Set the **Service** to be HTTP.</span></span> <span data-ttu-id="dd8f1-145">这将为你设置你的端口范围。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-145">This will set your port range up for you.</span></span>
    - <span data-ttu-id="dd8f1-146">将**优先级**设置为**1000**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-146">Set the **Priority** to **1000**.</span></span> <span data-ttu-id="dd8f1-147">它的数目必须低于默认**拒绝**规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-147">It has to be a lower number than the default **Deny** rule.</span></span> <span data-ttu-id="dd8f1-148">您可以在任何值上启动范围, 但建议您为自己提供一些空间, 以防以后需要创建异常。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-148">You can start the range at any value, but it's recommended that you give yourself some space in case an exception needs to be created later.</span></span>
    - <span data-ttu-id="dd8f1-149">为规则命名;我们将使用**允许 http 流量**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-149">Give the rule a name; we'll use **allow-http-traffic**.</span></span>
    - <span data-ttu-id="dd8f1-150">为规则提供说明。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-150">Give the rule a description.</span></span>

1. <span data-ttu-id="dd8f1-151">切换回**高级**模式。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-151">Switch back to the **Advanced** mode.</span></span> <span data-ttu-id="dd8f1-152">请注意, 我们的设置仍存在。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-152">Notice that our settings are still present.</span></span> <span data-ttu-id="dd8f1-153">我们可以使用此面板创建更精细的设置。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-153">We can use this panel to create more fine-grained settings.</span></span> <span data-ttu-id="dd8f1-154">特别是, 我们可能会将**源**限制为特定于相机的特定 ip 地址或 ip 地址范围。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-154">In particular, we would likely restrict the **Source** to be a specific IP address or range of IP addresses specific to the cameras.</span></span> <span data-ttu-id="dd8f1-155">如果您知道本地计算机的当前 IP 地址, 则可以尝试。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-155">If you know the current IP address of your local computer, you can try that.</span></span> <span data-ttu-id="dd8f1-156">否则, 将设置保留为 "**任意**", 以便可以测试该规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-156">Otherwise, leave the setting as **Any**, so you can test the rule.</span></span>

1. <span data-ttu-id="dd8f1-157">单击 "**添加**" 以创建规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-157">Click **Add** to create the rule.</span></span> <span data-ttu-id="dd8f1-158">这将更新入站规则列表-请注意, 它们按优先级顺序排列, 就像检查它们的方式一样。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-158">This will update the list of inbound rules - notice they are in priority order, which is how they will be examined.</span></span>

## <a name="apply-the-security-group"></a><span data-ttu-id="dd8f1-159">应用安全组</span><span class="sxs-lookup"><span data-stu-id="dd8f1-159">Apply the security group</span></span>

<span data-ttu-id="dd8f1-160">回想一下, 我们可以将安全组应用到网络接口, 以保护单个 VM 或将其应用于该子网上的任何资源的子网。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-160">Recall that we can apply the security group to a network interface to guard a single VM or to a subnet where it would apply to any resources on that subnet.</span></span> <span data-ttu-id="dd8f1-161">后一种方法往往是最常见的方法, 因此我们来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-161">The latter approach tends to be the most common, so let's do that.</span></span> <span data-ttu-id="dd8f1-162">我们可以通过虚拟网络资源或通过使用虚拟网络的 VM 间接访问 Azure 中的此资源。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-162">We could get to this resource in Azure through either the virtual network resource or indirectly through the VM that is using the virtual network.</span></span>

1. <span data-ttu-id="dd8f1-163">切换到虚拟机的**概述**面板。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-163">Switch to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="dd8f1-164">你可以在 "**所有资源**" 下找到 VM。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-164">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="dd8f1-165">选择 "**设置**" 部分中的 "**网络**" 项。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-165">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="dd8f1-166">在网络属性中, 您将找到有关应用到 VM 的网络的信息, 包括**虚拟网络/子网**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-166">In the networking properties, you will find information about the networking applied to the VM, including the **Virtual network/subnet**.</span></span> <span data-ttu-id="dd8f1-167">这是一个可单击的链接, 可用于访问资源。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-167">This is a clickable link to get to the resource.</span></span> <span data-ttu-id="dd8f1-168">单击它以打开虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-168">Click it to open the virtual network.</span></span> <span data-ttu-id="dd8f1-169">此外, VM 的**概述**面板中_也_提供了此链接。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-169">This link is _also_ available on the **Overview** panel of the VM.</span></span> <span data-ttu-id="dd8f1-170">这两种方法都将打开虚拟网络的**概述**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-170">Either of these will open the **Overview** of the virtual network.</span></span>

1. <span data-ttu-id="dd8f1-171">在 "**设置**" 部分中, 选择 "**子网**" 项。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-171">In the **Settings** section, select the **Subnets** item.</span></span>

1. <span data-ttu-id="dd8f1-172">在前面创建 VM + 网络时, 应定义单个子网 (默认)。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-172">We should have a single subnet defined (default) from when we created the VM + network earlier.</span></span> <span data-ttu-id="dd8f1-173">单击列表中的项目以打开详细信息。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-173">Click the item in the list to open the details.</span></span>

1. <span data-ttu-id="dd8f1-174">单击 "**网络安全组**" 条目。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-174">Click the **Network security group** entry.</span></span>

1. <span data-ttu-id="dd8f1-175">选择您的新安全组: **test-web-eus-nsg1**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-175">Select your new security group: **test-web-eus-nsg1**.</span></span> <span data-ttu-id="dd8f1-176">在这里, 还应存在另一个与 VM 一起创建的组。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-176">There should be another group here as well that was created with the VM.</span></span>

1. <span data-ttu-id="dd8f1-177">单击 "**保存**" 以保存更改。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-177">Click **Save** to save the change.</span></span> <span data-ttu-id="dd8f1-178">将需要一分钟才能应用到网络。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-178">It will take a minute to apply to the network.</span></span>

## <a name="update-the-nsg-on-the-network-interface"></a><span data-ttu-id="dd8f1-179">在网络接口上更新 NSG</span><span class="sxs-lookup"><span data-stu-id="dd8f1-179">Update the NSG on the network interface</span></span>

<span data-ttu-id="dd8f1-180">端口80在应用于子网的 NSG 上是打开的, 但仍将被阻止, 因为它在应用于网络接口的 NSG 上当前不允许。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-180">Port 80 is open on the NSG applied to the subnet, but it's still going to be blocked because it's not currently allowed on the NSG applied to the network interface.</span></span> <span data-ttu-id="dd8f1-181">我们来修复此问题, 然后我们应该能够进行连接。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-181">Let's fix that and then we should be able to connect.</span></span>

1. <span data-ttu-id="dd8f1-182">切换回虚拟机的**概述**面板。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-182">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="dd8f1-183">你可以在 "**所有资源**" 下找到 VM。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-183">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="dd8f1-184">在 "**设置**" 部分中, 选择 "**网络**" 项目。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-184">In the **Settings** section, select the **Networking** item.</span></span>

1. <span data-ttu-id="dd8f1-185">在 "**入站端口规则**" 部分, 您应该会看到子网的 NSG 规则, 然后是该子网正下方的网络接口的 NSG 规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-185">In the **Inbound port rules** section you should see the NSG rules for the subnet, then the NSG rules for the network interface just below it.</span></span> <span data-ttu-id="dd8f1-186">在网络接口的 NSG 规则中, 选择 "**添加入站端口规则**"。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-186">In the NSG rules for the network interface, select **Add inbound port rule**.</span></span>

1. <span data-ttu-id="dd8f1-187">切换到基本模式。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-187">Switch to the basic mode.</span></span>

1. <span data-ttu-id="dd8f1-188">添加有关我们的 HTTP 规则的信息:</span><span class="sxs-lookup"><span data-stu-id="dd8f1-188">Add the information for our HTTP rule:</span></span>

    - <span data-ttu-id="dd8f1-189">将**服务**设置为 HTTP。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-189">Set the **Service** to be HTTP.</span></span> <span data-ttu-id="dd8f1-190">这将为你设置你的端口范围。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-190">This will set your port range up for you.</span></span>
    - <span data-ttu-id="dd8f1-191">将**优先级**设置为**310**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-191">Set the **Priority** to **310**.</span></span>
    - <span data-ttu-id="dd8f1-192">为规则命名;我们将使用**允许 http 流量**。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-192">Give the rule a name; we'll use **allow-http-traffic**.</span></span>
    - <span data-ttu-id="dd8f1-193">为规则提供说明。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-193">Give the rule a description.</span></span>

1. <span data-ttu-id="dd8f1-194">单击 "**添加**" 以创建规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-194">Click **Add** to create the rule.</span></span>

## <a name="verify-the-rules"></a><span data-ttu-id="dd8f1-195">验证规则</span><span class="sxs-lookup"><span data-stu-id="dd8f1-195">Verify the rules</span></span>

<span data-ttu-id="dd8f1-196">让我们验证更改:</span><span class="sxs-lookup"><span data-stu-id="dd8f1-196">Let's validate the change:</span></span>

1. <span data-ttu-id="dd8f1-197">切换回虚拟机的**概述**面板。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-197">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="dd8f1-198">你可以在 "**所有资源**" 下找到 VM。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-198">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="dd8f1-199">选择 "**设置**" 部分中的 "**网络**" 项。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-199">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="dd8f1-200">在网络接口的详细信息中, 有一个用于**有效安全规则**的链接, 可快速向您显示规则的评估方式。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-200">In the network interface details, there is a link for **Effective security rules** that will quickly show you how rules are going to be evaluated.</span></span> <span data-ttu-id="dd8f1-201">单击该链接打开分析并确保您可以看到新的规则。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-201">Click the link to open the analysis and make sure you see your new rules.</span></span>

    ![显示为我们的网络提供有效安全规则的 Azure 门户的屏幕截图。](../media/8-effective-rules.png)

1. <span data-ttu-id="dd8f1-203">当然, 验证其全部工作的最佳方式是通过 HTTP 请求访问我们的服务器。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-203">Of course, the best way to validate it's all working is to hit our server with an HTTP request.</span></span> <span data-ttu-id="dd8f1-204">它现在应该能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-204">It should now work.</span></span>

    ![显示在新 Linux 虚拟机的 IP 上托管的 Apache 默认网页的 web 浏览器的屏幕截图。](../media/6-apache-works.png)

## <a name="one-more-thing"></a><span data-ttu-id="dd8f1-206">另一件事</span><span class="sxs-lookup"><span data-stu-id="dd8f1-206">One more thing</span></span>

<span data-ttu-id="dd8f1-207">安全规则的获取权限非常困难。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-207">Security rules are tricky to get right.</span></span> <span data-ttu-id="dd8f1-208">我们在应用此新安全组时出错了, 我们丢失了 SSH 访问!</span><span class="sxs-lookup"><span data-stu-id="dd8f1-208">We made a mistake when we applied this new security group - we lost our SSH access!</span></span> <span data-ttu-id="dd8f1-209">若要解决此问题, 可以将另一条规则添加到应用到子网的安全组, 以允许 SSH 访问。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-209">To fix this, you can add another rule to the security group applied to the subnet to allow SSH access.</span></span> <span data-ttu-id="dd8f1-210">请务必将规则的入站 tcp/ip 地址限制为您拥有的。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-210">Make sure to restrict the inbound TCP/IP addresses for the rule to be the ones you own.</span></span>

> [!WARNING]
> <span data-ttu-id="dd8f1-211">始终确保锁定用于管理访问的端口。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-211">Always make sure to lock down ports used for administrative access.</span></span> <span data-ttu-id="dd8f1-212">更好的方法是创建 VPN 以将虚拟网络链接到专用网络, 并只允许来自该地址范围的 RDP 或 SSH 请求。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-212">An even better approach is to create a VPN to link the virtual network to your private network and only allow RDP or SSH requests from that address range.</span></span> <span data-ttu-id="dd8f1-213">您还可以将 SSH 使用的端口更改为除默认值之外的其他内容。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-213">You can also change the port used by SSH to be something other than the default.</span></span> <span data-ttu-id="dd8f1-214">请注意, 更改端口不足以停止攻击。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-214">Keep in mind that changing ports is not sufficient to stop attacks.</span></span> <span data-ttu-id="dd8f1-215">它只是让它变得更难发现。</span><span class="sxs-lookup"><span data-stu-id="dd8f1-215">It simply makes it a little harder to discover.</span></span>