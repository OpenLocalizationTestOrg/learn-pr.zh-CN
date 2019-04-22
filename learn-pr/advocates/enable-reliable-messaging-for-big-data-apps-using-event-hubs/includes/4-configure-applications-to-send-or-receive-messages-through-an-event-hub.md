创建并配置事件中心之后, 您需要配置应用程序以发送和接收事件数据流。

例如, 付款处理解决方案将使用某种形式的发件人应用程序收集客户的信用卡数据和收件人应用程序, 以验证信用卡是否有效。

虽然与 .net 应用程序相比, Java 应用程序的配置方式不同, 但有一些一般原则, 可用于使应用程序连接到事件中心并成功发送或接收邮件。 因此, 尽管编辑 Java 配置文本文件的过程与使用 Visual Studio 准备 .net 应用程序的过程不同, 但原则是相同的。

## <a name="what-are-the-minimum-event-hub-application-requirements"></a>事件中心应用程序的最低要求是什么？

若要将应用程序配置为向事件中心发送邮件, 必须提供以下信息, 以便应用程序可以创建连接凭据:

- 事件中心命名空间名称
- 事件中心名称
- 共享访问策略名称
- 主共享访问密钥

若要将应用程序配置为从事件中心接收邮件, 请提供以下信息, 以便应用程序可以创建连接凭据:

- 事件中心命名空间名称
- 事件中心名称
- 共享访问策略名称
- 主共享访问密钥
- 存储帐户名称
- 存储帐户连接字符串
- 存储帐户容器名称

如果您有一个在 Azure Blob 存储中存储邮件的接收器应用程序, 您还需要先配置一个存储帐户。

## <a name="azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a>用于创建常规用途的标准存储帐户的 Azure CLI 命令

Azure CLI 提供了可用于创建和管理存储帐户的一组命令。 我们将在下一个单元中使用它们, 但下面是这些命令的基本概要。 

> [!TIP]
> 在模块简介中, 从**Azure 存储**开始, 有几个 MS 学习模块包含存储帐户。

| 指挥 | 说明 |
|---------|-------------|
| `storage account create` | 创建常规用途的 V2 存储帐户。 |
| `storage account key list` | 检索存储帐户密钥。 |
| `storage account show-connection-string` | 检索 Azure 存储帐户的连接字符串。 |
| `storage container create` | 在存储帐户中创建新容器。 |

## <a name="shell-command-for-cloning-an-application-github-repository"></a>用于克隆 application GitHub 存储库的命令行管理程序命令

Git 是一种协作工具, 它使用分布式版本控制模型, 旨在协作处理软件和文档项目。 git 客户端可用于多个平台 (包括 Windows), 且 git 命令行包含在 Azure Bash 云命令行管理程序中。 GitHub 是用于 Git 存储库的基于 web 的托管服务。 

如果您有一个作为 GitHub 中的项目托管的应用程序, 则可以通过使用**git clone**命令克隆其存储库来创建项目的本地副本。 我们将在下一个单元中执行此操作。

## <a name="editing-files-in-the-cloud-shell"></a>在云命令行管理程序中编辑文件

您可以使用云命令行管理程序中的内置编辑器之一修改组成应用程序的所有文件, 并添加事件中心命名空间、事件中心名称、共享访问策略名称和主键。 

云命令行管理程序支持**nano**、 **vim**和**emacs**以及名为**code**的 Visual Studio 类似代码的编辑器。 只需键入您想要的编辑器的名称, 它就会在环境中启动。 我们将在下一个单元中使用**代码**编辑器。

## <a name="summary"></a>摘要

必须使用有关事件中心环境的特定信息配置发件人和收件人应用程序。 如果您的接收器应用程序将邮件存储在 Blob 存储中, 则可以创建一个存储帐户。 如果您的应用程序托管在 GitHub 上, 则必须将其克隆到本地目录。 文本编辑器 (如**nano** ) 用于将命名空间添加到应用程序中。