::: zone pivot="csharp"
让我们添加代码来从配置文件中检索连接字符串, 并使用它连接到 Azure 存储帐户。

## <a name="retrieve-the-connection-string"></a>检索连接字符串

1. 在代码编辑器中打开**Program.cs** 。

1. 在文件`using`顶部添加一个语句以引用`Microsoft.WindowsAzure.Storage`命名空间:

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. 在该`Main`方法的末尾, 添加以下行以从配置文件中检索 Azure 存储帐户连接字符串。 传递的_密钥_必须与**appsettings**文件中使用的名称相匹配。

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>创建 blob 客户端

1. 使用静态`CloudStorageAccount.TryParse`方法创建`CloudStorageAccount`对象-它采用连接字符串和`out`参数以返回创建的对象。 它返回一个`bool`值, 指示它是否成功分析了字符串。
    - 如果失败, 则将消息输出到控制台, 并从方法返回。

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString,
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. 使用返回`CloudStorageAccount`的对象创建 blob 客户端。

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 接下来, 使用 blob 客户端检索对名为 "photoblobs" 的容器的引用。 与帐户名称非常相似, Blob 容器名称必须是小写的, 并且由字母和数字组成。

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. 使用`CreateIfNotExistsAsync`方法创建容器。 这将返回`bool`一个值, 指示是否创建容器。 将其存储在名为`created`的变量中。
    - 请注意, 这是一个**async**方法, 这意味着它将执行实际的网络调用。
    - 你将需要使用`await`关键字来获取`bool`结果。

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. 由于我们`await`使用的是关键字, 因此请继续并将`Main`方法的签名更改为`async` , 并返回。 `Task`

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

    您还需要在顶部添加一个新`using`语句:

    ```csharp
    using System.Threading.Tasks;
    ```

1. 最后, 输出是否已创建 Blob 容器。

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. 保存该文件。

如果你想要检查你的工作, 最终文件应如下所示。

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using Microsoft.WindowsAzure.Storage;
using System.Threading.Tasks;

namespace PhotoSharingApp
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
            var connectionString = configuration["StorageAccountConnectionString"];

            if (!CloudStorageAccount.TryParse(connectionString, out CloudStorageAccount storageAccount))
            {
                Console.WriteLine("Unable to parse connection string");
                return;
            }

            var blobClient = storageAccount.CreateCloudBlobClient();
            var blobContainer = blobClient.GetContainerReference("photoblobs");
            bool created = await blobContainer.CreateIfNotExistsAsync();

            Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
        }
    }
}
```

## <a name="use-c-71-to-build-our-app"></a>使用 c # 7.1 生成我们的应用程序

向 c `async` # `await` 7.1 `Main`中添加了对和 on 方法的支持。 这可能不是您正在使用的编译器的默认版本。 让我们通过在配置文件中设置来确保我们使用该版本的编译器。

1. 打开, `PhotoSharingApp.csproj`并将`<LangVersion>7.1</LangVersion>`添加到`PropertyGroup`指定的`TargetFramework`。 完成后, 它应如下所示:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <LangVersion>7.1</LangVersion>
        <TargetFramework>netcoreapp2.0</TargetFramework>
      </PropertyGroup>
      ...
    </Project>
    ```

1. 保存该文件。

## <a name="run-the-app"></a>运行应用程序

1. 生成并运行应用程序。 **注意:** 请确保你处于正确的工作目录中。

    ```bash
    dotnet run
    ```

::: zone-end

::: zone pivot="javascript"
让我们添加代码以使用存储连接字符串连接到 Azure 存储帐户。 Azure 客户端库将自动使用**AZURE_STORAGE_CONNECTION_STRING**环境变量获取连接字符串。

## <a name="create-a-blob-client"></a>创建 blob 客户端

1. 在代码编辑器中打开**index .js** 。

1. 首先, 将**azure 存储**模块包括在内。 将模块存储在名为 "**存储**" 的变量中。

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    const storage = require('azure-storage');
    ```

1. 接下来, 在后面, 使用**存储**对象创建`BlobService`对象并将其存储在全局命名的**blobService**中。 请记住, 这些是表示对存储帐户的访问权限的轻型对象。

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. 添加一个常量来表示要创建的容器。 我们将把容器命名为 "photoblobs"。

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a>创建容器

我们可以使用该`BlobService`对象来处理 Azure 存储中的 blob api。 如前所述, 进行网络调用的所有 api 都是异步的, 以保持应用程序的响应性。 此`createContainerIfNotExists`方法是一种方法。 我们将使用_承诺_来处理包含响应的回调。

1. 在文件`util`顶部添加一个常量 (添加最初`require`之后), 以加载`util`该包。

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const util = require('util');
    const storage = require('azure-storage');
    const blobService = storage.createBlobService();
    const containerName = 'photoblobs';
    ```
    
1. 接下来, 在所有常量之后, `util.promisify`使用获取回调版本`createContainerIfNotExists`并将其转换为承诺返回的方法。
    - 由于回调方法位于某个对象上, 因此请确保在末尾添加`bind`一个调用, 以将其连接到该上下文。
    - 在名为`createContainerAsync`的文件的顶部, 将返回值分配给一个常量, 如下所示。
    - 此外, 还需要在`require`靠近文件`util`顶部的模块中输入。

    ```javascript
    const util = require('util');
    const storage = require('azure-storage');
    const blobService = storage.createBlobService();
    const containerName = 'photoblobs';

    const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);
    ```

2. 删除 "Hello, World!" 输出`main()`。

3. 致电你的`createContainerAsync`新承诺。
    - 将**容器**的常量传递给它。
    - 将`await`关键字应用于该调用。
    - `try`  / 在`catch`构造中包装该调用, 并输出任何错误。

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. `createContainerAsync`承诺返回基础`createContainerIfNotExists`中的第一个值, 即容器结果。 其中包括有关是否创建容器的信息。 将结果捕获到一个变量中, 并输出容器是否是基于该`result.created`属性创建的。

    ```javascript
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. 最后, 使用`async`关键字`main`修饰函数。

1. 保存该文件。

如果你想要检查你的工作, 最终文件应如下所示。

```javascript
#!/usr/bin/env node

require('dotenv').load();

const util = require('util');

const storage = require('azure-storage');
const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';

async function main() {
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

main();
```

## <a name="run-the-app"></a>运行应用程序

1. 生成并运行应用程序。 **注意:** 请确保你在 PhotoSharingApp 目录中。

    ```bash
    node index.js
    ```

    > [!TIP]
    > 如果遇到有关使用`await`关键字的错误, 请确保已按照上述说明的最后步骤将`async`关键字添加到`main`函数定义。

::: zone-end

它应报告已创建 blob 容器。 如果您再次运行它, 它应告诉您它已存在。

验证容器:

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 导航到您的存储帐户。 您可以使用 "**所有资源**" 部分查找存储帐户或从位于门户窗口顶部的_搜索框_按名称进行搜索。

1. 在 " **blob 服务**" 部分中选择存储帐户的**blob**项。

1. 您应该会在 "blob" 面板中看到您的**photoblobs**容器。 您可以通过 "..." 删除容器。菜单, 以尝试使用您的应用程序重新创建该条目。

> [!NOTE]
> 容器将很快从门户中消失, 但需要几分钟的时间才能删除。 如果您尝试在完全取消预配之前重新创建它, 则会出现错误。

## <a name="delete-the-app"></a>删除应用程序
如果您决定不在云命令行管理器环境中保留应用程序源代码, 则可以使用以下命令删除该文件夹和所有内容。

```bash
rm -r PhotoSharingApp/
```
