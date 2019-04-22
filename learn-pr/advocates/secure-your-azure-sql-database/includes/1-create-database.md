<span data-ttu-id="af913-101">在这里, 你将设置在整个模块中使用所需的资源。</span><span class="sxs-lookup"><span data-stu-id="af913-101">Here you'll set up the resources you'll need for use throughout this module.</span></span> <span data-ttu-id="af913-102">让我们设想一种基本体系结构, 它由托管客户使用的应用程序的服务器组成, 连接到数据库以存储其数据。</span><span class="sxs-lookup"><span data-stu-id="af913-102">Let's envision a basic architecture consisting of a server hosting an application that your customers use, which connects to a database for the storage of its data.</span></span> <span data-ttu-id="af913-103">应用程序在虚拟机上运行, 并且最近将数据库从运行在 VM 上的 SQL Server 数据库迁移到 Azure SQL 数据库服务上的数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-103">The application runs on a virtual machine, and the database has been recently migrated from a SQL Server database running on a VM to a database on the Azure SQL Database service.</span></span> <span data-ttu-id="af913-104">若要演示如何保护数据库, 我们将设置以下资源以在此模块中使用:</span><span class="sxs-lookup"><span data-stu-id="af913-104">To show how you can secure your database, we're going to set up the following resources for use throughout this module:</span></span>

- <span data-ttu-id="af913-105">名为_appServer_的 Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="af913-105">A Linux VM named _appServer_.</span></span> <span data-ttu-id="af913-106">此服务器将充当用户要连接到的应用程序服务器, 将需要连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-106">This server will act as the application server that users would be connecting to, and will need to connect to the database.</span></span> <span data-ttu-id="af913-107">我们将在`sqlcmd` VM 上安装以模拟运行在_appServer_上的应用程序, 从而连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-107">We'll install `sqlcmd` on the VM to simulate an application running on _appServer_ making connections to the database.</span></span>
- <span data-ttu-id="af913-108">Azure SQL 数据库逻辑服务器。</span><span class="sxs-lookup"><span data-stu-id="af913-108">An Azure SQL Database logical server.</span></span> <span data-ttu-id="af913-109">需要此逻辑服务器来承载一个或多个数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-109">This logical server is needed to host one or more databases.</span></span>
- <span data-ttu-id="af913-110">我们的逻辑服务器上名为_marketplaceDb_的数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-110">A database on our logical server called _marketplaceDb_.</span></span> <span data-ttu-id="af913-111">我们将使用_AdventureWorksLT_ demo 数据库创建它, 以便我们有一些表和数据可供使用。</span><span class="sxs-lookup"><span data-stu-id="af913-111">We'll create it using the _AdventureWorksLT_ demo database so we have some tables and data to work with.</span></span> <span data-ttu-id="af913-112">这将包括一些敏感数据, 如我们要确保正确保护的电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="af913-112">This will include some sensitive data, such as email addresses and phone numbers that we'll want to make sure are properly secured.</span></span>

<span data-ttu-id="af913-113">让我们做准备吧!</span><span class="sxs-lookup"><span data-stu-id="af913-113">Let's get things set up!</span></span>

<!-- Activate the sandbox -->
[!INCLUDE [azure-sandbox-activate](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="af913-114">创建 Azure SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="af913-114">Create an Azure SQL Database</span></span>

1. <span data-ttu-id="af913-115">首先, 让我们设置一些变量。</span><span class="sxs-lookup"><span data-stu-id="af913-115">First, let's set up some variables.</span></span> <span data-ttu-id="af913-116">将下面显示`<>`的值替换为您选择的值。</span><span class="sxs-lookup"><span data-stu-id="af913-116">Replace values below that are shown in `<>` with values of your choice.</span></span> <span data-ttu-id="af913-117">请注意, `<password>`必须至少包含八个字符, 并且至少包含三个类别中的字符: 大写字符、小写字符、数字和非字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="af913-117">Note that the `<password>` must have at least eight characters and contain characters from at least three of these categories: uppercase characters, lowercase characters, numbers, and non-alphanumeric characters.</span></span> <span data-ttu-id="af913-118">保存登录以供以后使用。</span><span class="sxs-lookup"><span data-stu-id="af913-118">Save the login for use later.</span></span>

    ```bash
    # Set an admin login and password for your database
    export ADMINLOGIN='<ServerAdmin>'
    export PASSWORD='<password>'
    # Set the logical SQL server name. We'll add a random string as it needs to be globally unique.
    export SERVERNAME=server$RANDOM
    export RESOURCEGROUP=<rgn>[sandbox resource group name]</rgn>
    # Set the location, we'll pull the location from our resource group.
    export LOCATION=$(az group show --name <rgn>[sandbox resource group name]</rgn> | jq -r '.location')
    ```

1. <span data-ttu-id="af913-119">运行以下命令以创建新的 Azure SQL 数据库逻辑服务器。</span><span class="sxs-lookup"><span data-stu-id="af913-119">Run the following command to create a new Azure SQL Database logical server.</span></span>

    ```azurecli
    az sql server create \
        --name $SERVERNAME \
        --resource-group $RESOURCEGROUP \
        --location $LOCATION \
        --admin-user $ADMINLOGIN \
        --admin-password "$PASSWORD"
    ```

1. <span data-ttu-id="af913-120">现在, 运行以下各项, 在刚刚创建的逻辑服务器上创建名为**marketplaceDb**的数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-120">Now run the following to create the database called **marketplaceDb** on the logical server you just created.</span></span> <span data-ttu-id="af913-121">这将使用_AdventureWorksLT_数据库作为模板, 因此我们将使用一些预填充表来处理。</span><span class="sxs-lookup"><span data-stu-id="af913-121">This will use the _AdventureWorksLT_ database as a template so we'll have some pre-populated tables to work with.</span></span>

    ```azurecli
    az sql db create --resource-group $RESOURCEGROUP \
        --server $SERVERNAME \
        --name marketplaceDb \
        --sample-name AdventureWorksLT \
        --service-objective Basic
    ```

1. <span data-ttu-id="af913-122">让我们做最后一件事, 并获取此数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="af913-122">Let's do one last thing and get the connection string for this database.</span></span>

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name marketplaceDb --server $SERVERNAME | jq -r
    ```

    <span data-ttu-id="af913-123">您的输出与此类似。</span><span class="sxs-lookup"><span data-stu-id="af913-123">Your output resembles this.</span></span> <span data-ttu-id="af913-124">请务必这样做, 你将需要此命令在稍后在本模块中连接到你的数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-124">Keep this handy, you'll need this command to connect to your database later in this module.</span></span> <span data-ttu-id="af913-125">请注意`<username>`要`<password>`将其替换为您在前面的变量中指定的`ADMINLOGIN`和`PASSWORD`凭据的命令中的和占位符。</span><span class="sxs-lookup"><span data-stu-id="af913-125">Note the `<username>` and `<password>` placeholders in the command that you will want to replace with the `ADMINLOGIN` and `PASSWORD` credentials you specified in variables earlier.</span></span>

    ```output
    sqlcmd -S tcp:server12345.database.windows.net,1433 -d marketplaceDb -U <username> -P <password> -N -l 30
    ```

## <a name="create-and-configure-a-linux-virtual-machine"></a><span data-ttu-id="af913-126">创建和配置 Linux 虚拟机</span><span class="sxs-lookup"><span data-stu-id="af913-126">Create and configure a Linux virtual machine</span></span>

<span data-ttu-id="af913-127">现在, 让我们通过一些示例创建要使用的 Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="af913-127">Now let's create the Linux VM that we'll use through some examples.</span></span>

1. <span data-ttu-id="af913-128">运行以下命令以创建 VM。</span><span class="sxs-lookup"><span data-stu-id="af913-128">Run the following command to create the VM.</span></span>

    ```azurecli
    az vm create \
      --resource-group $RESOURCEGROUP \
      --name appServer \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --generate-ssh-keys
    ```

1. <span data-ttu-id="af913-129">成功创建虚拟机后, 通过 SSH 连接到它。</span><span class="sxs-lookup"><span data-stu-id="af913-129">Once your VM is successfully created, connect to it via SSH.</span></span>

    ```azurecli
    ssh <X.X.X.X>
    ```

    > [!NOTE]
    > <span data-ttu-id="af913-130">有两个注意事项。</span><span class="sxs-lookup"><span data-stu-id="af913-130">Two things to note.</span></span> <span data-ttu-id="af913-131">首先, 我们不需要密码, 因为我们生成了一个 SSH 密钥对作为 VM 创建的一部分。</span><span class="sxs-lookup"><span data-stu-id="af913-131">First, we don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="af913-132">其次, 在将初始命令行管理程序连接到 VM 时, 它会向你提供有关主机的真实性的提示。</span><span class="sxs-lookup"><span data-stu-id="af913-132">Second, on the initial shell connection into the VM it will give you a prompt about the authenticity of the host.</span></span> <span data-ttu-id="af913-133">这是因为我们要连接的是 IP 地址而不是主机名。</span><span class="sxs-lookup"><span data-stu-id="af913-133">This occurs because we are connecting to an IP address instead of a host name.</span></span> <span data-ttu-id="af913-134">回答 "是" 将把 IP 保存为有效的连接主机, 并允许连接继续进行。</span><span class="sxs-lookup"><span data-stu-id="af913-134">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

1. <span data-ttu-id="af913-135">现在, 让我们通过在 Linux VM 上安装 mssql-工具来完成此任务, 以便我们能够通过 sqlcmd 连接到我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-135">Now let's finish things up by installing mssql-tools on the Linux VM so we'll be able to connect to our database through sqlcmd.</span></span>

    ```bash
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
    source ~/.bashrc
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    sudo apt-get update
    sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev
    ```

    > [!NOTE]
    > <span data-ttu-id="af913-136">对于其中一些命令, 会滚动许多文本, 因此请确保在最后一个命令后按 enter, 以确保它能够运行。</span><span class="sxs-lookup"><span data-stu-id="af913-136">A lot of text will scroll by for some of these commands, so make sure you hit enter after the final command to ensure it runs.</span></span>

<span data-ttu-id="af913-137">我们已创建了 Azure SQL 数据库逻辑服务器、该逻辑服务器上的数据库以及一个名为_appServer_的虚拟机, 我们将使用这些虚拟机模拟来自应用程序服务器的网络连接。</span><span class="sxs-lookup"><span data-stu-id="af913-137">We've created an Azure SQL Database logical server, a database on that logical server, and a virtual machine called _appServer_ that we'll use to simulate network connectivity from an application server.</span></span> <span data-ttu-id="af913-138">我们来看看如何正确保护我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="af913-138">Let's take a look at how we can properly secure our database.</span></span>