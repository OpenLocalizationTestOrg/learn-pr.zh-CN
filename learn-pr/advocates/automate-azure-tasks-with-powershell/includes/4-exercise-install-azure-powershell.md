在此单元中, 将在本地计算机上安装**PowerShell** 。

> [!NOTE]
> 本练习将指导您完成在本地安装 PowerShell 工具。 模块的其余部分将使用 Azure 云命令行管理程序, 以便你可以在 Microsoft 学习中利用免费订阅支持。 您可以将此练习视为可选活动, 只需查看所需的说明即可。

::: zone pivot="linux"

## <a name="linux"></a>Linux

为 Linux 安装 PowerShell 将涉及使用程序包管理器。 我们将在本示例中使用**Ubuntu 18.04** , 但我们的[文档中有其他版本和分发的详细说明](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)。

您将使用高级打包工具 (**apt.**) 和 Bash 命令行在 Ubuntu Linux 上安装 PowerShell Core。 

1. 导入 Microsoft Ubuntu 存储库的加密密钥。 这将允许程序包管理器验证您安装的 PowerShell 核心包是否来自 Microsoft。

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. 注册**Microsoft Ubuntu 存储库**, 以便程序包管理器可以找到 PowerShell Core 程序包。

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. 更新程序包列表。

    ```bash
    sudo apt-get update
    ```

1. 安装 PowerShell Core。

    ```bash
    sudo apt-get install -y powershell
    ```

1. 启动 PowerShell 以验证它是否已成功安装。

    ```bash
    pwsh
    ```
::: zone-end

::: zone pivot="macos"

## <a name="macos"></a>MacOS

在 macOS 上, 第一步是安装**PowerShell Core**。 这是使用 Homebrew 程序包管理器完成的。

> [!IMPORTANT]
> 如果**brew**命令不可用, 则可能需要安装 Homebrew 程序包管理器。 有关详细信息, 请参阅[Homebrew 网站](https://brew.sh/)。

1. 安装 Homebrew-Cask 以获取更多程序包, 包括 PowerShell Core 程序包:

    ```bash
    brew tap caskroom/cask
    ```

1. 安装 PowerShell Core:

    ```bash
    brew cask install powershell
    ```

1. 启动 PowerShell Core 以验证它是否已成功安装:

    ```bash
    pwsh
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a>Windows
PowerShell 包含在 Windows 中, 但可能存在适用于您的计算机的更新。 我们打算使用的 Azure 支持需要 PowerShell 版本5.0 或更高版本。 您可以通过以下步骤检查已安装的版本:

1. 打开 "**开始**" 菜单并键入**Windows PowerShell**。 可能有多个可用的快捷方式链接:
    - Windows PowerShell-这是64位版本, 通常是应选择的内容。
    - Windows PowerShell (x86)-这是在64位 Windows 上安装的32位版本。
    - Windows PowerShell ISE-集成脚本环境 (ISE) 用于在 PowerShell 中编写脚本。 
    - Windows PowerShell ISE (x86)-32 位版本的 ISE。

1. 选择 "Windows PowerShell" 图标。

1. 键入以下命令, 以确定安装的 PowerShell 版本。

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
如果版本号低于 5.0, 请按照这些说明[升级现有 Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)。

::: zone-end

您已将本地计算机设置为支持 PowerShell。 接下来, 我们将讨论你可以添加的其他命令, 包括 Azure 模块。