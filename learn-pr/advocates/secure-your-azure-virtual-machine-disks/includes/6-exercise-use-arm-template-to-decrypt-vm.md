<span data-ttu-id="e2534-101">在此单元中, 你将使用 Azure 资源管理器模板来解密我们之前创建的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="e2534-101">In this unit, you'll use an Azure Resource Manager template to decrypt our Windows VM we created earlier.</span></span> <span data-ttu-id="e2534-102">我们在 Windows VM 上加密了 OS 驱动器。</span><span class="sxs-lookup"><span data-stu-id="e2534-102">We encrypted the OS drive on our Windows VM.</span></span> <span data-ttu-id="e2534-103">但是, OS 驱动器上不包含任何机密信息, 因此我们可以将其保留为未加密。</span><span class="sxs-lookup"><span data-stu-id="e2534-103">However, the OS drive won't have any confidential information on it, so we could leave it unencrypted.</span></span> <span data-ttu-id="e2534-104">让我们使用模板对 OS 驱动器进行解密。</span><span class="sxs-lookup"><span data-stu-id="e2534-104">Let's use a template to decrypt the OS drive.</span></span>

## <a name="decrypt-a-vm-using-an-azure-resource-manager-template"></a><span data-ttu-id="e2534-105">使用 Azure 资源管理器模板对 VM 进行解密</span><span class="sxs-lookup"><span data-stu-id="e2534-105">Decrypt a VM using an Azure Resource Manager template</span></span>

<span data-ttu-id="e2534-106">我们将使用 Microsoft 在 GitHub 上发布的模板, 该模板专门用于解密正在运行的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="e2534-106">We're going to use a template Microsoft has published on GitHub that is specifically designed to decrypt a running Windows VM.</span></span>

1. <span data-ttu-id="e2534-107">使用与激活沙盒时相同的帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="e2534-107">Sign into the [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) with the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="e2534-108">单击左侧边栏中**的 "创建资源**"。</span><span class="sxs-lookup"><span data-stu-id="e2534-108">Click **Create a Resource** in the left sidebar.</span></span>

1. <span data-ttu-id="e2534-109">在搜索框中键入**模板**。</span><span class="sxs-lookup"><span data-stu-id="e2534-109">Type **Template** in the search box.</span></span>

1. <span data-ttu-id="e2534-110">从生成的列表中选择 "**模板部署**", 然后单击 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="e2534-110">Select **Template Deployment** from the resulting list and click **Create**.</span></span>

    ![显示 "创建" 按钮选中的模板部署项目的屏幕截图](../media/6-create-template.png)

1. <span data-ttu-id="e2534-112">在 "**选择模板**" 搜索框中, 开始键入 "201-解密", 并选择 "201-不解密-不使用 aad 的 windows-vm-不安装-aad" 模板。</span><span class="sxs-lookup"><span data-stu-id="e2534-112">In the **Select a template** search box, start typing "201-decrypt" and select the "201-decrypt-running-windows-vm-without-aad" template.</span></span>

    ![显示 "选择模板" 搜索框和自动完成的屏幕截图](../media/6-custom-deployment.png)

1. <span data-ttu-id="e2534-114">单击 "**选择模板**" 以启动模板运行程序。</span><span class="sxs-lookup"><span data-stu-id="e2534-114">Click **Select Template** to launch the template runner.</span></span>

1. <span data-ttu-id="e2534-115">在 "设置" 视图中, 输入以下信息:</span><span class="sxs-lookup"><span data-stu-id="e2534-115">In the settings view, enter the following information:</span></span>
    - <span data-ttu-id="e2534-116">选择**订阅**的_Concierge 订阅_。</span><span class="sxs-lookup"><span data-stu-id="e2534-116">Select _Concierge Subscription_ for the **Subscription**.</span></span>
    - <span data-ttu-id="e2534-117">选择沙盒资源组<rgn>沙盒 RG</rgn>。</span><span class="sxs-lookup"><span data-stu-id="e2534-117">Select the sandbox resource group <rgn>Sandbox RG</rgn>.</span></span> <span data-ttu-id="e2534-118">这也将自动选择该区域。</span><span class="sxs-lookup"><span data-stu-id="e2534-118">This will auto-select the region as well.</span></span>
    - <span data-ttu-id="e2534-119">为**VM 名称**输入 "fmdata-vm01"。</span><span class="sxs-lookup"><span data-stu-id="e2534-119">Enter "fmdata-vm01" for the **VM Name**.</span></span>
    - <span data-ttu-id="e2534-120">将**卷类型**保留为 "_全部_"。</span><span class="sxs-lookup"><span data-stu-id="e2534-120">Leave the **Volume Type** as _All_.</span></span>

1. <span data-ttu-id="e2534-121">选中 "**我同意条款和条件**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="e2534-121">Select the **I agree to the terms and conditions** check box.</span></span>
1. <span data-ttu-id="e2534-122">单击 "**购买**" 以运行模板。</span><span class="sxs-lookup"><span data-stu-id="e2534-122">Click **Purchase** to run the template.</span></span> <span data-ttu-id="e2534-123">请注意, 此按钮没有成本-它是一个标准按钮。</span><span class="sxs-lookup"><span data-stu-id="e2534-123">Note that there is no cost to this - it's a standard button.</span></span>

<span data-ttu-id="e2534-124">部署可能需要几分钟时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="e2534-124">The deployment may take a few minutes to complete.</span></span>

## <a name="verify-the-encryption-status-of-the-vm"></a><span data-ttu-id="e2534-125">验证 VM 的加密状态</span><span class="sxs-lookup"><span data-stu-id="e2534-125">Verify the encryption status of the VM</span></span>

1. <span data-ttu-id="e2534-126">在 Azure 门户的边栏中, 单击 "**虚拟机**", 然后选择您**的 VM fmdata-vm01**。</span><span class="sxs-lookup"><span data-stu-id="e2534-126">In the sidebar of the Azure portal, click **Virtual machines** and select your VM **fmdata-vm01**.</span></span> <span data-ttu-id="e2534-127">或者, 您可以从**所有资源**按名称搜索 VM。</span><span class="sxs-lookup"><span data-stu-id="e2534-127">Alternatively, you can search for your VM by name from **All Resources**.</span></span>

1. <span data-ttu-id="e2534-128">在**虚拟机**边栏上的 "**设置**" 下, 单击 "**磁盘**"。</span><span class="sxs-lookup"><span data-stu-id="e2534-128">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="e2534-129">在**磁盘**边栏上, 请注意, OS 磁盘加密状态现已**禁用**。</span><span class="sxs-lookup"><span data-stu-id="e2534-129">On the **Disks** blade, notice the OS disk encryption status is now **Disabled**.</span></span>
