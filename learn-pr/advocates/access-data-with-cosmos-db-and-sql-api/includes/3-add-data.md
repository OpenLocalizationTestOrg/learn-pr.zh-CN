将数据添加到你的 Azure Cosmos DB 数据库非常简单。 您打开 Azure 门户, 导航到您的数据库, 并使用数据资源管理器将 JSON 文档添加到数据库中。 有更高级的添加数据的方法, 但我们将从这里开始, 因为数据浏览器是一个很好的工具, 可让你熟悉 Azure Cosmos DB 提供的内部工作原理和功能。

## <a name="what-is-the-data-explorer"></a>数据浏览器是什么？
azure Cosmos DB 数据浏览器是 azure 门户中包含的一个工具, 用于管理 azure Cosmos DB 中存储的数据。 它提供了用于查看和导航数据集合的 UI, 以及用于编辑数据库中的文档、查询数据以及创建和运行存储过程的 UI。

## <a name="add-data-using-the-data-explorer"></a>使用数据资源管理器添加数据

1. 使用与激活沙盒时相同的帐户登录到[沙盒的 Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

    > [!IMPORTANT]
    > 使用相同的帐户登录到 Azure 门户和沙盒。
    >
    > 使用上面的链接登录到 Azure 门户, 以确保您已连接到沙盒, 该沙箱提供对 Concierge 订阅的访问权限。

1. 单击 "**所有服务** > **数据库** > " "**Azure Cosmos DB**"。 然后选择您的帐户, 单击 "**数据资源管理器**", 然后单击 "以**全屏打开**"。

   ![在 Azure 门户中的数据资源管理器中创建新文档](../media/3-azure-cosmosdb-data-explorer-full-screen.png)

2. 在 "**打开**全屏显示" 框中, 单击 "**打开**"。

    web 浏览器将显示新的全屏数据浏览器, 这将为您提供更多空间和用于处理数据库的专用环境。

3. 若要创建新的 JSON 文档, 请在 "SQL API" 窗格中, 展开 "**衣服**", 单击 "**文档**", 然后单击 "**新建文档**"。

   ![在 Azure 门户中的数据资源管理器中创建新文档](../media/3-azure-cosmosdb-data-explorer-new-document.png)

4. 现在, 使用以下结构将文档添加到集合中。 只需将以下代码复制并粘贴到 "**文档**" 选项卡中, 即可覆盖当前内容:

     ```json
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
    }
     ```

5. 将 JSON 添加到 "**文档**" 选项卡后, 单击 "**保存**"。

    ![在 Azure 门户中复制 JSON 数据并单击 "在数据资源管理器中保存"](../media/3-azure-cosmosdb-data-explorer-save-document.png)

6. 再次创建并保存一个文档, 再次单击 "**新建文档**", 并将以下 JSON 对象复制到 "数据资源管理器" 中, 然后单击 "**保存**"。

     ```json
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "price": "49.99",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
           }
        }
    }
     ```

7. 单击左侧菜单上的 "**文档**", 确认已保存文档。

    "数据资源管理器" 在 "**文档**" 选项卡中显示两个文档。

在此单位中, 您将使用数据浏览器将两个文档 (每个文档都表示产品目录中的产品) 添加到数据库中。 数据浏览器是创建文档、修改文档以及开始使用 Azure Cosmos DB 的好方法。
