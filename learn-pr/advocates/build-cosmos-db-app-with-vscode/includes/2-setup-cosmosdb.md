Visual Studio Code 的 Azure Cosmos DB 扩展通过使您能够使用命令窗口创建资源, 从而简化了帐户、数据库和集合的创建。

在此单元中, 将安装 Visual Studio 的 Azure Cosmos DB 扩展, 然后使用它创建帐户、数据库和集合。

## <a name="install-the-azure-cosmos-db-extension-for-visual-studio"></a>安装 Visual Studio 的 Azure Cosmos DB 扩展

1. 转到[visual studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb&azure-portal=true)并安装适用于 visual studio Code 的**Azure Cosmos DB**扩展。

1. 在 Visual Studio Code 中加载 "扩展" 选项卡时, 单击 "**安装**"。

1. 安装完成后, 单击 "**重新加载**"。

    Visual Studio Code 显示 ![Azure 图标](../media/2-setup/visual-studio-code-explorer-icon.png) 安装并重新加载扩展后屏幕左侧的 Azure 图标。

## <a name="create-an-azure-cosmos-db-account-in-visual-studio-code"></a>在 Visual Studio Code 中创建 Azure Cosmos DB 帐户

[!include[](../../../includes/azure-sandbox-activate.md)]

1. 在 Visual Studio Code 中, 通过单击 "**查看** > **命令组件面板**" 并键入 " **azure: 登录**" 登录 azure。 您必须安装了[azure 帐户](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account&azure-portal=true)扩展才能使用 azure: 登录。

    > [!IMPORTANT]
    > 使用用于创建沙盒的相同帐户登录 Azure。 沙盒提供对 Concierge 订阅的访问权限。

    按照提示复制并粘贴 web 浏览器中提供的代码, 这将对 Visual Studio code session 进行身份验证。

1. 单击左侧![菜单上](../media/2-setup/visual-studio-code-explorer-icon.png)的 "azure 图标**azure** " 图标, 然后右键单击 " **Concierge 订阅**", 然后单击 "**创建帐户**"。

    > [!NOTE]
    > 如果你未看到列出的 Concierge 订阅, 请确保使用用于创建沙盒的相同帐户在 Visual Studio Code 中登录 Azure。 此外, 如果您已在 azure 帐户扩展中筛选出 azure 订阅, 请验证该`> Azure: Select Subscriptions`命令中是否已检查 Concierge 订阅。

1. 单击该__+__ 按钮以开始创建 Cosmos DB 帐户。 如果您有多个订阅, 系统将要求您选择订阅。

1. 在屏幕顶部的文本框中, 为您的 Azure Cosmos DB 帐户输入一个唯一的名称, 然后按 enter。 帐户名称只能包含小写字母、数字和 '-' 字符, 并且必须介于3和31个字符之间。

1. 接下来, 选择 " **SQL (DocumentDB)**", 然后选择 " **<rgn>[沙盒资源组名称]</rgn>**", 然后选择一个位置。

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    Visual Studio Code 中的 "输出" 选项卡显示帐户创建的进度。 完成此过程需要几分钟时间。

1. 创建帐户后, 在**azure: Cosmos DB**窗格中展开你的 azure 订阅, 扩展将显示新的 Azure Cosmos DB 帐户。 在下图中, 新帐户称为 "**学习模块**"。

    ![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/azure-cosmos-db-vs-code-extension.png)

## <a name="create-an-azure-cosmos-db-database-and-collection-in-visual-studio-code"></a>在 Visual Studio Code 中创建 Azure Cosmos DB 数据库和集合

现在, 让我们为客户创建一个新的数据库和集合。

1. 在 "Azure: Cosmos DB" 窗格中, 右键单击您的新帐户, 然后单击 "**创建数据库**"。
1. 在屏幕顶部的 "输入调色板" 中, 键入`Users`数据库名称, 然后按 enter。
1. 输入`WebCustomers`集合名称, 然后按 enter。
1. 为`userId`分区键输入, 然后按 enter。
1. 最后, 确认`1000`初始吞吐量容量, 然后按 enter 键。
1. 展开 " **Azure: Cosmos DB** " 窗格中的帐户, 将显示新的 "**用户**数据库" 和 " **WebCustomers** " 集合。

    ![显示以上说明的动画在 Visual Studio Code 中通过 Azure Cosmos DB 扩展运行。](../media/2-setup/vs-code-azure-cosmos-db-extension.gif)

现在, 你已拥有 Azure Cosmos DB 帐户, 我们可以在 Visual Studio Code 中使用它!
