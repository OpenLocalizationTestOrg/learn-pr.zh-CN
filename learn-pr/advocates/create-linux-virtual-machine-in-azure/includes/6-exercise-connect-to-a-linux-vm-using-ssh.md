让我们使用 SSH 连接到 Linux VM, 并配置 Apache, 因此我们有一个正在运行的 web 服务器。

### <a name="get-the-public-ip-address-of-the-vm"></a>获取 VM 的公共 IP 地址

1. 在[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)中, 确保先前创建的虚拟机的**概述**面板处于打开状态。 如果需要打开 VM, 则可以在 "**所有资源**" 下找到它。 通过概述面板, 可以

    - 查看虚拟机是否正在运行
    - 停止或重新启动 VM
    - 获取 VM 的公共 IP 地址
    - 查看 CPU、磁盘和网络的活动

1. 单击窗格顶部的 "**连接**" 按钮。

1. 在 "**连接到虚拟机**" 面板中, 记下**IP 地址**和**端口号**设置。 在 " **SSH** " 选项卡上, 您还将找到需要在本地执行以连接到 VM 的命令。 将命令复制到剪贴板。

    ![Azure 门户的屏幕截图, 显示已配置为通过 SSH 将连接到新创建的 Linux VM 的虚拟机面板的连接。](../media/5-connect-ssh.png)

## <a name="connect-with-ssh"></a>使用 SSH 进行连接

1. 将您的剪贴板中的命令粘贴到 Azure 云命令行管理程序中。 它应类似于下面的示例内容:但是, 它将具有不同的 IP 地址 (如果您不使用**jim**, 可能也会有不同的用户名!):

    ```bash
    ssh jim@137.117.101.249
    ```

    第一次连接时, SSH 将向我们询问我们如何针对未知主机进行身份验证。 SSH 告诉你之前从未连接到此服务器。 如果是这样, 则它是完全正常的, 您可以通过 **"是"** 进行响应, 以在已知主机文件中保存服务器的指纹:

    ```output
    The authenticity of host '137.117.101.249 (137.117.101.249)' can't be established.
    ECDSA key fingerprint is SHA256:w1h08h4ie1iMq7ibIVSQM/PhcXFV7O7EEhjEqhPYMWY.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added '137.117.101.249' (ECDSA) to the list of known hosts.
    ```

1. 此命令将打开 SSH 连接, 并将您置于 Linux 的命令提示符下。

1. 尝试执行几个 Linux 命令
    - `ls -la /`显示磁盘的根目录
    - `ps -l`显示所有正在运行的进程
    - `dmesg`列出所有内核消息
    - `lsblk`列出所有块设备-你将看到你的驱动器

    在驱动器列表中观察的更有趣的事情是_缺少_的内容。 请注意, **** 我们的数据`sdc`驱动器 () 存在, 但未装入文件系统中。 Azure 添加了一个 VHD, 但未将其初始化。

## <a name="initialize-data-disks"></a>初始化数据磁盘

从头开始创建的任何其他驱动器都需要进行初始化和格式化。 初始化的过程与物理磁盘相同:

1. 首先, 识别磁盘。 我们在上面执行了此操作。 您还可以使用`dmesg | grep SCSI`, 它将列出来自内核的 SCSI 设备的所有邮件。

1. 知道需要初始化的驱动器 (`sdc`) 后, 可以使用`fdisk`执行此操作。 您需要运行命令, `sudo`并提供要分区的磁盘。 我们可以使用以下命令创建新的主分区:

    ```bash
    (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
    ```

1. 接下来, 我们需要使用`mkfs`命令向分区中写入一个文件系统。

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```

1. 最后, 我们需要将驱动器安装到文件系统。 假设我们将拥有一个`data`文件夹。 让我们创建装入点文件夹并装入驱动器。

    ```bash
    sudo mkdir /data & sudo mount /dev/sdc1 /data
    ```

    > [!TIP]
    > 我们已初始化磁盘并已将其装入。 如果你对有关此过程的更多详细信息感兴趣, 请访问**Azure 虚拟机模块中的 "添加" 和 "大小" 磁盘**。 此处更详细地介绍了此任务。

## <a name="install-software-onto-the-vm"></a>将软件安装到 VM

正如你所看到的, SSH 允许你像本地计算机一样使用 Linux 虚拟机。 您可以像管理任何其他 Linux 计算机一样管理此 VM: 安装软件、配置角色、调整功能和其他日常任务。 我们将重点讲述安装软件一段时间。

通过 SSH 连接到 VM 时, 还可以从 internet 安装软件。 默认情况下, Azure 计算机连接到 internet。 您可以使用标准命令直接从标准存储库中安装常用软件包。 让我们使用此方法安装 Apache。

### <a name="install-the-apache-web-server"></a>安装 Apache web 服务器

Apache 在 Ubuntu 的默认软件存储库中可用, 因此我们将使用常规程序包管理工具进行安装:

1. 首先更新本地包索引以反映最新的上游更改:

    ```bash
    sudo apt-get update
    ```

1. 接下来, 安装 Apache:

    ```bash
    sudo apt-get install apache2 -y
    ```

1. 应自动启动, 我们可以使用`systemctl`以下内容检查状态:

    ```bash
    sudo systemctl status apache2 --no-pager
    ```

    该`systemctl`命令将返回类似如下的内容:

    ```output
    apache2.service - The Apache HTTP Server
       Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
      Drop-In: /lib/systemd/system/apache2.service.d
               └─apache2-systemd.conf
       Active: active (running) since Mon 2018-09-03 21:00:03 UTC; 1min 34s ago
     Main PID: 11156 (apache2)
        Tasks: 55 (limit: 4915)
       CGroup: /system.slice/apache2.service
               ├─11156 /usr/sbin/apache2 -k start
               ├─11158 /usr/sbin/apache2 -k start
               └─11159 /usr/sbin/apache2 -k start

    test-web-eus-vm1 systemd[1]: Starting The Apache HTTP Server...
    test-web-eus-vm1 apachectl[11129]: AH00558: apache2: Could not reliably determine the server's fully qua
    test-web-eus-vm1 systemd[1]: Started The Apache HTTP Server.
    ```
    > [!NOTE]
    > 执行类似这样的命令很简单, 但它是一个手动过程-如果我们总是需要安装一些软件, 则可以考虑使用脚本自动执行该过程。

1. 最后, 我们可以尝试通过公共 IP 地址检索默认页面。 但是, 即使 web 服务器在 VM 上运行, 也不会获得有效的连接或响应。 您是否知道为什么要这样做？

我们需要执行更多步骤, 以便能够与 web 服务器进行交互。 我们的虚拟网络阻止入站请求。 我们可以通过配置更改。 接下来, 我们来看一下允许入站请求接下来。