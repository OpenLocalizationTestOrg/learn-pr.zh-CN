<span data-ttu-id="b86ef-101">移动应用程序将运行, 并且已创建 Azure 函数的初始版本。</span><span class="sxs-lookup"><span data-stu-id="b86ef-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="b86ef-102">在此单位中, 从移动应用程序调用 Azure 函数, 传入用户的位置以及用户要向其发送短信的电话号码列表。</span><span class="sxs-lookup"><span data-stu-id="b86ef-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="b86ef-103">从移动应用程序调用 Azure 函数</span><span class="sxs-lookup"><span data-stu-id="b86ef-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="b86ef-104">打开`MainViewModel`。</span><span class="sxs-lookup"><span data-stu-id="b86ef-104">Open the `MainViewModel`.</span></span>

1. <span data-ttu-id="b86ef-105">在此类中, 添加一个`HttpClient`名`client`为的私有字段。</span><span class="sxs-lookup"><span data-stu-id="b86ef-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="b86ef-106">您需要添加对命名空间的`System.Net.Http`引用。</span><span class="sxs-lookup"><span data-stu-id="b86ef-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

1. <span data-ttu-id="b86ef-107">为函数的基 URL 添加常量字段。</span><span class="sxs-lookup"><span data-stu-id="b86ef-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="b86ef-108">将此设置为本地 Azure 函数运行时所侦听的地址。</span><span class="sxs-lookup"><span data-stu-id="b86ef-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="b86ef-109">在将该函数部署到 azure 后, 可以将此常量更改为 azure URL。</span><span class="sxs-lookup"><span data-stu-id="b86ef-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. <span data-ttu-id="b86ef-110">在`SendLocation`方法中, 找到位置之后, `PostData`使用用户输入的位置和电话号码列表创建一个新实例。</span><span class="sxs-lookup"><span data-stu-id="b86ef-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="b86ef-111">您需要为`ImHere.Data`命名空间添加 using 指令。</span><span class="sxs-lookup"><span data-stu-id="b86ef-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > [!NOTE]
    > <span data-ttu-id="b86ef-112">这假定电话号码是以正确的格式 (每个行在`Editor`控件中一个) 输入的。</span><span class="sxs-lookup"><span data-stu-id="b86ef-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="b86ef-113">在生产质量的应用程序中, 将针对此进行验证, 以确保输入一个或多个电话号码并采用正确的格式。</span><span class="sxs-lookup"><span data-stu-id="b86ef-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>    
 

1. <span data-ttu-id="b86ef-114">若要将`PostData`作为 json 序列化, 最简单的方法是使用 newtonsoft.json NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="b86ef-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.Json NuGet package.</span></span> <span data-ttu-id="b86ef-115">将此 NuGet 包添加到`ImHere`项目中, 就像在前面的单元中添加 Xamarin 一样。</span><span class="sxs-lookup"><span data-stu-id="b86ef-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

1. <span data-ttu-id="b86ef-116">`string`使用`JsonConvert`静态类`PostData`将对进行序列化。</span><span class="sxs-lookup"><span data-stu-id="b86ef-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="b86ef-117">您需要为`Newtonsoft.Json`命名空间添加 using 指令。</span><span class="sxs-lookup"><span data-stu-id="b86ef-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="b86ef-118">将此字符串编码为`StringContent`类, 以便可以将其作为 JSON 传递给 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="b86ef-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. <span data-ttu-id="b86ef-119">将此数据发布到函数, 并获取返回结果。</span><span class="sxs-lookup"><span data-stu-id="b86ef-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="b86ef-120">使用`/api/<function name>`来访问 Azure 函数, 因此假设本地函数运行时选择的端口是 7071, 则可以`SendLocation`在`http://localhost:7071/api/SendLocation`中访问该函数。</span><span class="sxs-lookup"><span data-stu-id="b86ef-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

1. <span data-ttu-id="b86ef-121">根据结果, 在 UI 上显示一条消息。</span><span class="sxs-lookup"><span data-stu-id="b86ef-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="b86ef-122">新字段和`SendLocation`方法的完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="b86ef-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a><span data-ttu-id="b86ef-123">测试</span><span class="sxs-lookup"><span data-stu-id="b86ef-123">Testing it out</span></span>

1. <span data-ttu-id="b86ef-124">请确保 Azure 函数仍在本地运行, 并且端口与`SendLocation`方法相匹配。</span><span class="sxs-lookup"><span data-stu-id="b86ef-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

1. <span data-ttu-id="b86ef-125">将 UWP 应用程序设置为启动应用程序并运行它。</span><span class="sxs-lookup"><span data-stu-id="b86ef-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="b86ef-126">单击 "**发送位置**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="b86ef-126">Click the **Send Location** button.</span></span> <span data-ttu-id="b86ef-127">您将在函数运行时控制台窗口中看到输出, 其中显示了所调用的函数以及显示生成的 URL 的日志记录。</span><span class="sxs-lookup"><span data-stu-id="b86ef-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![正在调用的函数的输出](../media/6-function-called.png)

1. <span data-ttu-id="b86ef-129">若要测试 URL 生成, 请将其从控制台粘贴到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="b86ef-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="b86ef-130">它应显示你的当前位置。</span><span class="sxs-lookup"><span data-stu-id="b86ef-130">It should show your current location.</span></span>

    > [!TIP]
    > <span data-ttu-id="b86ef-131">你将看到的位置是应用运行的位置, 因此将接近运行 VM 的数据中心。</span><span class="sxs-lookup"><span data-stu-id="b86ef-131">The location you'll see is the location where the app is running, so will be near to the data center that the VM is running from.</span></span> <span data-ttu-id="b86ef-132">如果此应用在本地设备上运行, 则会显示您的位置。</span><span class="sxs-lookup"><span data-stu-id="b86ef-132">If this app was running on your local device then it would show your location.</span></span>

## <a name="summary"></a><span data-ttu-id="b86ef-133">摘要</span><span class="sxs-lookup"><span data-stu-id="b86ef-133">Summary</span></span>

<span data-ttu-id="b86ef-134">在此单元中, 你学习了如何从移动应用程序调用 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="b86ef-134">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="b86ef-135">此呼叫已传递给用户的位置和其输入为 JSON 的电话号码。</span><span class="sxs-lookup"><span data-stu-id="b86ef-135">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="b86ef-136">在下一个单元中, 您将 Azure 函数绑定到 Twilio 以将此位置作为 SMS 消息发送。</span><span class="sxs-lookup"><span data-stu-id="b86ef-136">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>