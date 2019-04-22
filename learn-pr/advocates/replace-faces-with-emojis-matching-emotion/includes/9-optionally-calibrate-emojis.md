<span data-ttu-id="c82da-101">您不能将表情图标传递给面孔 API 以获得情感, 因为它不是人脸。</span><span class="sxs-lookup"><span data-stu-id="c82da-101">You can’t pass an image of the emoji to the Face API to get its emotion because it's not a human face.</span></span> <span data-ttu-id="c82da-102">因此, 对于每个表情符号, 您需要一个 emotive 坐标。</span><span class="sxs-lookup"><span data-stu-id="c82da-102">So for each emoji, you need an emotive coordinate.</span></span>

<span data-ttu-id="c82da-103">我们使用了一个非常简单的方法来生成模块中的 emotive 坐标。</span><span class="sxs-lookup"><span data-stu-id="c82da-103">We have used a very simple method of generating emotive coordinates in the module.</span></span> <span data-ttu-id="c82da-104">此方法</span><span class="sxs-lookup"><span data-stu-id="c82da-104">This method</span></span>

- <span data-ttu-id="c82da-105">使用带有表情符号的表达式接近于的一个真实脸。</span><span class="sxs-lookup"><span data-stu-id="c82da-105">Takes one real face with an expression approximating that of the emoji.</span></span> <span data-ttu-id="c82da-106">我们称之为代理映像。</span><span class="sxs-lookup"><span data-stu-id="c82da-106">We call this the proxy image.</span></span>
- <span data-ttu-id="c82da-107">通过 Azure 面孔 API 运行它</span><span class="sxs-lookup"><span data-stu-id="c82da-107">Runs it through the Azure Face API</span></span>
- <span data-ttu-id="c82da-108">使用该操作的结果作为表情符号的 emotive 坐标</span><span class="sxs-lookup"><span data-stu-id="c82da-108">Uses the result of that operation as the emotive coordinates for the emoji</span></span>

<span data-ttu-id="c82da-109">在此单元中, 我们将演示如何替换自己的代理图像, 并重新校准表情符号 emotive 坐标。</span><span class="sxs-lookup"><span data-stu-id="c82da-109">In this unit, we demonstrate how you can substitute your own proxy images, and re-calibrate the emoji emotive coordinates.</span></span>

<span data-ttu-id="c82da-110">作为扩展, 您还可以设计更严格的方法来执行此映射, 例如, 通过对许多图像集进行培训。</span><span class="sxs-lookup"><span data-stu-id="c82da-110">As an extension, you could also devise more a more rigorous method of performing this mapping, by training with many sets of images, for example.</span></span>

## <a name="proxy-images"></a><span data-ttu-id="c82da-111">代理映像</span><span class="sxs-lookup"><span data-stu-id="c82da-111">Proxy Images</span></span>

<span data-ttu-id="c82da-112">您可以在示例代码中查看`shared/proxy-images`文件夹中每个表情符号的代理图像列表。</span><span class="sxs-lookup"><span data-stu-id="c82da-112">You can see the list of proxy images for each emoji in the `shared/proxy-images` folder in the sample code.</span></span>

![某些云开发人员支持的一组配对的图像, 使各种表现力在其匹配的 mojified 图像的旁边。](../media/team.jpg)

<span data-ttu-id="c82da-114">这些代理图像被传递给面孔 API 以生成 emotive 点, 然后与表情图标相关联。</span><span class="sxs-lookup"><span data-stu-id="c82da-114">These proxy images were passed to the Face API to generate emotive points, which were then associated with an emoji image.</span></span> <span data-ttu-id="c82da-115">您可以在源代码中的`MOJIS` `shared/models/mojis.ts`文件中的数组中查看所提供的代理映像集的结果。</span><span class="sxs-lookup"><span data-stu-id="c82da-115">You can see the results of the supplied set of proxy images in the `MOJIS` array in the `shared/models/mojis.ts` file in the source code.</span></span>

## <a name="create-your-own-proxy-images-for-emojis"></a><span data-ttu-id="c82da-116">为表情符号创建自己的代理映像</span><span class="sxs-lookup"><span data-stu-id="c82da-116">Create your own proxy images for emojis</span></span>

>[!NOTE]
> <span data-ttu-id="c82da-117">如果愿意, 您可以使用自己的图像。</span><span class="sxs-lookup"><span data-stu-id="c82da-117">You can use your own images if you prefer.</span></span> <span data-ttu-id="c82da-118">在可宽延时间工作的 mojify 或团队工作时, 可能会非常有趣!</span><span class="sxs-lookup"><span data-stu-id="c82da-118">It can be fun to mojify yourself or your teammates at work in Slack!</span></span>

<span data-ttu-id="c82da-119">如果您计划使用自己的图像, 请亲自可模拟`shared/proxy-images`文件夹中的每个表情符号并替换原始的图像集。</span><span class="sxs-lookup"><span data-stu-id="c82da-119">If you plan to use your own images, then take a picture of yourself mimicking each emoji in the `shared/proxy-images` folder and replace the original set of images.</span></span>

## <a name="create-an-azure-function-to-calibrate-your-proxy-images"></a><span data-ttu-id="c82da-120">创建 Azure 函数以校准代理映像</span><span class="sxs-lookup"><span data-stu-id="c82da-120">Create an Azure function to calibrate your proxy images</span></span>

<span data-ttu-id="c82da-121">就像对`MojifyImage`和`RespondToSlackCommand`函数执行的操作一样, 创建另一个名`Calibrate`为的函数。</span><span class="sxs-lookup"><span data-stu-id="c82da-121">Just as you did for the `MojifyImage` and the `RespondToSlackCommand` function, create another function called `Calibrate`.</span></span>

<span data-ttu-id="c82da-122">将索引 .js 文件替换为名为 index 的文件, 并将以下代码复制到此文件中:</span><span class="sxs-lookup"><span data-stu-id="c82da-122">Replace the index.js file with a file called index.ts, and copy the following code into this file:</span></span>

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

## <a name="try-it-out"></a><span data-ttu-id="c82da-123">试用</span><span class="sxs-lookup"><span data-stu-id="c82da-123">Try it out</span></span>

<span data-ttu-id="c82da-124">现在是有趣的部分吧!</span><span class="sxs-lookup"><span data-stu-id="c82da-124">Now comes the fun part!</span></span> <span data-ttu-id="c82da-125">我们将通过 "面孔 API" `shared/proxy-images`运行每个图像, 以在情绪空间中为该表情符号计算情绪点。</span><span class="sxs-lookup"><span data-stu-id="c82da-125">We are going to run each of the images in the `shared/proxy-images` through the Face API to calculate an emotional point for that emoji in emotional space.</span></span>

<span data-ttu-id="c82da-126">从 "调试" 菜单启动或从终端运行该函数应用程序, 以确保该函数应用程序正在运行。</span><span class="sxs-lookup"><span data-stu-id="c82da-126">Make sure the function app is running by starting it from the debug menu or running it from the terminal.</span></span>
```bash
func host start
```

<span data-ttu-id="c82da-127">通过连接到`Calibrate`以下内容运行新函数http://localhost:7071/api/Calibrate:。</span><span class="sxs-lookup"><span data-stu-id="c82da-127">Run the new `Calibrate` function by connecting to: http://localhost:7071/api/Calibrate.</span></span>

> [!NOTE]
> <span data-ttu-id="c82da-128">面孔 API 限制可调用的速度。</span><span class="sxs-lookup"><span data-stu-id="c82da-128">The Face API restricts the rate at which it can be called.</span></span> <span data-ttu-id="c82da-129">如果速率限制超过了该代码, 将等待30秒, 然后重试。</span><span class="sxs-lookup"><span data-stu-id="c82da-129">If the rate limit is exceed the code will wait 30 seconds and try again.</span></span> <span data-ttu-id="c82da-130">由于校准功能是快速连续发出呼叫, 因此可能会达到此速率限制, 并看到校准函数需要一分钟或两分钟才能执行。</span><span class="sxs-lookup"><span data-stu-id="c82da-130">Since the calibrate function is make calls in quick succession you may hit this rate limit, and see that the Calibrate function takes a minute or two to execute.</span></span>

<span data-ttu-id="c82da-131">命令的输出显示在浏览器窗口中, 作为 emotive 点的 json 数组。</span><span class="sxs-lookup"><span data-stu-id="c82da-131">The output of the command is displayed in your browser window, as json array of emotive points.</span></span> <span data-ttu-id="c82da-132">您可以尝试不同的代理映像, 并查看 emotive 点中的变化。</span><span class="sxs-lookup"><span data-stu-id="c82da-132">You can try out different proxy images, and see the change in the emotive points.</span></span> <span data-ttu-id="c82da-133">您还可以将此数组重新复制`shared/models/mojis.ts`到中, 重新部署您的函数应用程序, 以便您在可宽延时间`/mojify`命令中使用自己的代理映像。</span><span class="sxs-lookup"><span data-stu-id="c82da-133">You can also copy this array back into `shared/models/mojis.ts`, redeploy your function app, so that you are using your own proxy images in your slack `/mojify` command.</span></span>
