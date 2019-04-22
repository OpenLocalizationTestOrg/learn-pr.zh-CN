<span data-ttu-id="e1644-101">使用作为查询目标添加到数据库中的两个文档, 让我们逐步了解一些查询基础知识。</span><span class="sxs-lookup"><span data-stu-id="e1644-101">Using the two documents you added to the database as the target of our queries, let's walk through some query basics.</span></span> <span data-ttu-id="e1644-102">Azure Cosmos DB 使用 sql 查询 (就像 sql Server) 执行查询操作。</span><span class="sxs-lookup"><span data-stu-id="e1644-102">Azure Cosmos DB uses SQL queries, just like SQL Server, to perform query operations.</span></span> <span data-ttu-id="e1644-103">默认情况下会自动为所有属性编制索引, 因此数据库中的所有数据将立即可供查询。</span><span class="sxs-lookup"><span data-stu-id="e1644-103">All properties are automatically indexed by default, so all data in the database is instantly available to query.</span></span>

## <a name="sql-query-basics"></a><span data-ttu-id="e1644-104">SQL 查询基础知识</span><span class="sxs-lookup"><span data-stu-id="e1644-104">SQL query basics</span></span>
<span data-ttu-id="e1644-105">每个 SQL 查询都包含一个 SELECT 子句以及可选的 from 和 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="e1644-105">Every SQL query consists of a SELECT clause and optional FROM and WHERE clauses.</span></span> <span data-ttu-id="e1644-106">此外, 还可以添加其他子句, 如 ORDER BY 和 JOIN, 以获取所需的信息。</span><span class="sxs-lookup"><span data-stu-id="e1644-106">In addition, you can add other clauses like ORDER BY and JOIN to get the information you need.</span></span>

<span data-ttu-id="e1644-107">SQL 查询具有以下格式:</span><span class="sxs-lookup"><span data-stu-id="e1644-107">A SQL query has the following format:</span></span>

    SELECT <select_list>
    [FROM <optional_from_specification>]
    [WHERE <optional_filter_condition>]
    [ORDER BY <optional_sort_specification>]
    [JOIN <optional_join_specification>]

## <a name="select-clause"></a><span data-ttu-id="e1644-108">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="e1644-108">SELECT clause</span></span>

<span data-ttu-id="e1644-109">SELECT 子句确定在执行查询时将生成的值的类型。</span><span class="sxs-lookup"><span data-stu-id="e1644-109">The SELECT clause determines the type of values that will be produced when the query is executed.</span></span> <span data-ttu-id="e1644-110">值`SELECT *`表示返回整个 JSON 文档。</span><span class="sxs-lookup"><span data-stu-id="e1644-110">A value of `SELECT *` indicates that the entire JSON document is returned.</span></span>

<span data-ttu-id="e1644-111">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-111">**Query**</span></span>
```
SELECT *
FROM Products p
WHERE p.id ="1"
```

<span data-ttu-id="e1644-112">**返回**</span><span class="sxs-lookup"><span data-stu-id="e1644-112">**Returns**</span></span>
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

<span data-ttu-id="e1644-113">或者, 您可以通过在 SELECT 子句中包含属性列表, 将输出限制为仅包含某些属性。</span><span class="sxs-lookup"><span data-stu-id="e1644-113">Or, you can limit the output to include only certain properties by including a list of properties in the SELECT clause.</span></span> <span data-ttu-id="e1644-114">在下面的查询中, 仅返回 ID、制造商和产品说明。</span><span class="sxs-lookup"><span data-stu-id="e1644-114">In the following query, only the ID, manufacturer, and product description are returned.</span></span>

<span data-ttu-id="e1644-115">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-115">**Query**</span></span>
```
SELECT 
    p.id, 
    p.manufacturer, 
    p.description
FROM Products p
WHERE p.id ="1"
```

<span data-ttu-id="e1644-116">**返回**</span><span class="sxs-lookup"><span data-stu-id="e1644-116">**Returns**</span></span>
```
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a><span data-ttu-id="e1644-117">from 子句</span><span class="sxs-lookup"><span data-stu-id="e1644-117">FROM clause</span></span>

<span data-ttu-id="e1644-118">FROM 子句指定查询运行时所依据的数据源。</span><span class="sxs-lookup"><span data-stu-id="e1644-118">The FROM clause specifies the data source upon which the query operates.</span></span> <span data-ttu-id="e1644-119">您可以使整个集合成为查询源, 也可以指定集合的子集。</span><span class="sxs-lookup"><span data-stu-id="e1644-119">You can make the whole collection the source of the query or you can specify a subset of the collection instead.</span></span> <span data-ttu-id="e1644-120">from 子句是可选的, 除非在查询中稍后对源进行筛选或计划。</span><span class="sxs-lookup"><span data-stu-id="e1644-120">The FROM clause is optional unless the source is filtered or projected later in the query.</span></span>

<span data-ttu-id="e1644-121">一个查询`SELECT * FROM Products` , 例如, "整个产品集合" 是枚举查询所依据的源。</span><span class="sxs-lookup"><span data-stu-id="e1644-121">A query such as `SELECT * FROM Products` indicates that the entire Products collection is the source over which to enumerate the query.</span></span>

<span data-ttu-id="e1644-122">集合可以`SELECT p.id FROM Products AS p`是别名, 如或简单`SELECT p.id FROM Products p`, 其中`p`的等效项。 `Products`</span><span class="sxs-lookup"><span data-stu-id="e1644-122">A collection can be aliased, such as `SELECT p.id FROM Products AS p` or simply `SELECT p.id FROM Products p`, where `p` is the equivalent of `Products`.</span></span> <span data-ttu-id="e1644-123">`AS`是用于别名标识符的可选关键字。</span><span class="sxs-lookup"><span data-stu-id="e1644-123">`AS` is an optional keyword to alias the identifier.</span></span>

<span data-ttu-id="e1644-124">一旦别名, 便无法绑定原始源。</span><span class="sxs-lookup"><span data-stu-id="e1644-124">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="e1644-125">例如, 语法`SELECT Products.id FROM Products p`无效, 因为无法再解析标识符 "Products"。</span><span class="sxs-lookup"><span data-stu-id="e1644-125">For example, `SELECT Products.id FROM Products p` is syntactically invalid because the identifier "Products" cannot be resolved anymore.</span></span>

<span data-ttu-id="e1644-126">需要引用的所有属性都必须是完全限定的。</span><span class="sxs-lookup"><span data-stu-id="e1644-126">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="e1644-127">如果没有严格的架构遵从性, 则会强制执行此项以避免任何不明确的绑定。</span><span class="sxs-lookup"><span data-stu-id="e1644-127">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="e1644-128">因此, `SELECT id FROM Products p`在语法上无效, 因为`id`该属性不受绑定。</span><span class="sxs-lookup"><span data-stu-id="e1644-128">Therefore, `SELECT id FROM Products p` is syntactically invalid because the property `id` is not bound.</span></span>

### <a name="subdocuments-in-a-from-clause"></a><span data-ttu-id="e1644-129">FROM 子句中的子文档</span><span class="sxs-lookup"><span data-stu-id="e1644-129">Subdocuments in a FROM clause</span></span>
<span data-ttu-id="e1644-130">也可以将源简化为较小的子集。</span><span class="sxs-lookup"><span data-stu-id="e1644-130">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="e1644-131">例如, 若要仅枚举每个文档中的子树, subroot 可能会成为源, 如以下示例所示:</span><span class="sxs-lookup"><span data-stu-id="e1644-131">For instance, to enumerate only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="e1644-132">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-132">**Query**</span></span>
```
SELECT * 
FROM Products.shipping
```

<span data-ttu-id="e1644-133">**引起**</span><span class="sxs-lookup"><span data-stu-id="e1644-133">**Results**</span></span>  

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

<span data-ttu-id="e1644-134">虽然上面的示例使用数组作为源, 但还可以将对象用作源, 如下例所示。</span><span class="sxs-lookup"><span data-stu-id="e1644-134">Although the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example.</span></span> <span data-ttu-id="e1644-135">源中可以找到的任何有效的 JSON 值 (未定义) 都将被视为包含在查询结果中。</span><span class="sxs-lookup"><span data-stu-id="e1644-135">Any valid JSON value (that's not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="e1644-136">如果某些产品没有`shipping.weight`值, 则会将其排除在查询结果中。</span><span class="sxs-lookup"><span data-stu-id="e1644-136">If some products don’t have a `shipping.weight` value, they are excluded in the query result.</span></span>

<span data-ttu-id="e1644-137">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-137">**Query**</span></span>

    SELECT * 
    FROM Products.shipping.weight

<span data-ttu-id="e1644-138">**引起**</span><span class="sxs-lookup"><span data-stu-id="e1644-138">**Results**</span></span>

    [
        1,
        2
    ]

## <a name="where-clause"></a><span data-ttu-id="e1644-139">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="e1644-139">WHERE clause</span></span>
<span data-ttu-id="e1644-140">WHERE 子句指定源提供的 JSON 文档必须满足的条件, 才能将其作为结果的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="e1644-140">The WHERE clause specifies the conditions that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="e1644-141">任何 JSON 文档都必须将指定的条件评估为**true** , 以便对结果进行考虑。</span><span class="sxs-lookup"><span data-stu-id="e1644-141">Any JSON document must evaluate the specified conditions to **true** to be considered for the result.</span></span> <span data-ttu-id="e1644-142">WHERE 子句是可选的。</span><span class="sxs-lookup"><span data-stu-id="e1644-142">The WHERE clause is optional.</span></span>

<span data-ttu-id="e1644-143">以下查询请求包含值为1的 ID 的文档:</span><span class="sxs-lookup"><span data-stu-id="e1644-143">The following query requests documents that contain an ID whose value is 1:</span></span>

<span data-ttu-id="e1644-144">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-144">**Query**</span></span>

    SELECT p.description
    FROM Products p 
    WHERE p.id = "1"

<span data-ttu-id="e1644-145">**引起**</span><span class="sxs-lookup"><span data-stu-id="e1644-145">**Results**</span></span>

    [
        {
            "description": "Quick dry crew neck t-shirt"
        }
    ]

## <a name="order-by-clause"></a><span data-ttu-id="e1644-146">ORDER by 子句</span><span class="sxs-lookup"><span data-stu-id="e1644-146">ORDER BY clause</span></span>

<span data-ttu-id="e1644-147">order BY 子句使您能够按升序或降序对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="e1644-147">The ORDER BY clause enables you to order the results in ascending or descending order.</span></span>

<span data-ttu-id="e1644-148">下面的 ORDER by 查询返回按价格排序的所有产品的价格、说明和产品 ID, 以升序排列:</span><span class="sxs-lookup"><span data-stu-id="e1644-148">The following ORDER BY query returns the price, description, and product ID for all products, ordered by price, in ascending order:</span></span>

<span data-ttu-id="e1644-149">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-149">**Query**</span></span>

    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC

<span data-ttu-id="e1644-150">**引起**</span><span class="sxs-lookup"><span data-stu-id="e1644-150">**Results**</span></span>

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

## <a name="join-clause"></a><span data-ttu-id="e1644-151">JOIN 子句</span><span class="sxs-lookup"><span data-stu-id="e1644-151">JOIN clause</span></span>

<span data-ttu-id="e1644-152">JOIN 子句使您能够执行与文档和文档 subroots 的内部联接。</span><span class="sxs-lookup"><span data-stu-id="e1644-152">The JOIN clause enables you to perform inner joins with the document and the document subroots.</span></span> <span data-ttu-id="e1644-153">因此, 在产品数据库中, 可以使用送货数据加入文档。</span><span class="sxs-lookup"><span data-stu-id="e1644-153">So in the product database, for example, you can join the documents with the shipping data.</span></span>  

<span data-ttu-id="e1644-154">在下面的查询中, 为每个具有装运方法的产品返回产品 id。</span><span class="sxs-lookup"><span data-stu-id="e1644-154">In the following query, the product IDs are returned for each product that has a shipping method.</span></span> <span data-ttu-id="e1644-155">如果添加的第三个产品没有发货属性, 则结果将相同, 因为第三个项目不包含发货属性。</span><span class="sxs-lookup"><span data-stu-id="e1644-155">If you added a third product that didn't have a shipping property, the result would be the same because the third item would be excluded for not having a shipping property.</span></span>

<span data-ttu-id="e1644-156">**查询**</span><span class="sxs-lookup"><span data-stu-id="e1644-156">**Query**</span></span>

    SELECT p.productId
    FROM Products p
    JOIN p.shipping

<span data-ttu-id="e1644-157">**引起**</span><span class="sxs-lookup"><span data-stu-id="e1644-157">**Results**</span></span>

    [
        {
            "productId": "33218896"
        },
        {
            "productId": "33218897"
        }
    ]

## <a name="geospatial-queries"></a><span data-ttu-id="e1644-158">地理空间查询</span><span class="sxs-lookup"><span data-stu-id="e1644-158">Geospatial queries</span></span>

<span data-ttu-id="e1644-159">地理空间查询使您能够使用 GeoJSON 点执行空间查询。</span><span class="sxs-lookup"><span data-stu-id="e1644-159">Geospatial queries enable you to perform spatial queries using GeoJSON Points.</span></span> <span data-ttu-id="e1644-160">通过使用数据库中的坐标, 可以计算两个点之间的距离, 并确定是点、多边形还是 LineString 在另一个点、多边形还是 LineString 中。</span><span class="sxs-lookup"><span data-stu-id="e1644-160">Using the coordinates in the database, you can calculate the distance between two points and determine whether a Point, Polygon, or LineString is within another Point, Polygon, or LineString.</span></span>

<span data-ttu-id="e1644-161">对于产品目录数据, 这将使您的用户能够输入其位置信息, 并确定是否有任何存储区中是否存在具有要查找的项的50英里的 radius。</span><span class="sxs-lookup"><span data-stu-id="e1644-161">For product catalog data, this would enable your users to enter their location information and determine whether there were any stores within a 50-mile radius that have the item they're looking for.</span></span> 

## <a name="summary"></a><span data-ttu-id="e1644-162">摘要</span><span class="sxs-lookup"><span data-stu-id="e1644-162">Summary</span></span>

<span data-ttu-id="e1644-163">能够在将所有数据添加到 Azure Cosmos DB 并使用熟悉的 SQL 查询技术的情况中快速查询所有数据, 可以帮助您和您的客户探索并深入了解存储的数据。</span><span class="sxs-lookup"><span data-stu-id="e1644-163">Being able to quickly query all your data after adding it to Azure Cosmos DB and using familiar SQL query techniques can help you and your customers to explore and gain insights into your stored data.</span></span>