你已在本地开发了两个 Azure 函数。 现在让我们让你的本地功能在云中运行, 以便可以从时差中调用它们。

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-function-app-on-azure"></a>在 azure 上创建 azure 函数应用

首先, 通过使用 VS Code 和 azure 函数扩展创建 azure Function App。

1. 依次单击 "**查看**" 和 "**命令组件面板**", 然后选择 " **Azure 函数: 部署到函数应用程序**"。

   ![在 VS 代码顶部部署到 "函数应用程序" 对话框。](../media/7.deploy-to-function-app.png)

2. 确认要上载当前项目。

   ![选择要部署的文件夹。 您还可以通过在演示应用文件夹下选择 "浏览" 来浏览其他文件夹 (如果尚未打开)。](../media/7.select-folder-to-deploy.png)

3. 选择**Concierge 订阅**沙盒订阅。

4. 选择 " **+ 新建函数应用程序**"。

   ![创建新的 Function App 对话框。](../media/7.create-new-function-app.png)

5. 命名您的应用程序。 选择一个全局唯一名称。 我们将使用**mojifier-可宽延的函数-应用程序**。

   ![使用之前键入的名称选择 "应用程序名称" 对话框。](../media/7.choose-app-name.png)

6. 选择您的资源组。 Azure 沙盒已创建一个可放置您的资源的_资源组_。 资源组名称为**<rgn>[沙盒资源组名称]</rgn>**。

7. 选择与沙盒关联的存储帐户。

8. 上载完成后, "输出" 窗口应显示 URL。

    ```output
    Deployment to "mojifier-slack-function-app" completed.
    HTTP Trigger Urls:
      MojifyImage: https://mojifier-slack-function-app.azurewebsites.net/api/MojifyImage
      RespondToSlackCommand: https://mojifier-slack-function-app.azurewebsites.net/api/ResponsToSlackCommand
    ```

## <a name="try-it-out"></a>试用

由于函数不依赖`RespondToSlackCommand`于任何其他依赖项, 因此应认为该函数正常工作。

请

```bash
<deployed-app-name>.azurewebsites.net/api/RespondToSlackCommand
```

您应该会看到返回的一些 json。

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "https://mojifier-slack.azurewebsites.net/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```

## <a name="upload-settings"></a>上载设置

请记住, 我们会将一些设置放`local.settings.json`在中。 这些设置是认知服务的密钥和 URL。 由于`local.settings.json`是本地的, 因此在部署时不会将其复制到生产环境中。

通常情况下, 需要打开 Azure 门户并在 UI 中手动添加设置, 或在 Azure CLI 中`func`使用。 由于您使用的是 VS 代码, 因此您可以使用 Azure 函数扩展和命令选项板上传本地设置!

1. 依次单击 "**查看**" 和 "**命令组件面板**" 和 " **Azure 函数: 上传本地设置**"。

    ![在 VS 代码中上载本地设置对话框。 它显示 ">upload local"。](../media/7.upload-local-settings.png)

2. 选择`local.settings.json`。

    ![从文件列表中选择 "本地设置"。](../media/7.choose-localsettings.png)

3. 选择与您的函数关联的订阅。

4. 选择要将设置上载到的函数应用程序。 在此示例中, 它称为 " **mojifier-可宽延功能-应用程序**"。

## <a name="try-it-out"></a>试用

如果一切按预期方式工作, 则 MojifyImage 终结点应正常工作。 请

```bash
https:<deployed-app-name>.azurewebsites.net/api/MojifyImage?imageUrl=<image-url>
```

您应该会在窗口中看到 mojified 图像。
