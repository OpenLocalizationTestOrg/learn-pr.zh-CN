## <a name="allow-azure-service-access"></a>允许 Azure 服务访问

在开始之前, 如果你想要使用 PowerShell 并`psql`连接到你的服务器, 你必须允许访问 Azure 服务。 请记住, 您可以通过两种方式允许访问。

您的第一种方法是启用**允许访问 Azure 服务**。 即使规则未在您创建的自定义规则列表中输入, 允许 access 也会创建防火墙规则。

第二种方法是创建允许访问所有 IP 地址的防火墙规则。 该规则将包含运行 PowerShell 的客户端的 IP 地址, 您将使用这些地址`psql`执行。

此外, 还需要禁用**强制 SSL 连接**选项。

### <a name="create-a-firewall-rule"></a>创建防火墙规则

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 导航到您要为其创建防火墙规则的服务器资源。

1. 选择 "**连接安全性**" 选项, 打开右侧的 "连接安全" 边栏。

    ![显示 PostgreSQL 数据库资源边栏的 "连接安全" 部分的 Azure 门户屏幕截图](../media/6-db-security-settings.png)

请记住, 您希望允许对运行`psql`的 PowerShell 客户端进行访问。

您可以选择执行以下操作之一:

- 将 "**允许访问 Azure 服务**" 设置为 **"打开"**
- 将 "**强制 SSL 连接**" 设置为 "**已禁用**"
- 单击 "**保存**" 按钮以保存所做的更改

或者, 您可以添加防火墙规则, 以允许通过添加防火墙规则访问所有 IP 地址。 使用以下值:

- 规则名称:`AllowAll`
- 起始 IP:`0.0.0.0`
- 结束 IP:`255.255.255.255`
- 将 "**强制 SSL 连接**" 设置为 "**已禁用**"
- 单击 "**保存**" 按钮以保存所做的更改

> [!Warning]
> 创建此防火墙规则将允许 Internet 上的任何 IP 地址尝试连接到您的服务器。 在生产环境中, 您需要限制对特定 IP 地址的访问。

### <a name="connect-to-the-database-with-psql"></a>使用 psql 连接到数据库

1. 在右侧的 Azure 云命令行管理程序中`psql` , 使用以下命令连接到您的服务器。 请务必替换服务器名称和管理员名称。

    ```bash
    psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
    ```

    使用为、和`server-name` `admin-user`的选择的值。

1. **postgres**是使用创建的每个 PostgreSQL 服务器的默认管理数据库。 系统将提示你输入创建服务器时提供的密码。

1. 成功连接后, 执行`\l`命令以列出所有数据库。 此命令将导致返回两个或更多的默认数据库。

1. 按`q` "退出列表"。

1. 使用以下 SQL 命令创建新数据库:

    ```sql
    CREATE DATABASE "Adventureworks";
    ```

1. 运行 psql 命令`\c Adventureworks`以连接到数据库。

1. 使用以下 SQL 命令向数据库添加一些数据, 以将数据添加到两个表中:

    ```sql
    CREATE TABLE PEOPLE(NAME TEXT NOT NULL, AGE INT NOT NULL);
    INSERT INTO PEOPLE(NAME, AGE) VALUES ('Bob', 35);
    INSERT INTO PEOPLE(NAME, AGE) VALUES ('Sarah', 28);
    CREATE TABLE LOCATIONS(CITY TEXT NOT NULL, STATE TEXT NOT NULL);
    INSERT INTO LOCATIONS(CITY, STATE) VALUES ('New York', 'NY');
    INSERT INTO LOCATIONS(CITY, STATE) VALUES ('Flint', 'MI');
    ```

1. 使用以下 SQL 命令检索添加的数据:

    ```sql
    SELECT * FROM PEOPLE;
    SELECT * FROM LOCATIONS;
    ```

1. 您可以尝试其他 psql 命令。
    - `-?`获取帮助。
    - `\dt`列出表。

1. 在服务器上执行完 psql 操作后, 请执行命令`\q`以退出 psql。
