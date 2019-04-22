数据库中的多个文档经常需要同时更新。 

对于您的在线零售版应用程序, 当用户下订单并想要使用优惠券代码、信用卡或被除数 (或同时是这三个) 时, 您需要为这些选项查询其帐户, 并对其帐户进行更新以表明他们使用了这些选项。、更新订单总计和处理订单。

所有这些操作都需要在一个事务中同时发生。 如果用户选择取消订单, 您希望回滚更改而不修改其帐户信息, 以便他们的优惠券代码、片尾和红利可用于下一次购买。

在 Azure Cosmos DB 中执行这些事务的方法是使用存储过程和用户定义的函数 (udf)。 存储过程是确保 ACID (原子性、一致性、隔离、持久性) 事务的唯一方法, 因为它们在服务器上运行, 因而称为服务器端编程。 udf 也存储在服务器上, 并在查询过程中用于对值或文档中的文档执行计算逻辑。 

在本模块中, 你将了解存储过程和 udf, 然后在门户中运行一些。

## <a name="stored-procedure-basics"></a>存储过程基础知识

存储过程对文档和属性执行复杂的事务。 存储过程是在 JavaScript 中编写的, 并存储在 Azure Cosmos DB 上的集合中。 通过对数据库引擎执行存储过程并接近数据, 可以提高客户端编程的性能。

存储过程是在 Azure Cosmos DB 中实现原子事务的唯一方法;客户端 sdk 不支持事务。

此外, 建议在存储过程中执行批处理操作, 因为减少了创建单独的事务的必要性。

## <a name="stored-procedure-example"></a>存储过程示例

下面的示例是一个简单的 HelloWorld 存储过程, 它可获取当前上下文并发送显示 "Hello, World" 的响应。

```javascript
function helloWorld() {
    var context = getContext();
    var response = context.getResponse();

    response.setBody("Hello, World");
}
```

## <a name="user-defined-function-basics"></a>用户定义的函数基础知识

udf 用于扩展 Azure Cosmos DB SQL 查询语言语法, 并实现自定义业务逻辑, 例如对属性和文档的计算。 udf 只能在内部查询中调用, 与存储过程不同, 它们不具有对 context 对象的访问权限, 因此它们无法读取或写入文档。

在在线商务方案中, UDF 可用于确定要应用于订单总计或应用于产品或订单的折扣百分比的增值税。

## <a name="user-defined-function-example"></a>用户定义的函数示例

下面的示例创建 UDF 以根据产品成本计算虚构公司产品中的税:

```javascript
function producttax(price) {
    if (price == undefined) 
        throw 'no input';

    var amount = parseFloat(price);

    if (amount < 1000) 
        return amount * 0.1;
    else if (amount < 10000) 
        return amount * 0.2;
    else
        return amount * 0.4;
}
```

## <a name="create-a-stored-procedure-in-the-portal"></a>在门户中创建存储过程

让我们在门户中创建一个新的存储过程。 门户将自动填充一个简单的存储过程, 用于检索集合中的第一个项目, 因此我们首先运行此存储过程。

1. 在 "数据浏览器" 中, 单击 "**新建存储过程**"。

    数据资源管理器显示带有示例存储过程的新选项卡。

2. 在 "**存储过程 Id** " 框中, 输入名称*示例*, 单击 "**保存**", 然后单击 "**执行**"。


3. 在 "**输入参数**" 框中, 键入分区键的名称*33218896*, 然后单击 "**执行**"。 请注意, 存储过程在单个分区中工作。

    ![在门户中运行存储过程](../media/6-stored-procedure.gif)

    **结果**窗格将显示集合中第一个文档的源。

## <a name="create-a-stored-procedure-that-creates-documents"></a>创建创建文档的存储过程

现在, 让我们创建一个创建文档的存储过程。

1. 在 "数据浏览器" 中, 单击 "**新建存储过程**"。 将此存储过程命名为*createMyDocument*, 将以下代码复制并粘贴到**存储过程正文**框中, 单击 "**保存**", 然后单击 "**执行**"。

    ```javascript
    function createMyDocument() {
        var context = getContext();
        var collection = context.getCollection();

        var doc = {
            "id": "3",
            "productId": "33218898",
            "description": "Contoso microfleece zip-up jacket",
            "price": "44.99"
        };

        var accepted = collection.createDocument(collection.getSelfLink(),
            doc,
            function (err, documentCreated) {
                if (err) throw new Error('Error' + err.message);
                context.getResponse().setBody(documentCreated)
            });
        if (!accepted) return;
    }
    ```

2. 在 "输入参数" 框中, 输入分区项值*33218898*, 然后单击 "**执行**"。

    数据资源管理器将在结果区域中显示新创建的文档。

    您可以返回到 "文档" 选项卡, 单击 "**刷新**" 按钮, 然后查看新文档。 

## <a name="create-a-user-defined-function"></a>创建用户定义函数

现在, 让我们在数据资源管理器中创建一个 UDF。

在 "数据浏览器" 中, 单击 "**新建 UDF**"。 您可能需要单击 "**新建存储 Prodedure** " 旁边的向下箭头以查看**新的 UDF**。 将下面的代码复制到窗口中, 命名 UDF *producttax*, 然后单击 "**保存**"。

```javascript
function producttax(price) {
    if (price == undefined) 
        throw 'no input';

    var amount = parseFloat(price);

    if (amount < 1000) 
        return amount * 0.1;
    else if (amount < 10000) 
        return amount * 0.2;
    else
        return amount * 0.4;
}
```

定义 UDF 后, 转到 "**查询 1** " 选项卡, 并将以下查询复制并粘贴到查询区域中, 以运行 UDF。

```sql
SELECT c.id, c.productId, c.price, udf.producttax(c.price) AS producttax FROM c
```
