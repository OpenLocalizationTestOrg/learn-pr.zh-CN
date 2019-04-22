至此, 我们已在 Azure 中创建了 Redis 缓存, 让我们创建一个应用程序来使用它。 请确保您的连接字符串信息来自 Azure 门户。

> [!NOTE]
> 可在右侧找到集成云命令行管理程序。 您可以使用该命令提示符创建并运行我们在此处构建的示例代码, 如果您有 .net Core 开发环境安装程序, 则可以在本地执行这些步骤。

## <a name="create-a-console-application"></a>创建控制台应用程序

我们将使用一个简单的控制台应用程序, 以便我们能够将重点放在 Redis 实现上。

1. 在云命令行管理程序中, 创建一个新的 .net Core 控制台应用程序, 将其命名为 "SportsStatsTracker"

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. 这将为项目创建一个文件夹, 继续并更改当前目录。

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a>添加连接字符串

让我们将从 Azure 门户获取的连接字符串添加到代码中。 请勿在源代码中将此类凭据存储为此代码。 若要使此示例简单, 我们要使用配置文件。 对于 azure 中的服务器端应用程序, 更好的方法是使用 Azure Key Vault 和证书。

1. 创建要添加到项目中的新的**appsettings**文件。

    ```bash
    touch appsettings.json
    ```

1. 在项目文件夹中键入`code .`以打开代码编辑器。 如果您在本地工作, 建议使用**Visual Studio Code**。 此处的步骤将主要与其使用一致。

1. 在编辑器中选择 " **appsettings** " 文件, 并添加以下文本。 将连接字符串粘贴到设置的**值**中。

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. 保存所做的更改。

    > [!IMPORTANT]
    > 只要您将代码粘贴或更改为编辑器中的文件, 就一定要使用 "..." 进行保存。菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

1. 单击编辑器中的 " **SportsStatsTracker** " 文件将其打开。

1. 将以下`<ItemGroup>`配置块添加到根`<Project>`元素中, 以将新文件包含在项目中, 并将其复制到输出文件夹。 这样可确保在编译/生成应用程序时, 将应用程序配置文件放在输出目录中。

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

1. 保存该文件。 (请务必执行此操作, 否则在下面添加包时, 会丢失所做的更改!)

## <a name="add-support-to-read-a-json-configuration-file"></a>添加对读取 JSON 配置文件的支持

.net Core 应用程序需要其他 NuGet 包才能读取 JSON 配置文件。

1. 在窗口的命令提示符部分, 添加对**Microsoft extension. Json** NuGet 包的引用。

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a>添加代码以读取配置文件

至此, 我们已经添加了启用读取配置所需的库, 我们需要在控制台应用程序中启用该功能。

1. 在编辑器中选择 " **Program.cs** "。

1. 在文件的顶部, 存在`using System`一行。 在该行下方, 添加以下代码行:

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. 将**Main**方法的内容替换为以下代码。 此代码会将配置系统初始化为从**appsettings**文件中读取。

    ```csharp
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json")
        .Build();
    ```

您的**Program.cs**文件现在应如下所示:

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

## <a name="get-the-connection-string-from-configuration"></a>从配置中获取连接字符串

1. 在**Program.cs**中, 在**Main**方法的末尾, 使用新的**配置**变量检索连接字符串, 并将其存储在名为**connectionString**的新变量中。
    - **config**变量包含一个索引器, 您可以在其中传递字符串以从**appSettings**文件中检索。

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a>添加对 Redis 缓存 .net 客户端的支持

接下来, 让我们将控制台应用程序配置为使用 .net 的**StackExchange Redis**客户端。

1. 使用云命令行管理程序编辑器底部的命令提示符将**StackExchange** NuGet 包添加到项目中。

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. 在编辑器中选择 " **Program.cs** ", `using`并为命名空间 StackExchange 添加一个 **。 Redis**

    ```csharp
    using StackExchange.Redis;
    ```
    
安装完成后, Redis 缓存客户端即可用于您的项目。

## <a name="connect-to-the-cache"></a>连接到缓存

让我们添加代码以连接到缓存。

1. 在编辑器中选择 " **Program.cs** "。

1. 通过将连接字符串传递给它来创建一个`ConnectionMultiplexer` `ConnectionMultiplexer.Connect` 将返回的值命名为**cache**。

1. 由于创建的连接是可_处置_的, 因此请`using`将其包装在块中。 您的代码应类似于以下内容:

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> 与 Redis 的 Azure 缓存的连接由`ConnectionMultiplexer`类管理。 应在整个客户端应用程序中共享和重用此类。 我们_不_想为每个操作创建新的连接。 相反, 我们希望将其作为类中的字段进行存储, 并对每个操作重用它。 此处, 我们只打算在**Main**方法中使用它, 但在生产应用程序中, 应将其存储在类字段或 singleton 中。

## <a name="add-a-value-to-the-cache"></a>将值添加到缓存

现在, 我们已建立了连接, 让我们将值添加到缓存中。

1. 在创建`using`连接后的块内, 使用`GetDatabase`方法检索`IDatabase`实例。

    ```csharp
    IDatabase db = cache.GetDatabase();
    ```

1. 对`StringSet` `IDatabase`对象的调用, 以将键 "test: key" 设置为值 "some value"。
    - 中`StringSet`的返回值是指示`bool`是否添加了该键的值。

1. 将返回值从`StringSet`控制台显示到控制台。

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a>从缓存中获取值

1. 接下来, 使用`StringGet`检索值。 这将采用密钥来检索和返回值。

1. 输出返回的值。

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. 代码应如下所示:

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
    
1. 运行应用程序以查看结果。 在`dotnet run`编辑器下方的 "终端" 窗口中键入。 确保您在项目文件夹中, 否则它将无法找到要生成和运行的代码。
    
    ```bash
    dotnet run
    ```
    
> [!TIP] 
> 如果程序不执行预期的操作, 但编译, 可能是因为您没有在编辑器中保存更改。 在终端和编辑器窗口之间切换时, 始终记得保存所做的更改 

## <a name="use-the-async-versions-of-the-methods"></a>使用方法的异步版本

我们可以从缓存中获取和设置值, 但我们使用的是较旧的同步版本。 在服务器端应用程序中, 这不是我们的线程的有效使用。 相反, 我们想要使用方法的_异步_版本。 你可以轻松地找到它们-它们都以**异步**方式结束。

若要使这些方法易于使用, 我们可以使用 c # `async`和`await`关键字。 但是, 我们需要_至少_使用 c # 7.1, 才能将这些关键字应用到**主**方法。

### <a name="switch-to-c-71"></a>切换到 c # 7。1

在 c `async` # `await` 7.1 之前, c # 和关键字在**Main**方法中不是有效的关键字。 我们可以通过 **.csproj**文件中的标志轻松切换到该编译器。

1. 在编辑器中打开**SportsStatsTracker**文件。

1. 在`<LangVersion>7.1</LangVersion>`生成文件中`PropertyGroup`添加到第一个中。 完成后, 其外观应如下所示。
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a>应用 async 关键字

接下来, 将`async`关键字应用于**Main**方法。 我们将需要执行三项操作。

1. 将`async`关键字添加到**Main**方法签名中。
1. 将返回类型从`void`更改为`Task`。
1. 添加要`using`包含`System.Threading.Tasks`的语句。

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

### <a name="get-and-set-values-asynchronously"></a>异步获取和设置值

我们可以将同步方法保持不变, 让我们添加对`StringSetAsync`和`StringGetAsync`方法的调用, 以将另一个值添加到缓存中。 将 "counter" 设置为值 "100"。  

1. 使用`StringSetAsync`和`StringGetAsync`方法设置和检索名为 "counter" 的密钥。 将值设置为 "100"。

1. 应用`await`关键字以获取每个方法的结果。

1. 将结果输出到控制台窗口, 就像对同步版本执行的操作一样。

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. 再次运行应用程序-它仍应正常运行, 并且现在有两个值。

#### <a name="increment-the-value"></a>递增值

1. 使用`StringIncrementAsync`方法可增加**计数器**值。 将数字**50**传递给计数器。
    - 请注意, 该方法采用键 _,_ `long`或者是或`double`。
    - 根据传递的参数, 它可以返回`long`或。 `double`

1. 将方法的结果输出到控制台。

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a>其他操作

最后, 让我们尝试使用`ExecuteAsync`支持执行几个其他方法。

1. 执行 "PING" 以测试服务器连接。 它应以 "乒乓球" 为响应。
1. 执行 "FLUSHDB" 以清除数据库值。 它应以 "确定" 响应。

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

最终代码应该如下所示:

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

## <a name="challenge"></a>质疑

作为一项挑战, 请尝试将对象类型序列化到缓存中。 下面是基本步骤。

1. 创建具有一些`class`公共属性的新属性。 您可以使用一个自己的库存 ("人员" 或 "汽车" 受欢迎), 也可以使用上一个单位中给出的 "GameStats" 示例。

1. 使用`dotnet add package`添加对**newtonsoft.json** NuGet 包的支持。

1. `using`为`Newtonsoft.Json`命名空间添加。

1. 创建一个对象。

1. 使用`JsonConvert.SerializeObject`将其序列化`StringSetAsync`并使用将其推送到缓存中。

1. 将其从缓存中返回`StringGetAsync` , 然后再将其反`JsonConvert.DeserializeObject<T>`序列化。

