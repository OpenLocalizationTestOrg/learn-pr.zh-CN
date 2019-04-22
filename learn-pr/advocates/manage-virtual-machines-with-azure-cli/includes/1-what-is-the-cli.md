it 部门很普遍地管理一组大型 azure 资源-从 azure 虚拟机到托管网站。

虽然 Azure 门户易于用于一次性任务, 但当您必须创建、更改或删除多个操作时, 通过不同的刀片导航可增加时间。 在这种情况下, 命令行非常出色-您可以快速高效地发出命令, 甚至可以使用脚本来运行重复的任务。 使用 azure, 你可以使用两种不同的命令行工具: azure PowerShell 和 azure CLI。

使用上述任一工具, 您都可以编写脚本来检查云服务器的状态、部署新配置、在防火墙中打开端口, 或连接到虚拟机以更改设置。 Windows 管理员倾向于首选 azure PowerShell, 而开发人员和 Linux 管理员通常使用 azure CLI。

本模块将重点介绍如何使用 azure CLI 创建和管理 azure 中托管的虚拟机。 如果你想要了解 azure CLI 的概述、如何安装以及如何使用 azure 订阅, 请确保使用 CLI 培训模块签出**控制 azure 服务**。

## <a name="what-is-the-azure-cli"></a>什么是 Azure CLI？

azure CLI 是 Microsoft 的用于管理 Azure 资源的跨平台命令行工具。 它可用于 macOS、Linux 和 Windows, 也可用于使用[Azure 云命令行](https://docs.microsoft.com/azure/cloud-shell/overview)管理程序的浏览器。

azure CLI 可帮助您从命令行或脚本管理 Azure 资源, 如虚拟机和磁盘。 让我们开始了解如何使用 Azure 虚拟机。

## <a name="learning-objectives"></a>学习目标

在本模块中, 您将:

- 使用 Azure CLI 创建虚拟机
- 使用 Azure CLI 调整虚拟机的大小。
- 使用 Azure CLI 执行基本管理任务。
- 使用 SSH 和 Azure CLI 连接到正在运行的 VM。

## <a name="prerequsites"></a>Prerequsites

- 从**使用 CLI 模块的 azure 服务控制**azure CLI 工具的基本了解。