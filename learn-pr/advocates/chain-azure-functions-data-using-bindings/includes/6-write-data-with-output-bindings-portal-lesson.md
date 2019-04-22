<span data-ttu-id="41de0-101">与输入绑定一样, 存在多种类型的输出绑定。</span><span class="sxs-lookup"><span data-stu-id="41de0-101">As with input bindings, there are multiple types of output bindings.</span></span> <span data-ttu-id="41de0-102">但并非所有类型都支持输入和输出。</span><span class="sxs-lookup"><span data-stu-id="41de0-102">However not all types support both input and output.</span></span> <span data-ttu-id="41de0-103">只要您想要发送或存储数据, 您都可以使用它们。</span><span class="sxs-lookup"><span data-stu-id="41de0-103">You'll use them anytime you want to send or store data.</span></span> <span data-ttu-id="41de0-104">在这里, 我们将介绍支持输出绑定的类型以及何时使用它们。</span><span class="sxs-lookup"><span data-stu-id="41de0-104">Here, we'll look at the types that support output bindings and when to use them.</span></span>

## <a name="output-binding-types"></a><span data-ttu-id="41de0-105">输出绑定类型</span><span class="sxs-lookup"><span data-stu-id="41de0-105">Output binding types</span></span>

- <span data-ttu-id="41de0-106">**blob 存储**-您可以使用 blob 输出绑定来编写 blob。</span><span class="sxs-lookup"><span data-stu-id="41de0-106">**Blob Storage** - You can use the blob output binding to write blobs.</span></span>

- <span data-ttu-id="41de0-107">**Cosmos db** -Azure Cosmos DB 输出绑定允许您使用 SQL API 将新文档写入 Azure Cosmos DB 数据库。</span><span class="sxs-lookup"><span data-stu-id="41de0-107">**Cosmos DB** - The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.</span></span>

- <span data-ttu-id="41de0-108">**事件中心**-使用事件中心输出绑定将事件写入事件流。</span><span class="sxs-lookup"><span data-stu-id="41de0-108">**Event Hubs** - Use the Event Hubs output binding to write events to an event stream.</span></span> <span data-ttu-id="41de0-109">您必须具有对事件中心的 "发送" 权限才能向其写入事件。</span><span class="sxs-lookup"><span data-stu-id="41de0-109">You must have send permission to an event hub to write events to it.</span></span>

- <span data-ttu-id="41de0-110">**http** -使用 http 输出绑定来响应 http 请求发件人。</span><span class="sxs-lookup"><span data-stu-id="41de0-110">**HTTP** - Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="41de0-111">此绑定需要一个 HTTP 触发器, 并允许您自定义与该触发器的请求关联的响应。</span><span class="sxs-lookup"><span data-stu-id="41de0-111">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="41de0-112">这也可用于连接到 web 挂钩。</span><span class="sxs-lookup"><span data-stu-id="41de0-112">This can also be used to connect to web hooks.</span></span>

- <span data-ttu-id="41de0-113">**microsoft** graph-microsoft graph 输出绑定允许您写入 OneDrive 中的文件、修改 Excel 数据以及通过 Outlook 发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="41de0-113">**Microsoft Graph** - Microsoft Graph output bindings allow you to write to files in OneDrive, modify Excel data, and send email through Outlook.</span></span>

- <span data-ttu-id="41de0-114">**移动应用**程序-移动应用程序输出绑定将新记录写入移动应用程序表。</span><span class="sxs-lookup"><span data-stu-id="41de0-114">**Mobile Apps** - The Mobile Apps output binding writes a new record to a Mobile Apps table.</span></span>

- <span data-ttu-id="41de0-115">**通知中心**-你可以发送带通知中心输出绑定的推送通知。</span><span class="sxs-lookup"><span data-stu-id="41de0-115">**Notification Hubs** - You can send push notifications with Notification Hubs output bindings.</span></span>

- <span data-ttu-id="41de0-116">**队列存储**-使用 Azure 队列存储输出绑定将消息写入队列。</span><span class="sxs-lookup"><span data-stu-id="41de0-116">**Queue Storage** - Use the Azure Queue storage output binding to write messages to a queue.</span></span>

- <span data-ttu-id="41de0-117">**发送网格**-使用 SendGrid 绑定发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="41de0-117">**Send Grid** - Send emails using SendGrid bindings.</span></span>

- <span data-ttu-id="41de0-118">**服务总线**-使用 Azure 服务总线输出绑定来发送队列或主题消息。</span><span class="sxs-lookup"><span data-stu-id="41de0-118">**Service Bus** - Use Azure Service Bus output binding to send queue or topic messages.</span></span>

- <span data-ttu-id="41de0-119">**表存储**-使用 azure 表存储输出绑定对 azure 存储帐户中的表进行写入。</span><span class="sxs-lookup"><span data-stu-id="41de0-119">**Table storage** - Use an Azure Table storage output binding to write to a table in an Azure Storage account.</span></span>

- <span data-ttu-id="41de0-120">**Twilio** -使用 Twilio 发送短信。</span><span class="sxs-lookup"><span data-stu-id="41de0-120">**Twilio** - Send text messages with Twilio.</span></span>

<span data-ttu-id="41de0-121">若要创建作为输出的绑定, 必须将定义定义`direction`为`out`。</span><span class="sxs-lookup"><span data-stu-id="41de0-121">To create a binding as an output, you must define the `direction` as `out`.</span></span> <span data-ttu-id="41de0-122">每种绑定类型的参数可能各不相同。</span><span class="sxs-lookup"><span data-stu-id="41de0-122">The parameters for each type of binding may vary.</span></span>

## <a name="combining-input-and-output-bindings"></a><span data-ttu-id="41de0-123">组合输入和输出绑定</span><span class="sxs-lookup"><span data-stu-id="41de0-123">Combining input and output bindings</span></span> 

<span data-ttu-id="41de0-124">可以向单个函数应用多个绑定。</span><span class="sxs-lookup"><span data-stu-id="41de0-124">It's possible to apply multiple bindings to a single function.</span></span> <span data-ttu-id="41de0-125">这使您可以同时定义输入绑定和输出绑定, 并且输入和输出甚至可以是相同的绑定类型。</span><span class="sxs-lookup"><span data-stu-id="41de0-125">This allows you to define both input and output bindings, and the input and output can even be the same binding type.</span></span>