<span data-ttu-id="5e425-101">我们了解了如何在 Azure 上部署服务之前估计你的成本, 但如果已部署了资源, 该怎么办？</span><span class="sxs-lookup"><span data-stu-id="5e425-101">We learned how to estimate your costs before you deploy services on Azure, but what if you already have resources deployed?</span></span> <span data-ttu-id="5e425-102">如何了解已累算的成本？</span><span class="sxs-lookup"><span data-stu-id="5e425-102">How do you get visibility into the costs you're already accruing?</span></span> <span data-ttu-id="5e425-103">如果我们已将以前的解决方案部署到 Azure, 并且现在想确保我们已正确调整虚拟机的大小并预测我们的费用, 我们该如何做呢？</span><span class="sxs-lookup"><span data-stu-id="5e425-103">If we had deployed our previous solution to Azure and now want to make sure that we've sized the virtual machines properly and predict how much our bill will be, how can we do this?</span></span> <span data-ttu-id="5e425-104">让我们来看一下 Azure 上的几个工具, 您可以使用这些工具来帮助您解决此问题。</span><span class="sxs-lookup"><span data-stu-id="5e425-104">Let's look at a few tools on Azure that you can use to help you solve this problem.</span></span>

## <a name="what-is-azure-advisor"></a><span data-ttu-id="5e425-105">什么是 Azure Advisor？</span><span class="sxs-lookup"><span data-stu-id="5e425-105">What is Azure Advisor?</span></span>

<span data-ttu-id="5e425-106">**azure Advisor**是一个内置于 azure 中的免费服务, 提供有关高可用性、安全性、性能和成本方面的建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-106">**Azure Advisor** is a free service built into Azure that provides recommendations on high availability, security, performance, and cost.</span></span> <span data-ttu-id="5e425-107">Advisor 分析已部署的服务, 并寻找在这四个领域改进环境的方法。</span><span class="sxs-lookup"><span data-stu-id="5e425-107">Advisor analyzes your deployed services and looks for ways to improve your environment across those four areas.</span></span> <span data-ttu-id="5e425-108">我们将重点介绍成本建议, 但你也需要花费一些时间来查看其他建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-108">We'll focus on the cost recommendations, but you'll want to take some time to review the other recommendations as well.</span></span>

<span data-ttu-id="5e425-109">Advisor 在以下方面提出成本建议:</span><span class="sxs-lookup"><span data-stu-id="5e425-109">Advisor makes cost recommendations in the following areas:</span></span>

1. <span data-ttu-id="5e425-110">**通过消除未被取消的 Azure ExpressRoute 电路降低成本。**</span><span class="sxs-lookup"><span data-stu-id="5e425-110">**Reduce costs by eliminating unprovisioned Azure ExpressRoute circuits.**</span></span>
    <span data-ttu-id="5e425-111">这将识别已处于*未预配*的提供程序状态的 ExpressRoute 电路, 如果不打算使用连接提供程序设置电路, 则建议删除该电路。</span><span class="sxs-lookup"><span data-stu-id="5e425-111">This identifies ExpressRoute circuits that have been in the provider status of *Not Provisioned* for more than one month and recommends deleting the circuit if you aren't planning to provision the circuit with your connectivity provider.</span></span>

1. <span data-ttu-id="5e425-112">**购买保留实例以节省资金, 而不是随你那样付费。**</span><span class="sxs-lookup"><span data-stu-id="5e425-112">**Buy reserved instances to save money over pay-as-you-go.**</span></span>
    <span data-ttu-id="5e425-113">这将检查最近30天内的虚拟机使用情况, 并确定是否可以通过购买保留实例来节省资金。</span><span class="sxs-lookup"><span data-stu-id="5e425-113">This will review your virtual machine usage over the last 30 days and determine if you could save money in the future by purchasing reserved instances.</span></span> <span data-ttu-id="5e425-114">Advisor 将向您显示可能具有最大成本的区域和大小, 并将向您显示从购买保留实例中可能获得的估计节省量。</span><span class="sxs-lookup"><span data-stu-id="5e425-114">Advisor will show you the regions and sizes where you potentially have the most savings and will show you the estimated savings you might achieve from purchasing reserved instances.</span></span>

1. <span data-ttu-id="5e425-115">**大小不充分或已关闭的虚拟机的大小已用完。**</span><span class="sxs-lookup"><span data-stu-id="5e425-115">**Right-size or shutdown underutilized virtual machines.**</span></span>
    <span data-ttu-id="5e425-116">这将监视你的虚拟机使用率为14天, 然后识别未充分利用的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="5e425-116">This monitors your virtual machine usage for 14 days and then identifies underutilized virtual machines.</span></span> <span data-ttu-id="5e425-117">平均 CPU 利用率为 5% 或更低且网络使用率为 7 MB 或更少的虚拟机被视为未充分利用的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="5e425-117">Virtual machines whose average CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered underutilized virtual machines.</span></span> <span data-ttu-id="5e425-118">平均 CPU 使用率阈值可调节为 20%。</span><span class="sxs-lookup"><span data-stu-id="5e425-118">The average CPU utilization threshold is adjustable up to 20 percent.</span></span> <span data-ttu-id="5e425-119">通过确定这些虚拟机, 可以决定将其大小调整为较小的实例类型, 从而降低成本。</span><span class="sxs-lookup"><span data-stu-id="5e425-119">By identifying these virtual machines, you can decide to resize them to a smaller instance type, reducing your costs.</span></span>

[!include[](../../../includes/azure-free-trial-note.md)]

<span data-ttu-id="5e425-120">让我们看一看在门户中可以找到 Azure Advisor 的位置。</span><span class="sxs-lookup"><span data-stu-id="5e425-120">Let's take a look at where you can find Azure Advisor in the portal.</span></span> 

1. <span data-ttu-id="5e425-121">使用你的 Microsoft 帐户登录到[Azure 门户](https://portal.azure.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="5e425-121">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true) using your Microsoft account.</span></span> 

1. <span data-ttu-id="5e425-122">单击 "**所有服务**", 然后在 "**管理工具**" 类别中, 您将看到 " **Advisor**"。</span><span class="sxs-lookup"><span data-stu-id="5e425-122">Click on **All Services**, and in the **Management Tools** category, you will see **Advisor**.</span></span> <span data-ttu-id="5e425-123">您还可以在`Advisor` "筛选器" 框中键入以仅筛选该服务。</span><span class="sxs-lookup"><span data-stu-id="5e425-123">You can also type `Advisor` in the filter box to filter on just that service.</span></span>

1. <span data-ttu-id="5e425-124">单击 "advisor", 你将转到 advisor 建议仪表板, 你可以在其中查看你的订阅的所有建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-124">Click on Advisor, and you'll be taken to the Advisor recommendations dashboard where you can see all the recommendations for your subscription.</span></span> <span data-ttu-id="5e425-125">你将看到每个建议类别的一个框。</span><span class="sxs-lookup"><span data-stu-id="5e425-125">You'll see a box for each category of recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="5e425-126">您可能没有对 Advisor 中的成本的任何建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-126">You might not have any recommendations on cost in Advisor.</span></span> <span data-ttu-id="5e425-127">这可能是因为评估尚未完成, 或者是因为 Advisor 没有建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-127">This could be because assessments have not yet completed or simply because Advisor has no recommendations.</span></span>

![显示具有四个类别框的 advisor 刀片的 Azure 门户屏幕截图建议: 高可用性、安全性、性能和成本。](../media/3-advisor-recommendations.png)

<span data-ttu-id="5e425-129">单击 "**成本**" 框将转到详细建议, 您可以在其中查看 Advisor 的建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-129">Clicking on the **Cost** box will take you to detailed recommendations where you can see the recommendations that Advisor has.</span></span>

![显示 Advisor 边栏的成本建议部分的 Azure 门户屏幕截图。](../media/3-advisor-cost-recommendations.png)

<span data-ttu-id="5e425-131">单击 "任何建议" 将获取有关该特定建议的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5e425-131">Clicking on any recommendation will take you to the details for that specific recommendation.</span></span> <span data-ttu-id="5e425-132">然后, 你将能够执行特定操作, 例如调整虚拟机的大小以减少支出。</span><span class="sxs-lookup"><span data-stu-id="5e425-132">Then you'll be able to take a specific action, such as resizing virtual machines to reduce spending.</span></span>

![Azure 门户的屏幕截图, 显示有关关机或调整虚拟机建议的大小的建议详细信息。](../media/3-advisor-resize-vm.png)

<span data-ttu-id="5e425-134">这些建议是你可能会在不效率的情况下花费资金的所有地方。</span><span class="sxs-lookup"><span data-stu-id="5e425-134">These recommendations are all places where you might be inefficiently spending money.</span></span> <span data-ttu-id="5e425-135">在寻找可降低成本的位置时, 它们是一个很好的开始和继续重新访问的地方。</span><span class="sxs-lookup"><span data-stu-id="5e425-135">They're a great place to start and continue to revisit when looking for places to reduce costs.</span></span> <span data-ttu-id="5e425-136">在我们的示例中, 如果我们采用这些建议, 我们将有机会在每月大约 $700。</span><span class="sxs-lookup"><span data-stu-id="5e425-136">In our example, there's an opportunity for us to save around $700 per month if we take these recommendations.</span></span> <span data-ttu-id="5e425-137">这种节省增加了, 因此请务必定期查看所有四个领域的建议。</span><span class="sxs-lookup"><span data-stu-id="5e425-137">This savings adds up, so be sure to review this periodically for recommendations across all four areas.</span></span>

## <a name="azure-cost-management"></a><span data-ttu-id="5e425-138">Azure 成本管理</span><span class="sxs-lookup"><span data-stu-id="5e425-138">Azure Cost Management</span></span>

<span data-ttu-id="5e425-139">azure 成本管理是另一个免费的内置 Azure 工具, 可用于深入了解云货币的发展方向。</span><span class="sxs-lookup"><span data-stu-id="5e425-139">Azure Cost Management is another free, built-in Azure tool that can be used to gain greater insights into where your cloud money is going.</span></span> <span data-ttu-id="5e425-140">您可以查看您要为其支出的服务的历史细目, 以及它是如何根据已设置的预算进行跟踪的。</span><span class="sxs-lookup"><span data-stu-id="5e425-140">You can see historical breakdowns of what services you are spending your money on and how it is tracking against budgets that you have set.</span></span> <span data-ttu-id="5e425-141">您可以设置预算、安排报告和分析成本领域。</span><span class="sxs-lookup"><span data-stu-id="5e425-141">You can set budgets, schedule reports, and analyze your cost areas.</span></span>

![显示成本管理 + 帐单刀片的成本分析部分的 Azure 门户屏幕截图。](../media/3-cost-management.png)

## <a name="cloudyn"></a><span data-ttu-id="5e425-143">Cloudyn</span><span class="sxs-lookup"><span data-stu-id="5e425-143">Cloudyn</span></span>

<span data-ttu-id="5e425-144">Cloudyn 是 Microsoft 子公司, 允许您跟踪 Azure 资源和其他云提供商 (包括 Amazon Web 服务和 Google) 的云使用情况和支出。</span><span class="sxs-lookup"><span data-stu-id="5e425-144">Cloudyn, a Microsoft subsidiary, allows you to track cloud usage and expenditures for your Azure resources and other cloud providers including Amazon Web Services and Google.</span></span> <span data-ttu-id="5e425-145">易于理解的仪表板报表帮助提供成本分摊和退款。</span><span class="sxs-lookup"><span data-stu-id="5e425-145">Easy-to-understand dashboard reports help with cost allocation and chargebacks.</span></span> <span data-ttu-id="5e425-146">成本管理通过找出尚未充分利用的资源来帮助优化你的云支出, 以便您可以进行管理和调整。</span><span class="sxs-lookup"><span data-stu-id="5e425-146">Cost Management helps optimize your cloud spending by identifying underutilized resources that you can then manage and adjust.</span></span> <span data-ttu-id="5e425-147">Azure 的使用是免费的, 为高级支持和查看来自其他云的数据提供了付费选项。</span><span class="sxs-lookup"><span data-stu-id="5e425-147">Usage for Azure is free, and there are paid options for premium support and to view data from other clouds.</span></span>

![显示 Cloudyn 管理仪表板的 Azure 门户的屏幕截图。](../media/3-cloudyn-mgt-dash.png)

<span data-ttu-id="5e425-149">正如您所看到的, 有几个可用于在 Azure 上进行跟踪和预测的云花费和确定环境在成本方面可能效率低下的工具。</span><span class="sxs-lookup"><span data-stu-id="5e425-149">As you can see, there are several tools available for no cost on Azure that you can use to track and predict your cloud spend and identify where your environment may be inefficient from a cost perspective.</span></span> <span data-ttu-id="5e425-150">您需要确保将其作为查看这些工具所提供的报告和建议的常规实践, 这样您就可以在云空间占用的范围内解除对成本的节省。</span><span class="sxs-lookup"><span data-stu-id="5e425-150">You'll want to make sure you make it a regular practice to review the reports and recommendations that these tools make available, so you can unlock savings across your cloud footprint.</span></span>