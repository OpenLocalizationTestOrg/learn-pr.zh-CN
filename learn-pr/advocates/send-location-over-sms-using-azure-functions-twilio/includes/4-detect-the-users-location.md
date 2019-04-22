应用程序具有 UI 和 ViewModel。 在此单元中, 你将使用 Xamarin 将位置查找添加到 ViewModel。

## <a name="enable-location-permissions"></a>启用位置权限

所有移动平台都有关于用户信息和某些硬件 (如相机、照片库和用户位置) 的安全性。 在应用程序可以访问用户的位置之前, 用户必须授予权限, 方法是在安装时隐式授予这些权限, 或者在运行时选择授予权限。 当您在应用商店中查看 UWP 应用程序时, 该列表将显示该应用程序所需的权限。 通过安装应用程序, 可以隐式授予权限。 这些权限是在应用程序清单文件中配置的。

1. 在`ImHere.UWP`应用程序项目中, 打开`Package.appxmanifest`文件。

1. 头转到 "**功能**" 选项卡, 然后检查*位置*功能。

    !["UWP 功能" 选项卡](../media/4-uwp-location-capability.png)

## <a name="query-for-the-users-location"></a>查询用户位置

有两种方法可以获取用户的位置-最后一个已知或最新的。 由于设备可能需要建立 GPS 链接并等待检索准确位置, 因此可能需要一些时间才能获取当前位置。 最快的方法是获取设备检测到的最后一个已知位置。 最近已知的位置可能更不准确, 但调用速度更快。 位置以小数和经度为单位, 以米以上的[度数](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true)表示设备的海拔高度。

1. 在`ImHere` .net `MainViewModel`标准项目中打开该类。

1. 为`Xamarin.Essentials`命名空间添加 using 指令。

    ```cs
        using Xamarin.Essentials;
    ```

1. 在`SendLocation`方法中, 对`GetLastKnownLocationAsync` `Geolocation` `Xamarin.Essentials`命名空间中的类调用静态方法。

    ```csharp
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

1. 如果找到`Message` , 则使用用户的位置更新该属性。

    ```csharp
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

    此方法的完整代码如下所示。
    
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

1. 运行应用程序, 然后单击 "**发送位置**" 按钮以查看 UI 上的位置。

    ![显示用户位置的正在运行的应用程序](../media/4-running-app-showing-location.png)

> [!NOTE]
> 此应用使用最近已知的位置。 在生产质量的应用程序中, 您可能希望使用超时获取当前准确的位置, 如果时间没有找到, 则回退到最后一个已知。 您可以阅读有关如何在[Xamarin 地理位置文档](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true)中执行此操作的详细信息。
> 
> 此应用不具有错误处理。 在生产质量的应用程序中, 应处理发生的任何异常, 如位置不可用。

## <a name="summary"></a>摘要

在此单元中, 你学习了如何使用 Xamarin 获取用户的位置。 在下一个单元中, 你将创建 Azure 函数以充当移动应用的后端。