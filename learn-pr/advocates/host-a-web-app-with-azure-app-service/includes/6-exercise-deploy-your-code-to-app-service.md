在此单元中, 你将 web 应用程序部署到应用服务。

::: zone pivot="csharp"

## <a name="use-a-local-git-repository-as-your-deployment-option"></a>将本地 Git 存储库用作部署选项

接下来, 我们将为 Git 部署配置应用服务。 这将使我们可以通过将我们的代码推送到 Azure 中的 Git 终结点来部署应用程序的新版本。

1. 在应用服务 web 应用程序的 "概述" 页中, 单击左侧导航栏上的 "**部署中心**" 菜单项。

1. 单击 "**本地 Git**"。

1. 单击 "**继续**"。

1. 单击 "**应用程序服务 Kudu" "生成服务器**"。

1. 单击 "**继续**"。

1. 查看您的设置, 然后单击 "**完成**"。

## <a name="create-deployment-credentials"></a>创建部署凭据

在可以使用 git 进行部署之前, 应用程序服务要求您设置可用于从 Git 客户端进行身份验证的用户名/密码。

1. 单击 "**部署凭据**" 按钮。

1. 单击 "**用户凭据**"。

1. 如果还未填充, 请设置**Username**字段。 这不一定与 Azure 帐户用户名相同。

1. 输入您选择的**密码**, 然后确认您的密码。

    > [!NOTE]
    > 请确保您不会忘记您的用户名和密码! 稍后当我们开始上载代码并将其部署到 Azure 时, 你将需要它们。

1. 单击 "**保存凭据**"。

1. 记下**Git 克隆 Uri**, 它是将用作本地应用程序代码存储库的**远程**的 Azure Git 存储库 URL。

## <a name="set-up-git-on-cloud-shell"></a>在云命令行管理程序上设置 Git

Git 已安装 Azure 云命令行管理程序, 但你需要为你的云命令行管理程序帐户设置用户名和电子邮件。

1. 在右侧的云命令行管理程序中, 键入以下命令, 将`[your name]`和`[your email]`占位符替换为您自己的姓名和电子邮件 (不带大括号):

    ```bash
    git config --global user.name "[your name]"
    git config --global user.email "[your email]"
    ```

1. 若要验证您的信息是否已由 Git 记录, 请键入以下命令:

    ```bash
    cat ~/.gitconfig
    ```

   您应看到以下内容, 并显示您的姓名和电子邮件:

    ```output
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-code"></a>为您的代码初始化本地 Git 存储库

若要开始使用 Git, 您需要为您的 .net Core 应用程序代码初始化本地 Git 存储库。

1. 请确保您在之前创建的项目文件夹中。

    ```bash
    cd ~/BestBikeApp/
    ```

1. 通过发出以下命令初始化新的 Git 存储库:

    ```bash
    git init
    ```

    如果该命令成功执行, 您将收到如下所示的消息:

    ```output
    Initialized empty Git repository in /home/{your-user}/BestBikeApp/.git/
    ```

1. 将所有应用程序文件暂存到 Git。

   下一步是让 Git 了解你的应用程序文件。 为此, 请添加工作目录的所有文件, 以便通过 Git**暂存**这些文件。 键入以下命令:

    ```bash
    git add .
    ```

    上面的命令将 "." 代表的所有文件添加到 Git 的暂存状态。

1. 现在, 你需要将所做的更改提交到 Git。

   使用 Git 暂存文件后, 需要将文件提交到本地计算机上的**Git 提交历史记录**。 为此, 请键入以下命令:

    ```bash
   git commit -m "Initial commit"
    ```

   该`commit`命令接受`-m`参数以在正在创建的提交中包含一封邮件。 稍后, 当你将代码推送到 Azure 时, 你将能够看到与此特定提交一起存储的相同消息。

## <a name="add-a-remote-for-the-local-git-repository"></a>为本地 Git 存储库添加远程

此时, 您已成功初始化了新的本地 Git 存储库。 此外, 您已将所有应用程序文件提交到 Git。 剩下的工作是添加一个**远程**, 将本地 Git 存储库连接到在 Azure 上托管的存储库。

为此, 需要执行以下操作:

1. 复制上面看到的**Git 克隆 url** 。

1. 复制后, 返回到**终端**窗口并使用您的 url 发出以下 Git 命令:

    ```bash
    git remote add origin https://[your-username]@BESTBIKE.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    上面的 git 命令将本地 git 存储库连接到 Azure 上托管的存储库`[your-username]` , 其中是您在创建部署凭据时指定的用户名。 现在, 您可以通过推送代码来部署代码。

1. 若要验证上面的命令, 请键入以下 Git 命令:

    ```bash
    git remote -v
    ```

    上面的命令将生成以下输出:

    ```output
    origin  https://[your-username]@BESTBIKE.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://[your-username]@BESTBIKE.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a>将你的代码推送到 Azure

现在, 您已将本地 git 存储库挂接到 azure 上的远程 Git 存储库, 您将开发并生成应用程序, 然后将应用程序代码推送到 Azure。

1. 键入以下 Git 命令以将**主**分支推送到 Azure 上的远程 Git 存储库:

    ```bash
    git push origin master
    ```

1. 系统将提示您输入您在上面的 "**部署凭据**" 部分中记录的密码。 输入您的密码, 然后按 Enter。 Git 开始将已提交的文件上载到 Azure 远程 Git 存储库。

## <a name="verify-the-code-is-uploaded-to-azure"></a>验证代码是否已上传到 Azure

1. 切换回 Azure 门户。

1. 单击左侧导航栏上的 "**所有资源**" 菜单项。

1. azure 门户会导航到到目前为止在 Azure 上创建的所有资源的列表。

1. 单击您的 web 应用程序。

1. 到达概述页面后, 转到 "**部署中心**"。

    你将看到, 你的计算机上本地的第一个提交现在已上载到 Azure 门户。

    当您将代码推送到 App Service 中的远程 Git 存储库时, Azure 将记录此操作。

    每次将您的代码推送到 Azure 时, 都会看到一条新记录以及提交消息 (您提供的用于`-m`参数的字符串), 在提交更改时键入。

    **![显示 "开发选项" 页中最近的 Git 存储库部署的 Azure 门户屏幕截图。](../media/7-staging-deployment-slot-after-uploading-files.png)**

1. 让我们访问应用程序 URL。 此 url 已在上面提到, 但是, 如果您忘记了该 url, 则可以始终转到 "暂存部署" 槽的 "**概述**" 页, 然后选取该 url。

1. 在浏览器地址栏中键入 URL。

    ![显示暂存部署槽网站的 web 浏览器视图的屏幕截图。](../media/7-staging-slot-hosted-online.png)

!! 你已成功在应用服务上托管应用程序!

::: zone-end

::: zone pivot="node"

可通过两种主要方式将 **.zip**文件上传到应用服务 web 应用程序。

首先, 可以使用专用内置网页将一个压缩的网站部署到应用服务。 如果导航到`https://<app_name>.scm.azurewebsites.net/ZipDeployUI` "", 则表明您可以拖放本地 **.zip**文件并将其上传到您的服务器。 在这种情况下, 需要使用用于创建网站的相同 Azure 凭据登录。 此方法类似于使用 FTP 上传到映射到网站主机的存储文件夹。

我们将在此处使用的第二种方法是命令行。 Azure CLI 包含用于上`webapp deployment`传包含网站所有文件的 ZIP 文件的命令。 使用以下命令将您的 zip 文件上传到已创建的网站。 请务必替换`<app_name>`和 .zip 文件名:

```azurecli
az webapp deployment source config-zip --resource-group <rgn>[sandbox resource group name]</rgn> --src helloworld.zip --name <app_name> 
```

这将使用包含传输详细信息的 JSON 块进行响应。

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

命令运行完毕后, 打开一个新的浏览器选项卡, `https://<app_name>.azurewebsites.net`然后导航到。 你将看到 "Hello World!" 已成功部署来自&mdash;你的应用的邮件!

::: zone-end

::: zone pivot="java"

## <a name="configure-deployment-credentials"></a>配置部署凭据

大多数应用服务部署技术 (包括我们将在此处使用的) 都需要用户名和密码, 与 Azure 登录分开。 每个 web 应用均预配置了其自己的用户名和密码, 可以将其重置为新的随机值, 但不能更改为您选择的内容。

您可以使用名为 "用户部署凭据" 的应用服务功能来创建您自己的用户名和密码, 而不是为每个应用程序找到这些凭据并将其存储在某个位置。 您选择的值将适用于您对其具有权限的*所有*应用服务 web 应用程序的部署, 其中包括您将来创建的新 web 应用程序。 你选择的用户名和密码与你的 Azure 登录相关且仅供你使用, 因此不与其他人共享。 您可以随时更改用户名和密码。

创建部署凭据的最简单方法是从 Azure CLI。 在云命令行管理程序中运行以下命令, 以对其`<username>`进行`<password>`设置, 并将其替换为您选择的值。

```azurecli
az webapp deployment user set --user-name <username> --password <password>
```

## <a name="deploy-the-application-package-with-wardeploy"></a>使用 wardeploy 部署应用程序包

**Wardeploy**是专门用于将 WAR web 应用程序包文件部署到 Java web 应用程序的应用程序服务部署机制。 Wardeploy 是 Kudu REST API 的一部分: 可通过 HTTP 访问的所有应用服务 web 应用上提供的管理服务接口。 使用 wardeploy 的最简单方法是从命令`curl`行使用 HTTP 实用程序。

运行以下命令以使用 wardeploy 部署您的应用程序。 将`<username>`和`<password>`替换为你在上面创建的部署用户用户名和密码, `<web_app_name>`并将替换为你的 web 应用的名称。

```console
cd ~/helloworld/target
curl -v -X POST -u <username>:<password> https://<sitename>.scm.azurewebsites.net/api/wardeploy --data-binary @helloworld.war
```

命令运行完毕后, 打开一个新的浏览器选项卡, `https://<web_app_name>.azurewebsites.net`然后导航到。 你将看到 "Hello World!" 已成功部署来自&mdash;你的应用的邮件!

::: zone-end