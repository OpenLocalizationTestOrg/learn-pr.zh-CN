<span data-ttu-id="b92f6-101">您的法律公司正在扩展其事例负载, 并且您已完成创建新的 Linux web 服务器以存储来自各种源 (客户端、其他法律公司和执法机构) 的关键文档的任务。</span><span class="sxs-lookup"><span data-stu-id="b92f6-101">Your law firm is expanding its case load and you have been tasked with creating a new Linux web server to store critical documents from a variety of sources - clients, other law firms, and law enforcement offices.</span></span> <span data-ttu-id="b92f6-102">web 服务器使用户能够上载文档并将其存储在磁盘上。</span><span class="sxs-lookup"><span data-stu-id="b92f6-102">The web server enables users to upload documents and store them on disk.</span></span>

> [!TIP]
> <span data-ttu-id="b92f6-103">本练习将使用 Linux 作为示例, 但创建虚拟机和添加磁盘的基本过程在 Windows 中是相同的。</span><span class="sxs-lookup"><span data-stu-id="b92f6-103">This exercise uses Linux as the example, but the basic process of creating VMs and adding disks is the same for Windows.</span></span> <span data-ttu-id="b92f6-104">主要区别是对磁盘进行分区和格式化。</span><span class="sxs-lookup"><span data-stu-id="b92f6-104">The primary difference would be in partitioning and formatting the disk.</span></span> <span data-ttu-id="b92f6-105">在 Windows 中, 你可以通过远程桌面连接到 VM, 并使用内置磁盘管理工具或部署类似于此处将使用的 Bash 脚本的 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="b92f6-105">On Windows, you can connect to your VM over Remote Desktop and use the built-in Disk Management tools or deploy a PowerShell script that's similar to the Bash script you'll use here.</span></span>

<span data-ttu-id="b92f6-106">您的目标是创建 Linux VM, 并将名为**uploadDataDisk1**的新虚拟硬盘 (VHD) 附加到存储`/uploads`目录。</span><span class="sxs-lookup"><span data-stu-id="b92f6-106">Your goal here is to create a Linux VM and attach a new virtual hard disk (VHD) named **uploadDataDisk1** to store the `/uploads` directory.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-azure-cli-default-values"></a><span data-ttu-id="b92f6-107">设置 Azure CLI 默认值</span><span class="sxs-lookup"><span data-stu-id="b92f6-107">Set Azure CLI default values</span></span>

<span data-ttu-id="b92f6-108">使用 Azure CLI, 可以设置默认值, 因此无需在每次运行命令时重复此操作。</span><span class="sxs-lookup"><span data-stu-id="b92f6-108">The Azure CLI enables you to set default values so you don't have to repeat them each time you run a command.</span></span>

<span data-ttu-id="b92f6-109">在这里, 你将指定默认的 Azure 位置或区域。</span><span class="sxs-lookup"><span data-stu-id="b92f6-109">Here you'll specify the default Azure location, or region.</span></span> <span data-ttu-id="b92f6-110">这是将放置 Azure VM 的位置。</span><span class="sxs-lookup"><span data-stu-id="b92f6-110">This is the location where your Azure VM will be placed.</span></span>

<span data-ttu-id="b92f6-111">理想情况下, 这将接近你的客户端。</span><span class="sxs-lookup"><span data-stu-id="b92f6-111">Ideally this would be close to your clients.</span></span> <span data-ttu-id="b92f6-112">在这种情况下, 从可用于 Azure 沙盒的位置选择最接近的区域。</span><span class="sxs-lookup"><span data-stu-id="b92f6-112">In this case, select the closest region to you from the locations available to the Azure sandbox.</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="b92f6-113">运行`az configure`以设置要使用的默认位置。</span><span class="sxs-lookup"><span data-stu-id="b92f6-113">Run `az configure` to set the default location you want to use.</span></span> <span data-ttu-id="b92f6-114">将**eastus**替换为在上面的步骤中选择的位置。</span><span class="sxs-lookup"><span data-stu-id="b92f6-114">Replace **eastus** with the location chosen in the step above.</span></span>

    ```azurecli
    az configure --defaults location=eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="b92f6-115">将默认资源组名称设置为通过 Azure 沙盒为您创建的预配置资源组: \*\* <rgn>[沙盒资源组]</rgn>\*\*</span><span class="sxs-lookup"><span data-stu-id="b92f6-115">Set the default resource group name to the pre-configured resource group created for you through the Azure sandbox: **<rgn>[sandbox resource group]</rgn>**</span></span>

    ```azurecli
    az configure --defaults group="<rgn>[sandbox Resource Group]</rgn>"
    ```

## <a name="create-a-linux-vm"></a><span data-ttu-id="b92f6-116">创建 Linux VM</span><span class="sxs-lookup"><span data-stu-id="b92f6-116">Create a Linux VM</span></span>

<span data-ttu-id="b92f6-117">在这里, 你将创建一个 Linux VM 来托管你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b92f6-117">Here you create a Linux VM to host your web server.</span></span>

1. <span data-ttu-id="b92f6-118">运行此`az vm create`命令以创建 Ubuntu Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="b92f6-118">Run this `az vm create` command to create an Ubuntu Linux VM.</span></span>

    ```azurecli
    az vm create \
      --name support-web-vm01 \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --admin-username azureuser \
      --generate-ssh-keys
    ```

    * <span data-ttu-id="b92f6-119">VM 的名称为**支持-web-vm01**。</span><span class="sxs-lookup"><span data-stu-id="b92f6-119">The VM's name is **support-web-vm01**.</span></span>
    * <span data-ttu-id="b92f6-120">其大小为**Standard_DS2_v2**。</span><span class="sxs-lookup"><span data-stu-id="b92f6-120">Its size is **Standard_DS2_v2**.</span></span>
    * <span data-ttu-id="b92f6-121">管理员用户名为**azureuser**。</span><span class="sxs-lookup"><span data-stu-id="b92f6-121">The admin username is **azureuser**.</span></span> <span data-ttu-id="b92f6-122">实际上, 此名称可以是任何您喜欢的名称。</span><span class="sxs-lookup"><span data-stu-id="b92f6-122">In practice, this name can be whatever you like.</span></span>
    * <span data-ttu-id="b92f6-123">此`--generate-ssh-keys`参数为你生成 SSH 密钥对, 使你能够通过 SSH 连接到 VM。</span><span class="sxs-lookup"><span data-stu-id="b92f6-123">The `--generate-ssh-keys` argument generates an SSH keypair for you, enabling you to connect to your VM over SSH.</span></span>

    <span data-ttu-id="b92f6-124">VM 需要几分钟时间。</span><span class="sxs-lookup"><span data-stu-id="b92f6-124">The VM takes a few minutes to come up.</span></span> <span data-ttu-id="b92f6-125">VM 准备就绪后, 您将看到 JSON 格式的相关信息。</span><span class="sxs-lookup"><span data-stu-id="b92f6-125">When the VM is ready, you see information about it in JSON format.</span></span> <span data-ttu-id="b92f6-126">下面是一个示例。</span><span class="sxs-lookup"><span data-stu-id="b92f6-126">Here's an example.</span></span>

    ```json
    {
      "fqdns": "",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/680469d8-edB7-42ec-b118-cd80d51741e7/providers/Microsoft.Compute/virtualMachines/support-web-vm01",
      "location": "eastus",
      "macAddress": "00-0D-3A-10-63-0A",
      "powerState": "VM running",
      "privateIpAddress": "10.0.0.4",
      "publicIpAddress": "104.211.38.211",
      "resourceGroup": "680469d8-edB7-42ec-b118-cd80d51741e7",
      "zones": ""
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="b92f6-127">在本课中, 你将使用此 VM 了解如何管理磁盘。</span><span class="sxs-lookup"><span data-stu-id="b92f6-127">In this lesson you're using this VM to learn how to manage disks.</span></span> <span data-ttu-id="b92f6-128">在实践中, 您可能还会安装 web 服务器和其他软件, `az vm open-port`然后运行, 以使您需要的端口成为外部世界的可用端口。</span><span class="sxs-lookup"><span data-stu-id="b92f6-128">In practice, you might also install web server and other software and then run `az vm open-port` to make the ports you need available to the outside world.</span></span>

## <a name="add-an-empty-data-disk-to-your-vm"></a><span data-ttu-id="b92f6-129">将空数据磁盘添加到 VM</span><span class="sxs-lookup"><span data-stu-id="b92f6-129">Add an empty data disk to your VM</span></span>

<span data-ttu-id="b92f6-130">在这里, 你将创建一个空的数据磁盘并将其附加到你的 VM。</span><span class="sxs-lookup"><span data-stu-id="b92f6-130">Here you'll create an empty data disk and attach it to your VM.</span></span> <span data-ttu-id="b92f6-131">你的数据磁盘最初的大小为 64 GB。</span><span class="sxs-lookup"><span data-stu-id="b92f6-131">Your data disk will initially be 64 GB in size.</span></span> <span data-ttu-id="b92f6-132">稍后, 将此磁盘装入你的 VM `/uploads`上的目录。</span><span class="sxs-lookup"><span data-stu-id="b92f6-132">Later, you'll mount this disk to the `/uploads` directory on your VM.</span></span>

> [!TIP]
> <span data-ttu-id="b92f6-133">出于学习目的, 您要创建虚拟机和数据磁盘作为独立步骤。</span><span class="sxs-lookup"><span data-stu-id="b92f6-133">For learning purposes you're creating the VM and data disk as separate steps.</span></span> <span data-ttu-id="b92f6-134">实际上, 您可以在创建 VM `--data-disk-sizes-gb`时指定`az vm create`命令的参数, 以添加数据磁盘。</span><span class="sxs-lookup"><span data-stu-id="b92f6-134">In practice, you can specify the `--data-disk-sizes-gb` argument to the `az vm create` command to add data disks when the VM is created.</span></span>

1. <span data-ttu-id="b92f6-135">运行以下`az vm disk attach`命令, 将新的空磁盘添加到 VM。</span><span class="sxs-lookup"><span data-stu-id="b92f6-135">Run the following `az vm disk attach` command to add a new empty disk to the VM.</span></span>

    ```azurecli
    az vm disk attach \
      --vm-name support-web-vm01 \
      --disk uploadDataDisk1 \
      --size-gb 64 \
      --sku Premium_LRS \
      --new
    ```

    <span data-ttu-id="b92f6-136">此命令:</span><span class="sxs-lookup"><span data-stu-id="b92f6-136">This command:</span></span>

    * <span data-ttu-id="b92f6-137">将磁盘命名为**uploadDataDisk1**。</span><span class="sxs-lookup"><span data-stu-id="b92f6-137">Names the disk **uploadDataDisk1**.</span></span>
    * <span data-ttu-id="b92f6-138">将其大小设置为 64 GB。</span><span class="sxs-lookup"><span data-stu-id="b92f6-138">Set its size to be 64 GB.</span></span>
    * <span data-ttu-id="b92f6-139">指定将高级存储与本地冗余结合使用。</span><span class="sxs-lookup"><span data-stu-id="b92f6-139">Specifies to use premium storage with local redundancy.</span></span>

<span data-ttu-id="b92f6-140">若要使用此磁盘, 需要对其进行分区和格式化。</span><span class="sxs-lookup"><span data-stu-id="b92f6-140">To use the disk, you'll need to partition and format it.</span></span> <span data-ttu-id="b92f6-141">接下来将执行此操作。</span><span class="sxs-lookup"><span data-stu-id="b92f6-141">You'll do that next.</span></span>

## <a name="initialize-and-format-your-data-disk"></a><span data-ttu-id="b92f6-142">初始化数据磁盘并设置其格式</span><span class="sxs-lookup"><span data-stu-id="b92f6-142">Initialize and format your data disk</span></span>

<span data-ttu-id="b92f6-143">您的空数据驱动器需要进行初始化和格式化。</span><span class="sxs-lookup"><span data-stu-id="b92f6-143">Your empty data drive needs to be initialized and formatted.</span></span> <span data-ttu-id="b92f6-144">执行此操作的过程与物理磁盘的过程相同。</span><span class="sxs-lookup"><span data-stu-id="b92f6-144">The process to do that is the same as for a physical disk.</span></span>

<span data-ttu-id="b92f6-145">对于一次性任务, 可以通过 SSH 手动连接到 VM 并运行所需的命令。</span><span class="sxs-lookup"><span data-stu-id="b92f6-145">For one-time tasks, you might manually connect to your VM over SSH and run the commands you need.</span></span> <span data-ttu-id="b92f6-146">若要使该过程更具可重复性且更少出错, 可以使用指定所需命令的 Bash 脚本 (或可用的 PowerShell 脚本)。</span><span class="sxs-lookup"><span data-stu-id="b92f6-146">To make the process more repeatable and less error-prone, you can use a Bash script (or a PowerShell script where available) that specifies the commands you need.</span></span>

<span data-ttu-id="b92f6-147">使用脚本自动执行此过程会带来额外的好处&ndash;您的脚本作为文档的执行过程的文档。</span><span class="sxs-lookup"><span data-stu-id="b92f6-147">Using a script to automate the process has an added benefit &ndash; your script serves as documentation for how the process is performed.</span></span> <span data-ttu-id="b92f6-148">其他用户可以阅读您的脚本以了解如何配置系统。</span><span class="sxs-lookup"><span data-stu-id="b92f6-148">Others can read your script to understand how the system is configured.</span></span> <span data-ttu-id="b92f6-149">如果需要更改该过程, 只需修改脚本并在临时暂存虚拟机上对其进行测试, 然后再将更改部署到生产环境中。</span><span class="sxs-lookup"><span data-stu-id="b92f6-149">If you need to change the process, you can simply modify your script and test it on a temporary scratch VM before you deploy your change to production.</span></span>

<span data-ttu-id="b92f6-150">若要在本课中自动执行此过程, 您将使用_自定义脚本扩展_。</span><span class="sxs-lookup"><span data-stu-id="b92f6-150">To automate the process in this lesson, you'll use the _Custom Script Extension_.</span></span> <span data-ttu-id="b92f6-151">自定义脚本扩展是在 Azure 虚拟机上下载和运行脚本的简单方法。</span><span class="sxs-lookup"><span data-stu-id="b92f6-151">The Custom Script Extension is an easy way to download and run scripts on your Azure VMs.</span></span> <span data-ttu-id="b92f6-152">它只是在 VM 启动并运行后配置系统的多种方法之一。</span><span class="sxs-lookup"><span data-stu-id="b92f6-152">It's just one of the many ways you can configure the system once your VM is up and running.</span></span>

<span data-ttu-id="b92f6-153">你可以将脚本存储在 Azure 存储或公共位置 (如 GitHub) 中。</span><span class="sxs-lookup"><span data-stu-id="b92f6-153">You can store your scripts in Azure storage or in a public location such as GitHub.</span></span> <span data-ttu-id="b92f6-154">您可以手动运行脚本, 也可以将其作为更自动化的部署的一部分运行。</span><span class="sxs-lookup"><span data-stu-id="b92f6-154">You can run scripts manually or as part of a more automated deployment.</span></span> <span data-ttu-id="b92f6-155">在这里, 你将运行 Azure CLI 命令, 从 GitHub 下载一个预先准备的 Bash 脚本并在你的 VM 上执行它。</span><span class="sxs-lookup"><span data-stu-id="b92f6-155">Here, you'll run an Azure CLI command to download a pre-made Bash script from GitHub and execute it on your VM.</span></span>

<span data-ttu-id="b92f6-156">出于学习目的, 您还将在 vm 上运行一些命令以验证 vm 是否按预期配置。</span><span class="sxs-lookup"><span data-stu-id="b92f6-156">For learning purposes, here you'll also run a few commands on your VM to verify that the VM is configured as you expect.</span></span>

1. <span data-ttu-id="b92f6-157">运行`az vm show`以获取你的 VM 的公共 IP 地址, 并将该 ip 地址另存为 Bash 变量。</span><span class="sxs-lookup"><span data-stu-id="b92f6-157">Run `az vm show` to get your VM's public IP address and save the IP address as a Bash variable.</span></span>

    ```azurecli
    ipaddress=$(az vm show \
      --name support-web-vm01 \
      --show-details \
      --query [publicIps] \
      --o tsv)
    ```

1. <span data-ttu-id="b92f6-158">运行以下`ssh`命令, 通过 SSH 连接`lsblk`使用刚创建的`ipaddress`变量数据在 VM 上运行命令。</span><span class="sxs-lookup"><span data-stu-id="b92f6-158">Run the following `ssh` command to run the `lsblk` command on your VM over an SSH connection using the `ipaddress` variable data you just created.</span></span> <span data-ttu-id="b92f6-159">回想一下`azureuser` , 我们创建 VM 时使用的是管理员用户名。</span><span class="sxs-lookup"><span data-stu-id="b92f6-159">Recall that `azureuser` was the admin username we used when we created the VM.</span></span> <span data-ttu-id="b92f6-160">如果选择了其他名称, 请改为使用该名称。</span><span class="sxs-lookup"><span data-stu-id="b92f6-160">If you chose a different name, use that instead.</span></span> <span data-ttu-id="b92f6-161">出现提示时, 输入 "yes"。</span><span class="sxs-lookup"><span data-stu-id="b92f6-161">Enter "yes" when prompted.</span></span>

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    <span data-ttu-id="b92f6-162">此命令的输出应该如下所示。</span><span class="sxs-lookup"><span data-stu-id="b92f6-162">The output of this command should look like the following.</span></span>

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk 
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom  
    sdc      8:32   0   64G  0 disk 
    sda      8:0    0   30G  0 disk 
    └─sda1   8:1    0   30G  0 part /
    ```

    <span data-ttu-id="b92f6-163">你会看到你刚创建的`sdc`64 GB 驱动器。</span><span class="sxs-lookup"><span data-stu-id="b92f6-163">You see the 64 GB drive, `sdc`, that you just created.</span></span> <span data-ttu-id="b92f6-164">您会发现它未装入。</span><span class="sxs-lookup"><span data-stu-id="b92f6-164">You see that it's not mounted.</span></span> <span data-ttu-id="b92f6-165">这是因为它尚未初始化。</span><span class="sxs-lookup"><span data-stu-id="b92f6-165">That's because it's hasn't yet been initialized.</span></span>

1. <span data-ttu-id="b92f6-166">运行以下`az vm extension set`命令, 在 VM 上运行预生成的 Bash 脚本。</span><span class="sxs-lookup"><span data-stu-id="b92f6-166">Run the following `az vm extension set` command to run the pre-made Bash script on your VM.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b92f6-167">该脚本将`/etc/fstab`进行修改。</span><span class="sxs-lookup"><span data-stu-id="b92f6-167">The script modifies `/etc/fstab`.</span></span> <span data-ttu-id="b92f6-168">错误地修改`/etc/fstab`文件可能会导致系统无法引导。</span><span class="sxs-lookup"><span data-stu-id="b92f6-168">Improperly modifying the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="b92f6-169">在部署到生产环境之前, 应始终在临时暂存系统上测试配置更改。</span><span class="sxs-lookup"><span data-stu-id="b92f6-169">Always test configuration changes on a temporary scratch system before you deploy to production.</span></span> <span data-ttu-id="b92f6-170">请参阅您的分发文档以了解如何正确修改此文件。</span><span class="sxs-lookup"><span data-stu-id="b92f6-170">Refer to your distribution's documentation to learn how to properly modify this file.</span></span> <span data-ttu-id="b92f6-171">在生产环境中, 我们还建议您创建此文件的备份, 以便您可以在需要时还原配置。</span><span class="sxs-lookup"><span data-stu-id="b92f6-171">In production, we also recommend that you create a backup of this file so you can restore the configuration if needed.</span></span>

    ```azurecli
    az vm extension set \
      --vm-name support-web-vm01 \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/add-data-disk.sh"]}' \
      --protected-settings '{"commandToExecute": "./add-data-disk.sh"}'
    ```

    <span data-ttu-id="b92f6-172">运行命令时, 可以从单独的浏览器选项卡[检查 Bash 脚本](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/add-data-disk.sh?azure-portal=true)(如果需要)。</span><span class="sxs-lookup"><span data-stu-id="b92f6-172">While the command runs, you can [examine the Bash script](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/add-data-disk.sh?azure-portal=true) from a separate browser tab if you'd like.</span></span>

    <span data-ttu-id="b92f6-173">总而言之, 脚本:</span><span class="sxs-lookup"><span data-stu-id="b92f6-173">To summarize, the script:</span></span>

    * <span data-ttu-id="b92f6-174">对驱动器`/dev/sdc`进行分区。</span><span class="sxs-lookup"><span data-stu-id="b92f6-174">Partitions the drive `/dev/sdc`.</span></span>
    * <span data-ttu-id="b92f6-175">在驱动器上创建 ext4 文件系统。</span><span class="sxs-lookup"><span data-stu-id="b92f6-175">Creates an ext4 filesystem on the drive.</span></span>
    * <span data-ttu-id="b92f6-176">创建`/uploads`目录, 将其用作装入点。</span><span class="sxs-lookup"><span data-stu-id="b92f6-176">Create the `/uploads` directory, which we use as our mount point.</span></span>
    * <span data-ttu-id="b92f6-177">将磁盘附加到装入点。</span><span class="sxs-lookup"><span data-stu-id="b92f6-177">Attaches the disk to the mount point.</span></span>
    * <span data-ttu-id="b92f6-178">更新`/etc/fstab` , 以便在系统重新启动后自动装入驱动器。</span><span class="sxs-lookup"><span data-stu-id="b92f6-178">Updates `/etc/fstab` so that the drive is mounted automatically after the system reboots.</span></span>

1. <span data-ttu-id="b92f6-179">若要验证配置, 请运行与`ssh`以前通过 SSH 连接在 VM 上运行`lsblk`命令相同的命令。</span><span class="sxs-lookup"><span data-stu-id="b92f6-179">To verify the configuration, run the same `ssh` command as you did previously to run the `lsblk` command on your VM over an SSH connection.</span></span>

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    <span data-ttu-id="b92f6-180">您`sdc/sdc1`会发现已分区并已按预期`/uploads`方式安装到目录中。</span><span class="sxs-lookup"><span data-stu-id="b92f6-180">You see that `sdc/sdc1` is partitioned and mounted to the `/uploads` directory as you expect.</span></span>

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk 
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom  
    sdc      8:32   0   64G  0 disk 
    └─sdc1   8:33   0   64G  0 part /uploads
    sda      8:0    0   30G  0 disk 
    └─sda1   8:1    0   30G  0 part /
    ```

> [!TIP]
> <span data-ttu-id="b92f6-181">一些 Linux 内核支持修整以放弃磁盘上未使用的块。</span><span class="sxs-lookup"><span data-stu-id="b92f6-181">Some Linux kernels support TRIM to discard unused blocks on disks.</span></span> <span data-ttu-id="b92f6-182">此功能在 Azure 磁盘上可用, 如果您创建大型文件, 然后将其删除, 则可以节省资金。</span><span class="sxs-lookup"><span data-stu-id="b92f6-182">This feature is available on Azure disks and can save you money if you create large files and then delete them.</span></span> <span data-ttu-id="b92f6-183">了解如何在 Azure 文档中[打开此功能](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="b92f6-183">Learn how to [turn this feature on](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure?azure-portal=true) in the Azure documentation.</span></span>

## <a name="summary"></a><span data-ttu-id="b92f6-184">摘要</span><span class="sxs-lookup"><span data-stu-id="b92f6-184">Summary</span></span>

<span data-ttu-id="b92f6-185">在这里, 你创建了一个数据磁盘并将其附加到你的 VM。</span><span class="sxs-lookup"><span data-stu-id="b92f6-185">Here, you created a data disk and attached it to your VM.</span></span> <span data-ttu-id="b92f6-186">您使用自定义脚本扩展在虚拟机上运行预生成的 Bash 脚本, 以使该过程更具可重复项。</span><span class="sxs-lookup"><span data-stu-id="b92f6-186">You used the Custom Script Extension to run a pre-made Bash script on your VM to make the process more repeatable.</span></span> <span data-ttu-id="b92f6-187">Bash 脚本对磁盘进行分区、格式化和装入, 以便您的 web 服务器可以写入磁盘。</span><span class="sxs-lookup"><span data-stu-id="b92f6-187">The Bash script partitions, formats, and mounts your disk so that your web server can write to it.</span></span>

<span data-ttu-id="b92f6-188">现在你已在 VM 上准备了数据磁盘, 让我们更好地了解你可以创建的各种类型的磁盘。</span><span class="sxs-lookup"><span data-stu-id="b92f6-188">Now that you've prepared the data disk on your VM, let's explore a bit more about the various types of disks you can create.</span></span> <span data-ttu-id="b92f6-189">主要决定是选择标准存储还是高级存储。</span><span class="sxs-lookup"><span data-stu-id="b92f6-189">Your primary decision is whether to choose Standard or Premium storage.</span></span>