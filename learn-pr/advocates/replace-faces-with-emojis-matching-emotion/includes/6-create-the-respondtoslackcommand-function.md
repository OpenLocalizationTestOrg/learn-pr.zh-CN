<span data-ttu-id="155bc-101">您已创建了 Azure 函数`MojifyImage`, 该函数将返回一个 mojified 图像。</span><span class="sxs-lookup"><span data-stu-id="155bc-101">You've created the Azure Function `MojifyImage`, which returns a mojified image.</span></span> <span data-ttu-id="155bc-102">您需要另一个终结点, 只要有人执行该`/mojify`命令, 就会发生时差。</span><span class="sxs-lookup"><span data-stu-id="155bc-102">You need a second endpoint that Slack calls whenever someone executes the `/mojify` command.</span></span> <span data-ttu-id="155bc-103">第二个终结点需要返回`MojifyImage`函数的 URL。</span><span class="sxs-lookup"><span data-stu-id="155bc-103">This second endpoint needs to return the URL to the `MojifyImage` function.</span></span>

<span data-ttu-id="155bc-104">当您运行如所示`/mojify <some-image-url>`的可宽延时间命令时, 它会向您配置的终结点发出`<some-image-url>` POST 请求`text` , 并作为嵌入在邮件正文中的查询参数传入。</span><span class="sxs-lookup"><span data-stu-id="155bc-104">When you run a Slack command like `/mojify <some-image-url>`, it makes a POST request to the endpoint you've configured, and passes in `<some-image-url>` as a `text` query parameter embedded in the body of the message.</span></span> <span data-ttu-id="155bc-105">您将创建此函数, 它将协调和响应 "可宽延时间" 命令`RespondToSlackCommand`。</span><span class="sxs-lookup"><span data-stu-id="155bc-105">You're going to create this function, which will coordinate and respond to the Slack commands as `RespondToSlackCommand`.</span></span> <span data-ttu-id="155bc-106">您将创建使用请求的格式可宽延时间的 HTTP 终结点, 以及如何获取该函数以使用图像进行响应。</span><span class="sxs-lookup"><span data-stu-id="155bc-106">You'll create the HTTP endpoint that uses the format Slack expects for the request, and how to get the function to respond with an image.</span></span>

## <a name="create-the-function-trigger-and-convert-to-typescript"></a><span data-ttu-id="155bc-107">创建函数 Trigger 并转换为 TypeScript</span><span class="sxs-lookup"><span data-stu-id="155bc-107">Create the Function Trigger and convert to TypeScript</span></span>

<span data-ttu-id="155bc-108">您需要创建另一个 HTTP 触发的 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="155bc-108">You need to create another HTTP-triggered Azure Function.</span></span> <span data-ttu-id="155bc-109">这些说明基本上与以前相同。</span><span class="sxs-lookup"><span data-stu-id="155bc-109">These instructions are basically the same as before.</span></span> <span data-ttu-id="155bc-110">不同之处是, 您调用的`RespondToSlackCommand` `MojifyImage`是此函数而不是。</span><span class="sxs-lookup"><span data-stu-id="155bc-110">What's different is that you're calling this function `RespondToSlackCommand` instead of `MojifyImage`.</span></span>

1. <span data-ttu-id="155bc-111">依次单击 "**查看**" 和 "**命令选项板**", 然后搜索并选择**Azure 函数: Create Function ...**</span><span class="sxs-lookup"><span data-stu-id="155bc-111">Click on **View** then **Command Palette**, then search for and select **Azure Functions: Create Function...**</span></span>

    ![在 VS 代码窗口顶部创建新的函数对话框](../media/4.create-function.png)

2. <span data-ttu-id="155bc-113">选择最初在其中创建 function 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="155bc-113">Select the folder where you originally created the function project.</span></span>

    ![显示当前文件夹位置的 "选择文件夹" 对话框](../media/4.select-current-project.png)

3. <span data-ttu-id="155bc-115">选择 " **HTTP 触发器**" 选项。</span><span class="sxs-lookup"><span data-stu-id="155bc-115">Select the **HTTP Trigger** option.</span></span>

    ![从可用触发器列表中选择 "HTTP 触发器", 包括 blob、队列和计时器触发器, 以及用于更改各种设置 (如 project runtime、project language 和 template filter) 的三个选项](../media/4.select-trigger.png)

4. <span data-ttu-id="155bc-117">键入`RespondToSlackCommand`作为函数的名称。</span><span class="sxs-lookup"><span data-stu-id="155bc-117">Type `RespondToSlackCommand` as the name of your function.</span></span>

    ![使用文本字段中提供的 MojifyImage 选择 "名称" 对话框](../media/4.choose-function-name.png)

5. <span data-ttu-id="155bc-119">选择 "**匿名**" 作为身份验证级别。</span><span class="sxs-lookup"><span data-stu-id="155bc-119">Choose **Anonymous** as the authentication level.</span></span>

    > [!NOTE]
    > <span data-ttu-id="155bc-120">通过选择 "**匿名**", 函数在世界范围内开放且不安全。</span><span class="sxs-lookup"><span data-stu-id="155bc-120">By choosing **Anonymous**, the function is open to the world and insecure.</span></span> <span data-ttu-id="155bc-121">如果将来创建其他函数, 则不建议使用此默认行为。</span><span class="sxs-lookup"><span data-stu-id="155bc-121">If you create other functions in the future, this isn't the recommended default behavior.</span></span> <span data-ttu-id="155bc-122">由于这是使用免费 Azure 学习资源的低风险操作, 因此目前尚不存在问题。</span><span class="sxs-lookup"><span data-stu-id="155bc-122">Since this is a low-risk exercise with free Azure learning resources, it's not a problem for now.</span></span>

    !["选择授权级别" 对话框提供可供选择的匿名、功能和管理选项。](../media/4.choose-auth-level.png)

    <span data-ttu-id="155bc-124">如果成功, 您现在应该将文件夹**RespondToSlackCommand**在根目录中。</span><span class="sxs-lookup"><span data-stu-id="155bc-124">If it was successful, then you should now have the folder **RespondToSlackCommand** in the root directory.</span></span>

    <span data-ttu-id="155bc-125">现在, 您可以将文件从 TypeScript 转换为 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="155bc-125">Now you can convert the file from TypeScript to JavaScript.</span></span>

6. <span data-ttu-id="155bc-126">在`RespondToSlackCommand`文件夹中创建`index.ts`一个名为的文件。</span><span class="sxs-lookup"><span data-stu-id="155bc-126">Create a file called `index.ts` in the `RespondToSlackCommand` folder.</span></span>

   <span data-ttu-id="155bc-127">确保生成过程仍`TypeScript`在运行, 并将自动编译到`index.js`和`index.js.map`文件中。</span><span class="sxs-lookup"><span data-stu-id="155bc-127">Make sure that the `TypeScript` build process is still running and that it automatically compiled into the `index.js` and `index.js.map` files.</span></span>

7. <span data-ttu-id="155bc-128">将中`index.ts`的代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="155bc-128">Replace the code in `index.ts` with the following code:</span></span>

    ```typescript
    export function index(context, req) {
      context.log("RespondToSlackCommand HTTP trigger");
      context.res.body = "Hello!";
      context.done();
    }
    ```

## <a name="try-it-out"></a><span data-ttu-id="155bc-129">试用</span><span class="sxs-lookup"><span data-stu-id="155bc-129">Try it out</span></span>

<span data-ttu-id="155bc-130">确保一切都可以通过访问 (http://localhost:7071/api/RespondToSlackCommand)在浏览器中) 进行操作。</span><span class="sxs-lookup"><span data-stu-id="155bc-130">Make sure that everything is working by visiting (http://localhost:7071/api/RespondToSlackCommand) in a browser.</span></span> <span data-ttu-id="155bc-131">应打印我们`Hello!`的。</span><span class="sxs-lookup"><span data-stu-id="155bc-131">It should print our `Hello!`.</span></span>

## <a name="write-the-index-function"></a><span data-ttu-id="155bc-132">编写`index`函数</span><span class="sxs-lookup"><span data-stu-id="155bc-132">Write the `index` function</span></span>

<span data-ttu-id="155bc-133">与`index(context, req)`以前的函数相比, 此 TypeScript 函数的编写速度要快得多。</span><span class="sxs-lookup"><span data-stu-id="155bc-133">This `index(context, req)` TypeScript function is a lot quicker to write than the previous function.</span></span>

1. <span data-ttu-id="155bc-134">在函数的`context.res`顶部设置对象。</span><span class="sxs-lookup"><span data-stu-id="155bc-134">Set up your `context.res` object at the top of the function.</span></span>

    ```typescript
    context.res = {
      headers: {
        "Content-Type": "application/json"
      },
      body: null
    };
    ```

    <span data-ttu-id="155bc-135">这次, 不需要设置`isRaw`属性, 因为此属性默认为。 `false`</span><span class="sxs-lookup"><span data-stu-id="155bc-135">This time, you don't need to set the `isRaw` property since this defaults to `false`.</span></span> <span data-ttu-id="155bc-136">但是, 您确实需要将内容类型设置为`application/json`。</span><span class="sxs-lookup"><span data-stu-id="155bc-136">However, you do need set the content type to be `application/json`.</span></span>

1. <span data-ttu-id="155bc-137">添加有用的库`querystring`。</span><span class="sxs-lookup"><span data-stu-id="155bc-137">Add the useful library `querystring`.</span></span>

    <span data-ttu-id="155bc-138">由于可宽延时间发送图像 URL, 因此您需要将其处理为包含键的`text`查询字符串。</span><span class="sxs-lookup"><span data-stu-id="155bc-138">Since Slack sends the image URL, you want to process it as a query string with the key of `text`.</span></span> <span data-ttu-id="155bc-139">它在请求的正文中嵌入此内容, 因此您需要花费一些更难的信息来获取正确的信息。</span><span class="sxs-lookup"><span data-stu-id="155bc-139">It embeds this in the body of the request, so you need to work a little harder to get the right information.</span></span> <span data-ttu-id="155bc-140">但这并不是太难!</span><span class="sxs-lookup"><span data-stu-id="155bc-140">It's not too hard though!</span></span>

    <span data-ttu-id="155bc-141">通过导入 node.js `querystring`包使自己的工作变得更加轻松。</span><span class="sxs-lookup"><span data-stu-id="155bc-141">Make life easier for yourself by importing the Node.js `querystring` package.</span></span> <span data-ttu-id="155bc-142">这是 node.js 的一部分, 因此无需安装任何额外的内容。</span><span class="sxs-lookup"><span data-stu-id="155bc-142">This is part of Node.js, so there's no need to install anything extra.</span></span> <span data-ttu-id="155bc-143">将此导入语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="155bc-143">Add this import statement to the top of the file.</span></span>

    ```typescript
    import * as querystring from "querystring";
    ```

1. <span data-ttu-id="155bc-144">在`index(context, req)`函数中, 将转换`req.body`为要从中提取`text`属性的对象。</span><span class="sxs-lookup"><span data-stu-id="155bc-144">In your `index(context, req)` function, convert the `req.body` into an object from which you'll extract the `text` property.</span></span>

    ```typescript
    const { text } = querystring.parse(req.body);
    ```

    <span data-ttu-id="155bc-145">如果用户正确键入命令, 则文本应包含图像的 URL。</span><span class="sxs-lookup"><span data-stu-id="155bc-145">If a user types the command properly, then the text should contain the URL of an image.</span></span> <span data-ttu-id="155bc-146">向其添加一些基本验证以确保其正常工作。</span><span class="sxs-lookup"><span data-stu-id="155bc-146">Add some basic validation to it to make sure it works.</span></span>

    ```typescript
    let message = "Your mojified image my liege...";
    if (!text) {
      message = "You must provide an image to mojify";
    }
    ```

    <span data-ttu-id="155bc-147">"可宽延时间`https://somedomain.com/api/RespondToSlackCommand`" 命令正在调用。</span><span class="sxs-lookup"><span data-stu-id="155bc-147">The Slack command is calling `https://somedomain.com/api/RespondToSlackCommand`.</span></span> <span data-ttu-id="155bc-148">它需要使用 MojifyImage URL 进行响应, 我们假定它将位于同一个域中。</span><span class="sxs-lookup"><span data-stu-id="155bc-148">It needs to respond with the MojifyImage URL, which we assume will be on the same domain.</span></span>

1. <span data-ttu-id="155bc-149">从请求`MojifyImage`请求 URL 中提取域。</span><span class="sxs-lookup"><span data-stu-id="155bc-149">Extract the domain from the request `MojifyImage` request URL.</span></span>

    ```typescript
    const mojifyUrl = req.originalUrl.substr(0, req.originalUrl.lastIndexOf("/")) + "/MojifyImage";
    ```

1. <span data-ttu-id="155bc-150">最后, 在`index(context, req)`函数底部将响应正文设置为可宽延时间的特定格式。</span><span class="sxs-lookup"><span data-stu-id="155bc-150">Finally, set the body of the response to the Slack-specific format at the bottom of the `index(context, req)` function.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="155bc-151">`image_url`需要`attachments`将属性设置为返回`mojifyUrl`, 并将命令中提供的用户作为`imageUrl`查询参数传入 URL 中。</span><span class="sxs-lookup"><span data-stu-id="155bc-151">The `image_url` in the `attachments` property needs to be set to return the `mojifyUrl`, passing in the URL the user supplied in the command as the `imageUrl` query parameter.</span></span>

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

## <a name="try-it-out"></a><span data-ttu-id="155bc-152">试用</span><span class="sxs-lookup"><span data-stu-id="155bc-152">Try it out</span></span>

1. <span data-ttu-id="155bc-153">确保使用以前使用的方法之一运行本地 Azure 函数应用程序: 使用`func host start`或从 "调试" 菜单使用 "**附加到 JavaScript 函数**" 任务来运行它。</span><span class="sxs-lookup"><span data-stu-id="155bc-153">Make sure that the local Azure function application is running using one of the methods you previously used: either use `func host start` or run it from the debug menu using the **Attach to JavaScript Function** task.</span></span>

    <span data-ttu-id="155bc-154">如果函数应用程序正确启动, 则 "输出" 窗口应显示如下所示的内容:</span><span class="sxs-lookup"><span data-stu-id="155bc-154">If the function app started correctly, then the output window should show something like this:</span></span>

    ```
    Http Functions:
            MojifyImage: http://localhost:7071/api/MojifyImage
            RespondToSlackCommand: http://localhost:7071/api/RespondToSlackCommand
    ```

<span data-ttu-id="155bc-155">通过在浏览器中进行访问http://localhost:7071/api/RespondToSlackCommand , 确保一切正常。</span><span class="sxs-lookup"><span data-stu-id="155bc-155">Make sure that everything is working by visiting http://localhost:7071/api/RespondToSlackCommand in your browser.</span></span> <span data-ttu-id="155bc-156">它现在应打印一些 json。</span><span class="sxs-lookup"><span data-stu-id="155bc-156">It should now print some json.</span></span>

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
