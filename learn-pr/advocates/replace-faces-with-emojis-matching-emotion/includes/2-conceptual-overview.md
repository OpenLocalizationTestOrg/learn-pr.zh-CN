在您开始设置和编写代码之前, 有一些高级问题值得回答。

## <a name="how-do-you-map-an-emotion-to-an-emoji"></a>如何将表情映射到表情符号？

假设只有两个感受、恐惧和幸福, 值范围从0到1。 这使您可以根据用户的情感在 2d_情绪空间_中绘制任何面, 如下所示:

![简单的图形。 "幸福" 位于 y 轴上, 恐惧在 x 轴上, 并且从 "引入单位" 开始的人脸的同一个样本图像在空白区域中绘制了约 1/4, 3/4 在右边。](../media/graph-1.jpg)

您可以使用它来计算每个表情符号的情绪点, 就像您对表面的一样。 在2d 情绪空间中绘制表情符号后, 您可以确定哪个表情符号与图片中的情感最近最接近。

![上图的更新版本显示了不同的表情符号, 并在 "幸福" 和 "恐惧" 尺度上绘制了不同的点。 其中一些包括带有眼睛的微笑的表情符号, 并在恐惧轴上增加了 "幸福" 轴、"恐惧轴上" 的 nervous 表情符号和 "幸福" 轴上更低的表情符号, 以及在害怕上哭泣的表情符号较低的幸福。](../media/graph-2.png)

此计算称为_Euclidian 距离_。 您不会只在2d 空间中使用此图, 而是在8D 中使用。激动人心的空间, 衡量 anger、contempt、disgust、恐惧、幸福、中性、sadness 和惊喜。

> [!Tip]
> 为了更轻松地使用名为 "[欧式](https://www.npmjs.com/package/euclidean-distance?azure-portal=true)" 的 npm 包。

## <a name="how-do-you-calculate-the-emotion-of-a-face"></a>如何计算面孔的情感？

### <a name="the-face-api"></a>面孔 API

计算情感是令人吃惊的应用程序中最易访问的部件之一。 Azure 认知服务[面孔 API](https://azure.microsoft.com/services/cognitive-services/face?azure-portal=true)采用图像输入, 并返回其相关信息, 包括是否检测到面孔及其位置。 如果请求, 它也会计算并返回感受的外观, 如下所示:

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

获取此图像的实例:

![女士脸的 closeup 图像。 她有褐色的头发, 在眼镜中, 正如在查看器中直接查看。](../media/example-face.jpg)

若要处理此图像, 请向 API 终结点发出 POST 请求, 如下所示:

 https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion

您可以在正文中提供图像:

```json
{
  "url": "<path-to-image>"
}
```

> [!Note]
> 默认情况下, API 不会返回情感。 您需要显式指定查询参数`returnFaceAttributes=emotion`。

使用密钥对 API 进行身份验证。 您需要使用标头发送此键。

```
Ocp-Apim-Subscription-Key: <your-subscription-key>
```

具有上述查询参数的 API 将返回 JSON, 如下所示:

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

它返回结果的数组-在图像中检测到的每个面一个。 每个结果都包含表面的大小和位置`faceRectangle` , 感受表示`faceAttributes`为从0到1的数字。

在[Mojifier 代码](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/faceapi/index.ts?azure-portal=true)存储库中, 将对面孔 API 的调用打包为您的便利函数。

### <a name="emotivepoint-class"></a>EmotivePoint 类

如果仔细查看`EmotivePoint` [shared/emotivePoint](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/models/emotivePoint.ts?azure-portal=true)中的类, 您会注意到一些事项。

构造函数采用包含 emotive 信息作为输入的对象, 并将其存储为局部成员变量, 如下所示:

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

它也有一个函数被`distance`调用, 我们可以使用它来计算两个 emotive 点之间的欧式距离, 如下所示:

```typescript
  distance(other) {
    let myPoint = this.toArray();
    let otherPoint = other.toArray();
    return distance(myPoint, otherPoint);
  }
```

使用此信息, 您可以创建两个 emotive 点, 并计算它们的接近程度:

```typescript
let a = new EmotivePoint({
  /* ... */
});
let b = new EmotivePoint({
  /* ... */
});
let distance = a.distance(b);
```

### <a name="face-class"></a>面孔类

另一个帮助程序类`Face`是类, 它组合了几个不同的属性`EmotivePoint` , 包括表盘和`Rect`类, 这是定义表盘边界的矩形。

如果检查`Face` [shared/面孔](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/models/faces.ts?azure-portal=true)中的类构造函数, 您将看到以下代码行:

```typescript
this.moji = this.chooseMoji(this.emotivePoint);
```

- `emotivePoint`是表面的 emotive 点。
- `chooseMoji`根据字型返回适当`emotivePoint`的表情符号。

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

- `MOJIS`是所有表情符号的 emotive 坐标的列表。 这些都是从设置每个表情符号的接近于感受[代理映像](https://github.com/MicrosoftDocs/mslearn-the-mojifier/blob/master/shared/proxy-images?azure-portal=true)中生成的。 您可以生成自己的代理映像集, 并在本模块后面校准表情符号的情绪坐标集, 作为可选步骤。
- `chooseMoji`函数计算此表面和表情符号之间的距离, 并返回最接近的距离。
