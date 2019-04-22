让我们再次看一下我们的解决方案体系结构。

![反馈排序体系结构的概念图。](../media/proposed-solution.PNG)

正如您可以在此图的右侧看到的那样, 我们想要将邮件发送到三个队列。 因此, 我们会将这些连接定义为函数中的输出绑定。 我们可以通过**输出绑定**UI 创建这些绑定。 但是, 为了节省时间, 我们将直接编辑配置文件。

## <a name="add-output-bindings-to-functionjson"></a>将输出绑定添加到函数 json

1. 在 "函数应用[!INCLUDE [func-name-discover](./func-name-discover.md)]门户" 中选择我们的函数。

1. 展开屏幕右侧的 "**查看文件**" 菜单。

1. 在 "**查看文件**" 选项卡下, 选择**函数. json**以在编辑器中打开配置文件。

1. 将**函数 json**的全部内容替换为以下 json 并选择 "**保存**"。

[!code-json[](../code/function.json)]

我们已向 config 添加了三个新绑定。

- 每个新绑定的类型`queue`为。 这些绑定适用于三个队列, 我们会在你知道反馈的看法后向我们填充反馈邮件。
- 每个绑定的方向定义为`out`, 因为我们会将邮件发布到这些队列。
- 每个绑定对存储帐户使用相同的连接。
- 每个绑定都有`queueName`唯一`name`的和。

将邮件发布到队列就像说一样简单, 例如`context.bindings.negativeFeedbackQueueItem = "<message>"`。

## <a name="update-the-function-implementation-to-sort-feedback-into-queues-based-on-sentiment-score"></a>更新函数实现以根据看法分数将反馈排序到队列中

我们的反馈分类器的目标是将反馈分类为三个存储桶: 正数、中性和负数。 到目前为止, 我们已提供了输入队列, 我们的代码可以调用文本分析 API, 并已定义了输出队列。 在本节中, 我们将添加逻辑, 以根据看法将邮件移动到这些队列中。

1. 导航到我们的函数[!INCLUDE [func-name-discover](./func-name-discover.md)], 并再次`index.js`在代码编辑器中打开。

1. 将实现替换为以下代码。

[!code-javascript[](../code/discover-sentiment+sort.js?highlight=26-48)]

我们已将突出显示的代码添加到实现中。 该代码分析来自文本分析 API 认知服务的响应。 根据看法分数, 邮件将被转发到我们的三个输出队列中的一个。 发布邮件的代码只是设置正确的绑定参数。

## <a name="try-it-out"></a>试用

若要测试更新后的实现, 我们将转到存储资源管理器。

1. 导航到门户的 "**资源组**" 部分中的资源组。

1. 选择<rgn>[沙盒资源组名称]</rgn>, 在本课中使用的资源组。

1. 在打开的 "**资源组**" 面板中, 找到存储帐户条目并选择它。
    ![在 "资源组" 窗口中选择的存储帐户的屏幕截图。](../media/select-storage-account.png)

1. 从 "存储帐户" 主窗口的左侧菜单中选择 "**存储资源管理器 (预览)** "。 此操作将在门户中打开 Azure 存储资源管理器。

    ![显示存储资源管理器的屏幕截图, 其中当前有一个队列。](../media/storage-explorer-menu-inputq.png)

    我们有一个队列列在 "**队列**" 集合下。 此队列是[!INCLUDE [input-q](./q-name-input.md)]在模块的前面的 "测试" 部分中定义的输入队列。        

1. 在[!INCLUDE [input-q](./q-name-input.md)]左侧菜单中选择, 以查看此队列的数据资源管理器。 正如预期的那样, 队列没有数据。 让我们使用窗口顶部的 "**添加消息**" 命令向队列中添加一条消息。

1. 在 "**添加消息**" 对话框中, 输入 "我在此练习中遇到了乐趣!" 放在 "**消息" 文本**字段中, 然后单击对话框底部的 **"确定"** 。

1. 将在的数据窗口中显示该消息[!INCLUDE [input-q](./q-name-input.md)]。 几秒钟后, 单击数据视图顶部的 "**刷新**" 以刷新队列视图。 观察邮件在一段时间后消失。 那么, 它会在什么位置？

1. 右键单击左侧菜单中的 "**队列**" 集合。 观察*新*队列是否已出现。
    ![存储资源管理器的屏幕截图, 显示已在集合中创建新的队列。 队列包含一封邮件。](../media/sa-new-output-q.png)

    队列[!INCLUDE [positive-q](./q-name-positive.md)]是在首次发布邮件时自动创建的。 使用 Azure 函数队列输出绑定, 无需在发布之前手动创建输出队列! 现在[!INCLUDE [positive-q](./q-name-positive.md)], 我们看到传入的邮件已被我们的函数分类, 我们来看看以下邮件位于何处。    

1. 使用上述相同步骤, 将以下消息添加到[!INCLUDE [input-q](./q-name-input.md)]。

    - "我不讨厌 broccoli!"
    - "Microsoft 是公司"

1. 再次**** 单击 " [!INCLUDE [input-q](./q-name-input.md)]刷新", 直到再次清空。 此过程可能需要几分钟时间, 并且需要进行多次刷新。

1. 右键单击 "**队列**" 集合并观察出现的两个队列。 队列名为[!INCLUDE [neutral-q](./q-name-neutral.md)]和[!INCLUDE [negative-q](./q-name-negative.md)]。 这可能需要几秒钟时间, 因此继续刷新**队列**集合, 直到出现新的队列。 完成后, 您的队列列表应如下所示。

    ![显示队列集合中的四个队列的存储资源管理器菜单的屏幕截图。](../media/sa-final-q-list.png)

1. 单击列表中的每个队列以查看是否有邮件。 如果添加了建议的邮件, 您应该会在[!INCLUDE [positive-q](./q-name-positive.md)]、 [!INCLUDE [neutral-q](./q-name-neutral.md)]和[!INCLUDE [negative-q](./q-name-negative.md)]中看到一个。

!! 现在, 我们有一个工作反馈分类器! 当邮件到达输入队列时, 我们的函数使用文本分析 API 服务来获取看法分数。 根据该分数, 该函数将邮件转发到相应的队列。 尽管函数似乎一次只处理一个队列项, Azure 函数运行时实际上会读取队列项的批处理, 并加速函数的其他实例以并行方式进行处理。