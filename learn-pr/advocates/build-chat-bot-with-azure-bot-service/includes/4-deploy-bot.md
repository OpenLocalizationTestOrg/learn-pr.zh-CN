[!INCLUDE [0-vm-note](0-vm-note.md)]

创建 azure web 应用程序部件时, 将部署 azure web 应用程序来托管它。 但是, bot 确实需要一些代码, 但仍需要将其部署到 Azure web 应用。 幸运的是, 由 Azure Bot 服务为你生成的代码。 在此单元中, 您将使用 Visual Studio Code 将代码放在本地 Git 存储库中, 并通过将本地存储库中的更改推送到 azure web 应用程序连接到承载机器人的远程存储库, 将这些程序发布到 azure: 这一过程称为[连续tegration](https://wikipedia.org/wiki/Continuous_integration)。

1. 在硬盘上的所选位置创建一个名为 "Factbot" 的文件夹, 以保存 bot 的源代码。

1. 返回到 VM 浏览器中的 Azure 门户, 并打开预先创建的练习资源组。 然后, 选择您在上一练习中创建的 Web 应用程序 Bot。

1. 选择左侧菜单中的 "**生成**", 然后选择 "**下载 bot 源代码**" 来准备包含 Bot 源代码的 zip 文件。 准备好 zip 文件后, 选择 "**下载机器人源代码**" 按钮进行下载。 下载完成后, 将 zip 文件的内容解压缩到之前创建的 "Factbot" 文件夹中。

1. 返回到 Azure 门户中的 Web 应用程序 Bot 生成边栏, 选择 "**配置连续部署**"。

1. 选择 "**部署**" 边栏顶部的 "**安装程序**", 然后选择 "**源**"。

1. 然后, 选择 "**本地 Git 存储库**" 作为部署源。

1. 接下来, 选择 "**设置连接**", 然后输入用户名和密码。 您可能需要输入除 "FactbotAdministrator" 之外的其他用户名, 因为该名称在 Azure 中必须是唯一的。 然后, 选择 **"确定"** 以返回到**部署选项**"边栏", 然后再次返回到 "**部署**" 边栏 **"确定**"。

    ![显示新的 bot 应用服务刀片的 Azure 门户屏幕截图, 其中突出显示了 "部署凭据" 菜单项和 "保存" 按钮。](../media/4-portal-enter-ci-creds.png)

1. 在部署系统进行设置时, 请关闭**部署**边栏, 并选择左侧菜单中的 "**所有应用服务设置**"。

1. 启动**Visual Studio Code**, 并使用**文件** > **打开文件夹 ...** 命令打开复制 bot 源代码的 "Factbot" 文件夹。

1. 在 Visual Studio Code 左侧的 "活动" 栏中选择 "**源代码控制**" 按钮。

1. 选择顶部的 "**初始化存储库**" 图标。

1. 在对话框中选择 "**初始化库**" 按钮。

1. 键入 "First commit"。 在消息框中。

1. 选中该复选标记以提交更改, 并在收到提示时暂存所有文件。

    > [!NOTE]
    > 如果您在 git 中遇到有关未设置标识的 Git 错误, 则启动命令提示符并运行以下命令, 并根据需要替换占位符电子邮件和名称值。 然后重试 "提交" 按钮。
    >
    > ```bash
    > git config --global user.email "Lab User"
    > git config --global user.name "LabUser#######@learn"
    > ```

1. 从 Visual Studio Code 的 "**视图**" 菜单中选择 "**终端**", 打开一个集成终端。

1. 在集成终端中执行以下命令, 将以下两个位置中的 BOT_NAME 替换为您在练习1中输入的 BOT 名称。

    > [!NOTE]
    > 此外, 还可以在**Git 克隆 URL**下的应用程序服务资源**概述**部分找到完整的 Git 远程 URL。

    ```bash
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. 返回到 "**源**" "控制面板", 选择 "源" 控制面板顶部的省略号 (三个点), 然后从菜单中选择 "**发布分支**", 将 bot 代码从本地存储库推送到 Azure。 如果系统提示输入凭据, 请输入您之前在本练习中指定的用户名和密码。

你的 bot 已发布到 Azure。 但在这里进行测试之前, 让我们在本地运行它, 并了解如何在 Visual Studio Code 中对其进行调试。
