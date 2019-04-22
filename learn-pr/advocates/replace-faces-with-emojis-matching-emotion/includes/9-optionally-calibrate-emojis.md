您不能将表情图标传递给面孔 API 以获得情感, 因为它不是人脸。 因此, 对于每个表情符号, 您需要一个 emotive 坐标。

我们使用了一个非常简单的方法来生成模块中的 emotive 坐标。 此方法

- 使用带有表情符号的表达式接近于的一个真实脸。 我们称之为代理映像。
- 通过 Azure 面孔 API 运行它
- 使用该操作的结果作为表情符号的 emotive 坐标

在此单元中, 我们将演示如何替换自己的代理图像, 并重新校准表情符号 emotive 坐标。

作为扩展, 您还可以设计更严格的方法来执行此映射, 例如, 通过对许多图像集进行培训。

## <a name="proxy-images"></a>代理映像

您可以在示例代码中查看`shared/proxy-images`文件夹中每个表情符号的代理图像列表。

![某些云开发人员支持的一组配对的图像, 使各种表现力在其匹配的 mojified 图像的旁边。](../media/team.jpg)

这些代理图像被传递给面孔 API 以生成 emotive 点, 然后与表情图标相关联。 您可以在源代码中的`MOJIS` `shared/models/mojis.ts`文件中的数组中查看所提供的代理映像集的结果。

## <a name="create-your-own-proxy-images-for-emojis"></a>为表情符号创建自己的代理映像

>[!NOTE]
> 如果愿意, 您可以使用自己的图像。 在可宽延时间工作的 mojify 或团队工作时, 可能会非常有趣!

如果您计划使用自己的图像, 请亲自可模拟`shared/proxy-images`文件夹中的每个表情符号并替换原始的图像集。

## <a name="create-an-azure-function-to-calibrate-your-proxy-images"></a>创建 Azure 函数以校准代理映像

就像对`MojifyImage`和`RespondToSlackCommand`函数执行的操作一样, 创建另一个名`Calibrate`为的函数。

将索引 .js 文件替换为名为 index 的文件, 并将以下代码复制到此文件中:

```typescript
import { EmotivePoint } from "../shared/models/emotivePoint";
import { Face } from "../shared/models/faces";
import * as FaceApi from "../shared/faceapi";
import * as emojiLookup from "emoji-dictionary";

const EMOJIS_TO_TRAIN = [
  "☺️",
  "🤓",
  "😃",
  "😆",
  "😉",
  "😍",
  "😎",
  "😐",
  "😕",
  "😖",
  "😘",
  "😜",
  "😝",
  "😠",
  "😧",
  "😩",
  "😬",
  "😭",
  "😱",
  "😳",
  "😴"
];

async function getCalibrationArrayString(context) {
  let str = "[";

  for (let emoji of EMOJIS_TO_TRAIN) {
    context.log(`Processing ${emoji}`);
    // Given an emoji like 😴 returns the word version, like 'sleepy'
    let emojiName = emojiLookup.getName(emoji);
    let emotion = await FaceApi.getEmotionFromLocalProxyImage(context, emojiName);
    let point = new EmotivePoint(emotion);
    let face = new Face(point, null);
    str += `{
        emotiveValues: new EmotivePoint({
            anger: ${emotion.anger},
            contempt: ${emotion.contempt},
            disgust: ${emotion.disgust},
            fear: ${emotion.fear},
            happiness: ${emotion.happiness},
            neutral: ${emotion.neutral},
            sadness: ${emotion.sadness},
            surprise: ${emotion.surprise}
        }),
        emojiIcon: "${emoji}"
      },`;
  }
  str += "]";
  return str;
}

export async function index(context, req) {
    context.log(`Calibrate HTTP trigger`);

    const array = await getCalibrationArrayString(context);
    const body = {MOJIS: array};

    context.res = {
      status: 200,
      headers: {
        "Content-Type": "application/json"
      },
      body: body
    };
}
```

## <a name="try-it-out"></a>试用

现在是有趣的部分吧! 我们将通过 "面孔 API" `shared/proxy-images`运行每个图像, 以在情绪空间中为该表情符号计算情绪点。

从 "调试" 菜单启动或从终端运行该函数应用程序, 以确保该函数应用程序正在运行。
```bash
func host start
```

通过连接到`Calibrate`以下内容运行新函数http://localhost:7071/api/Calibrate:。

> [!NOTE]
> 面孔 API 限制可调用的速度。 如果速率限制超过了该代码, 将等待30秒, 然后重试。 由于校准功能是快速连续发出呼叫, 因此可能会达到此速率限制, 并看到校准函数需要一分钟或两分钟才能执行。

命令的输出显示在浏览器窗口中, 作为 emotive 点的 json 数组。 您可以尝试不同的代理映像, 并查看 emotive 点中的变化。 您还可以将此数组重新复制`shared/models/mojis.ts`到中, 重新部署您的函数应用程序, 以便您在可宽延时间`/mojify`命令中使用自己的代理映像。
