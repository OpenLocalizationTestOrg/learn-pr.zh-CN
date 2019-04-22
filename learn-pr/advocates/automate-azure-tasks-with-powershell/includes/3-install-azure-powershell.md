假设您已选择 Azure PowerShell 作为自动化解决方案。 您的管理员更愿意在本地运行脚本, 而不是在 Azure 云命令行管理程序中运行。 团队使用运行 Linux、macOS 和 Windows 的计算机。 您需要让 Azure PowerShell 在其所有设备上正常工作。 

## <a name="what-must-be-installed"></a>必须安装哪些内容？
我们将在下一个单元中了解实际安装说明, 但我们来看一下组成 Azure PowerShell 的两个组件。

- **基 PowerShell 产品**这有两种变种: 在 Windows 上为 powershell, 在 macOS 和 Linux 上为 powershell Core。
- **Azure PowerShell 模块**必须安装此额外模块, 才能将特定于 Azure 的命令添加到 PowerShell。

> [!TIP]
> PowerShell 包含在 Windows 中 (但可能有可用的更新)。 你将需要在 Linux 和 macOS 上安装 PowerShell Core。

安装基本产品后, 即可将 Azure PowerShell 模块添加到安装中。

## <a name="how-to-install-powershell-core"></a>如何安装 PowerShell Core
在 Linux 和 macOS 上, 使用程序包管理器安装 PowerShell Core。 建议的程序包管理器因 OS 和分发而异。

> [!NOTE]
> PowerShell Core 在 Microsoft 存储库中可用, 因此你首先需要将该存储库添加到你的程序包管理器。

### <a name="linux"></a>Linux
在 linux 上, 程序包管理器将根据你选择的 Linux 分发进行更改。

| 分发 (s)  | 程序包管理器 |
|------------------|-----------------|
| Ubuntu、Debian   | `apt-get`       |
| Red Hat, CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
在 macOS 上, 您将`Homebrew`使用安装 PowerShell Core。

在下一节中, 您将完成一些常见平台的详细安装步骤。