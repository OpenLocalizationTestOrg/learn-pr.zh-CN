<span data-ttu-id="d7b77-101">您要构建的应用程序是与 Azure 功能交互的跨平台移动应用程序, 用于共享您的位置。</span><span class="sxs-lookup"><span data-stu-id="d7b77-101">The application you're building is a cross-platform mobile app that talks to the Azure Functions to share your location.</span></span> <span data-ttu-id="d7b77-102">在此单元中, 将使用 Visual Studio 创建一个空白移动应用程序, 并安装包含用于获取用户位置的 API 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="d7b77-102">In this unit, you'll create a blank mobile app using Visual Studio and install a NuGet package that has an API for getting the user's location.</span></span>

<span data-ttu-id="d7b77-103">若要完成此单元中的步骤, 您需要安装在 Visual Studio 中的 Xamarin 交叉平台 UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="d7b77-103">To complete the steps in this unit, you need Xamarin.Forms cross-platform UI toolkit installed in your Visual Studio.</span></span> <span data-ttu-id="d7b77-104">如果尚未安装, 请访问[安装 Xamarin](https://docs.microsoft.com/xamarin/get-started/installation/?tabs=windows)。</span><span class="sxs-lookup"><span data-stu-id="d7b77-104">If you do not have this already, visit [installing Xamarin](https://docs.microsoft.com/xamarin/get-started/installation/?tabs=windows).</span></span>

## <a name="create-the-xamarinforms-project"></a><span data-ttu-id="d7b77-105">创建 Xamarin. Forms 项目</span><span class="sxs-lookup"><span data-stu-id="d7b77-105">Create the Xamarin.Forms project</span></span>

1. <span data-ttu-id="d7b77-106">在 Visual Studio 中, 选择 " *File > 新建 > 项目 ...*"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-106">From Visual Studio, select *File > New > Project...*.</span></span>

1. <span data-ttu-id="d7b77-107">从左侧的树中, 选择 " *Visual c # > 跨平台*", 然后从中央面板中选择 "*移动应用程序 (Xamarin. Forms)* "。</span><span class="sxs-lookup"><span data-stu-id="d7b77-107">From the tree on the left-hand side, select *Visual C# > Cross-Platform* and then select *Mobile App (Xamarin.Forms)* from the panel in the center.</span></span>

1. <span data-ttu-id="d7b77-108">将解决方案命名为 "ImHere"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-108">Name the solution "ImHere".</span></span>

1. <span data-ttu-id="d7b77-109">为解决方案选择适当的位置。</span><span class="sxs-lookup"><span data-stu-id="d7b77-109">Choose an appropriate location for the solution.</span></span>

1. <span data-ttu-id="d7b77-110">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-110">Click **OK**.</span></span>

    !["新建解决方案" 对话框](../media/2-new-solution-dialog.png)

1. <span data-ttu-id="d7b77-112">从 "**新建跨平台应用程序**" 对话框中, 选择 "*空白" 应用*程序模板。</span><span class="sxs-lookup"><span data-stu-id="d7b77-112">From the **New Cross Platform App** dialog, select the *Blank App* template.</span></span>

1. <span data-ttu-id="d7b77-113">对于此模块, 您将构建一个 UWP 应用程序, 因此请取消选中 "iOS 和 Android" 并选中 "保留 UWP"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-113">For this module you will build a UWP app, so uncheck iOS and Android and leave UWP checked.</span></span>

1. <span data-ttu-id="d7b77-114">对于*代码共享策略*, 请选择 " **.net Standard**"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-114">For the *Code Sharing Strategy*, select **.NET Standard**.</span></span>

1. <span data-ttu-id="d7b77-115">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-115">Click **OK**.</span></span>

    !["配置新解决方案" 对话框](../media/2-configure-solution-dialog.png)

<span data-ttu-id="d7b77-117">Visual Studio 将为您创建两个项目</span><span class="sxs-lookup"><span data-stu-id="d7b77-117">Visual Studio will create two projects for you</span></span>

   - <span data-ttu-id="d7b77-118">名为的 UWP 应用`ImHere.UWP`</span><span class="sxs-lookup"><span data-stu-id="d7b77-118">a UWP app called `ImHere.UWP`</span></span>
   - <span data-ttu-id="d7b77-119">一个 .net 标准库,`ImHere`</span><span class="sxs-lookup"><span data-stu-id="d7b77-119">a .NET Standard library, `ImHere`</span></span>

<span data-ttu-id="d7b77-120">Xamarin. Forms 应用由两部分组成</span><span class="sxs-lookup"><span data-stu-id="d7b77-120">Xamarin.Forms apps are made up of two parts</span></span>
    - <span data-ttu-id="d7b77-121">一个或多个特定于平台的应用程序项目, 并且</span><span class="sxs-lookup"><span data-stu-id="d7b77-121">one or more platform-specific app projects, and</span></span>
    - <span data-ttu-id="d7b77-122">一个 (或多个) .net 标准库。</span><span class="sxs-lookup"><span data-stu-id="d7b77-122">one (or more) .NET Standard libraries.</span></span>

<span data-ttu-id="d7b77-123">特定于平台的应用程序项目包含在相关平台上运行应用程序所需的特定于平台的代码。</span><span class="sxs-lookup"><span data-stu-id="d7b77-123">The platform-specific app projects contain the platform-specific code needed to run an app on the relevant platform.</span></span> <span data-ttu-id="d7b77-124">然后, 这些项目启动跨平台 .net 标准库中定义的 Xamarin 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d7b77-124">These projects then launch a Xamarin.Forms app that is defined in a cross-platform .NET Standard library.</span></span> <span data-ttu-id="d7b77-125">在跨平台代码中构建应用程序, 在运行时, 您创建的任何用户界面都将转换为相关的特定于平台的 UI 组件。</span><span class="sxs-lookup"><span data-stu-id="d7b77-125">You build your app in cross-platform code and, at runtime, any user interfaces you create are translated into the relevant platform-specific UI components.</span></span>

## <a name="adding-xamarinessentials"></a><span data-ttu-id="d7b77-126">添加 Xamarin</span><span class="sxs-lookup"><span data-stu-id="d7b77-126">Adding Xamarin.Essentials</span></span>

<span data-ttu-id="d7b77-127">UWP、Android 和 iOS 平台提供了很多类似的功能, 可充分利用操作系统和硬件。</span><span class="sxs-lookup"><span data-stu-id="d7b77-127">The UWP, Android, and iOS platforms provide numerous similar capabilities that take advantage of the operating system and hardware.</span></span> <span data-ttu-id="d7b77-128">尽管存在这些相似之处, 但 api 的差异很大。</span><span class="sxs-lookup"><span data-stu-id="d7b77-128">Despite these similarities, the APIs are very different.</span></span> <span data-ttu-id="d7b77-129">从跨平台代码使用这些 api 需要在您向 .net 标准库公开的应用程序项目中编写特定于平台的代码。</span><span class="sxs-lookup"><span data-stu-id="d7b77-129">Using these APIs from cross-platform code requires writing platform-specific code in your app projects that you expose to your .NET Standard libraries.</span></span> <span data-ttu-id="d7b77-130">[Xamarin](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true)是一个 NuGet 包, 它提供跨多个 api 的跨平台抽象, 因此您无需编写特定于平台的代码。</span><span class="sxs-lookup"><span data-stu-id="d7b77-130">[Xamarin.Essentials](https://docs.microsoft.com/xamarin/essentials/?azure-portal=true) is a NuGet package that provides a cross-platform abstraction over a number of these APIs so that you don't need to write platform-specific code.</span></span> <span data-ttu-id="d7b77-131">这包括将在应用程序中使用的地理位置 api, 以获取用户的位置。</span><span class="sxs-lookup"><span data-stu-id="d7b77-131">This includes the geolocation APIs that you will use in your app to get the user's location.</span></span>

1. <span data-ttu-id="d7b77-132">右键单击 Visual Studio " `ImHere`解决方案资源管理器" 中的 "解决方案`ImHere` (顶级解决方案, 而不是 .net 标准项目)", 然后选择 "*管理解决方案的 NuGet 包 ...*"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-132">Right-click on the `ImHere` solution (the top level solution, not the `ImHere` .NET Standard project) in the Visual Studio Solution Explorer and select *Manage NuGet Packages for Solution...*.</span></span>

1. <span data-ttu-id="d7b77-133">选择 "**浏览**" 选项卡, 然后搜索 "Xamarin"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-133">Select the **Browse** tab and search for "Xamarin.Essentials".</span></span> <span data-ttu-id="d7b77-134">此包当前可用作预发布 NuGet 包, 请选中 "*包含 prelease* " 框。</span><span class="sxs-lookup"><span data-stu-id="d7b77-134">This package is currently available as a prerelease NuGet package, so check the *include prelease* box.</span></span>

    > [!TIP]
    > <span data-ttu-id="d7b77-135">如果看不到 Xamarin NuGet 包, 则选中 "*包含 prelease* " 的双重检查。</span><span class="sxs-lookup"><span data-stu-id="d7b77-135">If you do not see the Xamarin.Essentials NuGet package, double check that *include prelease* is checked.</span></span> 

1. <span data-ttu-id="d7b77-136">选择 " **Xamarin** NuGet 包"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-136">Select the **Xamarin.Essentials** NuGet package.</span></span>

1. <span data-ttu-id="d7b77-137">在右侧的 "项目" 列表中检查所有项目。</span><span class="sxs-lookup"><span data-stu-id="d7b77-137">Check all your projects in the project list on the right-hand side.</span></span>

1. <span data-ttu-id="d7b77-138">单击 "**安装**" 按钮以安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="d7b77-138">Click the **Install** button to install the NuGet package.</span></span> <span data-ttu-id="d7b77-139">你需要接受许可证才能继续。</span><span class="sxs-lookup"><span data-stu-id="d7b77-139">You'll need to accept the license to continue.</span></span>

    ![将 Xamarin NuGet 包添加到解决方案中的所有项目](../media/2-add-essentials-nuget.png)

## <a name="building-and-running-the-app"></a><span data-ttu-id="d7b77-141">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="d7b77-141">Building and running the app</span></span>

1. <span data-ttu-id="d7b77-142">右键单击 "解决方案资源`ImHere.UWP`管理器" 中的项目, 然后选择 "*设为启动项目*"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-142">Right-click on the `ImHere.UWP` project in Solution Explorer and select *Set as StartUp project*.</span></span>

1. <span data-ttu-id="d7b77-143">将 "生成配置" 设置为 "**调试**"、"用于**x86**的平台" 和 "要在**本地计算机**上运行的设备"。</span><span class="sxs-lookup"><span data-stu-id="d7b77-143">Set the build configuration to **Debug**, the platform to **x86**, and the device to run on to **Local Machine**.</span></span>

    ![设置要在本地设备上运行的调试 x86 配置](../media/2-debug-configuration.png)

1. <span data-ttu-id="d7b77-145">开始调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="d7b77-145">Start debugging the app.</span></span>

    ![运行的应用程序](../media/2-debuging-app.png)

## <a name="summary"></a><span data-ttu-id="d7b77-147">摘要</span><span class="sxs-lookup"><span data-stu-id="d7b77-147">Summary</span></span>

<span data-ttu-id="d7b77-148">在此单位中, 您创建了一个新的 Xamarin。 Forms 跨平台移动应用并添加了 xamarin NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="d7b77-148">In this unit, you created a new Xamarin.Forms cross-platform mobile app and added the Xamarin.Essentials NuGet package.</span></span> <span data-ttu-id="d7b77-149">接下来, 您将了解如何构建移动应用程序 UI 和逻辑。</span><span class="sxs-lookup"><span data-stu-id="d7b77-149">Next, you'll learn how to build up the mobile app UI and logic.</span></span>