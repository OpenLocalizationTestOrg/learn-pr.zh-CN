现在, 我们想要通过编写代码来读取队列中的下一封邮件, 并对其进行处理并将其从队列中删除来完成该应用程序。 

我们打算将此代码放入同一个应用程序中, 并在未传递任何参数时执行此代码, 但在我们的新闻服务方案中, 我们实际上会将此代码放入中间层服务器来处理这些情景。

## <a name="dequeue-a-message"></a>取消邮件排队

让我们添加一个新方法, 从队列中检索下一封邮件。

1. 在编辑器`Program.cs`中打开源文件。

1. 在名为`Program` `ReceiveArticleAsync`的类中创建静态方法, 该方法不采用任何`Task<string>`参数并返回。 我们将使用此方法从队列中提取新闻文章并将其返回。
    - 继续执行并将`async`关键字添加到方法, 因为我们将使用一些基于异步`Task`的方法。

    ```csharp
    static async Task<string> ReceiveArticleAsync()
    {
    }

1. All of the setup code to get a `CloudQueue` will be identical to what we did in the last exercise. Code duplication is a bad habit, even in samples so go ahead and, refactor the code that obtains the `CloudQueue` to a new method named `GetQueue` and change the `SendArticleAsync` to use your new method.
     - Make sure to leave the code that _creates_ the queue in the `SendArticleAsync` method; remember only the **publisher** should create the queue.

    ```csharp
    const string ConnectionString = ...;
    // ...

    static CloudQueue GetQueue()
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        return queueClient.GetQueueReference("newsqueue");
    }
    ```
    
1. 在您`ReceiveArticleAsync`的方法中, 调用`GetQueue`新方法以检索您的队列引用并将其分配给变量。

1. 接下来, 对`ExistsAsync` `CloudQueue`对象调用方法;这将返回是否已创建队列。 如果我们尝试从不存在的队列中检索邮件, 该 API 将引发异常。
    - 此方法是异步方法, `await`因此可用于获取返回值。
    - 您应该已经对`async` `ReceiveArticleAsync`方法使用了关键字, 但现在不添加它。


1. 将使用`if`返回值的块添加到`ExistsAsync`。 我们将添加代码以将队列中的值读取到块中。 向方法添加最后一个返回字符串, 以指示未读取任何值。 您的方法应如下所示:

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
    }

    return "<queue empty or not created>";
}
```

1. 对`GetMessageAsync`要从`CloudQueue`队列中获取第一个`CloudQueueMessage`的对象的调用。 如果队列是空的`null` , 返回值将为。

1. 如果不为 null, 则对该`AsString` `CloudQueueMessage`对象使用属性以获取邮件的内容。

1. 对`DeleteMessageAsync`要从`CloudQueue`队列中删除邮件的对象调用。

最终方法实现应类似于:

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
        CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
        if (retrievedArticle != null)
        {
            string newsMessage = retrievedArticle.AsString;
            await queue.DeleteMessageAsync(retrievedArticle);
            return newsMessage;
        }
    }

    return "<queue empty or not created>";
}
```

## <a name="call-the-receivearticleasync-method"></a>调用 ReceiveArticleAsync 方法

最后, 让我们添加支持, 以调用我们的新方法。 当我们未将任何参数传递到程序中时, 我们将执行此操作。

1. 找到您`Main`之前添加的用于`if`查找参数的方法并专门添加的块。

1. 添加一个`else`条件并调用`ReceiveArticleAsync`方法。 

1. 由于它是异步的, 因此`await`请使用关键字检索结果并将其打印到控制台窗口。 如果未将应用转换为 c # 7.1, 则可以使用返回的任务中`Result`的属性获取该值。

您的代码应类似于以下内容:

```csharp
if (args.Length > 0)
{
    // ...
}
else
{
    string value = await ReceiveArticleAsync();
    Console.WriteLine($"Received {value}");
}
```

## <a name="execute-the-application"></a>执行应用程序

代码现已完成。 它现在可以发送和检索邮件。 

> [!WARNING]
> 在生成和运行程序之前, 请确保已将所有文件保存在联机编辑器中。

若要对其进行`dotnet run`测试, 请使用并传递参数以发送邮件, 并保留用于读取单个邮件的参数。

如果要测试队列不存在的时间, 可以使用 Azure CLI 删除队列 (和所有数据)。 请确保替换`<connection-string>`参数 (或设置环境变量)。

```azurecli
az storage queue delete --name newsqueue --connection-string <connection-string> 
```

下次添加邮件时, 应重新创建该队列。

> [!NOTE]
> 删除操作实际上是异步进行的。 如果尚未完成, 则在尝试重新创建队列时可能会收到异常。