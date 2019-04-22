<span data-ttu-id="52372-101">在您开始设置和编写代码之前, 有一些高级问题值得回答。</span><span class="sxs-lookup"><span data-stu-id="52372-101">There's some high-level questions worth answering before you get into setting up and writing code.</span></span>

## <a name="how-do-you-map-an-emotion-to-an-emoji"></a><span data-ttu-id="52372-102">如何将表情映射到表情符号？</span><span class="sxs-lookup"><span data-stu-id="52372-102">How do you map an emotion to an emoji?</span></span>

<span data-ttu-id="52372-103">假设只有两个感受、恐惧和幸福, 值范围从0到1。</span><span class="sxs-lookup"><span data-stu-id="52372-103">Imagine there were only two emotions, fear and happiness, with values ranging from 0 to 1.</span></span> <span data-ttu-id="52372-104">这使您可以根据用户的情感在 2d_情绪空间_中绘制任何面, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="52372-104">This lets you plot any face in a 2D _emotional space_ based on the emotion of the user, like so:</span></span>

![简单的图形。](../media/graph-1.jpg)

<span data-ttu-id="52372-107">您可以使用它来计算每个表情符号的情绪点, 就像您对表面的一样。</span><span class="sxs-lookup"><span data-stu-id="52372-107">You can use this to figure out the emotional point for each emoji just like you did for the face.</span></span> <span data-ttu-id="52372-108">在2d 情绪空间中绘制表情符号后, 您可以确定哪个表情符号与图片中的情感最近最接近。</span><span class="sxs-lookup"><span data-stu-id="52372-108">After you plot the emojis in the 2D emotional space, you can figure out which emoji is closest to the emotion in the picture.</span></span>

![上图的更新版本显示了不同的表情符号, 并在 "幸福" 和 "恐惧" 尺度上绘制了不同的点。](../media/graph-2.png)

<span data-ttu-id="52372-111">此计算称为_Euclidian 距离_。</span><span class="sxs-lookup"><span data-stu-id="52372-111">This calculation is called the _Euclidian distance_.</span></span> <span data-ttu-id="52372-112">您不会只在2d 空间中使用此图, 而是在8D 中使用。激动人心的空间, 衡量 anger、contempt、disgust、恐惧、幸福、中性、sadness 和惊喜。</span><span class="sxs-lookup"><span data-stu-id="52372-112">You won't just use this in a 2D space, but rather in an 8D emotional space, measuring anger, contempt, disgust, fear, happiness, neutral, sadness, and surprise.</span></span>

> [!Tip]
> <span data-ttu-id="52372-113">为了更轻松地使用名为 "[欧式](https://www.npmjs.com/package/euclidean-distance?azure-portal=true)" 的 npm 包。</span><span class="sxs-lookup"><span data-stu-id="52372-113">To make like easier we used the npm package called [euclidean-distance](https://www.npmjs.com/package/euclidean-distance?azure-portal=true).</span></span>

## <a name="how-do-you-calculate-the-emotion-of-a-face"></a><span data-ttu-id="52372-114">如何计算面孔的情感？</span><span class="sxs-lookup"><span data-stu-id="52372-114">How do you calculate the emotion of a face?</span></span>

### <a name="the-face-api"></a><span data-ttu-id="52372-115">面孔 API</span><span class="sxs-lookup"><span data-stu-id="52372-115">The Face API</span></span>

<span data-ttu-id="52372-116">计算情感是令人吃惊的应用程序中最易访问的部件之一。</span><span class="sxs-lookup"><span data-stu-id="52372-116">Calculating emotion is, surprisingly, one of the most accessible parts of your app.</span></span> <span data-ttu-id="52372-117">Azure 认知服务[面孔 API](https://azure.microsoft.com/services/cognitive-services/face?azure-portal=true)采用图像输入, 并返回其相关信息, 包括是否检测到面孔及其位置。</span><span class="sxs-lookup"><span data-stu-id="52372-117">The Azure Cognitive Services [Face API](https://azure.microsoft.com/services/cognitive-services/face?azure-portal=true) takes image input and returns information about it, including whether a face was detected and its location.</span></span> <span data-ttu-id="52372-118">如果请求, 它也会计算并返回感受的外观, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="52372-118">If requested, it calculates and returns the emotions of the faces as well, like so:</span></span>

```json
{
  "anger": 0.572,
  "contempt": 0.025,
  "disgust": 0.242,
  "fear": 0.001,
  "happiness": 0.014,
  "neutral": 0.111,
  "sadness": 0.033,
  "surprise": 0.003
}
```

<span data-ttu-id="52372-119">获取此图像的实例:</span><span class="sxs-lookup"><span data-stu-id="52372-119">Take for instance this image:</span></span>

![女士脸的 closeup 图像。](../media/example-face.jpg)

<span data-ttu-id="52372-122">若要处理此图像, 请向 API 终结点发出 POST 请求, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="52372-122">To process this image, you make a POST request to an API endpoint, like this one:</span></span>

 https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion

<span data-ttu-id="52372-123">您可以在正文中提供图像:</span><span class="sxs-lookup"><span data-stu-id="52372-123">You provide the image in the body:</span></span>

```json
{
  "url": "<path-to-image>"
}
```

> [!Note]
> <span data-ttu-id="52372-124">默认情况下, API 不会返回情感。</span><span class="sxs-lookup"><span data-stu-id="52372-124">The API doesn’t return the emotion by default.</span></span> <span data-ttu-id="52372-125">您需要显式指定查询参数`returnFaceAttributes=emotion`。</span><span class="sxs-lookup"><span data-stu-id="52372-125">You need to explicitly specify the query parameter `returnFaceAttributes=emotion`.</span></span>

<span data-ttu-id="52372-126">使用密钥对 API 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="52372-126">The use of a secret key authenticates the API.</span></span> <span data-ttu-id="52372-127">您需要使用标头发送此键。</span><span class="sxs-lookup"><span data-stu-id="52372-127">You need to send this key with the header.</span></span>

```
Ocp-Apim-Subscription-Key: <your-subscription-key>
```

<span data-ttu-id="52372-128">具有上述查询参数的 API 将返回 JSON, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="52372-128">The API with the query parameters above would return a JSON, like so:</span></span>

```json
[
  {
    "faceRectangle": {
      "top": 207,
      "left": 198,
      "width": 229,
      "height": 229
    },
    "faceAttributes": {
      "emotion": {
        "anger": 0.001,
        "contempt": 0.014,
        "disgust": 0,
        "fear": 0,
        "happiness": 0.306,
        "neutral": 0.675,
        "sadness": 0.003,
        "surprise": 0.001
      }
    }
  }
]
```

<span data-ttu-id="52372-129">它返回结果的数组-在图像中检测到的每个面一个。</span><span class="sxs-lookup"><span data-stu-id="52372-129">It returns an array of results - one per face detected in the image.</span></span> <span data-ttu-id="52372-130">每个结果都包含表面的大小和位置`faceRectangle` , 感受表示`faceAttributes`为从0到1的数字。</span><span class="sxs-lookup"><span data-stu-id="52372-130">Each result contains the size and location of the face as `faceRectangle` and the emotions represented as `faceAttributes` as a number from 0 to 1.</span></span>

<span data-ttu-id="52372-131">在[Mojifier 代码](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.ts?azure-portal=true)存储库中, 将对面孔 API 的调用打包为您的便利函数。</span><span class="sxs-lookup"><span data-stu-id="52372-131">The calls to the Face API are wrapped into convenience functions for you in the [Mojifier code repo](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.ts?azure-portal=true)</span></span>

### <a name="emotivepoint-class"></a><span data-ttu-id="52372-132">EmotivePoint 类</span><span class="sxs-lookup"><span data-stu-id="52372-132">EmotivePoint class</span></span>

<span data-ttu-id="52372-133">如果仔细查看`EmotivePoint` [shared/emotivePoint](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/models/emotivePoint.ts?azure-portal=true)中的类, 您会注意到一些事项。</span><span class="sxs-lookup"><span data-stu-id="52372-133">If you look closely at the `EmotivePoint` class in [shared/emotivePoint.ts](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/models/emotivePoint.ts?azure-portal=true), you will notice a few things.</span></span>

<span data-ttu-id="52372-134">构造函数采用包含 emotive 信息作为输入的对象, 并将其存储为局部成员变量, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="52372-134">The constructor takes an object containing emotive information as input and stores it as local member variables, like so:</span></span>

```typescript
 constructor({
    anger,
    contempt,
    disgust,
    fear,
    happiness,
    neutral,
    sadness,
    surprise
  }) {
    this.anger = anger;
    this.contempt = contempt;
    this.disgust = disgust;
    this.fear = fear;
    this.happiness = happiness;
    this.neutral = neutral;
    this.sadness = sadness;
    this.surprise = surprise;
  }
```

<span data-ttu-id="52372-135">它也有一个函数被`distance`调用, 我们可以使用它来计算两个 emotive 点之间的欧式距离, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="52372-135">It also has a function called `distance`, which we can use to calculate the Euclidean distance between two emotive points, like so:</span></span>

```typescript
  distance(other) {
    let myPoint = this.toArray();
    let otherPoint = other.toArray();
    return distance(myPoint, otherPoint);
  }
```

<span data-ttu-id="52372-136">使用此信息, 您可以创建两个 emotive 点, 并计算它们的接近程度:</span><span class="sxs-lookup"><span data-stu-id="52372-136">Using this information, you can create two emotive points and calculate how close they are:</span></span>

```typescript
let a = new EmotivePoint({
  /* ... */
});
let b = new EmotivePoint({
  /* ... */
});
let distance = a.distance(b);
```

### <a name="face-class"></a><span data-ttu-id="52372-137">面孔类</span><span class="sxs-lookup"><span data-stu-id="52372-137">Face class</span></span>

<span data-ttu-id="52372-138">另一个帮助程序类`Face`是类, 它组合了几个不同的属性`EmotivePoint` , 包括表盘和`Rect`类, 这是定义表盘边界的矩形。</span><span class="sxs-lookup"><span data-stu-id="52372-138">Another helper class is the `Face` class, which combines a few different properties, including the `EmotivePoint` of a face and the `Rect` class, which is the rectangle that defines the boundaries of the face.</span></span>

<span data-ttu-id="52372-139">如果检查`Face` [shared/面孔](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/models/faces.ts?azure-portal=true)中的类构造函数, 您将看到以下代码行:</span><span class="sxs-lookup"><span data-stu-id="52372-139">If you review the `Face` class constructor in [shared/face.ts](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/models/faces.ts?azure-portal=true), you'll see this line of code:</span></span>

```typescript
this.moji = this.chooseMoji(this.emotivePoint);
```

- <span data-ttu-id="52372-140">`emotivePoint`是表面的 emotive 点。</span><span class="sxs-lookup"><span data-stu-id="52372-140">`emotivePoint` is the emotive point of the face itself.</span></span>
- <span data-ttu-id="52372-141">`chooseMoji`根据字型返回适当`emotivePoint`的表情符号。</span><span class="sxs-lookup"><span data-stu-id="52372-141">`chooseMoji` returns an appropriate emoji based on the `emotivePoint` of the face.</span></span>

```typescript
  chooseMoji(point) {
    let closestMoji = null;
    let closestDistance = Number.MAX_VALUE;
    for (let moji of MOJIS) {
      let emoPoint = moji.emotiveValues;
      let distance = emoPoint.distance(point);
      if (distance < closestDistance) {
        closestMoji = moji;
        closestDistance = distance;
      }
    }
    return closestMoji;
  }
```

- <span data-ttu-id="52372-142">`MOJIS`是所有表情符号的 emotive 坐标的列表。</span><span class="sxs-lookup"><span data-stu-id="52372-142">`MOJIS` is the list of emotive coordinates for all the emojis.</span></span> <span data-ttu-id="52372-143">这些都是从设置每个表情符号的接近于感受[代理映像](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/proxy-images?azure-portal=true)中生成的。</span><span class="sxs-lookup"><span data-stu-id="52372-143">These are generated from a set a [proxy images](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/proxy-images?azure-portal=true) approximating the emotions of each emoji.</span></span> <span data-ttu-id="52372-144">您可以生成自己的代理映像集, 并在本模块后面校准表情符号的情绪坐标集, 作为可选步骤。</span><span class="sxs-lookup"><span data-stu-id="52372-144">You can generate your own set of proxy images and calibrate the set of emoji emotional coordinates later in this module, as an optional step.</span></span>
- <span data-ttu-id="52372-145">`chooseMoji`函数计算此表面和表情符号之间的距离, 并返回最接近的距离。</span><span class="sxs-lookup"><span data-stu-id="52372-145">The `chooseMoji` function calculates the distance between this face and the emojis, returning the closest one.</span></span>
