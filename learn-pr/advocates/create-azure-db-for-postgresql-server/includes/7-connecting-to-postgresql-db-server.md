## <a name="allow-azure-service-access"></a><span data-ttu-id="6fac6-101">允许 Azure 服务访问</span><span class="sxs-lookup"><span data-stu-id="6fac6-101">Allow Azure service access</span></span>

<span data-ttu-id="6fac6-102">在开始之前, 如果你想要使用 PowerShell 并`psql`连接到你的服务器, 你必须允许访问 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="6fac6-102">Before we begin, you'll have to allow access to Azure services if you want to use PowerShell and `psql` to connect to your server.</span></span> <span data-ttu-id="6fac6-103">请记住, 您可以通过两种方式允许访问。</span><span class="sxs-lookup"><span data-stu-id="6fac6-103">Recall that you can allow access in two ways.</span></span>

<span data-ttu-id="6fac6-104">您的第一种方法是启用**允许访问 Azure 服务**。</span><span class="sxs-lookup"><span data-stu-id="6fac6-104">Your first option is to enable **Allow access to Azure services**.</span></span> <span data-ttu-id="6fac6-105">即使规则未在您创建的自定义规则列表中输入, 允许 access 也会创建防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="6fac6-105">Allowing access will create a firewall rule even though the rule isn't entered in the list of custom rules you create.</span></span>

<span data-ttu-id="6fac6-106">第二种方法是创建允许访问所有 IP 地址的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="6fac6-106">Your second option is to create a firewall rule that allows access to all IP addresses.</span></span> <span data-ttu-id="6fac6-107">该规则将包含运行 PowerShell 的客户端的 IP 地址, 您将使用这些地址`psql`执行。</span><span class="sxs-lookup"><span data-stu-id="6fac6-107">The rule will include the IP address for the client running PowerShell that you'll use to execute `psql` from.</span></span>

<span data-ttu-id="6fac6-108">此外, 还需要禁用**强制 SSL 连接**选项。</span><span class="sxs-lookup"><span data-stu-id="6fac6-108">You also need to disable the **Enforce SSL connection** option.</span></span>

### <a name="create-a-firewall-rule"></a><span data-ttu-id="6fac6-109">创建防火墙规则</span><span class="sxs-lookup"><span data-stu-id="6fac6-109">Create a firewall rule</span></span>

1. <span data-ttu-id="6fac6-110">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="6fac6-110">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="6fac6-111">导航到您要为其创建防火墙规则的服务器资源。</span><span class="sxs-lookup"><span data-stu-id="6fac6-111">Navigate to the server resource for which you would like to create a firewall rule.</span></span>

1. <span data-ttu-id="6fac6-112">选择 "**连接安全性**" 选项, 打开右侧的 "连接安全" 边栏。</span><span class="sxs-lookup"><span data-stu-id="6fac6-112">Select the **Connection Security** option to open the connection security blade to the right.</span></span>

    ![显示 PostgreSQL 数据库资源边栏的 "连接安全" 部分的 Azure 门户屏幕截图](../media/6-db-security-settings.png)

<span data-ttu-id="6fac6-114">请记住, 您希望允许对运行`psql`的 PowerShell 客户端进行访问。</span><span class="sxs-lookup"><span data-stu-id="6fac6-114">Recall that you want to allow access to PowerShell clients running `psql`.</span></span>

<span data-ttu-id="6fac6-115">您可以选择执行以下操作之一:</span><span class="sxs-lookup"><span data-stu-id="6fac6-115">You can choose to either:</span></span>

- <span data-ttu-id="6fac6-116">将 "**允许访问 Azure 服务**" 设置为 **"打开"**</span><span class="sxs-lookup"><span data-stu-id="6fac6-116">Set **Allow access to Azure services** to **ON**</span></span>
- <span data-ttu-id="6fac6-117">将 "**强制 SSL 连接**" 设置为 "**已禁用**"</span><span class="sxs-lookup"><span data-stu-id="6fac6-117">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="6fac6-118">单击 "**保存**" 按钮以保存所做的更改</span><span class="sxs-lookup"><span data-stu-id="6fac6-118">Click the **Save** button to save your changes</span></span>

<span data-ttu-id="6fac6-119">或者, 您可以添加防火墙规则, 以允许通过添加防火墙规则访问所有 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="6fac6-119">Or, you can add a firewall rule to allow access to all IP addresses by adding a firewall rule.</span></span> <span data-ttu-id="6fac6-120">使用以下值:</span><span class="sxs-lookup"><span data-stu-id="6fac6-120">Use the following values:</span></span>

- <span data-ttu-id="6fac6-121">规则名称:`AllowAll`</span><span class="sxs-lookup"><span data-stu-id="6fac6-121">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="6fac6-122">起始 IP:`0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="6fac6-122">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="6fac6-123">结束 IP:`255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="6fac6-123">End IP: `255.255.255.255`</span></span>
- <span data-ttu-id="6fac6-124">将 "**强制 SSL 连接**" 设置为 "**已禁用**"</span><span class="sxs-lookup"><span data-stu-id="6fac6-124">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="6fac6-125">单击 "**保存**" 按钮以保存所做的更改</span><span class="sxs-lookup"><span data-stu-id="6fac6-125">Click the **Save** button to save your changes</span></span>

> [!Warning]
> <span data-ttu-id="6fac6-126">创建此防火墙规则将允许 Internet 上的任何 IP 地址尝试连接到您的服务器。</span><span class="sxs-lookup"><span data-stu-id="6fac6-126">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="6fac6-127">在生产环境中, 您需要限制对特定 IP 地址的访问。</span><span class="sxs-lookup"><span data-stu-id="6fac6-127">In production environments, you'll want to restrict access to specific IP addresses.</span></span>

### <a name="connect-to-the-database-with-psql"></a><span data-ttu-id="6fac6-128">使用 psql 连接到数据库</span><span class="sxs-lookup"><span data-stu-id="6fac6-128">Connect to the database with psql</span></span>

1. <span data-ttu-id="6fac6-129">在右侧的 Azure 云命令行管理程序中`psql` , 使用以下命令连接到您的服务器。</span><span class="sxs-lookup"><span data-stu-id="6fac6-129">In the Azure Cloud Shell on the right, connect `psql` to your server using the following command.</span></span> <span data-ttu-id="6fac6-130">请务必替换服务器名称和管理员名称。</span><span class="sxs-lookup"><span data-stu-id="6fac6-130">Make sure to replace the server name and admin name.</span></span>

    ```bash
    psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
    ```

    <span data-ttu-id="6fac6-131">使用为、和`server-name` `admin-user`的选择的值。</span><span class="sxs-lookup"><span data-stu-id="6fac6-131">Use the values you chose for the `server-name`, and `admin-user`.</span></span>

1. <span data-ttu-id="6fac6-132">**postgres**是使用创建的每个 PostgreSQL 服务器的默认管理数据库。</span><span class="sxs-lookup"><span data-stu-id="6fac6-132">**postgres** is the default management database every PostgreSQL server is created with.</span></span> <span data-ttu-id="6fac6-133">系统将提示你输入创建服务器时提供的密码。</span><span class="sxs-lookup"><span data-stu-id="6fac6-133">You'll be prompted for the password you provided when you created the server.</span></span>

1. <span data-ttu-id="6fac6-134">成功连接后, 执行`\l`命令以列出所有数据库。</span><span class="sxs-lookup"><span data-stu-id="6fac6-134">Once successfully connected, execute the `\l` command to list all databases.</span></span> <span data-ttu-id="6fac6-135">此命令将导致返回两个或更多的默认数据库。</span><span class="sxs-lookup"><span data-stu-id="6fac6-135">This command will result in two or more default databases returned.</span></span>

1. <span data-ttu-id="6fac6-136">按`q` "退出列表"。</span><span class="sxs-lookup"><span data-stu-id="6fac6-136">Press `q` to exit the list.</span></span>

1. <span data-ttu-id="6fac6-137">使用以下 SQL 命令创建新数据库:</span><span class="sxs-lookup"><span data-stu-id="6fac6-137">Create a new database with the following SQL command:</span></span>

    ```sql
    CREATE DATABASE "Adventureworks";
    ```

1. <span data-ttu-id="6fac6-138">运行 psql 命令`\c Adventureworks`以连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="6fac6-138">Run the psql command `\c Adventureworks` to connect to the database.</span></span>

1. <span data-ttu-id="6fac6-139">使用以下 SQL 命令向数据库添加一些数据, 以将数据添加到两个表中:</span><span class="sxs-lookup"><span data-stu-id="6fac6-139">Add some data to the database with the following SQL commands that add data to two tables:</span></span>

    ```sql
    CREATE TABLE PEOPLE(NAME TEXT NOT NULL, AGE INT NOT NULL);
    INSERT INTO PEOPLE(NAME, AGE) VALUES ('Bob', 35);
    INSERT INTO PEOPLE(NAME, AGE) VALUES ('Sarah', 28);
    CREATE TABLE LOCATIONS(CITY TEXT NOT NULL, STATE TEXT NOT NULL);
    INSERT INTO LOCATIONS(CITY, STATE) VALUES ('New York', 'NY');
    INSERT INTO LOCATIONS(CITY, STATE) VALUES ('Flint', 'MI');
    ```

1. <span data-ttu-id="6fac6-140">使用以下 SQL 命令检索添加的数据:</span><span class="sxs-lookup"><span data-stu-id="6fac6-140">Retrieve the data you added using the following SQL commands:</span></span>

    ```sql
    SELECT * FROM PEOPLE;
    SELECT * FROM LOCATIONS;
    ```

1. <span data-ttu-id="6fac6-141">您可以尝试其他 psql 命令。</span><span class="sxs-lookup"><span data-stu-id="6fac6-141">You can try other psql commands.</span></span>
    - <span data-ttu-id="6fac6-142">`-?`获取帮助。</span><span class="sxs-lookup"><span data-stu-id="6fac6-142">`-?` to get help.</span></span>
    - <span data-ttu-id="6fac6-143">`\dt`列出表。</span><span class="sxs-lookup"><span data-stu-id="6fac6-143">`\dt` to list the tables.</span></span>

1. <span data-ttu-id="6fac6-144">在服务器上执行完 psql 操作后, 请执行命令`\q`以退出 psql。</span><span class="sxs-lookup"><span data-stu-id="6fac6-144">When you're finished executing psql operations on your server, execute the command `\q` to quit psql.</span></span>
