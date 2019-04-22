::: zone pivot="csharp"
让我们将 .net core 应用程序的支持添加到配置文件中, 以检索连接字符串。 我们将首先添加必要的管道来管理 JSON 文件中的配置。

## <a name="create-a-json-configuration-file"></a>创建 JSON 配置文件

1. `cd`如果尚不存在, 则为 PhotoSharingApp 目录。

1. 使用命令`touch`行中的工具创建一个名为**appsettings**的文件。

    ```bash
    touch appsettings.json
    ```

1. 在编辑器中打开项目。 如果您在本地工作, 请使用您的 "选择" 编辑器。 建议使用**Visual Studio Code**, 这是一个可扩展的跨平台 IDE。 如果使用的是云命令行管理程序, 我们建议使用云命令行管理程序编辑器。 以下命令适用于这两种情况。

    ```bash
    code .
    ```

1. 在编辑器中选择 " **appsettings** " 文件, 并添加以下文本。 保存该文件。 在云命令行管理程序编辑器中, 在右上角有一个菜单, 其中包含常见的文件操作。

    ```json
    {
      "StorageAccountConnectionString": "<value>"
    }
    ```

1. 现在, 我们需要获取存储帐户连接字符串, 并将其放入应用程序的配置中。 在云命令行管理程序中, 运行以下命令。

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. 复制从该命令返回的连接字符串, 并将**appsettings**文件`"<value>"`中的替换为此连接字符串。 保存该文件。

1. 接下来, 在编辑器中打开项目文件 (**PhotoSharingApp**)。

1. 添加以下配置块以将新文件包含在项目中, 并将其复制到输出文件夹。 这样可确保在编译/生成应用程序时, 将应用程序配置文件放在输出目录中。

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

1. 文件顶部有一个**使用系统;** 行。 在该行下方, 添加以下代码行:

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. 将**Main**方法的内容替换为以下代码。 此代码会将配置系统初始化为从**appsettings**文件中读取。

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

您的**Program.cs**文件现在应如下所示:

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace PhotoSharingApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
        }
    }
}
```

::: zone-end

::: zone pivot="javascript"

让我们将 node.js 应用程序的支持添加到配置文件中, 以检索连接字符串。 我们将首先添加必要的管道来管理 JavaScript 文件中的配置。

## <a name="create-a-env-configuration-file"></a>创建一个 env 配置文件

1. 确保您在项目的正确工作目录中。

1. 使用命令`touch`行中的工具创建名为 **. env**的文件。

    ```bash
    touch .env
    ```

1. 在云命令行管理程序编辑器中打开项目。

    ```bash
    code .
    ```

1. 选择编辑器中的 " **env** " 文件, 并添加以下文本。 

    > [!TIP]
    > 您可能需要单击代码中的 "刷新" 按钮才能查看新文件。
    
    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > **AZURE_STORAGE_CONNECTION_STRING**值是一个硬编码的环境变量, 用于存储 api 以查找访问密钥。 如果愿意, 您可以使用自己的名称, 但必须在您的`BlobService` node.js 应用程序中创建对象时提供该名称。

1. 保存该文件。

1. 现在, 我们需要获取存储帐户连接字符串, 并将其放入应用程序的配置中。 在云命令行管理程序中, 运行以下命令。

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --query connectionString \
        --name <name>
    ```

1. 复制从该命令返回的连接字符串, 减去引号, 并在**env**文件中`<value>`使用此连接字符串进行替换。

1. 保存该文件。

## <a name="add-support-to-read-an-environment-configuration-file"></a>添加对读取环境配置文件的支持

node.js 应用可以包括支持通过添加**dotenv**包从**env**文件中读取。

1. 在窗口的命令提示符部分, 使用`npm`将依赖项添加到**dotenv**包。

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a>添加代码以读取配置文件

至此, 我们已经添加了启用读取配置所需的库, 我们需要在应用程序中启用此功能。

1. 在编辑器中选择 " **.js** "。

1. 在文件的顶部, 存在`#!/usr/bin/env node`一行。 在该行下方, 添加一个`require`用于加载**dotenv**包的语句。 这将使在您的**env**文件中定义的环境变量可用于该程序。

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    // ... more code follows
    ```
::: zone-end

现在, 我们已将所有的连接好, 我们可以开始添加代码以使用我们的存储帐户。
