 <span data-ttu-id="5ae76-101">您的 PIO 要将虚拟机设置为充当本地媒体插座的 web 资源。</span><span class="sxs-lookup"><span data-stu-id="5ae76-101">Your PIO wants to set up a virtual machine to serve as a web resource for local media outlets.</span></span> <span data-ttu-id="5ae76-102">必须确保此虚拟机受到保护, 因为这样可以防止未经授权的访问。</span><span class="sxs-lookup"><span data-stu-id="5ae76-102">It is imperative that this virtual machine is as protected as it can be to prevent unauthorized access.</span></span> <span data-ttu-id="5ae76-103">作为安全配置文件的一部分, 您希望在此 VM 上实施更新管理, 以确保它始终保持最新的安全修补程序的最新状态。</span><span class="sxs-lookup"><span data-stu-id="5ae76-103">As part of your security profile, you want to implement Update Management on this VM so that you can ensure that it is always up-to-date with the latest security patches.</span></span> 

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-virtual-machine"></a><span data-ttu-id="5ae76-104">创建虚拟机</span><span class="sxs-lookup"><span data-stu-id="5ae76-104">Create a virtual machine</span></span>

<span data-ttu-id="5ae76-105">在这里, 将创建一个新的虚拟机, 以充当本地媒体的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="5ae76-105">Here you will create a new virtual machine to serve as a web server for the local media.</span></span>

1. <span data-ttu-id="5ae76-106">打开[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="5ae76-106">Open the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).</span></span>
2. <span data-ttu-id="5ae76-107">在左侧导航窗格中, 单击 "**创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-107">In the left navigation pane, click **Create a resource**.</span></span>
3. <span data-ttu-id="5ae76-108">在**新**窗格中, 单击 " **Windows Server 2016 VM**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-108">In the **New** pane, click **Windows Server 2016 VM**.</span></span>
4. <span data-ttu-id="5ae76-109">在 "**基本**" 窗格中按如下所示输入数据。</span><span class="sxs-lookup"><span data-stu-id="5ae76-109">In the **Basics** pane enter data as shown below.</span></span> <span data-ttu-id="5ae76-110">您可以选择自己的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="5ae76-110">You can choose your own Username and Password.</span></span> <span data-ttu-id="5ae76-111">将订阅方法更改为, 或者免费试用或按需付费。</span><span class="sxs-lookup"><span data-stu-id="5ae76-111">Change the subscription method to, either Free Trial or Pay-As-You-Go.</span></span> <span data-ttu-id="5ae76-112">为 "位置" 选择 "**美国东部**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-112">Select **East US** for location.</span></span> 
5. <span data-ttu-id="5ae76-113">创建新的资源组**RFD**</span><span class="sxs-lookup"><span data-stu-id="5ae76-113">Create new resource group **RFD**</span></span>

<span data-ttu-id="5ae76-114">![创建虚拟机基础知识](../media/3-create-mediawebserver-basics-edited.png "创建虚拟机基础知识")</span><span class="sxs-lookup"><span data-stu-id="5ae76-114">![Create VM Basics](../media/3-create-mediawebserver-basics-edited.png "Create VM Basics")</span></span>

6. <span data-ttu-id="5ae76-115">单击 "大小" 字段中的 "**更改大小**", 然后选择 " **B2s**", 然后单击 "**选择**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-115">Click **Change size** in the size field and choose **B2s**, and then click **Select**.</span></span>
7. <span data-ttu-id="5ae76-116">在 "**入站端口角色**" 部分中, 您需要进行的唯一更改是, 选择 "允许**公用入站端口**中的**选定端口**" 字段。</span><span class="sxs-lookup"><span data-stu-id="5ae76-116">In the **INBOUND PORT ROLES** section, the only change you need to make is, choose **Allow selected ports** in the **Public inbound ports** field.</span></span> <span data-ttu-id="5ae76-117">选择 "HTTP"、"HTTPS" 和 "RDP", 如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ae76-117">Select HTTP, HTTPS, and RDP as shown below.</span></span>

<span data-ttu-id="5ae76-118">![选择公用入站端口](../media/3-public-inbound-ports-edited.png "选择公用入站端口")</span><span class="sxs-lookup"><span data-stu-id="5ae76-118">![Select Public Inbound Ports](../media/3-public-inbound-ports-edited.png "Select Public Inbound Ports")</span></span>

8. <span data-ttu-id="5ae76-119">单击 "**审阅 + 创建**", 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-119">Click **Review + create** and then click **Create**.</span></span> <span data-ttu-id="5ae76-120">等待创建 VM。</span><span class="sxs-lookup"><span data-stu-id="5ae76-120">Wait for the VM to be created.</span></span> <span data-ttu-id="5ae76-121">您可以单击门户右上角的响铃图标来监视进度。</span><span class="sxs-lookup"><span data-stu-id="5ae76-121">You can click the Bell icon in the upper right corner of the portal to monitor the progress.</span></span>

## <a name="onboard-update-manager-to-the-vm"></a><span data-ttu-id="5ae76-122">到 VM 的板载更新管理器</span><span class="sxs-lookup"><span data-stu-id="5ae76-122">Onboard Update Manager to the VM</span></span>

<span data-ttu-id="5ae76-123">在这里, 你将在刚才创建的虚拟机上启用更新管理器。</span><span class="sxs-lookup"><span data-stu-id="5ae76-123">Here you'll enable Update Manager on the virtual machine you just created.</span></span>

1. <span data-ttu-id="5ae76-124">在左窗格中, 单击 "**虚拟机**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-124">In the left pane, click **Virtual machines**.</span></span>
2. <span data-ttu-id="5ae76-125">在 "**虚拟机**" 窗格中, 从列表中选择虚拟机。</span><span class="sxs-lookup"><span data-stu-id="5ae76-125">In the **Virtual machines** pane, select the virtual machine from the list.</span></span> <span data-ttu-id="5ae76-126">在此示例中, 选择 " **MediaWebServer**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-126">In this example, select **MediaWebServer**.</span></span>
3. <span data-ttu-id="5ae76-127">在 "MediaWebServer" 窗格中, 向下滚动到 "**操作**" 列表, 然后单击 "**更新管理**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-127">In the MediaWebServer pane, scroll down the list to **Operations**, and then click **Update management**.</span></span>
4. <span data-ttu-id="5ae76-128">在 "**更新管理**" 窗格中, 确保选择了 "**为此 VM 启用**" 单选按钮。</span><span class="sxs-lookup"><span data-stu-id="5ae76-128">In the **Update Management** pane, ensure that the **Enable for this VM** radio button is selected.</span></span> <span data-ttu-id="5ae76-129">请注意, 将创建默认的**Log Analytics workspace**和**Automation 帐户**。</span><span class="sxs-lookup"><span data-stu-id="5ae76-129">Note that a default **Log Analytics workspace** and **Automation account** will be created.</span></span> <span data-ttu-id="5ae76-130">接受其余的默认值, 然后单击 "**启用**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-130">Accept the remaining defaults, and then click **Enable**.</span></span>
5. <span data-ttu-id="5ae76-131">在左上角, 单击通知电铃并等待部署完成。</span><span class="sxs-lookup"><span data-stu-id="5ae76-131">In the upper left corner click the Notification bell and wait for deployment to finish.</span></span>
6. <span data-ttu-id="5ae76-132">更新管理部署完成后, 将显示 "更新管理" 菜单, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ae76-132">When Update Management deployment has completed, the Update Management menu will appear as shown below.</span></span>

<span data-ttu-id="5ae76-133">![完成更新管理部署](../media/3-update-management-deployment-complete-edited.png "完成更新管理部署")</span><span class="sxs-lookup"><span data-stu-id="5ae76-133">![Update Management Deployment Complete](../media/3-update-management-deployment-complete-edited.png "Update Management Deployment Complete")</span></span>

7. <span data-ttu-id="5ae76-134">等待至少15分钟, 同时更新管理配置虚拟机。</span><span class="sxs-lookup"><span data-stu-id="5ae76-134">Wait for at least 15 minutes while Update Management configures the virtual machine.</span></span>
8. <span data-ttu-id="5ae76-135">更新管理配置完成后, 将显示 "更新管理" 窗格, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ae76-135">When Update Management configuration is complete, the Update Management pane will appear as shown below.</span></span>

<span data-ttu-id="5ae76-136">![完成更新管理配置](../media/3-update-management-vm-configured-edited.png "完成更新管理配置")</span><span class="sxs-lookup"><span data-stu-id="5ae76-136">![Update Management Configuration Complete](../media/3-update-management-vm-configured-edited.png "Update Management Configuration Complete")</span></span>

9. <span data-ttu-id="5ae76-137">请注意,**合规**现已完成, 现已配置**失败的更新部署**计数器, 在此示例中, 更新管理已确定 Windows Server 的累积更新已可用。</span><span class="sxs-lookup"><span data-stu-id="5ae76-137">Note that **Compliance** is now complete, that the **Failed update deployments** counter is now configured, and that in this example, Update Management has identified that there is a Cumulative Update for Windows Server available.</span></span> <span data-ttu-id="5ae76-138">在 "累积更新" 通知的右侧, 在 "**信息链接**" 下有一个指向此累积更新的知识库文章的链接。</span><span class="sxs-lookup"><span data-stu-id="5ae76-138">To the right of the notification of the Cumulative Update, under **INFORMATION LINK** that there is a link to the knowledge base article for this Cumulative Update.</span></span> 

## <a name="examine-hybrid-worker-groups"></a><span data-ttu-id="5ae76-139">检查混合辅助角色组</span><span class="sxs-lookup"><span data-stu-id="5ae76-139">Examine Hybrid Worker Groups</span></span>

1. <span data-ttu-id="5ae76-140">在左侧导航窗格中, 单击 "**所有资源**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-140">In the left navigation pane, click **All resources**.</span></span>
1. <span data-ttu-id="5ae76-141">在 "**所有资源**" 窗格中, 检查 "**类型**" 列以查找 "**自动化" 帐户**类型的资源, 然后单击 "自动化" 帐户。</span><span class="sxs-lookup"><span data-stu-id="5ae76-141">In the **All resources** pane, examine the **TYPE** column to find the resource of type **Automation Account**, and then click the Automation account.</span></span>
1. <span data-ttu-id="5ae76-142">在 "自动化帐户" 窗格中, 向下滚动到 "**流程自动化**" 部分, 然后在其中单击 "**混合工作人员组**"。</span><span class="sxs-lookup"><span data-stu-id="5ae76-142">In the Automation account pane, scroll down to the **Process Automation** section and in there, click **Hybrid worker groups**.</span></span>
1. <span data-ttu-id="5ae76-143">在 "**混合辅助角色组**" 窗格中, 单击 "**系统混合工作器组**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5ae76-143">In the **Hybrid worker groups** pane click the **System hybrid worker groups** tab.</span></span>
1. <span data-ttu-id="5ae76-144">请注意, 您创建的虚拟机如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ae76-144">Note that the virtual machine you created is listed as shown below.</span></span> 

<span data-ttu-id="5ae76-145">![混合辅助角色组](../media/3-hybrid-worker-group.png "混合辅助角色组")</span><span class="sxs-lookup"><span data-stu-id="5ae76-145">![Hybrid Worker Group](../media/3-hybrid-worker-group.png "Hybrid Worker Group")</span></span>

