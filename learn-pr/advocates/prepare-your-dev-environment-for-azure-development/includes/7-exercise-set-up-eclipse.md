在这里, 你将在开发计算机上安装 Eclipse 和 Azure 工具包。 在练习的最后, 你将拥有创建连接到 Azure 的 Java 应用程序所需的一切。

## <a name="install-eclipse-ide"></a>安装日蚀式 IDE

1. 下载适用[于您的操作系统的 Eclipse IDE](https://www.eclipse.org/downloads/packages/installer)。

1. 下载 Eclipse 安装程序后启动。

    1. 在 Windows 上, 双击下载的文件。

    1. 在 macOS 和 Linux 上, 从下载的文件中解压缩安装程序并运行它。

        > [!NOTE]
        > 如果缺少 Java 开发工具包, 安装程序可能会提示您安装它。

1. 选择要安装的程序包。 对于 java 开发人员, 选择 java 或 java EE 日蚀式 IDE 选项。

1. 选择您的计算机上的安装目标。

1. 启动 Eclipse 以验证它是否已正确安装。

## <a name="install-azure-toolkit-for-eclipse"></a>为 Eclipse 安装 Azure 工具包

安装 Azure 工具包在 Windows、macOS 和 Linux 中是相同的。

1. 启动 Eclipse。

1. 转到 "**帮助** > **安装新软件 ...**"。

    下面的屏幕截图显示了 "**安装新软件 ...** " 项的菜单位置。

    ![在日蚀的帮助菜单中突出显示了 "安装新软件" 选项的屏幕截图。](../media/7-eclipse-install-new-software.png)

1. 将会打开 "**可用软件**" 对话框。 在 "**工作方式:** " 文本框中, `http://dl.microsoft.com/eclipse/`键入, 然后按 enter。

1. 在结果中, 查看 "**适用于 Java 的 Azure 工具包**" 选项。 确保在 "**安装过程中对所有更新网站进行更新以查找所需的软件**" 选项 (如果尚未选中)。

    下面的屏幕截图显示了**可用的软件**安装配置, 如上文所述。

    ![Eclipse 中的 "可用软件" 窗口的屏幕截图, 框突出显示了查找和安装适用于 Java 的 Azure 工具包所需的配置。](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. 单击"下一步"。

1. 在收到提示时查看并接受许可协议, 然后单击 "**完成**"。

1. 日蚀将下载并安装 Azure 工具包。

1. 如果需要, 请重新启动 Eclipse。

1. 验证是否可以在 Eclipse 中找到**** > "**azure** " 菜单选项来验证 azure 工具包的安装。
