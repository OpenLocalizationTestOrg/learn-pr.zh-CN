<span data-ttu-id="a5531-101">让我们使用 SSH 连接到 Linux VM, 并配置 Apache, 因此我们有一个正在运行的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="a5531-101">Let's connect to our Linux VM with SSH, and configure Apache, so we have a running web server.</span></span>

### <a name="get-the-public-ip-address-of-the-vm"></a><span data-ttu-id="a5531-102">获取 VM 的公共 IP 地址</span><span class="sxs-lookup"><span data-stu-id="a5531-102">Get the public IP address of the VM</span></span>

1. <span data-ttu-id="a5531-103">在[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)中, 确保先前创建的虚拟机的**概述**面板处于打开状态。</span><span class="sxs-lookup"><span data-stu-id="a5531-103">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="a5531-104">如果需要打开 VM, 则可以在 "**所有资源**" 下找到它。</span><span class="sxs-lookup"><span data-stu-id="a5531-104">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="a5531-105">通过概述面板, 可以</span><span class="sxs-lookup"><span data-stu-id="a5531-105">The overview panel allows you to</span></span>

    - <span data-ttu-id="a5531-106">查看虚拟机是否正在运行</span><span class="sxs-lookup"><span data-stu-id="a5531-106">See if the VM is running</span></span>
    - <span data-ttu-id="a5531-107">停止或重新启动 VM</span><span class="sxs-lookup"><span data-stu-id="a5531-107">Stop or restart the VM</span></span>
    - <span data-ttu-id="a5531-108">获取 VM 的公共 IP 地址</span><span class="sxs-lookup"><span data-stu-id="a5531-108">Get the public IP address of the VM</span></span>
    - <span data-ttu-id="a5531-109">查看 CPU、磁盘和网络的活动</span><span class="sxs-lookup"><span data-stu-id="a5531-109">See the activity of the CPU, disk, and network</span></span>

1. <span data-ttu-id="a5531-110">单击窗格顶部的 "**连接**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="a5531-110">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="a5531-111">在 "**连接到虚拟机**" 面板中, 记下**IP 地址**和**端口号**设置。</span><span class="sxs-lookup"><span data-stu-id="a5531-111">In the **Connect to virtual machine** panel, note the **IP address** and **Port number** settings.</span></span> <span data-ttu-id="a5531-112">在 " **SSH** " 选项卡上, 您还将找到需要在本地执行以连接到 VM 的命令。</span><span class="sxs-lookup"><span data-stu-id="a5531-112">On the **SSH** tab, you will also find the command you need to execute locally to connect to the VM.</span></span> <span data-ttu-id="a5531-113">将命令复制到剪贴板。</span><span class="sxs-lookup"><span data-stu-id="a5531-113">Copy the command to the clipboard.</span></span>

    ![Azure 门户的屏幕截图, 显示已配置为通过 SSH 将连接到新创建的 Linux VM 的虚拟机面板的连接。](../media/5-connect-ssh.png)

## <a name="connect-with-ssh"></a><span data-ttu-id="a5531-115">使用 SSH 进行连接</span><span class="sxs-lookup"><span data-stu-id="a5531-115">Connect with SSH</span></span>

1. <span data-ttu-id="a5531-116">将您的剪贴板中的命令粘贴到 Azure 云命令行管理程序中。</span><span class="sxs-lookup"><span data-stu-id="a5531-116">Paste the command from your clipboard into the Azure Cloud Shell.</span></span> <span data-ttu-id="a5531-117">它应类似于下面的示例内容:但是, 它将具有不同的 IP 地址 (如果您不使用**jim**, 可能也会有不同的用户名!):</span><span class="sxs-lookup"><span data-stu-id="a5531-117">It should look something like the sample below; however, it will have a different IP address (and perhaps a different username if you didn't use **jim**!):</span></span>

    ```bash
    ssh jim@137.117.101.249
    ```

    <span data-ttu-id="a5531-118">第一次连接时, SSH 将向我们询问我们如何针对未知主机进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a5531-118">The first time we connect, SSH will ask us about authenticating against an unknown host.</span></span> <span data-ttu-id="a5531-119">SSH 告诉你之前从未连接到此服务器。</span><span class="sxs-lookup"><span data-stu-id="a5531-119">SSH is telling you that you've never connected to this server before.</span></span> <span data-ttu-id="a5531-120">如果是这样, 则它是完全正常的, 您可以通过 **"是"** 进行响应, 以在已知主机文件中保存服务器的指纹:</span><span class="sxs-lookup"><span data-stu-id="a5531-120">If that's true, then it's perfectly normal, and you can respond with **yes** to save the fingerprint of the server in the known host file:</span></span>

    ```output
    The authenticity of host '137.117.101.249 (137.117.101.249)' can't be established.
    ECDSA key fingerprint is SHA256:w1h08h4ie1iMq7ibIVSQM/PhcXFV7O7EEhjEqhPYMWY.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added '137.117.101.249' (ECDSA) to the list of known hosts.
    ```

1. <span data-ttu-id="a5531-121">此命令将打开 SSH 连接, 并将您置于 Linux 的命令提示符下。</span><span class="sxs-lookup"><span data-stu-id="a5531-121">This command will open an SSH connection and place you at a shell command prompt for Linux.</span></span>

1. <span data-ttu-id="a5531-122">尝试执行几个 Linux 命令</span><span class="sxs-lookup"><span data-stu-id="a5531-122">Try executing a few Linux commands</span></span>
    - <span data-ttu-id="a5531-123">`ls -la /`显示磁盘的根目录</span><span class="sxs-lookup"><span data-stu-id="a5531-123">`ls -la /` to show the root of the disk</span></span>
    - <span data-ttu-id="a5531-124">`ps -l`显示所有正在运行的进程</span><span class="sxs-lookup"><span data-stu-id="a5531-124">`ps -l` to show all the running processes</span></span>
    - <span data-ttu-id="a5531-125">`dmesg`列出所有内核消息</span><span class="sxs-lookup"><span data-stu-id="a5531-125">`dmesg` to list all the kernel messages</span></span>
    - <span data-ttu-id="a5531-126">`lsblk`列出所有块设备-你将看到你的驱动器</span><span class="sxs-lookup"><span data-stu-id="a5531-126">`lsblk` to list all the block devices - here you will see your drives</span></span>

    <span data-ttu-id="a5531-127">在驱动器列表中观察的更有趣的事情是_缺少_的内容。</span><span class="sxs-lookup"><span data-stu-id="a5531-127">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="a5531-128">请注意, \*\*\*\* 我们的数据`sdc`驱动器 () 存在, 但未装入文件系统中。</span><span class="sxs-lookup"><span data-stu-id="a5531-128">Notice that our **Data** drive (`sdc`) is present but not mounted into the file system.</span></span> <span data-ttu-id="a5531-129">Azure 添加了一个 VHD, 但未将其初始化。</span><span class="sxs-lookup"><span data-stu-id="a5531-129">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="a5531-130">初始化数据磁盘</span><span class="sxs-lookup"><span data-stu-id="a5531-130">Initialize data disks</span></span>

<span data-ttu-id="a5531-131">从头开始创建的任何其他驱动器都需要进行初始化和格式化。</span><span class="sxs-lookup"><span data-stu-id="a5531-131">Any additional drives you create from scratch need to be initialized and formatted.</span></span> <span data-ttu-id="a5531-132">初始化的过程与物理磁盘相同:</span><span class="sxs-lookup"><span data-stu-id="a5531-132">The process for initializing is identical to a physical disk:</span></span>

1. <span data-ttu-id="a5531-133">首先, 识别磁盘。</span><span class="sxs-lookup"><span data-stu-id="a5531-133">First, identify the disk.</span></span> <span data-ttu-id="a5531-134">我们在上面执行了此操作。</span><span class="sxs-lookup"><span data-stu-id="a5531-134">We did that above.</span></span> <span data-ttu-id="a5531-135">您还可以使用`dmesg | grep SCSI`, 它将列出来自内核的 SCSI 设备的所有邮件。</span><span class="sxs-lookup"><span data-stu-id="a5531-135">You could also use `dmesg | grep SCSI`, which will list all the messages from the kernel for SCSI devices.</span></span>

1. <span data-ttu-id="a5531-136">知道需要初始化的驱动器 (`sdc`) 后, 可以使用`fdisk`执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a5531-136">Once you know the drive (`sdc`) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="a5531-137">您需要运行命令, `sudo`并提供要分区的磁盘。</span><span class="sxs-lookup"><span data-stu-id="a5531-137">You will need to run the command with `sudo` and supply the disk you want to partition.</span></span> <span data-ttu-id="a5531-138">我们可以使用以下命令创建新的主分区:</span><span class="sxs-lookup"><span data-stu-id="a5531-138">We can use the following command to create a new primary partition:</span></span>

    ```bash
    (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
    ```

1. <span data-ttu-id="a5531-139">接下来, 我们需要使用`mkfs`命令向分区中写入一个文件系统。</span><span class="sxs-lookup"><span data-stu-id="a5531-139">Next, we need to write a file system to the partition with the `mkfs` command.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```

1. <span data-ttu-id="a5531-140">最后, 我们需要将驱动器安装到文件系统。</span><span class="sxs-lookup"><span data-stu-id="a5531-140">Finally, we need to mount the drive to the file system.</span></span> <span data-ttu-id="a5531-141">假设我们将拥有一个`data`文件夹。</span><span class="sxs-lookup"><span data-stu-id="a5531-141">Let's assume we will have a `data` folder.</span></span> <span data-ttu-id="a5531-142">让我们创建装入点文件夹并装入驱动器。</span><span class="sxs-lookup"><span data-stu-id="a5531-142">Let's create the mount point folder and mount the drive.</span></span>

    ```bash
    sudo mkdir /data & sudo mount /dev/sdc1 /data
    ```

    > [!TIP]
    > <span data-ttu-id="a5531-143">我们已初始化磁盘并已将其装入。</span><span class="sxs-lookup"><span data-stu-id="a5531-143">We initialized the disk and mounted it.</span></span> <span data-ttu-id="a5531-144">如果你对有关此过程的更多详细信息感兴趣, 请访问**Azure 虚拟机模块中的 "添加" 和 "大小" 磁盘**。</span><span class="sxs-lookup"><span data-stu-id="a5531-144">If you are interested in more details on this process go through the **Add and size disks in Azure virtual machines** module.</span></span> <span data-ttu-id="a5531-145">此处更详细地介绍了此任务。</span><span class="sxs-lookup"><span data-stu-id="a5531-145">This task is covered in more detail there.</span></span>

## <a name="install-software-onto-the-vm"></a><span data-ttu-id="a5531-146">将软件安装到 VM</span><span class="sxs-lookup"><span data-stu-id="a5531-146">Install software onto the VM</span></span>

<span data-ttu-id="a5531-147">正如你所看到的, SSH 允许你像本地计算机一样使用 Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="a5531-147">As you can see, SSH allows you to work with the Linux VM just like a local computer.</span></span> <span data-ttu-id="a5531-148">您可以像管理任何其他 Linux 计算机一样管理此 VM: 安装软件、配置角色、调整功能和其他日常任务。</span><span class="sxs-lookup"><span data-stu-id="a5531-148">You can administer this VM as you would any other Linux computer: installing software, configuring roles, adjusting features, and other everyday tasks.</span></span> <span data-ttu-id="a5531-149">我们将重点讲述安装软件一段时间。</span><span class="sxs-lookup"><span data-stu-id="a5531-149">Let's focus on installing software for a moment.</span></span>

<span data-ttu-id="a5531-150">通过 SSH 连接到 VM 时, 还可以从 internet 安装软件。</span><span class="sxs-lookup"><span data-stu-id="a5531-150">You can also install software from the internet when you are connected to the VM via SSH.</span></span> <span data-ttu-id="a5531-151">默认情况下, Azure 计算机连接到 internet。</span><span class="sxs-lookup"><span data-stu-id="a5531-151">Azure machines are, by default, internet connected.</span></span> <span data-ttu-id="a5531-152">您可以使用标准命令直接从标准存储库中安装常用软件包。</span><span class="sxs-lookup"><span data-stu-id="a5531-152">You can use standard commands to install popular software packages directly from standard repositories.</span></span> <span data-ttu-id="a5531-153">让我们使用此方法安装 Apache。</span><span class="sxs-lookup"><span data-stu-id="a5531-153">Let's use this approach to install Apache.</span></span>

### <a name="install-the-apache-web-server"></a><span data-ttu-id="a5531-154">安装 Apache web 服务器</span><span class="sxs-lookup"><span data-stu-id="a5531-154">Install the Apache web server</span></span>

<span data-ttu-id="a5531-155">Apache 在 Ubuntu 的默认软件存储库中可用, 因此我们将使用常规程序包管理工具进行安装:</span><span class="sxs-lookup"><span data-stu-id="a5531-155">Apache is available within Ubuntu's default software repositories, so we will install it using conventional package management tools:</span></span>

1. <span data-ttu-id="a5531-156">首先更新本地包索引以反映最新的上游更改:</span><span class="sxs-lookup"><span data-stu-id="a5531-156">Start by updating the local package index to reflect the latest upstream changes:</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="a5531-157">接下来, 安装 Apache:</span><span class="sxs-lookup"><span data-stu-id="a5531-157">Next, install Apache:</span></span>

    ```bash
    sudo apt-get install apache2 -y
    ```

1. <span data-ttu-id="a5531-158">应自动启动, 我们可以使用`systemctl`以下内容检查状态:</span><span class="sxs-lookup"><span data-stu-id="a5531-158">It should start automatically - we can check the status using `systemctl`:</span></span>

    ```bash
    sudo systemctl status apache2 --no-pager
    ```

    <span data-ttu-id="a5531-159">该`systemctl`命令将返回类似如下的内容:</span><span class="sxs-lookup"><span data-stu-id="a5531-159">The `systemctl` command returns something like:</span></span>

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
    > <span data-ttu-id="a5531-160">执行类似这样的命令很简单, 但它是一个手动过程-如果我们总是需要安装一些软件, 则可以考虑使用脚本自动执行该过程。</span><span class="sxs-lookup"><span data-stu-id="a5531-160">It's trivial to execute commands like this, however it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>

1. <span data-ttu-id="a5531-161">最后, 我们可以尝试通过公共 IP 地址检索默认页面。</span><span class="sxs-lookup"><span data-stu-id="a5531-161">Finally, we can try retrieving the default page through the public IP address.</span></span> <span data-ttu-id="a5531-162">但是, 即使 web 服务器在 VM 上运行, 也不会获得有效的连接或响应。</span><span class="sxs-lookup"><span data-stu-id="a5531-162">However, even though the web server is running on the VM, you won't get a valid connection or response.</span></span> <span data-ttu-id="a5531-163">您是否知道为什么要这样做？</span><span class="sxs-lookup"><span data-stu-id="a5531-163">Do you know why?</span></span>

<span data-ttu-id="a5531-164">我们需要执行更多步骤, 以便能够与 web 服务器进行交互。</span><span class="sxs-lookup"><span data-stu-id="a5531-164">We need to perform one more step to be able to interact with the web server.</span></span> <span data-ttu-id="a5531-165">我们的虚拟网络阻止入站请求。</span><span class="sxs-lookup"><span data-stu-id="a5531-165">Our virtual network is blocking the inbound request.</span></span> <span data-ttu-id="a5531-166">我们可以通过配置更改。</span><span class="sxs-lookup"><span data-stu-id="a5531-166">We can change that through configuration.</span></span> <span data-ttu-id="a5531-167">接下来, 我们来看一下允许入站请求接下来。</span><span class="sxs-lookup"><span data-stu-id="a5531-167">Let's look at allowing the inbound request next.</span></span>