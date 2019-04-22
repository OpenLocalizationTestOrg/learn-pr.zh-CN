您的公司已选择 "Azure Cosmos DB" 以满足其扩展客户和基础产品的要求。 您已完成创建数据库的任务。

第一步是创建 Azure Cosmos DB 帐户。

## <a name="what-is-an-azure-cosmos-db-account"></a>什么是 Azure Cosmos DB 帐户？

azure Cosmos DB 帐户是充当数据库的组织实体的 azure 资源。 它将你的使用情况连接到 Azure 订阅以供计费。

每个 azure Cosmos DB 帐户都与 azure Cosmos db 支持的多个数据模型之一相关联, 并且您可以根据需要创建任意多个帐户。

如果要创建新的应用程序, 则 SQL API 是首选的数据模型。 如果使用的是图形或表格, 或者将 MongoDB 或 Cassandra 数据迁移到 Azure, 请创建其他帐户并选择相关的数据模型。

创建帐户时, 请选择对你有意义的 ID;您可以通过它标识帐户。 此外, 在 Azure 区域中创建与用户最接近的帐户, 以最大限度地减少数据中心和用户之间的延迟。

你可以选择在创建帐户的过程中设置虚拟网络和地域冗余, 但也可以在以后执行此操作。 在本模块中, 我们将不会启用这些设置。

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>在门户中创建 Azure Cosmos DB 帐户

1. 使用与激活沙盒时相同的帐户登录到[沙盒的 Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

    > [!IMPORTANT]
    > 使用上面的链接登录到 Azure 门户, 以确保您已连接到沙盒, 该沙箱提供对 Concierge 订阅的访问权限。

1. 单击 "**创建资源** > **数据库** > " "**Azure Cosmos DB**"。

   ![Azure portal 数据库窗格](../media/2-create-nosql-db-databases-json-tutorial.png)

1. 在 "**创建 Azure Cosmos db 帐户**" 页上, 输入新的 Azure Cosmos DB 帐户的设置, 包括位置。

    [!INCLUDE[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    设置|值|说明
    ---|---|---
    订购|*Concierge 订阅*|选择 "Concierge" 订阅。 如果您没有看到列出的 Concierge 订阅, 则您的订阅上启用了多个租户, 您需要更改租户。 为此, 请使用以下门户链接再次登录:[用于沙盒的 Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。
    资源组|使用现有<br><br>**<rgn>[沙盒资源组名称]</rgn>**|在这里, 您可以创建新的资源组, 也可以选择订阅中现有的资源组。
    帐户名称|*输入一个唯一的名称*|输入唯一名称以标识此 Azure Cosmos DB 帐户。 由于将*documents.azure.com*追加到您提供的用于创建 URI 的 ID, 因此请使用唯一但可识别的 id。<br><br>ID 只能包含小写字母、数字和连字符 (-) 字符, 并且必须包含3到31个字符。
    API|SQL|API 确定要创建的帐户类型。 Azure Cosmos DB 提供了五个 api 来满足您的应用程序需求: SQL (document database)、Gremlin (graph 数据库)、MongoDB (文档数据库)、Azure 表和 Cassandra, 每个用户都需要一个单独的帐户。 <br><br>Select **Core (SQL)** , 因为在此模块中, 您要创建可使用 sql 语法查询且可通过 sql API 访问的文档数据库。|
    位置|*从上面的列表中选择离你最近的地区*|选择数据库应位于的位置。
    地域冗余| 启用 | 此设置在第二个 (成对的) 区域中创建数据库的复制版本。 将此集保留为 "立即禁用", 因为稍后可复制数据库。
    多区域写入 | 启用 | 通过此设置, 您可以同时写入多个区域。

1. 单击 "**审阅 + 创建**"。

    ![Azure Cosmos DB 的 "新建帐户" 页](../media/2-azure-cosmos-db-create-new-account.png)

1. 验证设置后, 单击 "**创建**" 以创建帐户。

1. 帐户创建需要几分钟的时间。 等待门户显示部署成功的通知并单击通知。

    ![通知警报](../media/2-azure-cosmos-db-notification.png)

1. 在通知窗口中, 单击 "**转到资源**"。

    ![转到资源](../media/2-azure-cosmos-db-go-to-resource.png)

    门户将显示**恭喜!已创建 Azure Cosmos DB 帐户**页面。

    ![Azure 门户通知窗格](../media/2-azure-cosmos-db-account-created.png)

## <a name="summary"></a>摘要

您已创建 azure Cosmos db 帐户, 这是创建 azure Cosmos db 数据库的第一步。 您为数据类型选择了适当的设置, 并设置了帐户位置以最大限度地减少用户的延迟。
