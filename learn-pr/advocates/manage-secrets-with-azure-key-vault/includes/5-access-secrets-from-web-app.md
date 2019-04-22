<span data-ttu-id="a3b83-101">现在, 您已经了解如何为应用程序的托管标识创建标识以用于身份验证, 我们将创建一个使用该标识访问保管库中的机密的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a3b83-101">Now that you know how enabling managed identities for Azure resources creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

::: zone pivot="csharp"

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="a3b83-102">在 ASP.NET 核心应用程序中读取机密</span><span class="sxs-lookup"><span data-stu-id="a3b83-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="a3b83-103">Azure Key Vault api 是一个 REST API, 它处理密钥和电子仓库的所有管理和使用。</span><span class="sxs-lookup"><span data-stu-id="a3b83-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="a3b83-104">保管库中的每个密码都具有唯一的 URL, 并且使用 HTTP GET 请求检索机密值。</span><span class="sxs-lookup"><span data-stu-id="a3b83-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="a3b83-105">适用于 .net Core 的官方主要电子仓库客户`KeyVaultClient`端是 KeyVault NuGet 包中的类。</span><span class="sxs-lookup"><span data-stu-id="a3b83-105">The official Key Vault client for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="a3b83-106">您不需要直接使用它, 但&mdash;使用 ASP.NET Core 的`AddAzureKeyVault`方法时, 您可以将电子仓库中的所有密码加载到配置 API 中启动时。</span><span class="sxs-lookup"><span data-stu-id="a3b83-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="a3b83-107">使用此技术可以通过名称访问所有的密码, 方法是使用用于`IConfiguration`其余配置的相同接口。</span><span class="sxs-lookup"><span data-stu-id="a3b83-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="a3b83-108">使用`AddAzureKeyVault`的应用程序需要对保管库具有**Get**和**List**权限。</span><span class="sxs-lookup"><span data-stu-id="a3b83-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="a3b83-109">无论您用于构建应用程序的框架或语言如何, 都应设计它以在本地缓存机密值, 或在启动时将这些值加载到内存中, 除非您有具体原因不是这样。</span><span class="sxs-lookup"><span data-stu-id="a3b83-109">Regardless of the framework or language you use to build your app, you should design it to cache secret values locally or load them into memory at startup unless you have a specific reason not to.</span></span> <span data-ttu-id="a3b83-110">每次需要时, 直接从保管库中读取这些文件是不必要的速度和昂贵的。</span><span class="sxs-lookup"><span data-stu-id="a3b83-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="a3b83-111">`AddAzureKeyVault`仅需要将保管库名称作为输入, 我们将从我们的本地应用配置中获取此信息。</span><span class="sxs-lookup"><span data-stu-id="a3b83-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="a3b83-112">如果在部署到 azure 应用服务&mdash;的应用程序中使用托管标识启用了 azure 资源的托管标识, 则它还会自动处理托管身份验证, 它将检测托管标识令牌服务并使用它进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a3b83-112">It also automatically handles managed identity authentication &mdash; when used in an app deployed to Azure App Service with managed identities for Azure resources enabled, it will detect the managed identities token service and use it to authenticate.</span></span> <span data-ttu-id="a3b83-113">非常适合大多数场景并实现所有最佳实践, 我们将在此单元练习中使用它。</span><span class="sxs-lookup"><span data-stu-id="a3b83-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

::: zone-end

::: zone pivot="javascript"

## <a name="reading-secrets-in-a-nodejs-app"></a><span data-ttu-id="a3b83-114">在 node.js 应用中读取机密</span><span class="sxs-lookup"><span data-stu-id="a3b83-114">Reading secrets in a Node.js app</span></span>

<span data-ttu-id="a3b83-115">Azure Key Vault api 是一个 REST API, 它处理密钥和电子仓库的所有管理和使用。</span><span class="sxs-lookup"><span data-stu-id="a3b83-115">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="a3b83-116">保管库中的每个密码都具有唯一的 URL, 并且使用 HTTP GET 请求检索机密值。</span><span class="sxs-lookup"><span data-stu-id="a3b83-116">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="a3b83-117">node.js 应用的官方密钥保管库客户端是`KeyVaultClient` `azure-keyvault` npm 包中的类。</span><span class="sxs-lookup"><span data-stu-id="a3b83-117">The official Key Vault client for Node.js apps is the `KeyVaultClient` class in the `azure-keyvault` npm package.</span></span> <span data-ttu-id="a3b83-118">在其配置或代码中包含机密名称的应用程序通常只需使用其`getSecret`方法, 可在给定名称时加载一个机密值。</span><span class="sxs-lookup"><span data-stu-id="a3b83-118">Apps that include secret names in their configuration or code will generally only need to use its `getSecret` method, which loads a secret value given its name.</span></span> <span data-ttu-id="a3b83-119">`getSecret`要求您的应用程序的标识具有对保管库的**Get**权限。</span><span class="sxs-lookup"><span data-stu-id="a3b83-119">`getSecret` requires your app's identity to have the **Get** permission on the vault.</span></span> <span data-ttu-id="a3b83-120">设计用于从保管库加载所有机密的`getSecrets`应用程序也使用方法, 该方法将加载密码列表并需要**列表**权限。</span><span class="sxs-lookup"><span data-stu-id="a3b83-120">Apps designed to load all secrets from a vault will also use the `getSecrets` method, which loads a list of secrets and requires the **List** permission.</span></span>

<span data-ttu-id="a3b83-121">在您的应用程序可以`KeyVaultClient`创建实例之前, 它必须通过对保管库进行身份验证来获取 credential 对象。</span><span class="sxs-lookup"><span data-stu-id="a3b83-121">Before your app can create a `KeyVaultClient` instance, it must get a credential object by authenticating to the vault.</span></span> <span data-ttu-id="a3b83-122">若要进行身份验证, 请使用`ms-rest-azure` npm 包提供的一种登录函数。</span><span class="sxs-lookup"><span data-stu-id="a3b83-122">To authenticate, use the one of the login functions provided by the `ms-rest-azure` npm package.</span></span> <span data-ttu-id="a3b83-123">这些函数中的每一个都将返回一个 credential 对象, 可用于创建`KeyVaultClient`。</span><span class="sxs-lookup"><span data-stu-id="a3b83-123">Each of these functions will return a credential object that can be used to create a `KeyVaultClient`.</span></span> <span data-ttu-id="a3b83-124">`loginWithAppServiceMSI`函数将自动使用托管标识凭据, 应用程序服务可通过环境变量向应用程序提供这些凭据。</span><span class="sxs-lookup"><span data-stu-id="a3b83-124">The `loginWithAppServiceMSI` function will automatically use the managed identity credentials that App Service makes available to your app via environment variables.</span></span> <span data-ttu-id="a3b83-125">对于您的应用程序无法访问托管标识的测试环境或其他非应用服务环境, 您可以手动为您的应用程序创建服务主体并使用该`loginWithServicePrincipalSecret`函数进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a3b83-125">For test environments or other non-App Service environments where your app does not have access to a managed identity, you can manually create a service principal for your app and use the `loginWithServicePrincipalSecret` function to authenticate.</span></span>

> [!TIP]
> <span data-ttu-id="a3b83-126">无论您用于构建应用程序的框架或语言如何, 都应设计它以在本地缓存机密值, 或在启动时将这些值加载到内存中, 除非您有具体原因不是这样。</span><span class="sxs-lookup"><span data-stu-id="a3b83-126">Regardless of the framework or language you use to build your app, you should design it to cache secret values locally or load them into memory at startup unless you have a specific reason not to.</span></span> <span data-ttu-id="a3b83-127">每次需要时, 直接从保管库中读取这些文件是不必要的速度和昂贵的。</span><span class="sxs-lookup"><span data-stu-id="a3b83-127">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

::: zone-end

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="a3b83-128">在应用程序中处理机密</span><span class="sxs-lookup"><span data-stu-id="a3b83-128">Handling secrets in an app</span></span>

<span data-ttu-id="a3b83-129">将机密加载到应用程序后, 您的应用程序就可以安全地对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="a3b83-129">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="a3b83-130">在我们在此模块中构建的应用程序中, 我们将机密值写入客户端响应, 并在 web 浏览器中查看它以表明已成功加载它。</span><span class="sxs-lookup"><span data-stu-id="a3b83-130">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="a3b83-131">**通常情况下, 向客户端返回一个机密值*不*是什么!**</span><span class="sxs-lookup"><span data-stu-id="a3b83-131">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="a3b83-132">通常, 您将使用机密来执行数据库的初始化工作库或远程 api 等操作。</span><span class="sxs-lookup"><span data-stu-id="a3b83-132">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3b83-133">请务必认真查看代码, 以确保您的应用程序永远不会向任何类型的输出 (包括日志、存储和响应) 中写入机密信息。</span><span class="sxs-lookup"><span data-stu-id="a3b83-133">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="a3b83-134">健身</span><span class="sxs-lookup"><span data-stu-id="a3b83-134">Exercise</span></span>

::: zone pivot="csharp"

<span data-ttu-id="a3b83-135">我们将创建一个新的 ASP.NET Core web API, `AddAzureKeyVault`并使用我们的保管库加载机密。</span><span class="sxs-lookup"><span data-stu-id="a3b83-135">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="a3b83-136">创建应用程序</span><span class="sxs-lookup"><span data-stu-id="a3b83-136">Create the app</span></span>

<span data-ttu-id="a3b83-137">在 Azure 云 Shell 终端中, 运行以下命令以创建一个新的 ASP.NET Core web API 应用程序, 并在编辑器中打开它。</span><span class="sxs-lookup"><span data-stu-id="a3b83-137">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="a3b83-138">加载编辑器后, 在命令行管理程序中运行以下命令, 以添加包含`AddAzureKeyVault`和还原应用程序所有依赖项的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="a3b83-138">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault -v 2.1.1
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="a3b83-139">添加代码以加载和使用密码</span><span class="sxs-lookup"><span data-stu-id="a3b83-139">Add code to load and use secrets</span></span>

<span data-ttu-id="a3b83-140">为了演示密钥存储库的有效使用, 我们将修改应用程序, 以便在启动时从保管库加载密码。</span><span class="sxs-lookup"><span data-stu-id="a3b83-140">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="a3b83-141">我们还将添加一个新的控制器, 其中包含从保管库获取我们的**SecretPassword**机密的终结点。</span><span class="sxs-lookup"><span data-stu-id="a3b83-141">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="a3b83-142">首先, 应用程序启动: 打开`Program.cs`, 删除内容, 并将其替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="a3b83-142">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using a managed identity. If a managed identity
                    // is not available, it will check if Visual Studio and/or the Azure CLI are
                    // installed locally and see if they are configured with credentials that can
                    // access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="a3b83-143">完成编辑后, 请务必保存文件。</span><span class="sxs-lookup"><span data-stu-id="a3b83-143">Make sure to save files when you're done editing them.</span></span> <span data-ttu-id="a3b83-144">为此, 可以通过 "..."菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="a3b83-144">You can do this either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

<span data-ttu-id="a3b83-145">起始代码的唯一更改是添加`ConfigureAppConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="a3b83-145">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="a3b83-146">在这里, 我们将保管库名称从配置中加载`AddAzureKeyVault` , 并与之通话。</span><span class="sxs-lookup"><span data-stu-id="a3b83-146">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="a3b83-147">接下来, 控制器: 在名`Controllers` `SecretTestController.cs`为的文件夹中创建一个新文件, 并将以下代码粘贴到该文件中。</span><span class="sxs-lookup"><span data-stu-id="a3b83-147">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!TIP]
> <span data-ttu-id="a3b83-148">若要创建新文件, 请使用`touch`命令行管理程序中的命令。</span><span class="sxs-lookup"><span data-stu-id="a3b83-148">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="a3b83-149">在这种情况下`touch Controllers/SecretTestController.cs`, 请使用。</span><span class="sxs-lookup"><span data-stu-id="a3b83-149">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="a3b83-150">您需要单击编辑器的 "文件" 窗格中的 "刷新" 按钮以查看该文件。</span><span class="sxs-lookup"><span data-stu-id="a3b83-150">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

<span data-ttu-id="a3b83-151">在`dotnet build`命令行管理程序中运行以确保所有内容都进行编译。</span><span class="sxs-lookup"><span data-stu-id="a3b83-151">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="a3b83-152">现在, 该应用程序已&mdash;准备就绪, 可以立即开始运行!</span><span class="sxs-lookup"><span data-stu-id="a3b83-152">The app is ready to run &mdash; now let's get it into Azure!</span></span>

::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="a3b83-153">我们将使用 Express .js 创建一个新的 web API, 并使用`azure-keyvault`和`ms-rest-azure`包从我们的保管库加载机密。</span><span class="sxs-lookup"><span data-stu-id="a3b83-153">We'll create a new web API with Express.js and use the `azure-keyvault` and `ms-rest-azure` packages to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="a3b83-154">创建应用程序</span><span class="sxs-lookup"><span data-stu-id="a3b83-154">Create the app</span></span>

<span data-ttu-id="a3b83-155">在 Azure 云 Shell 终端中, 运行以下命令以初始化新的 node.js 应用程序, 安装所需的包, 并在编辑器中打开一个新文件。</span><span class="sxs-lookup"><span data-stu-id="a3b83-155">In the Azure Cloud Shell terminal, run the following to initialize a new Node.js application, install the needed packages, and open a new file in the editor.</span></span>

```console
mkdir KeyVaultDemoApp
cd KeyVaultDemoApp
npm init -y
npm install ms-rest-azure azure-keyvault express
touch app.js
code app.js
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="a3b83-156">添加代码以加载和使用密码</span><span class="sxs-lookup"><span data-stu-id="a3b83-156">Add code to load and use secrets</span></span>

<span data-ttu-id="a3b83-157">为了演示密钥保管库的有效使用, 我们的应用将在启动时从保管库加载密码。</span><span class="sxs-lookup"><span data-stu-id="a3b83-157">To demonstrate good usage of Key Vault, our app will load secrets from the vault at startup.</span></span> <span data-ttu-id="a3b83-158">为了说明已加载我们的机密, 我们将创建一个显示**SecretPassword**密码值的终结点。</span><span class="sxs-lookup"><span data-stu-id="a3b83-158">To demonstrate that our secrets have been loaded, we'll create an endpoint that displays the value of the **SecretPassword** secret.</span></span>

<span data-ttu-id="a3b83-159">首先, 将以下代码粘贴到编辑器中以设置应用程序。</span><span class="sxs-lookup"><span data-stu-id="a3b83-159">First, paste the following code into the editor to set up the application.</span></span> <span data-ttu-id="a3b83-160">这将导入所需的包, 设置端口和保管库 URL 配置, 并创建一个新对象来保存机密名称和值。</span><span class="sxs-lookup"><span data-stu-id="a3b83-160">This will import the necessary packages, set up the port and vault URL configuration, and create a new object to hold the secret names and values.</span></span>

```javascript
// Importing dependencies
const msRestAzure = require('ms-rest-azure');
const keyVault = require('azure-keyvault');
const app = require('express')();

// Initialize port
const port = process.env.PORT || 3000;

// Create Vault URL from App Settings
const vaultUrl = `https://${process.env.VaultName}.vault.azure.net/`;

// Map of key vault secret names to values
let vaultSecretsMap = {};
```

> [!IMPORTANT]
> <span data-ttu-id="a3b83-161">请务必在处理文件时保存这些文件, 尤其是在完成时。</span><span class="sxs-lookup"><span data-stu-id="a3b83-161">Make sure to save files as you work on them, especially when you're finished.</span></span> <span data-ttu-id="a3b83-162">为此, 可以通过 "..."菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="a3b83-162">You can do this either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

<span data-ttu-id="a3b83-163">接下来, 我们将添加代码以向保管库进行身份验证并加载密码。</span><span class="sxs-lookup"><span data-stu-id="a3b83-163">Next, we'll add the code to authenticate to the vault and load the secrets.</span></span> <span data-ttu-id="a3b83-164">我们将此添加为两个单独的函数。</span><span class="sxs-lookup"><span data-stu-id="a3b83-164">We'll add this as two separate functions.</span></span> <span data-ttu-id="a3b83-165">在之前添加的代码后面插入两个空行, 然后粘贴以下代码:</span><span class="sxs-lookup"><span data-stu-id="a3b83-165">Insert a couple of blank lines after the code you previously added and then paste in the following code:</span></span>

```javascript
const authenticateToKeyVault = async () => {
  try {
    let credentials;
    if (process.env.NODE_ENV === 'production') {
      credentials = await msRestAzure.loginWithAppServiceMSI({ resource: 'https://vault.azure.net' });
    } else {
      // For non-App Service environments. Set the APP_ID, APP_SECRET and TENANT_ID environment
      // variables to use.
      const appId = process.env.APP_ID;
      const appSecret = process.env.APP_SECRET;
      const tenantId = process.env.TENANT_ID;
      credentials = await msRestAzure.loginWithServicePrincipalSecret(appId, appSecret, tenantId);
    }
    return credentials;
  } catch(err) {
    throw err.message;
  }
}

const getKeyVaultSecrets = async credentials => {
  // Create a key vault client
  let keyVaultClient = new keyVault.KeyVaultClient(credentials);
  try {
    let secrets = await keyVaultClient.getSecrets(vaultUrl);
    // For each secret name, get the secret value from the vault
    for (const secret of secrets) {
      // Only load enabled secrets - getSecret will return an error for disabled secrets
      if (secret.attributes.enabled) {
        let secretId = secret.id;
        let secretName = secretId.substring(secretId.lastIndexOf('/') + 1);
        let secretValue = await keyVaultClient.getSecret(vaultUrl, secretName, '');
        vaultSecretsMap[secretName] = secretValue.value;
      }
    }
  } catch(err) {
    console.log(err.message)
  }
}
```

<span data-ttu-id="a3b83-166">现在, 创建 Express 终结点, 我们将使用它测试是否已加载密码。</span><span class="sxs-lookup"><span data-stu-id="a3b83-166">Now create the Express endpoint we'll use to test whether our secret was loaded.</span></span> <span data-ttu-id="a3b83-167">在下面的代码中粘贴:</span><span class="sxs-lookup"><span data-stu-id="a3b83-167">Paste in this code next:</span></span>

```javascript
app.get('/api/SecretTest', (req, res) => {
  let secretName = 'SecretPassword';
  let response;
  if (secretName in vaultSecretsMap) {
    response = `Secret value: ${vaultSecretsMap[secretName]}\n\nThis is for testing only! Never output a secret to a response or anywhere else in a real app!`;
  } else {
    response = `Error: No secret named ${secretName} was found...`
  }
  res.type('text');
  res.send(response);
});
```

<span data-ttu-id="a3b83-168">最后, 我们将调用我们的函数以从我们的保管库加载密码, 然后启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="a3b83-168">Finally, we'll call our functions to load the secrets from our vault, then start the app.</span></span> <span data-ttu-id="a3b83-169">粘贴到此最后一个代码段以完成应用程序:</span><span class="sxs-lookup"><span data-stu-id="a3b83-169">Paste in this last snippet to complete the application:</span></span>

```javascript
(async () =>  {
  let credentials = await authenticateToKeyVault();
  await getKeyVaultSecrets(credentials);
  app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
  });
})().catch(err => console.log(err));
```

<span data-ttu-id="a3b83-170">我们已完成编写代码, 因此请务必保存文件。</span><span class="sxs-lookup"><span data-stu-id="a3b83-170">We're finished writing code, so make sure to save the file.</span></span> <span data-ttu-id="a3b83-171">现在, 该应用程序已&mdash;准备就绪, 可以立即开始运行!</span><span class="sxs-lookup"><span data-stu-id="a3b83-171">The app is ready to run &mdash; now let's get it into Azure!</span></span>

::: zone-end