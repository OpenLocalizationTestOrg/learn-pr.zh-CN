<span data-ttu-id="4acb0-101">假设您正在管理一个在线零售商的存储。</span><span class="sxs-lookup"><span data-stu-id="4acb0-101">Imagine you're managing storage for an online retailer.</span></span> <span data-ttu-id="4acb0-102">您需要用于创建、更新和删除用户和产品数据的工具。</span><span class="sxs-lookup"><span data-stu-id="4acb0-102">You need tools to create, update, and delete your user and product data.</span></span>

<span data-ttu-id="4acb0-103">在本模块中, 将构建 Visual Studio Code 中的 .net Core 控制台应用程序, 以创建、更新和删除用户记录, 查询数据, 并使用 c # 执行存储过程。</span><span class="sxs-lookup"><span data-stu-id="4acb0-103">In this module, you will build a .NET Core console application in Visual Studio Code to create, update, and delete user records, query your data, and perform stored procedures using C#.</span></span>

<span data-ttu-id="4acb0-104">您的数据将存储在 Azure Cosmos DB 中, 该数据库具有一种方便的 Visual Studio 代码扩展, 因此您可以轻松地创建 Azure Cosmos DB 帐户、数据库和集合, 并将连接字符串复制到应用程序中, 而无需打开 Azure 门户。</span><span class="sxs-lookup"><span data-stu-id="4acb0-104">Your data will be stored in Azure Cosmos DB, which has a convenient Visual Studio Code extension so you can easily create an Azure Cosmos DB account, database, and collection, and copy your connection string into the app without having to open the Azure portal.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="4acb0-105">学习目标</span><span class="sxs-lookup"><span data-stu-id="4acb0-105">Learning objectives</span></span>

<span data-ttu-id="4acb0-106">在本模块中, 您将:</span><span class="sxs-lookup"><span data-stu-id="4acb0-106">In this module, you will:</span></span>  

- <span data-ttu-id="4acb0-107">使用 azure Cosmos db 扩展在 Visual Studio Code 中创建 azure Cosmos DB 帐户、数据库和集合</span><span class="sxs-lookup"><span data-stu-id="4acb0-107">Create an Azure Cosmos DB account, database, and collection in Visual Studio Code using the Azure Cosmos DB extension</span></span>
- <span data-ttu-id="4acb0-108">创建用于存储和查询 Azure Cosmos DB 中的数据的应用程序</span><span class="sxs-lookup"><span data-stu-id="4acb0-108">Create an application to store and query data in Azure Cosmos DB</span></span>
- <span data-ttu-id="4acb0-109">使用 Visual Studio Code 中的终端快速创建控制台应用程序</span><span class="sxs-lookup"><span data-stu-id="4acb0-109">Use the Terminal in Visual Studio Code to quickly create a console application</span></span>
- <span data-ttu-id="4acb0-110">使用适用于 Visual Studio Code 的 azure Cosmos db 扩展的帮助添加 azure Cosmos db 功能</span><span class="sxs-lookup"><span data-stu-id="4acb0-110">Add Azure Cosmos DB functionality with the help of the Azure Cosmos DB extension for Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4acb0-111">先决条件</span><span class="sxs-lookup"><span data-stu-id="4acb0-111">Prerequisites</span></span>

- <span data-ttu-id="4acb0-112">必须安装[Visual Studio 代码](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="4acb0-112">Must have [Visual Studio Code](https://code.visualstudio.com/) installed</span></span>
- <span data-ttu-id="4acb0-113">必须安装[.net Core 2.1](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="4acb0-113">Must have [.NET Core 2.1](https://www.microsoft.com/net/download) installed</span></span>
- <span data-ttu-id="4acb0-114">必须在 Visual Studio Code 中安装[Azure 帐户](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account)扩展</span><span class="sxs-lookup"><span data-stu-id="4acb0-114">Must have the [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) extension installed in Visual Studio Code</span></span>
