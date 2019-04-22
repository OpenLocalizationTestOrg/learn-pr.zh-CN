::: zone pivot="csharp"
<span data-ttu-id="f9320-101">让我们添加代码来从配置文件中检索连接字符串, 并使用它连接到 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="f9320-101">Let's add code to retrieve the connection string from the configuration file and use it to connect to the Azure storage account.</span></span>

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="f9320-102">检索连接字符串</span><span class="sxs-lookup"><span data-stu-id="f9320-102">Retrieve the connection string</span></span>

1. <span data-ttu-id="f9320-103">在代码编辑器中打开**Program.cs** 。</span><span class="sxs-lookup"><span data-stu-id="f9320-103">Open **Program.cs** in the code editor.</span></span>

1. <span data-ttu-id="f9320-104">在文件`using`顶部添加一个语句以引用`Microsoft.WindowsAzure.Storage`命名空间:</span><span class="sxs-lookup"><span data-stu-id="f9320-104">Add a `using` statement at the top of the file to reference the `Microsoft.WindowsAzure.Storage` namespace:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. <span data-ttu-id="f9320-105">在该`Main`方法的末尾, 添加以下行以从配置文件中检索 Azure 存储帐户连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f9320-105">At the end of the `Main` method, add the following line to retrieve the Azure storage account connection string from the configuration file.</span></span> <span data-ttu-id="f9320-106">传递的_密钥_必须与**appsettings**文件中使用的名称相匹配。</span><span class="sxs-lookup"><span data-stu-id="f9320-106">The passed _key_ must match the name used in your **appsettings.json** file.</span></span>

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a><span data-ttu-id="f9320-107">创建 blob 客户端</span><span class="sxs-lookup"><span data-stu-id="f9320-107">Create a blob client</span></span>

1. <span data-ttu-id="f9320-108">使用静态`CloudStorageAccount.TryParse`方法创建`CloudStorageAccount`对象-它采用连接字符串和`out`参数以返回创建的对象。</span><span class="sxs-lookup"><span data-stu-id="f9320-108">Use the static `CloudStorageAccount.TryParse` method to create a `CloudStorageAccount` object - it takes the connection string and an `out` parameter to return the created object.</span></span> <span data-ttu-id="f9320-109">它返回一个`bool`值, 指示它是否成功分析了字符串。</span><span class="sxs-lookup"><span data-stu-id="f9320-109">It returns a `bool` value indicating whether it successfully parsed the string.</span></span>
    - <span data-ttu-id="f9320-110">如果失败, 则将消息输出到控制台, 并从方法返回。</span><span class="sxs-lookup"><span data-stu-id="f9320-110">If it fails, output a message to the console and return from the method.</span></span>

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString,
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. <span data-ttu-id="f9320-111">使用返回`CloudStorageAccount`的对象创建 blob 客户端。</span><span class="sxs-lookup"><span data-stu-id="f9320-111">Use the returned `CloudStorageAccount` object to create a blob client.</span></span>

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="f9320-112">接下来, 使用 blob 客户端检索对名为 "photoblobs" 的容器的引用。</span><span class="sxs-lookup"><span data-stu-id="f9320-112">Next, use the blob client to retrieve a reference to a container named "photoblobs."</span></span> <span data-ttu-id="f9320-113">与帐户名称非常相似, Blob 容器名称必须是小写的, 并且由字母和数字组成。</span><span class="sxs-lookup"><span data-stu-id="f9320-113">Much like the account names, the Blob container names must be lowercase and composed of letters and numbers.</span></span>

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. <span data-ttu-id="f9320-114">使用`CreateIfNotExistsAsync`方法创建容器。</span><span class="sxs-lookup"><span data-stu-id="f9320-114">Use the `CreateIfNotExistsAsync` method to create the container.</span></span> <span data-ttu-id="f9320-115">这将返回`bool`一个值, 指示是否创建容器。</span><span class="sxs-lookup"><span data-stu-id="f9320-115">This returns a `bool` indicating whether the container was created.</span></span> <span data-ttu-id="f9320-116">将其存储在名为`created`的变量中。</span><span class="sxs-lookup"><span data-stu-id="f9320-116">Store this in a variable named `created`.</span></span>
    - <span data-ttu-id="f9320-117">请注意, 这是一个**async**方法, 这意味着它将执行实际的网络调用。</span><span class="sxs-lookup"><span data-stu-id="f9320-117">Notice that this is an **async** method - that means it will perform an actual network call.</span></span>
    - <span data-ttu-id="f9320-118">你将需要使用`await`关键字来获取`bool`结果。</span><span class="sxs-lookup"><span data-stu-id="f9320-118">You will need to use the `await` keywords to get the `bool` result.</span></span>

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. <span data-ttu-id="f9320-119">由于我们`await`使用的是关键字, 因此请继续并将`Main`方法的签名更改为`async` , 并返回。 `Task`</span><span class="sxs-lookup"><span data-stu-id="f9320-119">Because we are using the `await` keyword, go ahead and change the signature for the `Main` method to be `async` and return a `Task`.</span></span>

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

    <span data-ttu-id="f9320-120">您还需要在顶部添加一个新`using`语句:</span><span class="sxs-lookup"><span data-stu-id="f9320-120">You'll also need to add a new `using` statement at the top:</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="f9320-121">最后, 输出是否已创建 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="f9320-121">Finally, output whether we created the Blob container.</span></span>

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. <span data-ttu-id="f9320-122">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="f9320-122">Save the file.</span></span>

<span data-ttu-id="f9320-123">如果你想要检查你的工作, 最终文件应如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9320-123">The final file should look like this if you'd like to check your work.</span></span>

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

## <a name="use-c-71-to-build-our-app"></a><span data-ttu-id="f9320-124">使用 c # 7.1 生成我们的应用程序</span><span class="sxs-lookup"><span data-stu-id="f9320-124">Use C# 7.1 to build our app</span></span>

<span data-ttu-id="f9320-125">向 c `async` # `await` 7.1 `Main`中添加了对和 on 方法的支持。</span><span class="sxs-lookup"><span data-stu-id="f9320-125">Support for `async` and `await` on `Main` methods was added to C# 7.1.</span></span> <span data-ttu-id="f9320-126">这可能不是您正在使用的编译器的默认版本。</span><span class="sxs-lookup"><span data-stu-id="f9320-126">This might not be the default version of the compiler you are using.</span></span> <span data-ttu-id="f9320-127">让我们通过在配置文件中设置来确保我们使用该版本的编译器。</span><span class="sxs-lookup"><span data-stu-id="f9320-127">Let's make sure we use that version of the compiler by setting it in our configuration file.</span></span>

1. <span data-ttu-id="f9320-128">打开, `PhotoSharingApp.csproj`并将`<LangVersion>7.1</LangVersion>`添加到`PropertyGroup`指定的`TargetFramework`。</span><span class="sxs-lookup"><span data-stu-id="f9320-128">Open the `PhotoSharingApp.csproj` and add `<LangVersion>7.1</LangVersion>` to the `PropertyGroup` that specifies the `TargetFramework`.</span></span> <span data-ttu-id="f9320-129">完成后, 它应如下所示:</span><span class="sxs-lookup"><span data-stu-id="f9320-129">It should look like this when you're finished:</span></span>

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

1. <span data-ttu-id="f9320-130">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="f9320-130">Save the file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="f9320-131">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="f9320-131">Run the app</span></span>

1. <span data-ttu-id="f9320-132">生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="f9320-132">Build and run the application.</span></span> <span data-ttu-id="f9320-133">**注意:** 请确保你处于正确的工作目录中。</span><span class="sxs-lookup"><span data-stu-id="f9320-133">**Note:** make sure you're in the correct working directory.</span></span>

    ```bash
    dotnet run
    ```

::: zone-end

::: zone pivot="javascript"
<span data-ttu-id="f9320-134">让我们添加代码以使用存储连接字符串连接到 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="f9320-134">Let's add code to connect to the Azure storage account using our stored connection string.</span></span> <span data-ttu-id="f9320-135">Azure 客户端库将自动使用**AZURE_STORAGE_CONNECTION_STRING**环境变量获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f9320-135">The Azure client library will automatically use the **AZURE_STORAGE_CONNECTION_STRING** environment variable to get the connection string.</span></span>

## <a name="create-a-blob-client"></a><span data-ttu-id="f9320-136">创建 blob 客户端</span><span class="sxs-lookup"><span data-stu-id="f9320-136">Create a blob client</span></span>

1. <span data-ttu-id="f9320-137">在代码编辑器中打开**index .js** 。</span><span class="sxs-lookup"><span data-stu-id="f9320-137">Open **index.js** in the code editor.</span></span>

1. <span data-ttu-id="f9320-138">首先, 将**azure 存储**模块包括在内。</span><span class="sxs-lookup"><span data-stu-id="f9320-138">Start by including the **azure-storage** module.</span></span> <span data-ttu-id="f9320-139">将模块存储在名为 "**存储**" 的变量中。</span><span class="sxs-lookup"><span data-stu-id="f9320-139">Store the module in a variable named **storage**.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    const storage = require('azure-storage');
    ```

1. <span data-ttu-id="f9320-140">接下来, 在后面, 使用**存储**对象创建`BlobService`对象并将其存储在全局命名的**blobService**中。</span><span class="sxs-lookup"><span data-stu-id="f9320-140">Next, right after that, use the **storage** object to create the `BlobService` object and store it in a global named **blobService**.</span></span> <span data-ttu-id="f9320-141">请记住, 这些是表示对存储帐户的访问权限的轻型对象。</span><span class="sxs-lookup"><span data-stu-id="f9320-141">Remember, these are lightweight objects representing access to the storage account.</span></span>

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. <span data-ttu-id="f9320-142">添加一个常量来表示要创建的容器。</span><span class="sxs-lookup"><span data-stu-id="f9320-142">Add a constant to represent the container we want to create.</span></span> <span data-ttu-id="f9320-143">我们将把容器命名为 "photoblobs"。</span><span class="sxs-lookup"><span data-stu-id="f9320-143">We'll name the container "photoblobs".</span></span>

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a><span data-ttu-id="f9320-144">创建容器</span><span class="sxs-lookup"><span data-stu-id="f9320-144">Create a container</span></span>

<span data-ttu-id="f9320-145">我们可以使用该`BlobService`对象来处理 Azure 存储中的 blob api。</span><span class="sxs-lookup"><span data-stu-id="f9320-145">We can use the `BlobService` object to work with blob APIs in Azure storage.</span></span> <span data-ttu-id="f9320-146">如前所述, 进行网络调用的所有 api 都是异步的, 以保持应用程序的响应性。</span><span class="sxs-lookup"><span data-stu-id="f9320-146">As mentioned before, all the APIs that make network calls are asynchronous to keep the app responsive.</span></span> <span data-ttu-id="f9320-147">此`createContainerIfNotExists`方法是一种方法。</span><span class="sxs-lookup"><span data-stu-id="f9320-147">The `createContainerIfNotExists` method is one such method.</span></span> <span data-ttu-id="f9320-148">我们将使用_承诺_来处理包含响应的回调。</span><span class="sxs-lookup"><span data-stu-id="f9320-148">We'll use _promises_ to handle the callback that contains the response.</span></span>

1. <span data-ttu-id="f9320-149">在文件`util`顶部添加一个常量 (添加最初`require`之后), 以加载`util`该包。</span><span class="sxs-lookup"><span data-stu-id="f9320-149">Add a `util` constant at the top of the file (after the initial `require` you added) to load the `util` package.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const util = require('util');
    const storage = require('azure-storage');
    const blobService = storage.createBlobService();
    const containerName = 'photoblobs';
    ```
    
1. <span data-ttu-id="f9320-150">接下来, 在所有常量之后, `util.promisify`使用获取回调版本`createContainerIfNotExists`并将其转换为承诺返回的方法。</span><span class="sxs-lookup"><span data-stu-id="f9320-150">Next, after all the constants, use `util.promisify` to take the callback version of `createContainerIfNotExists` and turn it into a promise-returning method.</span></span>
    - <span data-ttu-id="f9320-151">由于回调方法位于某个对象上, 因此请确保在末尾添加`bind`一个调用, 以将其连接到该上下文。</span><span class="sxs-lookup"><span data-stu-id="f9320-151">Since the callback method is on an object, make sure to add a `bind` call at the end to connect it to that context.</span></span>
    - <span data-ttu-id="f9320-152">在名为`createContainerAsync`的文件的顶部, 将返回值分配给一个常量, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9320-152">Assign the return value to a constant at the top of the file named `createContainerAsync`, as shown below.</span></span>
    - <span data-ttu-id="f9320-153">此外, 还需要在`require`靠近文件`util`顶部的模块中输入。</span><span class="sxs-lookup"><span data-stu-id="f9320-153">You'll also need a `require` for the `util` module near the top of the file.</span></span>

    ```javascript
    const util = require('util');
    const storage = require('azure-storage');
    const blobService = storage.createBlobService();
    const containerName = 'photoblobs';

    const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);
    ```

2. <span data-ttu-id="f9320-154">删除 "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="f9320-154">Remove the "Hello, World!"</span></span> <span data-ttu-id="f9320-155">输出`main()`。</span><span class="sxs-lookup"><span data-stu-id="f9320-155">output from `main()`.</span></span>

3. <span data-ttu-id="f9320-156">致电你的`createContainerAsync`新承诺。</span><span class="sxs-lookup"><span data-stu-id="f9320-156">Call your new `createContainerAsync` promise.</span></span>
    - <span data-ttu-id="f9320-157">将**容器**的常量传递给它。</span><span class="sxs-lookup"><span data-stu-id="f9320-157">Pass it the **containerName** constant.</span></span>
    - <span data-ttu-id="f9320-158">将`await`关键字应用于该调用。</span><span class="sxs-lookup"><span data-stu-id="f9320-158">Apply the `await` keyword to the call.</span></span>
    - <span data-ttu-id="f9320-159">`try`  / 在`catch`构造中包装该调用, 并输出任何错误。</span><span class="sxs-lookup"><span data-stu-id="f9320-159">Wrap the call in a `try` / `catch` construct and output any error.</span></span>

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. <span data-ttu-id="f9320-160">`createContainerAsync`承诺返回基础`createContainerIfNotExists`中的第一个值, 即容器结果。</span><span class="sxs-lookup"><span data-stu-id="f9320-160">The `createContainerAsync` promise returns the first value from the underlying `createContainerIfNotExists`, which is the container result.</span></span> <span data-ttu-id="f9320-161">其中包括有关是否创建容器的信息。</span><span class="sxs-lookup"><span data-stu-id="f9320-161">This includes information on whether the container was created or not.</span></span> <span data-ttu-id="f9320-162">将结果捕获到一个变量中, 并输出容器是否是基于该`result.created`属性创建的。</span><span class="sxs-lookup"><span data-stu-id="f9320-162">Capture the result in a variable, and output whether the container was created based on the `result.created` property.</span></span>

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

1. <span data-ttu-id="f9320-163">最后, 使用`async`关键字`main`修饰函数。</span><span class="sxs-lookup"><span data-stu-id="f9320-163">Finally, decorate the `main` function with the `async` keyword.</span></span>

1. <span data-ttu-id="f9320-164">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="f9320-164">Save the file.</span></span>

<span data-ttu-id="f9320-165">如果你想要检查你的工作, 最终文件应如下所示。</span><span class="sxs-lookup"><span data-stu-id="f9320-165">The final file should look like this, if you'd like to check your work.</span></span>

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

## <a name="run-the-app"></a><span data-ttu-id="f9320-166">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="f9320-166">Run the app</span></span>

1. <span data-ttu-id="f9320-167">生成并运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="f9320-167">Build and run the application.</span></span> <span data-ttu-id="f9320-168">**注意:** 请确保你在 PhotoSharingApp 目录中。</span><span class="sxs-lookup"><span data-stu-id="f9320-168">**Note:** make sure you're in the PhotoSharingApp directory.</span></span>

    ```bash
    node index.js
    ```

    > [!TIP]
    > <span data-ttu-id="f9320-169">如果遇到有关使用`await`关键字的错误, 请确保已按照上述说明的最后步骤将`async`关键字添加到`main`函数定义。</span><span class="sxs-lookup"><span data-stu-id="f9320-169">If you get an error about the use of the `await` keyword, make sure you have added the `async` keyword to the `main` function definition per the final step in the instructions above.</span></span>

::: zone-end

<span data-ttu-id="f9320-170">它应报告已创建 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="f9320-170">It should report that the blob container was created.</span></span> <span data-ttu-id="f9320-171">如果您再次运行它, 它应告诉您它已存在。</span><span class="sxs-lookup"><span data-stu-id="f9320-171">If you run it a second time, it should tell you it already exists.</span></span>

<span data-ttu-id="f9320-172">验证容器:</span><span class="sxs-lookup"><span data-stu-id="f9320-172">To verify the container:</span></span>

1. <span data-ttu-id="f9320-173">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="f9320-173">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="f9320-174">导航到您的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="f9320-174">Navigate to your storage account.</span></span> <span data-ttu-id="f9320-175">您可以使用 "**所有资源**" 部分查找存储帐户或从位于门户窗口顶部的_搜索框_按名称进行搜索。</span><span class="sxs-lookup"><span data-stu-id="f9320-175">You can use the **All Resources** section to find the storage account or search by name from the _search box_ at the top of the portal window.</span></span>

1. <span data-ttu-id="f9320-176">在 " **blob 服务**" 部分中选择存储帐户的**blob**项。</span><span class="sxs-lookup"><span data-stu-id="f9320-176">Select the **Blobs** entry of the storage account in the **Blob services** section.</span></span>

1. <span data-ttu-id="f9320-177">您应该会在 "blob" 面板中看到您的**photoblobs**容器。</span><span class="sxs-lookup"><span data-stu-id="f9320-177">You should see your **photoblobs** container in the Blobs panel.</span></span> <span data-ttu-id="f9320-178">您可以通过 "..." 删除容器。菜单, 以尝试使用您的应用程序重新创建该条目。</span><span class="sxs-lookup"><span data-stu-id="f9320-178">You can delete the container through the "..." menu on the right-hand side of the entry to try recreating it with your app.</span></span>

> [!NOTE]
> <span data-ttu-id="f9320-179">容器将很快从门户中消失, 但需要几分钟的时间才能删除。</span><span class="sxs-lookup"><span data-stu-id="f9320-179">The container will disappear from the portal very quickly, but it takes a few minutes to delete.</span></span> <span data-ttu-id="f9320-180">如果您尝试在完全取消预配之前重新创建它, 则会出现错误。</span><span class="sxs-lookup"><span data-stu-id="f9320-180">If you attempt to recreate it before it's been completely de-provisioned, you will get an error.</span></span>

## <a name="delete-the-app"></a><span data-ttu-id="f9320-181">删除应用程序</span><span class="sxs-lookup"><span data-stu-id="f9320-181">Delete the app</span></span>
<span data-ttu-id="f9320-182">如果您决定不在云命令行管理器环境中保留应用程序源代码, 则可以使用以下命令删除该文件夹和所有内容。</span><span class="sxs-lookup"><span data-stu-id="f9320-182">If you decide you don't want to keep the application source code in your Cloud Shell environment, you can use the following command to remove the folder and all the contents.</span></span>

```bash
rm -r PhotoSharingApp/
```
