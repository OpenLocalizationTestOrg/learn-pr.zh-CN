<span data-ttu-id="90762-101">你已将所需的客户端库添加到应用程序, 并已准备好连接到你的 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="90762-101">You have added the required client libraries to your application and are ready to connect to your Azure storage account.</span></span>

<span data-ttu-id="90762-102">若要使用存储帐户中的数据, 应用将需要两个数据片段:</span><span class="sxs-lookup"><span data-stu-id="90762-102">To work with data in a storage account, your app will need two pieces of data:</span></span>

1. <span data-ttu-id="90762-103">一个访问键</span><span class="sxs-lookup"><span data-stu-id="90762-103">An access key</span></span>
1. <span data-ttu-id="90762-104">REST API 终结点</span><span class="sxs-lookup"><span data-stu-id="90762-104">The REST API endpoint</span></span>

## <a name="security-access-keys"></a><span data-ttu-id="90762-105">安全访问密钥</span><span class="sxs-lookup"><span data-stu-id="90762-105">Security access keys</span></span>

<span data-ttu-id="90762-106">每个存储帐户都有两个用于保护存储帐户的唯一_访问密钥_。</span><span class="sxs-lookup"><span data-stu-id="90762-106">Each storage account has two unique _access keys_ that are used to secure the storage account.</span></span> <span data-ttu-id="90762-107">如果您的应用程序需要连接到多个存储帐户, 则您的应用程序将需要每个存储帐户的访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-107">If your app needs to connect to multiple storage accounts, then your app will require an access key for each storage account.</span></span>

![显示连接到云中的两个不同存储帐户的应用程序的插图。](../media/6-multiple-accounts.png)

## <a name="rest-api-endpoint"></a><span data-ttu-id="90762-110">REST API 终结点</span><span class="sxs-lookup"><span data-stu-id="90762-110">REST API endpoint</span></span>

<span data-ttu-id="90762-111">除了访问存储帐户的身份验证密钥外, 您的应用程序还需要知道存储服务终结点才能发出 REST 请求。</span><span class="sxs-lookup"><span data-stu-id="90762-111">In addition to access keys for authentication to storage accounts, your app will need to know the storage service endpoints to issue the REST requests.</span></span> 

<span data-ttu-id="90762-112">REST 终结点是存储帐户_名称_、数据类型和已知域的组合。</span><span class="sxs-lookup"><span data-stu-id="90762-112">The REST endpoint is a combination of your storage account _name_, the data type, and a known domain.</span></span> <span data-ttu-id="90762-113">例如：</span><span class="sxs-lookup"><span data-stu-id="90762-113">For example:</span></span>

| <span data-ttu-id="90762-114">数据类型</span><span class="sxs-lookup"><span data-stu-id="90762-114">Data type</span></span> | <span data-ttu-id="90762-115">示例终结点</span><span class="sxs-lookup"><span data-stu-id="90762-115">Example endpoint</span></span> |
|-----------|------------------|
| <span data-ttu-id="90762-116">blob</span><span class="sxs-lookup"><span data-stu-id="90762-116">Blobs</span></span>     | `https://[name].blob.core.windows.net/` |
| <span data-ttu-id="90762-117">队列</span><span class="sxs-lookup"><span data-stu-id="90762-117">Queues</span></span>    | `https://[name].queue.core.windows.net/` |
| <span data-ttu-id="90762-118">Table</span><span class="sxs-lookup"><span data-stu-id="90762-118">Table</span></span>     | `https://[name].table.core.windows.net/` |
| <span data-ttu-id="90762-119">附件</span><span class="sxs-lookup"><span data-stu-id="90762-119">Files</span></span>     | `https://[name].file.core.windows.net/` |

<span data-ttu-id="90762-120">如果你有一个自定义域绑定到 Azure, 则还可以为终结点创建自定义域 URL。</span><span class="sxs-lookup"><span data-stu-id="90762-120">If you have a custom domain tied to Azure, then you can also create a custom domain URL for the endpoint.</span></span>

## <a name="connection-strings"></a><span data-ttu-id="90762-121">连接字符串</span><span class="sxs-lookup"><span data-stu-id="90762-121">Connection strings</span></span>

<span data-ttu-id="90762-122">在应用程序中处理访问键和终结点 url 的最简单方法是使用**存储帐户连接字符串**。</span><span class="sxs-lookup"><span data-stu-id="90762-122">The simplest way to handle access keys and endpoint URLs within applications is to use **storage account connection strings**.</span></span> <span data-ttu-id="90762-123">连接字符串在单个文本字符串中提供所有需要的连接信息。</span><span class="sxs-lookup"><span data-stu-id="90762-123">A connection string provides all needed connectivity information in a single text string.</span></span>

<span data-ttu-id="90762-124">Azure 存储连接字符串看起来与以下示例类似, 但具有特定存储帐户的访问密钥和帐户名称:</span><span class="sxs-lookup"><span data-stu-id="90762-124">Azure Storage connection strings look similar to the example below but with the access key and account name of your specific storage account:</span></span>

```
DefaultEndpointsProtocol=https;AccountName={your-storage};
   AccountKey={your-access-key};
   EndpointSuffix=core.windows.net
```

## <a name="security"></a><span data-ttu-id="90762-125">安全性</span><span class="sxs-lookup"><span data-stu-id="90762-125">Security</span></span>

<span data-ttu-id="90762-126">访问密钥对于提供对存储帐户的访问至关重要, 因此不应将其提供给您不希望对您的存储帐户具有访问权限的任何系统或个人。</span><span class="sxs-lookup"><span data-stu-id="90762-126">Access keys are critical to providing access to your storage account and as a result, should not be given to any system or person that you do not wish to have access to your storage account.</span></span> <span data-ttu-id="90762-127">访问密钥等效于访问你的计算机的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="90762-127">Access keys are the equivalent of a username and password to access your computer.</span></span>

<span data-ttu-id="90762-128">通常情况下, 存储帐户连接信息存储在环境变量、数据库或配置文件中。</span><span class="sxs-lookup"><span data-stu-id="90762-128">Typically, storage account connectivity information is stored within an environment variable, database, or configuration file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90762-129">请务必注意, 如果在源代码管理中包含该文件并将其存储在公共存储库中, 则将此信息存储在配置文件中可能会很危险。</span><span class="sxs-lookup"><span data-stu-id="90762-129">It is important to note that storing this information in a configuration file can be dangerous if you include that file in source control and store it in a public repository.</span></span> <span data-ttu-id="90762-130">这是一个常见错误, 它意味着任何人都可以浏览公用存储库中的源代码并查看您的存储帐户连接信息。</span><span class="sxs-lookup"><span data-stu-id="90762-130">This is a common mistake and means that anyone can browse your source code in the public repository and see your storage account connection information.</span></span>

<span data-ttu-id="90762-131">每个存储帐户有两个访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-131">Each storage account has two access keys.</span></span> <span data-ttu-id="90762-132">这样做的原因是, 在使存储帐户保持安全的安全最佳做法的一部分时, 应定期对密钥进行轮换 (重新生成)。</span><span class="sxs-lookup"><span data-stu-id="90762-132">The reason for this is to allow keys to be rotated (regenerated) periodically as part of security best practice in keeping your storage account secure.</span></span> <span data-ttu-id="90762-133">可以从 azure 门户或 azure CLI/PowerShell 命令行工具执行此过程。</span><span class="sxs-lookup"><span data-stu-id="90762-133">This process can be done from the Azure portal or the Azure CLI / PowerShell command line tool.</span></span>

<span data-ttu-id="90762-134">循环键会立即导致原始键值失效, 并将取消对任何未恰当获取密钥的用户的访问权限。</span><span class="sxs-lookup"><span data-stu-id="90762-134">Rotating a key will invalidate the original key value immediately and will revoke access to anyone who obtained the key inappropriately.</span></span> <span data-ttu-id="90762-135">通过对两个密钥的支持, 您可以旋转键, 而不会导致使用它们的应用程序中出现停机。</span><span class="sxs-lookup"><span data-stu-id="90762-135">With support for two keys, you can rotate keys without causing downtime in your applications that use them.</span></span> <span data-ttu-id="90762-136">您的应用程序可以在另一个密钥重新生成时切换到使用备用访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-136">Your app can switch to using the alternate access key while the other key is regenerated.</span></span> <span data-ttu-id="90762-137">如果您有多个使用此存储帐户的应用程序, 它们都应使用相同的密钥来支持此技术。</span><span class="sxs-lookup"><span data-stu-id="90762-137">If you have multiple apps using this storage account, they should all use the same key to support this technique.</span></span> <span data-ttu-id="90762-138">以下是基本想法:</span><span class="sxs-lookup"><span data-stu-id="90762-138">Here's the basic idea:</span></span>

1. <span data-ttu-id="90762-139">更新应用程序代码中的连接字符串以引用存储帐户的辅助访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-139">Update the connection strings in your application code to reference the secondary access key of the storage account.</span></span>
2. <span data-ttu-id="90762-140">使用 Azure 门户或命令行工具为你的存储帐户重新生成主访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-140">Regenerate the primary access key for your storage account using the Azure portal or command line tool.</span></span>
3. <span data-ttu-id="90762-141">更新代码中的连接字符串以引用新的主访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-141">Update the connection strings in your code to reference the new primary access key.</span></span>
4. <span data-ttu-id="90762-142">以相同方式重新生成辅助访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-142">Regenerate the secondary access key in the same manner.</span></span>

> [!TIP]
> <span data-ttu-id="90762-143">强烈建议您定期旋转访问密钥, 以确保它们保持私密, 就像更改密码一样。</span><span class="sxs-lookup"><span data-stu-id="90762-143">It's highly recommended that you periodically rotate your access keys to ensure they remain private, just like changing your passwords.</span></span> <span data-ttu-id="90762-144">如果您使用的是服务器应用程序中的密钥, 则可以使用**Azure key Vault**存储访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-144">If you are using the key in a server application, you can use an **Azure Key Vault** to store the access key for you.</span></span> <span data-ttu-id="90762-145">主要电子仓库包括支持直接与存储帐户同步并自动轮替密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-145">Key Vaults include support to synchronize directly to the Storage Account and automatically rotate the keys periodically.</span></span> <span data-ttu-id="90762-146">使用密钥存储库提供了额外的安全层, 因此您的应用程序永远不需要直接使用访问密钥。</span><span class="sxs-lookup"><span data-stu-id="90762-146">Using a Key Vault provides an additional layer of security, so your app never has to work directly with an access key.</span></span>

### <a name="shared-access-signatures-sas"></a><span data-ttu-id="90762-147">共享访问签名 (SAS)</span><span class="sxs-lookup"><span data-stu-id="90762-147">Shared access signatures (SAS)</span></span>

<span data-ttu-id="90762-148">访问密钥是对存储帐户的访问进行身份验证的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="90762-148">Access keys are the easiest approach to authenticating access to a storage account.</span></span> <span data-ttu-id="90762-149">但是, 它们提供对存储帐户中任何内容的完全访问权限, 类似于计算机上的根密码。</span><span class="sxs-lookup"><span data-stu-id="90762-149">However they provide full access to anything in the storage account, similar to a root password on a computer.</span></span>

<span data-ttu-id="90762-150">存储帐户提供了一种单独的身份验证机制, 称为_共享访问签名_, 在需要授予有限访问权限的方案中支持过期和受限权限。</span><span class="sxs-lookup"><span data-stu-id="90762-150">Storage accounts offer a separate authentication mechanism called _shared access signatures_ that support expiration and limited permissions for scenarios where you need to grant limited access.</span></span> <span data-ttu-id="90762-151">你应在允许其他用户读取数据并将数据写入你的存储帐户时使用此方法。</span><span class="sxs-lookup"><span data-stu-id="90762-151">You should use this approach when you are allowing other users to read and write data to your storage account.</span></span> <span data-ttu-id="90762-152">关于本高级主题的文档, 请参阅本模块结尾部分的链接。</span><span class="sxs-lookup"><span data-stu-id="90762-152">There are links to our documentation on this advanced topic at the end of the module.</span></span>
