在此单元中, 你将使用 Azure 门户验证你的事件中心是否正在工作并根据所需的预期执行。 您还将测试事件中心邮件在暂时不可用时的工作方式, 并使用事件中心指标检查事件中心的性能。

## <a name="view-event-hub-activity"></a>查看事件中心活动

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 使用搜索栏查找事件中心并将其打开。

1. 在 "概述" 页上, 查看邮件数。

    ![显示具有邮件计数的事件中心命名空间的 Azure 门户屏幕截图](../media/6-view-messages.png)

1. SimpleSend 和 EventProcessorSample 应用程序配置为发送/接收100消息。 您将看到事件中心已处理 SimpleSend 应用程序中的100邮件, 并已将100邮件传输到 EventProcessorSample 应用程序。

## <a name="test-event-hub-resilience"></a>测试事件中心恢复能力

使用以下步骤可查看当应用程序在事件中心暂时不可用时向其发送邮件时, 会发生什么情况。

1. 使用 SimpleSend 应用程序将邮件重新发送到事件中心。 使用以下命令:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. 如果看到 "**发送完成 ...**", 请按<kbd>enter</kbd>。

1. 在**概述**屏幕中选择事件中心-这将显示特定于事件中心的详细信息。 您还可以通过命名空间页面中的**事件中心**条目访问此屏幕。

1. 选择 "**设置** > **属性**"。

1. 在事件中心状态下, 单击 "**禁用**"。 保存所做的更改。

    ![禁用事件中心](../media/7-disable-event-hub.png)

    **等待至少5分钟。**

1. 单击 "事件中心状态" 下的 "**活动**" 以重新启用事件中心并保存所做的更改。

1. 重新运行 EventProcessorSample 应用程序以接收邮件。 使用以下命令。

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. 当邮件停止显示到控制台时, 请按<kbd>enter</kbd>。

1. 返回到 "Azure 门户", 返回到事件中心命名空间。 如果仍在 "事件中心" 页上, 则可以使用屏幕顶部的痕迹导航向后。 或者, 您可以搜索命名空间并选择它。

1. 单击 "**监视** > **指标 (预览)**"。

    ![显示事件中心指标以及显示的传入和传出邮件数量的屏幕截图。](../media/7-event-hub-metrics.png)

1. 从 "**指标**" 列表中, 选择 "**传入邮件**", 然后单击 "**添加指标**"。

1. 从 "**指标**" 列表中, 选择 "**传出邮件**", 然后单击 "**添加指标**"。

1. 在图表顶部, 单击 "**最近24小时 (自动)** ", 将时间段更改为**最近30分钟**以展开数据图形。

您会发现, 虽然在事件中心在一段时间内脱机之前已发送邮件, 但所有100邮件都已成功传输。

## <a name="summary"></a>摘要

在此单元中, 您使用事件中心指标测试事件中心是否成功处理发送和接收邮件。
