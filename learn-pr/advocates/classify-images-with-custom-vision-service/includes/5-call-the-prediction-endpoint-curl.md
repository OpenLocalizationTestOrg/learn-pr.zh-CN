在上一个练习中, 我们使用自定义远景服务门户的**快速测试**功能测试我们的训练有素的模型。 这是使用一些测试图像快速检查模型准确性的极好方法。 接下来, 让我们通过 HTTP 对模型的预测终结点进行调用。

[!include[](../../../includes/azure-sandbox-activate.md)]

1. 返回到**Artworks** \*项目在自定义远景服务门户中, 选择 "**性能**" 选项卡。

    ![突出显示了 "性能" 选项卡的 Artworks 项目顶栏的屏幕截图](../media/5-performance-tab.png)

1. 选择 "**设为默认值**" 以确保模型的最新小版本是默认迭代。

1. 选择 "**预测 URL**"。 这将显示一个对话框, 其中显示了我们进行呼叫所需的信息。 

    !["预测 url" 对话框的屏幕截图, 显示有关如何在具有图像 url 和具有图像文件时使用预测 API 的详细信息的详细信息](../media/5-portal-prediction-url.png)

    如对话框中所示, 我们可以调用预测终结点并向其传递图像 URL。 我们还可以将 raw 图像传递给请求正文中的终结点。

    请记下此对话框中的三条信息。
     - **预测-键**: 必须在所有请求中将此键设置为标头。 这就是我们为我们提供对终结点的访问权限。
    - **请求 URL**: 对话框显示两个不同的 url。 如果要发布图像 URL, 请使用第一个 url, 该 url 以`/url`。 如果我们要在请求的正文中发布 raw 图像, 我们将使用第二个 URL, 该 URL 以`/image`。
    - **内容类型**: 如果我们要发布 raw 图像, 则将请求的正文设置为图像的二进制表示形式和内容类型`application/octet-stream`。 如果要发布图像 URL, 则将其作为 JSON 放置在正文中, 并将内容类型设置为`application/json`。
    

3. 从 "**如何使用预测 API** " 对话框`Prediction-Key`中复制并保存第一个 URL 和值。 

> [!TIP]
> "**卷曲**" 是一种命令行工具, 可用于发送或接收文件。 它包含在 Linux、macOS 和 Windows 10 中, 可以为大多数其他操作系统下载。 卷支持多种协议, 如 HTTP、HTTPS、FTP、FTPS、SFTP、LDAP、TELNET、SMTP、POP3 等。有关详细信息, 请参阅以下链接:
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/> 
> 
> 卷曲已安装在沙盒中的 Azure 云命令行管理程序中。 因此, 我们将在此练习中进行, 以对我们的终结点进行 HTTP 调用。

2. 在云命令行管理程序中执行以下命令。 将 **[endpoint url]** 替换为您在上一步中保存的 URL。 将 **[预测键]** 替换为`Prediction-Key`您在上一步中保存的值。 

    ```azurecli
    curl [endpoint-URL] \
    -H "Prediction-Key: [Prediction-Key]" \
    -H "Content-Type: application/json" \
    -d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/VanGoghTest_02.jpg'}" \
    | jq '.'
    ```

    命令完成后, 你将看到一个 JSON 响应, 类似于以下屏幕截图。 API 为模型中的每个标记返回一个概率。 正如您所看到的, 对于`"painting"` **tagName**值而言, 概率接近1的情况下, 此图像绝对是一种绘画。 不过, 我们对我们的模型进行过培训的任何艺术家不会进行绘制。 

    ![显示每个标记的概率的 JSON 响应的屏幕截图](../media/5-prediction-json.png) 

3. 通过使用下表中的 url 替换上面请求正文中的 url, 尝试更多预测。 

    |图像  | URL  |
    |---------|---------|
    |![测试 picasso 图像的缩略图](../media/picasso-test-02-thumb.jpg)     | `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PicassoTest_02.jpg`        |
    |![测试 rembrandt 图像的缩略图](../media/rembrandt-test-01-thumb.jpg)     |  `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/RembrandtTest_01.jpg`       |
    |![测试 pollock 图像的缩略图](../media/pollock-test-01-thumb.jpg)  |   `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PollockTest_01.jpg`     |
   

我们的预测终结点按预期工作。 调用 API 就像使用预测密钥和图像 URL 对终结点发出 HTTP 请求一样简单。
