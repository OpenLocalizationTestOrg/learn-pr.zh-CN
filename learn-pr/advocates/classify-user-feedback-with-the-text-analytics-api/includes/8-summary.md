Azure 认知服务是一套丰富的智能服务, 可用于丰富应用程序。 文本分析 API 有几项操作可将文本转换为有意义的见解。 我们使用服务发现来自客户的文本反馈中的看法。 我们创建了一个托管在 Azure 函数中的解决方案, 用于将这些短信分类到不同的存储桶或队列中, 以供进一步处理。

一旦您知道如何调用 REST API, 就可以轻松地将这些智能服务集成到您的解决方案中。 它们都遵循类似的模式:

- 注册访问密钥。
- 浏览 API 测试控制台。
- 使用访问键和正确的区域来表述请求。
- 从解决方案中发布请求, 并分析见解的响应。

我们将此智能添加到在 Azure 函数中创建的无服务器逻辑。 您可以从其他类型的应用程序轻松调用这些服务。 有许多客户端库、教程和快速入门可帮助你入门。

## <a name="suggestions-for-further-enhancement-of-our-solution"></a>对我们的解决方案进一步增强的建议

下面介绍了一些建议, 以供你考虑是否需要我们做进一步的操作。

- 使用更多的文本示例测试解决方案。 确定我们设置的阈值是否适用于将看法分数分类为正数、负数和中性。
- 考虑向函数应用程序中添加另一个从[!INCLUDE [negative-q](./q-name-negative.md)]队列读取邮件的函数, 并调用文本分析 API 以在文本中查找关键短语。
- 我们的输入队列包含原始文本反馈。 在现实世界中, 我们会将反馈与某种形式的用户 ID (例如电子邮件地址、帐号等) 相关联。 将输入队列项增强为包含 ID 字段和文本的 JSON 文档。 在处理短信时使用该 ID。
- 目前我们的解决方案是 "硬编码" 为英语。 考虑要实现的更改, 使其能够处理文本分析 API 支持的所有语言的文本。
- 如果您熟悉逻辑应用程序, 请访问指向 "进一步阅读" 一节中的 "文本分析" 内置连接器的链接。

现在, 您已经知道如何调用其中一个认知服务 api, 请浏览一些其他服务, 并考虑如何在解决方案中使用它们。

## <a name="further-reading"></a>进一步阅读

- [文本分析概述](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview)
- [文本分析演示](https://azure.microsoft.com/services/cognitive-services/text-analytics/)
- [如何在文本分析中检测看法](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis)
- [认知服务文档](https://docs.microsoft.com/azure/cognitive-services/)

- [文本分析逻辑应用连接器](https://docs.microsoft.com/connectors/cognitiveservicestextanalytics/)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
