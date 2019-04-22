在这种情况下, 移动应用是一个简单的 "Hello World" 应用。 在此单元中, 你将添加 UI 和一些基本的应用程序逻辑。

应用程序的 UI 将包含以下内容:

- 一个用于输入一些电话号码的文本输入控件。
- 使用 Azure 功能将你的位置发送给这些号码的按钮。
- 将向当前状态的用户显示邮件的标签, 如发送的位置和成功发送的位置。

Xamarin 支持称为 "模型-视图-ViewModel (MVVM)" 的设计模式。 您可以在[Xamarin MVVM 文档](https://docs.microsoft.com/xamarin/xamarin-forms/enterprise-application-patterns/mvvm?azure-portal=true)中了解有关 MVVM 的更多信息, 但它的本质是, 每个页面 (视图) 都有一个公开属性和行为的 ViewModel。

ViewModel 属性是按名称 "绑定" 到 UI 上的组件, 此绑定可同步视图和 ViewModel 之间的数据。 例如, 名`string` `Name`为的 ViewModel 上的属性可以绑定到 UI 上`Text`的文本输入控件的属性。 文本输入控件显示`Name`属性中的值, 当用户更改 UI 中的文本时, 将`Name`更新属性。 如果在 ViewModel 中更改`Name`了属性的值, 则会引发一个事件来通知 UI 进行更新。

ViewModel 行为公开为命令属性, 该命令是一个包装在调用命令时执行的操作的对象。 这些命令按名称绑定到类似按钮的控件, 点击按钮将调用命令。

## <a name="create-a-base-viewmodel"></a>创建基本 ViewModel

ViewModels 实现`INotifyPropertyChanged`接口。 此接口具有单个事件`PropertyChanged`, 用于通知 UI 的任何更新。 此事件具有事件参数, 其中包含已更改的属性的名称。 常见的做法是创建基 ViewModel 类来实现此接口并提供一些帮助程序方法。

1. 右键单击 "ImHere 项目", 然后选择 "_添加_ > _类_"。

1. 将新类命名为 "BaseViewModel", 然后单击 "**添加**"。

1. 为`System.ComponentModel`和`System.Runtime.CompilerServices`添加 using 指令。

   ```cs
    using System.ComponentModel;
    using System.Runtime.CompilerServices;
    ```

1. 生成类`public`并从中派生`INotifyPropertyChanged`。

   ```cs
     public class BaseViewModel : INotifyPropertyChanged
   ```

1. 通过添加`INotifyPropertyChanged` `PropertyChanged`事件来实现接口:

    ```cs
    public event PropertyChangedEventHandler PropertyChanged;
    ```

1. 添加`Set`触发事件的`PropertyChanged`方法。

    ```cs
    protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
    {
        if (Equals(field, value)) return;
        field = value;
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
    ```

    此方法引用了支持字段、新值和属性名称。 如果该字段尚未更改, 则此方法返回, 否则, 将更新该字段并`PropertyChanged`引发事件。 方法上的`propertyName`参数是默认参数, 并使用`CallerMemberName`属性进行标记。 `Set` 从属性 setter 调用此方法时, 通常将此参数保留为默认值。 然后, 编译器会自动将参数值设置为调用属性的名称。

此类的完整代码如下所示。

```cs
using System.ComponentModel;
using System.Runtime.CompilerServices;

namespace ImHere
{
    public class BaseViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        protected void Set<T>(ref T field, T value, [CallerMemberName] string propertyName = null)
        {
            if (Equals(field, value)) return;
            field = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

## <a name="create-a-viewmodel-for-the-page"></a>为页面创建 ViewModel

`MainPage`将为电话号码提供一个文本输入控件和一个显示邮件的标签。 这些控件将绑定到 ViewModel 上的属性。

1. 创建一个在`ImHere` .net `MainViewModel` Standard 项目中调用的类。

1. 为`Xamarin.Forms`和`System.Threading.Tasks`添加 using 指令。

    ```cs
      using Xamarin.Forms;
      using System.Threading.Tasks;
     ```

1. 将此类设为公共, `BaseViewModel`并从中派生。
    ```cs
       public class MainViewModel : BaseViewModel
    ```
1. 添加两`string`个属性`PhoneNumbers` , `Message`每个都有一个支持字段。 在属性 setter 中, 使用基类`Set`方法更新值并引发`PropertyChanged`事件。

   ```cs
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
   ```

1. 添加名`SendLocationCommand`为的只读 command 属性。 此命令将具有`ICommand` `System.Windows.Input`命名空间中的类型。

    ```cs
    public ICommand SendLocationCommand { get; }
    ```

1. 向类中添加构造函数, 在此构造函数中, 将`SendLocationCommand`构造函数初始化为新的`Command`Xamarin。

    ```cs
    public MainViewModel()
    {
        SendLocationCommand = new Command(async () => await SendLocation());
    }

1. Create a `async` method called `SendLocation` and pass a lambda function that `await`s call to the constructor. The body of this method will be updated later in this module.

    ```cs
    async Task SendLocation()
    {
    }
    ```

此类的完整代码如下所示。

```cs
using System.Threading.Tasks;
using System.Windows.Input;
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

        async Task SendLocation()
        {
        }
    }
}
```

## <a name="create-the-user-interface"></a>创建用户界面

可以使用 XAML 构建 Forms ui。

1. 从`ImHere`项目`MainPage.xaml`中打开文件。 页面将在 XAML 编辑器中打开。

    > [!NOTE]
    >  该`ImHere.UWP`项目还包含一个名`MainPage.xaml`为的文件。 请确保您正在编辑 .net 标准库中的一个。

1. 在顶级中添加以下 XAML `ContentPage` , 以将 ViewModel 的实例设置为页面的绑定上下文。

    ```xml
    <ContentPage.BindingContext>
        <local:MainViewModel/>
    </ContentPage.BindingContext>
    ```

1. `StackLayout`使用以下代码覆盖:

     ```xml
    <StackLayout Padding="20">
        <Label Text="Phone numbers to send to:" HorizontalOptions="Start"/>
        <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
    </StackLayout>
    ```
    - 该`Editor`控件将用于添加电话号码, `Label`以上将介绍此字段对用户的用途。
    - `StackLayout`子控件以添加控件的顺序水平或垂直堆叠, 因此添加`Label`第一个会将其置于`Editor`。
    - `Editor`控件是多行输入控件, 允许用户输入多个电话号码, 每行一个。

    上`Text` `Editor`的属性绑定到上的`PhoneNumbers`属性。 `MainViewModel` 绑定的语法是将属性值设置为`"{Binding <property name>}"`。 大括号将告知 XAML 编译器此值是特殊的, 应与简单`string`的处理方式不同。

1. 在`Editor`控件`Button`下方添加一个。 我们将使用此按钮发送用户的位置。

    ```xml
    <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
            Command="{Binding SendLocationCommand}" />
    ```

    该`Command`属性绑定到 ViewModel 上`SendLocationCommand`的命令。 点击按钮时, 将执行命令。

1. 在`Button`控件`Label`下方添加一个。 将在此标签中显示状态消息。

    ```xml
    <Label Text="{Binding Message}"
           HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    ```

    此页面的完整代码如下所示。
    
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 xmlns:local="clr-namespace:ImHere"
                 x:Class="ImHere.MainPage">
        <ContentPage.BindingContext>
            <local:MainViewModel/>
        </ContentPage.BindingContext>
        <StackLayout Padding="20">
            <Label Text="Phone numbers to send to:" HorizontalOptions="Start"/>
            <Editor Text="{Binding PhoneNumbers}" HeightRequest="100"/>
            <Button Text="Send Location" BackgroundColor="Blue" TextColor="White"
                    Command="{Binding SendLocationCommand}" />
            <Label Text="{Binding Message}"
                   HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
        </StackLayout>
    </ContentPage>
    ```

1. 运行应用程序以查看新的 UI。 如果要在这种情况下验证绑定, 可以通过向属性或`SendLocation`方法添加断点来做到这一点。

    > [!NOTE]
    > 编译此应用程序时, 您将看到关于`SendLocation`缺少`await`修改者的警告。 可以忽略此警告, 因为在下一个单元中向此方法添加了更多代码后, 将会解决此警告。
    
    
    ![新的应用程序 UI](../media/3-new-ui.png)

## <a name="summary"></a>摘要

在此单元中, 您学习了如何使用 XAML 创建应用程序的 UI, 并使用 ViewModel 来处理应用程序的逻辑。 此外, 还学习了如何将 ViewModel 绑定到 UI。 在下一个单元中, 您将向 ViewModel 添加位置查找。
