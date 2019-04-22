<span data-ttu-id="0adf2-101">本模块全部介绍了如何将数据和服务集成到您的功能中。</span><span class="sxs-lookup"><span data-stu-id="0adf2-101">This module was all about integrating data and services into your functions.</span></span> <span data-ttu-id="0adf2-102">启动时, 我们将快速浏览在将其添加到函数时显示的绑定类型。</span><span class="sxs-lookup"><span data-stu-id="0adf2-102">We started off with a quick tour of the binding types that show up when you add them to a function.</span></span> <span data-ttu-id="0adf2-103">然后, 我们查看使用输入绑定从 Azure Cosmos DB 读取数据。</span><span class="sxs-lookup"><span data-stu-id="0adf2-103">We then looked at reading data from an Azure Cosmos DB by using an input binding.</span></span> <span data-ttu-id="0adf2-104">该平台负责管理连接字符串, 我们看到了使用绑定在代码中读取数据的难易程度。</span><span class="sxs-lookup"><span data-stu-id="0adf2-104">The platform takes care of managing connection strings, and we saw how easy it is to read data in our code by using the binding.</span></span> <span data-ttu-id="0adf2-105">最后, 我们重点关注的是使用输出绑定的帮助将数据写入不同的源。</span><span class="sxs-lookup"><span data-stu-id="0adf2-105">Finally, we focused our attention on writing data to different sources with the help of output bindings.</span></span> <span data-ttu-id="0adf2-106">下表汇总了这一旅程:</span><span class="sxs-lookup"><span data-stu-id="0adf2-106">This journey is summarized in the following table:</span></span>

[!INCLUDE [summary table](./summary-table.md)]

<span data-ttu-id="0adf2-107">您可以在此处应用您学习的方法, 以在函数中添加和测试绑定。</span><span class="sxs-lookup"><span data-stu-id="0adf2-107">You can apply the approaches you have learned here to add and test bindings in your functions.</span></span> <span data-ttu-id="0adf2-108">下面是几个有趣的想法, 可以通过绑定获取更多实践, 并根据这里了解到的内容进行构建。</span><span class="sxs-lookup"><span data-stu-id="0adf2-108">Here are a few interesting ideas to get more practice with bindings and to build on what you have learned here.</span></span>

* <span data-ttu-id="0adf2-109">创建另一个函数以读取从 Blob 存储和我们未在此模块中使用的其他输入绑定。</span><span class="sxs-lookup"><span data-stu-id="0adf2-109">Create another function to read from Blob storage and other input bindings that we haven't used in this module.</span></span>

* <span data-ttu-id="0adf2-110">使用其他受支持的输出绑定类型创建另一个函数以写入更多的目标。</span><span class="sxs-lookup"><span data-stu-id="0adf2-110">Create another function to write to more destinations by using other supported output binding types.</span></span>

* <span data-ttu-id="0adf2-111">在上面的单元中, 我们引入了一个队列, 并使用输出绑定将邮件发送给它。</span><span class="sxs-lookup"><span data-stu-id="0adf2-111">In the preceding unit, we introduced a queue and posted messages to it with an output binding.</span></span> <span data-ttu-id="0adf2-112">作为下一步, 请考虑添加另一个可读取队列中的邮件的函数, 并将**邮件文本**输出到的`console.log()`控制台。</span><span class="sxs-lookup"><span data-stu-id="0adf2-112">As a next step, consider adding another function that reads the messages in the queue and prints out the **MESSAGE TEXT** to the console with `console.log()`.</span></span>

<span data-ttu-id="0adf2-113">正如我们在本模块中看到的那样, Azure 门户提供了易于使用的功能, 可开始构建功能并将它们连接到数据和其他服务。</span><span class="sxs-lookup"><span data-stu-id="0adf2-113">As we saw in this module, the Azure portal offers easy-to-use features to start building functions and connecting them to data and other services.</span></span>

<span data-ttu-id="0adf2-114">如果你有兴趣使用直观工作流和少量或无自定义代码来执行无服务器集成 (如这些集成), 请查看 Azure 逻辑应用。</span><span class="sxs-lookup"><span data-stu-id="0adf2-114">If you're interested in doing serverless integrations like these with visual workflows and little or no custom code, check out Azure Logic Apps as well.</span></span>

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a><span data-ttu-id="0adf2-115">其他资源</span><span class="sxs-lookup"><span data-stu-id="0adf2-115">Additional Resources</span></span>

<span data-ttu-id="0adf2-116">虽然这并不是一个详尽的列表, 但下面是一些与此模块中所述主题相关的资源, 您可能会感兴趣:</span><span class="sxs-lookup"><span data-stu-id="0adf2-116">Although this is not intended to be an exhaustive list, the following are some resources related to the topics covered in this module that you might find interesting:</span></span>

* [<span data-ttu-id="0adf2-117">Azure 函数文档</span><span class="sxs-lookup"><span data-stu-id="0adf2-117">Azure Functions documentation</span></span>](https://docs.microsoft.com/azure/azure-functions/)
* [<span data-ttu-id="0adf2-118">Azure 函数质询</span><span class="sxs-lookup"><span data-stu-id="0adf2-118">The Azure Functions Challenge</span></span>](https://aka.ms/afc)
* [<span data-ttu-id="0adf2-119">Azure 无服务器计算手册</span><span class="sxs-lookup"><span data-stu-id="0adf2-119">Azure Serverless Computing Cookbook</span></span>](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)
* [<span data-ttu-id="0adf2-120">如何: 从 node.js 使用队列存储</span><span class="sxs-lookup"><span data-stu-id="0adf2-120">How to use Queue storage from Node.js</span></span>](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)
* [<span data-ttu-id="0adf2-121">Azure Cosmos DB 简介: SQL API</span><span class="sxs-lookup"><span data-stu-id="0adf2-121">Introduction to Azure Cosmos DB: SQL API</span></span>](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)
* [<span data-ttu-id="0adf2-122">Azure Cosmos DB 的技术概述</span><span class="sxs-lookup"><span data-stu-id="0adf2-122">A technical overview of Azure Cosmos DB</span></span>](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)
* [<span data-ttu-id="0adf2-123">Azure Cosmos DB 文档</span><span class="sxs-lookup"><span data-stu-id="0adf2-123">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/azure/cosmos-db/)
