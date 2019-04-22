队列保留邮件-其形状已知的发件人应用程序和收件人应用程序的数据数据包。 发件人创建队列并添加邮件。 收件人检索邮件, 对其进行处理, 然后从队列中删除邮件。 下图显示了此过程的典型流程。

![显示通过 Azure 队列的典型邮件流的插图。](../media/6-message-flow.png)

请注意`get` , `delete`和是单独的操作。 这种排列处理接收器中的潜在故障并实现一种_至少称为一次性传递_的概念。 接收器收到一条消息后, 该消息将保留在队列中, 但不可见30秒。 如果接收器在处理过程中崩溃或遇到断电故障, 则永远不会从队列中删除该邮件。 30秒后, 该邮件将重新显示在队列中, 并且收件人的另一个实例可以将其处理为完成。

## <a name="the-azure-storage-client-library-for-net"></a>适用于 .net 的 Azure 存储客户端库

**适用于 .net 的 Azure 存储客户端库**提供了用于表示您需要与之交互的每个对象的类型:

- `CloudStorageAccount`表示你的 Azure 存储帐户。
- `CloudQueueClient`表示 Azure 队列存储。
- `CloudQueue`表示您的队列实例之一。
- `CloudQueueMessage`代表一封邮件。

您将使用这些类来获取对您的队列的编程访问权限。 库既有同步方法, 也有异步方法;您应首选使用异步版本以避免阻止客户端应用程序。

> [!NOTE]
> **WindowsAzure** NuGet 包中提供了适用于 .net 的 Azure 存储客户端库。 您可以通过 IDE、Azure CLI 或通过 PowerShell `Install-Package WindowsAzure.Storage`安装它。

## <a name="how-to-connect-to-a-queue"></a>如何连接到队列

若要连接到队列, 请首先`CloudStorageAccount`使用连接字符串创建。 然后`CloudQueueClient`, 生成的对象可以创建, 后者又可以打开`CloudQueue`实例。 基本代码流如下所示。

```csharp
CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudQueueClient client = account.CreateCloudQueueClient();

CloudQueue queue = client.GetQueueReference("myqueue");
```

创建的`CloudQueue`并不一定意味着_实际_存储队列存在。 但是, 可以使用此对象创建、删除和检查现有队列。 如前所述, 所有方法都支持同步和异步版本, 但我们仅使用基于此的`Task`异步版本。

## <a name="how-to-create-a-queue"></a>如何创建队列

将使用常见的队列创建模式: 发件人应用程序应始终负责创建队列。 这将使您的应用程序更独立且更不依赖于管理设置。 

若要简化创建过程, 客户端库会公开`CreateIfNotExistsAsync`创建队列的方法 (如有必要), 如果`false`队列已经存在, 则返回。 

典型代码如下所示。

```csharp
CloudQueue queue;
//...

await queue.CreateIfNotExistsAsync();
```

> [!NOTE]
> 您必须拥有`Write`存储`Create`帐户的或权限, 才能使用此 API。 如果使用**访问密钥**安全模型, 则始终为 true, 但可以使用将仅允许对队列进行读取操作的其他方法锁定对帐户的权限。

## <a name="how-to-send-a-message"></a>如何发送邮件

若要发送邮件, 需要实例化`CloudQueueMessage`对象。 类有几个重载构造函数, 用于将数据加载到邮件中。 我们将使用采用的构造函数`string`。 创建邮件后, 使用`CloudQueue`对象发送该邮件。

下面是一个典型的示例:

```csharp
var message = new CloudQueueMessage("your message here");

CloudQueue queue;
//...

await queue.AddMessageAsync(message);
```

> [!NOTE]
> 虽然队列总数最高可达 500 TB, 但其中的各个邮件的大小最大只能为 64 kb (使用 Base64 编码时的 48 KB)。 如果需要更大的负载, 可以将队列和 blob 组合在一起, 将 URL 传递给邮件中的实际数据 (存储为 Blob)。 利用此方法, 您可以将单个项目的排队设置为 200 GB。

## <a name="how-to-receive-and-delete-a-message"></a>如何接收和删除邮件

在接收器中, 您将获得下一封邮件, 进行处理, 然后在处理成功后将其删除。 下面是一个简单的示例:

```C#
CloudQueue queue;
//...

CloudQueueMessage message = await queue.GetMessageAsync();

if (message != null)
{
    // Process the message
    //...

    await queue.DeleteMessageAsync(message);
}
```

现在让我们将此新知识应用到我们的应用程序!