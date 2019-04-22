在这种情况下, 移动应用程序已完成, 它可以将用户的位置和电话号码列表发送到可反序列化数据的 Azure 函数。 在此单元中, 您需要将函数绑定到 Twilio 以发送短信消息。

azure 函数可连接到其他服务 (在 Azure 或第三方)。 这些连接 (称为绑定) 存在于两个表单输入和输出绑定中。 输入绑定为您的函数和输出绑定提供数据, 从函数中获取数据并将其发送到其他服务。 您可以阅读[Azure 函数绑定文档](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true)中的绑定。

在 Visual Studio 中创建的 Azure 函数的绑定是使用函数的参数定义的, 并使用属性修饰。

## <a name="bind-the-azure-functions-to-twilio"></a>将 Azure 函数绑定到 Twilio

通过 Twilio 发送短信时, 需要使用帐户订阅 ID (SID) 和 Auth 令牌配置输出绑定。

1. 如果本地 Azure 函数运行时仍从上一个单元运行, 请停止运行时。

1. 将 "Twilio" NuGet 包添加到`ImHere.Functions`项目中。 此 NuGet 包包含绑定的相关类。
确保您的函数中还安装了 Mcrosoft 和最新 .net SDK 的 NuGet 包。 函数的 NuGet 部分应如下图所示:

   ![显示函数 NuGet 依赖项的屏幕截图](../media/Imhere-function-dependencies.png)

1. 打开 ImHere 项目中的 SendLocation 类以进行编辑。

1. 向类中添加 using `Twilio.Rest.Api.V2010.Account`指令。

    ```cs
      using Twilio.Rest.Api.V2010.Account;
    
    ```

1. 向静态`Run`方法中添加`messages`一个名`ICollector<CreateMessageOptions>`为 type 的新参数。 

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,"get", "post", Route = null)]HttpRequestMessage req, ICollector<CreateMessageOptions> messages, ILogger log)
    ```

1. 使用`TwilioSms`属性修饰`messages`新参数, 如下所示:

      ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",AuthTokenSetting = "TwilioAuthToken", From = "+1xxxxxxxxx")]ICollector<CreateMessageOptions> messages,
    ```
    此属性包含三个需要设置的参数:

    * **AccountSidSetting** -将此设置为`"TwilioAccountSid"`
  
        这是您之前在模块中记录的 Twilio 帐户的 SID。 此参数是将用于检索 SID 的函数应用程序设置中的值的名称, 而不是直接设置 sid。 稍后将定义此参数。

    * **AuthTokenSetting** -将此设置为`"TwilioAuthToken"`

       这是您在模块前面记录的 Twilio 帐户的身份验证令牌。 此参数是将用于检索身份验证令牌的函数应用程序设置中的值的名称, 而不是直接设置身份验证令牌。 稍后将定义此参数。

    * **从**-将此值设置为您之前在模块中记录的 Twilio 活动电话号码。

        SMS 消息将来自国际格式的 Twilio 电话号码 (\<+ 国家/地区代码\>\<电话号码\>, 例如 "+ 1555123456")。

    > [!IMPORTANT]
    > 请务必删除电话号码中的所有空格。

## <a name="define-twiliosms-variables-in-local-settings"></a>在本地设置中定义 TwilioSMS 变量

可以在`local.settings.json`文件内本地配置函数应用设置。 使用传递给该`TwilioSMS`属性的设置名称, 将您的 Twilio 帐户 SID 和 Auth 令牌添加到此 JSON 文件。

1. 在 " `local.settings.json` ImHere" 项目中打开文件, 并将现有代码替换为以下内容:

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "FUNCTIONS_WORKER_RUNTIME": "dotnet",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

1. 将\<您的\> SID \<和身份验证\>令牌替换为 Twilio 仪表板中的值。

    > [!NOTE]
    > 这些本地设置将仅用于本地运行。 在生产应用程序中, 这些值将是本地开发或测试帐户凭据。 azure 函数部署到 azure 后, 你将能够配置生产值。

    > [!NOTE]
    > 如果将代码签入到源代码控制中, 则也会签入这些本地应用程序设置值, 因此, 如果您的代码是任何窗体中的打开源代码或公共的, 则请注意不要签入这些文件中的任何实际值。

## <a name="create-the-sms-messages"></a>创建 SMS 消息

`ICollector<CreateMessageOptions>`参数是`CreateMessageOptions`实例的集合, 用于收集要发送的 SMS 消息。 函数完成运行后, 添加到此集合中`CreateMessageOptions`的任何实例都将传递给 Twilio, 并用于创建要发送给相关收件人的邮件。

1. 在 " `SendLocation' class` `Twilio.Types`向类添加 using 指令" 中。

    ```cs
      using Twilio.Types;
    
    ```

1. 在`SendLocation`函数中, 添加代码以循环访问中的电话号码`PostData` , 并为每个电话号码创建一条短信。

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        PhoneNumber number = new PhoneNumber(toNo);
        CreateMessageOptions message = new CreateMessageOptions(number)
        {
            Body = $"I'm here! {url}"
        };
    }
    ```

    邮件需要要发送的电话号码和包含从用户位置创建的 Google Maps URL 的正文。

1. 记录每封邮件, 然后将其添加到`messages`集合中。

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

完整`SendLocation`的方法如下所示。 您的活动电话号码将替换`From`参数中的占位符。

```cs
[FunctionName("SendLocation")]
public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                         "get", "post",
                                                         Route = null)]HttpRequest req,
                                            [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                       AuthTokenSetting = "TwilioAuthToken",
                                                       From = "+1xxxxxxxxx")] ICollector<CreateMessageOptions> messages,
                                            ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.LogInformation($"URL created - {url}");

    foreach (string toNo in data.ToNumbers)
    {
        PhoneNumber number = new PhoneNumber(toNo);
        CreateMessageOptions message = new CreateMessageOptions(number)
        {
            Body = $"I'm here! {url}"
        };
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }

    return new OkResult();
}
```

## <a name="test-it-out"></a>测试

1. 将`ImHere.Functions`应用程序设置为启动项目, 并启动它而不进行调试。

1. 将`ImHere.UWP`应用程序设置为启动项目并运行它。

1. 在 Xamarin. Forms 应用中, 输入国际格式\<的电话\>\<号码 (\>+ 国家/地区代码电话号码)。 Twilio 试用帐户可以仅将邮件发送到已验证的电话号码, 因此现在, 只有在您升级到付费帐户或验证其他号码时, 才可以自行发送邮件。

1. 单击 "**发送位置**" 按钮。 如果短信发送成功, 您将在 Xamarin 应用程序中看到一条消息 "已成功发送位置"。

    ![显示 "已发送" 位置的 Xamarin 应用程序](../media/7-ui-location-sent.png)

1. 在您的函数的控制台日志中, 您将看到正在创建和发送的消息。 如果出现任何错误 (例如, 数字格式错误), 则会在此处注销。

    ![显示已发送邮件的 Azure 函数控制台](../media/7-function-message-sent.png)

1. 检查你的电话中是否有消息。 按照邮件中的链接查看您的位置。

    ![在移动电话上收到的短信消息](../media/7-message-received.png)

    > [!TIP]
    > 你将看到的位置是应用运行的位置, 因此将接近运行 VM 的数据中心。 如果此应用在本地设备上运行, 则会显示您的位置。

## <a name="summary"></a>摘要

在此单元中, 您学习了如何为 Azure 函数创建 Twilio 绑定, 并向在本地运行的函数发送带有用户位置的 SMS 消息。 在下一个设备中, 将函数发布到 Azure。
