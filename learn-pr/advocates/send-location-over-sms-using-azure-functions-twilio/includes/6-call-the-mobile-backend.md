移动应用程序将运行, 并且已创建 Azure 函数的初始版本。 在此单位中, 从移动应用程序调用 Azure 函数, 传入用户的位置以及用户要向其发送短信的电话号码列表。

## <a name="calling-the-azure-function-from-the-mobile-app"></a>从移动应用程序调用 Azure 函数

1. 打开`MainViewModel`。

1. 在此类中, 添加一个`HttpClient`名`client`为的私有字段。 您需要添加对命名空间的`System.Net.Http`引用。

    ```cs
    HttpClient client = new HttpClient();
    ```

1. 为函数的基 URL 添加常量字段。 将此设置为本地 Azure 函数运行时所侦听的地址。 在将该函数部署到 azure 后, 可以将此常量更改为 azure URL。

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. 在`SendLocation`方法中, 找到位置之后, `PostData`使用用户输入的位置和电话号码列表创建一个新实例。 您需要为`ImHere.Data`命名空间添加 using 指令。

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > [!NOTE]
    > 这假定电话号码是以正确的格式 (每个行在`Editor`控件中一个) 输入的。 在生产质量的应用程序中, 将针对此进行验证, 以确保输入一个或多个电话号码并采用正确的格式。    
 

1. 若要将`PostData`作为 json 序列化, 最简单的方法是使用 newtonsoft.json NuGet 包。 将此 NuGet 包添加到`ImHere`项目中, 就像在前面的单元中添加 Xamarin 一样。

1. `string`使用`JsonConvert`静态类`PostData`将对进行序列化。 您需要为`Newtonsoft.Json`命名空间添加 using 指令。 将此字符串编码为`StringContent`类, 以便可以将其作为 JSON 传递给 Azure 函数。

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. 将此数据发布到函数, 并获取返回结果。

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   使用`/api/<function name>`来访问 Azure 函数, 因此假设本地函数运行时选择的端口是 7071, 则可以`SendLocation`在`http://localhost:7071/api/SendLocation`中访问该函数。

1. 根据结果, 在 UI 上显示一条消息。

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

新字段和`SendLocation`方法的完整代码如下所示。

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

## <a name="testing-it-out"></a>测试

1. 请确保 Azure 函数仍在本地运行, 并且端口与`SendLocation`方法相匹配。

1. 将 UWP 应用程序设置为启动应用程序并运行它。 单击 "**发送位置**" 按钮。 您将在函数运行时控制台窗口中看到输出, 其中显示了所调用的函数以及显示生成的 URL 的日志记录。

    ![正在调用的函数的输出](../media/6-function-called.png)

1. 若要测试 URL 生成, 请将其从控制台粘贴到浏览器中。 它应显示你的当前位置。

    > [!TIP]
    > 你将看到的位置是应用运行的位置, 因此将接近运行 VM 的数据中心。 如果此应用在本地设备上运行, 则会显示您的位置。

## <a name="summary"></a>摘要

在此单元中, 你学习了如何从移动应用程序调用 Azure 函数。 此呼叫已传递给用户的位置和其输入为 JSON 的电话号码。 在下一个单元中, 您将 Azure 函数绑定到 Twilio 以将此位置作为 SMS 消息发送。