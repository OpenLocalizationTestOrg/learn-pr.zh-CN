向您的客户提供对在线衣物网站上产品的最快访问权限对您的客户和您的企业成功至关重要。 通过减少数据与用户之间的距离, 可以更快地传递更多的内容。 如果数据存储在 Azure Cosmos DB 中, 则将网站的数据复制到世界各地的多个区域是一个点, 然后单击 "操作"。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

在此单元中, 你将了解全局分发和本机多核数据库服务的优势, 然后将你的帐户复制到三个其他区域。

## <a name="global-distribution-basics"></a>全球分布基础知识

通过全局分发, 可以将数据从一个区域复制到多个 Azure 区域。 您可以在任何时候添加或删除数据库复制到的区域, Azure Cosmos DB 可确保在您添加其他区域时, 数据在30分钟内可用于操作, 假定您的数据为 100 tb 或更低。

在两个或更多区域中复制数据的常见方案有两个:

1. 将低延迟数据访问传递给最终用户, 无论它们位于全球的何处
2. 为业务连续性和灾难恢复添加区域弹性 (BCDR)

若要向客户提供低延迟访问, 建议您将数据复制到离用户最接近的地区。 对于您的在线服装公司, 您的洛杉矶、纽约和东京的客户。 查看 " [Azure 区域](https://azure.microsoft.com/global-infrastructure/regions/)" 页面, 并确定与这些客户组最接近的地区, 因为这些是您将向其复制用户的位置。

若要提供 BCDR 解决方案, 建议根据[业务连续性和灾难恢复 (BCDR)](https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/)中描述的区域对添加区域: Azure 配对区域文章。

当复制数据库时, 吞吐量和存储也同样进行复制。 因此, 如果您的原始数据库的存储空间为 10gb, 并且吞吐量为 1000 RU/秒, 并且如果您将其复制到三个其他区域, 则每个区域的吞吐量都是 10gb, 1000 RU/秒。 由于存储和吞吐量是在每个区域中复制的, 因此复制到区域的成本与原始区域相同, 因此复制到3个其他区域的成本大约是原始非复制数据库的四倍。

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>在门户中创建 Azure Cosmos DB 帐户

1. 使用用于激活沙盒的相同帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

    > [!IMPORTANT]
    > 使用相同的帐户登录到 Azure 门户和沙盒。
    >
    > 使用上面的链接登录到 Azure 门户, 以确保您已连接到沙盒, 该沙箱提供对 Concierge 订阅的访问权限。

1. 单击 "**创建资源** > **数据库** > " "**Azure Cosmos DB**"。

   ![Azure portal 数据库窗格](../media/2-global-distribution/2-create-nosql-db-databases-json-tutorial.png)

1. 在 "**创建 Azure Cosmos db 帐户**" 页上, 输入新的 Azure Cosmos DB 帐户的设置, 包括位置。

    <!-- Resource selection -->  
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    设置|值|说明
    ---|---|---
    订购|*Concierge 订阅*|选择您的 Concierge 订阅。 如果您没有看到列出的 Concierge 订阅, 则您的订阅上启用了多个租户, 您需要更改租户。 为此, 请使用以下门户链接再次登录:[用于沙盒的 Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。
    资源组|使用现有<br><br><rgn>[沙盒资源组名称]</rgn>|选择 "**使用现有**", 然后输入<rgn>[沙盒资源组名称]</rgn>。
    帐户名称|*输入一个唯一的名称*|输入唯一名称以标识此 Azure Cosmos DB 帐户。 由于将*documents.azure.com*追加到您提供的用于创建 URI 的 ID, 因此请使用唯一但可识别的 id。<br><br>ID 只能包含小写字母、数字和连字符 (-) 字符, 并且必须包含3到31个字符。
    API|SQL|API 确定要创建的帐户类型。 Azure Cosmos DB 提供了五个 api 来满足您的应用程序需求: SQL (document database)、Gremlin (graph 数据库)、MongoDB (文档数据库)、Azure 表和 Cassandra, 每个用户都需要一个单独的帐户。 <br><br>选择**SQL** , 因为在此模块中, 您要创建可使用 sql 语法查询且可通过 sql API 访问的文档数据库。|
    位置|*选择最接近你的区域*|从上述区域列表中选择离你最近的地区。
    地域冗余| 启用 | 此设置在第二个 (成对的) 区域中创建数据库的复制版本。 将此设置保留为 "现在禁用", 因为稍后将对数据库进行复制。
    多区域写入 | 启用 | 通过此设置, 您可以同时写入多个区域。 仅可在创建帐户过程中配置此设置。

1. 单击 "**审阅 + 创建**"。

    ![Azure Cosmos DB 的 "新建帐户" 页](../media/2-global-distribution/2-azure-cosmos-db-create-new-account.png)

1. 验证设置后, 单击 "**创建**" 以创建帐户。

1. 帐户创建需要几分钟的时间。 等待门户显示部署成功的通知并单击通知。

    ![通知警报](../media/2-global-distribution/2-azure-cosmos-db-notification.png)

1. 在通知窗口中, 单击 "**转到资源**"。

    ![转到资源](../media/2-global-distribution/2-azure-cosmos-db-go-to-resource.png)

    门户将显示**恭喜!已创建 Azure Cosmos DB 帐户**页面。

    ![Azure 门户通知窗格](../media/2-global-distribution/2-azure-cosmos-db-account-created.png)

## <a name="replicate-data-in-multiple-regions"></a>复制多个区域中的数据

现在, 让我们在洛杉矶、纽约和东京中复制离您最近的全局用户的数据库。

1. 在 "帐户" 页中, 单击菜单中的 "从**全局处复制数据**"。
1. 在 "在**全局复制数据**" 页中, 选择 "美国西部 2"、"东 us" 和 "日本东部地区", 然后单击 "**保存**"。

    如果在 Azure 门户中看不到地图, 请将屏幕左侧的菜单最小化以显示它。

    页面将在向新区域写入数据时显示**更新**消息。 新区域中的数据将在30分钟内可用。

    ![单击地图中的区域以将其添加](../media/2-global-distribution/2-global-replication.gif)

## <a name="summary"></a>摘要

在此单元中, 您将数据库复制到您的用户最集中的世界区域, 从而为其提供对网站上数据的低延迟访问。
