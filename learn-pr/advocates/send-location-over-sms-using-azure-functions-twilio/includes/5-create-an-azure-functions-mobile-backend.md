<span data-ttu-id="a06bf-101">此时, 应用正在努力获取用户的位置, 并准备将其发送到 Azure 功能。</span><span class="sxs-lookup"><span data-stu-id="a06bf-101">At this point, the app is working to get the user's location and is ready to be sent to an Azure function.</span></span> <span data-ttu-id="a06bf-102">在此单位中, 将生成 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-102">In this unit, you build the Azure function.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="a06bf-103">创建 Azure 函数项目</span><span class="sxs-lookup"><span data-stu-id="a06bf-103">Create an Azure Functions project</span></span>

1. <span data-ttu-id="a06bf-104">通过右键单击解决方案并选择`ImHere` " *>New 项目 ...*", 将新项目添加到解决方案中。</span><span class="sxs-lookup"><span data-stu-id="a06bf-104">Add a new project to the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

1. <span data-ttu-id="a06bf-105">从左侧的树中, 选择 " *Visual c #->Cloud*", 然后从中心的面板中选择 " *Azure 函数*"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-105">From the tree on the left-hand side, select *Visual C#->Cloud*, and then select *Azure Functions* from the panel in the center.</span></span>

1. <span data-ttu-id="a06bf-106">将项目命名为 "ImHere", 然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-106">Name the project "ImHere.Functions", and then click **OK**.</span></span>

    !["添加新项目" 对话框](../media/5-add-new-functions-project.png)

1. <span data-ttu-id="a06bf-108">将显示 "**新建项目**配置" 对话框, 它可能会在左下角显示一个微调框, 同时加载更新的模板。</span><span class="sxs-lookup"><span data-stu-id="a06bf-108">The **New Project** configuration dialog will appear, and it may show a spinner in the bottom-left whilst loading updated templates.</span></span> <span data-ttu-id="a06bf-109">如果你看到此项, 请等待此操作完成加载, 然后, 如果更新的模板可用, 请单击将显示的 "**刷新**" 选项以确保你获取的是最新的函数模板。</span><span class="sxs-lookup"><span data-stu-id="a06bf-109">If you see this, wait until this has finished loading, then if updated templates are available, click the **Refresh** option that will appear to ensure you get the latest Function templates.</span></span>

    !["新建项目" 对话框, 用于加载最新模板](../media/5-loading-templates.png)

1. <span data-ttu-id="a06bf-111">在 "**新建项目**配置" 对话框中, 确保 "函数版本" 设置为 " *Azure 函数 v2 (.net Standard)* (**不**是_v1 (.net Framework)_")。</span><span class="sxs-lookup"><span data-stu-id="a06bf-111">In the **New Project** configuration dialog, ensure the Functions version is set to *Azure Functions v2 (.NET Standard)* (**NOT** _v1 (.NET Framework)_).</span></span> <span data-ttu-id="a06bf-112">选择 " *Http 触发器*", 将存储帐户设置为 "*存储仿真程序*", 并将访问权限设置为 "*匿名*"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-112">Select *Http Trigger*, leave the storage account set to *Storage Emulator*, and set the access rights to *Anonymous*.</span></span> <span data-ttu-id="a06bf-113">然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="a06bf-113">Then click **OK**.</span></span>

    ![Azure 函数项目配置对话框](../media/5-configure-trigger.png)

    <span data-ttu-id="a06bf-115">将创建新项目, 并调用`Function1`一个默认函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-115">The new project will be created and have a default function called `Function1`.</span></span>

> [!NOTE]
> <span data-ttu-id="a06bf-116">此函数是使用匿名访问创建的。</span><span class="sxs-lookup"><span data-stu-id="a06bf-116">This function was created with anonymous access.</span></span> <span data-ttu-id="a06bf-117">一旦发布到 Azure, 知道该 URL 的任何人都将能够调用此函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-117">Once published to Azure, anybody who knows the URL will be able to call this function.</span></span> <span data-ttu-id="a06bf-118">在实际方案中, 您可以使用某种形式的身份验证 (如[azure 应用服务身份验证](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview?azure-portal=true)或[azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c?azure-portal=true)) 保护这种情况。</span><span class="sxs-lookup"><span data-stu-id="a06bf-118">In a real-world scenario, you would protect this with some form of authentication, such as [Azure App Service authentication](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview?azure-portal=true) or [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c?azure-portal=true).</span></span>

## <a name="create-the-function"></a><span data-ttu-id="a06bf-119">创建函数</span><span class="sxs-lookup"><span data-stu-id="a06bf-119">Create the function</span></span>

<span data-ttu-id="a06bf-120">Azure 函数项目是通过调用`Function1`的单个 HTTP 触发器函数创建的。</span><span class="sxs-lookup"><span data-stu-id="a06bf-120">The Azure Functions project is created with a single HTTP trigger function called `Function1`.</span></span> <span data-ttu-id="a06bf-121">http 触发器允许您使用 http 请求调用函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-121">HTTP triggers allow you to invoke your functions using HTTP requests.</span></span> <span data-ttu-id="a06bf-122">函数本身作为`Run` `Function1`类中的静态方法实现。</span><span class="sxs-lookup"><span data-stu-id="a06bf-122">The function itself is implemented as a static `Run` method in the `Function1` class.</span></span>

1. <span data-ttu-id="a06bf-123">将 "解决方案资源管理器" 中的文件从 "Function1.cs" 重命名为 "SendLocation.cs"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-123">Rename the file in Solution Explorer from "Function1.cs" to "SendLocation.cs".</span></span> <span data-ttu-id="a06bf-124">当系统提示您重命名对 code 元素`Function1`的所有引用时, 请单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="a06bf-124">When prompted to rename all references to the code element `Function1`, click **Yes**.</span></span>

1. <span data-ttu-id="a06bf-125">将属性中的函数名称重命名为 "SendLocation"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-125">Rename the function name in the attribute to "SendLocation".</span></span>

    ```cs
    [FunctionName("SendLocation")]
    ```

1. <span data-ttu-id="a06bf-126">删除函数的内容, 但将信息消息写入记录器的第一行除外。</span><span class="sxs-lookup"><span data-stu-id="a06bf-126">Delete the contents of the function, except the first line that writes an information message to the logger.</span></span>

    ```cs
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                             "get", "post",
                                                             Route = null)]HttpRequestMessage req,
                                                ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a><span data-ttu-id="a06bf-127">创建类以在移动应用程序和功能之间共享数据</span><span class="sxs-lookup"><span data-stu-id="a06bf-127">Create a class to share data between the mobile app and function</span></span>

<span data-ttu-id="a06bf-128">将数据发送到 Azure 函数时, 它将以 JSON 的形式发送。</span><span class="sxs-lookup"><span data-stu-id="a06bf-128">When data is sent to the Azure function, it will be sent as JSON.</span></span> <span data-ttu-id="a06bf-129">移动应用程序会将数据序列化为 json, 并且函数将从 JSON 反序列化。</span><span class="sxs-lookup"><span data-stu-id="a06bf-129">The mobile app will serialize data into JSON and the function will deserialize from JSON.</span></span> <span data-ttu-id="a06bf-130">若要使该数据在移动应用程序和功能之间保持一致, 请创建一个新项目, 其中包含一个用于保存位置和电话号码数据的类。</span><span class="sxs-lookup"><span data-stu-id="a06bf-130">To keep this data consistent between the mobile app and the function, create a new project that contains a class to hold the location and phone number data.</span></span> <span data-ttu-id="a06bf-131">然后, 应用程序和功能将引用此项目。</span><span class="sxs-lookup"><span data-stu-id="a06bf-131">This project will then be referenced by the app and function.</span></span>

1. <span data-ttu-id="a06bf-132">右键单击解决方案并选择 " `ImHere` *>New 项目 ...*", 在解决方案下创建一个新项目。</span><span class="sxs-lookup"><span data-stu-id="a06bf-132">Create a new project under the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

1. <span data-ttu-id="a06bf-133">从左侧的树中, 选择 " *Visual c #-> Standard*", 然后从中央面板中选择 "类库 *(.net Standard)* "。</span><span class="sxs-lookup"><span data-stu-id="a06bf-133">From the tree on the left-hand side, select *Visual C#->.NET Standard*, and then select *Class Library (.NET Standard)* from the panel in the center.</span></span>

1. <span data-ttu-id="a06bf-134">将项目命名为 "ImHere", 然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-134">Name the project "ImHere.Data", and then click **OK**.</span></span>

    !["添加新项目" 对话框](../media/5-add-new-net-standard-project.png)

1. <span data-ttu-id="a06bf-136">删除自动生成的 "Class1.cs" 文件。</span><span class="sxs-lookup"><span data-stu-id="a06bf-136">Delete the auto-generated "Class1.cs" file.</span></span>

1. <span data-ttu-id="a06bf-137">在`ImHere.Data`项目中创建一个新类, `PostData`方法是右键单击该项目, 然后选择 "*添加->Class ...*"。将新类命名为 "PostData", 然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-137">Create a new class in the `ImHere.Data` project called `PostData` by right-clicking on the project and then selecting *Add->Class...*. Name the new class "PostData" and click **OK**.</span></span> <span data-ttu-id="a06bf-138">将此新类标记`public`为。</span><span class="sxs-lookup"><span data-stu-id="a06bf-138">Mark this new class as `public`.</span></span>

1. <span data-ttu-id="a06bf-139">添加`double`纬度和经度的属性, 以及要发送到的`string[]`电话号码的属性。</span><span class="sxs-lookup"><span data-stu-id="a06bf-139">Add `double` properties for the latitude and longitude, as well as a `string[]` property for the phone numbers to send to.</span></span>

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

1. <span data-ttu-id="a06bf-140">通过右键单击项目, 然后选择 " `ImHere.Functions` *添加->Reference ...*", 将对此项目的引用添加到项目和`ImHere`项目中。从左侧的树中选择 "*项目*", 然后选中 " *ImHere*" 旁边的框。</span><span class="sxs-lookup"><span data-stu-id="a06bf-140">Add a reference to this project to both the `ImHere.Functions` and `ImHere` projects by right-clicking on the project and then selecting *Add->Reference...*. Select *Projects* from the tree on the left-hand side, and then check the box next to *ImHere.Data*.</span></span>

    ![配置项目引用](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a><span data-ttu-id="a06bf-142">读取发送给函数的数据</span><span class="sxs-lookup"><span data-stu-id="a06bf-142">Read the data sent to the function</span></span>

<span data-ttu-id="a06bf-143">在 Azure 函数中, `req`参数包含所进行的 HTTP 请求, 此请求中的数据将是 JSON 序列化`PostData`对象。</span><span class="sxs-lookup"><span data-stu-id="a06bf-143">In the Azure function, the `req` parameter contains the HTTP request that was made and the data inside this request will be a JSON serialized `PostData` object.</span></span>

1. <span data-ttu-id="a06bf-144">在`ImHere.Functions`项目`SendLocation`中打开该类。</span><span class="sxs-lookup"><span data-stu-id="a06bf-144">Open the `SendLocation` class in the `ImHere.Functions` project.</span></span>

1. <span data-ttu-id="a06bf-145">将 HTTP 请求的内容读入一个字符串, 然后将其反序列化为一个`PostData`对象, 并为该`ImHere.Data`命名空间添加 using 指令。</span><span class="sxs-lookup"><span data-stu-id="a06bf-145">Read the contents of the HTTP request into a string, then deserialize it into a `PostData` object, adding a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    ```

1. <span data-ttu-id="a06bf-146">使用中的纬度和经度构造 Google Maps URL `PostData`。</span><span class="sxs-lookup"><span data-stu-id="a06bf-146">Construct a Google Maps URL using the latitude and longitude from the `PostData`.</span></span>

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

1. <span data-ttu-id="a06bf-147">记录 URL。</span><span class="sxs-lookup"><span data-stu-id="a06bf-147">Log the URL.</span></span>

    ```cs
    log.LogInformation($"URL created - {url}");
    ```

1. <span data-ttu-id="a06bf-148">返回200状态代码以显示函数已完成, 且未出错。</span><span class="sxs-lookup"><span data-stu-id="a06bf-148">Return a 200 status code to show the function completed without error.</span></span>

    ```cs
    return new OkResult();
    ```

<span data-ttu-id="a06bf-149">完整的函数如下所示。</span><span class="sxs-lookup"><span data-stu-id="a06bf-149">The complete function is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                         Route = null)]HttpRequest req,
                                                    ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.LogInformation($"URL created - {url}");
    return new OkResult();
}
```

## <a name="run-the-azure-function-locally"></a><span data-ttu-id="a06bf-150">在本地运行 Azure 函数</span><span class="sxs-lookup"><span data-stu-id="a06bf-150">Run the Azure function locally</span></span>

<span data-ttu-id="a06bf-151">可以使用本地存储帐户和本地 Azure 函数运行时在本地运行函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-151">Functions can be run locally using a local storage account and local Azure Functions runtime.</span></span> <span data-ttu-id="a06bf-152">此本地运行时允许你先测试函数, 然后再将其部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="a06bf-152">This local runtime allows you to test out your function before deploying it to Azure.</span></span>

1. <span data-ttu-id="a06bf-153">在 "解决方案资源管理`ImHere.Functions`器" 中右键单击该项目, 然后选择 "*设为启动项目*"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-153">Right-click on the `ImHere.Functions` project in the solution explorer, and then select *Set as StartUp project*.</span></span>

1. <span data-ttu-id="a06bf-154">从 "*调试*" 菜单中, 选择 "*启动 (不调试*)"。</span><span class="sxs-lookup"><span data-stu-id="a06bf-154">From the *Debug* menu, select *Start Without Debugging*.</span></span> <span data-ttu-id="a06bf-155">本地 Azure 函数运行时将在控制台窗口中启动, 并启动您的功能, 并在上`localhost`的可用端口上进行侦听。</span><span class="sxs-lookup"><span data-stu-id="a06bf-155">The local Azure Functions runtime will launch inside a console window and start your function, listening on an available port on `localhost`.</span></span> <span data-ttu-id="a06bf-156">如果你看到请求防火墙访问的对话框, 则允许访问专用网络 (默认选项)。</span><span class="sxs-lookup"><span data-stu-id="a06bf-156">If you see a dialog asking for firewall access, allow access to private networks (the default option).</span></span>

    ![本地运行的 Azure 函数](../media/5-function-running-locally.png)

1. <span data-ttu-id="a06bf-158">记下函数所侦听的端口。</span><span class="sxs-lookup"><span data-stu-id="a06bf-158">Take a note of the port that the function is listening on.</span></span> <span data-ttu-id="a06bf-159">你将在下一个单元中需要此项来测试移动应用。</span><span class="sxs-lookup"><span data-stu-id="a06bf-159">You'll need this in the next unit to test out the mobile app.</span></span> <span data-ttu-id="a06bf-160">在上面的图像中, 函数在端口**7071**上进行侦听。</span><span class="sxs-lookup"><span data-stu-id="a06bf-160">In the image above, the function is listening on port **7071**.</span></span>

    ```sh
    Listening on http://localhost:7071/
    ```

1. <span data-ttu-id="a06bf-161">使函数保持运行状态, 以便您可以在下一个设备中测试移动应用。</span><span class="sxs-lookup"><span data-stu-id="a06bf-161">Leave the function running so that you can test the mobile app in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="a06bf-162">摘要</span><span class="sxs-lookup"><span data-stu-id="a06bf-162">Summary</span></span>

<span data-ttu-id="a06bf-163">在此单元中, 您学习了如何在 Visual Studio 中创建 Azure function 项目, 添加了一个共享项目, 其中包含要在移动应用程序和函数之间共享的数据对象, 并了解如何创建函数的基本实现以反序列化数据传入。</span><span class="sxs-lookup"><span data-stu-id="a06bf-163">In this unit, you learned how to create an Azure Functions project in Visual Studio, added a shared project with a data object to be shared between the mobile app and the function, and learned how to create a basic implementation of the function to deserialize the data passed in.</span></span> <span data-ttu-id="a06bf-164">此外, 还学习了如何在本地运行 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-164">You also learned how to run an Azure function locally.</span></span> <span data-ttu-id="a06bf-165">在下一个设备中, 你将从移动应用程序调用 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="a06bf-165">In the next unit, you'll call the Azure function from the mobile app.</span></span>