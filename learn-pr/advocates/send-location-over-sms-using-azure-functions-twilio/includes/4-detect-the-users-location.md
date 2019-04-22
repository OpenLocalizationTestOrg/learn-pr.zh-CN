<span data-ttu-id="1ee60-101">应用程序具有 UI 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="1ee60-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="1ee60-102">在此单元中, 使用 Xamarin 将位置查找添加到 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="1ee60-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="1ee60-103">启用位置权限</span><span class="sxs-lookup"><span data-stu-id="1ee60-103">Enable location permissions</span></span>

<span data-ttu-id="1ee60-104">所有移动平台都具有有关用户信息和某些硬件 (如照相机、照片库和用户位置) 的安全性。</span><span class="sxs-lookup"><span data-stu-id="1ee60-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="1ee60-105">在应用程序可以访问用户的位置之前, 用户必须授予权限, 方法是在安装时隐式授予这些权限, 或者在运行时选择授予权限。</span><span class="sxs-lookup"><span data-stu-id="1ee60-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="1ee60-106">当您在 store 上查看 UWP 应用程序时, 该列表将显示该应用程序所需的权限。</span><span class="sxs-lookup"><span data-stu-id="1ee60-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="1ee60-107">通过安装应用程序, 可以隐式授予权限。</span><span class="sxs-lookup"><span data-stu-id="1ee60-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="1ee60-108">这些权限是在应用程序清单文件中配置的。</span><span class="sxs-lookup"><span data-stu-id="1ee60-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="1ee60-109">在`ImHere.UWP`应用程序项目中, 打开`Package.appxmanifest`文件。</span><span class="sxs-lookup"><span data-stu-id="1ee60-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

1. <span data-ttu-id="1ee60-110">头转到 "**功能**" 选项卡, 然后检查*位置*功能。</span><span class="sxs-lookup"><span data-stu-id="1ee60-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    !["UWP 功能" 选项卡](../media/4-uwp-location-capability.png)

## <a name="query-for-the-users-location"></a><span data-ttu-id="1ee60-112">查询用户位置</span><span class="sxs-lookup"><span data-stu-id="1ee60-112">Query for the user's location</span></span>

<span data-ttu-id="1ee60-113">有两种方法可以获取用户的位置-最后一个已知或最新的。</span><span class="sxs-lookup"><span data-stu-id="1ee60-113">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="1ee60-114">由于设备可能需要建立 GPS 链接并等待检索准确位置, 因此可能需要一些时间才能获取当前位置。</span><span class="sxs-lookup"><span data-stu-id="1ee60-114">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="1ee60-115">最快的方法是获取设备检测到的最后一个已知位置。</span><span class="sxs-lookup"><span data-stu-id="1ee60-115">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="1ee60-116">最近已知的位置可能更不准确, 但调用速度更快。</span><span class="sxs-lookup"><span data-stu-id="1ee60-116">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="1ee60-117">位置以小数和经度为单位, 以米以上的[度数](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true)表示设备的海拔高度。</span><span class="sxs-lookup"><span data-stu-id="1ee60-117">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="1ee60-118">在`ImHere` .net `MainViewModel`标准项目中打开该类。</span><span class="sxs-lookup"><span data-stu-id="1ee60-118">Open the `MainViewModel` class in the `ImHere` .NET Standard project.</span></span>

1. <span data-ttu-id="1ee60-119">在`SendLocation`方法中, 对`GetLastKnownLocationAsync` `Geolocation` `Xamarin.Essentials`命名空间中的类调用静态方法。</span><span class="sxs-lookup"><span data-stu-id="1ee60-119">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span> <span data-ttu-id="1ee60-120">您将需要为`Xamarin.Essentials`命名空间添加 using 指令。</span><span class="sxs-lookup"><span data-stu-id="1ee60-120">You will need to add a using directive for the `Xamarin.Essentials` namespace.</span></span>

    ```csharp
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

1. <span data-ttu-id="1ee60-121">如果找到`Message` , 则使用用户的位置更新该属性。</span><span class="sxs-lookup"><span data-stu-id="1ee60-121">Update the `Message` property with the user's location if one is found.</span></span>

    ```csharp
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

    <span data-ttu-id="1ee60-122">此方法的完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="1ee60-122">The full code for this method is below.</span></span>
    
    ```csharp
    async Task SendLocation()
    {
        Location location = await Geolocation.GetLastKnownLocationAsync();
    
        if (location != null)
        {
            Message = $"Location found: {location.Latitude}, {location.Longitude}.";
        }
    }
    ```

1. <span data-ttu-id="1ee60-123">运行应用程序, 然后单击 "**发送位置**" 按钮以查看 UI 上的位置。</span><span class="sxs-lookup"><span data-stu-id="1ee60-123">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

    ![显示用户位置的正在运行的应用程序](../media/4-running-app-showing-location.png)    

> [!NOTE]
> <span data-ttu-id="1ee60-125">此应用使用最近已知的位置。</span><span class="sxs-lookup"><span data-stu-id="1ee60-125">This app uses the last known location.</span></span> <span data-ttu-id="1ee60-126">在生产质量的应用程序中, 您可能希望使用超时获取当前准确的位置, 如果时间没有找到, 则回退到最后一个已知。</span><span class="sxs-lookup"><span data-stu-id="1ee60-126">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="1ee60-127">您可以阅读有关如何在[Xamarin 地理位置文档](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true)中执行此操作的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1ee60-127">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true).</span></span>
> 
> <span data-ttu-id="1ee60-128">此应用不具有错误处理。</span><span class="sxs-lookup"><span data-stu-id="1ee60-128">This app does not have error handling.</span></span> <span data-ttu-id="1ee60-129">在生产质量的应用程序中, 应处理发生的任何异常, 如位置不可用。</span><span class="sxs-lookup"><span data-stu-id="1ee60-129">In a production-quality app, you should handle any exceptions that occur, such as if the location was not available.</span></span>

## <a name="summary"></a><span data-ttu-id="1ee60-130">摘要</span><span class="sxs-lookup"><span data-stu-id="1ee60-130">Summary</span></span>

<span data-ttu-id="1ee60-131">在此单元中, 你学习了如何使用 Xamarin 获取用户的位置。</span><span class="sxs-lookup"><span data-stu-id="1ee60-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="1ee60-132">在下一个单元中, 你将创建一个 Azure 函数作为移动应用程序的后端。</span><span class="sxs-lookup"><span data-stu-id="1ee60-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>