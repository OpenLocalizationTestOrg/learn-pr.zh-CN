[!INCLUDE [0-vm-note](0-vm-note.md)]

<span data-ttu-id="7df7c-101">创建 azure web 应用程序部件时, 将部署 azure web 应用程序来托管它。</span><span class="sxs-lookup"><span data-stu-id="7df7c-101">When you created an Azure web app bot, an Azure web app was deployed to host it.</span></span> <span data-ttu-id="7df7c-102">但是, bot 确实需要一些代码, 但仍需要将其部署到 Azure web 应用。</span><span class="sxs-lookup"><span data-stu-id="7df7c-102">But the bot does require some code, and it still needs to be deployed to the Azure web app.</span></span> <span data-ttu-id="7df7c-103">幸运的是, 由 Azure Bot 服务为你生成的代码。</span><span class="sxs-lookup"><span data-stu-id="7df7c-103">Fortunately, the code was generated for you by the Azure Bot Service.</span></span> <span data-ttu-id="7df7c-104">在此单元中, 您将使用 Visual Studio Code 将代码放在本地 Git 存储库中, 并通过将本地存储库中的更改推送到 azure web 应用程序连接到承载机器人的远程存储库, 将这些程序发布到 azure: 这一过程称为[连续tegration](https://wikipedia.org/wiki/Continuous_integration)。</span><span class="sxs-lookup"><span data-stu-id="7df7c-104">In this unit, you will use Visual Studio Code to place the code in a local Git repository and publish the bot to Azure by pushing changes from the local repository to a remote repository connected to the Azure web app that hosts the bot — a process known as [continuous integration](https://wikipedia.org/wiki/Continuous_integration).</span></span>

1. <span data-ttu-id="7df7c-105">在硬盘上的所选位置创建一个名为 "Factbot" 的文件夹, 以保存 bot 的源代码。</span><span class="sxs-lookup"><span data-stu-id="7df7c-105">Create a folder named "Factbot" in the location of your choice on your hard disk to hold the bot's source code.</span></span>

1. <span data-ttu-id="7df7c-106">返回到 VM 浏览器中的 Azure 门户, 并打开预先创建的练习资源组。</span><span class="sxs-lookup"><span data-stu-id="7df7c-106">Return to the Azure portal in the VM browser and open the pre-created exercise resource group.</span></span> <span data-ttu-id="7df7c-107">然后, 选择您在上一练习中创建的 Web 应用程序 Bot。</span><span class="sxs-lookup"><span data-stu-id="7df7c-107">Then, select the Web App Bot you created in the prior exercise.</span></span>

1. <span data-ttu-id="7df7c-108">选择左侧菜单中的 "**生成**", 然后选择 "**下载 bot 源代码**" 来准备包含 Bot 源代码的 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="7df7c-108">Select **Build** in the menu on the left, then select **Download Bot source code** to prepare a zip file containing the bot's source code.</span></span> <span data-ttu-id="7df7c-109">准备好 zip 文件后, 选择 "**下载机器人源代码**" 按钮进行下载。</span><span class="sxs-lookup"><span data-stu-id="7df7c-109">Once the zip file is prepared, select the **Download Bot source code** button to download it.</span></span> <span data-ttu-id="7df7c-110">下载完成后, 将 zip 文件的内容解压缩到之前创建的 "Factbot" 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="7df7c-110">When the download is complete, extract the contents of the zip file to the "Factbot" folder that you created earlier.</span></span>

1. <span data-ttu-id="7df7c-111">返回到 Azure 门户中的 Web 应用程序 Bot 生成边栏, 选择 "**配置连续部署**"。</span><span class="sxs-lookup"><span data-stu-id="7df7c-111">Back in the Web App Bot's Build blade in the Azure portal, select **Configure continuous deployment**.</span></span>

1. <span data-ttu-id="7df7c-112">选择 "**部署**" 边栏顶部的 "**安装程序**", 然后选择 "**源**"。</span><span class="sxs-lookup"><span data-stu-id="7df7c-112">Select **Setup** at the top of the **Deployments** blade, followed by **Choose Source**.</span></span>

1. <span data-ttu-id="7df7c-113">然后, 选择 "**本地 Git 存储库**" 作为部署源。</span><span class="sxs-lookup"><span data-stu-id="7df7c-113">Then, select **Local Git Repository** as the deployment source.</span></span>

1. <span data-ttu-id="7df7c-114">接下来, 选择 "**设置连接**", 然后输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="7df7c-114">Next, select **Setup connection** and enter a username and password.</span></span> <span data-ttu-id="7df7c-115">您可能需要输入除 "FactbotAdministrator" 之外的其他用户名, 因为该名称在 Azure 中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7df7c-115">You will probably have to enter a user name other than "FactbotAdministrator" because the name must be unique within Azure.</span></span> <span data-ttu-id="7df7c-116">然后, 选择 **"确定"** 以返回到**部署选项**"边栏", 然后再次返回到 "**部署**" 边栏 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="7df7c-116">Then, select **OK** to return to the **Deployment option** blade and **OK** again to return to the **Deployments** blade.</span></span>

    ![显示新的 bot 应用服务刀片的 Azure 门户屏幕截图, 其中突出显示了 "部署凭据" 菜单项和 "保存" 按钮。](../media/4-portal-enter-ci-creds.png)

1. <span data-ttu-id="7df7c-118">在部署系统进行设置时, 请关闭**部署**边栏, 并选择左侧菜单中的 "**所有应用服务设置**"。</span><span class="sxs-lookup"><span data-stu-id="7df7c-118">While the deployment system is provisioning, close the **Deployments** blade, and select **All App service settings** in the menu on the left.</span></span>

1. <span data-ttu-id="7df7c-119">启动**Visual Studio Code**, 并使用**文件** > **打开文件夹 ...** 命令打开复制 bot 源代码的 "Factbot" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="7df7c-119">Start **Visual Studio Code**, and use the **File** > **Open Folder...** command to open the "Factbot" folder where you copied the bot's source code.</span></span>

1. <span data-ttu-id="7df7c-120">在 Visual Studio Code 左侧的 "活动" 栏中选择 "**源代码控制**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="7df7c-120">Select the **Source Control** button in the activity bar on the left side of Visual Studio Code.</span></span>

1. <span data-ttu-id="7df7c-121">选择顶部的 "**初始化存储库**" 图标。</span><span class="sxs-lookup"><span data-stu-id="7df7c-121">Select the **Initialize Repository** icon at the top.</span></span>

1. <span data-ttu-id="7df7c-122">在对话框中选择 "**初始化库**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="7df7c-122">Select the **Initialize Repository** button in the dialog.</span></span>

1. <span data-ttu-id="7df7c-123">键入 "First commit"。</span><span class="sxs-lookup"><span data-stu-id="7df7c-123">Type "First commit."</span></span> <span data-ttu-id="7df7c-124">在消息框中。</span><span class="sxs-lookup"><span data-stu-id="7df7c-124">into the message box.</span></span>

1. <span data-ttu-id="7df7c-125">选中该复选标记以提交更改, 并在收到提示时暂存所有文件。</span><span class="sxs-lookup"><span data-stu-id="7df7c-125">Select the check mark to commit your changes, staging all the files when prompted.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7df7c-126">如果您在 git 中遇到有关未设置标识的 Git 错误, 则启动命令提示符并运行以下命令, 并根据需要替换占位符电子邮件和名称值。</span><span class="sxs-lookup"><span data-stu-id="7df7c-126">If you get a Git error about not having your identity set in Git, launch a Command Prompt and run the following commands, replacing the placeholder email and name values if you wish.</span></span> <span data-ttu-id="7df7c-127">然后重试 "提交" 按钮。</span><span class="sxs-lookup"><span data-stu-id="7df7c-127">Then retry the commit button.</span></span>
    >
    > ```bash
    > git config --global user.email "Lab User"
    > git config --global user.name "LabUser#######@learn"
    > ```

1. <span data-ttu-id="7df7c-128">从 Visual Studio Code 的 "**视图**" 菜单中选择 "**终端**", 打开一个集成终端。</span><span class="sxs-lookup"><span data-stu-id="7df7c-128">Select **Terminal** from Visual Studio Code's **View** menu to open an integrated terminal.</span></span>

1. <span data-ttu-id="7df7c-129">在集成终端中执行以下命令, 将以下两个位置中的 BOT_NAME 替换为您在练习1中输入的 BOT 名称。</span><span class="sxs-lookup"><span data-stu-id="7df7c-129">Execute the following command in the integrated terminal, replacing BOT_NAME in the following two places with the bot name you entered in Exercise 1.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7df7c-130">此外, 还可以在**Git 克隆 URL**下的应用程序服务资源**概述**部分找到完整的 Git 远程 URL。</span><span class="sxs-lookup"><span data-stu-id="7df7c-130">The full Git remote URL can also be found in the App Service resource's **Overview** section under **Git clone url**.</span></span>

    ```bash
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. <span data-ttu-id="7df7c-131">返回到 "**源**" "控制面板", 选择 "源" 控制面板顶部的省略号 (三个点), 然后从菜单中选择 "**发布分支**", 将 bot 代码从本地存储库推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="7df7c-131">Return to the **Source Control** panel and select the ellipsis (the three dots) at the top of the SOURCE CONTROL panel, and select **Publish Branch** from the menu to push the bot code from the local repository to Azure.</span></span> <span data-ttu-id="7df7c-132">如果系统提示输入凭据, 请输入您之前在本练习中指定的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="7df7c-132">If prompted for credentials, enter the username and password you specified previously in this exercise.</span></span>

<span data-ttu-id="7df7c-133">你的 bot 已发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="7df7c-133">Your bot has been published to Azure.</span></span> <span data-ttu-id="7df7c-134">但在这里进行测试之前, 让我们在本地运行它, 并了解如何在 Visual Studio Code 中对其进行调试。</span><span class="sxs-lookup"><span data-stu-id="7df7c-134">But before you test it there, let's run it locally and learn how to debug it in Visual Studio Code.</span></span>
