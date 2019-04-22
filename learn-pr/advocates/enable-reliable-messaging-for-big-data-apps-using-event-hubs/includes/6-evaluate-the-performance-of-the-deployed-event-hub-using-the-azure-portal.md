<span data-ttu-id="7c014-101">在使用事件中心时, 监视中心以确保其正常运行并按预期执行, 这一点非常关键。</span><span class="sxs-lookup"><span data-stu-id="7c014-101">When using Event Hubs, it's crucial for you to monitor your hub to ensure that it's working and performing as expected.</span></span>

<span data-ttu-id="7c014-102">继续使用银行示例, 假定您已部署 Azure 事件中心和配置的发件人和收件人应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c014-102">Continuing with the banking example, suppose that you've deployed Azure Event Hubs and configured sender and receiver applications.</span></span> <span data-ttu-id="7c014-103">您的应用程序已准备好测试付款处理解决方案。</span><span class="sxs-lookup"><span data-stu-id="7c014-103">Your applications are ready for testing the payment processing solution.</span></span> <span data-ttu-id="7c014-104">发件人应用程序收集客户的信用卡数据, 收件人应用程序验证信用卡是否有效。</span><span class="sxs-lookup"><span data-stu-id="7c014-104">The sender application collects customer's credit card data and the receiver application verifies that the credit card is valid.</span></span> <span data-ttu-id="7c014-105">由于你的员工的敏感性质, 你的支付过程非常重要, 即使它暂时不可用也是可靠的。</span><span class="sxs-lookup"><span data-stu-id="7c014-105">Due to the sensitive nature of your employer's business, it's essential that your payment processing is robust and reliable, even when it's temporarily unavailable.</span></span>

<span data-ttu-id="7c014-106">您必须通过测试事件中心是否按预期处理数据来评估事件中心。</span><span class="sxs-lookup"><span data-stu-id="7c014-106">You must evaluate your Event Hub by testing that your Event Hub is processing data as expected.</span></span> <span data-ttu-id="7c014-107">事件中心中的可用指标可确保其正常工作。</span><span class="sxs-lookup"><span data-stu-id="7c014-107">The metrics available in the Event Hubs allow you to ensure that it's working fine.</span></span>

## <a name="how-do-you-use-the-azure-portal-to-view-your-event-hub-activity"></a><span data-ttu-id="7c014-108">如何使用 Azure 门户查看事件中心活动？</span><span class="sxs-lookup"><span data-stu-id="7c014-108">How do you use the Azure portal to view your Event Hub activity?</span></span>

<span data-ttu-id="7c014-109">事件中心的 "Azure 门户 > 概述" 页显示邮件数。</span><span class="sxs-lookup"><span data-stu-id="7c014-109">The Azure portal > Overview page for your Event Hub shows message counts.</span></span> <span data-ttu-id="7c014-110">这些邮件计数代表事件中心接收和发送的数据 (事件)。</span><span class="sxs-lookup"><span data-stu-id="7c014-110">These message counts represent the data (events) received and sent by the Event Hub.</span></span> <span data-ttu-id="7c014-111">您可以选择查看这些事件的时间刻度。</span><span class="sxs-lookup"><span data-stu-id="7c014-111">You can choose the timescale for viewing these events.</span></span>

![显示具有邮件计数的事件中心命名空间的 Azure 门户屏幕截图。](../media/6-view-messages.png)

## <a name="how-can-you-test-event-hub-resilience"></a><span data-ttu-id="7c014-113">如何测试事件中心恢复能力？</span><span class="sxs-lookup"><span data-stu-id="7c014-113">How can you test Event Hub resilience?</span></span>

<span data-ttu-id="7c014-114">Azure 事件中心始终接收来自发件人应用程序的邮件, 即使它不可用。</span><span class="sxs-lookup"><span data-stu-id="7c014-114">Azure Event Hubs keeps receiving messages from the sender application even when it's unavailable.</span></span> <span data-ttu-id="7c014-115">一旦中心可用, 在此期间收到的邮件就会成功传输。</span><span class="sxs-lookup"><span data-stu-id="7c014-115">The messages received during this period are transmitted successfully as soon as the hub becomes available.</span></span>

<span data-ttu-id="7c014-116">若要测试此功能, 您可以使用 Azure 门户禁用事件中心。</span><span class="sxs-lookup"><span data-stu-id="7c014-116">To test this functionality, you can use the Azure portal to disable your Event Hub.</span></span>

<span data-ttu-id="7c014-117">重新启用事件中心时, 可以重新运行接收器应用程序, 并使用事件中心指标检查命名空间, 以检查是否已成功传输和接收所有发件人邮件。</span><span class="sxs-lookup"><span data-stu-id="7c014-117">When you re-enable your Event Hub, you can rerun your receiver application and use Event Hubs metrics for your namespace to check whether all sender messages have been successfully transmitted and received.</span></span>

<span data-ttu-id="7c014-118">事件中心中提供的其他有用指标包括:</span><span class="sxs-lookup"><span data-stu-id="7c014-118">Other useful metrics available in the Event Hubs include:</span></span>

- <span data-ttu-id="7c014-119">限制的请求: 由于超过了吞吐量单位使用率而受到限制的请求数。</span><span class="sxs-lookup"><span data-stu-id="7c014-119">Throttled Requests: The number of requests that were throttled because the throughput unit usage was exceeded.</span></span>
- <span data-ttu-id="7c014-120">ActiveConnections: 命名空间或事件中心上的活动连接数。</span><span class="sxs-lookup"><span data-stu-id="7c014-120">ActiveConnections: The number of active connections on a namespace or Event Hub.</span></span>
- <span data-ttu-id="7c014-121">传入/传出字节: 在指定时间段内从事件中心服务发送到/接收的字节数。</span><span class="sxs-lookup"><span data-stu-id="7c014-121">Incoming/Outgoing Bytes: The number of bytes sent to/received from the Event Hubs service over a specified period.</span></span>

## <a name="summary"></a><span data-ttu-id="7c014-122">摘要</span><span class="sxs-lookup"><span data-stu-id="7c014-122">Summary</span></span>

<span data-ttu-id="7c014-123">Azure 门户提供了邮件计数和其他指标, 您可以将这些指标用作事件中心的运行状况检查。</span><span class="sxs-lookup"><span data-stu-id="7c014-123">The Azure portal provides message counts and other metrics that you can use as a health check for your Event Hubs.</span></span>
