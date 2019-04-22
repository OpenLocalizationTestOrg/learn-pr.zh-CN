<span data-ttu-id="f5ce6-101">在将数据库连接到您的应用程序之前, 您需要检查您是否可以连接到它, 添加一个基本表, 并使用示例数据。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-101">Before you connect the database to your app, you want to check that you can connect to it, add a basic table, and work with sample data.</span></span>

<span data-ttu-id="f5ce6-102">我们维护 Azure SQL 数据库的基础结构、软件更新和修补程序。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-102">We maintain the infrastructure, software updates, and patches for your Azure SQL database.</span></span> <span data-ttu-id="f5ce6-103">此外, 您还可以像对待任何其他 SQL Server 安装那样对待您的 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-103">Beyond that, you can treat your Azure SQL database like you would any other SQL Server installation.</span></span> <span data-ttu-id="f5ce6-104">例如, 您可以使用 Visual studio、SQL Server Management Studio、Azure Data Studio 或其他工具来管理 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-104">For example, you can use Visual Studio, SQL Server Management Studio, Azure Data Studio, or other tools to manage your Azure SQL database.</span></span>

<span data-ttu-id="f5ce6-105">您如何访问数据库并将其连接到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-105">How you access your database and connect it to your app is up to you.</span></span> <span data-ttu-id="f5ce6-106">但是, 若要获得一些使用数据库的经验, 可直接从门户连接到它, 创建一个表, 并运行几个基本的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-106">But to get some experience working with your database, here you'll connect to it directly from the portal, create a table, and run a few basic CRUD operations.</span></span> <span data-ttu-id="f5ce6-107">你将了解:</span><span class="sxs-lookup"><span data-stu-id="f5ce6-107">You'll learn:</span></span>

- <span data-ttu-id="f5ce6-108">什么是云命令行管理程序, 以及如何从门户访问它。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-108">What Cloud Shell is and how to access it from the portal.</span></span>
- <span data-ttu-id="f5ce6-109">如何从 Azure CLI 访问有关数据库的信息, 包括连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-109">How to access information about your database from the Azure CLI, including connection strings.</span></span>
- <span data-ttu-id="f5ce6-110">如何使用`sqlcmd`连接到您的数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-110">How to connect to your database using `sqlcmd`.</span></span>
- <span data-ttu-id="f5ce6-111">如何使用基本表和一些示例数据初始化数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-111">How to initialize your database with a basic table and some sample data.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="f5ce6-112">什么是 Azure 云命令行管理程序？</span><span class="sxs-lookup"><span data-stu-id="f5ce6-112">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="f5ce6-113">azure 云命令行管理程序是用于管理和开发 Azure 资源的基于浏览器的命令行管理程序体验。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-113">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span> <span data-ttu-id="f5ce6-114">将云命令行管理程序视为一个在云中运行的交互控制台。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-114">Think of Cloud Shell as an interactive console that runs in the cloud.</span></span>

<span data-ttu-id="f5ce6-115">在幕后, 云命令行管理程序在 Linux 上运行。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-115">Behind the scenes, Cloud Shell runs on Linux.</span></span> <span data-ttu-id="f5ce6-116">但根据您是否喜欢 Linux 或 Windows 环境, 您有两种体验可供选择: Bash 和 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-116">But depending on whether you prefer a Linux or Windows environment, you have two experiences to choose from: Bash and PowerShell.</span></span>

<span data-ttu-id="f5ce6-117">可以从任何位置访问云命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-117">Cloud Shell is accessible from anywhere.</span></span> <span data-ttu-id="f5ce6-118">除了门户之外, 您还可以从[shell.azure.com](https://shell.azure.com/)、azure 移动应用或 Visual Studio Code 中访问云命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-118">Besides the portal, you can also access Cloud Shell from [shell.azure.com](https://shell.azure.com/), the Azure mobile app, or from Visual Studio Code.</span></span> <span data-ttu-id="f5ce6-119">右侧的面板是云命令行管理程序终端, 可供您在本练习中使用。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-119">The panel on the right is a Cloud Shell terminal for you to use during this exercise.</span></span>

<span data-ttu-id="f5ce6-120">云命令行管理程序包含流行工具和文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-120">Cloud Shell includes popular tools and text editors.</span></span> <span data-ttu-id="f5ce6-121">下面简要介绍`az` `jq`了、和`sqlcmd`, 将用于当前任务的三个工具。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-121">Here's a brief look at `az`, `jq`, and `sqlcmd`, three tools you'll use for our current task.</span></span>

- <span data-ttu-id="f5ce6-122">`az`也称为 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-122">`az` is also known as the Azure CLI.</span></span> <span data-ttu-id="f5ce6-123">它是用于使用 Azure 资源的命令行界面。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-123">It's the command-line interface for working with Azure resources.</span></span> <span data-ttu-id="f5ce6-124">您将使用此信息获取有关您的数据库的信息, 包括连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-124">You'll use this to get information about your database, including the connection string.</span></span>
- <span data-ttu-id="f5ce6-125">`jq`是命令行 JSON 分析器。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-125">`jq` is a command-line JSON parser.</span></span> <span data-ttu-id="f5ce6-126">您将从`az`命令到此工具的管道输出, 以从 JSON 输出中提取重要字段。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-126">You'll pipe output from `az` commands to this tool to extract important fields from JSON output.</span></span>
- <span data-ttu-id="f5ce6-127">`sqlcmd`使您能够在 SQL Server 上执行语句。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-127">`sqlcmd` enables you to execute statements on SQL Server.</span></span> <span data-ttu-id="f5ce6-128">你将使用`sqlcmd` Azure SQL 数据库创建交互式会话。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-128">You'll use `sqlcmd` to create an interactive session with your Azure SQL database.</span></span>

## <a name="get-information-about-your-azure-sql-database"></a><span data-ttu-id="f5ce6-129">获取有关 Azure SQL 数据库的信息</span><span class="sxs-lookup"><span data-stu-id="f5ce6-129">Get information about your Azure SQL database</span></span>

<span data-ttu-id="f5ce6-130">在连接到数据库之前, 最好先验证它是否存在并处于联机状态。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-130">Before you connect to your database, it's a good idea to verify it exists and is online.</span></span>

<span data-ttu-id="f5ce6-131">在这里, 使用该`az`实用工具列出数据库, 并显示有关**后勤**数据库的一些信息, 包括其最大大小和状态。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-131">Here, you use the `az` utility to list your databases and show some information about the **Logistics** database, including its maximum size and status.</span></span>

1. <span data-ttu-id="f5ce6-132">您`az`要运行的命令需要资源组的名称和 Azure SQL 逻辑服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-132">The `az` commands you'll run require the name of your resource group and the name of your Azure SQL logical server.</span></span> <span data-ttu-id="f5ce6-133">若要保存键入, 请`azure configure`运行此命令以将其指定为默认值。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-133">To save typing, run this `azure configure` command to specify them as default values.</span></span>
    <span data-ttu-id="f5ce6-134">将`<server-name>`替换为 Azure SQL 逻辑服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-134">Replace `<server-name>` with the name of your Azure SQL logical server.</span></span> <span data-ttu-id="f5ce6-135">请注意, 根据您在门户中所处的刀片式服务器, 这可能显示为 FQDN (servername.database.windows.net), 但您只需要一个不带. database.windows.net 后缀的逻辑名称。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-135">Note that depending on the blade you are on in the portal this may show as a FQDN (servername.database.windows.net), but you only need the logical name without the .database.windows.net suffix.</span></span>

    ```azurecli
    az configure --defaults group=<rgn>[sandbox resource group name]</rgn> sql-server=<server-name>
    ```

1. <span data-ttu-id="f5ce6-136">运行`az sql db list`以列出 Azure SQL 逻辑服务器上的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-136">Run `az sql db list` to list all databases on your Azure SQL logical server.</span></span>

    ```azurecli
    az sql db list
    ```
    <span data-ttu-id="f5ce6-137">您看到的 JSON 块是一个大的输出块。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-137">You see a large block of JSON as output.</span></span>

1. <span data-ttu-id="f5ce6-138">由于我们只需要数据库名称, 第二次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-138">Since we want just the database names, run the command a second time.</span></span> <span data-ttu-id="f5ce6-139">这次, 将输出管道传输`jq`到仅打印名称字段。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-139">This time, pipe the output to `jq` to print out only the name fields.</span></span>
   
     ```azurecli
    az sql db list | jq '[.[] | {name: .name}]'
    ```
    
    <span data-ttu-id="f5ce6-140">您应该会看到此输出。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-140">You should see this output.</span></span>
    
    ```json
    [
      {
        "name": "Logistics"
      },
      {
        "name": "master"
      }
    ]
    ```

    <span data-ttu-id="f5ce6-141">**后勤**是您的数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-141">**Logistics** is your database.</span></span> <span data-ttu-id="f5ce6-142">与 SQL Server 一样, **master**包括服务器元数据, 例如登录帐户和系统配置设置。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-142">Like SQL Server, **master** includes server metadata, such as sign-in accounts and system configuration settings.</span></span>

1. <span data-ttu-id="f5ce6-143">运行此`az sql db show`命令可获取有关**后勤**数据库的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-143">Run this `az sql db show` command to get details about the **Logistics** database.</span></span>

    ```azurecli
    az sql db show --name Logistics
    ```

    <span data-ttu-id="f5ce6-144">如前所述, 您会看到一个 JSON 作为输出的大块。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-144">As before, you see a large block of JSON as output.</span></span>

1. <span data-ttu-id="f5ce6-145">第二次运行该命令。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-145">Run the command a second time.</span></span> <span data-ttu-id="f5ce6-146">这次, 将输出管道传输`jq`到, 以将输出限制为仅为**物流**数据库的名称、最大大小和状态。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-146">This time, pipe the output to `jq` to limit output to only the name, maximum size, and status of the **Logistics** database.</span></span>

    ```azurecli
    az sql db show --name Logistics | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
    ```

    <span data-ttu-id="f5ce6-147">您会发现数据库处于联机状态, 并且可以容纳大约 2 GB 的数据。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-147">You see that the database is online and can hold around 2 GB of data.</span></span>

    ```json
    {
      "name": "Logistics",
      "maxSizeBytes": 2147483648,
      "status": "Online"
    }
    ```

## <a name="connect-to-your-database"></a><span data-ttu-id="f5ce6-148">连接到您的数据库</span><span class="sxs-lookup"><span data-stu-id="f5ce6-148">Connect to your database</span></span>

<span data-ttu-id="f5ce6-149">现在您已经了解了有关数据库的几点, 让我们使用`sqlcmd`创建一个表, 其中包含有关运输驱动因素的信息, 并执行几个基本的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-149">Now that you understand a bit about your database, let's connect to it using `sqlcmd`, create a table that holds information about transportation drivers, and perform a few basic CRUD operations.</span></span>

<span data-ttu-id="f5ce6-150">请注意, CRUD 代表 "**创建**"、"**读取**"、"**更新**" 和 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-150">Remember that CRUD stands for **create**, **read**, **update**, and **delete**.</span></span> <span data-ttu-id="f5ce6-151">这些术语指的是对表数据执行的操作, 并且是应用所需的四个基本操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-151">These terms refer to operations you perform on table data and are the four basic operations you need for your app.</span></span> <span data-ttu-id="f5ce6-152">现在我们来验证你是否可以执行每个工作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-152">Now's a good time to verify you can perform each of them.</span></span>

1. <span data-ttu-id="f5ce6-153">运行此`az sql db show-connection-string`命令, 以`sqlcmd`可使用的格式获取**后勤**数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-153">Run this `az sql db show-connection-string` command to get the connection string to the **Logistics** database in a format that `sqlcmd` can use.</span></span>

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name Logistics
    ```

    <span data-ttu-id="f5ce6-154">您的输出与此类似。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-154">Your output resembles this.</span></span>

    ```output
    "sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U <username> -P <password> -N -l 30"
    ```

1. <span data-ttu-id="f5ce6-155">运行上`sqlcmd`一步的输出中的语句以创建交互式会话。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-155">Run the `sqlcmd` statement from the output of the previous step to create an interactive session.</span></span> <span data-ttu-id="f5ce6-156">删除周围的引号, 并`<username>`将`<password>`其替换为您在创建数据库时指定的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-156">Remove the surrounding quotes and replace `<username>` and `<password>` with the username and password you specified when you created your database.</span></span> <span data-ttu-id="f5ce6-157">下面是一个示例。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-157">Here's an example.</span></span>

    ```console
    sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U martina -P "password1234$" -N -l 30
    ```

    > [!TIP]
    > <span data-ttu-id="f5ce6-158">将密码放在引号中, 以便 "&" 和其他特殊字符不会解释为处理指令。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-158">Place your password in quotes so that "&" and other special characters aren't interpreted as processing instructions.</span></span>

1. <span data-ttu-id="f5ce6-159">在`sqlcmd`会话中, 创建一个名为`Drivers`的表。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-159">From your `sqlcmd` session, create a table named `Drivers`.</span></span>

    ```sql
    CREATE TABLE Drivers (DriverID int, LastName varchar(255), FirstName varchar(255), OriginCity varchar(255));
    GO
    ```

    <span data-ttu-id="f5ce6-160">该表包含四列: 唯一标识符、驱动程序的姓氏和名字以及驱动程序的源城市。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-160">The table contains four columns: a unique identifier, the driver's last and first name, and the driver's city of origin.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5ce6-161">您在此处看到的语言是 transact-sql 或 t-sql。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-161">The language you see here is Transact-SQL, or T-SQL.</span></span>

1. <span data-ttu-id="f5ce6-162">验证`Drivers`表是否存在。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-162">Verify that the `Drivers` table exists.</span></span>

    ```sql
    SELECT name FROM sys.tables;
    GO
    ```

    <span data-ttu-id="f5ce6-163">您应该会看到此输出。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-163">You should see this output.</span></span>

    ```output
    name
    --------------------------------------------------------------------------------------------------------------------------------
    Drivers

    (1 rows affected)
    ```

1. <span data-ttu-id="f5ce6-164">运行此`INSERT` t-sql 语句以向表中添加示例行。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-164">Run this `INSERT` T-SQL statement to add a sample row to the table.</span></span> <span data-ttu-id="f5ce6-165">这是**创建**操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-165">This is the **create** operation.</span></span>

    ```sql
    INSERT INTO Drivers (DriverID, LastName, FirstName, OriginCity) VALUES (123, 'Zirne', 'Laura', 'Springfield');
    GO
    ```

    <span data-ttu-id="f5ce6-166">你会看到此指示操作已成功。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-166">You see this to indicate the operation succeeded.</span></span>

    ```output
    (1 rows affected)
    ```

1. <span data-ttu-id="f5ce6-167">运行此`SELECT` t-sql 语句以列出表中所有`DriverID`行`OriginCity`的和列。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-167">Run this `SELECT` T-SQL statement to list the `DriverID` and `OriginCity` columns from all rows in the table.</span></span> <span data-ttu-id="f5ce6-168">这是**读取**操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-168">This is the **read** operation.</span></span>

    ```sql
    SELECT DriverID, OriginCity FROM Drivers;
    GO
    ```

    <span data-ttu-id="f5ce6-169">你将看到在上一`DriverID`步`OriginCity`中创建的行与和对应的一个结果。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-169">You see one result with the `DriverID` and `OriginCity` for the row you created in the previous step.</span></span>

    ```output
    DriverID    OriginCity
    ----------- --------------------------
            123 Springfield

    (1 rows affected)
    ```

1. <span data-ttu-id="f5ce6-170">运行此`UPDATE` t-sql 语句可将驱动程序的 "Springfield" 的 "源城市" 更改为 123 `DriverID`的驱动程序的 "波士顿"。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-170">Run this `UPDATE` T-SQL statement to change the city of origin from "Springfield" to "Boston" for the driver with a `DriverID` of 123.</span></span> <span data-ttu-id="f5ce6-171">这是**更新**操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-171">This is the **update** operation.</span></span>

    ```sql
    UPDATE Drivers SET OriginCity='Boston' WHERE DriverID=123;
    GO
    SELECT DriverID, OriginCity FROM Drivers;
    GO
    ```

    <span data-ttu-id="f5ce6-172">您应该会看到以下输出。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-172">You should see the following output.</span></span> <span data-ttu-id="f5ce6-173">请注意, `OriginCity`如何反映对波士顿的更新。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-173">Notice how the `OriginCity` reflects the update to Boston.</span></span>

    ```output
    DriverID    OriginCity
    ----------- --------------------------
            123 Boston

    (1 rows affected)
    ```

1. <span data-ttu-id="f5ce6-174">运行此`DELETE` t-sql 语句以删除记录。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-174">Run this `DELETE` T-SQL statement to delete the record.</span></span> <span data-ttu-id="f5ce6-175">这是**删除**操作。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-175">This is the **delete** operation.</span></span>

    ```sql
    DELETE FROM Drivers WHERE DriverID=123;
    GO
    ```

    ```output
    (1 rows affected)
    ```

1. <span data-ttu-id="f5ce6-176">运行此`SELECT` t-sql 语句以验证`Drivers`表是否为空。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-176">Run this `SELECT` T-SQL statement to verify the `Drivers` table is empty.</span></span>

    ```sql
    SELECT COUNT(*) FROM Drivers;
    GO
    ```

    <span data-ttu-id="f5ce6-177">您会发现该表不包含任何行。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-177">You see that the table contains no rows.</span></span>

    ```output
    -----------
              0

    (1 rows affected)
    ```

<span data-ttu-id="f5ce6-178">现在, 您已从云命令行管理程序使用了 Azure SQL 数据库, 您可以获取最喜爱的 sql 管理工具&ndash;的连接字符串, 而不管它是来自 SQL Server management Studio、Visual studio 还是其他内容。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-178">Now that you have the hang of working with Azure SQL Database from Cloud Shell, you can get the connection string for your favorite SQL management tool &ndash; whether that's from SQL Server Management Studio, Visual Studio, or something else.</span></span>

<span data-ttu-id="f5ce6-179">云命令行管理程序使您可以轻松地访问和使用 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-179">Cloud Shell makes it easy to access and work with your Azure resources.</span></span> <span data-ttu-id="f5ce6-180">由于云命令行管理程序是基于浏览器的, 因此可以从 Windows、macOS 或&ndash; Linux 中通过 web 浏览器的任何系统访问该命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-180">Because Cloud Shell is browser-based, you can access it from Windows, macOS, or Linux &ndash; essentially any system with a web browser.</span></span>

<span data-ttu-id="f5ce6-181">你获得了一些运行 azure CLI 命令的实践经验, 以获取有关 Azure SQL 数据库的信息。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-181">You gained some hands-on experience running Azure CLI commands to get information about your Azure SQL database.</span></span> <span data-ttu-id="f5ce6-182">作为一项奖金, 你为你的 T-SQL 技能做了练习。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-182">As a bonus, you practiced your T-SQL skills.</span></span>

<span data-ttu-id="f5ce6-183">最后, 让我们总结并了解如何拉出您的数据库。</span><span class="sxs-lookup"><span data-stu-id="f5ce6-183">Finally, let's wrap up and see how to tear down your database.</span></span>
