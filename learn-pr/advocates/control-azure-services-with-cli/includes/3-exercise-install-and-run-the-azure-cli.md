让我们在您的本地计算机上安装 Azure CLI, 然后运行命令来验证您的安装。 您用于安装 Azure CLI 的方法取决于您的计算机的操作系统。 选择适用于您的操作系统的步骤。

> [!NOTE]
> 本练习将指导您在本地安装 Azure CLI 工具。 模块的其余部分将使用 Azure 云命令行管理程序, 以便你可以在 Microsoft 学习中利用免费订阅支持。 您可以将此练习视为可选活动, 只需查看所需的说明即可。

::: zone pivot="linux"

## <a name="linux"></a>Linux

在这里, 你将使用高级打包工具 (**apt.**) 和 Bash 命令行在**Ubuntu Linux**上安装 Azure CLI。

> [!TIP]
> 下面列出的命令适用于 Ubuntu 版本18.04。 其他版本和 linux 的分发有不同的说明。 如果您使用的是其他 Linux 版本, 请查看[官方文档](https://docs.microsoft.com/cli/azure/install-azure-cli)。

1. 修改源列表以注册 Microsoft 存储库, 并且程序包管理器可以找到 Azure CLI 程序包。

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. 导入 Microsoft Ubuntu 存储库的加密密钥。 这将允许程序包管理器验证您安装的 Azure CLI 程序包是否来自 Microsoft。

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. 安装 Azure CLI。

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

::: zone-end

::: zone pivot="macos"

## <a name="macos"></a>macOS

在这里, 将使用 Homebrew 程序包管理器在 macOS 上安装 Azure CLI。

> [!IMPORTANT]
> 如果**brew**命令不可用, 则可能需要安装 Homebrew 程序包管理器。 有关详细信息, 请参阅[Homebrew 网站](https://brew.sh/)。

1. 更新你的 brew 存储库以确保你获取最新的 Azure CLI 程序包。

    ```bash
    brew update
    ```

1. 安装 Azure CLI。

    ```bash
    brew install azure-cli
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a>Windows

在这里, 你将使用 MSI 安装程序在 Windows 上安装 Azure CLI。

1. 转到[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), 并在 "浏览器安全性" 对话框中, 单击 "**运行**"。
1. 在安装程序中, 接受许可条款, 然后单击 "**安装**"。
1. 在 "**用户帐户控制**" 对话框中, 选择 **"是"**。

::: zone-end

## <a name="running-the-azure-cli"></a>运行 Azure CLI

您可以通过打开 bash 命令行管理程序 (Linux 和 macOS) 或命令提示符或 PowerShell (Windows) 来运行 Azure CLI。

1. 启动 Azure CLI, 并通过运行版本检查来验证您的安装。

    ```azurecli
    az --version
    ```

::: zone pivot="windows"

> [!TIP]
> 从 PowerShell 运行 azure cli 与从 Windows 命令提示符运行 azure cli 有一些优势。 PowerShell 通过命令提示符处提供的其他选项卡完成功能。

::: zone-end

你将本地计算机设置为使用 azure CLI 管理 azure 资源。 现在, 您可以在本地使用 Azure CLI 输入命令或执行脚本。 azure CLI 将你的命令转发到 azure 数据中心, 以在 azure 订阅中运行它们。