在将数据库连接到您的应用程序之前, 您需要检查您是否可以连接到它, 添加一个基本表, 并使用示例数据。

我们维护 Azure SQL 数据库的基础结构、软件更新和修补程序。 此外, 您还可以像对待任何其他 SQL Server 安装那样对待您的 Azure SQL 数据库。 例如, 您可以使用 Visual studio、SQL Server Management Studio、Azure Data Studio 或其他工具来管理 Azure SQL 数据库。

您如何访问数据库并将其连接到您的应用程序。 但是, 若要获得一些使用数据库的经验, 可直接从门户连接到它, 创建一个表, 并运行几个基本的 CRUD 操作。 你将了解:

- 什么是云命令行管理程序, 以及如何从门户访问它。
- 如何从 Azure CLI 访问有关数据库的信息, 包括连接字符串。
- 如何使用`sqlcmd`连接到您的数据库。
- 如何使用基本表和一些示例数据初始化数据库。

## <a name="what-is-azure-cloud-shell"></a>什么是 Azure 云命令行管理程序？

azure 云命令行管理程序是用于管理和开发 Azure 资源的基于浏览器的命令行管理程序体验。 将云命令行管理程序视为一个在云中运行的交互控制台。

在幕后, 云命令行管理程序在 Linux 上运行。 但根据您是否喜欢 Linux 或 Windows 环境, 您有两种体验可供选择: Bash 和 PowerShell。

可以从任何位置访问云命令行管理程序。 除了门户之外, 您还可以从[shell.azure.com](https://shell.azure.com/)、azure 移动应用或 Visual Studio Code 中访问云命令行管理程序。 右侧的面板是云命令行管理程序终端, 可供您在本练习中使用。

云命令行管理程序包含流行工具和文本编辑器。 下面简要介绍`az` `jq`了、和`sqlcmd`, 将用于当前任务的三个工具。

- `az`也称为 Azure CLI。 它是用于使用 Azure 资源的命令行界面。 您将使用此信息获取有关您的数据库的信息, 包括连接字符串。
- `jq`是命令行 JSON 分析器。 您将从`az`命令到此工具的管道输出, 以从 JSON 输出中提取重要字段。
- `sqlcmd`使您能够在 SQL Server 上执行语句。 你将使用`sqlcmd` Azure SQL 数据库创建交互式会话。

## <a name="get-information-about-your-azure-sql-database"></a>获取有关 Azure SQL 数据库的信息

在连接到数据库之前, 最好先验证它是否存在并处于联机状态。

在这里, 使用该`az`实用工具列出数据库, 并显示有关**后勤**数据库的一些信息, 包括其最大大小和状态。

1. 您`az`要运行的命令需要资源组的名称和 Azure SQL 逻辑服务器的名称。 若要保存键入, 请`azure configure`运行此命令以将其指定为默认值。
    将`<server-name>`替换为 Azure SQL 逻辑服务器的名称。 请注意, 根据您在门户中所处的刀片式服务器, 这可能显示为 FQDN (servername.database.windows.net), 但您只需要一个不带. database.windows.net 后缀的逻辑名称。

    ```azurecli
    az configure --defaults group=<rgn>[sandbox resource group name]</rgn> sql-server=<server-name>
    ```

1. 运行`az sql db list`以列出 Azure SQL 逻辑服务器上的所有数据库。

    ```azurecli
    az sql db list
    ```
    您看到的 JSON 块是一个大的输出块。

1. 由于我们只需要数据库名称, 第二次运行该命令。 这次, 将输出管道传输`jq`到仅打印名称字段。
   
     ```azurecli
    az sql db list | jq '[.[] | {name: .name}]'
    ```
    
    您应该会看到此输出。
    
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

    **后勤**是您的数据库。 与 SQL Server 一样, **master**包括服务器元数据, 例如登录帐户和系统配置设置。

1. 运行此`az sql db show`命令可获取有关**后勤**数据库的详细信息。

    ```azurecli
    az sql db show --name Logistics
    ```

    如前所述, 您会看到一个 JSON 作为输出的大块。

1. 第二次运行该命令。 这次, 将输出管道传输`jq`到, 以将输出限制为仅为**物流**数据库的名称、最大大小和状态。

    ```azurecli
    az sql db show --name Logistics | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
    ```

    您会发现数据库处于联机状态, 并且可以容纳大约 2 GB 的数据。

    ```json
    {
      "name": "Logistics",
      "maxSizeBytes": 2147483648,
      "status": "Online"
    }
    ```

## <a name="connect-to-your-database"></a>连接到您的数据库

现在您已经了解了有关数据库的几点, 让我们使用`sqlcmd`创建一个表, 其中包含有关运输驱动因素的信息, 并执行几个基本的 CRUD 操作。

请注意, CRUD 代表 "**创建**"、"**读取**"、"**更新**" 和 "**删除**"。 这些术语指的是对表数据执行的操作, 并且是应用所需的四个基本操作。 现在我们来验证你是否可以执行每个工作。

1. 运行此`az sql db show-connection-string`命令, 以`sqlcmd`可使用的格式获取**后勤**数据库的连接字符串。

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name Logistics
    ```

    您的输出与此类似。

    ```output
    "sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U <username> -P <password> -N -l 30"
    ```

1. 运行上`sqlcmd`一步的输出中的语句以创建交互式会话。 删除周围的引号, 并`<username>`将`<password>`其替换为您在创建数据库时指定的用户名和密码。 下面是一个示例。

    ```console
    sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U martina -P "password1234$" -N -l 30
    ```

    > [!TIP]
    > 将密码放在引号中, 以便 "&" 和其他特殊字符不会解释为处理指令。

1. 在`sqlcmd`会话中, 创建一个名为`Drivers`的表。

    ```sql
    CREATE TABLE Drivers (DriverID int, LastName varchar(255), FirstName varchar(255), OriginCity varchar(255));
    GO
    ```

    该表包含四列: 唯一标识符、驱动程序的姓氏和名字以及驱动程序的源城市。

    > [!NOTE]
    > 您在此处看到的语言是 transact-sql 或 t-sql。

1. 验证`Drivers`表是否存在。

    ```sql
    SELECT name FROM sys.tables;
    GO
    ```

    您应该会看到此输出。

    ```output
    name
    --------------------------------------------------------------------------------------------------------------------------------
    Drivers

    (1 rows affected)
    ```

1. 运行此`INSERT` t-sql 语句以向表中添加示例行。 这是**创建**操作。

    ```sql
    INSERT INTO Drivers (DriverID, LastName, FirstName, OriginCity) VALUES (123, 'Zirne', 'Laura', 'Springfield');
    GO
    ```

    你会看到此指示操作已成功。

    ```output
    (1 rows affected)
    ```

1. 运行此`SELECT` t-sql 语句以列出表中所有`DriverID`行`OriginCity`的和列。 这是**读取**操作。

    ```sql
    SELECT DriverID, OriginCity FROM Drivers;
    GO
    ```

    你将看到在上一`DriverID`步`OriginCity`中创建的行与和对应的一个结果。

    ```output
    DriverID    OriginCity
    ----------- --------------------------
            123 Springfield

    (1 rows affected)
    ```

1. 运行此`UPDATE` t-sql 语句可将驱动程序的 "Springfield" 的 "源城市" 更改为 123 `DriverID`的驱动程序的 "波士顿"。 这是**更新**操作。

    ```sql
    UPDATE Drivers SET OriginCity='Boston' WHERE DriverID=123;
    GO
    SELECT DriverID, OriginCity FROM Drivers;
    GO
    ```

    您应该会看到以下输出。 请注意, `OriginCity`如何反映对波士顿的更新。

    ```output
    DriverID    OriginCity
    ----------- --------------------------
            123 Boston

    (1 rows affected)
    ```

1. 运行此`DELETE` t-sql 语句以删除记录。 这是**删除**操作。

    ```sql
    DELETE FROM Drivers WHERE DriverID=123;
    GO
    ```

    ```output
    (1 rows affected)
    ```

1. 运行此`SELECT` t-sql 语句以验证`Drivers`表是否为空。

    ```sql
    SELECT COUNT(*) FROM Drivers;
    GO
    ```

    您会发现该表不包含任何行。

    ```output
    -----------
              0

    (1 rows affected)
    ```

现在, 您已从云命令行管理程序使用了 Azure SQL 数据库, 您可以获取最喜爱的 sql 管理工具&ndash;的连接字符串, 而不管它是来自 SQL Server management Studio、Visual studio 还是其他内容。

云命令行管理程序使您可以轻松地访问和使用 Azure 资源。 由于云命令行管理程序是基于浏览器的, 因此可以从 Windows、macOS 或&ndash; Linux 中通过 web 浏览器的任何系统访问该命令行管理程序。

你获得了一些运行 azure CLI 命令的实践经验, 以获取有关 Azure SQL 数据库的信息。 作为一项奖金, 你为你的 T-SQL 技能做了练习。

最后, 让我们总结并了解如何拉出您的数据库。
