<span data-ttu-id="430ae-101">应用和 Azure 函数现在已完成并在本地运行。</span><span class="sxs-lookup"><span data-stu-id="430ae-101">The app and Azure Functions are now complete and running locally.</span></span> <span data-ttu-id="430ae-102">在此单元中, 你将把函数发布到 Azure 以在云中运行。</span><span class="sxs-lookup"><span data-stu-id="430ae-102">In this unit, you'll publish the function to Azure to run in the cloud.</span></span>

<span data-ttu-id="430ae-103">你将从 Visual Studio 发布函数。</span><span class="sxs-lookup"><span data-stu-id="430ae-103">You'll publish your function from Visual Studio.</span></span> <span data-ttu-id="430ae-104">这是开始使用概念证明、原型和学习的好方法, 但对于生产质量的应用程序,**不**应使用此方法。</span><span class="sxs-lookup"><span data-stu-id="430ae-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="430ae-105">您应使用某种形式的基于 CI 的部署。</span><span class="sxs-lookup"><span data-stu-id="430ae-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="430ae-106">您可以在[Azure 函数部署文档](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true)中阅读有关此操作的详细信息。</span><span class="sxs-lookup"><span data-stu-id="430ae-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true).</span></span>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="430ae-107">将应用程序发布到 Azure</span><span class="sxs-lookup"><span data-stu-id="430ae-107">Publishing your app to Azure</span></span>

<span data-ttu-id="430ae-108">azure 函数可从 Visual Studio 内部发布到 azure。</span><span class="sxs-lookup"><span data-stu-id="430ae-108">Azure Functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="430ae-109">如果本地 Azure 函数运行时仍从上一个单元运行, 请停止运行时。</span><span class="sxs-lookup"><span data-stu-id="430ae-109">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="430ae-110">右键单击 "解决方案资源`ImHere.Functions`管理器" 中的应用程序, 然后选择 "*发布 ...*"。</span><span class="sxs-lookup"><span data-stu-id="430ae-110">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![右键单击 "函数" 应用程序上的 "发布"](../media/8-right-click-publish.png)

1. <span data-ttu-id="430ae-112">从 "**选择发布目标**" 对话框中, 选择 " *azure 函数应用*", 并选择 " **azure 应用服务**", 然后选择 "*新建*"。</span><span class="sxs-lookup"><span data-stu-id="430ae-112">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="430ae-113">单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="430ae-113">Click **Publish**.</span></span>

    ![创建要发布到的新 Azure 应用服务](../media/8-pick-publish-target.png)

1. <span data-ttu-id="430ae-115">登录到你的 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="430ae-115">Sign in to your Azure account.</span></span>

1. <span data-ttu-id="430ae-116">为你的应用程序输入一个名称。</span><span class="sxs-lookup"><span data-stu-id="430ae-116">Enter a name for you app.</span></span>

1. <span data-ttu-id="430ae-117">选择你的_订阅_、_资源组_、_托管计划_和_存储帐户_。</span><span class="sxs-lookup"><span data-stu-id="430ae-117">Select your _Subscription_, _Resource Group_, _Hosting Plan_, and _Storage Account_.</span></span>

1. <span data-ttu-id="430ae-118">单击 "**创建**" 以设置 azure 上的所有资源并发布 azure 函数应用。</span><span class="sxs-lookup"><span data-stu-id="430ae-118">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![创建应用服务](../media/8-create-app-service.png)

1. <span data-ttu-id="430ae-120">系统可能会询问您是否要更新 Azure 上的函数版本。</span><span class="sxs-lookup"><span data-stu-id="430ae-120">You may be asked if you want to update the functions version on Azure.</span></span> <span data-ttu-id="430ae-121">如果显示此对话框, 请选择 **"是"** 以确保您的 function app 使用最新的 Azure 函数运行时版本进行发布。</span><span class="sxs-lookup"><span data-stu-id="430ae-121">If this dialog appears, select **Yes** to ensure your function app is published with the latest Azure Functions runtime version.</span></span>
    <span data-ttu-id="430ae-122">!["更新 Azure 函数" 对话框](../media/8-update-functions-on-azure.png)</span><span class="sxs-lookup"><span data-stu-id="430ae-122">![The update Azure Functions dialog](../media/8-update-functions-on-azure.png)</span></span>

<span data-ttu-id="430ae-123">预配将需要几分钟时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="430ae-123">Provisioning will take a couple of minutes to complete.</span></span> <span data-ttu-id="430ae-124">将预配以下资源:</span><span class="sxs-lookup"><span data-stu-id="430ae-124">The following resources will be provisioned:</span></span>

- <span data-ttu-id="430ae-125">一个存储帐户, 用于存储 Azure 函数应用所需的文件</span><span class="sxs-lookup"><span data-stu-id="430ae-125">A storage account to store the files needed for the Azure Functions app</span></span>
- <span data-ttu-id="430ae-126">用于管理 Azure 函数应用所需的计算资源的应用程序服务计划</span><span class="sxs-lookup"><span data-stu-id="430ae-126">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
- <span data-ttu-id="430ae-127">运行 Azure 函数的应用程序服务</span><span class="sxs-lookup"><span data-stu-id="430ae-127">The App Service that runs the Azure Functions</span></span>

<span data-ttu-id="430ae-128">函数现在将发布, 并可在**https://\<\>** 上进行调用。 azurewebsites.net/api/SendLocation。</span><span class="sxs-lookup"><span data-stu-id="430ae-128">The function will now be published and available to call at **https://\<your-app-name\>.azurewebsites.net/api/SendLocation**.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="430ae-129">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="430ae-129">Configuring your app</span></span>

<span data-ttu-id="430ae-130">当 Azure 函数在本地运行时, 它使用的是存储在`local.settings.json`文件中的 Twilio 凭据。</span><span class="sxs-lookup"><span data-stu-id="430ae-130">When the Azure Functions was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="430ae-131">顾名思义, 此文件适用于本地设置, 不适用于 Azure 设置。</span><span class="sxs-lookup"><span data-stu-id="430ae-131">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="430ae-132">在 azure 函数可以在 azure 中调用之前, 需要`TwilioAccountSid`配置`TwilioAuthToken`和设置。</span><span class="sxs-lookup"><span data-stu-id="430ae-132">Before the Azure Functions can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="430ae-133">从 "发布" 选项卡中, 单击 "**管理应用程序设置**" 选项。</span><span class="sxs-lookup"><span data-stu-id="430ae-133">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    !["管理应用程序设置" 选项](../media/8-application-settings-option.png)

1. <span data-ttu-id="430ae-135">"**应用程序设置**" 对话框将显示带有本地和远程值的应用程序设置-本地来自您`local.settings.json`的文件, 远程值是在 Azure 中托管时, 您的函数将使用的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="430ae-135">The **Application Settings** dialog will show application settings with both a local and remote value - the local coming from your `local.settings.json` file, and the remote value is the one your function will use when it is hosted in Azure.</span></span> <span data-ttu-id="430ae-136">将 " **TwilioAccountSid** " 和 " **TwilioAuthToken** " 值的*本地*框中的值复制到*远程*框中。</span><span class="sxs-lookup"><span data-stu-id="430ae-136">Copy the values from the *Local* to the *Remote* boxes for the **TwilioAccountSid** and **TwilioAuthToken** values.</span></span>

    ![在应用程序设置中设置 Twilio 凭据](../media/8-set-creds-in-app-settings.png)

1. <span data-ttu-id="430ae-138">单击"确定"。</span><span class="sxs-lookup"><span data-stu-id="430ae-138">Click **OK**.</span></span> <span data-ttu-id="430ae-139">这会将值发布到 Azure 函数应用。</span><span class="sxs-lookup"><span data-stu-id="430ae-139">This will publish the values to the Azure Functions app.</span></span>

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="430ae-140">将移动应用程序指向 Azure</span><span class="sxs-lookup"><span data-stu-id="430ae-140">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="430ae-141">从 "发布" 选项卡中, 使用值旁边的 "**复制到剪贴板**" 按钮复制**网站 URL** 。</span><span class="sxs-lookup"><span data-stu-id="430ae-141">From the Publish tab, copy the **Site URL** using the **Copy to clipboard** button next to the value.</span></span>

    ![从 "发布" 选项卡复制网站 URL](../media/8-copy-site-url.png)

1. <span data-ttu-id="430ae-143">`MainViewModel`从`ImHere`项目中打开。</span><span class="sxs-lookup"><span data-stu-id="430ae-143">Open the `MainViewModel` from the `ImHere` project.</span></span>

1. <span data-ttu-id="430ae-144">将`baseUrl`字段的值更新为从 "发布" 选项卡复制的网站 URL。</span><span class="sxs-lookup"><span data-stu-id="430ae-144">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="430ae-145">测试</span><span class="sxs-lookup"><span data-stu-id="430ae-145">Test it out</span></span>

1. <span data-ttu-id="430ae-146">将`ImHere.UWP`应用程序设置为启动应用程序并运行它。</span><span class="sxs-lookup"><span data-stu-id="430ae-146">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

1. <span data-ttu-id="430ae-147">输入电话号码, 然后单击 "**发送位置**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="430ae-147">Enter a phone number and click the **Send Location** button.</span></span>

1. <span data-ttu-id="430ae-148">您应以 SMS 消息的形式收到该位置。</span><span class="sxs-lookup"><span data-stu-id="430ae-148">You should receive the location as an SMS message.</span></span>

1. <span data-ttu-id="430ae-149">如果您收到一项*服务不可用*错误, 请检查您的函数应用程序使用的是哪个版本的 "Twilio" NuGet 包, 它应为 3.0.0-rc1, 而不是3.0.0。</span><span class="sxs-lookup"><span data-stu-id="430ae-149">If you get back a *Service Unavailable* error, check what version of the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package your functions app is using, it should be 3.0.0-rc1, NOT 3.0.0.</span></span>
1. <span data-ttu-id="430ae-150">如果您收到一项*服务不可用*错误, 请检查您的函数应用程序使用的是哪个版本的 "Twilio" NuGet 包, 它应为 3.0.0-rc1,**而不**是3.0.0。</span><span class="sxs-lookup"><span data-stu-id="430ae-150">If you get back a *Service Unavailable* error, check what version of the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package your functions app is using, it should be 3.0.0-rc1, **NOT** 3.0.0.</span></span>

## <a name="summary"></a><span data-ttu-id="430ae-151">摘要</span><span class="sxs-lookup"><span data-stu-id="430ae-151">Summary</span></span>

<span data-ttu-id="430ae-152">在此单元中, 你学习了如何在 Visual Studio 中将 azure 函数项目发布到 azure, 并配置应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="430ae-152">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>