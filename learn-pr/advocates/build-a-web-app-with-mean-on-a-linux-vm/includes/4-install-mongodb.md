许多应用程序都需要一个数据库。 在这里, 你将在 "平均" 堆栈中安装 MongoDB ("M")。 它是一个免费且开放源代码的流行的 NoSQL 数据库解决方案。 NoSQL 数据库不需要按照预定义的方式对数据进行结构化, 就像 SQL Server 或 MySQL 这样的关系数据库那样。

MongoDB 将数据存储在类似 JSON 的文档中, 而不需要严格的数据结构。 您使用使用 JavaScript 对象表示法或 JSON 发送的查询和命令与 MongoDB 进行交互。

## <a name="what-mongodb-editions-are-available"></a>哪些 MongoDB 版本可用？

MongoDB 提供了两个版本:

- MongoDB 社区服务器
- MongoDB Enterprise Server

在这里, 你将安装 MongoDB 社区服务器。 稍后, 您将使用 MongoDB 存储书籍的相关信息。

## <a name="how-do-i-install-mongodb"></a>如何安装 MongoDB？

您可以在 Linux、macOS 和 Windows 上安装 MongoDB。 为便于学习, 在这里, 你将使用 ubuntu 的`apt`程序包管理器在 Ubuntu 上安装 MongoDB。

安装过程因操作系统不同而有所不同。 如果你不熟悉 Ubuntu, 你仍然可以继续关注, 以了解如何工作。

稍后, 您可以[查看安装指南](https://docs.mongodb.com/manual/administration/install-community?azure-portal=true)以了解详细信息。

## <a name="install-mongodb"></a>安装 MongoDB

在这里, 你将只使用几个命令安装 MongoDB。 此过程涉及到注册 MongoDB 存储库, `apt`以便能够找到该包。

> [!IMPORTANT]
> 在这里, 你将从 SSH 连接工作到你在上一个设备中创建的 Ubuntu VM。

1. 导入 MongoDB 存储库的加密密钥。 这使程序包管理器能够验证您安装的程序包是否来自 MongoDB inc.。

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    > [!NOTE]
    > `sudo`部件意味着我们希望使用管理权限运行命令。

1. 注册 MongoDB 存储库, 以便包管理器可以找到包, 如下所示。

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. 更新`apt`包数据库, 以便获得最新的包信息。

    ```bash
    sudo apt-get update
    ```

1. 安装 MongoDB 程序包。

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. 启动 MongoDB 服务。

    ```bash
    sudo service mongod start
    ```

1. 运行`mongod --version`以验证安装。

    ```bash
    mongod --version
    ```

将 SSH 连接保持打开状态, 以获取下一部分。