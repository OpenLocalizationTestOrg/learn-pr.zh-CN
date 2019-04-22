<span data-ttu-id="b0a49-101">你已在 Azure 中创建 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="b0a49-101">You have created a Linux VM in Azure.</span></span> <span data-ttu-id="b0a49-102">接下来要做的是, 将其配置为要迁移到 Azure 的任务。</span><span class="sxs-lookup"><span data-stu-id="b0a49-102">The next thing you’ll do is configure it for the tasks we want to move to Azure.</span></span>

<span data-ttu-id="b0a49-103">除非已将站点到站点 VPN 设置为 azure, 否则你的 azure vm 将无法从你的本地网络访问。</span><span class="sxs-lookup"><span data-stu-id="b0a49-103">Unless you’ve set up a site-to-site VPN to Azure, your Azure VMs won’t be accessible from your local network.</span></span> <span data-ttu-id="b0a49-104">如果只是开始使用 Azure, 您不太可能拥有工作的站点到站点 VPN。</span><span class="sxs-lookup"><span data-stu-id="b0a49-104">If you’re just getting started with Azure, it’s unlikely that you have a working site-to-site VPN.</span></span> <span data-ttu-id="b0a49-105">那么, 如何才能连接到虚拟机呢？</span><span class="sxs-lookup"><span data-stu-id="b0a49-105">So how can you connect to the virtual machine?</span></span>

## <a name="azure-vm-ip-addresses"></a><span data-ttu-id="b0a49-106">Azure VM IP 地址</span><span class="sxs-lookup"><span data-stu-id="b0a49-106">Azure VM IP addresses</span></span>

<span data-ttu-id="b0a49-107">正如我们看到的, Azure 虚拟机在虚拟网络上进行通信。</span><span class="sxs-lookup"><span data-stu-id="b0a49-107">As we saw a moment ago, Azure VMs communicate on a virtual network.</span></span> <span data-ttu-id="b0a49-108">他们还可以为其分配一个可选的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b0a49-108">They can also have an optional public IP address assigned to them.</span></span> <span data-ttu-id="b0a49-109">通过公用 IP, 我们可以通过 Internet 与 VM 进行交互。</span><span class="sxs-lookup"><span data-stu-id="b0a49-109">With a public IP, we can interact with the VM over the Internet.</span></span> <span data-ttu-id="b0a49-110">此外, 我们还可以设置将本地网络连接到 Azure 的虚拟专用网络 (VPN), 让我们能够安全地连接到 VM, 而不公开公共 IP。</span><span class="sxs-lookup"><span data-stu-id="b0a49-110">Alternatively, we can set up a virtual private network (VPN) that connects our on-premises network to Azure - letting us securely connect to the VM without exposing a public IP.</span></span> <span data-ttu-id="b0a49-111">此方法在其他模块中进行了介绍, 如果您有兴趣浏览该选项, 则会对其进行全面记录。</span><span class="sxs-lookup"><span data-stu-id="b0a49-111">This approach is covered in another module and is fully documented if you are interested in exploring that option.</span></span>

<span data-ttu-id="b0a49-112">默认情况下, Azure 中的公用 IP 地址是动态分配的。</span><span class="sxs-lookup"><span data-stu-id="b0a49-112">Public IP addresses in Azure are dynamically allocated by default.</span></span> <span data-ttu-id="b0a49-113">这意味着 ip 地址可以随着时间的推移而变化 ip 地址分配在重新启动 VM 时发生。</span><span class="sxs-lookup"><span data-stu-id="b0a49-113">That means the IP address can change over time - for VMs the IP address assignment happens when the VM is restarted.</span></span> <span data-ttu-id="b0a49-114">如果要直接连接到 ip 地址, 并且需要确保 ip 地址不会发生更改, 则可以使用更多的费用来分配静态地址。</span><span class="sxs-lookup"><span data-stu-id="b0a49-114">You can pay more to assign static addresses, if you want to connect directly to an IP address and need to ensure that the IP address will not change.</span></span>

<span data-ttu-id="b0a49-115">确认这些限制以及上述替代方法时, 我们将使用此模块中 VM 的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b0a49-115">Acknowledging these restrictions, and the alternatives described above, we will use the public IP address of the VM in this module.</span></span>

## <a name="connecting-to-the-vm-with-ssh"></a><span data-ttu-id="b0a49-116">使用 SSH 连接到 VM</span><span class="sxs-lookup"><span data-stu-id="b0a49-116">Connecting to the VM with SSH</span></span>

<span data-ttu-id="b0a49-117">若要通过 SSH 连接到 VM, 需要执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="b0a49-117">To connect to the VM via SSH, you need:</span></span>

- <span data-ttu-id="b0a49-118">VM 的公共 IP 地址</span><span class="sxs-lookup"><span data-stu-id="b0a49-118">the public IP address of the VM</span></span>
- <span data-ttu-id="b0a49-119">VM 上的本地帐户的用户名</span><span class="sxs-lookup"><span data-stu-id="b0a49-119">the username of the local account on the VM</span></span>
- <span data-ttu-id="b0a49-120">在该帐户中配置的公钥</span><span class="sxs-lookup"><span data-stu-id="b0a49-120">a public key configured in that account</span></span>
- <span data-ttu-id="b0a49-121">对相应私钥的访问权限</span><span class="sxs-lookup"><span data-stu-id="b0a49-121">access to the corresponding private key</span></span>
- <span data-ttu-id="b0a49-122">VM 上打开的端口22</span><span class="sxs-lookup"><span data-stu-id="b0a49-122">port 22 open on the VM</span></span>

<span data-ttu-id="b0a49-123">以前, 您生成了 SSH 密钥对, 并向 VM 配置添加了公钥, 并确保端口22已打开。</span><span class="sxs-lookup"><span data-stu-id="b0a49-123">Previously, you generated an SSH key pair, and added the public key to the VM configuration, and ensured that port 22 was open.</span></span>

<span data-ttu-id="b0a49-124">在下一个设备中, 你将使用此信息, 在 VM 上使用 SSH 打开安全终端。</span><span class="sxs-lookup"><span data-stu-id="b0a49-124">In the next unit, you'll use this information to open a secure terminal on the VM using SSH.</span></span>

<span data-ttu-id="b0a49-125">终端打开后, 您可以访问所有标准 Linux 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="b0a49-125">Once the terminal is open, you have access to all of the standard Linux command-line tools.</span></span>

<span data-ttu-id="b0a49-126">接下来, 让我们使用 SSH 连接到 VM。</span><span class="sxs-lookup"><span data-stu-id="b0a49-126">Next, let's connect to the VM using SSH.</span></span>