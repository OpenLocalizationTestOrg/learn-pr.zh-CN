<span data-ttu-id="d2d62-101">创建并配置事件中心之后, 您需要配置应用程序以发送和接收事件数据流。</span><span class="sxs-lookup"><span data-stu-id="d2d62-101">After you have created and configured your Event Hub, you'll need to configure applications to send and receive event data streams.</span></span>

<span data-ttu-id="d2d62-102">例如, 付款处理解决方案将使用某种形式的发件人应用程序收集客户的信用卡数据和收件人应用程序, 以验证信用卡是否有效。</span><span class="sxs-lookup"><span data-stu-id="d2d62-102">For example, a payment processing solution will use some form of sender application to collect customer's credit card data and a receiver application to verify that the credit card is valid.</span></span>

<span data-ttu-id="d2d62-103">虽然与 .net 应用程序相比, Java 应用程序的配置方式不同, 但有一些一般原则, 可用于使应用程序连接到事件中心并成功发送或接收邮件。</span><span class="sxs-lookup"><span data-stu-id="d2d62-103">Although there are differences in how a Java application is configured, compared to a .NET application, there are general principles for enabling applications to connect to an Event Hub, and to successfully send or receive messages.</span></span> <span data-ttu-id="d2d62-104">因此, 尽管编辑 Java 配置文本文件的过程与使用 Visual Studio 准备 .net 应用程序的过程不同, 但原则是相同的。</span><span class="sxs-lookup"><span data-stu-id="d2d62-104">So, although the process of editing Java configuration text files is different to preparing a .NET application using Visual Studio, the principles are the same.</span></span>

## <a name="what-are-the-minimum-event-hub-application-requirements"></a><span data-ttu-id="d2d62-105">事件中心应用程序的最低要求是什么？</span><span class="sxs-lookup"><span data-stu-id="d2d62-105">What are the minimum Event Hub application requirements?</span></span>

<span data-ttu-id="d2d62-106">若要将应用程序配置为向事件中心发送邮件, 必须提供以下信息, 以便应用程序可以创建连接凭据:</span><span class="sxs-lookup"><span data-stu-id="d2d62-106">To configure an application to send messages to an Event Hub, you must provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="d2d62-107">事件中心命名空间名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-107">Event Hub namespace name</span></span>
- <span data-ttu-id="d2d62-108">事件中心名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-108">Event Hub name</span></span>
- <span data-ttu-id="d2d62-109">共享访问策略名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-109">Shared access policy name</span></span>
- <span data-ttu-id="d2d62-110">主共享访问密钥</span><span class="sxs-lookup"><span data-stu-id="d2d62-110">Primary shared access key</span></span>

<span data-ttu-id="d2d62-111">若要将应用程序配置为从事件中心接收邮件, 请提供以下信息, 以便应用程序可以创建连接凭据:</span><span class="sxs-lookup"><span data-stu-id="d2d62-111">To configure an application to receive messages from an Event Hub, provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="d2d62-112">事件中心命名空间名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-112">Event Hub namespace name</span></span>
- <span data-ttu-id="d2d62-113">事件中心名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-113">Event Hub name</span></span>
- <span data-ttu-id="d2d62-114">共享访问策略名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-114">Shared access policy name</span></span>
- <span data-ttu-id="d2d62-115">主共享访问密钥</span><span class="sxs-lookup"><span data-stu-id="d2d62-115">Primary shared access key</span></span>
- <span data-ttu-id="d2d62-116">存储帐户名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-116">Storage account name</span></span>
- <span data-ttu-id="d2d62-117">存储帐户连接字符串</span><span class="sxs-lookup"><span data-stu-id="d2d62-117">Storage account connection string</span></span>
- <span data-ttu-id="d2d62-118">存储帐户容器名称</span><span class="sxs-lookup"><span data-stu-id="d2d62-118">Storage account container name</span></span>

<span data-ttu-id="d2d62-119">如果您有一个在 Azure Blob 存储中存储邮件的接收器应用程序, 您还需要先配置一个存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d2d62-119">If you have a receiver application that stores messages in Azure Blob Storage, you'll also need to first configure a storage account.</span></span>

## <a name="azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a><span data-ttu-id="d2d62-120">用于创建常规用途的标准存储帐户的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="d2d62-120">Azure CLI commands for creating a general-purpose standard storage account</span></span>

<span data-ttu-id="d2d62-121">Azure CLI 提供了可用于创建和管理存储帐户的一组命令。</span><span class="sxs-lookup"><span data-stu-id="d2d62-121">The Azure CLI provides a set of commands you can use to create and manage a storage account.</span></span> <span data-ttu-id="d2d62-122">我们将在下一个单元中使用它们, 但下面是这些命令的基本概要。</span><span class="sxs-lookup"><span data-stu-id="d2d62-122">We'll work with them in the next unit, but here's a basic synopsis of the commands.</span></span> 

> [!TIP]
> <span data-ttu-id="d2d62-123">在模块简介中, 从**Azure 存储**开始, 有几个 MS 学习模块包含存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d2d62-123">There are several MS Learn modules that cover storage accounts, starting in the module **Introduction to Azure Storage**.</span></span>

| <span data-ttu-id="d2d62-124">指挥</span><span class="sxs-lookup"><span data-stu-id="d2d62-124">Command</span></span> | <span data-ttu-id="d2d62-125">说明</span><span class="sxs-lookup"><span data-stu-id="d2d62-125">Description</span></span> |
|---------|-------------|
| `storage account create` | <span data-ttu-id="d2d62-126">创建常规用途的 V2 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d2d62-126">Create a general-purpose V2 Storage account.</span></span> |
| `storage account key list` | <span data-ttu-id="d2d62-127">检索存储帐户密钥。</span><span class="sxs-lookup"><span data-stu-id="d2d62-127">Retrieve the storage account key.</span></span> |
| `storage account show-connection-string` | <span data-ttu-id="d2d62-128">检索 Azure 存储帐户的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d2d62-128">Retrieve the connection string for an Azure Storage account.</span></span> |
| `storage container create` | <span data-ttu-id="d2d62-129">在存储帐户中创建新容器。</span><span class="sxs-lookup"><span data-stu-id="d2d62-129">Creates a new container in a storage account.</span></span> |

## <a name="shell-command-for-cloning-an-application-github-repository"></a><span data-ttu-id="d2d62-130">用于克隆 application GitHub 存储库的命令行管理程序命令</span><span class="sxs-lookup"><span data-stu-id="d2d62-130">Shell command for cloning an application GitHub repository</span></span>

<span data-ttu-id="d2d62-131">Git 是一种协作工具, 它使用分布式版本控制模型, 旨在协作处理软件和文档项目。</span><span class="sxs-lookup"><span data-stu-id="d2d62-131">Git is a collaboration tool that uses a distributed version control model, and is designed for collaborative working on software and documentation projects.</span></span> <span data-ttu-id="d2d62-132">git 客户端可用于多个平台 (包括 Windows), 且 git 命令行包含在 Azure Bash 云命令行管理程序中。</span><span class="sxs-lookup"><span data-stu-id="d2d62-132">Git clients are available for multiple platforms, including Windows, and the Git command line is included in the Azure Bash cloud shell.</span></span> <span data-ttu-id="d2d62-133">GitHub 是用于 Git 存储库的基于 web 的托管服务。</span><span class="sxs-lookup"><span data-stu-id="d2d62-133">GitHub is a web-based hosting service for Git repositories.</span></span> 

<span data-ttu-id="d2d62-134">如果您有一个作为 GitHub 中的项目托管的应用程序, 则可以通过使用**git clone**命令克隆其存储库来创建项目的本地副本。</span><span class="sxs-lookup"><span data-stu-id="d2d62-134">If you have an application that is hosted as a project in GitHub, you can make a local copy of the project, by cloning its repository using the **git clone** command.</span></span> <span data-ttu-id="d2d62-135">我们将在下一个单元中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="d2d62-135">We'll do this in the next unit.</span></span>

## <a name="editing-files-in-the-cloud-shell"></a><span data-ttu-id="d2d62-136">在云命令行管理程序中编辑文件</span><span class="sxs-lookup"><span data-stu-id="d2d62-136">Editing files in the Cloud SHell</span></span>

<span data-ttu-id="d2d62-137">您可以使用云命令行管理程序中的内置编辑器之一修改组成应用程序的所有文件, 并添加事件中心命名空间、事件中心名称、共享访问策略名称和主键。</span><span class="sxs-lookup"><span data-stu-id="d2d62-137">You can use one of the built-in editors in the Cloud Shell to modify all the files that make up the application and add your Event Hub namespace, Event Hub name, shared access policy name, and primary key.</span></span> 

<span data-ttu-id="d2d62-138">云命令行管理程序支持**nano**、 **vim**和**emacs**以及名为**code**的 Visual Studio 类似代码的编辑器。</span><span class="sxs-lookup"><span data-stu-id="d2d62-138">The Cloud Shell supports **nano**, **vim** and **emacs** as well as a Visual Studio Code-like editor named **code**.</span></span> <span data-ttu-id="d2d62-139">只需键入您想要的编辑器的名称, 它就会在环境中启动。</span><span class="sxs-lookup"><span data-stu-id="d2d62-139">Just type the name of the editor you want and it will launch in the environment.</span></span> <span data-ttu-id="d2d62-140">我们将在下一个单元中使用**代码**编辑器。</span><span class="sxs-lookup"><span data-stu-id="d2d62-140">We'll use the **code** editor in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="d2d62-141">摘要</span><span class="sxs-lookup"><span data-stu-id="d2d62-141">Summary</span></span>

<span data-ttu-id="d2d62-142">必须使用有关事件中心环境的特定信息配置发件人和收件人应用程序。</span><span class="sxs-lookup"><span data-stu-id="d2d62-142">Sender and receiver applications must be configured with specific information about the Event Hub environment.</span></span> <span data-ttu-id="d2d62-143">如果您的接收器应用程序将邮件存储在 Blob 存储中, 则可以创建一个存储帐户。</span><span class="sxs-lookup"><span data-stu-id="d2d62-143">You create a storage account if your receiver application stores messages in Blob Storage.</span></span> <span data-ttu-id="d2d62-144">如果您的应用程序托管在 GitHub 上, 则必须将其克隆到本地目录。</span><span class="sxs-lookup"><span data-stu-id="d2d62-144">If your application is hosted on GitHub, you have to clone it to your local directory.</span></span> <span data-ttu-id="d2d62-145">文本编辑器 (如**nano** ) 用于将命名空间添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="d2d62-145">Text editors, such as **nano** are used to add your namespace to the application.</span></span>