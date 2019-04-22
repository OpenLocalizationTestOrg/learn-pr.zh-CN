若要将 visual studio code 用于 Azure 开发, 需要在本地安装 visual studio code 和一个或多个 azure 扩展。 在本练习中, 我们将添加**Azure 应用服务**扩展。

## <a name="install-visual-studio-code"></a>安装 Visual Studio Code

::: zone pivot="windows"

### <a name="windows"></a>Windows

1. [下载 Visual Studio Code installer for Windows](https://code.visualstudio.com/)。

1. 运行安装程序。

1. 打开 visual studio code, 方法是按 Windows 键或单击任务栏上的 "Windows" 图标, 键入 "visual studio code" 并单击**visual studio code** result。

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a>macOS

1. [下载 macOS 的 Visual Studio Code](https://code.visualstudio.com/)。

1. 双击下载的存档以展开内容。

1. 将 Visual Studio Code. app 拖到应用程序文件夹。

1. 通过单击图标 "应用" 部分或通过在 "聚光灯" 中搜索 Visual studio code 来打开 visual studio code。

::: zone-end

::: zone pivot="linux"

### <a name="linux"></a>Linux 

#### <a name="debian-and-ubuntu"></a>Debian 和 Ubuntu

1. 下载并安装[deb 程序包 (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868) (如果可用) 或通过命令行 (替换为下载的. deb 文件名) 中的图形`<file>`软件中心 (替换为. filename):

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

#### <a name="rhel-fedora-and-centos"></a>RHEL、Fedora 和 CentOS

1. 使用以下脚本安装密钥和存储库:

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. 更新包缓存, 并使用 dnf (Fedora 22 及更高版本) 安装程序包:

    ```bash
    dnf check-update
    sudo dnf install code
    ```

#### <a name="opensuse-and-sle"></a>openSUSE 和 SLE

1. yum 存储库还适用于基于 openSUSE 和 SLE 的系统。 下面的脚本将安装密钥和存储库:

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. 使用以下内容更新包缓存并安装包:

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> 有关在各种 Linux 分发上安装或更新 Visual studio code 的详细信息, 请参阅在[linux 文档中运行 visual studio code](https://code.visualstudio.com/docs/setup/linux)。

::: zone-end

## <a name="install-azure-app-service-extension"></a>安装 Azure 应用服务扩展

1. 如果尚未打开, 请打开 Visual Studio Code。

1. 打开扩展浏览器;它通过左侧的菜单进行访问。

1. 搜索**Azure 应用服务**。

1. 选择 " **Azure 应用服务**结果", 然后单击 "**安装**"。

    下面的屏幕截图显示了从 Visual Studio Code extension 搜索结果中选择的 Azure 应用服务扩展。

    ![显示在搜索结果中突出显示了 Azure 应用服务扩展的 "扩展" 选项卡的 Visual Studio 代码的屏幕截图。](../media/3-install-azure-extension.png)

这将安装扩展。 现已准备好连接到 azure 订阅, 并将 web、移动或 API 应用程序部署到 azure 应用服务。
