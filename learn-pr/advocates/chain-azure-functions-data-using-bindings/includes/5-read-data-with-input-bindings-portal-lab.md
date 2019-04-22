假设您想要创建一个简单的书签查找服务。 您的服务最初是只读的。 如果用户想要查找条目, 则会向其发送 ID 为的请求, 并返回该 URL。 下面的流程图对流进行了说明:

![显示在我们的 Cosmos DB 后端中查找书签的过程的流程图。 当 Azure 函数接收到包含书签 id 的请求时, 它首先检查该请求是否有效, 如果不生成错误响应。 对于有效的请求, 函数将检查 Cosmos DB 中是否存在书签 id (如果不存在, 则会生成错误响应)。 如果找到了书签 id, 则会生成成功响应。](../media/5-find-bookmark-flow-small.png)

当用户向你发送带有一些文本的请求时, 请尝试在后端数据库中查找包含此文本的条目作为密钥或 ID。 您将返回一个结果, 指示是否找到了该条目。

您需要将数据存储在某个位置。 在此流程图中, 数据存储是一个 Azure Cosmos DB 实例。 但如何从函数连接到数据库并读取数据？ 在函数世界中, 可以为该作业配置*输入绑定*。  通过 Azure 门户配置绑定非常简单。 正如您很快就会看到的, 您不必为打开存储连接这样的任务编写代码。 Azure 函数运行时和绑定会为你处理这些任务。

## <a name="create-an-azure-cosmos-db-account"></a>创建 Azure Cosmos DB 帐户

> [!NOTE]
> 本单元不是 Azure Cosmos DB 上的教程。 如果您有兴趣在完成本模块后了解详细信息, 请在 Cosmos DB 上提供完整的学习路径。

### <a name="create-a-database-account"></a>创建数据库帐户

数据库帐户是用于管理一个或多个数据库的容器。 在可以创建数据库之前, 我们需要创建一个数据库帐户。

1. 请确保使用随激活沙盒的相同帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 选择 "**创建资源**" 按钮 (位于 Azure 门户的左上角), 然后选择 "**数据库** > **azure Cosmos DB**"。

1. 在 "**创建 azure Cosmos db 帐户**" 页中, 输入新的 Azure Cosmos DB 帐户的设置。

    |设置  |值  |说明  |
    |---------|---------|---------|
    |订购     |  Concierge 订阅       |  要用于此 Azure Cosmos DB 帐户的 Azure 订阅。       |
    |资源组     |   <rgn>[沙盒资源组名称]</rgn>      |  将使用沙盒中的资源组预填充此字段。       |
    |帐户名称     | *输入一个唯一的名称*        |  输入唯一名称以标识此 Azure Cosmos DB 帐户。 由于`documents.azure.com`将追加到您为创建 URI 而提供的名称, 因此请使用唯一但可识别的名称。<br><br>帐户名称只能包含小写字母、数字和连字符 (-) 字符, 并且必须包含3到50个字符。       |
    |API     | Core (SQL)        |  API 确定要创建的帐户类型。 Azure Cosmos DB 提供了五个 api 来满足您的应用程序的需求: SQL (document database)、Gremlin (graph 数据库)、MongoDB (文档数据库)、Azure 表和 Cassandra, 每个当前需要一个单独的帐户。 <br><br>选择 " **Core (SQL)**"。 目前, Azure Cosmos DB trigger、input 绑定和输出绑定仅适用于 SQL API 和 Graph API 帐户。        |
    |位置     | 从列表中选择        | 选择最接近的一个, 也可以是下面列出的允许的*沙盒区域*之一。        |

     将**新帐户**边栏中的所有其他字段保留为其默认值。

    ### <a name="sandbox-regions"></a>沙盒区域
    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]


1. 选择 "**审阅 + 创建**" 以查看和验证配置。 

1. 在下一个屏幕上, 选择 "**创建**" 设置和部署数据库帐户。

1. 部署可能需要一些时间。 因此, 在继续之前, 请等待通知中心中的 "**部署已成功**" 消息。

    ![已完成数据库帐户部署的通知](../media/5-db-deploy-success.PNG)

1. 选择 "**转到资源**" 以导航到门户中的数据库帐户。 接下来, 我们将向数据库中添加一个集合。

### <a name="add-a-collection"></a>添加集合

在 Cosmos DB 中,*容器*包含用户生成的任意实体。 对于 SQL 和 MongoDB API 帐户, 容器映射到*集合*。 在集合中, 我们存储文档。

我们来使用 Azure 门户中的数据资源管理器工具来创建数据库和集合。

1. 选择 "**数据资源管理器** > **新集合**"。

2. 在 "**添加集合**" 下, 输入新集合的设置。

    >[!TIP]
    >"**添加集合**" 区域显示在最右侧。 您可能需要向右滚动才能看到它。

    |设置|建议值|说明
    |---|---|---|
    |数据库 ID|[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]| 数据库名称必须包含1到255个字符, 并且不能包含/、 \\、#、? 或尾部空格。<br><br>您可以随意在此处输入所需的内容, 但我们[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]建议将其作为新数据库的名称, 这就是我们在此单位中要参考的内容。 |
    |集合 ID|[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]|输入[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]作为新集合的名称。 集合 id 与数据库名称具有相同的字符要求。|
    |分区键|**/id**| partition 键指定 Cosmos DB 集合中的文档分布在逻辑数据分区中的方式。 为了方便起见, `id`我们将使用字段, 因为我们不关注此模块中的数据库性能。 若要了解有关 Cosmos 数据库分区键策略的详细信息, 请浏览 Microsoft 学习 Cosmos DB 模块。|
    |提高|1000 RU|将吞吐量更改为每秒1000个请求单元 (RU/秒)。 如果要减少延迟, 可以在以后扩展性能。|

3. 单击"确定"。 数据资源管理器显示新的数据库和集合。 现在, 我们有一个数据库。 在数据库中, 我们定义了一个集合。 接下来, 我们将添加一些数据 (也称为 "文档")。

### <a name="add-test-data"></a>添加测试数据

我们在名[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]为的数据库中定义了一个集合。 我们想要在每个文档中存储 URL 和 ID, 如网页书签列表。

您将使用数据浏览器将数据添加到新集合中。

1. 在数据资源管理器中, 新数据库将显示在 "集合" 窗格中。 展开[!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]数据库, 展开[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]集合, 选择 "**文档**", 然后选择 "**新建文档**"。

2. 将新文档的默认内容替换为以下 JSON。

     ```json
     {
         "id": "docs",
         "URL": "https://docs.microsoft.com/azure"
     }
     ```

3. 将 JSON 添加到 "**文档**" 选项卡后, 选择 "**保存**"。

    请注意, 有些属性比我们添加的属性多。 它们都以下划线 (_rid、_self、_etag、_attachments、_ts) 开头。 这些是由系统生成的用于帮助管理文档的属性。

    |属性  |说明  |
    |---------|---------|
    | `_rid`     |     资源 ID 是一个唯一的标识符, 它在资源模型上也按资源堆栈为层次结构。 它在内部用于放置和导航文档资源。    |
    | `_self`     |   资源的唯一可寻址 URI。      |
    | `_etag`     |   对于开放式并发控制是必需的。     |
    | `_attachments`     |  附件资源的可寻址路径。       |
    | `_ts`     |    此资源的上次更新时间戳。    |

4. 让我们向集合中添加更多文档。 使用以下内容创建另外四个文档。 请记住保存您的工作。

    ```json
    {
        "id": "portal",
        "URL": "https://portal.azure.com"
    }
    ```

    ```json
    {
        "id": "learn",
        "URL": "https://docs.microsoft.com/learn"
    }
    ```

    ```json
    {
        "id": "marketplace",
        "URL": "https://azuremarketplace.microsoft.com/marketplace/apps"
    }
    ```

    ```json
    {
        "id": "blog",
        "URL": "https://azure.microsoft.com/blog"
    }
    ```

1. 完成后, 您的集合应如下所示:

    ![门户中的 SQL API UI, 显示添加到书签集合中的项的列表。](../media/5-db-bookmark-coll.PNG)

您现在在书签集合中有几个条目。 我们的方案将按如下方式工作。 如果请求收到 (例如, "id = 文档"), 您将在书签集合中查找该 id 并返回 URL `https://docs.microsoft.com/azure`。 让我们创建一个用于查找此集合中的值的 Azure 函数。

## <a name="create-your-function"></a>创建函数

1. 导航到在前面的单元中创建的函数应用程序。

1. 选择 "**函数**"**+** 旁边的 "**添加**" () 按钮以启动函数创建过程。 
   页面显示一组完整的受支持的触发器。

1. 选择**HTTP 触发器**

1. 使用以下值填写显示在右侧的 "**新建函数**" 对话框。

    | Field | 值 |
    |----------|--------|
    | 名称     | [!INCLUDE [func-name-find](./func-name-find.md)] |
    | 授权级别 | **函数** |

1. 选择 "**创建**" 以创建函数。
    此操作将在代码编辑器中打开该 *.js*文件, 并显示 HTTP 触发的函数的默认实现。

### <a name="verify-the-function"></a>验证函数

您可以通过测试新函数来验证我们已完成的操作, 如下所示:

1. 在新函数中, 单击右上角的 "**获取函数 URL** ", 选择 "**默认 (功能键)**", 然后单击 "**复制**"。

1. 将复制的函数 URL 粘贴到浏览器的地址栏中。 将查询字符串值`&name=<yourname>`添加到 URL 的末尾, 然后按**enter**以执行请求。 应在浏览器中获取 Azure 函数权限的响应。

现在我们已开始使用我们的基本功能, 我们将重点介绍如何从 Azure Cosmos DB 或我们的方案 (我们[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)]的集合) 中读取数据。

## <a name="add-an-azure-cosmos-db-input-binding"></a>添加 Azure Cosmos DB 输入绑定

若要从数据库中读取数据, 需要定义输入绑定。 正如您所看到的, 可以配置一个绑定, 只需几个步骤即可与您的数据库进行对话。

1. 在左窗格中选择 "**集成**" 以打开 "集成" 选项卡。您使用的模板创建了一个 http 触发器和一个 http 输出绑定。 现在, 添加新的 Azure Cosmos DB 输入绑定。

1. 在 "**输入**" 列中选择 "**新建输入**"。
   将显示所有可能的输入绑定类型的列表。

1. 在列表中, 选择 " **Azure Cosmos DB**", 然后选择 "**选择**"。
   此操作将打开 "Azure Cosmos DB 输入配置" 页。 接下来, 您将设置与您的数据库的连接。

1. 如果在**Azure Cosmos DB 输入**配置 UI 中出现以下消息, 告诉您必须安装扩展, 请选择 "**安装**"。 

    ![HTTP 触发 Azure 函数的默认 JavaScript 实现](../media/extension-not-installed.png)

    > [!NOTE]
    > 安装扩展可能需要一段时间, 因此请等待安装完成, 然后再继续执行下一步。

1. 在 " **Azure Cosmos DB 帐户连接**" 框旁边, 选择 "**新建**"。
   此操作将打开 "**连接**" 窗口, 该窗口已选择 " **azure Cosmos DB 帐户**" 和 "azure 订阅"。 剩下的唯一事情是选择数据库帐户 ID。

1. 在 "创建数据库帐户" 部分中, 必须提供 ID 值。 在 "**数据库帐户**" 下拉列表中找到该值, 然后单击 "**选择**"。

1. 已配置与数据库的新连接, 并显示在 " **Azure Cosmos DB 帐户连接**" 字段中。 如果您想了解此抽象名称的实际背后的内容, 请单击 "*显示值*" 以显示连接字符串。

您想要查找具有特定 ID 的书签, 让我们将接收到的 id 与绑定的 id 关联起来。

1. 在 "**文档 ID (可选)** " 字段中`{id}`, 输入。 此语法称为*绑定表达式*。 此函数由 HTTP 请求触发, 该请求使用查询字符串指定要查找的 ID。 由于 id 在集合中是唯一的, 因此绑定将返回0个 (未找到) 或1个 (找到的) 文档。

1. 使用下表中的值仔细填写本页上的其余字段。 您可以随时单击每个字段名称右侧的信息图标, 以了解有关每个字段的用途的详细信息。

    |设置  |值  |说明  |
    |---------|---------|---------|
    |文档参数名称     |  **书签**       |  用于标识代码中的此绑定的名称。      |
    |数据库名称     |  [!INCLUDE [cosmos-db-name](./cosmos-db-name.md)]       | 要使用的数据库。 此值是我们在本课前面设置的数据库名称。        |
    |集合名称     |  [!INCLUDE [cosmos-db-name](./cosmos-coll-name.md)]        | 将从中读取数据的集合。 此设置是在本课前面的部分定义的。 |
    |SQL 查询 (可选)    |   保留为空       |   我们仅基于 ID 在一次检索一个文档。 因此, 使用 "文档 ID" 字段进行筛选比在此实例中使用 SQL 查询更好。 我们可以手工创建一个 SQL 查询, 以返回一个`SELECT * from b where b.ID = {id}`条目 ()。 该查询确实会返回一个文档, 但会将其返回到文档集合中。 我们的代码必须不必要地处理集合。 当您想要获取多个文档时, 请使用 SQL 查询方法。   |
    |分区键 (可选) | **号** |  在前面创建[!INCLUDE [cosmos-coll-name](./cosmos-coll-name.md)] Cosmos DB 集合时, 添加已定义的分区键。  此处输入的项 (在输入绑定格式`{<key>}`中指定) 必须与集合中的键相匹配。|

9. 选择 "**保存**" 以保存对此绑定配置所做的所有更改。

现在, 您已定义绑定, 现在可以在您的函数中使用它了。

## <a name="update-function-implementation"></a>更新函数实现

1. 选择您[!INCLUDE [func-name-find](./func-name-find.md)]的函数, 在代码编辑器中打开*node.js* 。 您已添加了要从数据库读取的输入绑定, 因此请更新逻辑以使用此绑定。

2. 将*index .js*中的所有代码替换为以下代码段中的代码, 然后单击 "**保存**"。

   [!code-javascript[](../code/find-bookmark-single.js)]

传入的 HTTP 请求将触发函数, 并将`id`查询参数传递给 Cosmos DB 输入绑定。 如果数据库找到与此 ID 匹配的文档, 则会将`bookmark`该参数设置为找到的文档。 在这种情况下, 我们将构建一个响应, 其中包含在书签标记的文档中找到的 URL 值。 如果找不到与此键匹配的文档, 我们将使用有效负载和状态代码进行响应, 告知用户出现坏消息。

## <a name="try-it-out"></a>试用

1. 选择右上角的 "**获取函数 URL** ", 选择 "**默认 (功能键)**", 然后选择 "**复制**" 以复制函数的 URL。

2. 将复制的函数 URL 粘贴到浏览器的地址栏中。 将查询字符串值`&id=docs`添加到此 URL 的末尾, 然后按键盘`Enter`上的键以执行请求。 您应该会看到一个包含指向该资源的 URL 的响应。

3. 将`&id=docs`替换`&id=missing`为, 并观察响应。

    >[!TIP]
    >您还可以使用 function portal UI 中的 "**测试**" 选项卡来测试函数。 您可以添加查询参数或提供请求正文, 以获取与前面步骤中所述相同的结果。

在此单位中, 我们已手动创建了第一个输入绑定, 以从 Azure Cosmos DB 数据库进行读取。 我们为搜索数据库和读取数据而编写的代码量最小, 这归功于绑定。 我们做的大部分工作都以声明方式配置绑定, 而平台负责处理 rest。

在下一个单元中, 我们将通过 Azure Cosmos DB 输出绑定向书签集合中添加更多数据。