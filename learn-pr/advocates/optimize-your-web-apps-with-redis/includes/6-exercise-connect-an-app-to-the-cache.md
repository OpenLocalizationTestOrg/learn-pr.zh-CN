<span data-ttu-id="39f63-101">至此, 我们已在 Azure 中创建了 Redis 缓存, 让我们创建一个应用程序来使用它。</span><span class="sxs-lookup"><span data-stu-id="39f63-101">Now that we have a Redis cache created in Azure, let's create an application to use it.</span></span> <span data-ttu-id="39f63-102">请确保您的连接字符串信息来自 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="39f63-102">Make sure you have your connection string information from the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="39f63-103">可在右侧找到集成云命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="39f63-103">The integrated Cloud Shell is available on the right.</span></span> <span data-ttu-id="39f63-104">您可以使用该命令提示符创建并运行我们在此处构建的示例代码, 如果您有 .net Core 开发环境安装程序, 则可以在本地执行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="39f63-104">You can use that command prompt to create and run the example code we are building here, or perform these steps locally if you have a .NET Core development environment setup.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="39f63-105">创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="39f63-105">Create a Console Application</span></span>

<span data-ttu-id="39f63-106">我们将使用一个简单的控制台应用程序, 以便我们能够将重点放在 Redis 实现上。</span><span class="sxs-lookup"><span data-stu-id="39f63-106">We'll use a simple Console Application so we can focus on the Redis implementation.</span></span>

1. <span data-ttu-id="39f63-107">在云命令行管理程序中, 创建一个新的 .net Core 控制台应用程序, 将其命名为 "SportsStatsTracker"</span><span class="sxs-lookup"><span data-stu-id="39f63-107">In the Cloud Shell, create a new .NET Core Console Application, name it "SportsStatsTracker"</span></span>

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. <span data-ttu-id="39f63-108">这将为项目创建一个文件夹, 继续并更改当前目录。</span><span class="sxs-lookup"><span data-stu-id="39f63-108">This will create a folder for the project, go ahead and change the current directory.</span></span>

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a><span data-ttu-id="39f63-109">添加连接字符串</span><span class="sxs-lookup"><span data-stu-id="39f63-109">Add the connection string</span></span>

<span data-ttu-id="39f63-110">让我们将从 Azure 门户获取的连接字符串添加到代码中。</span><span class="sxs-lookup"><span data-stu-id="39f63-110">Let's add the connection string we got from the Azure portal into the code.</span></span> <span data-ttu-id="39f63-111">请勿在源代码中将此类凭据存储为此代码。</span><span class="sxs-lookup"><span data-stu-id="39f63-111">Never store credentials like this in your source code.</span></span> <span data-ttu-id="39f63-112">若要使此示例简单, 我们要使用配置文件。</span><span class="sxs-lookup"><span data-stu-id="39f63-112">To keep this sample simple, we're going to use a configuration file.</span></span> <span data-ttu-id="39f63-113">对于 azure 中的服务器端应用程序, 更好的方法是使用 Azure Key Vault 和证书。</span><span class="sxs-lookup"><span data-stu-id="39f63-113">A better approach for a server-side application in Azure would be to use Azure Key Vault with certificates.</span></span>

1. <span data-ttu-id="39f63-114">创建要添加到项目中的新的**appsettings**文件。</span><span class="sxs-lookup"><span data-stu-id="39f63-114">Create a new **appsettings.json** file to add to the project.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="39f63-115">在项目文件夹中键入`code .`以打开代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="39f63-115">Open the code editor by typing `code .` in the project folder.</span></span> <span data-ttu-id="39f63-116">如果您在本地工作, 建议使用**Visual Studio Code**。</span><span class="sxs-lookup"><span data-stu-id="39f63-116">If you are working locally, we recommend using **Visual Studio Code**.</span></span> <span data-ttu-id="39f63-117">此处的步骤将主要与其使用一致。</span><span class="sxs-lookup"><span data-stu-id="39f63-117">The steps here will mostly align with it's usage.</span></span>

1. <span data-ttu-id="39f63-118">在编辑器中选择 " **appsettings** " 文件, 并添加以下文本。</span><span class="sxs-lookup"><span data-stu-id="39f63-118">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="39f63-119">将连接字符串粘贴到设置的**值**中。</span><span class="sxs-lookup"><span data-stu-id="39f63-119">Paste your connection string into the **value** of the setting.</span></span>

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. <span data-ttu-id="39f63-120">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="39f63-120">Save the changes.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="39f63-121">只要您将代码粘贴或更改为编辑器中的文件, 就一定要使用 "..." 进行保存。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="39f63-121">Whenever you paste or change code into a file in the editor, make sure to save afterwards using the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="39f63-122">单击编辑器中的 " **SportsStatsTracker** " 文件将其打开。</span><span class="sxs-lookup"><span data-stu-id="39f63-122">Click on the **SportsStatsTracker.csproj** file in the editor to open it.</span></span>

1. <span data-ttu-id="39f63-123">将以下`<ItemGroup>`配置块添加到根`<Project>`元素中, 以将新文件包含在项目中, 并将其复制到输出文件夹。</span><span class="sxs-lookup"><span data-stu-id="39f63-123">Add the following `<ItemGroup>` configuration block into the root `<Project>` element to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="39f63-124">这样可确保在编译/生成应用程序时, 将应用程序配置文件放在输出目录中。</span><span class="sxs-lookup"><span data-stu-id="39f63-124">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. <span data-ttu-id="39f63-125">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="39f63-125">Save the file.</span></span> <span data-ttu-id="39f63-126">(请务必执行此操作, 否则在下面添加包时, 会丢失所做的更改!)</span><span class="sxs-lookup"><span data-stu-id="39f63-126">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="39f63-127">添加对读取 JSON 配置文件的支持</span><span class="sxs-lookup"><span data-stu-id="39f63-127">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="39f63-128">.net Core 应用程序需要其他 NuGet 包才能读取 JSON 配置文件。</span><span class="sxs-lookup"><span data-stu-id="39f63-128">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="39f63-129">在窗口的命令提示符部分, 添加对**Microsoft extension. Json** NuGet 包的引用。</span><span class="sxs-lookup"><span data-stu-id="39f63-129">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="39f63-130">添加代码以读取配置文件</span><span class="sxs-lookup"><span data-stu-id="39f63-130">Add code to read the configuration file</span></span>

<span data-ttu-id="39f63-131">至此, 我们已经添加了启用读取配置所需的库, 我们需要在控制台应用程序中启用该功能。</span><span class="sxs-lookup"><span data-stu-id="39f63-131">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="39f63-132">在编辑器中选择 " **Program.cs** "。</span><span class="sxs-lookup"><span data-stu-id="39f63-132">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="39f63-133">在文件的顶部, 存在`using System`一行。</span><span class="sxs-lookup"><span data-stu-id="39f63-133">At the top of the file, a `using System` line is present.</span></span> <span data-ttu-id="39f63-134">在该行下方, 添加以下代码行:</span><span class="sxs-lookup"><span data-stu-id="39f63-134">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="39f63-135">将**Main**方法的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="39f63-135">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="39f63-136">此代码会将配置系统初始化为从**appsettings**文件中读取。</span><span class="sxs-lookup"><span data-stu-id="39f63-136">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json")
        .Build();
    ```

<span data-ttu-id="39f63-137">您的**Program.cs**文件现在应如下所示:</span><span class="sxs-lookup"><span data-stu-id="39f63-137">Your **Program.cs** file should now look like the following:</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace SportsStatsTracker
{
    class Program
    {
        static void Main(string[] args)
        {
            var config = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json")
                .Build();
        }
    }
}
```

## <a name="get-the-connection-string-from-configuration"></a><span data-ttu-id="39f63-138">从配置中获取连接字符串</span><span class="sxs-lookup"><span data-stu-id="39f63-138">Get the connection string from configuration</span></span>

1. <span data-ttu-id="39f63-139">在**Program.cs**中, 在**Main**方法的末尾, 使用新的**配置**变量检索连接字符串, 并将其存储在名为**connectionString**的新变量中。</span><span class="sxs-lookup"><span data-stu-id="39f63-139">In **Program.cs**, at the end of the **Main** method, use the new **config** variable to retrieve the connection string and store it in a new variable named **connectionString**.</span></span>
    - <span data-ttu-id="39f63-140">**config**变量包含一个索引器, 您可以在其中传递字符串以从**appSettings**文件中检索。</span><span class="sxs-lookup"><span data-stu-id="39f63-140">The **config** variable has an indexer where you can pass in a string to retrieve from your **appSettings.json** file.</span></span>

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a><span data-ttu-id="39f63-141">添加对 Redis 缓存 .net 客户端的支持</span><span class="sxs-lookup"><span data-stu-id="39f63-141">Add support for the Redis cache .NET client</span></span>

<span data-ttu-id="39f63-142">接下来, 让我们将控制台应用程序配置为使用 .net 的**StackExchange Redis**客户端。</span><span class="sxs-lookup"><span data-stu-id="39f63-142">Next, let's configure the console application to use the **StackExchange.Redis** client for .NET.</span></span>

1. <span data-ttu-id="39f63-143">使用云命令行管理程序编辑器底部的命令提示符将**StackExchange** NuGet 包添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="39f63-143">Add the **StackExchange.Redis** NuGet package to the project using the command prompt at the bottom of the Cloud Shell editor.</span></span>

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. <span data-ttu-id="39f63-144">在编辑器中选择 " **Program.cs** ", `using`并为命名空间 StackExchange 添加一个 **。 Redis**</span><span class="sxs-lookup"><span data-stu-id="39f63-144">Select **Program.cs** in the editor and add a `using` for the namespace **StackExchange.Redis**</span></span>

    ```csharp
    using StackExchange.Redis;
    ```
    
<span data-ttu-id="39f63-145">安装完成后, Redis 缓存客户端即可用于您的项目。</span><span class="sxs-lookup"><span data-stu-id="39f63-145">Once the installation is completed, the Redis cache client is available to use with your project.</span></span>

## <a name="connect-to-the-cache"></a><span data-ttu-id="39f63-146">连接到缓存</span><span class="sxs-lookup"><span data-stu-id="39f63-146">Connect to the cache</span></span>

<span data-ttu-id="39f63-147">让我们添加代码以连接到缓存。</span><span class="sxs-lookup"><span data-stu-id="39f63-147">Let's add the code to connect to the cache.</span></span>

1. <span data-ttu-id="39f63-148">在编辑器中选择 " **Program.cs** "。</span><span class="sxs-lookup"><span data-stu-id="39f63-148">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="39f63-149">通过将连接字符串传递给它来创建一个`ConnectionMultiplexer` `ConnectionMultiplexer.Connect`</span><span class="sxs-lookup"><span data-stu-id="39f63-149">Create a `ConnectionMultiplexer` using `ConnectionMultiplexer.Connect` by passing it your connection string.</span></span> <span data-ttu-id="39f63-150">将返回的值命名为**cache**。</span><span class="sxs-lookup"><span data-stu-id="39f63-150">Name the returned value **cache**.</span></span>

1. <span data-ttu-id="39f63-151">由于创建的连接是可_处置_的, 因此请`using`将其包装在块中。</span><span class="sxs-lookup"><span data-stu-id="39f63-151">Since the created connection is _disposable_, wrap it in a `using` block.</span></span> <span data-ttu-id="39f63-152">您的代码应类似于以下内容:</span><span class="sxs-lookup"><span data-stu-id="39f63-152">Your code should look something like:</span></span>

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> <span data-ttu-id="39f63-153">与 Redis 的 Azure 缓存的连接由`ConnectionMultiplexer`类管理。</span><span class="sxs-lookup"><span data-stu-id="39f63-153">The connection to Azure Cache for Redis is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="39f63-154">应在整个客户端应用程序中共享和重用此类。</span><span class="sxs-lookup"><span data-stu-id="39f63-154">This class should be shared and reused throughout your client application.</span></span> <span data-ttu-id="39f63-155">我们_不_想为每个操作创建新的连接。</span><span class="sxs-lookup"><span data-stu-id="39f63-155">We do _not_ want to create a new connection for each operation.</span></span> <span data-ttu-id="39f63-156">相反, 我们希望将其作为类中的字段进行存储, 并对每个操作重用它。</span><span class="sxs-lookup"><span data-stu-id="39f63-156">Instead, we want to store it off as a field in our class and reuse it for each operation.</span></span> <span data-ttu-id="39f63-157">此处, 我们只打算在**Main**方法中使用它, 但在生产应用程序中, 应将其存储在类字段或 singleton 中。</span><span class="sxs-lookup"><span data-stu-id="39f63-157">Here we are only going to use it in the **Main** method, but in a production application, it should be stored in a class field, or a singleton.</span></span>

## <a name="add-a-value-to-the-cache"></a><span data-ttu-id="39f63-158">将值添加到缓存</span><span class="sxs-lookup"><span data-stu-id="39f63-158">Add a value to the cache</span></span>

<span data-ttu-id="39f63-159">现在, 我们已建立了连接, 让我们将值添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="39f63-159">Now that we have the connection, let's add a value to the cache.</span></span>

1. <span data-ttu-id="39f63-160">在创建`using`连接后的块内, 使用`GetDatabase`方法检索`IDatabase`实例。</span><span class="sxs-lookup"><span data-stu-id="39f63-160">Inside the `using` block after the connection has been created, use the `GetDatabase` method to retrieve an `IDatabase` instance.</span></span>

    ```csharp
    IDatabase db = cache.GetDatabase();
    ```

1. <span data-ttu-id="39f63-161">对`StringSet` `IDatabase`对象的调用, 以将键 "test: key" 设置为值 "some value"。</span><span class="sxs-lookup"><span data-stu-id="39f63-161">Call `StringSet` on the `IDatabase` object to set the key "test:key" to the value "some value".</span></span>
    - <span data-ttu-id="39f63-162">中`StringSet`的返回值是指示`bool`是否添加了该键的值。</span><span class="sxs-lookup"><span data-stu-id="39f63-162">the return value from `StringSet` is a `bool` indicating whether the key was added.</span></span>

1. <span data-ttu-id="39f63-163">将返回值从`StringSet`控制台显示到控制台。</span><span class="sxs-lookup"><span data-stu-id="39f63-163">Display the return value from `StringSet` onto the console.</span></span>

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a><span data-ttu-id="39f63-164">从缓存中获取值</span><span class="sxs-lookup"><span data-stu-id="39f63-164">Get a value from the cache</span></span>

1. <span data-ttu-id="39f63-165">接下来, 使用`StringGet`检索值。</span><span class="sxs-lookup"><span data-stu-id="39f63-165">Next, retrieve the value using `StringGet`.</span></span> <span data-ttu-id="39f63-166">这将采用密钥来检索和返回值。</span><span class="sxs-lookup"><span data-stu-id="39f63-166">This takes the key to retrieve and returns the value.</span></span>

1. <span data-ttu-id="39f63-167">输出返回的值。</span><span class="sxs-lookup"><span data-stu-id="39f63-167">Output the returned value.</span></span>

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. <span data-ttu-id="39f63-168">代码应如下所示:</span><span class="sxs-lookup"><span data-stu-id="39f63-168">Your code should look like this:</span></span>

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;
    using StackExchange.Redis;
    
    namespace SportsStatsTracker
    {
        class Program
        {
            static void Main(string[] args)
            {
                var config = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json")
                    .Build();
    
                string connectionString = config["CacheConnection"];
    
                using (var cache = ConnectionMultiplexer.Connect(connectionString))
                {
                    IDatabase db = cache.GetDatabase();
    
                    bool setValue = db.StringSet("test:key", "some value");
                    Console.WriteLine($"SET: {setValue}");
    
                    string getValue = db.StringGet("test:key");
                    Console.WriteLine($"GET: {getValue}");
                }
            }
        }
    }
    ```
    
1. <span data-ttu-id="39f63-169">运行应用程序以查看结果。</span><span class="sxs-lookup"><span data-stu-id="39f63-169">Run the application to see the result.</span></span> <span data-ttu-id="39f63-170">在`dotnet run`编辑器下方的 "终端" 窗口中键入。</span><span class="sxs-lookup"><span data-stu-id="39f63-170">Type `dotnet run` into the terminal window below the editor.</span></span> <span data-ttu-id="39f63-171">确保您在项目文件夹中, 否则它将无法找到要生成和运行的代码。</span><span class="sxs-lookup"><span data-stu-id="39f63-171">Make sure you are in the project folder or it won't find your code to build and run.</span></span>
    
    ```bash
    dotnet run
    ```
    
> [!TIP] 
> <span data-ttu-id="39f63-172">如果程序不执行预期的操作, 但编译, 可能是因为您没有在编辑器中保存更改。</span><span class="sxs-lookup"><span data-stu-id="39f63-172">If the program doesn't do what you expect, but compiles, it may be because you have not saved changes in the editor.</span></span> <span data-ttu-id="39f63-173">在终端和编辑器窗口之间切换时, 始终记得保存所做的更改</span><span class="sxs-lookup"><span data-stu-id="39f63-173">Always remember to save changes as you switch between the terminal and the editor windows</span></span> 

## <a name="use-the-async-versions-of-the-methods"></a><span data-ttu-id="39f63-174">使用方法的异步版本</span><span class="sxs-lookup"><span data-stu-id="39f63-174">Use the async versions of the methods</span></span>

<span data-ttu-id="39f63-175">我们可以从缓存中获取和设置值, 但我们使用的是较旧的同步版本。</span><span class="sxs-lookup"><span data-stu-id="39f63-175">We have been able to get and set values from the cache, but we are using the older synchronous versions.</span></span> <span data-ttu-id="39f63-176">在服务器端应用程序中, 这不是我们的线程的有效使用。</span><span class="sxs-lookup"><span data-stu-id="39f63-176">In server-side applications, these are not an efficient use of our threads.</span></span> <span data-ttu-id="39f63-177">相反, 我们想要使用方法的_异步_版本。</span><span class="sxs-lookup"><span data-stu-id="39f63-177">Instead, we want to use the _asynchronous_ versions of the methods.</span></span> <span data-ttu-id="39f63-178">你可以轻松地找到它们-它们都以**异步**方式结束。</span><span class="sxs-lookup"><span data-stu-id="39f63-178">You can easily spot them - they all end in **Async**.</span></span>

<span data-ttu-id="39f63-179">若要使这些方法易于使用, 我们可以使用 c # `async`和`await`关键字。</span><span class="sxs-lookup"><span data-stu-id="39f63-179">To make these methods easy to work with, we can use the C# `async` and `await` keywords.</span></span> <span data-ttu-id="39f63-180">但是, 我们需要_至少_使用 c # 7.1, 才能将这些关键字应用到**主**方法。</span><span class="sxs-lookup"><span data-stu-id="39f63-180">However, we will need to be using _at least_ C# 7.1 to be able to apply these keywords to our **Main** method.</span></span>

### <a name="switch-to-c-71"></a><span data-ttu-id="39f63-181">切换到 c # 7。1</span><span class="sxs-lookup"><span data-stu-id="39f63-181">Switch to C# 7.1</span></span>

<span data-ttu-id="39f63-182">在 c `async` # `await` 7.1 之前, c # 和关键字在**Main**方法中不是有效的关键字。</span><span class="sxs-lookup"><span data-stu-id="39f63-182">C#'s `async` and `await` keywords were not valid keywords in **Main** methods until C# 7.1.</span></span> <span data-ttu-id="39f63-183">我们可以通过 **.csproj**文件中的标志轻松切换到该编译器。</span><span class="sxs-lookup"><span data-stu-id="39f63-183">We can easily switch to that compiler through a flag in the **.csproj** file.</span></span>

1. <span data-ttu-id="39f63-184">在编辑器中打开**SportsStatsTracker**文件。</span><span class="sxs-lookup"><span data-stu-id="39f63-184">Open the **SportsStatsTracker.csproj** file in the editor.</span></span>

1. <span data-ttu-id="39f63-185">在`<LangVersion>7.1</LangVersion>`生成文件中`PropertyGroup`添加到第一个中。</span><span class="sxs-lookup"><span data-stu-id="39f63-185">Add `<LangVersion>7.1</LangVersion>` into the first `PropertyGroup` in the build file.</span></span> <span data-ttu-id="39f63-186">完成后, 其外观应如下所示。</span><span class="sxs-lookup"><span data-stu-id="39f63-186">It should look like the following when you are finished.</span></span>
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a><span data-ttu-id="39f63-187">应用 async 关键字</span><span class="sxs-lookup"><span data-stu-id="39f63-187">Apply the async keyword</span></span>

<span data-ttu-id="39f63-188">接下来, 将`async`关键字应用于**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="39f63-188">Next, apply the `async` keyword to the **Main** method.</span></span> <span data-ttu-id="39f63-189">我们将需要执行三项操作。</span><span class="sxs-lookup"><span data-stu-id="39f63-189">We will have to do three things.</span></span>

1. <span data-ttu-id="39f63-190">将`async`关键字添加到**Main**方法签名中。</span><span class="sxs-lookup"><span data-stu-id="39f63-190">Add the `async` keyword onto the **Main** method signature.</span></span>
1. <span data-ttu-id="39f63-191">将返回类型从`void`更改为`Task`。</span><span class="sxs-lookup"><span data-stu-id="39f63-191">Change the return type from `void` to `Task`.</span></span>
1. <span data-ttu-id="39f63-192">添加要`using`包含`System.Threading.Tasks`的语句。</span><span class="sxs-lookup"><span data-stu-id="39f63-192">Add a `using` statement to include `System.Threading.Tasks`.</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using StackExchange.Redis;
using System.Threading.Tasks;

namespace SportsStatsTracker
{
    class Program
    {
        static async Task Main(string[] args)
        {
        ...
```

### <a name="get-and-set-values-asynchronously"></a><span data-ttu-id="39f63-193">异步获取和设置值</span><span class="sxs-lookup"><span data-stu-id="39f63-193">Get and set values asynchronously</span></span>

<span data-ttu-id="39f63-194">我们可以将同步方法保持不变, 让我们添加对`StringSetAsync`和`StringGetAsync`方法的调用, 以将另一个值添加到缓存中。</span><span class="sxs-lookup"><span data-stu-id="39f63-194">We can leave the synchronous methods in place, let's add a call to the `StringSetAsync` and `StringGetAsync` methods to add another value to the cache.</span></span> <span data-ttu-id="39f63-195">将 "counter" 设置为值 "100"。</span><span class="sxs-lookup"><span data-stu-id="39f63-195">Set "counter" to the value "100".</span></span>  

1. <span data-ttu-id="39f63-196">使用`StringSetAsync`和`StringGetAsync`方法设置和检索名为 "counter" 的密钥。</span><span class="sxs-lookup"><span data-stu-id="39f63-196">Use the `StringSetAsync` and `StringGetAsync` methods to set and retrieve a key named "counter".</span></span> <span data-ttu-id="39f63-197">将值设置为 "100"。</span><span class="sxs-lookup"><span data-stu-id="39f63-197">Set the value to "100".</span></span>

1. <span data-ttu-id="39f63-198">应用`await`关键字以获取每个方法的结果。</span><span class="sxs-lookup"><span data-stu-id="39f63-198">Apply the `await` keyword to get the results from each method.</span></span>

1. <span data-ttu-id="39f63-199">将结果输出到控制台窗口, 就像对同步版本执行的操作一样。</span><span class="sxs-lookup"><span data-stu-id="39f63-199">Output the results to the console window - just as you did with the synchronous versions.</span></span>

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. <span data-ttu-id="39f63-200">再次运行应用程序-它仍应正常运行, 并且现在有两个值。</span><span class="sxs-lookup"><span data-stu-id="39f63-200">Run the application again - it should still work and now have two values.</span></span>

#### <a name="increment-the-value"></a><span data-ttu-id="39f63-201">递增值</span><span class="sxs-lookup"><span data-stu-id="39f63-201">Increment the value</span></span>

1. <span data-ttu-id="39f63-202">使用`StringIncrementAsync`方法可增加**计数器**值。</span><span class="sxs-lookup"><span data-stu-id="39f63-202">Use the `StringIncrementAsync` method to increment your **counter** value.</span></span> <span data-ttu-id="39f63-203">将数字**50**传递给计数器。</span><span class="sxs-lookup"><span data-stu-id="39f63-203">Pass the number **50** to add to the counter.</span></span>
    - <span data-ttu-id="39f63-204">请注意, 该方法采用键 _,_ `long`或者是或`double`。</span><span class="sxs-lookup"><span data-stu-id="39f63-204">Notice that the method takes the key _and_ either a `long` or `double`.</span></span>
    - <span data-ttu-id="39f63-205">根据传递的参数, 它可以返回`long`或。 `double`</span><span class="sxs-lookup"><span data-stu-id="39f63-205">Depending on the parameters passed, it either returns a `long` or `double`.</span></span>

1. <span data-ttu-id="39f63-206">将方法的结果输出到控制台。</span><span class="sxs-lookup"><span data-stu-id="39f63-206">Output the results of the method to the console.</span></span>

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a><span data-ttu-id="39f63-207">其他操作</span><span class="sxs-lookup"><span data-stu-id="39f63-207">Other operations</span></span>

<span data-ttu-id="39f63-208">最后, 让我们尝试使用`ExecuteAsync`支持执行几个其他方法。</span><span class="sxs-lookup"><span data-stu-id="39f63-208">Finally, let's try executing a few additional methods with the `ExecuteAsync` support.</span></span>

1. <span data-ttu-id="39f63-209">执行 "PING" 以测试服务器连接。</span><span class="sxs-lookup"><span data-stu-id="39f63-209">Execute "PING" to test the server connection.</span></span> <span data-ttu-id="39f63-210">它应以 "乒乓球" 为响应。</span><span class="sxs-lookup"><span data-stu-id="39f63-210">It should respond with "PONG".</span></span>
1. <span data-ttu-id="39f63-211">执行 "FLUSHDB" 以清除数据库值。</span><span class="sxs-lookup"><span data-stu-id="39f63-211">Execute "FLUSHDB" to clear the database values.</span></span> <span data-ttu-id="39f63-212">它应以 "确定" 响应。</span><span class="sxs-lookup"><span data-stu-id="39f63-212">It should respond with "OK".</span></span>

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

<span data-ttu-id="39f63-213">最终代码应该如下所示:</span><span class="sxs-lookup"><span data-stu-id="39f63-213">The final code should look something like:</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using StackExchange.Redis;
using System.Threading.Tasks;

namespace SportsStatsTracker
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var config = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json")
                .Build();

            string connectionString = config["CacheConnection"];

            using (var cache = ConnectionMultiplexer.Connect(connectionString))
            {
                IDatabase db = cache.GetDatabase();

                bool setValue = db.StringSet("test:key", "some value");
                Console.WriteLine($"SET: {setValue}");

                string getValue = db.StringGet("test:key");
                Console.WriteLine($"GET: {getValue}");

                setValue = await db.StringSetAsync("test", "100");
                Console.WriteLine($"SET: {setValue}");

                getValue = await db.StringGetAsync("test");
                Console.WriteLine($"GET: {getValue}");

                var result = await db.ExecuteAsync("ping");
                Console.WriteLine($"PING = {result.Type} : {result}");
                
                result = await db.ExecuteAsync("flushdb");
                Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
            }
        }
    }
}
```

## <a name="challenge"></a><span data-ttu-id="39f63-214">质疑</span><span class="sxs-lookup"><span data-stu-id="39f63-214">Challenge</span></span>

<span data-ttu-id="39f63-215">作为一项挑战, 请尝试将对象类型序列化到缓存中。</span><span class="sxs-lookup"><span data-stu-id="39f63-215">As a challenge, try serializing an object type to the cache.</span></span> <span data-ttu-id="39f63-216">下面是基本步骤。</span><span class="sxs-lookup"><span data-stu-id="39f63-216">Here are the basic steps.</span></span>

1. <span data-ttu-id="39f63-217">创建具有一些`class`公共属性的新属性。</span><span class="sxs-lookup"><span data-stu-id="39f63-217">Create a new `class` with some public properties.</span></span> <span data-ttu-id="39f63-218">您可以使用一个自己的库存 ("人员" 或 "汽车" 受欢迎), 也可以使用上一个单位中给出的 "GameStats" 示例。</span><span class="sxs-lookup"><span data-stu-id="39f63-218">You can invent one of your own ("Person" or "Car" are popular), or use the "GameStats" example given in the previous unit.</span></span>

1. <span data-ttu-id="39f63-219">使用`dotnet add package`添加对**newtonsoft.json** NuGet 包的支持。</span><span class="sxs-lookup"><span data-stu-id="39f63-219">Add support for the **Newtonsoft.Json** NuGet package using `dotnet add package`.</span></span>

1. <span data-ttu-id="39f63-220">`using`为`Newtonsoft.Json`命名空间添加。</span><span class="sxs-lookup"><span data-stu-id="39f63-220">Add a `using` for the `Newtonsoft.Json` namespace.</span></span>

1. <span data-ttu-id="39f63-221">创建一个对象。</span><span class="sxs-lookup"><span data-stu-id="39f63-221">Create one of your objects.</span></span>

1. <span data-ttu-id="39f63-222">使用`JsonConvert.SerializeObject`将其序列化`StringSetAsync`并使用将其推送到缓存中。</span><span class="sxs-lookup"><span data-stu-id="39f63-222">Serialize it with `JsonConvert.SerializeObject` and use `StringSetAsync` to push it into the cache.</span></span>

1. <span data-ttu-id="39f63-223">将其从缓存中返回`StringGetAsync` , 然后再将其反`JsonConvert.DeserializeObject<T>`序列化。</span><span class="sxs-lookup"><span data-stu-id="39f63-223">Get it back from the cache with `StringGetAsync` and then deserialize it with `JsonConvert.DeserializeObject<T>`.</span></span>

