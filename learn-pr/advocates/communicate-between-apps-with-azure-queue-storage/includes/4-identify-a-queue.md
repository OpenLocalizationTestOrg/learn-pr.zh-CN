现在我们拥有了一个存储帐户, 我们来看看如何处理它将包含的队列。

若要访问队列, 需要三条信息:

 1. 存储帐户名称
 2. 队列名称
 3. 授权令牌

与队列通信的两个应用程序均使用此信息 (添加邮件的 web 前端和处理它们的中端)。

## <a name="queue-identity"></a>队列标识

每个队列都具有您在创建过程中分配的名称。 名称在您的存储帐户中必须是唯一的, 但不需要全局唯一 (与存储帐户名称不同)。

存储帐户名称和队列名称的组合唯一地标识队列。

## <a name="access-authorization"></a>访问授权

对队列的每个请求都必须经过授权, 并且有多个选项可供选择。

| 授权类型 | 说明 |
|--------------------|-------------|
| **Azure Active Directory** | 您可以使用基于角色的身份验证, 并根据 AAD 凭据标识特定客户端。 |
| **共享密钥** | 有时也称为 "**帐户密钥**", 这是与存储帐户关联的加密密钥签名。 每个存储帐户都有两个可与每个请求一起传递的密钥, 以对访问进行身份验证。 使用此方法就像使用根密码一样, 它提供对存储帐户的_完全访问权限_。 |
| **共享访问签名** | 共享访问签名 (sa) 是生成的 URI, 可向客户端授予对存储帐户中的对象的有限访问权限。 您可以限制对数据区域的特定资源、权限和范围的访问, 以在一段时间后自动关闭 access。  |

> [!NOTE]
> 我们将使用帐户密钥授权, 因为它是开始使用队列的最简单方法, 但建议您在生产应用程序中使用共享访问签名 (SAS) 或 Azure Active Directory (AAD)。

### <a name="retrieving-the-account-key"></a>检索帐户密钥
 
您的帐户密钥在 Azure 门户中存储帐户的 "**设置 > 访问密钥**" 部分中可用, 也可以通过命令行检索它:

```azurecli
az storage account keys list ...
```

```powershell
Get-AzStorageAccountKey ...
```

## <a name="accessing-queues"></a>访问队列

使用 REST API 访问队列。 为此, 您将使用一个 URL, 该 URL 将您为存储帐户提供的名称与域`queue.core.windows.net`和要使用的队列的路径组合在一起。 例如: `http://<storage account>.queue.core.windows.net/<queue name>`。 每`Authorization`个请求都必须包含一个标头。 该值可以是三种授权样式中的任何一种。

### <a name="using-the-azure-storage-client-library-for-net"></a>使用适用于 .net 的 Azure 存储客户端库

适用于 .net 的 Azure 存储客户端库是 Microsoft 提供的库, 它由 Microsoft 为你 formulates rest 请求和分析 rest 响应。 这极大地减少了需要编写的代码量。 使用客户端库的访问权限仍需要相同的信息段 (存储帐户名称、队列名称和帐户密钥);但是, 它们的组织方式不同。

客户端库使用**连接字符串**建立连接。 您的连接字符串在 azure 门户中的存储帐户的 "**设置**" 部分中, 或通过 Azure CLI 和 PowerShell 提供。

连接字符串是一个字符串, 它将存储帐户名称和帐户密钥组合在一起, 并且必须知道应用程序才能访问存储帐户。 格式如下所示:

```csharp
string connectionString = "DefaultEndpointsProtocol=https;AccountName=<your storage account name>;AccountKey=<your key>;EndpointSuffix=core.windows.net"
```

> [!WARNING]
> 此字符串值应存储在安全位置, 因为有权访问此连接字符串的任何人都可以操作队列。

请注意, 连接字符串不包括队列名称。 当您建立与队列的连接时, 将在代码中提供队列名称。

我们来获取来自 Azure 的连接字符串, 并设置新的应用程序以使用它。