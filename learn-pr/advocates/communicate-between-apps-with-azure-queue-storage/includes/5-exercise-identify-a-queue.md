让我们创建一个客户端应用程序以使用队列。 然后, 将我们的连接字符串添加到代码中。

> [!NOTE]
> 如果已安装 .net Core, 或者直接在云命令行管理器环境中, 则可以在本地计算机上创建客户端应用程序。

## <a name="create-the-application"></a>创建应用程序

我们将创建可在 Linux、macOS 或 Windows 上运行的 .net Core 应用程序。 让我们将其命名为**QueueApp**。 为简单起见, 我们将使用单个应用程序, 该应用将通过我们的队列发送和接收邮件。

1. 使用`dotnet new`命令创建名称为 " **QueueApp**" 的新控制台应用程序。 您可以将命令键入到右侧的云命令行管理程序中, 或者如果您正在本地运行, 请在终端/控制台窗口中键入命令。 此命令将创建一个包含单个源文件的简单应用程序`Program.cs`:。

    ```azurecli
    dotnet new console -n QueueApp
    ```

1. 切换到新创建`QueueApp`的文件夹, 并生成应用程序以验证是否一切正常。

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a>获取您的连接字符串

请记住, 您的连接字符串在您的存储帐户的 "Azure 门户**设置 > 访问密钥**" 部分中可用。

您还可以通过 Azure CLI 或 PowerShell 工具进行检索。 让我们使用 Azure CLI 命令。 请记住, 将`<name>`替换为您创建的存储帐户的特定名称。 如果需要提醒`az storage account list` , 可以使用。

```azurecli
az storage account show-connection-string --name <name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

此命令将使用您的连接字符串返回一个 JSON 块。 它将包括存储帐户名称和帐户密钥:

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a>将连接字符串添加到应用程序

最后, 让我们将连接字符串添加到我们的应用程序中, 以便它可以访问存储帐户。

> [!WARNING]
> 为简单起见, 您将在**Program.cs**文件中放置连接字符串。 在生产应用程序中, 应将其存储在安全位置。 对于服务器端使用, 我们建议使用 Azure Key Vault。

1. 在`code .` "终端" 中键入以打开 "联机代码编辑器"。 或者, 如果您自己处理自己的工作, 则可以使用您选择的 IDE。 建议使用 Visual Studio Code, 这是一种优秀的跨平台 IDE。

1. 打开项目`Program.cs`中的源文件。

1. 在`Program`类中, 添加一个`const string`值以保存连接字符串。 您只需要此值 (它以文本**DefaultEndpointsProtocol**开头)。

1. 保存该文件。 您可以单击椭圆 "..."在云编辑器的右下角, 或使用加速器键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> , macOS 上的<kbd>Cmd + s</kbd> )。

代码应类似于以下内容 (字符串值对您的帐户是唯一的)。

```csharp
...
namespace QueueApp
{
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https; ...";
        
        ...
    }
}
```

至此, 我们已提供了此初学者项目设置, 我们来看看如何在代码中使用队列。 所有这些都是从_邮件_开始。