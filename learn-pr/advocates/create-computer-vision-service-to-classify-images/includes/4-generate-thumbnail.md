<span data-ttu-id="471dc-101">产品的 Frontline 分销商扫描和上载商店货位的图像。</span><span class="sxs-lookup"><span data-stu-id="471dc-101">Frontline distributors of your products scan and upload images of store shelves they're restocking.</span></span> <span data-ttu-id="471dc-102">作为贵公司的开发人员主管, 您负责创建图像的缩略图。</span><span class="sxs-lookup"><span data-stu-id="471dc-102">As a lead developer at your company, you are responsible for creating thumbnails of the images.</span></span> <span data-ttu-id="471dc-103">缩略图在您为销售团队创建的联机报告中使用。</span><span class="sxs-lookup"><span data-stu-id="471dc-103">The thumbnails are used in the online reports you create for the sales team.</span></span> <span data-ttu-id="471dc-104">最近, 销售经理说, 报告中的图像模糊, 并且通常没有产品的前端和中心, 使扫描大型报告变得困难。</span><span class="sxs-lookup"><span data-stu-id="471dc-104">Recently, the sales manager said that the images in the report are blurry and often don't have the product front and center, making it difficult to scan the large report.</span></span> <span data-ttu-id="471dc-105">你将由你来改进这种情况。</span><span class="sxs-lookup"><span data-stu-id="471dc-105">It's up to you to improve the situation.</span></span>

<span data-ttu-id="471dc-106">您决定尝试计算机远景 API 的缩略图生成功能。</span><span class="sxs-lookup"><span data-stu-id="471dc-106">You decide to try the thumbnail generation feature of the Computer Vision API.</span></span> <span data-ttu-id="471dc-107">或许它可以执行比您编写的调整大小函数更好的工作。</span><span class="sxs-lookup"><span data-stu-id="471dc-107">Perhaps it can do a better job than the resizing function you wrote.</span></span>

<span data-ttu-id="471dc-108">计算机远景首先生成高质量的缩略图, 然后分析图像中的对象以确定感兴趣的区域 (ROI)。</span><span class="sxs-lookup"><span data-stu-id="471dc-108">Computer Vision first generates a high-quality thumbnail and then analyzes the objects within the image to determine the region of interest (ROI).</span></span> <span data-ttu-id="471dc-109">计算机远景然后裁剪图像以满足感兴趣的区域的要求。</span><span class="sxs-lookup"><span data-stu-id="471dc-109">Computer Vision then crops the image to fit the requirements of the region of interest.</span></span> <span data-ttu-id="471dc-110">根据您的需要, 可以使用与原始图像的纵横比不同的高宽比显示生成的缩略图。</span><span class="sxs-lookup"><span data-stu-id="471dc-110">The generated thumbnail can be presented using an aspect ratio that is different from the aspect ratio of the original image, depending on your needs.</span></span> <span data-ttu-id="471dc-111">让我们看看它在操作中。</span><span class="sxs-lookup"><span data-stu-id="471dc-111">Let's see it in action.</span></span>

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a><span data-ttu-id="471dc-112">调用计算机远景 API 以生成缩略图</span><span class="sxs-lookup"><span data-stu-id="471dc-112">Calling the Computer Vision API to generate a thumbnail</span></span>

<span data-ttu-id="471dc-113">该`generateThumbnail`操作将创建具有用户指定的宽度和高度的缩略图图像。</span><span class="sxs-lookup"><span data-stu-id="471dc-113">The `generateThumbnail` operation creates a thumbnail image with the user-specified width and height.</span></span> <span data-ttu-id="471dc-114">默认情况下, 该服务会分析图像, 标识感兴趣的区域 (ROI), 并基于 ROI 生成智能裁剪坐标。</span><span class="sxs-lookup"><span data-stu-id="471dc-114">By default, the service analyzes the image, identifies the region of interest (ROI), and generates smart cropping coordinates based on the ROI.</span></span> <span data-ttu-id="471dc-115">当您指定与输入图像的纵横比不同的纵横比时, 智能裁剪将会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="471dc-115">Smart cropping helps when you specify an aspect ratio that differs from aspect ratio of the input image.</span></span> <span data-ttu-id="471dc-116">请求 URL 的格式如下:</span><span class="sxs-lookup"><span data-stu-id="471dc-116">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=<...>&height=<...>&smartCropping=<...>`

<span data-ttu-id="471dc-117">可以向 API 提供不同的参数, 以生成适当的缩略图来满足您的需求。</span><span class="sxs-lookup"><span data-stu-id="471dc-117">Different parameters can be provided to the API to generate the proper thumbnail for your needs.</span></span> <span data-ttu-id="471dc-118">和`width` `height`参数是必需的。</span><span class="sxs-lookup"><span data-stu-id="471dc-118">The `width` and `height` parameters are required.</span></span> <span data-ttu-id="471dc-119">它们告诉 API 您需要用于特定图像的大小。</span><span class="sxs-lookup"><span data-stu-id="471dc-119">They tell the API which size you need for a specific image.</span></span> <span data-ttu-id="471dc-120">`smartCropping`参数通过分析图像中感兴趣的区域以将其保留在缩略图中, 从而生成更智能的裁剪。</span><span class="sxs-lookup"><span data-stu-id="471dc-120">The `smartCropping` parameter generates smarter cropping by analyzing the region of interest in your image to keep it within the thumbnail.</span></span> <span data-ttu-id="471dc-121">例如, 在启用智能裁剪的情况下, 裁剪的配置文件图片会使某人在图片框架中的表面保持不被使用, 即使该图片的纵横比较不同也是如此。</span><span class="sxs-lookup"><span data-stu-id="471dc-121">As an example, with smart cropping enabled, a cropped profile picture would keep someone's face within the picture frame even when the picture has a different aspect ratio.</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a><span data-ttu-id="471dc-122">生成缩略图</span><span class="sxs-lookup"><span data-stu-id="471dc-122">Generate a thumbnail</span></span>

<span data-ttu-id="471dc-123">我们将在此示例中使用下面的图像, 但你可以随时尝试使用指向其他图像的 url 的相同命令。</span><span class="sxs-lookup"><span data-stu-id="471dc-123">We'll use the following image in this example, but you're free to try the same command with URLs to other images.</span></span>

![一种可爱的白色狗坐在绿色草地中的图片。](../media/4-dog.png)

1. <span data-ttu-id="471dc-125">在 Azure 云命令行管理程序中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="471dc-125">Execute the following commands in Azure Cloud Shell.</span></span> <span data-ttu-id="471dc-126">在`<region>`命令中使用您的认知服务帐户的区域进行替换</span><span class="sxs-lookup"><span data-stu-id="471dc-126">Replace `<region>` in the command with the region of your cognitive services account</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

<span data-ttu-id="471dc-127">在此示例中, 我们要求服务创建一个100x100 的缩略图。</span><span class="sxs-lookup"><span data-stu-id="471dc-127">In this example, we ask the service to create a thumbnail that is 100x100.</span></span> <span data-ttu-id="471dc-128">启用智能裁剪。</span><span class="sxs-lookup"><span data-stu-id="471dc-128">Smart cropping is enabled.</span></span> <span data-ttu-id="471dc-129">成功的响应包含缩略图图像二进制, 我们会将其写入到名为 ".jpg" 的文件中。</span><span class="sxs-lookup"><span data-stu-id="471dc-129">A successful response contains the thumbnail image binary, which we write to a file called thumbnail.jpg.</span></span>

> [!CAUTION]
> <span data-ttu-id="471dc-130">`-o`参数将输出重定向到文件。</span><span class="sxs-lookup"><span data-stu-id="471dc-130">The `-o` parameter redirects the output to a file.</span></span> <span data-ttu-id="471dc-131">始终会覆盖该文件, 因此, 如果您想要在尝试此命令时保留多个缩略图, 请更改文件名。</span><span class="sxs-lookup"><span data-stu-id="471dc-131">The file is always overwritten, so if you want to keep around  more than one thumbnail while trying this command, change the file name.</span></span>

## <a name="view-the-generated-thumbnail"></a><span data-ttu-id="471dc-132">查看生成的缩略图</span><span class="sxs-lookup"><span data-stu-id="471dc-132">View the generated thumbnail</span></span>

<span data-ttu-id="471dc-133">将在你的 Azure 云 Shell 存储帐户中找到生成的缩略图。</span><span class="sxs-lookup"><span data-stu-id="471dc-133">The generated thumbnail will be found in your Azure Cloud Shell storage account.</span></span> <span data-ttu-id="471dc-134">已将文件**缩略图**命名为 .jpg。</span><span class="sxs-lookup"><span data-stu-id="471dc-134">We named the file **thumbnail.jpg**.</span></span>

<span data-ttu-id="471dc-135">Microsoft 学习中的云命令行管理程序无法下载文件, 但您可以按照这些说明操作, 通过 Azure 门户下载缩略图。</span><span class="sxs-lookup"><span data-stu-id="471dc-135">The Cloud Shell in Microsoft Learn doesn't have the ability to download files, but you can follow these instructions to download the thumbnail through the Azure portal.</span></span>

1. <span data-ttu-id="471dc-136">在 Azure 云命令行管理程序中执行以下命令, 以确认您的主文件夹中存在文件**缩略图。**</span><span class="sxs-lookup"><span data-stu-id="471dc-136">Execute the following commands in Azure Cloud Shell to confirm that the file **thumbnail.jpg** exists in your home folder.</span></span>

    ```azurecli
    cd ~
    ls -l
    ```



1. <span data-ttu-id="471dc-137">执行以下命令以移动`thumbnail.jpg`到 clouddrive 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="471dc-137">Execute the following command to move `thumbnail.jpg` into the clouddrive folder.</span></span>

    ```azurecli
    mv ~/thumbnail.jpg ~/clouddrive
    ```
1. <span data-ttu-id="471dc-138">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="471dc-138">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>
1. <span data-ttu-id="471dc-139">在 "门户" 仪表板的 "**所有资源**" 面板中, 选择名称以开头`cloudshell`的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="471dc-139">In the **All resources** panel of the portal dashboard, select the storage account with name beginning with `cloudshell`.</span></span>
1. <span data-ttu-id="471dc-140">在 "存储帐户" 面板中, 依次选择 "**存储资源管理器**"、"**文件共享**" 和该集合中的文件共享 (以**cloudshellfiles**开头的名称)。</span><span class="sxs-lookup"><span data-stu-id="471dc-140">In the Storage account panel, select **Storage Explorer**, then **FILE SHARES** and then the file share in that collection with the name beginning with **cloudshellfiles**.</span></span>
1. <span data-ttu-id="471dc-141">选择 " *thunbnail* " 文件, 然后从顶部菜单中进行**下载**以查看图像。</span><span class="sxs-lookup"><span data-stu-id="471dc-141">Select the *thunbnail.jpg* file and then **Download** from the top menu to see the image.</span></span>

<span data-ttu-id="471dc-142">该`generateThumbnail`操作是功能强大的缩略图生成器, 能够在缩略图中保持图像的感兴趣 (ROI)。</span><span class="sxs-lookup"><span data-stu-id="471dc-142">The `generateThumbnail` operation is a powerful thumbnail generator that is capable of keeping the Region Of Interest (ROI) of an image in the thumbnail.</span></span>

<span data-ttu-id="471dc-143">有关此`generateThumbnails`操作的详细信息, 请参阅[获取缩略图](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb)参考文档。</span><span class="sxs-lookup"><span data-stu-id="471dc-143">For more information about the `generateThumbnails` operation, see the [Get Thumbnail](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) reference documentation.</span></span>
