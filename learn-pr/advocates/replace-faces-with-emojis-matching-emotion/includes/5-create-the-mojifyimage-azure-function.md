现在, 您已创建了 azure function 项目和最低 JavaScript Azure 函数, 你将在 TypeScript 中开发此 azure 函数。 final 函数将从其查询参数中读取图像 URL, 使用表面 API 在图像中查找表面及其感受, 然后将这些面替换为匹配的表情符号 (s)。 它返回此复合图像作为 raw 图像数据。

## <a name="convert-to-typescript"></a>转换为 TypeScript

Azure 函数扩展创建了一个 JavaScript 函数。 我们需要将其转换为 TypeScript。

1. 将`index.js`文件重命名为`index.ts`

    > [!NOTE]
    > 如果您正在运行`npm run build`和相关`tsc -w`命令, 则`index.ts`文件将立即编译为。 `index.js` 它还应创建一个`index.js.map`文件。 如果和`index.js` `index.js.map`文件不是自动创建的, 请检查`npm run build`命令是否正在运行, 并且输出不显示任何错误。

1. 将中`index.ts`的代码替换为以下代码:

    ```typescript
    export async function index(context, req) {
      context.log("ReplyWithMojifiedImage HTTP trigger");
      context.res.body = "Hello!";
    }
    ```

    > [!NOTE]
    > 使用`context.log` Azure 函数而不是`console.log`将输出记录到控制台。

## <a name="test-your-function"></a>测试函数

1. 确保使用以前使用的方法之一运行本地 Azure function 应用程序: 使用`func host start`或从 "调试" 菜单使用 "**附加到 JavaScript 函数**" 任务运行它。

    如果函数应用程序正确启动, 则 "输出" 窗口应显示类似于以下输出的内容:

    ```
    Http Functions:
            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

1. 访问浏览器中的 URL。 如果一切正常, 它应打印出来`Hello!`。

    如果看到`Hello`, 您已将函数触发器从 TypeScript 转换为 JavaScript。

## <a name="configure-your-face-api-environment-variables"></a>配置你的面孔 API 环境变量

为了提高代码的安全性, 您不应在代码中对私有数据进行硬编码。 而是使用环境变量来存储面孔 API URL 和密钥。

在创建 Azure 函数项目时, 它会创建一个名`local.settings.json`为的文件。 此文件位于`.gitignore`文件中, 因此未签入到源代码管理中。 它是存储不希望发布的敏感或本地配置的位置。 将对象中`Values`的任何内容作为环境变量提供给 node.js 代码。

1. 在`local.settings.json` Visual Studio Code 中打开。 默认情况下, 该文件包含以下内容:

    ```json
    {
      "IsEncrypted": false,
      "Values": {
        "AzureWebJobsStorage": "",
        "FUNCTIONS_WORKER_RUNTIME": "node"
      }
    }
    ```

1. 将此文件的内容**替换**为你的面孔 API 变量 (即, 删除该文件中的默认设置)。 创建面孔`<face-api-url>` API `<face-api-key>` Azure 资源时, 请将和值替换为您保存的变量。

    ```json
    {
        "Values": {
          "FACE_API_URL": "<face-api-url>",
          "FACE_API_KEY": "<face-api-key>"
        }
    }
    ```

`FACE_API_URL`和`FACE_API_KEY`变量将作为环境变量提供给 node.js。

在对[面孔 API 的调用](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.ts)中使用这些变量

## <a name="write-the-mojifyimage-function"></a>编写 MojifyImage 函数

1. 将中`MojifyImage/index.ts`的代码替换为以下代码:

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

    你将在此单元`createMojifiedImage`中开发函数`index`和函数。

1. 使用图像调用面孔 API 并获取响应

    将`index(context, req)` `index.ts`文件中的函数正文替换为以下代码。

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

1. 在浏览器中运行此函数

    在传递图像时, 您应该会看到表面 API 返回的 json 响应: `http://localhost:7071/api/MojifyImage?imageUrl=<image>`。

    查看中[`shared/faceapi/index.ts`](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.tsazure-portal=true)的代码, 了解如何将来自面孔 API 的响应转换为对象数组的`Face`实例。 每`Face`个对象包含 emotive 坐标、图像表面的位置、匹配的表情符号以及表情符号图标。

1. 创建 mojified 图像

    接下来, 填写`createMojifiedImage(context, imageUrl, faces)` TypeScript 函数, 以创建由原始图像及其匹配的表情符号组成的复合图像。 此函数使用`Jimp` npm 包, 即开放源代码图像操作库。

    将此`TODO`函数中的行替换为以下代码:

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

    让我们分步分解此代码

    - 若要使用 Jimp 加载图像, 请使用`Jimp.read`函数。

        ```typescript
        let sourceImage = await Jimp.read(imageUrl);
        ```

    - 中`shared/emojis`的每个表情符号都有一个 png 文件目录。

    - 对于图像中的每个面
        - 加载表情图标

            ```typescript
            let mojiPath = path.resolve(
                __dirname,
                "../shared/emojis/" + mojiName + ".png"
            );
            let emojiImage = await Jimp.read(mojiPath);
            ```

        - 将表情图标的大小调整为图像中找到的图符的大小

            ```typescript
            emojiImage.resize(faceWidth, faceHeight);
            ```

        - 创建原始图像的复合图像和图像中的图符上调整后的表情符号

            ```typescript
            compositeImage = compositeImage.composite(emojiImage, faceLeft, faceTop);
            ```

    - 将复合图像作为缓冲区返回

        ```typescript
        try {
            return await compositeImage.getBufferAsync(Jimp.MIME_JPEG);
        } catch (error) {
            context.log(`There was an error adding the emoji to the image: ${error}`);
            throw new Error(error);
        }
        ```

1. 在`index`函数中设置返回 HTTP 响应

    将以下代码添加到`index(context, req)` TypeScript 函数的顶部, 以配置 HTTP 响应:

    ```typescript
    context.res = {
        status: 200,
        headers: {
          "Content-Type": "image/jpeg"
        },
        isRaw: true
    };
    ```

1. 从函数中添加调用, 将`try`块替换为: `index` `createMojifiedImage`

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

## <a name="try-it-out"></a>试用

1. 确保使用以前使用的方法之一运行本地 Azure 函数应用程序: 使用`func host start`或从 "调试" 菜单使用 "**附加到 JavaScript 函数**" 任务来运行它。

    如果函数应用程序正确启动, 则 "输出" 窗口应显示类似于以下输出的内容:

    ```
    Http Functions:
            MojifyImage: http://localhost:7071/api/MojifyImage
    ```

1. 访问浏览器中的 URL。 请记住通过`imageUrl`查询参数传入图像的 URL。

1. 它应返回图像的 mojified 版本。

    您已在 TypeScript 中编写 Azure 函数以 mojify 图像! 👏👏👏

    ![Mojified 图像](../media/4.mojified-image.png)
