azure CLI 是一个命令行程序, 用于连接到 azure 并在 azure 资源上执行管理命令。 它在 Linux、macOS 和 Windows 上运行, 并允许管理员和开发人员通过终端或命令行提示符 (或 script!) 而不是 web 浏览器来执行其命令。 例如, 若要重新启动虚拟机 (VM), 应使用类似如下的命令:

 ```azurecli
 az vm restart -g MyResourceGroup -n MyVm
 ```

azure CLI 提供用于管理 Azure 资源的跨平台命令行工具, 并且可以在 Linux、Mac 或 Windows 计算机上本地安装。 也可以通过 azure 云命令行管理程序在浏览器中使用 azure CLI。 在这两种情况下, 可以交互使用, 也可以编写脚本。 为进行交互式使用, 您首先在 Windows 上或在 Linux 或 macOS 上启动一个命令行管理程序 (如 cmd.exe), 然后在命令行管理程序提示符处发出命令。 若要自动执行重复任务, 请使用所选命令行管理程序的脚本语法将 CLI 命令组合到命令行管理程序脚本中, 然后执行该脚本。

## <a name="how-to-install-the-azure-cli"></a>如何安装 Azure CLI

在 Linux 和 macOS 上, 使用程序包管理器安装 Azure CLI。 建议的程序包管理器因 OS 和分发而异:

- Linux: **apt.-get** Ubuntu、 **yum** on Red Hat 和**zypper** on OpenSUSE
- Mac: **Homebrew**

Azure CLI 在 Microsoft 存储库中可用, 因此你首先需要将该存储库添加到你的程序包管理器。

在 Windows 上, 您可以通过下载并运行 MSI 文件来安装 Azure CLI。

## <a name="using-the-azure-cli-in-scripts"></a>在脚本中使用 Azure CLI

如果要在脚本中使用 Azure CLI 命令, 则需要了解用于运行脚本的 "命令行管理程序" 或环境的任何问题。 例如, 在 bash 命令行管理程序中, 设置变量时将使用以下语法:

```azurecli
variable="value"
variable=integer
```

如果使用 PowerShell 环境运行 Azure CLI 脚本, 则需要对变量使用以下语法:

```powershell
$variable="value"
$variable=integer
```

必须先安装 Azure CLI, 然后才能将其用于管理本地计算机中的 azure 资源。 安装步骤因 Windows、Linux 和 macOS 而异, 但安装后, 这些命令在各个平台之间是常见的。
