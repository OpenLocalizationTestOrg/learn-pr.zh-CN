<span data-ttu-id="e3e85-101">现在我们拥有了一个存储帐户, 我们来看看如何处理它将包含的队列。</span><span class="sxs-lookup"><span data-stu-id="e3e85-101">Now that we have a storage account, let's look at how we work with the queue that it will hold.</span></span>

<span data-ttu-id="e3e85-102">若要访问队列, 需要三条信息:</span><span class="sxs-lookup"><span data-stu-id="e3e85-102">To access a queue, you need three pieces of information:</span></span>

 1. <span data-ttu-id="e3e85-103">存储帐户名称</span><span class="sxs-lookup"><span data-stu-id="e3e85-103">Storage account name</span></span>
 2. <span data-ttu-id="e3e85-104">队列名称</span><span class="sxs-lookup"><span data-stu-id="e3e85-104">Queue name</span></span>
 3. <span data-ttu-id="e3e85-105">授权令牌</span><span class="sxs-lookup"><span data-stu-id="e3e85-105">Authorization token</span></span>

<span data-ttu-id="e3e85-106">与队列通信的两个应用程序均使用此信息 (添加邮件的 web 前端和处理它们的中端)。</span><span class="sxs-lookup"><span data-stu-id="e3e85-106">This information is used by both applications that talk to the queue (the web front end that adds messages and the mid-tier that processes them).</span></span>

## <a name="queue-identity"></a><span data-ttu-id="e3e85-107">队列标识</span><span class="sxs-lookup"><span data-stu-id="e3e85-107">Queue identity</span></span>

<span data-ttu-id="e3e85-108">每个队列都具有您在创建过程中分配的名称。</span><span class="sxs-lookup"><span data-stu-id="e3e85-108">Every queue has a name that you assign during creation.</span></span> <span data-ttu-id="e3e85-109">名称在您的存储帐户中必须是唯一的, 但不需要全局唯一 (与存储帐户名称不同)。</span><span class="sxs-lookup"><span data-stu-id="e3e85-109">The name must be unique within your storage account but doesn't need to be globally unique (unlike the storage account name).</span></span>

<span data-ttu-id="e3e85-110">存储帐户名称和队列名称的组合唯一地标识队列。</span><span class="sxs-lookup"><span data-stu-id="e3e85-110">The combination of your storage account name and your queue name uniquely identifies a queue.</span></span>

## <a name="access-authorization"></a><span data-ttu-id="e3e85-111">访问授权</span><span class="sxs-lookup"><span data-stu-id="e3e85-111">Access authorization</span></span>

<span data-ttu-id="e3e85-112">对队列的每个请求都必须经过授权, 并且有多个选项可供选择。</span><span class="sxs-lookup"><span data-stu-id="e3e85-112">Every request to a queue must be authorized and there are several options to choose from.</span></span>

| <span data-ttu-id="e3e85-113">授权类型</span><span class="sxs-lookup"><span data-stu-id="e3e85-113">Authorization Type</span></span> | <span data-ttu-id="e3e85-114">说明</span><span class="sxs-lookup"><span data-stu-id="e3e85-114">Description</span></span> |
|--------------------|-------------|
| <span data-ttu-id="e3e85-115">**Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="e3e85-115">**Azure Active Directory**</span></span> | <span data-ttu-id="e3e85-116">您可以使用基于角色的身份验证, 并根据 AAD 凭据标识特定客户端。</span><span class="sxs-lookup"><span data-stu-id="e3e85-116">You can use role-based authentication and identify specific clients based on AAD credentials.</span></span> |
| <span data-ttu-id="e3e85-117">**共享密钥**</span><span class="sxs-lookup"><span data-stu-id="e3e85-117">**Shared Key**</span></span> | <span data-ttu-id="e3e85-118">有时也称为 "**帐户密钥**", 这是与存储帐户关联的加密密钥签名。</span><span class="sxs-lookup"><span data-stu-id="e3e85-118">Sometimes referred to as an **account key**, this is an encrypted key signature associated with the storage account.</span></span> <span data-ttu-id="e3e85-119">每个存储帐户都有两个可与每个请求一起传递的密钥, 以对访问进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e3e85-119">Every storage account has two of these keys that can be passed with each request to authenticate access.</span></span> <span data-ttu-id="e3e85-120">使用此方法就像使用根密码一样, 它提供对存储帐户的_完全访问权限_。</span><span class="sxs-lookup"><span data-stu-id="e3e85-120">Using this approach is like using a root password - it provides _full access_ to the storage account.</span></span> |
| <span data-ttu-id="e3e85-121">**共享访问签名**</span><span class="sxs-lookup"><span data-stu-id="e3e85-121">**Shared access signature**</span></span> | <span data-ttu-id="e3e85-122">共享访问签名 (sa) 是生成的 URI, 可向客户端授予对存储帐户中的对象的有限访问权限。</span><span class="sxs-lookup"><span data-stu-id="e3e85-122">A shared access signature (SAS) is a generated URI that grants limited access to objects in your storage account to clients.</span></span> <span data-ttu-id="e3e85-123">您可以限制对数据区域的特定资源、权限和范围的访问, 以在一段时间后自动关闭 access。</span><span class="sxs-lookup"><span data-stu-id="e3e85-123">You can restrict access to specific resources, permissions, and scope to a data range to automatically turn off access after a period of time.</span></span>  |

> [!NOTE]
> <span data-ttu-id="e3e85-124">我们将使用帐户密钥授权, 因为它是开始使用队列的最简单方法, 但建议您在生产应用程序中使用共享访问签名 (SAS) 或 Azure Active Directory (AAD)。</span><span class="sxs-lookup"><span data-stu-id="e3e85-124">We will use the account key authorization because it is the simplest way to get started working with queues, however it's recommended that you either use shared access signature (SAS) or Azure Active Directory (AAD) in production apps.</span></span>

### <a name="retrieving-the-account-key"></a><span data-ttu-id="e3e85-125">检索帐户密钥</span><span class="sxs-lookup"><span data-stu-id="e3e85-125">Retrieving the account key</span></span>
 
<span data-ttu-id="e3e85-126">您的帐户密钥在 Azure 门户中存储帐户的 "**设置 > 访问密钥**" 部分中可用, 也可以通过命令行检索它:</span><span class="sxs-lookup"><span data-stu-id="e3e85-126">Your account key is available in the **Settings > Access keys** section of your storage account in the Azure portal, or you can retrieve it through the command line:</span></span>

```azurecli
az storage account keys list ...
```

```powershell
Get-AzStorageAccountKey ...
```

## <a name="accessing-queues"></a><span data-ttu-id="e3e85-127">访问队列</span><span class="sxs-lookup"><span data-stu-id="e3e85-127">Accessing queues</span></span>

<span data-ttu-id="e3e85-128">使用 REST API 访问队列。</span><span class="sxs-lookup"><span data-stu-id="e3e85-128">You access a queue using a REST API.</span></span> <span data-ttu-id="e3e85-129">为此, 您将使用一个 URL, 该 URL 将您为存储帐户提供的名称与域`queue.core.windows.net`和要使用的队列的路径组合在一起。</span><span class="sxs-lookup"><span data-stu-id="e3e85-129">To do this, you'll use a URL that combines the name you gave the storage account with the domain `queue.core.windows.net` and the path to the queue you want to work with.</span></span> <span data-ttu-id="e3e85-130">例如: `http://<storage account>.queue.core.windows.net/<queue name>`。</span><span class="sxs-lookup"><span data-stu-id="e3e85-130">For example: `http://<storage account>.queue.core.windows.net/<queue name>`.</span></span> <span data-ttu-id="e3e85-131">每`Authorization`个请求都必须包含一个标头。</span><span class="sxs-lookup"><span data-stu-id="e3e85-131">An `Authorization` header must be included with every request.</span></span> <span data-ttu-id="e3e85-132">该值可以是三种授权样式中的任何一种。</span><span class="sxs-lookup"><span data-stu-id="e3e85-132">The value can be any of the three authorization styles.</span></span>

### <a name="using-the-azure-storage-client-library-for-net"></a><span data-ttu-id="e3e85-133">使用适用于 .net 的 Azure 存储客户端库</span><span class="sxs-lookup"><span data-stu-id="e3e85-133">Using the Azure Storage Client Library for .NET</span></span>

<span data-ttu-id="e3e85-134">适用于 .net 的 Azure 存储客户端库是 Microsoft 提供的库, 它由 Microsoft 为你 formulates rest 请求和分析 rest 响应。</span><span class="sxs-lookup"><span data-stu-id="e3e85-134">The Azure Storage Client Library for .NET is a library provided by Microsoft that formulates REST requests and parses REST responses for you.</span></span> <span data-ttu-id="e3e85-135">这极大地减少了需要编写的代码量。</span><span class="sxs-lookup"><span data-stu-id="e3e85-135">This greatly reduces the amount of code you need to write.</span></span> <span data-ttu-id="e3e85-136">使用客户端库的访问权限仍需要相同的信息段 (存储帐户名称、队列名称和帐户密钥);但是, 它们的组织方式不同。</span><span class="sxs-lookup"><span data-stu-id="e3e85-136">Access using the client library still requires the same pieces of information (storage account name, queue name, and account key); however, they are organized differently.</span></span>

<span data-ttu-id="e3e85-137">客户端库使用**连接字符串**建立连接。</span><span class="sxs-lookup"><span data-stu-id="e3e85-137">The client library uses a **connection string** to establish your connection.</span></span> <span data-ttu-id="e3e85-138">您的连接字符串在 azure 门户中的存储帐户的 "**设置**" 部分中, 或通过 Azure CLI 和 PowerShell 提供。</span><span class="sxs-lookup"><span data-stu-id="e3e85-138">Your connection string is available in the **Settings** section of your Storage Account in the Azure portal, or through the Azure CLI and PowerShell.</span></span>

<span data-ttu-id="e3e85-139">连接字符串是一个字符串, 它将存储帐户名称和帐户密钥组合在一起, 并且必须知道应用程序才能访问存储帐户。</span><span class="sxs-lookup"><span data-stu-id="e3e85-139">A connection string is a string that combines a storage account name and account key and must be known to the application to access the storage account.</span></span> <span data-ttu-id="e3e85-140">格式如下所示:</span><span class="sxs-lookup"><span data-stu-id="e3e85-140">The format looks like this:</span></span>

```csharp
string connectionString = "DefaultEndpointsProtocol=https;AccountName=<your storage account name>;AccountKey=<your key>;EndpointSuffix=core.windows.net"
```

> [!WARNING]
> <span data-ttu-id="e3e85-141">此字符串值应存储在安全位置, 因为有权访问此连接字符串的任何人都可以操作队列。</span><span class="sxs-lookup"><span data-stu-id="e3e85-141">This string value should be stored in a secure location since anyone who has access to this connection string would be able to manipulate the queue.</span></span>

<span data-ttu-id="e3e85-142">请注意, 连接字符串不包括队列名称。</span><span class="sxs-lookup"><span data-stu-id="e3e85-142">Notice that the connection string doesn't include the queue name.</span></span> <span data-ttu-id="e3e85-143">当您建立与队列的连接时, 将在代码中提供队列名称。</span><span class="sxs-lookup"><span data-stu-id="e3e85-143">The queue name is supplied in your code when you establish a connection to the queue.</span></span>

<span data-ttu-id="e3e85-144">我们来获取来自 Azure 的连接字符串, 并设置新的应用程序以使用它。</span><span class="sxs-lookup"><span data-stu-id="e3e85-144">Let's get our connection string from Azure and set up a new application to use it.</span></span>