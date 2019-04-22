接下来, 我们将继续使用我们的齿轮驱动器示例, 并添加温度服务的逻辑。 具体来说, 我们将从 HTTP 请求中接收数据。

## <a name="function-requirements"></a>函数要求

首先, 我们需要为逻辑定义一些要求:

- 0-25 之间的温度应标记为 **"确定"**。
- 应将26-50 之间的温度标记为**警告**。
- 应将高于50的温度标记为**危险**。

## <a name="add-a-function-to-our-function-app"></a>向我们的函数应用程序添加函数

如前面的单元中所述, Azure 提供可帮助您开始构建功能的模板。 在此单元中, 我们将使用`HttpTrigger`模板来实施温度服务。

1. 登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 通过选择左侧菜单中的 "**所有资源**", 然后选择 "**<rgn>[沙盒资源组名称]</rgn>**", 从第一个练习中选择资源组。

1. 然后, 将显示组的资源。 单击您在上一练习中创建的函数应用程序的名称, 方法是选择 "自动**扶梯函数-xxxxxxx** " 项 (也由闪电形函数图标指示)。

    ![显示 "所有资源" 边栏已突出显示的 Azure 门户屏幕截图以及我们创建的自动扶梯功能应用程序的屏幕截图。](../media/5-access-function-app.png)

1. 选择 "函数"**+** 旁边的 "添加****" () 按钮。 此操作将启动函数创建过程。

1. 在 "**适用于 JavaScript 的 Azure 函数-入门**" 页上, 选择 "**在门户中**", 然后选择 "**继续**"。

1. 在 "**创建函数**" 步骤中, 选择 "**更多模板 ...** ", 然后选择 "完成", 然后单击 "**查看模板**"。

1. 在可用于此函数应用程序的所有模板的列表中, 选择 " **Http 触发器**"。

1. 在出现的 "**新建函数**" 对话框的 "名称" 字段中输入**DriveGearTemperatureService** 。 将授权级别保留为 "函数", 然后按 "**创建**" 按钮以创建函数。

1. 函数创建完成后, 代码编辑器将打开, 并附带*索引 .js*代码文件的内容。 下面的代码片段中列出了为我们生成的模板所生成的默认代码。

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

    我们的函数需要通过 HTTP 请求查询字符串或作为请求正文的一部分传入的名称。 函数通过返回邮件**Hello, {name}** 回显在请求中发送的名称进行响应。

    在 "源" 视图的右侧, 您将找到两个选项卡。 "**查看文件**" 选项卡列出了函数的代码和配置文件。  选择**函数 json**以查看函数的配置, 其外观应类似于以下内容:

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

    此配置声明函数在收到 HTTP 请求时运行。 输出绑定声明响应将作为 HTTP 响应发送。    

## <a name="test-the-function"></a>测试函数

> [!TIP]
> "**卷曲**" 是一种命令行工具, 可用于发送或接收文件。 它包含在 Linux、macOS 和 Windows 10 中, 可以为大多数其他操作系统下载。 卷支持多种协议, 如 HTTP、HTTPS、FTP、FTPS、SFTP、LDAP、TELNET、SMTP、POP3 等。有关详细信息, 请参阅以下链接:
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

若要测试函数, 可以在命令行中使用曲线向函数 URL 发送 HTTP 请求。 若要查找函数的终结点 URL, 请返回到您的函数代码并选择**Get 函数 URL**链接, 如以下屏幕截图所示。 临时保存此链接。

![显示 "函数编辑器" 的 Azure 门户屏幕截图, 其中突出显示了 Get 函数 URL 按钮。](../media/5-get-function-url.png)

### <a name="securing-http-triggers"></a>保护 HTTP 触发器

通过 HTTP 触发器, 可以通过要求在每个请求上提供密钥来使用 API 密钥阻止未知的调用方。 创建函数时, 请选择 "_授权级别_"。 默认情况下, 它设置为 "函数", 它需要一个特定于函数的 API 键, 但也可以将其设置为 "Admin" 以使用全局 "主" 键, 或 "匿名" 以指示无需任何键。 您还可以在创建后通过函数属性更改授权级别。

由于我们在创建此函数时指定了 "函数", 因此我们需要在发送 HTTP 请求时提供密钥。 您可以将其作为名为的查询字符串`code`参数或作为名`x-functions-key`为的 HTTP 标头 (首选) 发送。

扩展函数时, 可以在 "**管理**" 部分找到函数和主密钥。 默认情况下, 它们是隐藏的, 您需要显示它们。

1. 展开您的函数并选择 "**管理**" 部分, 显示默认的功能键, 并将其复制到剪贴板。

    ![显示功能管理刀片并突出显示的功能键的 Azure 门户屏幕截图。](../media/5-get-function-key.png)

1. 接下来, 从安装了**卷曲**工具的命令行中, 使用函数的 URL 和功能键格式化卷曲命令。

    - 使用`POST`请求。
    - 添加一个`Content-Type`类型`application/json`的标头值。
    - 请确保将以下 URL 替换为您自己的 URL。
    - 将 Function 键作为标头值`x-functions-key`传递。

    ```bash
    curl --header "Content-Type: application/json" --header "x-functions-key: <your-function-key>" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
    ```

函数将使用文本`"Hello Azure Function"`进行回复。

> [!CAUTION]
> 如果您在 Windows 上, 请从`cURL`命令提示符运行。 PowerShell 有*卷曲*的命令, 但它是 WebRequest 的别名, 与不同`cURL`。

> [!NOTE]
> 您还可以使用所选函数一侧的 "**测试**" 选项卡来测试单个函数的节, 尽管无法验证该功能键系统是否正常工作, 但此处不需要它。 在测试界面中添加适当的标头和参数值, 然后单击 "**运行**" 按钮以查看测试输出。

## <a name="add-business-logic-to-the-function"></a>向函数中添加业务逻辑

接下来, 让我们向检查其收到的温度读数的函数添加逻辑, 并为每个函数设置状态。

我们的函数需要一组温度读数。 下面的 JSON 代码片段是我们将发送给我们的函数的请求正文的示例。 每`reading`个条目都有 ID、时间戳和温度。

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

接下来, 我们将使用实现业务逻辑的以下代码替换函数中的默认代码。

1. 打开一个**索引 .js**文件, 并将其替换为以下代码。

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

我们添加的逻辑非常简单。 我们循环访问读数数组并检查温度字段。 根据该字段的值, 我们设置状态 **"正常**"、"**警告**" 或 "**危险**"。 然后, 将返回包含一个添加到每个条目的状态字段的读数数组。

请注意`log`语句。 函数运行时, 这些语句将在日志窗口中添加消息。

## <a name="test-our-business-logic"></a>测试我们的业务逻辑

在这种情况下, 我们将使用门户中的 "**测试**" 窗格来测试函数。

1. 从右侧的弹出菜单中打开 "**测试**" 窗口。

1. 将示例请求粘贴到 "请求正文" 文本框中。

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

1. 选择 "**运行**" 并在 "输出" 窗格中查看响应。 若要查看日志消息, 请在页面的底部浮出控件中打开 "**日志**" 选项卡。 下面的屏幕截图显示了输出窗格中的示例响应和**日志**窗格中的邮件。

    ![在 "测试" 和 "日志" 选项卡可见的情况 Azure 门户中显示函数编辑器边栏的屏幕截图。 在输出窗格中显示函数的示例响应。](../media/5-portal-testing.png)

    您可以在 "输出" 窗格中看到, 我们的 "状态" 字段已正确添加到每个读数中。

    如果导航到 "**监视**" 仪表板, 则会看到该请求已记录到 Application Insights 中。

    ![Azure 门户的屏幕截图, 显示函数监视器仪表板中的前一个测试成功结果。](../media/5-app-insights.png)
