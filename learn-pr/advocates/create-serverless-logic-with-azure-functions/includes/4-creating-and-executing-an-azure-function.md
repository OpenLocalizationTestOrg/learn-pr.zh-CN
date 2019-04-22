现在, 我们已创建了 function 应用程序, 我们来看看如何生成、配置和执行函数。

### <a name="triggers"></a>触发

函数是事件驱动的, 这意味着它们在响应事件时运行。

启动函数的事件的类型称为**触发器**。 必须使用恰好一个触发器配置函数。

Azure 支持以下服务的触发器。

| 服务                 | 触发器说明  |
|-------------------------|---------|
| Blob 存储            | 在检测到新的或更新的 blob 时启动函数。       |
| Cosmos DB               | 在检测到插入和更新时启动函数。      |
| 事件网格              | 从事件网格收到事件时启动函数。       |
| http.sys                    | 启动具有 HTTP 请求的函数。      |
| Microsoft Graph 事件  | 启动用于响应来自 Microsoft Graph 的传入 webhook 的函数。 此触发器的每个实例都可以对一种 Microsoft Graph 资源类型做出反应。       |
| 队列存储           | 当队列上收到新项目时, 启动一个函数。 队列消息作为函数的输入提供。      |
| 服务总线             | 启动用于响应来自服务总线队列的邮件的函数。       |
| 计时器                   | 按计划启动函数。       |

### <a name="bindings"></a>绑定

绑定是一种将数据和服务连接到您的函数的声明性方法。 绑定知道如何与不同的服务进行通信, 这意味着您无需在函数中编写代码即可连接到数据源和管理连接。 平台会将此复杂性作为绑定代码的一部分。 每个绑定都有一个方向代码从*输入*绑定中读取数据并将数据写入*输出*绑定。 每个函数都可以有零个或多个绑定, 以管理由函数处理的输入和输出数据。

触发器是一种特殊类型的输入绑定, 它具有启动执行的额外功能。

Azure 提供了[大量绑定](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings)以连接到不同的存储和邮件服务。

### <a name="a-sample-binding-definition"></a>示例绑定定义

我们来看一个使用输入绑定 (触发器) 和输出绑定配置函数的示例。 假设我们要从 Blob 存储中读取数据, 在我们的函数中进行处理, 然后向队列中写入一条消息。 您可以配置类型为*blob*的_输入绑定_和类型为*queue*的_输出绑定_。

可以在 Azure 门户中定义绑定, 并将其存储为 JSON 文件, 也可以直接编辑它们。 下面的 JSON 是函数的触发器和绑定的示例定义。

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

此示例显示了一个函数, 该函数由添加到名为**myqueue**的队列中的邮件触发。 然后, 它将函数的返回值发送到 Azure 表存储中的**outTable**表。 这是一个非常简单的示例, 我们可以将输出更改为使用 SendGrid 绑定的电子邮件, 或将事件放在服务总线上, 以在体系结构中通知某个其他组件, 甚至让多个输出绑定将数据推送到各种服务。

## <a name="creating-a-function-in-the-azure-portal"></a>在 Azure 门户中创建函数

Azure 为常见方案提供了几个预先准备的函数模板。

### <a name="quickstart-templates"></a>快速入门模板

添加您的第一个函数时, 将显示快速入门屏幕。 此屏幕允许您选择触发器类型 (HTTP、计时器或数据) 和编程语言 (c #、JavaScript、F # 或 Java)。 然后, 根据你的选择, Azure 将使用提供的一些示例代码为你生成函数代码和配置, 以显示日志中收到的输入数据。

### <a name="custom-function-templates"></a>自定义函数模板

通过选择快速入门模板, 可轻松访问最常见的方案。 但是, Azure 提供了30多个可供你使用的其他模板。 在创建后续函数或使用快速入门屏幕上的 "**自定义函数**" 选项进行选择时, 可以从 "模板列表" 屏幕中选择这些功能。

- HTTP 触发器 w/c #、F # 或 JavaScript
- 带有 c #、F # 或 JavaScript 的计时器触发器
- 带有 c #、F # 或 JavaScript 的队列触发器
- 服务总线队列触发器 w/c #、F # 或 JavaScript
- Cosmos DB 触发器 w/c # 或 JavaScript
- 带有 c #、F # 或 JavaScript 的 IoT 中心 (事件中心)
- ...以及更多

## <a name="navigating-to-your-function-and-files"></a>导航到您的函数和文件

从模板创建函数时, 将创建多个文件。 例如, 如果您选择使用 JavaScript + API 快速入门, 则生成的文件将是配置文件、**函数 json**和源代码文件 (即 **.js**)。 在函数应用门户中创建的函数将显示在 function 应用门户中的 "**函数**" 菜单项下。

当您在函数应用程序中选择函数时, 代码编辑器将打开并显示函数的代码, 如以下屏幕截图中所示。

![显示 "函数编辑器" 边栏的 Azure 门户屏幕截图, 其中包括展开的 "视图文件" 菜单, 在应用程序服务导航中选择 "HttpTriggerJS1" 功能, 并突出显示 "查看文件" 菜单。](../media/4-file-navigation.png)

如前面的屏幕截图中所示, 在右侧有一个弹出菜单, 其中包含用于**查看文件**的选项卡。 选择此选项卡将显示构成函数的文件结构。

## <a name="testing-your-azure-function"></a>测试 Azure 函数

创建函数后, 需要对其进行测试。 有几种方法: 从 Azure 门户本身内部手动执行和测试。

### <a name="manual-execution"></a>手动执行

您可以通过手动触发已配置的触发器来启动函数。 例如, 如果您使用的是 HTTP 触发器, 则可以使用 Postman 或卷曲的工具启动对函数终结点 URL 的 http 请求, 该 URL 可从 HTTP 触发器定义 (**Get function url**)。

### <a name="testing-in-the-azure-portal"></a>在 Azure 门户中进行测试

门户还提供了一种方便的方法来测试您的函数。 在代码窗口的右侧有一个弹出菜单选项卡式导航菜单。 此菜单包含一个**测试**项。 展开菜单并选择此选项卡将为您提供执行函数和查看结果的另一种方法。 当您在此测试窗口中单击 "**运行**" 时, 结果将显示在 "输出" 窗口中, 并显示一个状态代码。

## <a name="monitoring-dashboard"></a>监控仪表板

在开发和生产过程中, 监视函数的能力非常关键。 如果你启用 application Insights 集成, Azure 门户将提供一个可用的监控仪表板。 在函数应用程序导航菜单中, 展开函数节点后, 您将看到一个**监视器**菜单项。 此监视器仪表板提供了查看函数执行的历史记录的快速方法, 并显示了 Application Insights 填充的时间戳、结果代码、持续时间和操作 ID。

![显示 http 函数监视器刀片的 Azure 门户屏幕截图, 其中包含多个函数结果及其对应的 HTTP 状态代码, 并突出显示函数的模块菜单项。](../media/4-monitor-function.png)

## <a name="streaming-log-window"></a>流式处理日志窗口

您还可以将日志记录语句添加到您的函数以在 Azure 门户中进行调试。 向每种语言的被调用方法传递一个 "日志记录" 对象, 该对象可用于将信息记录到位于 "代码" 窗口底部的选项卡式弹出菜单中的 "日志" 窗口中。

以下 JavaScript 代码段显示了如何使用`context.log`方法记录消息 ( `context`对象传递给处理程序)。

```javascript
  context.log('Enter your logging statement here');
```

我们可以使用`log.Info`方法在 c # 中执行相同的操作。 在这种情况下`log` , 对象将传递给处理函数的 c # 方法。

```csharp
  log.Info("Enter your logging statement here");
```

### <a name="errors-and-warnings-window"></a>"错误和警告" 窗口

您可以在日志窗口所在的同一个弹出菜单中找到 "错误和警告" 窗口选项卡。 此窗口将显示代码中的编译错误和警告。
