在这里, 将安装 node.js, 即表示首字母缩写词中的**N** 。 与 MongoDB 一样, node.js 是开放源代码。 

node.js 将充当 web 应用程序的服务器端主机, 并处理入站 HTTP 流量。 node.js 还提供了一种与 MongoDB 安装进行通信的方法, 稍后将会看到。

## <a name="what-versions-of-nodejs-are-available"></a>有哪些版本的 node.js？

可以通过两种方式获取 node.js:

- 长期**支持 (LTS)** -LTS 通常被视为更稳定, 建议用于大多数用户和生产环境。
- **current**适用于那些想要试用最新功能的人员。 由于它可能会导致发布之间发生重大更改, 因此不建议在生产环境中进行更改。

在这里, 你将使用 node.js LTS。

## <a name="how-do-i-install-nodejs"></a>如何安装 node.js？

与 MongoDB 一样, 您可以在 Windows、macOS 和 Linux 上运行 node.js。 node.js 还支持基于 Unix 的操作系统, 如 SunOS 和 AIX。

就像 MongoDB 一样, 你将注册 node.js 存储库, 以便`apt`能够找到该包。

回想一下你正在使用 Ubuntu VM。 稍后, 您可以[查看安装指南](https://nodejs.org/en/download/package-manager?azure-portal=true), 了解如何在你喜爱的平台上安装 node.js。

## <a name="install-nodejs"></a>安装 node.js

在这里, 将安装 node.js。 与 MongoDB 一样, 此过程涉及注册 node.js 存储库, 以便`apt`能够查找该包。

> [!IMPORTANT]
> 在这里, 你将从 SSH 连接工作到你在本模块前面创建的 Ubuntu VM。

1. 注册 node.js 存储库, 以便程序包管理器可以找到程序包, 如下所示。

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. 安装 node.js 包。

    ```bash
    sudo apt-get install -y Node.js
    ```

1. 运行`node -v`以验证安装。

    ```bash
    node -v
    ```

    输出显示, 您具有 node.js 的最新 LTS 版本。

## <a name="exit-your-ssh-session"></a>退出 SSH 会话

你现在已经在 VM 上直接完成了操作。 运行`exit`以将 SSH 会话保留到 VM。

```bash
exit
```

你现在将回到云 Shell 会话。