创建管理脚本是优化工作流的一种有效方式。 您可以自动执行常见的重复性任务, 一旦脚本经过验证, 它将持续运行, 很可能会减少错误。

假设您在使用 Azure 虚拟机 (vm) 测试客户关系管理 (CRM) 软件的公司工作。 vm 是从包含 web 前端的映像、实现业务逻辑的 web 服务和 SQL 数据库构建而成。

您在单个 VM 上执行了多次测试, 但发现数据库和配置文件中的更改可能会导致不一致的结果。 在一种情况下, bug 在数据库中创建了没有对应客户的电话呼叫记录。 即使在修复了 bug 之后, 孤立记录也会导致后续集成测试失败。 您计划通过对每个测试周期使用全新的 VM 部署来解决此问题。 您希望自动执行 VM 创建安装程序, 因为它将每周执行多次。 

在这里, 你将了解如何使用 azure PowerShell 管理 azure 资源。 您将使用 Azure PowerShell 以交互方式执行一次性任务, 并编写脚本以自动执行重复任务。 

## <a name="learning-objectives"></a>学习目标
在本模块中, 您将:

- 确定 azure PowerShell 是否为你的 azure 管理任务的正确工具
- 在 Linux、macOS 和/或 Windows 上安装 Azure PowerShell
- 使用 azure PowerShell 连接到 azure 订阅
- 使用 azure PowerShell 创建 Azure 资源

## <a name="prerequisites"></a>先决条件

- 使用命令行界面 (如 PowerShell 或 Bash) 的体验
- 基本 Azure 概念 (例如资源组和虚拟机) 的知识
- 使用 azure 门户管理 azure 资源的体验
