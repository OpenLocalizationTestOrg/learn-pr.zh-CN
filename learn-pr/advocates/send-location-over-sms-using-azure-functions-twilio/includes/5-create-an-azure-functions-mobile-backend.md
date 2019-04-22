此时, 应用正在努力获取用户的位置, 并准备将其发送到 Azure 功能。 在此单位中, 您将构建自己的 Azure 函数。

## <a name="create-an-azure-functions-project"></a>创建 Azure 函数项目

1. 右键单击该解决方案, `ImHere`然后选择 "*添加 > 新建项目 ...*"。

1. 从左侧的树中, 选择 " *Visual c # > 云*", 然后从中心的面板中选择 " *Azure 函数*"。

1. 将项目命名为 "ImHere", 然后单击 **"确定**"。

    !["添加新项目" 对话框](../media/5-add-new-functions-project.png)

1. 将显示 "**新建项目**配置" 对话框, 它可能会在左下角显示一个微调框, 同时加载更新的模板。 如果你看到此项, 请等待此操作完成加载, 然后, 如果更新的模板可用, 请单击将显示的 "**刷新**" 选项以确保你获取的是最新的函数模板。

    !["新建项目" 对话框, 用于加载最新模板](../media/5-loading-templates.png)

1. 在 "**新建项目**配置" 对话框中, 确保 "函数版本" 设置为 " *Azure 函数 v2 (.net Standard)* (**不**是_v1 (.net Framework)_")。 选择 " *Http 触发器*", 将存储帐户设置为 "*存储仿真程序*", 并将访问权限设置为 "*匿名*"。 然后单击 **"确定"**。

    !["Azure 函数项目配置" 对话框](../media/5-configure-trigger.png)

    将创建新项目, 并调用`Function1`一个默认函数。

> [!NOTE]
> 此函数是使用匿名访问创建的。 一旦发布到 Azure, 知道该 URL 的任何人都将能够调用此函数。 在实际方案中, 您可以使用某种形式的身份验证 (如[azure 应用服务身份验证](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview?azure-portal=true)或[azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c?azure-portal=true)) 保护这种情况。

## <a name="create-the-function"></a>创建函数

Azure 函数项目是通过调用`Function1`的单个 HTTP 触发器函数创建的。 http 触发器允许您使用 http 请求调用函数。 函数本身作为`Run` `Function1`类中的静态方法实现。

1. 将 "解决方案资源管理器" 中的文件从 "Function1.cs" 重命名为 "SendLocation.cs"。 当系统提示您重命名对 code 元素`Function1`的所有引用时, 请单击 **"是"**。

1. 将属性中的函数名称重命名为 "SendLocation"。

    ```cs
    [FunctionName("SendLocation")]
    ```

1. 删除函数的内容, 但将信息消息写入记录器的第一行除外。

    ```cs
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                             "get", "post",
                                                             Route = null)]HttpRequestMessage req,
                                                ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a>创建类以在移动应用程序和功能之间共享数据

将数据发送到 Azure 函数时, 它将以 JSON 的形式发送。 移动应用程序会将数据序列化为 json, 并且函数将从 JSON 反序列化。 若要使该数据在移动应用程序和功能之间保持一致, 请创建一个新项目, 其中包含一个用于保存位置和电话号码数据的类。 然后, 应用程序和功能将引用此项目。

1. 右键单击解决方案, 然后选择`ImHere` "*添加 > 新建项目 ...*", 在解决方案下创建一个新项目。

1. 从左侧的树中, 选择 " *Visual c # > .net Standard*", 然后从中央面板中选择 "类库 *(.net standard)* "。

1. 将项目命名为 "ImHere", 然后单击 **"确定**"。

    !["添加新项目" 对话框](../media/5-add-new-net-standard-project.png)

1. 删除自动生成的 "Class1.cs" 文件。

1. 右键单击该项目, `ImHere.Data`然后选择 "*添加 > 类 ...* " 以创建一个新类。

1. 将新类命名为 "PostData", 然后单击 **"确定**"。 将此新类标记`public`为。

1. 添加`double`纬度和经度的属性, 以及要发送到的`string[]`电话号码的属性。

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

1. 在和`ImHere`项目中添加对此项目的`ImHere.Functions`引用, 方法是右键单击该项目, 然后选择 "*添加->Reference ...*"。从左侧的树中选择 "*项目*", 然后选中 " *ImHere*" 旁边的框。

    ![配置项目引用](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a>读取发送给函数的数据

在 Azure 函数中, `req`参数包含所进行的 HTTP 请求, 此请求中的数据将是 JSON 序列化`PostData`对象。

1. 在`ImHere.Functions`项目`SendLocation`中打开该类。

1. 将 HTTP 请求的内容读入一个字符串, 然后将其反序列化为一个`PostData`对象, 并为该`ImHere.Data`命名空间添加 using 指令。

    ```cs
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    ```

1. 使用中的纬度和经度构造 Google Maps URL `PostData`。

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

1. 记录 URL。

    ```cs
    log.LogInformation($"URL created - {url}");
    ```

1. 返回200状态代码以显示函数已完成, 且未出错。

    ```cs
    return new OkResult();
    ```

完整的函数如下所示。

  ```cs 

    using System.IO;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using Microsoft.AspNetCore.Http;
    using ImHere.Data;
    using System.Threading.Tasks;
    using Microsoft.Extensions.Logging;
    using Newtonsoft.Json;

    namespace ImHere.Functions
    {
        public static class SendLocation
        {
            [FunctionName("SendLocation")]
            public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post",
                                                             Route = null)]HttpRequest req, ILogger log)
            {
                log.LogInformation("C# HTTP trigger function processed a request.");
                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
                string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
                log.LogInformation($"URL created - {url}");
                return new OkResult();
            }
        }
    }

 ```

## <a name="run-the-azure-functions-locally"></a>在本地运行 Azure 函数

可以使用本地存储帐户和本地 Azure 函数运行时在本地运行函数。 此本地运行时允许你先测试函数, 然后再将其部署到 Azure。

1. 在 "解决方案资源管理`ImHere.Functions`器" 中右键单击该项目, 然后选择 "*设为启动项目*"。

1. 从 "*调试*" 菜单中, 选择 "*启动 (不调试*)"。 本地 Azure 函数运行时将在控制台窗口中启动, 并启动您的功能, 并在上`localhost`的可用端口上进行侦听。 如果你看到请求防火墙访问的对话框, 则允许访问专用网络 (默认选项)。

    ![本地运行的 Azure 函数](../media/5-function-running-locally.png)

1. 记下函数所侦听的端口。 你将在下一个单元中需要此项来测试移动应用。 在上面的图像中, 函数在端口**7071**上进行侦听。

    ```sh
    Listening on http://localhost:7071/
    ```

1. 使函数保持运行状态, 以便您可以在下一个设备中测试移动应用。

## <a name="summary"></a>摘要

在此单元中, 您学习了如何在 Visual Studio 中创建 Azure function 项目, 添加了一个共享项目, 其中包含要在移动应用程序和函数之间共享的数据对象, 并了解如何创建函数的基本实现以反序列化数据传入。 此外, 还学习了如何在本地运行 Azure 函数。 在下一个设备中, 你将从移动应用程序调用 Azure 函数。