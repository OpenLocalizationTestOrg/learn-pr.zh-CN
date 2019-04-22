<span data-ttu-id="811e6-101">现在, 您已创建了 azure function 项目和最低 JavaScript Azure 函数, 你将在 TypeScript 中开发此 azure 函数。</span><span class="sxs-lookup"><span data-stu-id="811e6-101">Now that you've created your Azure Function project, and a minimal JavaScript Azure function, you're going to develop this Azure Function in TypeScript.</span></span> <span data-ttu-id="811e6-102">final 函数将从其查询参数中读取图像 URL, 使用表面 API 在图像中查找表面及其感受, 然后将这些面替换为匹配的表情符号 (s)。</span><span class="sxs-lookup"><span data-stu-id="811e6-102">The final function will read an image URL from its query parameters, use the Face API to find the faces and their emotions in the image, then replace the face(s) with matching emoji(s).</span></span> <span data-ttu-id="811e6-103">它返回此复合图像作为 raw 图像数据。</span><span class="sxs-lookup"><span data-stu-id="811e6-103">It returns this composite image as raw image data.</span></span>

## <a name="convert-to-typescript"></a><span data-ttu-id="811e6-104">转换为 TypeScript</span><span class="sxs-lookup"><span data-stu-id="811e6-104">Convert to TypeScript</span></span>

<span data-ttu-id="811e6-105">Azure 函数扩展创建了一个 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="811e6-105">The Azure function extension created a JavaScript function.</span></span> <span data-ttu-id="811e6-106">我们需要将其转换为 TypeScript。</span><span class="sxs-lookup"><span data-stu-id="811e6-106">We need to convert it to TypeScript.</span></span>

1. <span data-ttu-id="811e6-107">将`index.js`文件重命名为`index.ts`</span><span class="sxs-lookup"><span data-stu-id="811e6-107">Rename the `index.js` file to `index.ts`</span></span>

    > [!NOTE]
    > <span data-ttu-id="811e6-108">如果您正在运行`npm run build`和相关`tsc -w`命令, 则`index.ts`文件将立即编译为。 `index.js`</span><span class="sxs-lookup"><span data-stu-id="811e6-108">If you're running `npm run build` and the related `tsc -w` command, then the `index.ts` file is instantly compiled to `index.js`.</span></span> <span data-ttu-id="811e6-109">它还应创建一个`index.js.map`文件。</span><span class="sxs-lookup"><span data-stu-id="811e6-109">It should also create an `index.js.map` file.</span></span> <span data-ttu-id="811e6-110">如果和`index.js` `index.js.map`文件不是自动创建的, 请检查`npm run build`命令是否正在运行, 并且输出不显示任何错误。</span><span class="sxs-lookup"><span data-stu-id="811e6-110">If the `index.js` and `index.js.map` files are not automatically created, check whether the `npm run build` command is running and that the output doesn't show any errors.</span></span>

1. <span data-ttu-id="811e6-111">将中`index.ts`的代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="811e6-111">Replace the code in `index.ts` with the following code:</span></span>

    ```typescript
    export async function index(context, req) {
      context.log("ReplyWithMojifiedImage HTTP trigger");
      context.res.body = "Hello!";
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="811e6-112">使用`context.log` Azure 函数而不是`console.log`将输出记录到控制台。</span><span class="sxs-lookup"><span data-stu-id="811e6-112">With Azure Functions we use `context.log` instead of `console.log` to log output to the console.</span></span>

## <a name="test-your-function"></a><span data-ttu-id="811e6-113">测试函数</span><span class="sxs-lookup"><span data-stu-id="811e6-113">Test your function</span></span>

1. <span data-ttu-id="811e6-114">确保使用以前使用的方法之一运行本地 Azure function 应用程序: 使用`func host start`或从 "调试" 菜单使用 "**附加到 JavaScript 函数**" 任务运行它。</span><span class="sxs-lookup"><span data-stu-id="811e6-114">Make sure the local Azure function application is running using one of the methods you previously used: either use `func host start` or run it from the debug menu using the **Attach to JavaScript Function** task.</span></span>

    <span data-ttu-id="811e6-115">如果函数应用程序正确启动, 则 "输出" 窗口应显示类似于以下输出的内容:</span><span class="sxs-lookup"><span data-stu-id="811e6-115">If the function app started correctly, then the output window should show something like this output:</span></span>

    ```
    Http Functions:
            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

1. <span data-ttu-id="811e6-116">访问浏览器中的 URL。</span><span class="sxs-lookup"><span data-stu-id="811e6-116">Visit the URL in your browser.</span></span> <span data-ttu-id="811e6-117">如果一切正常, 它应打印出来`Hello!`。</span><span class="sxs-lookup"><span data-stu-id="811e6-117">If everything is functioning correctly, it should print out `Hello!`.</span></span>

    <span data-ttu-id="811e6-118">如果看到`Hello`, 您已将函数触发器从 TypeScript 转换为 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="811e6-118">If you see `Hello`, you've converted your function trigger from TypeScript to JavaScript.</span></span>

## <a name="configure-your-face-api-environment-variables"></a><span data-ttu-id="811e6-119">配置你的面孔 API 环境变量</span><span class="sxs-lookup"><span data-stu-id="811e6-119">Configure your Face API environment variables</span></span>

<span data-ttu-id="811e6-120">为了提高代码的安全性, 您不应在代码中对私有数据进行硬编码。</span><span class="sxs-lookup"><span data-stu-id="811e6-120">To make your code more secure, you shouldn't hard-code private data in your code.</span></span> <span data-ttu-id="811e6-121">而是使用环境变量来存储面孔 API URL 和密钥。</span><span class="sxs-lookup"><span data-stu-id="811e6-121">Instead we use environment variables to store the Face API URL and key.</span></span>

<span data-ttu-id="811e6-122">在创建 Azure 函数项目时, 它会创建一个名`local.settings.json`为的文件。</span><span class="sxs-lookup"><span data-stu-id="811e6-122">When you create an Azure Functions project, it creates a file called `local.settings.json`.</span></span> <span data-ttu-id="811e6-123">此文件位于`.gitignore`文件中, 因此未签入到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="811e6-123">This file is in the `.gitignore` file so it isn't checked into source control.</span></span> <span data-ttu-id="811e6-124">它是存储不希望发布的敏感或本地配置的位置。</span><span class="sxs-lookup"><span data-stu-id="811e6-124">It's a place to store sensitive or local configurations that you don't want to be published.</span></span> <span data-ttu-id="811e6-125">将对象中`Values`的任何内容作为环境变量提供给 node.js 代码。</span><span class="sxs-lookup"><span data-stu-id="811e6-125">Anything in the `Values` object is made available to your Node.js code as an environment variable.</span></span>

1. <span data-ttu-id="811e6-126">在`local.settings.json` Visual Studio Code 中打开。</span><span class="sxs-lookup"><span data-stu-id="811e6-126">Open `local.settings.json` in Visual Studio Code.</span></span> <span data-ttu-id="811e6-127">默认情况下, 该文件包含以下内容:</span><span class="sxs-lookup"><span data-stu-id="811e6-127">By default, the file has these contents:</span></span>

    ```json
    {
      "IsEncrypted": false,
      "Values": {
        "AzureWebJobsStorage": "",
        "FUNCTIONS_WORKER_RUNTIME": "node"
      }
    }
    ```

1. <span data-ttu-id="811e6-128">将此文件的内容**替换**为你的面孔 API 变量 (即, 删除该文件中的默认设置)。</span><span class="sxs-lookup"><span data-stu-id="811e6-128">**Replace** the contents of this file with your Face API variables (i.e. remove the default settings from the file).</span></span> <span data-ttu-id="811e6-129">创建面孔`<face-api-url>` API `<face-api-key>` Azure 资源时, 请将和值替换为您保存的变量。</span><span class="sxs-lookup"><span data-stu-id="811e6-129">Replace the `<face-api-url>` and `<face-api-key>` values with the variables that you saved, when you created your Face API Azure resource.</span></span>

    ```json
    {
        "Values": {
          "FACE_API_URL": "<face-api-url>",
          "FACE_API_KEY": "<face-api-key>"
        }
    }
    ```

<span data-ttu-id="811e6-130">`FACE_API_URL`和`FACE_API_KEY`变量将作为环境变量提供给 node.js。</span><span class="sxs-lookup"><span data-stu-id="811e6-130">The `FACE_API_URL` and `FACE_API_KEY` variables will be available to Node.js as environment variables.</span></span>

<span data-ttu-id="811e6-131">在对[面孔 API 的调用](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.ts)中使用这些变量</span><span class="sxs-lookup"><span data-stu-id="811e6-131">The variables are used in the [calls to the Face API](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.ts)</span></span>

## <a name="write-the-mojifyimage-function"></a><span data-ttu-id="811e6-132">编写 MojifyImage 函数</span><span class="sxs-lookup"><span data-stu-id="811e6-132">Write the MojifyImage function</span></span>

1. <span data-ttu-id="811e6-133">将中`MojifyImage/index.ts`的代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="811e6-133">Replace the code in `MojifyImage/index.ts` with the following code:</span></span>

    ```typescript
    import Jimp = require("jimp");
    import * as path from "path";
    import * as FaceApi from "../shared/faceapi";

    async function createMojifiedImage(context, imageUrl, faces) {
      // TODO
    }

    export async function index(context, req) {
      context.log(`ReplyWithMojifiedImage HTTP trigger`);
      context.res.body = "Hello!";
    }
    ```

    <span data-ttu-id="811e6-134">你将在此单元`createMojifiedImage`中开发函数`index`和函数。</span><span class="sxs-lookup"><span data-stu-id="811e6-134">You'll be developing the `createMojifiedImage` function and the `index` function in this unit.</span></span>

1. <span data-ttu-id="811e6-135">使用图像调用面孔 API 并获取响应</span><span class="sxs-lookup"><span data-stu-id="811e6-135">Call the Face API with an image and get a response</span></span>

    <span data-ttu-id="811e6-136">将`index(context, req)` `index.ts`文件中的函数正文替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="811e6-136">Replace the body of the `index(context, req)` function in the `index.ts` file with the following code.</span></span>

    ```typescript
    const { imageUrl } = req.query;

    if (!imageUrl) {
      let message = `imageUrl is required`;
      context.log(message);
      context.res = { status: 400, body: message }
    } else {
      context.log(`Called with imageUrl: "${imageUrl}"`);

      // Get the response from the faceAPI
      try {
        let faces = await FaceApi.getFaces(context, imageUrl);
        context.log(faces);
        context.res = { status: 200, body: faces }
      } catch (err) {
        let message = `There was an error processing this image: ${err.message}`;
        context.log(message);
        context.res = { status: 400, body: message };
      }
    }
    ```

1. <span data-ttu-id="811e6-137">在浏览器中运行此函数</span><span class="sxs-lookup"><span data-stu-id="811e6-137">Run this function in your browser</span></span>

    <span data-ttu-id="811e6-138">在传递图像时, 您应该会看到表面 API 返回的 json 响应: `http://localhost:7071/api/MojifyImage?imageUrl=<image>`。</span><span class="sxs-lookup"><span data-stu-id="811e6-138">You should see the json response that the Face API returns when passed an image: `http://localhost:7071/api/MojifyImage?imageUrl=<image>`.</span></span>

    <span data-ttu-id="811e6-139">查看中[`shared/faceapi/index.ts`](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.tsazure-portal=true)的代码, 了解如何将来自面孔 API 的响应转换为对象数组的`Face`实例。</span><span class="sxs-lookup"><span data-stu-id="811e6-139">Look at the code in [`shared/faceapi/index.ts`](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.tsazure-portal=true) to see how the response from the Face API is being converted into an instance of an array of `Face` objects.</span></span> <span data-ttu-id="811e6-140">每`Face`个对象包含 emotive 坐标、图像表面的位置、匹配的表情符号以及表情符号图标。</span><span class="sxs-lookup"><span data-stu-id="811e6-140">Each `Face` object contains the emotive coordinates, the location of the face in the image, the matching emoji, and the emoji icon.</span></span>

1. <span data-ttu-id="811e6-141">创建 mojified 图像</span><span class="sxs-lookup"><span data-stu-id="811e6-141">Create the mojified image</span></span>

    <span data-ttu-id="811e6-142">接下来, 填写`createMojifiedImage(context, imageUrl, faces)` TypeScript 函数, 以创建由原始图像及其匹配的表情符号组成的复合图像。</span><span class="sxs-lookup"><span data-stu-id="811e6-142">Next, fill in the `createMojifiedImage(context, imageUrl, faces)` TypeScript function to create the composite image consisting of the original image along with its matching emoji(s).</span></span> <span data-ttu-id="811e6-143">此函数使用`Jimp` npm 包, 即开放源代码图像操作库。</span><span class="sxs-lookup"><span data-stu-id="811e6-143">This function uses the `Jimp` npm package, an open-source image manipulation library.</span></span>

    <span data-ttu-id="811e6-144">将此`TODO`函数中的行替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="811e6-144">Replace the `TODO` line in this function with the following code:</span></span>

    ```typescript
    let sourceImage = await Jimp.read(imageUrl);
    // Create a composite image, we will "append" to this composite an emoji image for each face found
    let compositeImage = sourceImage;

    if (faces.length == 0) {
      throw new Error(`No faces found in image`);
    }

    for (let face of faces) {
      const mojiName = face.mojiName;
      const faceHeight = face.faceRectangle.height;
      const faceWidth = face.faceRectangle.width;
      const faceTop = face.faceRectangle.top;
      const faceLeft = face.faceRectangle.left;

      // Load the emoji from disk
      let mojiPath = path.resolve(
        __dirname,
        "../shared/emojis/" + mojiName + ".png"
      );
      let emojiImage = await Jimp.read(mojiPath);

      // Resize the emoji to fit the face
      emojiImage.resize(faceWidth, faceHeight);

      // Compose the emoji on the image
      compositeImage = compositeImage.composite(emojiImage, faceLeft, faceTop);
    }

    try {
      return await compositeImage.getBufferAsync(Jimp.MIME_JPEG);
    } catch (error) {
      context.log(`There was an error adding the emoji to the image: ${error}`);
      throw new Error(error);
    }
    ```

    <span data-ttu-id="811e6-145">让我们分步分解此代码</span><span class="sxs-lookup"><span data-stu-id="811e6-145">Let's break this code down step by step</span></span>

    - <span data-ttu-id="811e6-146">若要使用 Jimp 加载图像, 请使用`Jimp.read`函数。</span><span class="sxs-lookup"><span data-stu-id="811e6-146">To load an image using Jimp, you use the `Jimp.read` function.</span></span>

        ```typescript
        let sourceImage = await Jimp.read(imageUrl);
        ```

    - <span data-ttu-id="811e6-147">中`shared/emojis`的每个表情符号都有一个 png 文件目录。</span><span class="sxs-lookup"><span data-stu-id="811e6-147">There is a directory of png files for each emoji in `shared/emojis`.</span></span>

    - <span data-ttu-id="811e6-148">对于图像中的每个面</span><span class="sxs-lookup"><span data-stu-id="811e6-148">For each face in the image</span></span>
        - <span data-ttu-id="811e6-149">加载表情图标</span><span class="sxs-lookup"><span data-stu-id="811e6-149">Load up the emoji image</span></span>

            ```typescript
            let mojiPath = path.resolve(
                __dirname,
                "../shared/emojis/" + mojiName + ".png"
            );
            let emojiImage = await Jimp.read(mojiPath);
            ```

        - <span data-ttu-id="811e6-150">将表情图标的大小调整为图像中找到的图符的大小</span><span class="sxs-lookup"><span data-stu-id="811e6-150">Resize the emoji image to the size of the face found in the image</span></span>

            ```typescript
            emojiImage.resize(faceWidth, faceHeight);
            ```

        - <span data-ttu-id="811e6-151">创建原始图像的复合图像和图像中的图符上调整后的表情符号</span><span class="sxs-lookup"><span data-stu-id="811e6-151">Create a composite image of the original image and the resized emoji located on the face in the image</span></span>

            ```typescript
            compositeImage = compositeImage.composite(emojiImage, faceLeft, faceTop);
            ```

    - <span data-ttu-id="811e6-152">将复合图像作为缓冲区返回</span><span class="sxs-lookup"><span data-stu-id="811e6-152">Return the composite image as a buffer</span></span>

        ```typescript
        try {
            return await compositeImage.getBufferAsync(Jimp.MIME_JPEG);
        } catch (error) {
            context.log(`There was an error adding the emoji to the image: ${error}`);
            throw new Error(error);
        }
        ```

1. <span data-ttu-id="811e6-153">在`index`函数中设置返回 HTTP 响应</span><span class="sxs-lookup"><span data-stu-id="811e6-153">Set up the return HTTP response in the `index` function</span></span>

    <span data-ttu-id="811e6-154">将以下代码添加到`index(context, req)` TypeScript 函数的顶部, 以配置 HTTP 响应:</span><span class="sxs-lookup"><span data-stu-id="811e6-154">Add the following code to the top of the `index(context, req)` TypeScript function to configure the HTTP response:</span></span>

    ```typescript
    context.res = {
        status: 200,
        headers: {
          "Content-Type": "image/jpeg"
        },
        isRaw: true
    };
    ```

1. <span data-ttu-id="811e6-155">从函数中添加调用, 将`try`块替换为: `index` `createMojifiedImage`</span><span class="sxs-lookup"><span data-stu-id="811e6-155">Add the call to `createMojifiedImage` from the `index` function, replacing the `try` block with:</span></span>

    ```typescript
    try {
      let faces = await FaceApi.getFaces(context, imageUrl);
      if (faces) {
        let buffer = await createMojifiedImage(context, imageUrl, faces);
        context.res.body = buffer;
        context.log(`Posted reply with mojified image`);
      } else {
        context.res = { status: 400, body: `Could not process image: ${imageUrl}` };
      }
    } catch (err) {
      let message = `There was an error processing this image: ${err.message}`;
      context.log(message);
      context.res = { status: 400, body: message };
    }
    ```

## <a name="try-it-out"></a><span data-ttu-id="811e6-156">试用</span><span class="sxs-lookup"><span data-stu-id="811e6-156">Try it out</span></span>

1. <span data-ttu-id="811e6-157">确保使用以前使用的方法之一运行本地 Azure 函数应用程序: 使用`func host start`或从 "调试" 菜单使用 "**附加到 JavaScript 函数**" 任务来运行它。</span><span class="sxs-lookup"><span data-stu-id="811e6-157">Make sure that the local Azure function application is running using one of the methods you previously used: either use `func host start` or run it from the debug menu using the **Attach to JavaScript Function** task.</span></span>

    <span data-ttu-id="811e6-158">如果函数应用程序正确启动, 则 "输出" 窗口应显示类似于以下输出的内容:</span><span class="sxs-lookup"><span data-stu-id="811e6-158">If the function app started correctly, then the output window should show something like this output:</span></span>

    ```
    Http Functions:
            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

1. <span data-ttu-id="811e6-159">访问浏览器中的 URL。</span><span class="sxs-lookup"><span data-stu-id="811e6-159">Visit the URL in your browser.</span></span> <span data-ttu-id="811e6-160">请记住通过`imageUrl`查询参数传入图像的 URL。</span><span class="sxs-lookup"><span data-stu-id="811e6-160">Remember to pass in the URL of an image via the `imageUrl` query parameter.</span></span>

1. <span data-ttu-id="811e6-161">它应返回图像的 mojified 版本。</span><span class="sxs-lookup"><span data-stu-id="811e6-161">It should return a mojified version of the image.</span></span>

    <span data-ttu-id="811e6-162">您已在 TypeScript 中编写 Azure 函数以 mojify 图像!</span><span class="sxs-lookup"><span data-stu-id="811e6-162">You've written an Azure function in TypeScript to mojify an image!</span></span> <span data-ttu-id="811e6-163">👏👏👏</span><span class="sxs-lookup"><span data-stu-id="811e6-163"></span></span>

    ![Mojified 图像](../media/4.mojified-image.png)
