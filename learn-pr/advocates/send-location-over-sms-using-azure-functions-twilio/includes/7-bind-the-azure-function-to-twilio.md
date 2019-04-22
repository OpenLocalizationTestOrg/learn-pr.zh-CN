<span data-ttu-id="1d808-101">在这种情况下, 移动应用程序已完成, 它可以将用户的位置和电话号码列表发送到可反序列化数据的 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="1d808-101">At this point, the mobile app is complete and it can send the user's location and list of phone numbers to the Azure Functions that can deserialize the data.</span></span> <span data-ttu-id="1d808-102">在此单元中, 您需要将函数绑定到 Twilio 以发送短信消息。</span><span class="sxs-lookup"><span data-stu-id="1d808-102">In this unit, you'll bind your function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="1d808-103">azure 函数可连接到其他服务 (在 Azure 或第三方)。</span><span class="sxs-lookup"><span data-stu-id="1d808-103">Azure Functions can be connected to other services, either in Azure or third-party.</span></span> <span data-ttu-id="1d808-104">这些连接 (称为绑定) 存在于两个表单输入和输出绑定中。</span><span class="sxs-lookup"><span data-stu-id="1d808-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="1d808-105">输入绑定为您的函数和输出绑定提供数据, 从函数中获取数据并将其发送到其他服务。</span><span class="sxs-lookup"><span data-stu-id="1d808-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="1d808-106">您可以阅读[Azure 函数绑定文档](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true)中的绑定。</span><span class="sxs-lookup"><span data-stu-id="1d808-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true).</span></span>

<span data-ttu-id="1d808-107">在 Visual Studio 中创建的 Azure 函数的绑定是使用函数的参数定义的, 并使用属性修饰。</span><span class="sxs-lookup"><span data-stu-id="1d808-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-functions-to-twilio"></a><span data-ttu-id="1d808-108">将 Azure 函数绑定到 Twilio</span><span class="sxs-lookup"><span data-stu-id="1d808-108">Bind the Azure Functions to Twilio</span></span>

<span data-ttu-id="1d808-109">通过 Twilio 发送短信时, 需要使用帐户订阅 ID (SID) 和 Auth 令牌配置输出绑定。</span><span class="sxs-lookup"><span data-stu-id="1d808-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="1d808-110">如果本地 Azure 函数运行时仍从上一个单元运行, 请停止运行时。</span><span class="sxs-lookup"><span data-stu-id="1d808-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="1d808-111">将 "Twilio" NuGet 包添加到`ImHere.Functions`项目中。</span><span class="sxs-lookup"><span data-stu-id="1d808-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="1d808-112">此 NuGet 包包含绑定的相关类。</span><span class="sxs-lookup"><span data-stu-id="1d808-112">This NuGet package contains the relevant classes for the binding.</span></span>
<span data-ttu-id="1d808-113">确保您的函数中还安装了 Mcrosoft 和最新 .net SDK 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1d808-113">Make sure that you also have NuGet packages for Mcrosoft.Azure.WebJobs and latest .NET SDK installed in your function.</span></span> <span data-ttu-id="1d808-114">函数的 NuGet 部分应如下图所示:</span><span class="sxs-lookup"><span data-stu-id="1d808-114">The NuGet section for your function should look like the screenshot below:</span></span>

   ![显示函数 NuGet 依赖项的屏幕截图](../media/Imhere-function-dependencies.png)

1. <span data-ttu-id="1d808-116">打开 ImHere 项目中的 SendLocation 类以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="1d808-116">Open the SendLocation class in the ImHere.Functions project for editing.</span></span>

1. <span data-ttu-id="1d808-117">向类中添加 using `Twilio.Rest.Api.V2010.Account`指令。</span><span class="sxs-lookup"><span data-stu-id="1d808-117">Add a using directive for `Twilio.Rest.Api.V2010.Account` to the class.</span></span>

    ```cs
      using Twilio.Rest.Api.V2010.Account;
    
    ```

1. <span data-ttu-id="1d808-118">向静态`Run`方法中添加`messages`一个名`ICollector<CreateMessageOptions>`为 type 的新参数。</span><span class="sxs-lookup"><span data-stu-id="1d808-118">Add a new parameter called `messages` of type `ICollector<CreateMessageOptions>` to the static `Run` method.</span></span> 

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,"get", "post", Route = null)]HttpRequestMessage req, ICollector<CreateMessageOptions> messages, ILogger log)
    ```

1. <span data-ttu-id="1d808-119">使用`TwilioSms`属性修饰`messages`新参数, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="1d808-119">Decorate the new `messages` parameter with the `TwilioSms` attribute as follows:</span></span>

      ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",AuthTokenSetting = "TwilioAuthToken", From = "+1xxxxxxxxx")]ICollector<CreateMessageOptions> messages,
    ```
    <span data-ttu-id="1d808-120">此属性包含三个需要设置的参数:</span><span class="sxs-lookup"><span data-stu-id="1d808-120">This attribute has three parameters you need to set:</span></span>

    * <span data-ttu-id="1d808-121">**AccountSidSetting** -将此设置为`"TwilioAccountSid"`</span><span class="sxs-lookup"><span data-stu-id="1d808-121">**AccountSidSetting** - set this to `"TwilioAccountSid"`</span></span>
  
        <span data-ttu-id="1d808-122">这是您之前在模块中记录的 Twilio 帐户的 SID。</span><span class="sxs-lookup"><span data-stu-id="1d808-122">This is the SID for your Twilio account that you recorded earlier in the module.</span></span> <span data-ttu-id="1d808-123">此参数是将用于检索 SID 的函数应用程序设置中的值的名称, 而不是直接设置 sid。</span><span class="sxs-lookup"><span data-stu-id="1d808-123">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> <span data-ttu-id="1d808-124">稍后将定义此参数。</span><span class="sxs-lookup"><span data-stu-id="1d808-124">We will define this parameter later.</span></span>

    * <span data-ttu-id="1d808-125">**AuthTokenSetting** -将此设置为`"TwilioAuthToken"`</span><span class="sxs-lookup"><span data-stu-id="1d808-125">**AuthTokenSetting** - set this to `"TwilioAuthToken"`</span></span>

       <span data-ttu-id="1d808-126">这是您在模块前面记录的 Twilio 帐户的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="1d808-126">This is the Auth Token for your Twilio account that you recorded earlier in the module.</span></span> <span data-ttu-id="1d808-127">此参数是将用于检索身份验证令牌的函数应用程序设置中的值的名称, 而不是直接设置身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="1d808-127">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> <span data-ttu-id="1d808-128">稍后将定义此参数。</span><span class="sxs-lookup"><span data-stu-id="1d808-128">We will define this parameter later.</span></span>

    * <span data-ttu-id="1d808-129">**从**-将此值设置为您之前在模块中记录的 Twilio 活动电话号码。</span><span class="sxs-lookup"><span data-stu-id="1d808-129">**From** - set this to your Twilio active phone number that you recorded earlier in the module.</span></span>

        <span data-ttu-id="1d808-130">SMS 消息将来自国际格式的 Twilio 电话号码 (\<+ 国家/地区代码\>\<电话号码\>, 例如 "+ 1555123456")。</span><span class="sxs-lookup"><span data-stu-id="1d808-130">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1d808-131">请务必删除电话号码中的所有空格。</span><span class="sxs-lookup"><span data-stu-id="1d808-131">Make sure to remove all spaces from the phone number.</span></span>

## <a name="define-twiliosms-variables-in-local-settings"></a><span data-ttu-id="1d808-132">在本地设置中定义 TwilioSMS 变量</span><span class="sxs-lookup"><span data-stu-id="1d808-132">Define TwilioSMS variables in local settings</span></span>

<span data-ttu-id="1d808-133">可以在`local.settings.json`文件内本地配置函数应用设置。</span><span class="sxs-lookup"><span data-stu-id="1d808-133">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="1d808-134">使用传递给该`TwilioSMS`属性的设置名称, 将您的 Twilio 帐户 SID 和 Auth 令牌添加到此 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="1d808-134">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

1. <span data-ttu-id="1d808-135">在 " `local.settings.json` ImHere" 项目中打开文件, 并将现有代码替换为以下内容:</span><span class="sxs-lookup"><span data-stu-id="1d808-135">Open the `local.settings.json` file in the ImHere.Functions project and replace the existing code with the following:</span></span>

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

1. <span data-ttu-id="1d808-136">将\<您的\> SID \<和身份验证\>令牌替换为 Twilio 仪表板中的值。</span><span class="sxs-lookup"><span data-stu-id="1d808-136">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d808-137">这些本地设置将仅用于本地运行。</span><span class="sxs-lookup"><span data-stu-id="1d808-137">These local settings will be only for running locally.</span></span> <span data-ttu-id="1d808-138">在生产应用程序中, 这些值将是本地开发或测试帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="1d808-138">In a production app, these values would be your local development or test account credentials.</span></span> <span data-ttu-id="1d808-139">azure 函数部署到 azure 后, 你将能够配置生产值。</span><span class="sxs-lookup"><span data-stu-id="1d808-139">Once the Azure Functions has been deployed to Azure, you'll be able to configure the production values.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1d808-140">如果将代码签入到源代码控制中, 则也会签入这些本地应用程序设置值, 因此, 如果您的代码是任何窗体中的打开源代码或公共的, 则请注意不要签入这些文件中的任何实际值。</span><span class="sxs-lookup"><span data-stu-id="1d808-140">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="1d808-141">创建 SMS 消息</span><span class="sxs-lookup"><span data-stu-id="1d808-141">Create the SMS messages</span></span>

<span data-ttu-id="1d808-142">`ICollector<CreateMessageOptions>`参数是`CreateMessageOptions`实例的集合, 用于收集要发送的 SMS 消息。</span><span class="sxs-lookup"><span data-stu-id="1d808-142">The `ICollector<CreateMessageOptions>` parameter is a collection of `CreateMessageOptions` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="1d808-143">函数完成运行后, 添加到此集合中`CreateMessageOptions`的任何实例都将传递给 Twilio, 并用于创建要发送给相关收件人的邮件。</span><span class="sxs-lookup"><span data-stu-id="1d808-143">After the function has finished running, any instances of `CreateMessageOptions` added to this collection are passed to Twilio and used to create messages to be sent to the relevant recipients.</span></span>

1. <span data-ttu-id="1d808-144">在 " `SendLocation' class` `Twilio.Types`向类添加 using 指令" 中。</span><span class="sxs-lookup"><span data-stu-id="1d808-144">In the `SendLocation' class` add a using directive for `Twilio.Types` to the class.</span></span>

    ```cs
      using Twilio.Types;
    
    ```

1. <span data-ttu-id="1d808-145">在`SendLocation`函数中, 添加代码以循环访问中的电话号码`PostData` , 并为每个电话号码创建一条短信。</span><span class="sxs-lookup"><span data-stu-id="1d808-145">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

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

    <span data-ttu-id="1d808-146">邮件需要要发送的电话号码和包含从用户位置创建的 Google Maps URL 的正文。</span><span class="sxs-lookup"><span data-stu-id="1d808-146">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

1. <span data-ttu-id="1d808-147">记录每封邮件, 然后将其添加到`messages`集合中。</span><span class="sxs-lookup"><span data-stu-id="1d808-147">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="1d808-148">完整`SendLocation`的方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="1d808-148">The complete `SendLocation` method is shown below.</span></span> <span data-ttu-id="1d808-149">您的活动电话号码将替换`From`参数中的占位符。</span><span class="sxs-lookup"><span data-stu-id="1d808-149">Your active phone number would replace the placeholder in the `From` parameter.</span></span>

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

## <a name="test-it-out"></a><span data-ttu-id="1d808-150">测试</span><span class="sxs-lookup"><span data-stu-id="1d808-150">Test it out</span></span>

1. <span data-ttu-id="1d808-151">将`ImHere.Functions`应用程序设置为启动项目, 并启动它而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="1d808-151">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

1. <span data-ttu-id="1d808-152">将`ImHere.UWP`应用程序设置为启动项目并运行它。</span><span class="sxs-lookup"><span data-stu-id="1d808-152">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

1. <span data-ttu-id="1d808-153">在 Xamarin. Forms 应用中, 输入国际格式\<的电话\>\<号码 (\>+ 国家/地区代码电话号码)。</span><span class="sxs-lookup"><span data-stu-id="1d808-153">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="1d808-154">Twilio 试用帐户可以仅将邮件发送到已验证的电话号码, 因此现在, 只有在您升级到付费帐户或验证其他号码时, 才可以自行发送邮件。</span><span class="sxs-lookup"><span data-stu-id="1d808-154">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

1. <span data-ttu-id="1d808-155">单击 "**发送位置**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="1d808-155">Click the **Send Location** button.</span></span> <span data-ttu-id="1d808-156">如果短信发送成功, 您将在 Xamarin 应用程序中看到一条消息 "已成功发送位置"。</span><span class="sxs-lookup"><span data-stu-id="1d808-156">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying, "Location sent successfully".</span></span>

    ![显示 "已发送" 位置的 Xamarin 应用程序](../media/7-ui-location-sent.png)

1. <span data-ttu-id="1d808-158">在您的函数的控制台日志中, 您将看到正在创建和发送的消息。</span><span class="sxs-lookup"><span data-stu-id="1d808-158">In the console logs for your function, you'll see the message being created and sent.</span></span> <span data-ttu-id="1d808-159">如果出现任何错误 (例如, 数字格式错误), 则会在此处注销。</span><span class="sxs-lookup"><span data-stu-id="1d808-159">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![显示已发送邮件的 Azure 函数控制台](../media/7-function-message-sent.png)

1. <span data-ttu-id="1d808-161">检查你的电话中是否有消息。</span><span class="sxs-lookup"><span data-stu-id="1d808-161">Check your phone for a message.</span></span> <span data-ttu-id="1d808-162">按照邮件中的链接查看您的位置。</span><span class="sxs-lookup"><span data-stu-id="1d808-162">Follow the link in the message to see your location.</span></span>

    ![在移动电话上收到的短信消息](../media/7-message-received.png)

    > [!TIP]
    > <span data-ttu-id="1d808-164">你将看到的位置是应用运行的位置, 因此将接近运行 VM 的数据中心。</span><span class="sxs-lookup"><span data-stu-id="1d808-164">The location you'll see is the location where the app is running, so will be near to the data center that the VM is running from.</span></span> <span data-ttu-id="1d808-165">如果此应用在本地设备上运行, 则会显示您的位置。</span><span class="sxs-lookup"><span data-stu-id="1d808-165">If this app was running on your local device then it would show your location.</span></span>

## <a name="summary"></a><span data-ttu-id="1d808-166">摘要</span><span class="sxs-lookup"><span data-stu-id="1d808-166">Summary</span></span>

<span data-ttu-id="1d808-167">在此单元中, 您学习了如何为 Azure 函数创建 Twilio 绑定, 并向在本地运行的函数发送带有用户位置的 SMS 消息。</span><span class="sxs-lookup"><span data-stu-id="1d808-167">In this unit, you learned how to create a Twilio binding for the Azure Functions and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="1d808-168">在下一个设备中, 将函数发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1d808-168">In the next unit, you publish the function to Azure.</span></span>
