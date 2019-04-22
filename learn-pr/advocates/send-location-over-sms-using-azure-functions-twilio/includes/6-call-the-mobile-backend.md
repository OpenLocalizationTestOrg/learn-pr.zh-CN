<span data-ttu-id="cd5b5-101">你的移动应用现已启动并且正在运行, 并且你已创建的初始版本。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-101">Your mobile app is now up and running and you've created the initial version of the .</span></span> <span data-ttu-id="cd5b5-102">在此单位中, 您将从移动应用程序调用 Azure 功能, 传入用户的位置和用户要发送短信的电话号码列表。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-102">In this unit, you'll call the Azure Functions from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS to.</span></span>

## <a name="call-the-azure-functions-from-the-mobile-app"></a><span data-ttu-id="cd5b5-103">从移动应用程序调用 Azure 函数</span><span class="sxs-lookup"><span data-stu-id="cd5b5-103">Call the Azure Functions from the mobile app</span></span>

1. <span data-ttu-id="cd5b5-104">`MainViewModel`在 "ImHere" 项目中打开。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-104">Open the `MainViewModel` in the ImHere project.</span></span>

1. <span data-ttu-id="cd5b5-105">为`System.Net.Http`、 `Newtonsoft.Json`和`ImHere.Data`添加 using 指令。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-105">Add a using directive for `System.Net.Http`, `Newtonsoft.Json`, and `ImHere.Data`.</span></span>

    ```cs
    using System.Net.Http;
    using ImHere.Data;
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="cd5b5-106">在此类中, 添加一个`HttpClient`名`client`为的私有字段。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-106">In this class, add a private `HttpClient` field called `client`.</span></span> 

    ```cs
    HttpClient client = new HttpClient();
    ```

1. <span data-ttu-id="cd5b5-107">为函数的基 URL 添加常量字段。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="cd5b5-108">将此设置为本地 Azure 函数运行时所侦听的地址。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="cd5b5-109">在将该函数部署到 azure 后, 可以将此常量更改为 azure URL。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. <span data-ttu-id="cd5b5-110">在`SendLocation`方法中, 创建一个`PostData`使用位置和用户输入的电话号码列表的新实例。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-110">In the `SendLocation` method create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > [!NOTE]
    > <span data-ttu-id="cd5b5-111">这假定电话号码是以正确的格式 (每个行在`Editor`控件中一个) 输入的。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-111">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="cd5b5-112">在生产质量的应用程序中, 将针对此进行验证, 以确保输入一个或多个电话号码并采用正确的格式。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-112">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>    
 
1. <span data-ttu-id="cd5b5-113">若要将`PostData`作为 json 序列化, 最简单的方法是使用 newtonsoft.json NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-113">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.Json NuGet package.</span></span> <span data-ttu-id="cd5b5-114">将此 NuGet 包添加到`ImHere`。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-114">Add this NuGet package to the `ImHere`.</span></span>

     - <span data-ttu-id="cd5b5-115">右键单击 "ImHere" 项目下的 "**依赖项**", 然后选择 "_管理 NuGet 程序包 ..._"。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-115">Right-click **Dependencies** under the ImHere project and select _Manage NuGet Packages..._.</span></span>
     - <span data-ttu-id="cd5b5-116">在 "**浏览**" 选项卡中, 搜索 "newtonsoft.json" 包并单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-116">In the **Browse** tab, search for Newtonsoft.Json package and click **Install**.</span></span> <span data-ttu-id="cd5b5-117">NuGet 包将添加到您的项目中。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-117">The NuGet package will be added to your project.</span></span>

1. <span data-ttu-id="cd5b5-118">`string`使用`JsonConvert`静态类`PostData`将对进行序列化。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-118">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="cd5b5-119">将此字符串编码为`StringContent`类, 以便可以将其作为 JSON 传递给 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-119">Encode this string into a `StringContent` class so that it can be passed to the Azure Functions as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. <span data-ttu-id="cd5b5-120">将此数据发布到函数, 并获取返回结果。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-120">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="cd5b5-121">使用`/api/<function name>`来访问 Azure 函数, 因此假设本地函数运行时选择的端口是 7071, 则可以`SendLocation`在`http://localhost:7071/api/SendLocation`中访问该函数。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-121">Azure Functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

1. <span data-ttu-id="cd5b5-122">根据结果, 在 UI 上显示一条消息。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-122">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="cd5b5-123">以下是 MainViewModel 的完整代码, 包括`SendLocation`方法的新字段。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-123">The following is the full code for the MainViewModel, including the new fields for the `SendLocation` method.</span></span>

```cs
using System.Threading.Tasks;
using System.Windows.Input;
using System.Text;
using Xamarin.Essentials;
using ImHere.Data;
using Newtonsoft.Json;
using System.Net.Http;
using Xamarin.Forms;


namespace ImHere
{
    public class MainViewModel : BaseViewModel
    {
        string message = "";
        public string Message
        {
            get => message;
            set => Set(ref message, value);
        }

        string phoneNumbers = "";
        public string PhoneNumbers
        {
            get => phoneNumbers;
            set => Set(ref phoneNumbers, value);
        }

        public MainViewModel()
        {
            SendLocationCommand = new Command(async () => await SendLocation());
        }

        public ICommand SendLocationCommand { get; }

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
    }
}
```

## <a name="testing-it-out"></a><span data-ttu-id="cd5b5-124">测试</span><span class="sxs-lookup"><span data-stu-id="cd5b5-124">Testing it out</span></span>

1. <span data-ttu-id="cd5b5-125">请确保您的函数仍在本地运行, 并且端口与`SendLocation`方法相匹配。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-125">Make sure that you function is still running locally and the port matches the `SendLocation` method.</span></span>

1. <span data-ttu-id="cd5b5-126">将 UWP 应用程序设置为启动应用程序并运行它。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-126">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="cd5b5-127">单击 "**发送位置**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-127">Click the **Send Location** button.</span></span> <span data-ttu-id="cd5b5-128">您将在函数运行时控制台窗口中看到输出, 其中显示了所调用的函数以及显示生成的 URL 的日志记录。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-128">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![正在调用的函数的输出](../media/6-function-called.png)

1. <span data-ttu-id="cd5b5-130">若要测试 URL 生成, 请将其从控制台粘贴到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-130">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="cd5b5-131">它应显示你的当前位置。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-131">It should show your current location.</span></span>

    > [!TIP]
    > <span data-ttu-id="cd5b5-132">你将看到的位置是应用运行的位置, 因此将接近运行 VM 的数据中心。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-132">The location you'll see is the location where the app is running, so will be near to the data center that the VM is running from.</span></span> <span data-ttu-id="cd5b5-133">如果此应用在本地设备上运行, 则会显示您的位置。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-133">If this app was running on your local device then it would show your location.</span></span>

## <a name="summary"></a><span data-ttu-id="cd5b5-134">摘要</span><span class="sxs-lookup"><span data-stu-id="cd5b5-134">Summary</span></span>

<span data-ttu-id="cd5b5-135">在此单元中, 你学习了如何从移动应用程序调用 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-135">In this unit, you learned how to call the Azure Functions from the mobile app.</span></span> <span data-ttu-id="cd5b5-136">此呼叫已传递给用户的位置和其输入为 JSON 的电话号码。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-136">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="cd5b5-137">在下一个单元中, 将您的函数绑定到 Twilio 以将此位置作为 SMS 消息发送。</span><span class="sxs-lookup"><span data-stu-id="cd5b5-137">In the next unit, you'll bind your function to Twilio to send this location as an SMS message.</span></span>