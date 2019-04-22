您已创建了 Azure 函数`MojifyImage`, 该函数将返回一个 mojified 图像。 您需要另一个终结点, 只要有人执行该`/mojify`命令, 就会发生时差。 第二个终结点需要返回`MojifyImage`函数的 URL。

当您运行如所示`/mojify <some-image-url>`的可宽延时间命令时, 它会向您配置的终结点发出`<some-image-url>` POST 请求`text` , 并作为嵌入在邮件正文中的查询参数传入。 您将创建此函数, 它将协调和响应 "可宽延时间" 命令`RespondToSlackCommand`。 您将创建使用请求的格式可宽延时间的 HTTP 终结点, 以及如何获取该函数以使用图像进行响应。

## <a name="create-the-function-trigger-and-convert-to-typescript"></a>创建函数 Trigger 并转换为 TypeScript

您需要创建另一个 HTTP 触发的 Azure 函数。 这些说明基本上与以前相同。 不同之处是, 您调用的`RespondToSlackCommand` `MojifyImage`是此函数而不是。

1. 依次单击 "**查看**" 和 "**命令选项板**", 然后搜索并选择**Azure 函数: Create Function ...**

    ![在 VS 代码窗口顶部创建新的函数对话框](../media/4.create-function.png)

2. 选择最初在其中创建 function 项目的文件夹。

    ![显示当前文件夹位置的 "选择文件夹" 对话框](../media/4.select-current-project.png)

3. 选择 " **HTTP 触发器**" 选项。

    ![从可用触发器列表中选择 "HTTP 触发器", 包括 blob、队列和计时器触发器, 以及用于更改各种设置 (如 project runtime、project language 和 template filter) 的三个选项](../media/4.select-trigger.png)

4. 键入`RespondToSlackCommand`作为函数的名称。

    ![使用文本字段中提供的 MojifyImage 选择 "名称" 对话框](../media/4.choose-function-name.png)

5. 选择 "**匿名**" 作为身份验证级别。

    > [!NOTE]
    > 通过选择 "**匿名**", 函数在世界范围内开放且不安全。 如果将来创建其他函数, 则不建议使用此默认行为。 由于这是使用免费 Azure 学习资源的低风险操作, 因此目前尚不存在问题。

    !["选择授权级别" 对话框提供可供选择的匿名、功能和管理选项。](../media/4.choose-auth-level.png)

    如果成功, 您现在应该将文件夹**RespondToSlackCommand**在根目录中。

    现在, 您可以将文件从 TypeScript 转换为 JavaScript。

6. 在`RespondToSlackCommand`文件夹中创建`index.ts`一个名为的文件。

   确保生成过程仍`TypeScript`在运行, 并将自动编译到`index.js`和`index.js.map`文件中。

7. 将中`index.ts`的代码替换为以下代码:

    ```typescript
    export function index(context, req) {
      context.log("RespondToSlackCommand HTTP trigger");
      context.res.body = "Hello!";
      context.done();
    }
    ```

## <a name="try-it-out"></a>试用

确保一切都可以通过访问 (http://localhost:7071/api/RespondToSlackCommand)在浏览器中) 进行操作。 应打印我们`Hello!`的。

## <a name="write-the-index-function"></a>编写`index`函数

与`index(context, req)`以前的函数相比, 此 TypeScript 函数的编写速度要快得多。

1. 在函数的`context.res`顶部设置对象。

    ```typescript
    context.res = {
      headers: {
        "Content-Type": "application/json"
      },
      body: null
    };
    ```

    这次, 不需要设置`isRaw`属性, 因为此属性默认为。 `false` 但是, 您确实需要将内容类型设置为`application/json`。

1. 添加有用的库`querystring`。

    由于可宽延时间发送图像 URL, 因此您需要将其处理为包含键的`text`查询字符串。 它在请求的正文中嵌入此内容, 因此您需要花费一些更难的信息来获取正确的信息。 但这并不是太难!

    通过导入 node.js `querystring`包使自己的工作变得更加轻松。 这是 node.js 的一部分, 因此无需安装任何额外的内容。 将此导入语句添加到文件顶部。

    ```typescript
    import * as querystring from "querystring";
    ```

1. 在`index(context, req)`函数中, 将转换`req.body`为要从中提取`text`属性的对象。

    ```typescript
    const { text } = querystring.parse(req.body);
    ```

    如果用户正确键入命令, 则文本应包含图像的 URL。 向其添加一些基本验证以确保其正常工作。

    ```typescript
    let message = "Your mojified image my liege...";
    if (!text) {
      message = "You must provide an image to mojify";
    }
    ```

    "可宽延时间`https://somedomain.com/api/RespondToSlackCommand`" 命令正在调用。 它需要使用 MojifyImage URL 进行响应, 我们假定它将位于同一个域中。

1. 从请求`MojifyImage`请求 URL 中提取域。

    ```typescript
    const mojifyUrl = req.originalUrl.substr(0, req.originalUrl.lastIndexOf("/")) + "/MojifyImage";
    ```

1. 最后, 在`index(context, req)`函数底部将响应正文设置为可宽延时间的特定格式。

    > [!IMPORTANT]
    > `image_url`需要`attachments`将属性设置为返回`mojifyUrl`, 并将命令中提供的用户作为`imageUrl`查询参数传入 URL 中。

    ```typescript
    context.res.body = {
      response_type: "in_channel",
      text: message,
      attachments: [
        {
          image_url: `${mojifyUrl}?imageUrl=${text}`
        }
      ]
    };

    context.done();
    ```

## <a name="try-it-out"></a>试用

1. 确保使用以前使用的方法之一运行本地 Azure 函数应用程序: 使用`func host start`或从 "调试" 菜单使用 "**附加到 JavaScript 函数**" 任务来运行它。

    如果函数应用程序正确启动, 则 "输出" 窗口应显示如下所示的内容:

    ```
    Http Functions:
            MojifyImage: http://localhost:7071/api/MojifyImage
            RespondToSlackCommand: http://localhost:7071/api/RespondToSlackCommand
    ```

通过在浏览器中进行访问http://localhost:7071/api/RespondToSlackCommand , 确保一切正常。 它现在应打印一些 json。

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "http://localhost:7071/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```
