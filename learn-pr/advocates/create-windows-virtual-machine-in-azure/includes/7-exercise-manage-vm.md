<span data-ttu-id="18ed6-101">我们的服务器已准备好处理视频数据;要做的最后一件事是打开流量相机将用于将视频文件上传到我们的服务器的端口。</span><span class="sxs-lookup"><span data-stu-id="18ed6-101">Our server is ready to process video data; the last thing we need to do is open the ports that the traffic cameras will use to upload video files to our server.</span></span>

## <a name="create-a-network-security-group"></a><span data-ttu-id="18ed6-102">创建网络安全组</span><span class="sxs-lookup"><span data-stu-id="18ed6-102">Create a network security group</span></span>

<span data-ttu-id="18ed6-103">Azure 应为我们创建了一个安全组, 因为我们指出我们需要远程桌面访问。</span><span class="sxs-lookup"><span data-stu-id="18ed6-103">Azure should have created a security group for us because we indicated we wanted Remote Desktop access.</span></span> <span data-ttu-id="18ed6-104">但让我们创建一个新的安全组, 以便您可以完成整个过程。</span><span class="sxs-lookup"><span data-stu-id="18ed6-104">But let's create a new security group so you can walk through the entire process.</span></span> <span data-ttu-id="18ed6-105">如果决定在 vm_之前_创建虚拟网络, 这一点尤其重要。</span><span class="sxs-lookup"><span data-stu-id="18ed6-105">This is particularly important if you decide to create your virtual network _before_ your VMs.</span></span> <span data-ttu-id="18ed6-106">如前面所述, 安全组是_可选_的, 并且不一定是通过网络创建的。</span><span class="sxs-lookup"><span data-stu-id="18ed6-106">As mentioned earlier, security groups are _optional_ and not necessarily created with the network.</span></span>

> [!NOTE]
> <span data-ttu-id="18ed6-107">由于这是__ 第二个 VM, 因此我们已有一个安全组应用于我们的网络, 但我们假设你不知道, 或者此虚拟机的规则不同。</span><span class="sxs-lookup"><span data-stu-id="18ed6-107">Since this is _supposed_ to be the second VM, we would already have a security group to apply to our network, but let's pretend for a moment that we don't, or that the rules are different for this VM.</span></span>

1. <span data-ttu-id="18ed6-108">在[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)中, 单击左侧侧边条中的 "**创建资源**" 按钮以启动新的资源创建。</span><span class="sxs-lookup"><span data-stu-id="18ed6-108">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), click the **Create a resource** button in the left corner sidebar to start a new resource creation.</span></span>

1. <span data-ttu-id="18ed6-109">在 "筛选器" 框中键入 "网络安全组", 并选择列表中的匹配项。</span><span class="sxs-lookup"><span data-stu-id="18ed6-109">Type "Network security group" into the filter box and select the matching item in the list.</span></span>

1. <span data-ttu-id="18ed6-110">确保选择了 "**资源管理器**" 部署模型, 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="18ed6-110">Make sure the **Resource Manager** deployment model is selected and click **Create**.</span></span>

1. <span data-ttu-id="18ed6-111">为安全组提供**名称**。</span><span class="sxs-lookup"><span data-stu-id="18ed6-111">Provide a **Name** for your security group.</span></span> <span data-ttu-id="18ed6-112">同样, 在这里, 命名约定是一个好主意, 我们将 "测试部副 nsg2" 用于 "测试视频处理器网络安全组 #2"。</span><span class="sxs-lookup"><span data-stu-id="18ed6-112">Again, naming conventions are a good idea here, let's use "test-vp-nsg2" for "Test Video Processor Network Security Group #2".</span></span>

1. <span data-ttu-id="18ed6-113">选择正确的**订阅**, 并使用现有的**资源组**"<rgn>[沙盒资源组名称]</rgn>"。</span><span class="sxs-lookup"><span data-stu-id="18ed6-113">Select the proper **Subscription** and use your existing **Resource group**, "<rgn>[sandbox resource group name]</rgn>".</span></span>

1. <span data-ttu-id="18ed6-114">最后, 将其置于 VM/虚拟网络所在的**位置**。</span><span class="sxs-lookup"><span data-stu-id="18ed6-114">Finally, put it into the same **Location** as the VM / Virtual Network.</span></span> <span data-ttu-id="18ed6-115">这一点很重要-如果此资源位于不同的位置, 则不能应用该资源。</span><span class="sxs-lookup"><span data-stu-id="18ed6-115">This is important - you won't be able to apply this resource if it's in a different location.</span></span>

1. <span data-ttu-id="18ed6-116">单击 "**创建**" 以创建组。</span><span class="sxs-lookup"><span data-stu-id="18ed6-116">Click **Create** to create the group.</span></span>

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a><span data-ttu-id="18ed6-117">将新的入站规则添加到我们的网络安全组</span><span class="sxs-lookup"><span data-stu-id="18ed6-117">Add a new inbound rule to our Network Security Group</span></span>

<span data-ttu-id="18ed6-118">部署应很快完成。</span><span class="sxs-lookup"><span data-stu-id="18ed6-118">Deployment should complete quickly.</span></span>

1. <span data-ttu-id="18ed6-119">查找新的安全组资源并在 Azure 门户中选择它。</span><span class="sxs-lookup"><span data-stu-id="18ed6-119">Find the new security group resource and select it in the Azure portal.</span></span>

1. <span data-ttu-id="18ed6-120">在 "概述" 页上, 您会发现它有一些创建的用于锁定网络的默认规则。</span><span class="sxs-lookup"><span data-stu-id="18ed6-120">On the overview page, you'll find that it has some default rules created to lock down the network.</span></span>

    <span data-ttu-id="18ed6-121">在入站端:</span><span class="sxs-lookup"><span data-stu-id="18ed6-121">On the inbound side:</span></span>

    - <span data-ttu-id="18ed6-122">允许从一个 VNet 到另一个 VNet 的所有入站流量。</span><span class="sxs-lookup"><span data-stu-id="18ed6-122">All inbound traffic from one VNet to another is allowed.</span></span> <span data-ttu-id="18ed6-123">这样, VNet 中的资源可以相互对话。</span><span class="sxs-lookup"><span data-stu-id="18ed6-123">This lets resources on the VNet talk to each other.</span></span>
    - <span data-ttu-id="18ed6-124">Azure 负载平衡器的 "探测" 请求, 以确保 VM 处于活动状态</span><span class="sxs-lookup"><span data-stu-id="18ed6-124">Azure Load balancer "probe" requests to ensure the VM is alive</span></span>
    - <span data-ttu-id="18ed6-125">其他所有入站流量将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="18ed6-125">All other inbound traffic is denied.</span></span>

    <span data-ttu-id="18ed6-126">在出站端:</span><span class="sxs-lookup"><span data-stu-id="18ed6-126">On the outbound side:</span></span>
    - <span data-ttu-id="18ed6-127">VNet 中的所有网络通信都是允许的。</span><span class="sxs-lookup"><span data-stu-id="18ed6-127">All in-network traffic on the VNet is allowed.</span></span>
    - <span data-ttu-id="18ed6-128">允许到 Internet 的所有出站流量。</span><span class="sxs-lookup"><span data-stu-id="18ed6-128">All outbound traffic to the Internet is allowed.</span></span>
    - <span data-ttu-id="18ed6-129">其他所有出站通信都将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="18ed6-129">All other outbound traffic is denied.</span></span>

> [!NOTE]
> <span data-ttu-id="18ed6-130">这些默认规则是使用高优先级值设置的, 这意味着它们将得到_最后_评估。</span><span class="sxs-lookup"><span data-stu-id="18ed6-130">These default rules are set with high priority values, which means that they get evaluated _last_.</span></span> <span data-ttu-id="18ed6-131">不能更改或删除它们, 但可以通过创建更具体的规则来将您的流量与优先级较低的值相匹配来_覆盖_它们。</span><span class="sxs-lookup"><span data-stu-id="18ed6-131">They cannot be changed or deleted, but you can _override_ them by creating more specific rules to match your traffic with a lower priority value.</span></span>

1. <span data-ttu-id="18ed6-132">在安全组的 "**设置**" 面板中, 单击 "**入站安全规则**" 部分。</span><span class="sxs-lookup"><span data-stu-id="18ed6-132">Click the **Inbound security rules** section in the **Settings** panel for the security group.</span></span>

1. <span data-ttu-id="18ed6-133">单击 " **+ 添加**" 以添加新的安全规则。</span><span class="sxs-lookup"><span data-stu-id="18ed6-133">Click **+ Add** to add a new security rule.</span></span>

    ![显示 "添加安全规则" 对话框的屏幕截图。](../media/8-add-rule.png)

    <span data-ttu-id="18ed6-135">有两种方法可输入安全规则所需的信息: 基本和高级。</span><span class="sxs-lookup"><span data-stu-id="18ed6-135">There are two ways to enter the information necessary for a security rule: basic and advanced.</span></span> <span data-ttu-id="18ed6-136">您可以通过单击 "添加" 面板顶部的按钮在它们之间进行切换。</span><span class="sxs-lookup"><span data-stu-id="18ed6-136">You can switch between them by clicking the button at the top of the "add" panel.</span></span>

    ![Azure 门户的一对显示基本和高级规则输入之间切换的屏幕截图, 其中突出显示了切换按钮的两种状态之间的箭头链接。](../media/8-advanced-create-rule.png)

    <span data-ttu-id="18ed6-138">高级模式提供了完全自定义规则的功能, 但是, 如果只需要配置已知协议, 基本模式会更易于使用。</span><span class="sxs-lookup"><span data-stu-id="18ed6-138">The advanced mode provides the ability to completely customize the rule, however, if you just need to configure a known protocol, the basic mode is a bit easier to work with.</span></span>

1. <span data-ttu-id="18ed6-139">该面板以**高级**模式启动, 单击顶部的 "**基本**" 按钮以切换到基本模式, 该模式的填充选项较少。</span><span class="sxs-lookup"><span data-stu-id="18ed6-139">The panel starts in **Advanced** mode, click the **Basic** button at the top to switch to basic mode which has less options to fill out.</span></span>

1. <span data-ttu-id="18ed6-140">添加有关我们的 FTP 规则的信息。</span><span class="sxs-lookup"><span data-stu-id="18ed6-140">Add the information for our FTP rule.</span></span>

    - <span data-ttu-id="18ed6-141">将**服务**设置为 FTP。</span><span class="sxs-lookup"><span data-stu-id="18ed6-141">Set the **Service** to be FTP.</span></span> <span data-ttu-id="18ed6-142">这将为你设置你的端口范围。</span><span class="sxs-lookup"><span data-stu-id="18ed6-142">This will set your port range up for you.</span></span>
    - <span data-ttu-id="18ed6-143">将**优先级**设置为 "1000"。</span><span class="sxs-lookup"><span data-stu-id="18ed6-143">Set the **Priority** to "1000".</span></span> <span data-ttu-id="18ed6-144">它的数目必须低于默认**拒绝**规则。</span><span class="sxs-lookup"><span data-stu-id="18ed6-144">It has to be a lower number than the default **Deny** rule.</span></span> <span data-ttu-id="18ed6-145">可以在任何值上启动范围, 但建议您为自己提供一些空间, 以防以后需要创建异常。</span><span class="sxs-lookup"><span data-stu-id="18ed6-145">You can start the range at any value, but it's recommended you give yourself some space in case an exception needs to be created later.</span></span>
    - <span data-ttu-id="18ed6-146">为规则命名时, 我们将使用 "流量-cam-ftp-上传-2"。</span><span class="sxs-lookup"><span data-stu-id="18ed6-146">Give the rule a name, we'll use "traffic-cam-ftp-upload-2".</span></span>
    - <span data-ttu-id="18ed6-147">为规则提供说明。</span><span class="sxs-lookup"><span data-stu-id="18ed6-147">Give the rule a description.</span></span>

1. <span data-ttu-id="18ed6-148">单击顶部的 "**高级**" 按钮, 切换回 "**高级**" 模式。</span><span class="sxs-lookup"><span data-stu-id="18ed6-148">Switch back to the **Advanced** mode by clicking the **Advanced** button at the top.</span></span> <span data-ttu-id="18ed6-149">请注意, 我们的设置仍存在。</span><span class="sxs-lookup"><span data-stu-id="18ed6-149">Notice that our settings are still present.</span></span> <span data-ttu-id="18ed6-150">我们可以使用此面板创建更精细的设置。</span><span class="sxs-lookup"><span data-stu-id="18ed6-150">We can use this panel to create more fine-grained settings.</span></span> <span data-ttu-id="18ed6-151">特别是, 我们可能会将**源**限制为特定于相机的特定 ip 地址或 ip 地址范围。</span><span class="sxs-lookup"><span data-stu-id="18ed6-151">In particular, we would likely restrict the **Source** to be a specific IP address or range of IP addresses specific to the cameras.</span></span> <span data-ttu-id="18ed6-152">如果您知道本地计算机的当前 IP 地址, 则可以尝试。</span><span class="sxs-lookup"><span data-stu-id="18ed6-152">If you know the current IP address of your local computer, you can try that.</span></span> <span data-ttu-id="18ed6-153">否则, 将设置保留为 "任何", 以便可以测试该规则。</span><span class="sxs-lookup"><span data-stu-id="18ed6-153">Otherwise, leave the setting as "Any" so you can test the rule.</span></span>

1. <span data-ttu-id="18ed6-154">单击 "**添加**" 以创建规则。</span><span class="sxs-lookup"><span data-stu-id="18ed6-154">Click **Add** to create the rule.</span></span> <span data-ttu-id="18ed6-155">这将更新入站规则列表-请注意, 它们按优先级顺序排列, 就像检查它们的方式一样。</span><span class="sxs-lookup"><span data-stu-id="18ed6-155">This will update the list of inbound rules - notice they are in priority order, which is how they will be examined.</span></span>

## <a name="apply-the-security-group"></a><span data-ttu-id="18ed6-156">应用安全组</span><span class="sxs-lookup"><span data-stu-id="18ed6-156">Apply the security group</span></span>

<span data-ttu-id="18ed6-157">请记住, 我们可以将安全组应用到网络接口, 以保护单个 VM 或将其应用于该子网上的任何资源的子网。</span><span class="sxs-lookup"><span data-stu-id="18ed6-157">Recall that we can apply the security group to a network interface to guard a single VM, or to a subnet where it would apply to any resources on that subnet.</span></span> <span data-ttu-id="18ed6-158">后一种方法往往是最常见的方法, 因此让我们来实现。</span><span class="sxs-lookup"><span data-stu-id="18ed6-158">The latter approach tends to be the most common so let's do that.</span></span> <span data-ttu-id="18ed6-159">我们可以通过虚拟网络资源或通过 VM (使用虚拟网络) 间接访问 Azure 中的此资源。</span><span class="sxs-lookup"><span data-stu-id="18ed6-159">We could get to this resource in Azure through either the virtual network resource or indirectly through the VM, which is using the virtual network.</span></span>

1. <span data-ttu-id="18ed6-160">切换到虚拟机的**概述**面板。</span><span class="sxs-lookup"><span data-stu-id="18ed6-160">Switch to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="18ed6-161">你可以在 "**所有资源**" 下找到 VM。</span><span class="sxs-lookup"><span data-stu-id="18ed6-161">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="18ed6-162">选择 "**设置**" 部分中的 "**网络**" 项。</span><span class="sxs-lookup"><span data-stu-id="18ed6-162">Select the **Networking** item in the **Settings** section.</span></span>

    ![在应用了网络安全组的虚拟机设置中显示网络项详细信息的屏幕截图。](../media/8-network-settings.png)

1. <span data-ttu-id="18ed6-164">在网络属性中, 您将找到有关应用到 VM 的网络 (包括**虚拟网络/子网**) 的信息。</span><span class="sxs-lookup"><span data-stu-id="18ed6-164">In the networking properties, you will find information about the networking applied to the VM including the **Virtual network/subnet**.</span></span> <span data-ttu-id="18ed6-165">这是一个可单击的链接, 可用于访问资源。</span><span class="sxs-lookup"><span data-stu-id="18ed6-165">This is a clickable link to get to the resource.</span></span> <span data-ttu-id="18ed6-166">单击它以打开虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="18ed6-166">Click it to open the virtual network.</span></span> <span data-ttu-id="18ed6-167">此外, VM 的**概述**面板中_也_提供了此链接。</span><span class="sxs-lookup"><span data-stu-id="18ed6-167">This link is _also_ available on the **Overview** panel of the VM.</span></span> <span data-ttu-id="18ed6-168">这两种方法都将打开虚拟网络的**概述**。</span><span class="sxs-lookup"><span data-stu-id="18ed6-168">Either of these will open the **Overview** of the virtual network.</span></span>

1. <span data-ttu-id="18ed6-169">在 "**设置**" 部分中, 选择 "**子网**" 项。</span><span class="sxs-lookup"><span data-stu-id="18ed6-169">In the **Settings** section, select the **Subnets** item.</span></span>

1. <span data-ttu-id="18ed6-170">在前面创建 VM + 网络时, 应定义单个子网 (默认)。</span><span class="sxs-lookup"><span data-stu-id="18ed6-170">We should have a single subnet defined (default) from when we created the VM + network earlier.</span></span> <span data-ttu-id="18ed6-171">单击列表中的项目以打开详细信息。</span><span class="sxs-lookup"><span data-stu-id="18ed6-171">Click the item in the list to open the details.</span></span>

1. <span data-ttu-id="18ed6-172">单击 "**网络安全组**" 条目。</span><span class="sxs-lookup"><span data-stu-id="18ed6-172">Click the **Network security group** entry.</span></span>

1. <span data-ttu-id="18ed6-173">选择您的新安全组: "**测试部-nsg2**"。</span><span class="sxs-lookup"><span data-stu-id="18ed6-173">Select your new security group: **test-vp-nsg2**.</span></span>

1. <span data-ttu-id="18ed6-174">单击 "**保存**" 以保存更改。</span><span class="sxs-lookup"><span data-stu-id="18ed6-174">Click **Save** to save the change.</span></span> <span data-ttu-id="18ed6-175">将需要一分钟才能应用到网络。</span><span class="sxs-lookup"><span data-stu-id="18ed6-175">It will take a minute to apply to the network.</span></span>

## <a name="verify-the-rules"></a><span data-ttu-id="18ed6-176">验证规则</span><span class="sxs-lookup"><span data-stu-id="18ed6-176">Verify the rules</span></span>

<span data-ttu-id="18ed6-177">让我们验证更改。</span><span class="sxs-lookup"><span data-stu-id="18ed6-177">Let's validate the change.</span></span>

1. <span data-ttu-id="18ed6-178">切换回虚拟机的**概述**面板。</span><span class="sxs-lookup"><span data-stu-id="18ed6-178">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="18ed6-179">你可以在 "**所有资源**" 下找到 VM。</span><span class="sxs-lookup"><span data-stu-id="18ed6-179">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="18ed6-180">选择 "**设置**" 部分中的 "**网络**" 项。</span><span class="sxs-lookup"><span data-stu-id="18ed6-180">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="18ed6-181">在网络的**概述**面板中, 有一个用于**有效安全规则**的链接, 可快速向你展示规则的评估方式。</span><span class="sxs-lookup"><span data-stu-id="18ed6-181">In the **Overview** panel for the network, there is a link for **Effective security rules** that will quickly show you how rules are going to be evaluated.</span></span> <span data-ttu-id="18ed6-182">单击该链接打开分析并确保看到您的 FTP 规则。</span><span class="sxs-lookup"><span data-stu-id="18ed6-182">Click the link to open the analysis and make sure you see your FTP rule.</span></span>

    ![显示我们的网络的有效安全规则的屏幕截图。](../media/8-effective-rules.png)

1. <span data-ttu-id="18ed6-184">此规则将允许您连接到 FTP 服务器;如果我们添加了 ftp worker 角色和配置的文件夹, 则可以使用 ftp 客户端连接到服务器。</span><span class="sxs-lookup"><span data-stu-id="18ed6-184">This rule would let you connect to an FTP server; if we had added the FTP worker role and configured folders, you would be able to use an FTP client to connect to the server.</span></span>

## <a name="one-more-thing"></a><span data-ttu-id="18ed6-185">另一件事</span><span class="sxs-lookup"><span data-stu-id="18ed6-185">One more thing</span></span>

<span data-ttu-id="18ed6-186">安全规则的获取权限非常困难。</span><span class="sxs-lookup"><span data-stu-id="18ed6-186">Security rules are tricky to get right.</span></span> <span data-ttu-id="18ed6-187">我们实际上在应用此新安全组时出错了, 我们丢失了远程桌面访问!</span><span class="sxs-lookup"><span data-stu-id="18ed6-187">We actually made a mistake when we applied this new security group - we lost our Remote Desktop access!</span></span> <span data-ttu-id="18ed6-188">若要解决此问题, 可以向安全组添加另一条规则以支持 RDP 访问。</span><span class="sxs-lookup"><span data-stu-id="18ed6-188">To fix this, you can add another rule to the security group to support RDP access.</span></span> <span data-ttu-id="18ed6-189">请务必将规则的入站 tcp/ip 地址限制为您拥有的。</span><span class="sxs-lookup"><span data-stu-id="18ed6-189">Make sure to restrict the inbound TCP/IP addresses for the rule to be the ones you own.</span></span>

> [!WARNING]
> <span data-ttu-id="18ed6-190">始终确保锁定用于管理访问的端口。</span><span class="sxs-lookup"><span data-stu-id="18ed6-190">Always make sure to lock down ports used for administrative access.</span></span> <span data-ttu-id="18ed6-191">更好的方法是创建 VPN 以将虚拟网络链接到专用网络, 并只允许来自该地址范围的 RDP 或 SSH 请求。</span><span class="sxs-lookup"><span data-stu-id="18ed6-191">An even better approach is to create a VPN to link the virtual network to your private network and only allow RDP or SSH requests from that address range.</span></span> <span data-ttu-id="18ed6-192">您还可以将 RDP 使用的端口更改为除默认值3389之外的其他内容。</span><span class="sxs-lookup"><span data-stu-id="18ed6-192">You can also change the port used by RDP to be something other than the default 3389.</span></span> <span data-ttu-id="18ed6-193">请注意, 更改端口不足以阻止攻击, 只是使其难以发现。</span><span class="sxs-lookup"><span data-stu-id="18ed6-193">Keep in mind that changing ports is not sufficient to stop attacks, it simply makes it a little harder to discover.</span></span>