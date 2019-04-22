在这里, 你将设置在整个模块中使用所需的资源。 让我们设想一种基本体系结构, 它由托管客户使用的应用程序的服务器组成, 连接到数据库以存储其数据。 应用程序在虚拟机上运行, 并且最近将数据库从运行在 VM 上的 SQL Server 数据库迁移到 Azure SQL 数据库服务上的数据库。 若要演示如何保护数据库, 我们将设置以下资源以在此模块中使用:

- 名为_appServer_的 Linux 虚拟机。 此服务器将充当用户要连接到的应用程序服务器, 将需要连接到数据库。 我们将在`sqlcmd` VM 上安装以模拟运行在_appServer_上的应用程序, 从而连接到数据库。
- Azure SQL 数据库逻辑服务器。 需要此逻辑服务器来承载一个或多个数据库。
- 我们的逻辑服务器上名为_marketplaceDb_的数据库。 我们将使用_AdventureWorksLT_ demo 数据库创建它, 以便我们有一些表和数据可供使用。 这将包括一些敏感数据, 如我们要确保正确保护的电子邮件地址和电话号码。

让我们做准备吧!

<!-- Activate the sandbox -->
[!INCLUDE [azure-sandbox-activate](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-sql-database"></a>创建 Azure SQL 数据库

1. 首先, 让我们设置一些变量。 将下面显示`<>`的值替换为您选择的值。 请注意, `<password>`必须至少包含八个字符, 并且至少包含三个类别中的字符: 大写字符、小写字符、数字和非字母数字字符。 保存登录以供以后使用。

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

1. 运行以下命令以创建新的 Azure SQL 数据库逻辑服务器。

    ```azurecli
    az sql server create \
        --name $SERVERNAME \
        --resource-group $RESOURCEGROUP \
        --location $LOCATION \
        --admin-user $ADMINLOGIN \
        --admin-password "$PASSWORD"
    ```

1. 现在, 运行以下各项, 在刚刚创建的逻辑服务器上创建名为**marketplaceDb**的数据库。 这将使用_AdventureWorksLT_数据库作为模板, 因此我们将使用一些预填充表来处理。

    ```azurecli
    az sql db create --resource-group $RESOURCEGROUP \
        --server $SERVERNAME \
        --name marketplaceDb \
        --sample-name AdventureWorksLT \
        --service-objective Basic
    ```

1. 让我们做最后一件事, 并获取此数据库的连接字符串。

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name marketplaceDb --server $SERVERNAME | jq -r
    ```

    您的输出与此类似。 请务必这样做, 你将需要此命令在稍后在本模块中连接到你的数据库。 请注意`<username>`要`<password>`将其替换为您在前面的变量中指定的`ADMINLOGIN`和`PASSWORD`凭据的命令中的和占位符。

    ```output
    sqlcmd -S tcp:server12345.database.windows.net,1433 -d marketplaceDb -U <username> -P <password> -N -l 30
    ```

## <a name="create-and-configure-a-linux-virtual-machine"></a>创建和配置 Linux 虚拟机

现在, 让我们通过一些示例创建要使用的 Linux 虚拟机。

1. 运行以下命令以创建 VM。

    ```azurecli
    az vm create \
      --resource-group $RESOURCEGROUP \
      --name appServer \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --generate-ssh-keys
    ```

1. 成功创建虚拟机后, 通过 SSH 连接到它。

    ```azurecli
    ssh <X.X.X.X>
    ```

    > [!NOTE]
    > 有两个注意事项。 首先, 我们不需要密码, 因为我们生成了一个 SSH 密钥对作为 VM 创建的一部分。 其次, 在将初始命令行管理程序连接到 VM 时, 它会向你提供有关主机的真实性的提示。 这是因为我们要连接的是 IP 地址而不是主机名。 回答 "是" 将把 IP 保存为有效的连接主机, 并允许连接继续进行。

1. 现在, 让我们通过在 Linux VM 上安装 mssql-工具来完成此任务, 以便我们能够通过 sqlcmd 连接到我们的数据库。

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
    > 对于其中一些命令, 会滚动许多文本, 因此请确保在最后一个命令后按 enter, 以确保它能够运行。

我们已创建了 Azure SQL 数据库逻辑服务器、该逻辑服务器上的数据库以及一个名为_appServer_的虚拟机, 我们将使用这些虚拟机模拟来自应用程序服务器的网络连接。 我们来看看如何正确保护我们的数据库。