<span data-ttu-id="4e683-101">在上一个练习中, 我们使用自定义远景服务门户的**快速测试**功能测试我们的训练有素的模型。</span><span class="sxs-lookup"><span data-stu-id="4e683-101">In the last exercise, we tested our trained model using the **Quick Test** feature of the Custom Vision Service portal.</span></span> <span data-ttu-id="4e683-102">这是使用一些测试图像快速检查模型准确性的极好方法。</span><span class="sxs-lookup"><span data-stu-id="4e683-102">This is a great way to quickly check the accuracy of the model with some test images.</span></span> <span data-ttu-id="4e683-103">接下来, 让我们通过 HTTP 对模型的预测终结点进行调用。</span><span class="sxs-lookup"><span data-stu-id="4e683-103">Let's go a little further and make calls to the prediction endpoint of our model over HTTP.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

1. <span data-ttu-id="4e683-104">返回到**Artworks** \*项目在自定义远景服务门户中, 选择 "**性能**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="4e683-104">Returning to your **Artworks**\* project in the Custom Vision Service portal, select the  **Performance** tab.</span></span>

    ![突出显示了 "性能" 选项卡的 Artworks 项目顶栏的屏幕截图](../media/5-performance-tab.png)

1. <span data-ttu-id="4e683-106">选择 "**设为默认值**" 以确保模型的最新小版本是默认迭代。</span><span class="sxs-lookup"><span data-stu-id="4e683-106">Select **Make default** to make sure the latest iteration of the model is the default iteration.</span></span>

1. <span data-ttu-id="4e683-107">选择 "**预测 URL**"。</span><span class="sxs-lookup"><span data-stu-id="4e683-107">Select **Prediction URL**.</span></span> <span data-ttu-id="4e683-108">这将显示一个对话框, 其中显示了我们进行呼叫所需的信息。</span><span class="sxs-lookup"><span data-stu-id="4e683-108">This displays a dialog of the information we need to make our calls.</span></span> 

    !["预测 url" 对话框的屏幕截图, 显示有关如何在具有图像 url 和具有图像文件时使用预测 API 的详细信息的详细信息](../media/5-portal-prediction-url.png)

    <span data-ttu-id="4e683-110">如对话框中所示, 我们可以调用预测终结点并向其传递图像 URL。</span><span class="sxs-lookup"><span data-stu-id="4e683-110">As the dialog shows, we can call the prediction endpoint and pass it an image URL.</span></span> <span data-ttu-id="4e683-111">我们还可以将 raw 图像传递给请求正文中的终结点。</span><span class="sxs-lookup"><span data-stu-id="4e683-111">We can also pass a raw image to the endpoint in the body of the request.</span></span>

    <span data-ttu-id="4e683-112">请记下此对话框中的三条信息。</span><span class="sxs-lookup"><span data-stu-id="4e683-112">Take note of three pieces of information from this dialog.</span></span>
     - <span data-ttu-id="4e683-113">**预测-键**: 必须在所有请求中将此键设置为标头。</span><span class="sxs-lookup"><span data-stu-id="4e683-113">**Prediction-Key**: This key has to be set as a header in all requests.</span></span> <span data-ttu-id="4e683-114">这就是我们为我们提供对终结点的访问权限。</span><span class="sxs-lookup"><span data-stu-id="4e683-114">That's what gives us access to the endpoint.</span></span>
    - <span data-ttu-id="4e683-115">**请求 URL**: 对话框显示两个不同的 url。</span><span class="sxs-lookup"><span data-stu-id="4e683-115">**Request URL**: The dialog shows two different URLs.</span></span> <span data-ttu-id="4e683-116">如果要发布图像 URL, 请使用第一个 url, 该 url 以`/url`。</span><span class="sxs-lookup"><span data-stu-id="4e683-116">If we're posting an image URL, then use the first URL, which ends in `/url`.</span></span> <span data-ttu-id="4e683-117">如果我们要在请求的正文中发布 raw 图像, 我们将使用第二个 URL, 该 URL 以`/image`。</span><span class="sxs-lookup"><span data-stu-id="4e683-117">If we want to post a raw image in the body of our request, we use the second URL, which ends in `/image`.</span></span>
    - <span data-ttu-id="4e683-118">**内容类型**: 如果我们要发布 raw 图像, 则将请求的正文设置为图像的二进制表示形式和内容类型`application/octet-stream`。</span><span class="sxs-lookup"><span data-stu-id="4e683-118">**Content-Type**: If we're posting a raw image, we set the body of the request to the binary representation of the image and the content type to `application/octet-stream`.</span></span> <span data-ttu-id="4e683-119">如果要发布图像 URL, 则将其作为 JSON 放置在正文中, 并将内容类型设置为`application/json`。</span><span class="sxs-lookup"><span data-stu-id="4e683-119">If we're posting an image URL, we put that as JSON in the body and set the content type to `application/json`.</span></span>
    

3. <span data-ttu-id="4e683-120">从 "**如何使用预测 API** " 对话框`Prediction-Key`中复制并保存第一个 URL 和值。</span><span class="sxs-lookup"><span data-stu-id="4e683-120">Copy and save the first URL and the `Prediction-Key` value from the **How to use the Prediction API** dialog.</span></span> 

> [!TIP]
> <span data-ttu-id="4e683-121">"**卷曲**" 是一种命令行工具, 可用于发送或接收文件。</span><span class="sxs-lookup"><span data-stu-id="4e683-121">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="4e683-122">它包含在 Linux、macOS 和 Windows 10 中, 可以为大多数其他操作系统下载。</span><span class="sxs-lookup"><span data-stu-id="4e683-122">It's included with Linux, macOS, and Windows 10, and can be downloaded for most other operating systems.</span></span> <span data-ttu-id="4e683-123">卷支持多种协议, 如 HTTP、HTTPS、FTP、FTPS、SFTP、LDAP、TELNET、SMTP、POP3 等。有关详细信息, 请参阅以下链接:</span><span class="sxs-lookup"><span data-stu-id="4e683-123">cURL supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3, etc. For more information, refer to the links below:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/> 
> 
> <span data-ttu-id="4e683-124">卷曲已安装在沙盒中的 Azure 云命令行管理程序中。</span><span class="sxs-lookup"><span data-stu-id="4e683-124">cURL is already installed in the Azure Cloud Shell in the sandbox.</span></span> <span data-ttu-id="4e683-125">因此, 我们将在此练习中进行, 以对我们的终结点进行 HTTP 调用。</span><span class="sxs-lookup"><span data-stu-id="4e683-125">So, we'll cURL in this exercise to make HTTP calls to our endpoint.</span></span>

2. <span data-ttu-id="4e683-126">在云命令行管理程序中执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="4e683-126">Execute the following command in the Cloud Shell.</span></span> <span data-ttu-id="4e683-127">将 **[endpoint url]** 替换为您在上一步中保存的 URL。</span><span class="sxs-lookup"><span data-stu-id="4e683-127">Replace **[endpoint-URL]** with the URL you saved from the last step.</span></span> <span data-ttu-id="4e683-128">将 **[预测键]** 替换为`Prediction-Key`您在上一步中保存的值。</span><span class="sxs-lookup"><span data-stu-id="4e683-128">Replace **[Prediction-Key]** with the value of `Prediction-Key` you saved from the last step.</span></span> 

    ```azurecli
    curl [endpoint-URL] \
    -H "Prediction-Key: [Prediction-Key]" \
    -H "Content-Type: application/json" \
    -d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/VanGoghTest_02.jpg'}" \
    | jq '.'
    ```

    <span data-ttu-id="4e683-129">命令完成后, 你将看到一个 JSON 响应, 类似于以下屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="4e683-129">When the command completes, you'll see a JSON response similar to the following screenshot.</span></span> <span data-ttu-id="4e683-130">API 为模型中的每个标记返回一个概率。</span><span class="sxs-lookup"><span data-stu-id="4e683-130">The API returns a probability for every tag in the model.</span></span> <span data-ttu-id="4e683-131">正如您所看到的, 对于`"painting"` **tagName**值而言, 概率接近1的情况下, 此图像绝对是一种绘画。</span><span class="sxs-lookup"><span data-stu-id="4e683-131">As you can see, with a probability close to 1 for the `"painting"` **tagName** value, this image is definitely a painting.</span></span> <span data-ttu-id="4e683-132">不过, 我们对我们的模型进行过培训的任何艺术家不会进行绘制。</span><span class="sxs-lookup"><span data-stu-id="4e683-132">However, it's not a painting by any of the artists with which we trained our model.</span></span> 

    ![显示每个标记的概率的 JSON 响应的屏幕截图](../media/5-prediction-json.png) 

3. <span data-ttu-id="4e683-134">通过使用下表中的 url 替换上面请求正文中的 url, 尝试更多预测。</span><span class="sxs-lookup"><span data-stu-id="4e683-134">Try more predictions by replacing the URL in the request body above, with the URLs in the following table.</span></span> 

    |<span data-ttu-id="4e683-135">图像</span><span class="sxs-lookup"><span data-stu-id="4e683-135">Image</span></span>  | <span data-ttu-id="4e683-136">URL</span><span class="sxs-lookup"><span data-stu-id="4e683-136">URL</span></span>  |
    |---------|---------|
    |![测试 picasso 图像的缩略图](../media/picasso-test-02-thumb.jpg)     | `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PicassoTest_02.jpg`        |
    |![测试 rembrandt 图像的缩略图](../media/rembrandt-test-01-thumb.jpg)     |  `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/RembrandtTest_01.jpg`       |
    |![测试 pollock 图像的缩略图](../media/pollock-test-01-thumb.jpg)  |   `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PollockTest_01.jpg`     |
   

<span data-ttu-id="4e683-140">我们的预测终结点按预期工作。</span><span class="sxs-lookup"><span data-stu-id="4e683-140">Our prediction endpoint is working as expected.</span></span> <span data-ttu-id="4e683-141">调用 API 就像使用预测密钥和图像 URL 对终结点发出 HTTP 请求一样简单。</span><span class="sxs-lookup"><span data-stu-id="4e683-141">Calling the API is as simple as making a HTTP request to the endpoint with a Prediction-Key and an image URL.</span></span>
