<span data-ttu-id="e575a-101">接下来, 我们将继续使用我们的齿轮驱动器示例, 并添加温度服务的逻辑。</span><span class="sxs-lookup"><span data-stu-id="e575a-101">Let's continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="e575a-102">具体来说, 我们将从 HTTP 请求中接收数据。</span><span class="sxs-lookup"><span data-stu-id="e575a-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="e575a-103">函数要求</span><span class="sxs-lookup"><span data-stu-id="e575a-103">Function requirements</span></span>

<span data-ttu-id="e575a-104">首先, 我们需要为逻辑定义一些要求:</span><span class="sxs-lookup"><span data-stu-id="e575a-104">First, we need to define some requirements for our logic:</span></span>

- <span data-ttu-id="e575a-105">0-25 之间的温度应标记为 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e575a-105">Temperatures between 0-25 should be flagged as **OK**.</span></span>
- <span data-ttu-id="e575a-106">应将26-50 之间的温度标记为**警告**。</span><span class="sxs-lookup"><span data-stu-id="e575a-106">Temperatures between 26-50 should be flagged as **CAUTION**.</span></span>
- <span data-ttu-id="e575a-107">应将高于50的温度标记为**危险**。</span><span class="sxs-lookup"><span data-stu-id="e575a-107">Temperatures above 50 should be flagged as **DANGER**.</span></span>

## <a name="add-a-function-to-our-function-app"></a><span data-ttu-id="e575a-108">向我们的函数应用程序添加函数</span><span class="sxs-lookup"><span data-stu-id="e575a-108">Add a function to our function app</span></span>

<span data-ttu-id="e575a-109">如前面的单元中所述, Azure 提供可帮助您开始构建功能的模板。</span><span class="sxs-lookup"><span data-stu-id="e575a-109">As we discussed in the preceding unit, Azure provides templates that help you get started building functions.</span></span> <span data-ttu-id="e575a-110">在此单元中, 我们将使用`HttpTrigger`模板来实施温度服务。</span><span class="sxs-lookup"><span data-stu-id="e575a-110">In this unit, we'll use the `HttpTrigger` template to implement the temperature service.</span></span>

1. <span data-ttu-id="e575a-111">登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="e575a-111">Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).</span></span>

1. <span data-ttu-id="e575a-112">通过选择左侧菜单中的 "**所有资源**", 然后选择 "**<rgn>[沙盒资源组名称]</rgn>**", 从第一个练习中选择资源组。</span><span class="sxs-lookup"><span data-stu-id="e575a-112">Select the resource group from the first exercise by choosing **All resources** in the left-hand menu, and then selecting "**<rgn>[sandbox resource group name]</rgn>**".</span></span>

1. <span data-ttu-id="e575a-113">然后, 将显示组的资源。</span><span class="sxs-lookup"><span data-stu-id="e575a-113">The resources for the group will then be displayed.</span></span> <span data-ttu-id="e575a-114">单击您在上一练习中创建的函数应用程序的名称, 方法是选择 "自动**扶梯函数-xxxxxxx** " 项 (也由闪电形函数图标指示)。</span><span class="sxs-lookup"><span data-stu-id="e575a-114">Click the name of the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt Function icon).</span></span>

    ![显示 "所有资源" 边栏已突出显示的 Azure 门户屏幕截图以及我们创建的自动扶梯功能应用程序的屏幕截图。](../media/5-access-function-app.png)

1. <span data-ttu-id="e575a-116">选择 "函数"**+** 旁边的 "添加\*\*\*\*" () 按钮。</span><span class="sxs-lookup"><span data-stu-id="e575a-116">Select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="e575a-117">此操作将启动函数创建过程。</span><span class="sxs-lookup"><span data-stu-id="e575a-117">This action starts the function creation process.</span></span>

1. <span data-ttu-id="e575a-118">在 "**适用于 JavaScript 的 Azure 函数-入门**" 页上, 选择 "**在门户中**", 然后选择 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="e575a-118">On the **Azure Functions for JavaScript - getting started** page, select **In-portal** and then select **continue**.</span></span>

1. <span data-ttu-id="e575a-119">在 "**创建函数**" 步骤中, 选择 "**更多模板 ...** ", 然后选择 "完成", 然后单击 "**查看模板**"。</span><span class="sxs-lookup"><span data-stu-id="e575a-119">In the **Create a function** step, select **More templates...** and then select **Finish and view templates**.</span></span>

1. <span data-ttu-id="e575a-120">在可用于此函数应用程序的所有模板的列表中, 选择 " **Http 触发器**"。</span><span class="sxs-lookup"><span data-stu-id="e575a-120">In the list of all templates available to this function app, select **Http trigger** .</span></span>

1. <span data-ttu-id="e575a-121">在出现的 "**新建函数**" 对话框的 "名称" 字段中输入**DriveGearTemperatureService** 。</span><span class="sxs-lookup"><span data-stu-id="e575a-121">Enter **DriveGearTemperatureService** in the name field of the **New Function** dialog that appears.</span></span> <span data-ttu-id="e575a-122">将授权级别保留为 "函数", 然后按 "**创建**" 按钮以创建函数。</span><span class="sxs-lookup"><span data-stu-id="e575a-122">Leave the Authorization level as "Function" and press the **Create** button to create the function.</span></span>

1. <span data-ttu-id="e575a-123">函数创建完成后, 代码编辑器将打开, 并附带*索引 .js*代码文件的内容。</span><span class="sxs-lookup"><span data-stu-id="e575a-123">When your function creation completes, the code editor opens with the contents of the *index.js* code file.</span></span> <span data-ttu-id="e575a-124">下面的代码片段中列出了为我们生成的模板所生成的默认代码。</span><span class="sxs-lookup"><span data-stu-id="e575a-124">The default code that the template generated for us is listed in the following snippet.</span></span>

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');
    
        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

    <span data-ttu-id="e575a-125">我们的函数需要通过 HTTP 请求查询字符串或作为请求正文的一部分传入的名称。</span><span class="sxs-lookup"><span data-stu-id="e575a-125">Our function expects a name to be passed in either through the HTTP request query string or as part of the request body.</span></span> <span data-ttu-id="e575a-126">函数通过返回邮件**Hello, {name}** 回显在请求中发送的名称进行响应。</span><span class="sxs-lookup"><span data-stu-id="e575a-126">The function responds by returning the message  **Hello, {name}**, echoing back the name that was sent in the request.</span></span>

    <span data-ttu-id="e575a-127">在 "源" 视图的右侧, 您将找到两个选项卡。</span><span class="sxs-lookup"><span data-stu-id="e575a-127">On the right-hand side of the source view, you'll find two tabs.</span></span> <span data-ttu-id="e575a-128">"**查看文件**" 选项卡列出了函数的代码和配置文件。</span><span class="sxs-lookup"><span data-stu-id="e575a-128">The **View files** tab lists the code and config file for your function.</span></span>  <span data-ttu-id="e575a-129">选择**函数 json**以查看函数的配置, 其外观应类似于以下内容:</span><span class="sxs-lookup"><span data-stu-id="e575a-129">Select **function.json** to view the configuration of the function, which should look like the following:</span></span>

    ```javascript
    {
        "disabled": false,
        "bindings": [
        {
            "authLevel": "function",
            "type": "httpTrigger",
            "direction": "in",
            "name": "req"
        },
        {
            "type": "http",
            "direction": "out",
            "name": "res"
        }
        ]
    }
    ```

    <span data-ttu-id="e575a-130">此配置声明函数在收到 HTTP 请求时运行。</span><span class="sxs-lookup"><span data-stu-id="e575a-130">This configuration declares that the function runs when it receives an HTTP request.</span></span> <span data-ttu-id="e575a-131">输出绑定声明响应将作为 HTTP 响应发送。</span><span class="sxs-lookup"><span data-stu-id="e575a-131">The output binding declares that the response will be sent as an HTTP response.</span></span>    

## <a name="test-the-function"></a><span data-ttu-id="e575a-132">测试函数</span><span class="sxs-lookup"><span data-stu-id="e575a-132">Test the function</span></span>

> [!TIP]
> <span data-ttu-id="e575a-133">"**卷曲**" 是一种命令行工具, 可用于发送或接收文件。</span><span class="sxs-lookup"><span data-stu-id="e575a-133">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="e575a-134">它包含在 Linux、macOS 和 Windows 10 中, 可以为大多数其他操作系统下载。</span><span class="sxs-lookup"><span data-stu-id="e575a-134">It's included with Linux, macOS, and Windows 10, and can be downloaded for most other operating systems.</span></span> <span data-ttu-id="e575a-135">卷支持多种协议, 如 HTTP、HTTPS、FTP、FTPS、SFTP、LDAP、TELNET、SMTP、POP3 等。有关详细信息, 请参阅以下链接:</span><span class="sxs-lookup"><span data-stu-id="e575a-135">cURL supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3, etc. For more information, refer to the links below:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

<span data-ttu-id="e575a-136">若要测试函数, 可以在命令行中使用曲线向函数 URL 发送 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="e575a-136">To test the function, you can send an HTTP request to the function URL using cURL on the command line.</span></span> <span data-ttu-id="e575a-137">若要查找函数的终结点 URL, 请返回到您的函数代码并选择**Get 函数 URL**链接, 如以下屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="e575a-137">To find the endpoint URL of the function, return to your function code and select the **Get function URL** link, as shown in the following screenshot.</span></span> <span data-ttu-id="e575a-138">临时保存此链接。</span><span class="sxs-lookup"><span data-stu-id="e575a-138">Save this link temporarily.</span></span>

![显示 "函数编辑器" 的 Azure 门户屏幕截图, 其中突出显示了 Get 函数 URL 按钮。](../media/5-get-function-url.png)

### <a name="securing-http-triggers"></a><span data-ttu-id="e575a-140">保护 HTTP 触发器</span><span class="sxs-lookup"><span data-stu-id="e575a-140">Securing HTTP triggers</span></span>

<span data-ttu-id="e575a-141">通过 HTTP 触发器, 可以通过要求在每个请求上提供密钥来使用 API 密钥阻止未知的调用方。</span><span class="sxs-lookup"><span data-stu-id="e575a-141">HTTP triggers let you use API keys to block unknown callers by requiring the key to be present on each request.</span></span> <span data-ttu-id="e575a-142">创建函数时, 请选择 "_授权级别_"。</span><span class="sxs-lookup"><span data-stu-id="e575a-142">When you create a function, you select the _authorization level_.</span></span> <span data-ttu-id="e575a-143">默认情况下, 它设置为 "函数", 它需要一个特定于函数的 API 键, 但也可以将其设置为 "Admin" 以使用全局 "主" 键, 或 "匿名" 以指示无需任何键。</span><span class="sxs-lookup"><span data-stu-id="e575a-143">By default, it's set to "Function", which requires a function-specific API key, but it can also be set to "Admin" to use a global "master" key, or "Anonymous" to indicate that no key is required.</span></span> <span data-ttu-id="e575a-144">您还可以在创建后通过函数属性更改授权级别。</span><span class="sxs-lookup"><span data-stu-id="e575a-144">You can also change the authorization level through the function properties after creation.</span></span>

<span data-ttu-id="e575a-145">由于我们在创建此函数时指定了 "函数", 因此我们需要在发送 HTTP 请求时提供密钥。</span><span class="sxs-lookup"><span data-stu-id="e575a-145">Since we specified "Function" when we created this function, we will need to supply the key when we send the HTTP request.</span></span> <span data-ttu-id="e575a-146">您可以将其作为名为的查询字符串`code`参数或作为名`x-functions-key`为的 HTTP 标头 (首选) 发送。</span><span class="sxs-lookup"><span data-stu-id="e575a-146">You can send it as a query string parameter named `code`, or as an HTTP header (preferred) named `x-functions-key`.</span></span>

<span data-ttu-id="e575a-147">扩展函数时, 可以在 "**管理**" 部分找到函数和主密钥。</span><span class="sxs-lookup"><span data-stu-id="e575a-147">The function and master keys are found in the **Manage** section when the function is expanded.</span></span> <span data-ttu-id="e575a-148">默认情况下, 它们是隐藏的, 您需要显示它们。</span><span class="sxs-lookup"><span data-stu-id="e575a-148">By default, they are hidden, and you need to display them.</span></span>

1. <span data-ttu-id="e575a-149">展开您的函数并选择 "**管理**" 部分, 显示默认的功能键, 并将其复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="e575a-149">Expand your function and select the **Manage** section, show the default Function Key, and copy it to the clipboard.</span></span>

    ![显示功能管理刀片并突出显示的功能键的 Azure 门户屏幕截图。](../media/5-get-function-key.png)

1. <span data-ttu-id="e575a-151">接下来, 从安装了**卷曲**工具的命令行中, 使用函数的 URL 和功能键格式化卷曲命令。</span><span class="sxs-lookup"><span data-stu-id="e575a-151">Next, from the command line where you installed the **cURL** tool, format a cURL command with the URL for your function, and the Function key.</span></span>

    - <span data-ttu-id="e575a-152">使用`POST`请求。</span><span class="sxs-lookup"><span data-stu-id="e575a-152">Use a `POST` request.</span></span>
    - <span data-ttu-id="e575a-153">添加一个`Content-Type`类型`application/json`的标头值。</span><span class="sxs-lookup"><span data-stu-id="e575a-153">Add a `Content-Type` header value of type `application/json`.</span></span>
    - <span data-ttu-id="e575a-154">请确保将以下 URL 替换为您自己的 URL。</span><span class="sxs-lookup"><span data-stu-id="e575a-154">Make sure to replace the URL below with your own.</span></span>
    - <span data-ttu-id="e575a-155">将 Function 键作为标头值`x-functions-key`传递。</span><span class="sxs-lookup"><span data-stu-id="e575a-155">Pass the Function Key as the header value `x-functions-key`.</span></span>

    ```bash
    curl --header "Content-Type: application/json" --header "x-functions-key: <your-function-key>" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
    ```

<span data-ttu-id="e575a-156">函数将使用文本`"Hello Azure Function"`进行回复。</span><span class="sxs-lookup"><span data-stu-id="e575a-156">The function will respond back with the text `"Hello Azure Function"`.</span></span>

> [!CAUTION]
> <span data-ttu-id="e575a-157">如果您在 Windows 上, 请从`cURL`命令提示符运行。</span><span class="sxs-lookup"><span data-stu-id="e575a-157">If you are on Windows, please run  `cURL` from the command prompt.</span></span> <span data-ttu-id="e575a-158">PowerShell 有*卷曲*的命令, 但它是 WebRequest 的别名, 与不同`cURL`。</span><span class="sxs-lookup"><span data-stu-id="e575a-158">PowerShell has a *curl* command, but it's an alias for Invoke-WebRequest and is not the same as `cURL`.</span></span>

> [!NOTE]
> <span data-ttu-id="e575a-159">您还可以使用所选函数一侧的 "**测试**" 选项卡来测试单个函数的节, 尽管无法验证该功能键系统是否正常工作, 但此处不需要它。</span><span class="sxs-lookup"><span data-stu-id="e575a-159">You can also test from an individual function's section with the **Test** tab on the side of a selected function, though you won't be able to verify the function key system is working, as it is not required here.</span></span> <span data-ttu-id="e575a-160">在测试界面中添加适当的标头和参数值, 然后单击 "**运行**" 按钮以查看测试输出。</span><span class="sxs-lookup"><span data-stu-id="e575a-160">Add the appropriate header and parameter values in the Test interface and click the **Run** button to see the test output.</span></span>

## <a name="add-business-logic-to-the-function"></a><span data-ttu-id="e575a-161">向函数中添加业务逻辑</span><span class="sxs-lookup"><span data-stu-id="e575a-161">Add business logic to the function</span></span>

<span data-ttu-id="e575a-162">接下来, 让我们向检查其收到的温度读数的函数添加逻辑, 并为每个函数设置状态。</span><span class="sxs-lookup"><span data-stu-id="e575a-162">Next, let's add the logic to the function that checks temperature readings that it receives and sets a status for each.</span></span>

<span data-ttu-id="e575a-163">我们的函数需要一组温度读数。</span><span class="sxs-lookup"><span data-stu-id="e575a-163">Our function is expecting an array of temperature readings.</span></span> <span data-ttu-id="e575a-164">下面的 JSON 代码片段是我们将发送给我们的函数的请求正文的示例。</span><span class="sxs-lookup"><span data-stu-id="e575a-164">The following JSON snippet is an example of the request body that we'll send to our function.</span></span> <span data-ttu-id="e575a-165">每`reading`个条目都有 ID、时间戳和温度。</span><span class="sxs-lookup"><span data-stu-id="e575a-165">Each `reading` entry has an ID, timestamp, and temperature.</span></span>

```json
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

<span data-ttu-id="e575a-166">接下来, 我们将使用实现业务逻辑的以下代码替换函数中的默认代码。</span><span class="sxs-lookup"><span data-stu-id="e575a-166">Next, we'll replace the default code in our function with the following code that implements our business logic.</span></span>

1. <span data-ttu-id="e575a-167">打开一个**索引 .js**文件, 并将其替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e575a-167">Open the **index.js** file and replace it with the following code.</span></span>

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        req.body.readings.forEach(function(reading) {

            if(reading.temperature<=25) {
                reading.status = 'OK';
            } else if (reading.temperature<=50) {
                reading.status = 'CAUTION';
            } else {
                reading.status = 'DANGER'
            }
            context.log('Reading is ' + reading.status);
        });

        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

<span data-ttu-id="e575a-168">我们添加的逻辑非常简单。</span><span class="sxs-lookup"><span data-stu-id="e575a-168">The logic we added is straightforward.</span></span> <span data-ttu-id="e575a-169">我们循环访问读数数组并检查温度字段。</span><span class="sxs-lookup"><span data-stu-id="e575a-169">We iterate over the array of readings and check the temperature field.</span></span> <span data-ttu-id="e575a-170">根据该字段的值, 我们设置状态 **"正常**"、"**警告**" 或 "**危险**"。</span><span class="sxs-lookup"><span data-stu-id="e575a-170">Depending on the value of that field, we set a status of **OK**, **CAUTION**, or **DANGER**.</span></span> <span data-ttu-id="e575a-171">然后, 将返回包含一个添加到每个条目的状态字段的读数数组。</span><span class="sxs-lookup"><span data-stu-id="e575a-171">We then send back the array of readings with a status field added to each entry.</span></span>

<span data-ttu-id="e575a-172">请注意`log`语句。</span><span class="sxs-lookup"><span data-stu-id="e575a-172">Notice the `log` statements.</span></span> <span data-ttu-id="e575a-173">函数运行时, 这些语句将在日志窗口中添加消息。</span><span class="sxs-lookup"><span data-stu-id="e575a-173">When the function runs, these statements will add messages in the log window.</span></span>

## <a name="test-our-business-logic"></a><span data-ttu-id="e575a-174">测试我们的业务逻辑</span><span class="sxs-lookup"><span data-stu-id="e575a-174">Test our business logic</span></span>

<span data-ttu-id="e575a-175">在这种情况下, 我们将使用门户中的 "**测试**" 窗格来测试函数。</span><span class="sxs-lookup"><span data-stu-id="e575a-175">In this case, we're going to use the **Test** pane in the portal to test our function.</span></span>

1. <span data-ttu-id="e575a-176">从右侧的弹出菜单中打开 "**测试**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="e575a-176">Open the **Test** window from the right-hand side flyout menu.</span></span>

1. <span data-ttu-id="e575a-177">将示例请求粘贴到 "请求正文" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="e575a-177">Paste the sample request into the request body text box.</span></span>

    ```json
    {
        "readings": [
            {
                "driveGearId": 1,
                "timestamp": 1534263995,
                "temperature": 23
            },
            {
                "driveGearId": 3,
                "timestamp": 1534264048,
                "temperature": 45
            },
            {
                "driveGearId": 18,
                "timestamp": 1534264050,
                "temperature": 55
            }
        ]
    }
    ```

1. <span data-ttu-id="e575a-178">选择 "**运行**" 并在 "输出" 窗格中查看响应。</span><span class="sxs-lookup"><span data-stu-id="e575a-178">Select **Run** and view the response in the output pane.</span></span> <span data-ttu-id="e575a-179">若要查看日志消息, 请在页面的底部浮出控件中打开 "**日志**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="e575a-179">To see log messages, open the **Logs** tab in the bottom flyout of the page.</span></span> <span data-ttu-id="e575a-180">下面的屏幕截图显示了输出窗格中的示例响应和**日志**窗格中的邮件。</span><span class="sxs-lookup"><span data-stu-id="e575a-180">The following screenshot shows an example response in the output pane and messages in the  **Logs** pane.</span></span>

    ![在 "测试" 和 "日志" 选项卡可见的情况 Azure 门户中显示函数编辑器边栏的屏幕截图。](../media/5-portal-testing.png)

    <span data-ttu-id="e575a-183">您可以在 "输出" 窗格中看到, 我们的 "状态" 字段已正确添加到每个读数中。</span><span class="sxs-lookup"><span data-stu-id="e575a-183">You can see in the output pane that our status field has been correctly added to each of the readings.</span></span>

    <span data-ttu-id="e575a-184">如果导航到 "**监视**" 仪表板, 则会看到该请求已记录到 Application Insights 中。</span><span class="sxs-lookup"><span data-stu-id="e575a-184">If you navigate to the **Monitor** dashboard, you'll see that the request has been logged to Application Insights.</span></span>

    ![Azure 门户的屏幕截图, 显示函数监视器仪表板中的前一个测试成功结果。](../media/5-app-insights.png)
