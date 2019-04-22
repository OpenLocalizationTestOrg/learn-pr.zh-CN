<span data-ttu-id="b78f6-101">请记住, 我们的目标是将运行 Apache 的现有 Linux 服务器移动到 Azure。</span><span class="sxs-lookup"><span data-stu-id="b78f6-101">Recall that our goal is to move an existing Linux server running Apache to Azure.</span></span> <span data-ttu-id="b78f6-102">我们将首先创建 Ubuntu Linux 服务器。</span><span class="sxs-lookup"><span data-stu-id="b78f6-102">We'll start by creating an Ubuntu Linux server.</span></span>

## <a name="create-a-new-linux-virtual-machine"></a><span data-ttu-id="b78f6-103">创建新的 Linux 虚拟机</span><span class="sxs-lookup"><span data-stu-id="b78f6-103">Create a new Linux virtual machine</span></span>

<span data-ttu-id="b78f6-104">我们可以使用 azure 门户、azure CLI 或 azure PowerShell 创建 Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b78f6-104">We can create Linux VMs with the Azure portal, the Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="b78f6-105">从 Azure 开始时, 最简单的方法是使用门户, 因为它将引导您完成所需的信息, 并在创建过程中提供提示和有用的消息:</span><span class="sxs-lookup"><span data-stu-id="b78f6-105">The easiest approach when you are starting with Azure is to use the portal because it walks you through the required information and provides hints and helpful messages during the creation:</span></span>

1. <span data-ttu-id="b78f6-106">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="b78f6-106">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="b78f6-107">单击 Azure 门户左上角的 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="b78f6-107">Click **Create a resource** in the upper-left corner of the Azure portal.</span></span>

1. <span data-ttu-id="b78f6-108">在搜索框中, 输入**Ubuntu 服务器**以查看可用的不同版本。</span><span class="sxs-lookup"><span data-stu-id="b78f6-108">In the search box, enter  **Ubuntu Server** to see the different versions available.</span></span> <span data-ttu-id="b78f6-109">从显示的列表中选择 " **Ubuntu Server 18.04 LTS** "。</span><span class="sxs-lookup"><span data-stu-id="b78f6-109">Select **Ubuntu Server 18.04 LTS** from the presented list.</span></span>

1. <span data-ttu-id="b78f6-110">单击 "**创建**" 按钮开始配置 VM。</span><span class="sxs-lookup"><span data-stu-id="b78f6-110">Click the **Create** button to start configuring the VM.</span></span>

## <a name="configure-the-vm-settings"></a><span data-ttu-id="b78f6-111">配置虚拟机设置</span><span class="sxs-lookup"><span data-stu-id="b78f6-111">Configure the VM settings</span></span>

<span data-ttu-id="b78f6-112">门户中的 VM 创建体验以一种向导格式显示, 以引导您完成 VM 的所有配置区域。</span><span class="sxs-lookup"><span data-stu-id="b78f6-112">The VM creation experience in the portal is presented in a wizard format to walk you through all the configuration areas for the VM.</span></span> <span data-ttu-id="b78f6-113">单击 "**下一步**" 按钮将转到下一个可配置的部分。</span><span class="sxs-lookup"><span data-stu-id="b78f6-113">Clicking the **Next** button will take you to the next configurable section.</span></span> <span data-ttu-id="b78f6-114">但是, 您可以在中的各节之间移动, 这些选项卡将在标识每个部件的顶部运行。</span><span class="sxs-lookup"><span data-stu-id="b78f6-114">However, you can move between the sections at will with the tabs running across the top that identify each part.</span></span>

![显示初始创建 Ubuntu 服务器计算机的虚拟机薄片的 Azure 门户屏幕截图。](../media/3-azure-portal-create-vm.png)

<span data-ttu-id="b78f6-116">一旦您填写了所有必需的选项 (用红色星号标识), 您就可以跳过向导体验的其余部分, 并通过底部的 "**审阅 + 创建**" 按钮开始创建 VM。</span><span class="sxs-lookup"><span data-stu-id="b78f6-116">Once you fill in all the required options (identified with red asterisks), you can skip the remainder of the wizard experience and start creating the VM through the **Review + Create** button at the bottom.</span></span>

<span data-ttu-id="b78f6-117">我们将从 "**基础知识**" 部分开始。</span><span class="sxs-lookup"><span data-stu-id="b78f6-117">We'll start with the **Basics** section.</span></span> <span data-ttu-id="b78f6-118">这些说明适用于沙盒门户。</span><span class="sxs-lookup"><span data-stu-id="b78f6-118">These instructions are for the Sandbox portal.</span></span> <span data-ttu-id="b78f6-119">如果你使用的是其他 Azure 门户帐户, 你可能需要相应地调整一些详细信息。</span><span class="sxs-lookup"><span data-stu-id="b78f6-119">If you are using another Azure portal account, you may need to adapt some details accordingly.</span></span>

### <a name="configure-basic-vm-settings"></a><span data-ttu-id="b78f6-120">配置基本虚拟机设置</span><span class="sxs-lookup"><span data-stu-id="b78f6-120">Configure basic VM settings</span></span>

1. <span data-ttu-id="b78f6-121">对于**订阅**, 默认情况下应为您选择沙盒订阅。</span><span class="sxs-lookup"><span data-stu-id="b78f6-121">For **Subscription**, the sandbox subscription should be selected for you by default.</span></span>

1. <span data-ttu-id="b78f6-122">对于**资源组**, 默认情况下应为您选择名称为**<rgn>[沙盒资源组名称]</rgn>** 的资源组。</span><span class="sxs-lookup"><span data-stu-id="b78f6-122">For **Resource group**, the resource group with the name **<rgn>[sandbox resource group name]</rgn>** should be selected for you by default.</span></span>

1. <span data-ttu-id="b78f6-123">在 "**实例详细信息**" 部分, 输入您的 web 服务器 VM 的名称, 例如**eus-vm1**。</span><span class="sxs-lookup"><span data-stu-id="b78f6-123">In the **INSTANCE DETAILS** section, enter a name for your web server VM, such as **test-web-eus-vm1**.</span></span> <span data-ttu-id="b78f6-124">这表示环境 (**测试**)、角色 (**web**)、位置 (**东 US**)、服务 (**vm**) 和实例号 (**1**)。</span><span class="sxs-lookup"><span data-stu-id="b78f6-124">This indicates the environment (**test**), the role (**web**), location (**East US**), service (**vm**), and instance number (**1**).</span></span>
    - <span data-ttu-id="b78f6-125">我们认为, 最佳做法是对资源名称进行标准化, 以便您可以快速确定其用途。</span><span class="sxs-lookup"><span data-stu-id="b78f6-125">It's considered best practice to standardize your resource names, so you can quickly identify their purpose.</span></span> <span data-ttu-id="b78f6-126">Linux VM 名称必须介于1到64个字符之间, 并且由数字、字母和短划线组成。</span><span class="sxs-lookup"><span data-stu-id="b78f6-126">Linux VM names must be between 1 and 64 characters and be comprised of numbers, letters, and dashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b78f6-127">当您在每个自由文本字段中更改设置和选项卡时, Azure 将自动验证每个值, 并在其正常时在其旁边放置绿色复选标记。</span><span class="sxs-lookup"><span data-stu-id="b78f6-127">As you change settings and tab out of each free-text field, Azure will validate each value automatically and place a green check mark next to it when it's good.</span></span> <span data-ttu-id="b78f6-128">您可以将鼠标指针悬停在错误指示器上方, 以获取有关它发现的问题的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b78f6-128">You can hover your mouse pointer over error indicators to get more information on issues it discovers.</span></span>

1. <span data-ttu-id="b78f6-129">选择一个位置。</span><span class="sxs-lookup"><span data-stu-id="b78f6-129">Select a location.</span></span>

    <!-- Resource selection -->  
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="b78f6-130">将**可用性选项**设置为 "**无需任何基础结构冗余**"。</span><span class="sxs-lookup"><span data-stu-id="b78f6-130">Set **Availability options** to **No infrastructure redundancy required**.</span></span> <span data-ttu-id="b78f6-131">此选项可用于通过将多个虚拟机作为一组进行分组以处理计划内或计划外的维护事件或中断, 从而确保虚拟机高度可用。</span><span class="sxs-lookup"><span data-stu-id="b78f6-131">This option can be used to ensure the VM is highly available by grouping multiple VMs together as a set to deal with planned or unplanned maintenance events or outages.</span></span> <span data-ttu-id="b78f6-132">在本练习中, 我们将不需要此服务。</span><span class="sxs-lookup"><span data-stu-id="b78f6-132">For this exercise we will not need this service.</span></span>

1. <span data-ttu-id="b78f6-133">确保将图像设置为**Ubuntu Server 18.04 LTS**。</span><span class="sxs-lookup"><span data-stu-id="b78f6-133">Ensure that the image is set to **Ubuntu Server 18.04 LTS**.</span></span> <span data-ttu-id="b78f6-134">您可以打开下拉列表以查看所有可用选项。</span><span class="sxs-lookup"><span data-stu-id="b78f6-134">You can open the drop-down list to see all the options available.</span></span>

1. <span data-ttu-id="b78f6-135">**Size**字段不是直接可编辑的, 并且具有**DS2_v3**默认大小, 这是通用计算选择之一。</span><span class="sxs-lookup"><span data-stu-id="b78f6-135">The **Size** field is not directly editable and has a **DS2_v3** default size, which is one of the general-purpose computing selections.</span></span> <span data-ttu-id="b78f6-136">此选项对于公共 web 服务器而言非常理想, 但用于演示单击 "**更改大小**" 链接以浏览其他 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b78f6-136">This choice is perfect for a public web server, but for demonstration click the **Change size** link to explore other VM sizes.</span></span> <span data-ttu-id="b78f6-137">请注意, 生成的对话框允许您基于 # of **vCPUs**、 **Name**和**Disk Type**进行筛选。</span><span class="sxs-lookup"><span data-stu-id="b78f6-137">Note that the resulting dialog allows you to filter based on **# of vCPUs**, **Name**, and **Disk Type**.</span></span> <span data-ttu-id="b78f6-138">选择相同的**DS2_v3**选项, 它为您提供了两个具有 8 GB RAM 的 vCPUs。</span><span class="sxs-lookup"><span data-stu-id="b78f6-138">Select the same **DS2_v3** choice, which gives you two vCPUs with 8 GB of RAM.</span></span>

1. <span data-ttu-id="b78f6-139">若要转到 "**管理员访问**" 部分, 请在 "**身份验证类型**" 中选择 " **SSH 公钥**" 选项。</span><span class="sxs-lookup"><span data-stu-id="b78f6-139">Moving on to the **ADMINISTRATOR ACCESS** section, for **Authentication type** select the **SSH public key** option.</span></span>

1. <span data-ttu-id="b78f6-140">输入你将用于使用 SSH 登录的**用户名**。</span><span class="sxs-lookup"><span data-stu-id="b78f6-140">Enter a **username** you'll use to sign in with SSH.</span></span> <span data-ttu-id="b78f6-141">选择你可以记住或记下它的内容。</span><span class="sxs-lookup"><span data-stu-id="b78f6-141">Choose something you can remember or write it down.</span></span>

1. <span data-ttu-id="b78f6-142">从您在上一个设备中创建的公钥文件中复制 SSH 密钥, 并将其粘贴到**SSH 公钥**字段中。</span><span class="sxs-lookup"><span data-stu-id="b78f6-142">Copy the SSH key from your public key file you created in the previous unit and paste it into the **SSH public key** field.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b78f6-143">将公钥复制到 Azure 门户中时, 请确保不添加任何其他空格或换行符。</span><span class="sxs-lookup"><span data-stu-id="b78f6-143">When you copy the public key into the Azure portal, make sure not to add any additional whitespace or line-feed characters.</span></span>

1. <span data-ttu-id="b78f6-144">在 "**入站端口规则**" 部分, 选择 "**允许选择的端口**"。</span><span class="sxs-lookup"><span data-stu-id="b78f6-144">In the **INBOUND PORT RULES** section, first select **Allow selected ports**.</span></span> <span data-ttu-id="b78f6-145">由于这是 Linux VM, 因此我们希望能够远程使用 SSH 访问 VM。</span><span class="sxs-lookup"><span data-stu-id="b78f6-145">Since this is a Linux VM, we want to be able to access the VM using SSH remotely.</span></span> <span data-ttu-id="b78f6-146">如有必要, 滚动 "**选择入站端口**" 列表, 直到找到**SSH (22)** 并启用它。</span><span class="sxs-lookup"><span data-stu-id="b78f6-146">Scroll the **Select inbound ports** list if necessary until you find **SSH (22)** and enable it.</span></span>

    ![显示入站端口设置的 Azure 门户的屏幕截图, 如为 SSH 访问打开 Linux VM 所述。](../media/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a><span data-ttu-id="b78f6-148">为 VM 配置磁盘</span><span class="sxs-lookup"><span data-stu-id="b78f6-148">Configure disks for the VM</span></span>

1. <span data-ttu-id="b78f6-149">单击 "**下一步: 磁盘 >** " 移动到 "**磁盘**" 部分。</span><span class="sxs-lookup"><span data-stu-id="b78f6-149">Click **Next: Disks >** to move to the **Disks** section.</span></span>

1. <span data-ttu-id="b78f6-150">为**OS 磁盘类型**选择 "**高级 SSD** "。</span><span class="sxs-lookup"><span data-stu-id="b78f6-150">Choose **Premium SSD** for the **OS disk type**.</span></span>

### <a name="create-a-data-disk"></a><span data-ttu-id="b78f6-151">创建数据磁盘</span><span class="sxs-lookup"><span data-stu-id="b78f6-151">Create a data disk</span></span>

<span data-ttu-id="b78f6-152">回想一下, 我们将获取 OS 磁盘 (/dev/sda) 和临时磁盘 (/dev/sdb)。</span><span class="sxs-lookup"><span data-stu-id="b78f6-152">Recall that we will get an OS disk (/dev/sda) and a temporary disk (/dev/sdb).</span></span> <span data-ttu-id="b78f6-153">还可以添加数据磁盘:</span><span class="sxs-lookup"><span data-stu-id="b78f6-153">Let's add a data disk as well:</span></span>

1. <span data-ttu-id="b78f6-154">单击 "**数据磁盘**" 部分中的 "**创建并附加新磁盘**" 链接。</span><span class="sxs-lookup"><span data-stu-id="b78f6-154">Click the **Create and attach a new disk** link in the **DATA DISKS** section.</span></span>

    ![显示 "创建新磁盘" 边栏的 Azure 门户屏幕截图。](../media/3-add-data-disk.png)

1. <span data-ttu-id="b78f6-156">您可以采用所有默认值:**高级 SSD**、自动生成的名称、 **1023** GiB 的大小和**无 (空磁盘)** 作为**源类型**, 但请注意, 源类型是可以使用快照或 Azure Blob 存储创建 VHD 的位置。.</span><span class="sxs-lookup"><span data-stu-id="b78f6-156">You can take all the defaults: **Premium SSD**, the auto-generated name, size of **1023** GiB, and **None (empty disk)** for **Source type**, although notice that source type is where you could use a snapshot or Azure Blob storage to create a VHD.</span></span>

1. <span data-ttu-id="b78f6-157">单击 **"确定"** 以创建磁盘并返回到 "**数据磁盘**" 部分。</span><span class="sxs-lookup"><span data-stu-id="b78f6-157">Click **OK** to create the disk and go back to the **DATA DISKS** section.</span></span>

1. <span data-ttu-id="b78f6-158">现在, 第一行中应该有一个新磁盘。</span><span class="sxs-lookup"><span data-stu-id="b78f6-158">There should now be a new disk in the first row.</span></span>

    ![显示用于 VM 创建过程的新创建的数据磁盘行的 Azure 门户屏幕截图。](../media/3-new-disk.png)

## <a name="configure-the-network"></a><span data-ttu-id="b78f6-160">配置网络</span><span class="sxs-lookup"><span data-stu-id="b78f6-160">Configure the network</span></span>

1. <span data-ttu-id="b78f6-161">单击 "**下一步: 网络 >** " 移动到 "**网络**" 部分。</span><span class="sxs-lookup"><span data-stu-id="b78f6-161">Click **Next: Networking >** to move to the **Networking** section.</span></span>

1. <span data-ttu-id="b78f6-162">在我们已有其他组件的生产环境中, 您想要利用_现有_的虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="b78f6-162">In a production environment where we already have other components, you'd want to utilize an _existing_ virtual network.</span></span> <span data-ttu-id="b78f6-163">这样一来, 你的 VM 可以与解决方案中的其他云服务进行通信。</span><span class="sxs-lookup"><span data-stu-id="b78f6-163">That way, your VM can communicate with the other cloud services in your solution.</span></span> <span data-ttu-id="b78f6-164">如果尚未在此位置中定义任何一个, 则可以在此处创建并配置以下内容:</span><span class="sxs-lookup"><span data-stu-id="b78f6-164">If there isn't one defined in this location yet, you can create it here and configure the:</span></span>
    - <span data-ttu-id="b78f6-165">**地址空间**: 此网络可用的总 IPV4 空间。</span><span class="sxs-lookup"><span data-stu-id="b78f6-165">**Address space**: The overall IPV4 space available to this network.</span></span>
    - <span data-ttu-id="b78f6-166">**子网范围**: 要细分地址空间的第一个子网-它必须在定义的地址空间内。</span><span class="sxs-lookup"><span data-stu-id="b78f6-166">**Subnet range**: The first subnet to subdivide the address space - it must fit within the defined address space.</span></span> <span data-ttu-id="b78f6-167">创建 VNet 后, 可以添加其他子网。</span><span class="sxs-lookup"><span data-stu-id="b78f6-167">Once the VNet is created, you can add additional subnets.</span></span>

> [!NOTE]
> <span data-ttu-id="b78f6-168">默认情况下, Azure 将为你的 VM 创建虚拟网络、网络接口和公用 IP。</span><span class="sxs-lookup"><span data-stu-id="b78f6-168">By default, Azure will create a virtual network, network interface, and public IP for your VM.</span></span> <span data-ttu-id="b78f6-169">在创建虚拟机之后更改网络选项并不常用, 因此请务必仔细检查在 Azure 中创建的服务上的网络分配。</span><span class="sxs-lookup"><span data-stu-id="b78f6-169">It's not trivial to change the networking options after the VM has been created, so always double-check the network assignments on services you create in Azure.</span></span> <span data-ttu-id="b78f6-170">在本练习中, 默认值应正常运行。</span><span class="sxs-lookup"><span data-stu-id="b78f6-170">For this exercise, the defaults should work fine.</span></span>

## <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="b78f6-171">完成虚拟机的配置并创建映像</span><span class="sxs-lookup"><span data-stu-id="b78f6-171">Finish configuring the VM and create the image</span></span>

<span data-ttu-id="b78f6-172">其余选项具有合理的默认设置, 无需更改任何其他选项。</span><span class="sxs-lookup"><span data-stu-id="b78f6-172">The rest of the options have reasonable defaults, and there's no need to change any of them.</span></span> <span data-ttu-id="b78f6-173">如果愿意, 你可以浏览其他选项卡。</span><span class="sxs-lookup"><span data-stu-id="b78f6-173">You can explore the other tabs if you like.</span></span> <span data-ttu-id="b78f6-174">各个选项旁边都有`(i)`一个图标, 将显示一个帮助提示来说明该选项。</span><span class="sxs-lookup"><span data-stu-id="b78f6-174">The individual options have an `(i)` icon next to them that will show a help tip to explain the option.</span></span> <span data-ttu-id="b78f6-175">这是了解可用于配置 VM 的各种选项的好方法:</span><span class="sxs-lookup"><span data-stu-id="b78f6-175">This is a great way to learn about the various options you can use to configure the VM:</span></span>

1. <span data-ttu-id="b78f6-176">单击面板底部的 "**审阅 + 创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="b78f6-176">Click the **Review + create** button at the bottom of the panel.</span></span>

1. <span data-ttu-id="b78f6-177">系统将验证您的选项, 并提供有关正在创建的 VM 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b78f6-177">The system will validate your options and give you details about the VM being created.</span></span>

1. <span data-ttu-id="b78f6-178">单击 "**创建**" 以创建和部署 VM。</span><span class="sxs-lookup"><span data-stu-id="b78f6-178">Click **Create** to create and deploy the VM.</span></span> <span data-ttu-id="b78f6-179">Azure 仪表板将显示正在部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="b78f6-179">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="b78f6-180">这可能需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="b78f6-180">This may take several minutes.</span></span>

<span data-ttu-id="b78f6-181">在部署时, 让我们来看看我们可以使用此 VM 做什么。</span><span class="sxs-lookup"><span data-stu-id="b78f6-181">While that's deploying, let's look at what we can do with this VM.</span></span>
