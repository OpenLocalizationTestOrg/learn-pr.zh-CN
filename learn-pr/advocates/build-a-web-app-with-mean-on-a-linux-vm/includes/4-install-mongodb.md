<span data-ttu-id="c0329-101">许多应用程序都需要一个数据库。</span><span class="sxs-lookup"><span data-stu-id="c0329-101">Many applications require a database.</span></span> <span data-ttu-id="c0329-102">在这里, 你将在 "平均" 堆栈中安装 MongoDB ("M")。</span><span class="sxs-lookup"><span data-stu-id="c0329-102">Here you'll install MongoDB, the "M" in the MEAN stack.</span></span> <span data-ttu-id="c0329-103">它是一个免费且开放源代码的流行的 NoSQL 数据库解决方案。</span><span class="sxs-lookup"><span data-stu-id="c0329-103">It's a popular NoSQL database solution that's free and open source.</span></span> <span data-ttu-id="c0329-104">NoSQL 数据库不需要按照预定义的方式对数据进行结构化, 就像 SQL Server 或 MySQL 这样的关系数据库那样。</span><span class="sxs-lookup"><span data-stu-id="c0329-104">A NoSQL database doesn't require data to be structured in a pre-defined way as it would with a relational database like SQL Server or MySQL.</span></span>

<span data-ttu-id="c0329-105">MongoDB 将数据存储在类似 JSON 的文档中, 而不需要严格的数据结构。</span><span class="sxs-lookup"><span data-stu-id="c0329-105">MongoDB stores its data in JSON-like documents that don't require rigid data structures.</span></span> <span data-ttu-id="c0329-106">您使用使用 JavaScript 对象表示法或 JSON 发送的查询和命令与 MongoDB 进行交互。</span><span class="sxs-lookup"><span data-stu-id="c0329-106">You interact with MongoDB using queries and commands sent using JavaScript Object Notation, or JSON.</span></span>

## <a name="what-mongodb-editions-are-available"></a><span data-ttu-id="c0329-107">哪些 MongoDB 版本可用？</span><span class="sxs-lookup"><span data-stu-id="c0329-107">What MongoDB editions are available?</span></span>

<span data-ttu-id="c0329-108">MongoDB 提供了两个版本:</span><span class="sxs-lookup"><span data-stu-id="c0329-108">MongoDB provides two editions:</span></span>

- <span data-ttu-id="c0329-109">MongoDB 社区服务器</span><span class="sxs-lookup"><span data-stu-id="c0329-109">MongoDB Community Server</span></span>
- <span data-ttu-id="c0329-110">MongoDB Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="c0329-110">MongoDB Enterprise Server</span></span>

<span data-ttu-id="c0329-111">在这里, 你将安装 MongoDB 社区服务器。</span><span class="sxs-lookup"><span data-stu-id="c0329-111">Here you'll install MongoDB Community Server.</span></span> <span data-ttu-id="c0329-112">稍后, 您将使用 MongoDB 存储书籍的相关信息。</span><span class="sxs-lookup"><span data-stu-id="c0329-112">Later, you'll use MongoDB to store information about books.</span></span>

## <a name="how-do-i-install-mongodb"></a><span data-ttu-id="c0329-113">如何安装 MongoDB？</span><span class="sxs-lookup"><span data-stu-id="c0329-113">How do I install MongoDB?</span></span>

<span data-ttu-id="c0329-114">您可以在 Linux、macOS 和 Windows 上安装 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="c0329-114">You can install MongoDB on Linux, macOS, and Windows.</span></span> <span data-ttu-id="c0329-115">为便于学习, 在这里, 你将使用 ubuntu 的`apt`程序包管理器在 Ubuntu 上安装 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="c0329-115">For learning purposes, here you'll install MongoDB on Ubuntu using Ubuntu's `apt` package manager.</span></span>

<span data-ttu-id="c0329-116">安装过程因操作系统不同而有所不同。</span><span class="sxs-lookup"><span data-stu-id="c0329-116">The installation process varies depending on your operating system.</span></span> <span data-ttu-id="c0329-117">如果你不熟悉 Ubuntu, 你仍然可以继续关注, 以了解如何工作。</span><span class="sxs-lookup"><span data-stu-id="c0329-117">If you're not familiar with Ubuntu, you can still follow along to get a sense for how things work.</span></span>

<span data-ttu-id="c0329-118">稍后, 您可以[查看安装指南](https://docs.mongodb.com/manual/administration/install-community?azure-portal=true)以了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0329-118">Later, you can [check out the installation guide](https://docs.mongodb.com/manual/administration/install-community?azure-portal=true) to learn more.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="c0329-119">安装 MongoDB</span><span class="sxs-lookup"><span data-stu-id="c0329-119">Install MongoDB</span></span>

<span data-ttu-id="c0329-120">在这里, 你将只使用几个命令安装 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="c0329-120">Here you'll install MongoDB with just a few commands.</span></span> <span data-ttu-id="c0329-121">此过程涉及到注册 MongoDB 存储库, `apt`以便能够找到该包。</span><span class="sxs-lookup"><span data-stu-id="c0329-121">The process involves registering the MongoDB repository so that `apt` can locate the package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0329-122">在这里, 你将从 SSH 连接工作到你在上一个设备中创建的 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="c0329-122">Here, you'll work from the SSH connection to the Ubuntu VM that you created in the previous unit.</span></span>

1. <span data-ttu-id="c0329-123">导入 MongoDB 存储库的加密密钥。</span><span class="sxs-lookup"><span data-stu-id="c0329-123">Import the encryption key for the MongoDB repository.</span></span> <span data-ttu-id="c0329-124">这使程序包管理器能够验证您安装的程序包是否来自 MongoDB inc.。</span><span class="sxs-lookup"><span data-stu-id="c0329-124">This  allows the package manager to verify that the packages you install are coming from MongoDB Inc.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    > [!NOTE]
    > <span data-ttu-id="c0329-125">`sudo`部件意味着我们希望使用管理权限运行命令。</span><span class="sxs-lookup"><span data-stu-id="c0329-125">The `sudo` part means that we want to run the command with administrative privileges.</span></span>

1. <span data-ttu-id="c0329-126">注册 MongoDB 存储库, 以便包管理器可以找到包, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="c0329-126">Register the MongoDB repository so the package manager can locate the packages, like this.</span></span>

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. <span data-ttu-id="c0329-127">更新`apt`包数据库, 以便获得最新的包信息。</span><span class="sxs-lookup"><span data-stu-id="c0329-127">Update the `apt` package database so you have the latest package information.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="c0329-128">安装 MongoDB 程序包。</span><span class="sxs-lookup"><span data-stu-id="c0329-128">Install the MongoDB package.</span></span>

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. <span data-ttu-id="c0329-129">启动 MongoDB 服务。</span><span class="sxs-lookup"><span data-stu-id="c0329-129">Start the MongoDB service.</span></span>

    ```bash
    sudo service mongod start
    ```

1. <span data-ttu-id="c0329-130">运行`mongod --version`以验证安装。</span><span class="sxs-lookup"><span data-stu-id="c0329-130">Run `mongod --version` to verify the installation.</span></span>

    ```bash
    mongod --version
    ```

<span data-ttu-id="c0329-131">将 SSH 连接保持打开状态, 以获取下一部分。</span><span class="sxs-lookup"><span data-stu-id="c0329-131">Keep your SSH connection open for the next part.</span></span>