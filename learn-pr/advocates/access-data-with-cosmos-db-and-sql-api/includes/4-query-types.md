使用作为查询目标添加到数据库中的两个文档, 让我们逐步了解一些查询基础知识。 Azure Cosmos DB 使用 sql 查询 (就像 sql Server) 执行查询操作。 默认情况下会自动为所有属性编制索引, 因此数据库中的所有数据将立即可供查询。

## <a name="sql-query-basics"></a>SQL 查询基础知识
每个 SQL 查询都包含一个 SELECT 子句以及可选的 from 和 WHERE 子句。 此外, 还可以添加其他子句, 如 ORDER BY 和 JOIN, 以获取所需的信息。

SQL 查询具有以下格式:

    SELECT <select_list>
    [FROM <optional_from_specification>]
    [WHERE <optional_filter_condition>]
    [ORDER BY <optional_sort_specification>]
    [JOIN <optional_join_specification>]

## <a name="select-clause"></a>SELECT 子句

SELECT 子句确定在执行查询时将生成的值的类型。 值`SELECT *`表示返回整个 JSON 文档。

**查询**
```
SELECT *
FROM Products p
WHERE p.id ="1"
```

**返回**
```
[
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
        },
        "_rid": "iAEeANrzNAAJAAAAAAAAAA==",
        "_self": "dbs/iAEeAA==/colls/iAEeANrzNAA=/docs/iAEeANrzNAAJAAAAAAAAAA==/",
        "_etag": "\"00003a02-0000-0000-0000-5b9208440000\"",
        "_attachments": "attachments/",
        "_ts": 1536297028
    }
]
```

或者, 您可以通过在 SELECT 子句中包含属性列表, 将输出限制为仅包含某些属性。 在下面的查询中, 仅返回 ID、制造商和产品说明。

**查询**
```
SELECT 
    p.id, 
    p.manufacturer, 
    p.description
FROM Products p
WHERE p.id ="1"
```

**返回**
```
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a>from 子句

FROM 子句指定查询运行时所依据的数据源。 您可以使整个集合成为查询源, 也可以指定集合的子集。 from 子句是可选的, 除非在查询中稍后对源进行筛选或计划。

一个查询`SELECT * FROM Products` , 例如, "整个产品集合" 是枚举查询所依据的源。

集合可以`SELECT p.id FROM Products AS p`是别名, 如或简单`SELECT p.id FROM Products p`, 其中`p`的等效项。 `Products` `AS`是用于别名标识符的可选关键字。

一旦别名, 便无法绑定原始源。 例如, 语法`SELECT Products.id FROM Products p`无效, 因为无法再解析标识符 "Products"。

需要引用的所有属性都必须是完全限定的。 如果没有严格的架构遵从性, 则会强制执行此项以避免任何不明确的绑定。 因此, `SELECT id FROM Products p`在语法上无效, 因为`id`该属性不受绑定。

### <a name="subdocuments-in-a-from-clause"></a>FROM 子句中的子文档
也可以将源简化为较小的子集。 例如, 若要仅枚举每个文档中的子树, subroot 可能会成为源, 如以下示例所示:

**查询**
```
SELECT * 
FROM Products.shipping
```

**引起**  

```
[
    {
        "weight": 1,
        "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
        }
    },
    {
        "weight": 2,
        "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
        }
    }
]
```

虽然上面的示例使用数组作为源, 但还可以将对象用作源, 如下例所示。 源中可以找到的任何有效的 JSON 值 (未定义) 都将被视为包含在查询结果中。 如果某些产品没有`shipping.weight`值, 则会将其排除在查询结果中。

**查询**

    SELECT * 
    FROM Products.shipping.weight

**引起**

    [
        1,
        2
    ]

## <a name="where-clause"></a>WHERE 子句
WHERE 子句指定源提供的 JSON 文档必须满足的条件, 才能将其作为结果的一部分包括在内。 任何 JSON 文档都必须将指定的条件评估为**true** , 以便对结果进行考虑。 WHERE 子句是可选的。

以下查询请求包含值为1的 ID 的文档:

**查询**

    SELECT p.description
    FROM Products p 
    WHERE p.id = "1"

**引起**

    [
        {
            "description": "Quick dry crew neck t-shirt"
        }
    ]

## <a name="order-by-clause"></a>ORDER by 子句

order BY 子句使您能够按升序或降序对结果进行排序。

下面的 ORDER by 查询返回按价格排序的所有产品的价格、说明和产品 ID, 以升序排列:

**查询**

    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC

**引起**

```
[
    {
        "price": "14.99",
        "description": "Quick dry crew neck t-shirt",
        "productId": "33218896"
    },
    {
        "price": "49.99",
        "description": "Black wool pea-coat",
        "productId": "33218897"
    }
]
```

## <a name="join-clause"></a>JOIN 子句

JOIN 子句使您能够执行与文档和文档 subroots 的内部联接。 因此, 在产品数据库中, 可以使用送货数据加入文档。  

在下面的查询中, 为每个具有装运方法的产品返回产品 id。 如果添加的第三个产品没有发货属性, 则结果将相同, 因为第三个项目不包含发货属性。

**查询**

    SELECT p.productId
    FROM Products p
    JOIN p.shipping

**引起**

    [
        {
            "productId": "33218896"
        },
        {
            "productId": "33218897"
        }
    ]

## <a name="geospatial-queries"></a>地理空间查询

地理空间查询使您能够使用 GeoJSON 点执行空间查询。 通过使用数据库中的坐标, 可以计算两个点之间的距离, 并确定是点、多边形还是 LineString 在另一个点、多边形还是 LineString 中。

对于产品目录数据, 这将使您的用户能够输入其位置信息, 并确定是否有任何存储区中是否存在具有要查找的项的50英里的 radius。 

## <a name="summary"></a>摘要

能够在将所有数据添加到 Azure Cosmos DB 并使用熟悉的 SQL 查询技术的情况中快速查询所有数据, 可以帮助您和您的客户探索并深入了解存储的数据。