<span data-ttu-id="09411-101">Azure 存储提供 REST API 以使用存储在每个帐户中的容器和数据。</span><span class="sxs-lookup"><span data-stu-id="09411-101">Azure Storage provides a REST API to work with the containers and data stored in each account.</span></span> <span data-ttu-id="09411-102">有一些独立的 api 可用于处理可存储的每种数据类型。</span><span class="sxs-lookup"><span data-stu-id="09411-102">There are independent APIs available to work with each type of data you can store.</span></span> <span data-ttu-id="09411-103">请记住, 我们有四种特定的数据类型:</span><span class="sxs-lookup"><span data-stu-id="09411-103">Recall that we have four specific data types:</span></span>

- <span data-ttu-id="09411-104">非结构化数据 (如二进制文件和文本文件) 的**blob** 。</span><span class="sxs-lookup"><span data-stu-id="09411-104">**Blobs** for unstructured data such as binary and text files.</span></span>
- <span data-ttu-id="09411-105">持久邮件传递的**队列**。</span><span class="sxs-lookup"><span data-stu-id="09411-105">**Queues** for persistent messaging.</span></span>
- <span data-ttu-id="09411-106">键/值的结构化存储**表**。</span><span class="sxs-lookup"><span data-stu-id="09411-106">**Tables** for structured storage of key/values.</span></span>
- <span data-ttu-id="09411-107">用于传统 SMB 文件共享的**文件**。</span><span class="sxs-lookup"><span data-stu-id="09411-107">**Files** for traditional SMB file shares.</span></span>

## <a name="using-the-rest-api"></a><span data-ttu-id="09411-108">使用 REST API</span><span class="sxs-lookup"><span data-stu-id="09411-108">Using the REST API</span></span>

<span data-ttu-id="09411-109">可以通过任何可发送 http/https 请求的应用程序, 从 Internet 上的任何位置访问存储 REST api, 并接收 http/https 响应。</span><span class="sxs-lookup"><span data-stu-id="09411-109">The Storage REST APIs are accessible from anywhere on the Internet, by any application that can send an HTTP/HTTPS request and receive an HTTP/HTTPS response.</span></span>

<span data-ttu-id="09411-110">例如, 如果要列出容器中的所有 blob, 您将发送类似如下所示的内容:</span><span class="sxs-lookup"><span data-stu-id="09411-110">For example, if you wanted to list all the blobs in a container, you would send something like:</span></span>

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

<span data-ttu-id="09411-111">这将返回一个 XML 块, 其中包含特定于该帐户的数据:</span><span class="sxs-lookup"><span data-stu-id="09411-111">This would return an XML block with data specific to the account:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults AccountName="https://[url-for-service-account]/">  
  <Containers>  
    <Container>  
      <Name>container1</Name>  
      <Url>https://[url-for-service-account]/container1</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 18:09:03 GMT</Last-Modified>  
        <Etag>0x8CAE7D0C4AF4487</Etag>  
      </Properties>  
      <Metadata>  
        <Color>orange</Color>  
        <ContainerNumber>01</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container2</Name>  
      <Url>https://[url-for-service-account]/container2</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8C24928</Etag>  
      </Properties>  
      <Metadata>  
        <Color>pink</Color>  
        <ContainerNumber>02</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container3</Name>  
      <Url>https://[url-for-service-account]/container3</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8EAC0BB</Etag>  
      </Properties>  
      <Metadata>  
        <Color>brown</Color>  
        <ContainerNumber>03</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
  </Containers>  
  <NextMarker>container4</NextMarker>  
</EnumerationResults>  
```

<span data-ttu-id="09411-112">但是, 这种方法需要进行大量手动分析, 并创建 HTTP 数据包来处理每个 API。</span><span class="sxs-lookup"><span data-stu-id="09411-112">However, this approach requires a lot of manual parsing and the creation of HTTP packets to work with each API.</span></span> <span data-ttu-id="09411-113">出于此原因, Azure 提供了预构建的_客户端库_, 使常见语言和框架更易于使用服务。</span><span class="sxs-lookup"><span data-stu-id="09411-113">For this reason, Azure provides pre-built _client libraries_ that make working with the service easier for common languages and frameworks.</span></span>

## <a name="using-a-client-library"></a><span data-ttu-id="09411-114">使用客户端库</span><span class="sxs-lookup"><span data-stu-id="09411-114">Using a client library</span></span>

<span data-ttu-id="09411-115">由于测试 API, 客户端库可以为应用程序开发人员节省大量的工作, 这通常会提供 REST API 发送和接收的数据模型周围的地利用包装。</span><span class="sxs-lookup"><span data-stu-id="09411-115">Client libraries can save a significant amount of work for application developers because the API is tested and it often provides nicer wrappers around the data models sent and received by the REST API.</span></span>

:::row:::  
    :::column:::  
    <span data-ttu-id="09411-116">Microsoft 具有支持多种语言和框架的 Azure 客户端库, 其中包括:</span><span class="sxs-lookup"><span data-stu-id="09411-116">Microsoft has Azure client libraries that support a number of languages and frameworks including:</span></span>
    - <span data-ttu-id="09411-117">.NET</span><span class="sxs-lookup"><span data-stu-id="09411-117">.NET</span></span>
    - <span data-ttu-id="09411-118">Java</span><span class="sxs-lookup"><span data-stu-id="09411-118">Java</span></span>
    - <span data-ttu-id="09411-119">Python</span><span class="sxs-lookup"><span data-stu-id="09411-119">Python</span></span>
    - <span data-ttu-id="09411-120">node.js</span><span class="sxs-lookup"><span data-stu-id="09411-120">Node.js</span></span>
    - <span data-ttu-id="09411-121">超越</span><span class="sxs-lookup"><span data-stu-id="09411-121">Go</span></span>
    :::column-end:::
    :::column:::
        <br> ![Sample logos of supported frameworks you can use with Azure](../media/4-common-tools.png)
    :::column-end:::  
:::row-end:::  

<span data-ttu-id="09411-122">例如, 若要检索 c # 中的 blob 列表, 我们可以使用以下代码片段:</span><span class="sxs-lookup"><span data-stu-id="09411-122">For example, to retrieve the same list of blobs in C#, we could use the following code snippet:</span></span>

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

<span data-ttu-id="09411-123">或在 JavaScript 中:</span><span class="sxs-lookup"><span data-stu-id="09411-123">Or in JavaScript:</span></span>

```javascript
const containerName = "...";
const blobService = storage.createBlobService();

blobService.listBlobsSegmented(containerName, null, function (error, results) {
    if (results) {
        for (var i = 0, blob; blob = results.entries[i]; i++) {
            // Work with blob item .. could be page blob, block blob, etc.
        }
    }
});
```

> [!NOTE]
> <span data-ttu-id="09411-124">客户端库只是 REST API 的精简_包装_。</span><span class="sxs-lookup"><span data-stu-id="09411-124">The client libraries are just thin _wrappers_ over the REST API.</span></span> <span data-ttu-id="09411-125">如果您直接使用 web 服务, 这些操作就完全是要做的。</span><span class="sxs-lookup"><span data-stu-id="09411-125">They are doing exactly what you would do if you used the web services directly.</span></span> <span data-ttu-id="09411-126">这些库也是开放源代码, 这会导致它们非常透明。</span><span class="sxs-lookup"><span data-stu-id="09411-126">These libraries are also open source, making them very transparent.</span></span> <span data-ttu-id="09411-127">在 GitHub 上查找它们。</span><span class="sxs-lookup"><span data-stu-id="09411-127">Look for them on GitHub.</span></span>

<span data-ttu-id="09411-128">让我们将客户端库支持添加到我们的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="09411-128">Let's add client library support to our application.</span></span>
