<span data-ttu-id="1c233-101">您要构建的应用程序是一个跨平台的移动应用程序, 它与 Azure 功能进行交互以共享您的位置。</span><span class="sxs-lookup"><span data-stu-id="1c233-101">The application you're building is a cross-platform mobile app that talks to an Azure function to share your location.</span></span> <span data-ttu-id="1c233-102">在此单元中, 将使用 Visual Studio 创建空白移动应用程序, 并安装包含用于获取用户位置的 API 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1c233-102">In this unit, you create the blank mobile app using Visual Studio and install a NuGet package that has an API for getting the user's location.</span></span>

## <a name="create-the-xamarinforms-project"></a><span data-ttu-id="1c233-103">创建 Xamarin. Forms 项目</span><span class="sxs-lookup"><span data-stu-id="1c233-103">Create the Xamarin.Forms project</span></span>

1. <span data-ttu-id="1c233-104">在 Visual Studio 中, 选择 "*文件"-">New->Project ...*"。</span><span class="sxs-lookup"><span data-stu-id="1c233-104">From Visual Studio, select *File->New->Project...*.</span></span>

1. <span data-ttu-id="1c233-105">从左侧的树中, 选择 " *Visual c #->Cross* ", 然后从中央面板中选择 "*移动应用程序 (Xamarin. Forms)* "。</span><span class="sxs-lookup"><span data-stu-id="1c233-105">From the tree on the left-hand side, select *Visual C#->Cross-Platform* and then select *Mobile App (Xamarin.Forms)* from the panel in the center.</span></span>

1. <span data-ttu-id="1c233-106">将解决方案命名为 "ImHere"。</span><span class="sxs-lookup"><span data-stu-id="1c233-106">Name the solution "ImHere".</span></span>

1. <span data-ttu-id="1c233-107">为解决方案选择适当的位置。</span><span class="sxs-lookup"><span data-stu-id="1c233-107">Choose an appropriate location for the solution.</span></span>

1. <span data-ttu-id="1c233-108">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="1c233-108">Click **OK**.</span></span>

    !["新建解决方案" 对话框](../media/2-new-solution-dialog.png)

1. <span data-ttu-id="1c233-110">从 "**新建跨平台应用程序**" 对话框中, 选择 "*空白" 应用*程序模板。</span><span class="sxs-lookup"><span data-stu-id="1c233-110">From the **New Cross Platform App** dialog, select the *Blank App* template.</span></span>

1. <span data-ttu-id="1c233-111">对于此模块, 您将构建一个 UWP 应用程序, 因此请取消选中 "iOS 和 Android" 并选中 "保留 UWP"。</span><span class="sxs-lookup"><span data-stu-id="1c233-111">For this module you will build a UWP app, so uncheck iOS and Android and leave UWP checked.</span></span>

1. <span data-ttu-id="1c233-112">对于*代码共享策略*, 请选择 " **.net Standard**"。</span><span class="sxs-lookup"><span data-stu-id="1c233-112">For the *Code Sharing Strategy*, select **.NET Standard**.</span></span>

1. <span data-ttu-id="1c233-113">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="1c233-113">Click **OK**.</span></span>

    !["配置新解决方案" 对话框](../media/2-configure-solution-dialog.png)

<span data-ttu-id="1c233-115">Visual Studio 将为您创建两个项目: 一个名`ImHere.UWP`为的 UWP 应用程序和一个`ImHere`.net 标准库。</span><span class="sxs-lookup"><span data-stu-id="1c233-115">Visual Studio will create two projects for you - a UWP app called `ImHere.UWP` and a .NET Standard library, `ImHere`.</span></span> <span data-ttu-id="1c233-116">Xamarin. Forms 应用程序由两部分组成-一个或多个平台特定的应用程序项目以及一个 (或多个) .net 标准库。</span><span class="sxs-lookup"><span data-stu-id="1c233-116">Xamarin.Forms apps are made up of two parts - one or more platform-specific app projects and one (or more) .NET Standard libraries.</span></span> <span data-ttu-id="1c233-117">特定于平台的应用程序项目包含在相关平台上运行应用程序所需的特定于平台的代码。</span><span class="sxs-lookup"><span data-stu-id="1c233-117">The platform-specific app projects contain the platform-specific code needed to run an app on the relevant platform.</span></span> <span data-ttu-id="1c233-118">然后, 这些项目启动跨平台 .net 标准库中定义的 Xamarin 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c233-118">These projects then launch a Xamarin.Forms app that is defined in a cross-platform .NET Standard library.</span></span> <span data-ttu-id="1c233-119">在跨平台代码中构建应用程序, 在运行时, 您创建的任何用户界面都将转换为相关的特定于平台的 UI 组件。</span><span class="sxs-lookup"><span data-stu-id="1c233-119">You build your app in cross-platform code and, at runtime, any user interfaces you create are translated into the relevant platform-specific UI components.</span></span>

## <a name="adding-xamarinessentials"></a><span data-ttu-id="1c233-120">添加 Xamarin</span><span class="sxs-lookup"><span data-stu-id="1c233-120">Adding Xamarin.Essentials</span></span>

<span data-ttu-id="1c233-121">UWP、Android 和 iOS 平台提供了很多类似的功能, 可充分利用操作系统和硬件。</span><span class="sxs-lookup"><span data-stu-id="1c233-121">The UWP, Android, and iOS platforms provide numerous similar capabilities that take advantage of the operating system and hardware.</span></span> <span data-ttu-id="1c233-122">尽管存在这些相似之处, 但 api 的差异很大。</span><span class="sxs-lookup"><span data-stu-id="1c233-122">Despite these similarities, the APIs are very different.</span></span> <span data-ttu-id="1c233-123">从跨平台代码使用这些 api 需要在您向 .net 标准库公开的应用程序项目中编写特定于平台的代码。</span><span class="sxs-lookup"><span data-stu-id="1c233-123">Using these APIs from cross-platform code requires writing platform-specific code in your app projects that you expose to your .NET Standard libraries.</span></span> <span data-ttu-id="1c233-124">[Xamarin](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true)是一个 NuGet 包, 它提供跨多个 api 的跨平台抽象, 因此您无需编写特定于平台的代码。</span><span class="sxs-lookup"><span data-stu-id="1c233-124">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true) is a NuGet package that provides a cross-platform abstraction over a number of these APIs so that you don't need to write platform-specific code.</span></span> <span data-ttu-id="1c233-125">这包括将在应用程序中使用的地理位置 api, 以获取用户的位置。</span><span class="sxs-lookup"><span data-stu-id="1c233-125">This includes the geolocation APIs that you will use in your app to get the user's location.</span></span>

1. <span data-ttu-id="1c233-126">右键单击 Visual Studio " `ImHere`解决方案资源管理器" 中的 "解决方案`ImHere` (顶级解决方案, 而不是 .net 标准项目)", 然后选择 "*管理解决方案的 NuGet 包 ...*"。</span><span class="sxs-lookup"><span data-stu-id="1c233-126">Right-click on the `ImHere` solution (the top level solution, not the `ImHere` .NET Standard project) in the Visual Studio Solution Explorer and select *Manage NuGet Packages for Solution...*.</span></span>

1. <span data-ttu-id="1c233-127">选择 "**浏览**" 选项卡, 然后搜索 "Xamarin"。</span><span class="sxs-lookup"><span data-stu-id="1c233-127">Select the **Browse** tab and search for "Xamarin.Essentials".</span></span> <span data-ttu-id="1c233-128">此包当前可用作预发布 NuGet 包, 请选中 "*包含 prelease* " 框。</span><span class="sxs-lookup"><span data-stu-id="1c233-128">This package is currently available as a prerelease NuGet package, so check the *include prelease* box.</span></span>

    > [!TIP]
    > <span data-ttu-id="1c233-129">如果看不到 Xamarin NuGet 包, 则选中 "*包含 prelease* " 的双重检查。</span><span class="sxs-lookup"><span data-stu-id="1c233-129">If you do not see the Xamarin.Essentials NuGet package, double check that *include prelease* is checked.</span></span> 

1. <span data-ttu-id="1c233-130">选择 " **Xamarin** NuGet 包"。</span><span class="sxs-lookup"><span data-stu-id="1c233-130">Select the **Xamarin.Essentials** NuGet package.</span></span>

1. <span data-ttu-id="1c233-131">在右侧的 "项目" 列表中检查所有项目。</span><span class="sxs-lookup"><span data-stu-id="1c233-131">Check all your projects in the project list on the right-hand side.</span></span>

1. <span data-ttu-id="1c233-132">单击 "**安装**" 按钮以安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1c233-132">Click the **Install** button to install the NuGet package.</span></span> <span data-ttu-id="1c233-133">你需要接受许可证才能继续。</span><span class="sxs-lookup"><span data-stu-id="1c233-133">You'll need to accept the license to continue.</span></span>

    ![将 Xamarin NuGet 包添加到解决方案中的所有项目](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a><span data-ttu-id="1c233-135">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1c233-135">Building and running the app</span></span>

1. <span data-ttu-id="1c233-136">右键单击 "解决方案资源`ImHere.UWP`管理器" 中的项目, 然后选择 "*设为启动项目*"。</span><span class="sxs-lookup"><span data-stu-id="1c233-136">Right-click on the `ImHere.UWP` project in Solution Explorer and select *Set as StartUp project*.</span></span>

1. <span data-ttu-id="1c233-137">将 "生成配置" 设置为 "**调试**"、"用于**x86**的平台" 和 "要在**本地计算机**上运行的设备"。</span><span class="sxs-lookup"><span data-stu-id="1c233-137">Set the build configuration to **Debug**, the platform to **x86**, and the device to run on to **Local Machine**.</span></span>

    ![设置要在本地设备上运行的调试 x86 配置](../media/2-debug-configuration.png)

1. <span data-ttu-id="1c233-139">开始调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c233-139">Start debugging the app.</span></span>

    ![运行的应用程序](../media/2-debuging-app.png)

## <a name="summary"></a><span data-ttu-id="1c233-141">摘要</span><span class="sxs-lookup"><span data-stu-id="1c233-141">Summary</span></span>

<span data-ttu-id="1c233-142">在此单位中, 您创建了一个新的 Xamarin。 Forms 跨平台移动应用并添加了 xamarin NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1c233-142">In this unit, you created a new Xamarin.Forms cross-platform mobile app and added the Xamarin.Essentials NuGet package.</span></span> <span data-ttu-id="1c233-143">接下来, 您将了解如何构建移动应用程序 UI 和逻辑。</span><span class="sxs-lookup"><span data-stu-id="1c233-143">Next, you learn how to build up the mobile app UI and logic.</span></span>