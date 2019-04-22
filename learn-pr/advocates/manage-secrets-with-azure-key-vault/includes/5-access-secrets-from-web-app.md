现在, 您已经了解如何为应用程序的托管标识创建标识以用于身份验证, 我们将创建一个使用该标识访问保管库中的机密的应用程序。

::: zone pivot="csharp"

## <a name="reading-secrets-in-an-aspnet-core-app"></a>在 ASP.NET 核心应用程序中读取机密

Azure Key Vault api 是一个 REST API, 它处理密钥和电子仓库的所有管理和使用。 保管库中的每个密码都具有唯一的 URL, 并且使用 HTTP GET 请求检索机密值。

适用于 .net Core 的官方主要电子仓库客户`KeyVaultClient`端是 KeyVault NuGet 包中的类。 您不需要直接使用它, 但&mdash;使用 ASP.NET Core 的`AddAzureKeyVault`方法时, 您可以将电子仓库中的所有密码加载到配置 API 中启动时。 使用此技术可以通过名称访问所有的密码, 方法是使用用于`IConfiguration`其余配置的相同接口。 使用`AddAzureKeyVault`的应用程序需要对保管库具有**Get**和**List**权限。

> [!TIP]
> 无论您用于构建应用程序的框架或语言如何, 都应设计它以在本地缓存机密值, 或在启动时将这些值加载到内存中, 除非您有具体原因不是这样。 每次需要时, 直接从保管库中读取这些文件是不必要的速度和昂贵的。

`AddAzureKeyVault`仅需要将保管库名称作为输入, 我们将从我们的本地应用配置中获取此信息。 如果在部署到 azure 应用服务&mdash;的应用程序中使用托管标识启用了 azure 资源的托管标识, 则它还会自动处理托管身份验证, 它将检测托管标识令牌服务并使用它进行身份验证。 非常适合大多数场景并实现所有最佳实践, 我们将在此单元练习中使用它。

::: zone-end

::: zone pivot="javascript"

## <a name="reading-secrets-in-a-nodejs-app"></a>在 node.js 应用中读取机密

Azure Key Vault api 是一个 REST API, 它处理密钥和电子仓库的所有管理和使用。 保管库中的每个密码都具有唯一的 URL, 并且使用 HTTP GET 请求检索机密值。

node.js 应用的官方密钥保管库客户端是`KeyVaultClient` `azure-keyvault` npm 包中的类。 在其配置或代码中包含机密名称的应用程序通常只需使用其`getSecret`方法, 可在给定名称时加载一个机密值。 `getSecret`要求您的应用程序的标识具有对保管库的**Get**权限。 设计用于从保管库加载所有机密的`getSecrets`应用程序也使用方法, 该方法将加载密码列表并需要**列表**权限。

在您的应用程序可以`KeyVaultClient`创建实例之前, 它必须通过对保管库进行身份验证来获取 credential 对象。 若要进行身份验证, 请使用`ms-rest-azure` npm 包提供的一种登录函数。 这些函数中的每一个都将返回一个 credential 对象, 可用于创建`KeyVaultClient`。 `loginWithAppServiceMSI`函数将自动使用托管标识凭据, 应用程序服务可通过环境变量向应用程序提供这些凭据。 对于您的应用程序无法访问托管标识的测试环境或其他非应用服务环境, 您可以手动为您的应用程序创建服务主体并使用该`loginWithServicePrincipalSecret`函数进行身份验证。

> [!TIP]
> 无论您用于构建应用程序的框架或语言如何, 都应设计它以在本地缓存机密值, 或在启动时将这些值加载到内存中, 除非您有具体原因不是这样。 每次需要时, 直接从保管库中读取这些文件是不必要的速度和昂贵的。

::: zone-end

## <a name="handling-secrets-in-an-app"></a>在应用程序中处理机密

将机密加载到应用程序后, 您的应用程序就可以安全地对其进行处理。 在我们在此模块中构建的应用程序中, 我们将机密值写入客户端响应, 并在 web 浏览器中查看它以表明已成功加载它。 **通常情况下, 向客户端返回一个机密值*不*是什么!** 通常, 您将使用机密来执行数据库的初始化工作库或远程 api 等操作。

> [!IMPORTANT]
> 请务必认真查看代码, 以确保您的应用程序永远不会向任何类型的输出 (包括日志、存储和响应) 中写入机密信息。

## <a name="exercise"></a>健身

::: zone pivot="csharp"

我们将创建一个新的 ASP.NET Core web API, `AddAzureKeyVault`并使用我们的保管库加载机密。

### <a name="create-the-app"></a>创建应用程序

在 Azure 云 Shell 终端中, 运行以下命令以创建一个新的 ASP.NET Core web API 应用程序, 并在编辑器中打开它。

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

加载编辑器后, 在命令行管理程序中运行以下命令, 以添加包含`AddAzureKeyVault`和还原应用程序所有依赖项的 NuGet 包。

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault -v 2.1.1
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>添加代码以加载和使用密码

为了演示密钥存储库的有效使用, 我们将修改应用程序, 以便在启动时从保管库加载密码。 我们还将添加一个新的控制器, 其中包含从保管库获取我们的**SecretPassword**机密的终结点。

首先, 应用程序启动: 打开`Program.cs`, 删除内容, 并将其替换为以下代码:

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
> 完成编辑后, 请务必保存文件。 为此, 可以通过 "..."菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

起始代码的唯一更改是添加`ConfigureAppConfiguration`。 在这里, 我们将保管库名称从配置中加载`AddAzureKeyVault` , 并与之通话。

接下来, 控制器: 在名`Controllers` `SecretTestController.cs`为的文件夹中创建一个新文件, 并将以下代码粘贴到该文件中。

> [!TIP]
> 若要创建新文件, 请使用`touch`命令行管理程序中的命令。 在这种情况下`touch Controllers/SecretTestController.cs`, 请使用。 您需要单击编辑器的 "文件" 窗格中的 "刷新" 按钮以查看该文件。

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

在`dotnet build`命令行管理程序中运行以确保所有内容都进行编译。 现在, 该应用程序已&mdash;准备就绪, 可以立即开始运行!

::: zone-end

::: zone pivot="javascript"

我们将使用 Express .js 创建一个新的 web API, 并使用`azure-keyvault`和`ms-rest-azure`包从我们的保管库加载机密。

### <a name="create-the-app"></a>创建应用程序

在 Azure 云 Shell 终端中, 运行以下命令以初始化新的 node.js 应用程序, 安装所需的包, 并在编辑器中打开一个新文件。

```console
mkdir KeyVaultDemoApp
cd KeyVaultDemoApp
npm init -y
npm install ms-rest-azure azure-keyvault express
touch app.js
code app.js
```

### <a name="add-code-to-load-and-use-secrets"></a>添加代码以加载和使用密码

为了演示密钥保管库的有效使用, 我们的应用将在启动时从保管库加载密码。 为了说明已加载我们的机密, 我们将创建一个显示**SecretPassword**密码值的终结点。

首先, 将以下代码粘贴到编辑器中以设置应用程序。 这将导入所需的包, 设置端口和保管库 URL 配置, 并创建一个新对象来保存机密名称和值。

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
> 请务必在处理文件时保存这些文件, 尤其是在完成时。 为此, 可以通过 "..."菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

接下来, 我们将添加代码以向保管库进行身份验证并加载密码。 我们将此添加为两个单独的函数。 在之前添加的代码后面插入两个空行, 然后粘贴以下代码:

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

现在, 创建 Express 终结点, 我们将使用它测试是否已加载密码。 在下面的代码中粘贴:

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

最后, 我们将调用我们的函数以从我们的保管库加载密码, 然后启动应用程序。 粘贴到此最后一个代码段以完成应用程序:

```javascript
(async () =>  {
  let credentials = await authenticateToKeyVault();
  await getKeyVaultSecrets(credentials);
  app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
  });
})().catch(err => console.log(err));
```

我们已完成编写代码, 因此请务必保存文件。 现在, 该应用程序已&mdash;准备就绪, 可以立即开始运行!

::: zone-end