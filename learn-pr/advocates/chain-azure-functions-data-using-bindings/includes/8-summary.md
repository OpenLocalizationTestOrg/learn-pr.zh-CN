本模块全部介绍了如何将数据和服务集成到您的功能中。 启动时, 我们将快速浏览在将其添加到函数时显示的绑定类型。 然后, 我们查看使用输入绑定从 Azure Cosmos DB 读取数据。 该平台负责管理连接字符串, 我们看到了使用绑定在代码中读取数据的难易程度。 最后, 我们重点关注的是使用输出绑定的帮助将数据写入不同的源。 下表汇总了这一旅程:

[!INCLUDE [summary table](./summary-table.md)]

您可以在此处应用您学习的方法, 以在函数中添加和测试绑定。 下面是几个有趣的想法, 可以通过绑定获取更多实践, 并根据这里了解到的内容进行构建。

* 创建另一个函数以读取从 Blob 存储和我们未在此模块中使用的其他输入绑定。

* 使用其他受支持的输出绑定类型创建另一个函数以写入更多的目标。

* 在上面的单元中, 我们引入了一个队列, 并使用输出绑定将邮件发送给它。 作为下一步, 请考虑添加另一个可读取队列中的邮件的函数, 并将**邮件文本**输出到的`console.log()`控制台。

正如我们在本模块中看到的那样, Azure 门户提供了易于使用的功能, 可开始构建功能并将它们连接到数据和其他服务。

如果你有兴趣使用直观工作流和少量或无自定义代码来执行无服务器集成 (如这些集成), 请查看 Azure 逻辑应用。

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>其他资源

虽然这并不是一个详尽的列表, 但下面是一些与此模块中所述主题相关的资源, 您可能会感兴趣:

* [Azure 函数文档](https://docs.microsoft.com/azure/azure-functions/)
* [Azure 函数质询](https://aka.ms/afc)
* [Azure 无服务器计算手册](https://azure.microsoft.com/resources/azure-serverless-computing-cookbook/)
* [如何: 从 node.js 使用队列存储](https://docs.microsoft.com/azure/storage/queues/storage-nodejs-how-to-use-queues)
* [Azure Cosmos DB 简介: SQL API](https://docs.microsoft.com/azure/cosmos-db/sql-api-introduction)
* [Azure Cosmos DB 的技术概述](https://azure.microsoft.com/blog/a-technical-overview-of-azure-cosmos-db/)
* [Azure Cosmos DB 文档](https://docs.microsoft.com/azure/cosmos-db/)
