<span data-ttu-id="47c74-101">在不同服务产品之间组合 sla 时, 结果 sla 称为 "*复合 sla*"。</span><span class="sxs-lookup"><span data-stu-id="47c74-101">When combining SLAs across different service offerings, the resultant SLA is a called a *Composite SLA*.</span></span> <span data-ttu-id="47c74-102">生成的复合 SLA 可提供更高或更低的正常运行时间值, 具体取决于应用程序的体系结构。</span><span class="sxs-lookup"><span data-stu-id="47c74-102">The resulting composite SLA can provide higher or lower uptime values, depending on your application architecture.</span></span>

## <a name="calculating-downtime"></a><span data-ttu-id="47c74-103">计算停机时间</span><span class="sxs-lookup"><span data-stu-id="47c74-103">Calculating downtime</span></span> 

<span data-ttu-id="47c74-104">考虑写入 Azure SQL 数据库的应用程序服务 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="47c74-104">Consider an App Service web app that writes to Azure SQL Database.</span></span> <span data-ttu-id="47c74-105">这些 Azure 服务目前具有以下 sla:</span><span class="sxs-lookup"><span data-stu-id="47c74-105">These Azure services currently have the following SLAs:</span></span>

![表示 Web 应用及其 sla 正常运行时间值为 99.95%、SQL 数据库及其 sla 值为 99.99% 的图像。](../media/7-sla-compositesla1.png)

<span data-ttu-id="47c74-107">在此示例中, 如果其中一个服务失败, 整个应用程序将失败。</span><span class="sxs-lookup"><span data-stu-id="47c74-107">In this example, if either service fails the whole application will fail.</span></span> <span data-ttu-id="47c74-108">通常, 每个服务的各个概率值都是独立的。</span><span class="sxs-lookup"><span data-stu-id="47c74-108">In general, the individual probability values for each service are independent.</span></span> <span data-ttu-id="47c74-109">但是, 此应用程序的复合 SLA 值为:</span><span class="sxs-lookup"><span data-stu-id="47c74-109">However, the composite SLA value for this application is:</span></span> 

`99.95 percent × 99.99 percent = 99.94 percent`

<span data-ttu-id="47c74-110">这意味着**故障的组合可能性**高于各个 SLA 值。</span><span class="sxs-lookup"><span data-stu-id="47c74-110">This means the **combined probability of failure** is higher than the individual SLA values.</span></span> <span data-ttu-id="47c74-111">这并不令人吃惊, 因为依赖于多个服务的应用程序可能会有更多的故障点。</span><span class="sxs-lookup"><span data-stu-id="47c74-111">This isn't surprising, because an application that relies on multiple services has more potential failure points.</span></span>

<span data-ttu-id="47c74-112">相反, 您可以通过创建独立的回退路径来改进复合 SLA。</span><span class="sxs-lookup"><span data-stu-id="47c74-112">Conversely, you can improve the composite SLA by creating independent fallback paths.</span></span> <span data-ttu-id="47c74-113">例如, 如果 SQL 数据库不可用, 则可以将事务放入队列中, 以便以后进行处理。</span><span class="sxs-lookup"><span data-stu-id="47c74-113">For example, if SQL Database is unavailable, you can put transactions into a queue for processing at a later time.</span></span>

![表示 Web 应用及其 sla 正常运行时间值为 99.95% 和 SQL database 的图像以及其 sla 值为 99.99%。](../media/7-sla-compositesla2.png)

<span data-ttu-id="47c74-115">在此设计中, 应用程序仍然可用, 即使它无法连接到数据库也是如此。</span><span class="sxs-lookup"><span data-stu-id="47c74-115">With this design, the application is still available even if it can't connect to the database.</span></span> <span data-ttu-id="47c74-116">但是, 如果数据库_和_队列同时发生故障, 则会失败。</span><span class="sxs-lookup"><span data-stu-id="47c74-116">However, it fails if both the database _and_ the queue fail simultaneously.</span></span> 

<span data-ttu-id="47c74-117">如果同时发生故障的预期时间百分比为**0.0001 × 0.001**, 则数据库_或_队列的此组合路径的复合 SLA 为:</span><span class="sxs-lookup"><span data-stu-id="47c74-117">If the expected percentage of time for a simultaneous failure is **0.0001 × 0.001**, the composite SLA for this combined path of a database _or_ queue would be:</span></span>

`1.0 − (0.0001 × 0.001) = 99.99999 percent`

<span data-ttu-id="47c74-118">因此, 如果我们将队列添加到 web 应用中, 总的复合 SLA 为:</span><span class="sxs-lookup"><span data-stu-id="47c74-118">Therefore, if we add the queue to our web app, the total composite SLA is:</span></span>

`99.95 percent × 99.99999 percent = ~99.95 percent`

<span data-ttu-id="47c74-119">请注意, 我们已改进了 SLA 行为。</span><span class="sxs-lookup"><span data-stu-id="47c74-119">Notice we've improved our SLA behavior.</span></span> <span data-ttu-id="47c74-120">但是, 使用此方法时, 需要进行权衡: 应用程序逻辑更复杂, 需要支付更多的队列支持, 并且可能因重试行为而必须处理的数据一致性问题。</span><span class="sxs-lookup"><span data-stu-id="47c74-120">However, there are trade-offs to using this approach: the application logic is more complicated, you are paying more to add the queue support, and there may be data-consistency issues you'll have to deal with due to retry behavior.</span></span>
