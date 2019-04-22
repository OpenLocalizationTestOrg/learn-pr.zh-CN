
## <a name="what-is-microsoft-cognitive-services"></a>什么是 Microsoft 认知服务？

Microsoft 认知服务是一组可用作任何用户使用的服务的机器学习算法。 我们可以使用这些服务进行远景、语音、语言、知识和搜索, 而无需从头开始为我们的应用构建此智能。 你可以免费试用每个服务。 在决定将服务集成到您的应用程序时, 请注册付费订阅。 我们将重点关注此模型中的计算机远景 API。

> [!TIP]
> 若要查看所有认知服务的列表, 请查看[认知服务目录](https://azure.microsoft.com/services/cognitive-services/directory/)。 

## <a name="what-is-the-computer-vision-api"></a>什么是计算机远景 API？

计算机远景 API 提供用于处理图像和返回见解的算法。 例如, 您可以找出某个图像是否包含成人内容, 或能否使用它来查找图像中的所有表面。 它还具有其他功能, 如估计主要和强调颜色、使用完整的英文句子对图像内容进行分类以及描述图像。 此外, 它还可以智能地生成图像缩略图, 以有效显示大图像。

> [!TIP]
> 计算机远景 API 在全球范围内提供了许多区域。 若要查找离你最近的地区, 请参阅[按地区提供的产品](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all)。

您可以使用计算机远景 API 执行以下操作:

- 分析图像的洞察力
- 使用光学字符识别 (OCR) 从图像中提取打印的文本。
- 从图像中识别打印的和手写的文本
- 识别 celebrities 和使
- 分析视频 
- 生成图像的缩略图 

## <a name="how-to-call-the-computer-vision-api"></a>如何调用计算机远景 API

您可以使用客户端库或 REST API 直接调用应用程序中的计算机远景。 我们将在此模块中调用 REST API。 拨打电话:

1. 获取 API 访问密钥

    注册计算机远景服务帐户时, 系统会向你分配访问密钥。 必须在**每个**请求的标头中传递一个键。 

1. 向 API 发出 POST 调用

    设置 URL 格式, 如下所**** 示: api.cognitive.microsoft.com/vision/v2.0/**资源**/**[parameters]** 

    - **region** -您在其中创建帐户的区域, 例如, *westus*。
    - **resource** -你正在呼叫的计算机远景资源`analyze`, `describe` `generateThumbnail` `ocr` `models`如、、、、、 `recognizeText`、 `tag`。

    您可以提供要作为原始图像二进制文件或图像 URL 处理的图像。

    请求标头必须包含订阅密钥, 该密钥提供对此 API 的访问权限。

1. 分析响应

    该响应包含计算机远景 API 对你的图像的见解, 作为 JSON 有效负载。

在本模块中, 我们将使用集成云命令行管理程序运行 Azure CLI 中的所有练习。 让我们进一步了解一下此设置。

## <a name="what-is-the-azure-cli"></a>什么是 Azure CLI

azure CLI 是 Microsoft 的用于管理 Azure 资源的跨平台命令行工具。 它可用于 macOS、Linux 和 Windows, 也可用于使用[Azure 云命令行](https://docs.microsoft.com/azure/cloud-shell/overview)管理程序的浏览器。

> [!IMPORTANT]
> 有两个版本的 azure cli 工具现已推出: azure cli 1.0 和 Azure cli 2.0。 我们将使用 Azure CLI 2.0, 它是最新版本, 建议使用, 除非您运行的是旧版脚本。 azure cli 1.0 是通过`azure`命令启动的, 并且使用`az`命令启动 azure cli 2.0。

## <a name="az-cognitiveservices-commands"></a>az cognitiveservices 命令

azure CLI 包含用于管理`cognitiveservices` Azure 中的认知服务帐户的命令。 我们可以提供几个子命令来完成特定任务。 最常见的包括:

| 子命令 | 说明 |
|-------------|-------------|
| `list` | 列出可用的 Azure 认知服务帐户。 |
| `account show` | 获取 Azure 认知服务帐户的详细信息。 |
| `account create` | 创建 Azure 认知服务帐户。 |
| `account delete` | 删除 Azure 认知服务帐户。 |
| `keys list` | 列出 Azure 认知服务帐户的密钥。 |

让我们在 Azure CLI 中创建一个认知服务。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a>创建认知服务帐户

我们需要一个 API 访问密钥来调用计算机远景 API。 若要获取访问密钥, 我们需要一个适用于计算机远景 API 的认知服务帐户。 我们将使用`az cognitiveservices create`在订阅中创建帐户。

 该命令`az cognitiveservices create`用于在资源组中创建认知服务帐户。  调用此命令时, 必须提供以下五个参数。

> [!Tip]
> 大多数 Azure CLI 参数的标志都可以缩写为单个字符。 例如, 我们可以说`-l` , 而不`--location`是。 为清楚起见, 使用长格式。

| 参数 | 说明 |
|-----------|-------------|
| `resource-group` | 将拥有认知服务帐户的资源组。 在此交互式沙盒会话中, 将使用<rgn>[沙盒资源组名称]</rgn> |
| `kind` | 认知服务帐户的 API 名称。 |
| `name` | 认知服务帐户名称。 |
| `sku` | 认知服务帐户的 Sku。|
| `location` | 要从中调用此 API 的位置或区域。 从以下列表中选择一个位置。 |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

在 Azure 云命令行管理程序中执行以下命令。 请务必将替换`[location]`为你附近的位置。

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--name ComputerVisionService \
--sku S1 \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--location [location]
```

> [!NOTE]
> 记住您选择的位置。 你将从该区域对 API 进行所有调用。

我们为**ComputerVision** API 创建了一个认知服务帐户。 我们选择了*S1* sku 并命名为 "我们的帐户**ComputerVisionService**"。 我们的帐户归资源组**<rgn>[沙盒资源组名称]</rgn>** 所有, 我们将从在`--location`参数中设置的位置调用 API。 

命令完成创建认知服务帐户后, 您将获得 JSON 响应, 其中包括设置为 "**成功**" 的**provisioningState**属性。

## <a name="get-an-access-key"></a>获取访问键

成功创建帐户后, 我们可以为此帐户检索订阅密钥或访问密钥。

1. 在 Azure 云命令行管理程序中执行以下命令:

    ```azurecli
    az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn>
    ```
    
    上面的命令返回与认知服务帐户 (名为**ComputerVisionService**) 相关联的键, 该帐户归给定资源组所有。 它返回两个键: 一个是备用密钥。 这些项很难记住, 因此我们将把第一个关键字存储在一个变量中, 我们将使用此变量对 API 的所有调用。

2.  在 Azure 云命令行管理程序中执行以下命令:

    ```azurecli
    key=$(az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query key1 -o tsv)
    ```
    
    Azure CLI 2.0 使用`--query`参数对命令结果执行 JMESPath 查询。 JMESPath 是 JSON 的查询语言, 使您能够从 CLI 输出中选择和呈现数据。 这些查询在 JSON 输出上对任何显示格式执行。
    Azure `--query` CLI 中的所有命令都支持该参数。 
    
    在我们的示例中, 我们将查询名为 "key1" 的项的键列表, 并将结果输出到**tsv**格式。 此格式将删除字符串值周围的引号。 我们将结果分配给一个变量**键**。
    
    > [!IMPORTANT]
    > 我们打算在整个模块中使用此项, 因此最好将其保存在变量中。 如果丢失了值或变量变为未设置, 则再次运行该命令以进行设置。  

3. 若要查看我们的键的值, 请在 Azure 云命令行管理程序中执行以下命令:

    ```azurecli
    echo $key
    ```

现在我们已拥有帐户和密钥, 接下来是要对 API 进行一些调用。