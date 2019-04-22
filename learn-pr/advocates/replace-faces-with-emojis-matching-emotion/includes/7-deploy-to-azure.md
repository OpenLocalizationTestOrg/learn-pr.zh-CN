<span data-ttu-id="2ddc2-101">你已在本地开发了两个 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-101">You've developed two Azure functions locally.</span></span> <span data-ttu-id="2ddc2-102">现在让我们让你的本地功能在云中运行, 以便可以从时差中调用它们。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-102">Let's now get your local functions running in the cloud so that you can call them from Slack.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-function-app-on-azure"></a><span data-ttu-id="2ddc2-103">在 azure 上创建 azure 函数应用</span><span class="sxs-lookup"><span data-stu-id="2ddc2-103">Create an Azure Function App on Azure</span></span>

<span data-ttu-id="2ddc2-104">首先, 通过使用 VS Code 和 azure 函数扩展创建 azure Function App。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-104">You're going to start by creating the Azure Function App using VS Code, and the Azure Functions extension.</span></span>

1. <span data-ttu-id="2ddc2-105">依次单击 "**查看**" 和 "**命令组件面板**", 然后选择 " **Azure 函数: 部署到函数应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-105">Click on **View** then **Command Palette** and select **Azure Function: Deploy to Function App**.</span></span>

   ![在 VS 代码顶部部署到 "函数应用程序" 对话框。](../media/7.deploy-to-function-app.png)

2. <span data-ttu-id="2ddc2-107">确认要上载当前项目。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-107">Confirm that you want to upload the current project.</span></span>

   ![选择要部署的文件夹。](../media/7.select-folder-to-deploy.png)

3. <span data-ttu-id="2ddc2-110">选择**Concierge 订阅**沙盒订阅。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-110">Choose the **Concierge Subscription** sandbox subscription.</span></span>

4. <span data-ttu-id="2ddc2-111">选择 " **+ 新建函数应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-111">Choose **+Create New Function App**.</span></span>

   ![创建新的 Function App 对话框。](../media/7.create-new-function-app.png)

5. <span data-ttu-id="2ddc2-113">命名您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-113">Name your app.</span></span> <span data-ttu-id="2ddc2-114">选择一个全局唯一名称。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-114">Select a globally unique name.</span></span> <span data-ttu-id="2ddc2-115">我们将使用**mojifier-可宽延的函数-应用程序**。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-115">We'll use **mojifier-slack-function-app**.</span></span>

   ![使用之前键入的名称选择 "应用程序名称" 对话框。](../media/7.choose-app-name.png)

6. <span data-ttu-id="2ddc2-117">选择您的资源组。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-117">Select your resource group.</span></span> <span data-ttu-id="2ddc2-118">Azure 沙盒已创建一个可放置您的资源的_资源组_。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-118">The Azure sandbox has created a _resource group_ into which can place your resources.</span></span> <span data-ttu-id="2ddc2-119">资源组名称为**<rgn>[沙盒资源组名称]</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-119">The resource group name is **<rgn>[sandbox resource group name]</rgn>**.</span></span>

7. <span data-ttu-id="2ddc2-120">选择与沙盒关联的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-120">Choose the storage account associated with the sandbox.</span></span>

8. <span data-ttu-id="2ddc2-121">上载完成后, "输出" 窗口应显示 URL。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-121">Once the upload completes, the output window should show a URL.</span></span>

    ```output
    Deployment to "mojifier-slack-function-app" completed.
    HTTP Trigger Urls:
      MojifyImage: https://mojifier-slack-function-app.azurewebsites.net/api/MojifyImage
      RespondToSlackCommand: https://mojifier-slack-function-app.azurewebsites.net/api/ResponsToSlackCommand
    ```

## <a name="try-it-out"></a><span data-ttu-id="2ddc2-122">试用</span><span class="sxs-lookup"><span data-stu-id="2ddc2-122">Try it out</span></span>

<span data-ttu-id="2ddc2-123">由于函数不依赖`RespondToSlackCommand`于任何其他依赖项, 因此应认为该函数正常工作。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-123">You should expect the `RespondToSlackCommand` function to work since it doesn't rely on any other dependencies.</span></span>

<span data-ttu-id="2ddc2-124">请</span><span class="sxs-lookup"><span data-stu-id="2ddc2-124">Visit</span></span>

```bash
<deployed-app-name>.azurewebsites.net/api/RespondToSlackCommand
```

<span data-ttu-id="2ddc2-125">您应该会看到返回的一些 json。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-125">You should see some json returned.</span></span>

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

## <a name="upload-settings"></a><span data-ttu-id="2ddc2-126">上载设置</span><span class="sxs-lookup"><span data-stu-id="2ddc2-126">Upload settings</span></span>

<span data-ttu-id="2ddc2-127">请记住, 我们会将一些设置放`local.settings.json`在中。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-127">Remember, you have some settings we put in `local.settings.json`.</span></span> <span data-ttu-id="2ddc2-128">这些设置是认知服务的密钥和 URL。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-128">These settings were the keys and URL for Cognitive Services.</span></span> <span data-ttu-id="2ddc2-129">由于`local.settings.json`是本地的, 因此在部署时不会将其复制到生产环境中。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-129">Since `local.settings.json` is local, it's never copied to production when you deploy.</span></span>

<span data-ttu-id="2ddc2-130">通常情况下, 需要打开 Azure 门户并在 UI 中手动添加设置, 或在 Azure CLI 中`func`使用。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-130">Usually, you would need to open the Azure portal and manually add the settings in the UI, or use `func` in the Azure CLI.</span></span> <span data-ttu-id="2ddc2-131">由于您使用的是 VS 代码, 因此您可以使用 Azure 函数扩展和命令选项板上传本地设置!</span><span class="sxs-lookup"><span data-stu-id="2ddc2-131">Since you're using VS Code, you can use the Azure Function extension and the command palette to upload your local settings!</span></span>

1. <span data-ttu-id="2ddc2-132">依次单击 "**查看**" 和 "**命令组件面板**" 和 " **Azure 函数: 上传本地设置**"。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-132">Click on **View** then **Command Palette** and select **Azure Functions: Upload Local Settings**.</span></span>

    ![在 VS 代码中上载本地设置对话框。](../media/7.upload-local-settings.png)

2. <span data-ttu-id="2ddc2-135">选择`local.settings.json`。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-135">Choose `local.settings.json`.</span></span>

    ![从文件列表中选择 "本地设置"。](../media/7.choose-localsettings.png)

3. <span data-ttu-id="2ddc2-137">选择与您的函数关联的订阅。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-137">Choose the subscription that's associated with your function.</span></span>

4. <span data-ttu-id="2ddc2-138">选择要将设置上载到的函数应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-138">Select the function app that you want to upload settings to.</span></span> <span data-ttu-id="2ddc2-139">在此示例中, 它称为 " **mojifier-可宽延功能-应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-139">In the example, it's called **mojifier-slack-function-app**.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="2ddc2-140">试用</span><span class="sxs-lookup"><span data-stu-id="2ddc2-140">Try it out</span></span>

<span data-ttu-id="2ddc2-141">如果一切按预期方式工作, 则 MojifyImage 终结点应正常工作。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-141">If everything is working as expected, the MojifyImage endpoint should be working.</span></span> <span data-ttu-id="2ddc2-142">请</span><span class="sxs-lookup"><span data-stu-id="2ddc2-142">Visit:</span></span>

```bash
https:<deployed-app-name>.azurewebsites.net/api/MojifyImage?imageUrl=<image-url>
```

<span data-ttu-id="2ddc2-143">您应该会在窗口中看到 mojified 图像。</span><span class="sxs-lookup"><span data-stu-id="2ddc2-143">and you should see the mojified image in the window.</span></span>
