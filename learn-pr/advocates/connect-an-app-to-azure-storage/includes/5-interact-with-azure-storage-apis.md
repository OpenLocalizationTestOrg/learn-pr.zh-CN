Azure 存储提供 REST API 以使用存储在每个帐户中的容器和数据。 有一些独立的 api 可用于处理可存储的每种数据类型。 请记住, 我们有四种特定的数据类型:

- 非结构化数据 (如二进制文件和文本文件) 的**blob** 。
- 持久邮件传递的**队列**。
- 键/值的结构化存储**表**。
- 用于传统 SMB 文件共享的**文件**。

## <a name="using-the-rest-api"></a>使用 REST API

可以通过任何可发送 http/https 请求的应用程序, 从 Internet 上的任何位置访问存储 REST api, 并接收 http/https 响应。

例如, 如果要列出容器中的所有 blob, 您将发送类似如下所示的内容:

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

这将返回一个 XML 块, 其中包含特定于该帐户的数据:

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

但是, 这种方法需要进行大量手动分析, 并创建 HTTP 数据包来处理每个 API。 出于此原因, Azure 提供了预构建的_客户端库_, 使常见语言和框架更易于使用服务。

## <a name="using-a-client-library"></a>使用客户端库

由于测试 API, 客户端库可以为应用程序开发人员节省大量的工作, 这通常会提供 REST API 发送和接收的数据模型周围的地利用包装。

:::row:::  
    :::column:::  
    Microsoft 具有支持多种语言和框架的 Azure 客户端库, 其中包括:
    - .NET
    - Java
    - Python
    - node.js
    - 超越
    :::column-end:::
    :::column:::
        <br> ![Sample logos of supported frameworks you can use with Azure](../media/4-common-tools.png)
    :::column-end:::  
:::row-end:::  

例如, 若要检索 c # 中的 blob 列表, 我们可以使用以下代码片段:

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

或在 JavaScript 中:

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
> 客户端库只是 REST API 的精简_包装_。 如果您直接使用 web 服务, 这些操作就完全是要做的。 这些库也是开放源代码, 这会导致它们非常透明。 在 GitHub 上查找它们。

让我们将客户端库支持添加到我们的应用程序中。
