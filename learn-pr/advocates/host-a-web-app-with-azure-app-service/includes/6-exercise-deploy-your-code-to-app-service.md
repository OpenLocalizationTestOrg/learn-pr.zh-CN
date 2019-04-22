<span data-ttu-id="fe889-101">在此单元中, 你将 web 应用程序部署到应用服务。</span><span class="sxs-lookup"><span data-stu-id="fe889-101">In this unit, you'll deploy your web application to App Service.</span></span>

::: zone pivot="csharp"

## <a name="use-a-local-git-repository-as-your-deployment-option"></a><span data-ttu-id="fe889-102">将本地 Git 存储库用作部署选项</span><span class="sxs-lookup"><span data-stu-id="fe889-102">Use a local Git repository as your deployment option</span></span>

<span data-ttu-id="fe889-103">接下来, 我们将为 Git 部署配置应用服务。</span><span class="sxs-lookup"><span data-stu-id="fe889-103">Next, we'll configure App Service for Git deployment.</span></span> <span data-ttu-id="fe889-104">这将使我们可以通过将我们的代码推送到 Azure 中的 Git 终结点来部署应用程序的新版本。</span><span class="sxs-lookup"><span data-stu-id="fe889-104">This will enable us to deploy new versions of our application by pushing our code to a Git endpoint in Azure.</span></span>

1. <span data-ttu-id="fe889-105">在应用服务 web 应用程序的 "概述" 页中, 单击左侧导航栏上的 "**部署中心**" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="fe889-105">In the overview page for your App Service web app, click the **Deployment Center** menu item on the left-hand navigation.</span></span>

1. <span data-ttu-id="fe889-106">单击 "**本地 Git**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-106">Click on **Local Git**.</span></span>

1. <span data-ttu-id="fe889-107">单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-107">Click **Continue**.</span></span>

1. <span data-ttu-id="fe889-108">单击 "**应用程序服务 Kudu" "生成服务器**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-108">Click on **App Service Kudu build server**.</span></span>

1. <span data-ttu-id="fe889-109">单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-109">Click **Continue**.</span></span>

1. <span data-ttu-id="fe889-110">查看您的设置, 然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-110">Review your settings, then click **Finish**.</span></span>

## <a name="create-deployment-credentials"></a><span data-ttu-id="fe889-111">创建部署凭据</span><span class="sxs-lookup"><span data-stu-id="fe889-111">Create deployment credentials</span></span>

<span data-ttu-id="fe889-112">在可以使用 git 进行部署之前, 应用程序服务要求您设置可用于从 Git 客户端进行身份验证的用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="fe889-112">Before you can deploy with Git, App Service requires you to set up a username/password that can be used to authenticate from the Git client.</span></span>

1. <span data-ttu-id="fe889-113">单击 "**部署凭据**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fe889-113">Click the **Deployment Credentials** button.</span></span>

1. <span data-ttu-id="fe889-114">单击 "**用户凭据**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-114">Click on **User Credentials**.</span></span>

1. <span data-ttu-id="fe889-115">如果还未填充, 请设置**Username**字段。</span><span class="sxs-lookup"><span data-stu-id="fe889-115">If not already populated, set the **Username** field.</span></span> <span data-ttu-id="fe889-116">这不一定与 Azure 帐户用户名相同。</span><span class="sxs-lookup"><span data-stu-id="fe889-116">This does not have to be the same as your Azure account username.</span></span>

1. <span data-ttu-id="fe889-117">输入您选择的**密码**, 然后确认您的密码。</span><span class="sxs-lookup"><span data-stu-id="fe889-117">Enter a **Password** of your choice, and then confirm your password.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe889-118">请确保您不会忘记您的用户名和密码!</span><span class="sxs-lookup"><span data-stu-id="fe889-118">Make sure you don't forget your username and password!</span></span> <span data-ttu-id="fe889-119">稍后当我们开始上载代码并将其部署到 Azure 时, 你将需要它们。</span><span class="sxs-lookup"><span data-stu-id="fe889-119">You will need them later when we start uploading and deploying our code to Azure.</span></span>

1. <span data-ttu-id="fe889-120">单击 "**保存凭据**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-120">Click on **Save Credentials**.</span></span>

1. <span data-ttu-id="fe889-121">记下**Git 克隆 Uri**, 它是将用作本地应用程序代码存储库的**远程**的 Azure Git 存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="fe889-121">Take note of the **Git Clone Uri**, which is the Azure Git repository URL that you will use as a **remote** for your local application code repository.</span></span>

## <a name="set-up-git-on-cloud-shell"></a><span data-ttu-id="fe889-122">在云命令行管理程序上设置 Git</span><span class="sxs-lookup"><span data-stu-id="fe889-122">Set up Git on Cloud Shell</span></span>

<span data-ttu-id="fe889-123">Git 已安装 Azure 云命令行管理程序, 但你需要为你的云命令行管理程序帐户设置用户名和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="fe889-123">Git is already installed Azure Cloud Shell but you'll want to set your username and email for your cloud shell account.</span></span>

1. <span data-ttu-id="fe889-124">在右侧的云命令行管理程序中, 键入以下命令, 将`[your name]`和`[your email]`占位符替换为您自己的姓名和电子邮件 (不带大括号):</span><span class="sxs-lookup"><span data-stu-id="fe889-124">In the Cloud Shell on the right, type the following commands, replacing the `[your name]` and `[your email]` placeholders with your own name and email (without the braces):</span></span>

    ```bash
    git config --global user.name "[your name]"
    git config --global user.email "[your email]"
    ```

1. <span data-ttu-id="fe889-125">若要验证您的信息是否已由 Git 记录, 请键入以下命令:</span><span class="sxs-lookup"><span data-stu-id="fe889-125">To verify that your information has been recorded by Git, type the following command:</span></span>

    ```bash
    cat ~/.gitconfig
    ```

   <span data-ttu-id="fe889-126">您应看到以下内容, 并显示您的姓名和电子邮件:</span><span class="sxs-lookup"><span data-stu-id="fe889-126">You should be seeing the following, with your name and email shown:</span></span>

    ```output
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-code"></a><span data-ttu-id="fe889-127">为您的代码初始化本地 Git 存储库</span><span class="sxs-lookup"><span data-stu-id="fe889-127">Initialize a local Git repository for your code</span></span>

<span data-ttu-id="fe889-128">若要开始使用 Git, 您需要为您的 .net Core 应用程序代码初始化本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="fe889-128">To start using Git, you need to initialize a local Git repository for your .NET Core application code.</span></span>

1. <span data-ttu-id="fe889-129">请确保您在之前创建的项目文件夹中。</span><span class="sxs-lookup"><span data-stu-id="fe889-129">Make sure you are in the project folder you created earlier.</span></span>

    ```bash
    cd ~/BestBikeApp/
    ```

1. <span data-ttu-id="fe889-130">通过发出以下命令初始化新的 Git 存储库:</span><span class="sxs-lookup"><span data-stu-id="fe889-130">Initialize a new Git repository by issuing the following command:</span></span>

    ```bash
    git init
    ```

    <span data-ttu-id="fe889-131">如果该命令成功执行, 您将收到如下所示的消息:</span><span class="sxs-lookup"><span data-stu-id="fe889-131">If the command is successful, you receive a message like the following:</span></span>

    ```output
    Initialized empty Git repository in /home/{your-user}/BestBikeApp/.git/
    ```

1. <span data-ttu-id="fe889-132">将所有应用程序文件暂存到 Git。</span><span class="sxs-lookup"><span data-stu-id="fe889-132">Stage all the application files to Git.</span></span>

   <span data-ttu-id="fe889-133">下一步是让 Git 了解你的应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="fe889-133">The next step is to let Git know about your application files.</span></span> <span data-ttu-id="fe889-134">为此, 请添加工作目录的所有文件, 以便通过 Git**暂存**这些文件。</span><span class="sxs-lookup"><span data-stu-id="fe889-134">Do that by adding all the files of the working directory so that they get **staged** by Git.</span></span> <span data-ttu-id="fe889-135">键入以下命令:</span><span class="sxs-lookup"><span data-stu-id="fe889-135">Type the following command:</span></span>

    ```bash
    git add .
    ```

    <span data-ttu-id="fe889-136">上面的命令将 "." 代表的所有文件添加到 Git 的暂存状态。</span><span class="sxs-lookup"><span data-stu-id="fe889-136">The command above adds all files, represented by the ".", to the staging state of Git.</span></span>

1. <span data-ttu-id="fe889-137">现在, 你需要将所做的更改提交到 Git。</span><span class="sxs-lookup"><span data-stu-id="fe889-137">Now, you need to commit your changes to Git.</span></span>

   <span data-ttu-id="fe889-138">使用 Git 暂存文件后, 需要将文件提交到本地计算机上的**Git 提交历史记录**。</span><span class="sxs-lookup"><span data-stu-id="fe889-138">Once you stage the files with Git, you need to commit your files to the **Git commit history** on your local machine.</span></span> <span data-ttu-id="fe889-139">为此, 请键入以下命令:</span><span class="sxs-lookup"><span data-stu-id="fe889-139">You do that by typing the following command:</span></span>

    ```bash
   git commit -m "Initial commit"
    ```

   <span data-ttu-id="fe889-140">该`commit`命令接受`-m`参数以在正在创建的提交中包含一封邮件。</span><span class="sxs-lookup"><span data-stu-id="fe889-140">The `commit` command accepts the `-m` argument to include a message with the commit you are creating.</span></span> <span data-ttu-id="fe889-141">稍后, 当你将代码推送到 Azure 时, 你将能够看到与此特定提交一起存储的相同消息。</span><span class="sxs-lookup"><span data-stu-id="fe889-141">Later on, when you push your code to Azure, you will be able to see the same message stored with this particular commit.</span></span>

## <a name="add-a-remote-for-the-local-git-repository"></a><span data-ttu-id="fe889-142">为本地 Git 存储库添加远程</span><span class="sxs-lookup"><span data-stu-id="fe889-142">Add a remote for the local Git repository</span></span>

<span data-ttu-id="fe889-143">此时, 您已成功初始化了新的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="fe889-143">At this point, you have successfully initialized a new local Git repository.</span></span> <span data-ttu-id="fe889-144">此外, 您已将所有应用程序文件提交到 Git。</span><span class="sxs-lookup"><span data-stu-id="fe889-144">In addition, you've committed all of your application files to Git.</span></span> <span data-ttu-id="fe889-145">剩下的工作是添加一个**远程**, 将本地 Git 存储库连接到在 Azure 上托管的存储库。</span><span class="sxs-lookup"><span data-stu-id="fe889-145">What remains is to add a **remote** to connect your local Git repository to that hosted on Azure.</span></span>

<span data-ttu-id="fe889-146">为此, 需要执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="fe889-146">To do so, you need to:</span></span>

1. <span data-ttu-id="fe889-147">复制上面看到的**Git 克隆 url** 。</span><span class="sxs-lookup"><span data-stu-id="fe889-147">Copy the **Git clone url** that you saw above.</span></span>

1. <span data-ttu-id="fe889-148">复制后, 返回到**终端**窗口并使用您的 url 发出以下 Git 命令:</span><span class="sxs-lookup"><span data-stu-id="fe889-148">Once copied, you go back to the **Terminal** window and issue the following Git command with your url:</span></span>

    ```bash
    git remote add origin https://[your-username]@BESTBIKE.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    <span data-ttu-id="fe889-149">上面的 git 命令将本地 git 存储库连接到 Azure 上托管的存储库`[your-username]` , 其中是您在创建部署凭据时指定的用户名。</span><span class="sxs-lookup"><span data-stu-id="fe889-149">The above Git command connects your local Git repository to the one hosted on Azure, where `[your-username]` is the username that you specified when you created your deployment credentials.</span></span> <span data-ttu-id="fe889-150">现在, 您可以通过推送代码来部署代码。</span><span class="sxs-lookup"><span data-stu-id="fe889-150">Now you can deploy your code by pushing to it.</span></span>

1. <span data-ttu-id="fe889-151">若要验证上面的命令, 请键入以下 Git 命令:</span><span class="sxs-lookup"><span data-stu-id="fe889-151">To verify the above command, type the following Git command:</span></span>

    ```bash
    git remote -v
    ```

    <span data-ttu-id="fe889-152">上面的命令将生成以下输出:</span><span class="sxs-lookup"><span data-stu-id="fe889-152">The command above generates the following output:</span></span>

    ```output
    origin  https://[your-username]@BESTBIKE.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://[your-username]@BESTBIKE.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a><span data-ttu-id="fe889-153">将你的代码推送到 Azure</span><span class="sxs-lookup"><span data-stu-id="fe889-153">Push your code to Azure</span></span>

<span data-ttu-id="fe889-154">现在, 您已将本地 git 存储库挂接到 azure 上的远程 Git 存储库, 您将开发并生成应用程序, 然后将应用程序代码推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="fe889-154">Now that you have your local Git repository hooked to the remote Git repository on Azure, you will develop and build the app, and then push your application code to Azure.</span></span>

1. <span data-ttu-id="fe889-155">键入以下 Git 命令以将**主**分支推送到 Azure 上的远程 Git 存储库:</span><span class="sxs-lookup"><span data-stu-id="fe889-155">Type the following Git command to push your **master** branch to the remote Git repository on Azure:</span></span>

    ```bash
    git push origin master
    ```

1. <span data-ttu-id="fe889-156">系统将提示您输入您在上面的 "**部署凭据**" 部分中记录的密码。</span><span class="sxs-lookup"><span data-stu-id="fe889-156">You will be prompted to enter the password that you noted from the **Deployment Credentials** section above.</span></span> <span data-ttu-id="fe889-157">输入您的密码, 然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="fe889-157">Enter your password and hit Enter.</span></span> <span data-ttu-id="fe889-158">Git 开始将已提交的文件上载到 Azure 远程 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="fe889-158">Git starts uploading your committed files to the Azure remote Git repository.</span></span>

## <a name="verify-the-code-is-uploaded-to-azure"></a><span data-ttu-id="fe889-159">验证代码是否已上传到 Azure</span><span class="sxs-lookup"><span data-stu-id="fe889-159">Verify the code is uploaded to Azure</span></span>

1. <span data-ttu-id="fe889-160">切换回 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="fe889-160">Switch back to the Azure portal.</span></span>

1. <span data-ttu-id="fe889-161">单击左侧导航栏上的 "**所有资源**" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="fe889-161">Click on the **All Resources** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="fe889-162">azure 门户会导航到到目前为止在 Azure 上创建的所有资源的列表。</span><span class="sxs-lookup"><span data-stu-id="fe889-162">The Azure portal navigates you to the list of all resources created on Azure so far.</span></span>

1. <span data-ttu-id="fe889-163">单击您的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe889-163">Click on your web app.</span></span>

1. <span data-ttu-id="fe889-164">到达概述页面后, 转到 "**部署中心**"。</span><span class="sxs-lookup"><span data-stu-id="fe889-164">Once you arrive to the overview page, go to **Deployment Center**.</span></span>

    <span data-ttu-id="fe889-165">你将看到, 你的计算机上本地的第一个提交现在已上载到 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="fe889-165">You will see that your first commit that you have locally on your machine is now uploaded to the Azure portal.</span></span>

    <span data-ttu-id="fe889-166">当您将代码推送到 App Service 中的远程 Git 存储库时, Azure 将记录此操作。</span><span class="sxs-lookup"><span data-stu-id="fe889-166">When you push your code to the remote Git repository in App Service, Azure records this operation.</span></span>

    <span data-ttu-id="fe889-167">每次将您的代码推送到 Azure 时, 都会看到一条新记录以及提交消息 (您提供的用于`-m`参数的字符串), 在提交更改时键入。</span><span class="sxs-lookup"><span data-stu-id="fe889-167">Every time you push your code to Azure, you will see a new record, together with the commit message (the string that you supply with the `-m` argument) that you type when committing your changes.</span></span>

    <span data-ttu-id="fe889-168">**![显示 "开发选项" 页中最近的 Git 存储库部署的 Azure 门户屏幕截图。](../media/7-staging-deployment-slot-after-uploading-files.png)**</span><span class="sxs-lookup"><span data-stu-id="fe889-168">**![Screenshot of the Azure portal showing a recent Git repo deployment in the Development options page.](../media/7-staging-deployment-slot-after-uploading-files.png)**</span></span>

1. <span data-ttu-id="fe889-169">让我们访问应用程序 URL。</span><span class="sxs-lookup"><span data-stu-id="fe889-169">Let's visit the application URL.</span></span> <span data-ttu-id="fe889-170">此 url 已在上面提到, 但是, 如果您忘记了该 url, 则可以始终转到 "暂存部署" 槽的 "**概述**" 页, 然后选取该 url。</span><span class="sxs-lookup"><span data-stu-id="fe889-170">The URL was mentioned above, however, if you forget that URL, you can always go to the **Overview** page of the staging deployment slot and pick up the URL.</span></span>

1. <span data-ttu-id="fe889-171">在浏览器地址栏中键入 URL。</span><span class="sxs-lookup"><span data-stu-id="fe889-171">Type the URL in your browser address bar.</span></span>

    ![显示暂存部署槽网站的 web 浏览器视图的屏幕截图。](../media/7-staging-slot-hosted-online.png)

<span data-ttu-id="fe889-173">!!</span><span class="sxs-lookup"><span data-stu-id="fe889-173">Congratulations!</span></span> <span data-ttu-id="fe889-174">你已成功在应用服务上托管应用程序!</span><span class="sxs-lookup"><span data-stu-id="fe889-174">You have successfully hosted your application on App Service!</span></span>

::: zone-end

::: zone pivot="node"

<span data-ttu-id="fe889-175">可通过两种主要方式将 **.zip**文件上传到应用服务 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe889-175">There are two primary ways to upload a **.zip** file to an App Service web app.</span></span>

<span data-ttu-id="fe889-176">首先, 可以使用专用内置网页将一个压缩的网站部署到应用服务。</span><span class="sxs-lookup"><span data-stu-id="fe889-176">First, you can deploy a zipped website up to App Service using a dedicated built-in web page.</span></span> <span data-ttu-id="fe889-177">如果导航到`https://<app_name>.scm.azurewebsites.net/ZipDeployUI` "", 则表明您可以拖放本地 **.zip**文件并将其上传到您的服务器。</span><span class="sxs-lookup"><span data-stu-id="fe889-177">If you navigate to `https://<app_name>.scm.azurewebsites.net/ZipDeployUI` you are shown a site you can drag/drop the local **.zip** file and upload it to your server.</span></span> <span data-ttu-id="fe889-178">在这种情况下, 需要使用用于创建网站的相同 Azure 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="fe889-178">You need to sign in with the same Azure credentials used to create the site in this case.</span></span> <span data-ttu-id="fe889-179">此方法类似于使用 FTP 上传到映射到网站主机的存储文件夹。</span><span class="sxs-lookup"><span data-stu-id="fe889-179">This approach is similar to using FTP to upload to the storage folder mapped to the website host.</span></span>

<span data-ttu-id="fe889-180">我们将在此处使用的第二种方法是命令行。</span><span class="sxs-lookup"><span data-stu-id="fe889-180">The second approach which we'll use here is the command line.</span></span> <span data-ttu-id="fe889-181">Azure CLI 包含用于上`webapp deployment`传包含网站所有文件的 ZIP 文件的命令。</span><span class="sxs-lookup"><span data-stu-id="fe889-181">The Azure CLI includes the `webapp deployment` command to upload a ZIP file that contains all the files for the website.</span></span> <span data-ttu-id="fe889-182">使用以下命令将您的 zip 文件上传到已创建的网站。</span><span class="sxs-lookup"><span data-stu-id="fe889-182">Use the following command to upload your zip file to your created website.</span></span> <span data-ttu-id="fe889-183">请务必替换`<app_name>`和 .zip 文件名:</span><span class="sxs-lookup"><span data-stu-id="fe889-183">Make sure to replace the `<app_name>` and .zip filename:</span></span>

```azurecli
az webapp deployment source config-zip --resource-group <rgn>[sandbox resource group name]</rgn> --src helloworld.zip --name <app_name> 
```

<span data-ttu-id="fe889-184">这将使用包含传输详细信息的 JSON 块进行响应。</span><span class="sxs-lookup"><span data-stu-id="fe889-184">This will respond with a JSON block with the details about the transfer.</span></span>

```json
{
  "active": true,
  "author": "N/A",
  "author_email": "N/A",
  "complete": true,
  "deployer": "Push-Deployer",
  "end_time": "2018-12-19T18:04:13.441193Z",
  "id": "ddd8d88c04194a00a0eb7cb96766c054",
  "is_readonly": true,
  "is_temp": false,
  "last_success_end_time": "2018-12-19T18:04:13.441193Z",
  "log_url": "https://<app_name>.scm.azurewebsites.net/api/deployments/latest/log",
  "message": "Created via a push deployment",
  "progress": "",
  "received_time": "2018-12-19T18:04:09.585955Z",
  "site_name": "<app_name>",
  "start_time": "2018-12-19T18:04:09.843809Z",
  "status": 4,
  "status_text": "",
  "url": "https://<app_name>.scm.azurewebsites.net/api/deployments/latest"
}
```

<span data-ttu-id="fe889-185">命令运行完毕后, 打开一个新的浏览器选项卡, `https://<app_name>.azurewebsites.net`然后导航到。</span><span class="sxs-lookup"><span data-stu-id="fe889-185">When the command finishes running, open a new browser tab and navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="fe889-186">你将看到 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="fe889-186">You'll see the "Hello World!"</span></span> <span data-ttu-id="fe889-187">已成功部署来自&mdash;你的应用的邮件!</span><span class="sxs-lookup"><span data-stu-id="fe889-187">message from your app &mdash; you've deployed successfully!</span></span>

::: zone-end

::: zone pivot="java"

## <a name="configure-deployment-credentials"></a><span data-ttu-id="fe889-188">配置部署凭据</span><span class="sxs-lookup"><span data-stu-id="fe889-188">Configure deployment credentials</span></span>

<span data-ttu-id="fe889-189">大多数应用服务部署技术 (包括我们将在此处使用的) 都需要用户名和密码, 与 Azure 登录分开。</span><span class="sxs-lookup"><span data-stu-id="fe889-189">Most App Service deployment techniques, including the one we'll use here, require a username and password that are separate from your Azure login.</span></span> <span data-ttu-id="fe889-190">每个 web 应用均预配置了其自己的用户名和密码, 可以将其重置为新的随机值, 但不能更改为您选择的内容。</span><span class="sxs-lookup"><span data-stu-id="fe889-190">Every web app comes preconfigured with its own username and a password that can be reset to a new random value, but can't be changed to something you choose.</span></span>

<span data-ttu-id="fe889-191">您可以使用名为 "用户部署凭据" 的应用服务功能来创建您自己的用户名和密码, 而不是为每个应用程序找到这些凭据并将其存储在某个位置。</span><span class="sxs-lookup"><span data-stu-id="fe889-191">Instead of finding those credentials for each one of your apps and storing them somewhere, you can use an App Service feature called User Deployment Credentials to create your own username and password.</span></span> <span data-ttu-id="fe889-192">您选择的值将适用于您对其具有权限的*所有*应用服务 web 应用程序的部署, 其中包括您将来创建的新 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe889-192">The values you choose will work for deployments on *all* App Service web apps that you have permissions to, including new web apps that you create in the future.</span></span> <span data-ttu-id="fe889-193">你选择的用户名和密码与你的 Azure 登录相关且仅供你使用, 因此不与其他人共享。</span><span class="sxs-lookup"><span data-stu-id="fe889-193">The username and password you select are tied to your Azure login and intended only for your use, so don't share them with others.</span></span> <span data-ttu-id="fe889-194">您可以随时更改用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="fe889-194">You can change both the username and password at any time.</span></span>

<span data-ttu-id="fe889-195">创建部署凭据的最简单方法是从 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="fe889-195">The easiest way to create deployment credentials is from the Azure CLI.</span></span> <span data-ttu-id="fe889-196">在云命令行管理程序中运行以下命令, 以对其`<username>`进行`<password>`设置, 并将其替换为您选择的值。</span><span class="sxs-lookup"><span data-stu-id="fe889-196">Run the following command in the Cloud Shell to set them up, substituting `<username>` and `<password>` with values you choose.</span></span>

```azurecli
az webapp deployment user set --user-name <username> --password <password>
```

## <a name="deploy-the-application-package-with-wardeploy"></a><span data-ttu-id="fe889-197">使用 wardeploy 部署应用程序包</span><span class="sxs-lookup"><span data-stu-id="fe889-197">Deploy the application package with wardeploy</span></span>

<span data-ttu-id="fe889-198">**Wardeploy**是专门用于将 WAR web 应用程序包文件部署到 Java web 应用程序的应用程序服务部署机制。</span><span class="sxs-lookup"><span data-stu-id="fe889-198">**Wardeploy** is an App Service deployment mechanism specifically designed for deploying WAR web application package files to Java web apps.</span></span> <span data-ttu-id="fe889-199">Wardeploy 是 Kudu REST API 的一部分: 可通过 HTTP 访问的所有应用服务 web 应用上提供的管理服务接口。</span><span class="sxs-lookup"><span data-stu-id="fe889-199">Wardeploy is part of the Kudu REST API: an administrative service interface, available on all App Service web apps, that can be accessed over HTTP.</span></span> <span data-ttu-id="fe889-200">使用 wardeploy 的最简单方法是从命令`curl`行使用 HTTP 实用程序。</span><span class="sxs-lookup"><span data-stu-id="fe889-200">The simplest way to use wardeploy is with the `curl` HTTP utility from the command line.</span></span>

<span data-ttu-id="fe889-201">运行以下命令以使用 wardeploy 部署您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe889-201">Run the following commands to deploy your app with wardeploy.</span></span> <span data-ttu-id="fe889-202">将`<username>`和`<password>`替换为你在上面创建的部署用户用户名和密码, `<web_app_name>`并将替换为你的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="fe889-202">Replace `<username>` and `<password>` with the Deployment User username and password you created above, and replace `<web_app_name>` with the name of your web app.</span></span>

```console
cd ~/helloworld/target
curl -v -X POST -u <username>:<password> https://<sitename>.scm.azurewebsites.net/api/wardeploy --data-binary @helloworld.war
```

<span data-ttu-id="fe889-203">命令运行完毕后, 打开一个新的浏览器选项卡, `https://<web_app_name>.azurewebsites.net`然后导航到。</span><span class="sxs-lookup"><span data-stu-id="fe889-203">When the command finishes running, open a new browser tab and navigate to `https://<web_app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="fe889-204">你将看到 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="fe889-204">You'll see the "Hello World!"</span></span> <span data-ttu-id="fe889-205">已成功部署来自&mdash;你的应用的邮件!</span><span class="sxs-lookup"><span data-stu-id="fe889-205">message from your app &mdash; you've deployed successfully!</span></span>

::: zone-end