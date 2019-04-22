现在, 您已经了解了可以创建哪些类型的查询, 我们将使用 Azure 门户中的数据浏览器检索和筛选您的产品数据。

在 "数据浏览器" 窗口中, 请注意, 默认情况下, "**文档**" 选项`SELECT * FROM c`卡上的查询设置为, 如下图所示。 此默认查询检索并显示集合中的所有文档。

![数据资源管理器中的默认查询是从 c 中选择 *](../media/5-azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a>创建新查询

1. 在数据资源管理器中, 单击 "**新建 SQL 查询**"。 请注意, "新建**查询 1** " 选项卡上的默认`SELECT * from c`查询再次返回, 这将返回集合中的所有文档。 

1. 单击 "**执行查询**"。 此查询将返回数据库中的所有结果。

    ![通过添加 ORDER by _ts DESC 并单击 "应用筛选器" 来更改默认查询](../media/5-azure-cosmosdb-data-explorer-edit-query.png)

2. 现在, 让我们运行在上一个设备中讨论的一些查询。 在 "查询" 选项卡`SELECT * from c`上, 删除、复制并粘贴以下查询, 然后单击 "**执行查询**":

    ```sql
    SELECT * 
    FROM Products p 
    WHERE p.id ="1"
    ```

    结果返回的产品的`productId`为1。

    ![id 为1的查询](../media/5-azure-cosmosdb-data-explorer-query-by-id.png)

3. 删除以前的查询, 复制并粘贴以下查询, 然后单击 "**执行查询**"。 此查询返回按价格以升序排序的所有产品的价格、说明和产品 ID。
 
    ```sql
    SELECT p.price, p.description, p.productId 
    FROM Products p 
    ORDER BY p.price ASC
    ```

## <a name="summary"></a>摘要

现在, 您已对 Azure Cosmos DB 中的数据完成了一些基本查询。 