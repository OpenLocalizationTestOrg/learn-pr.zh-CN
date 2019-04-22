您的法律公司正在扩展其事例负载, 并且您已完成创建新的 Linux web 服务器以存储来自各种源 (客户端、其他法律公司和执法机构) 的关键文档的任务。 web 服务器使用户能够上载文档并将其存储在磁盘上。

> [!TIP]
> 本练习将使用 Linux 作为示例, 但创建虚拟机和添加磁盘的基本过程在 Windows 中是相同的。 主要区别是对磁盘进行分区和格式化。 在 Windows 中, 你可以通过远程桌面连接到 VM, 并使用内置磁盘管理工具或部署类似于此处将使用的 Bash 脚本的 PowerShell 脚本。

您的目标是创建 Linux VM, 并将名为**uploadDataDisk1**的新虚拟硬盘 (VHD) 附加到存储`/uploads`目录。

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-azure-cli-default-values"></a>设置 Azure CLI 默认值

使用 Azure CLI, 可以设置默认值, 因此无需在每次运行命令时重复此操作。

在这里, 你将指定默认的 Azure 位置或区域。 这是将放置 Azure VM 的位置。

理想情况下, 这将接近你的客户端。 在这种情况下, 从可用于 Azure 沙盒的位置选择最接近的区域。

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. 运行`az configure`以设置要使用的默认位置。 将**eastus**替换为在上面的步骤中选择的位置。

    ```azurecli
    az configure --defaults location=eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. 将默认资源组名称设置为通过 Azure 沙盒为您创建的预配置资源组: ** <rgn>[沙盒资源组]</rgn>**

    ```azurecli
    az configure --defaults group="<rgn>[sandbox Resource Group]</rgn>"
    ```

## <a name="create-a-linux-vm"></a>创建 Linux VM

在这里, 你将创建一个 Linux VM 来托管你的 web 服务器。

1. 运行此`az vm create`命令以创建 Ubuntu Linux 虚拟机。

    ```azurecli
    az vm create \
      --name support-web-vm01 \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --admin-username azureuser \
      --generate-ssh-keys
    ```

    * VM 的名称为**支持-web-vm01**。
    * 其大小为**Standard_DS2_v2**。
    * 管理员用户名为**azureuser**。 实际上, 此名称可以是任何您喜欢的名称。
    * 此`--generate-ssh-keys`参数为你生成 SSH 密钥对, 使你能够通过 SSH 连接到 VM。

    VM 需要几分钟时间。 VM 准备就绪后, 您将看到 JSON 格式的相关信息。 下面是一个示例。

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
    > 在本课中, 你将使用此 VM 了解如何管理磁盘。 在实践中, 您可能还会安装 web 服务器和其他软件, `az vm open-port`然后运行, 以使您需要的端口成为外部世界的可用端口。

## <a name="add-an-empty-data-disk-to-your-vm"></a>将空数据磁盘添加到 VM

在这里, 你将创建一个空的数据磁盘并将其附加到你的 VM。 你的数据磁盘最初的大小为 64 GB。 稍后, 将此磁盘装入你的 VM `/uploads`上的目录。

> [!TIP]
> 出于学习目的, 您要创建虚拟机和数据磁盘作为独立步骤。 实际上, 您可以在创建 VM `--data-disk-sizes-gb`时指定`az vm create`命令的参数, 以添加数据磁盘。

1. 运行以下`az vm disk attach`命令, 将新的空磁盘添加到 VM。

    ```azurecli
    az vm disk attach \
      --vm-name support-web-vm01 \
      --disk uploadDataDisk1 \
      --size-gb 64 \
      --sku Premium_LRS \
      --new
    ```

    此命令:

    * 将磁盘命名为**uploadDataDisk1**。
    * 将其大小设置为 64 GB。
    * 指定将高级存储与本地冗余结合使用。

若要使用此磁盘, 需要对其进行分区和格式化。 接下来将执行此操作。

## <a name="initialize-and-format-your-data-disk"></a>初始化数据磁盘并设置其格式

您的空数据驱动器需要进行初始化和格式化。 执行此操作的过程与物理磁盘的过程相同。

对于一次性任务, 可以通过 SSH 手动连接到 VM 并运行所需的命令。 若要使该过程更具可重复性且更少出错, 可以使用指定所需命令的 Bash 脚本 (或可用的 PowerShell 脚本)。

使用脚本自动执行此过程会带来额外的好处&ndash;您的脚本作为文档的执行过程的文档。 其他用户可以阅读您的脚本以了解如何配置系统。 如果需要更改该过程, 只需修改脚本并在临时暂存虚拟机上对其进行测试, 然后再将更改部署到生产环境中。

若要在本课中自动执行此过程, 您将使用_自定义脚本扩展_。 自定义脚本扩展是在 Azure 虚拟机上下载和运行脚本的简单方法。 它只是在 VM 启动并运行后配置系统的多种方法之一。

你可以将脚本存储在 Azure 存储或公共位置 (如 GitHub) 中。 您可以手动运行脚本, 也可以将其作为更自动化的部署的一部分运行。 在这里, 你将运行 Azure CLI 命令, 从 GitHub 下载一个预先准备的 Bash 脚本并在你的 VM 上执行它。

出于学习目的, 您还将在 vm 上运行一些命令以验证 vm 是否按预期配置。

1. 运行`az vm show`以获取你的 VM 的公共 IP 地址, 并将该 ip 地址另存为 Bash 变量。

    ```azurecli
    ipaddress=$(az vm show \
      --name support-web-vm01 \
      --show-details \
      --query [publicIps] \
      --o tsv)
    ```

1. 运行以下`ssh`命令, 通过 SSH 连接`lsblk`使用刚创建的`ipaddress`变量数据在 VM 上运行命令。 回想一下`azureuser` , 我们创建 VM 时使用的是管理员用户名。 如果选择了其他名称, 请改为使用该名称。 出现提示时, 输入 "yes"。

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    此命令的输出应该如下所示。

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk 
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom  
    sdc      8:32   0   64G  0 disk 
    sda      8:0    0   30G  0 disk 
    └─sda1   8:1    0   30G  0 part /
    ```

    你会看到你刚创建的`sdc`64 GB 驱动器。 您会发现它未装入。 这是因为它尚未初始化。

1. 运行以下`az vm extension set`命令, 在 VM 上运行预生成的 Bash 脚本。

    > [!WARNING]
    > 该脚本将`/etc/fstab`进行修改。 错误地修改`/etc/fstab`文件可能会导致系统无法引导。 在部署到生产环境之前, 应始终在临时暂存系统上测试配置更改。 请参阅您的分发文档以了解如何正确修改此文件。 在生产环境中, 我们还建议您创建此文件的备份, 以便您可以在需要时还原配置。

    ```azurecli
    az vm extension set \
      --vm-name support-web-vm01 \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/add-data-disk.sh"]}' \
      --protected-settings '{"commandToExecute": "./add-data-disk.sh"}'
    ```

    运行命令时, 可以从单独的浏览器选项卡[检查 Bash 脚本](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/add-data-disk.sh?azure-portal=true)(如果需要)。

    总而言之, 脚本:

    * 对驱动器`/dev/sdc`进行分区。
    * 在驱动器上创建 ext4 文件系统。
    * 创建`/uploads`目录, 将其用作装入点。
    * 将磁盘附加到装入点。
    * 更新`/etc/fstab` , 以便在系统重新启动后自动装入驱动器。

1. 若要验证配置, 请运行与`ssh`以前通过 SSH 连接在 VM 上运行`lsblk`命令相同的命令。

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    您`sdc/sdc1`会发现已分区并已按预期`/uploads`方式安装到目录中。

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
> 一些 Linux 内核支持修整以放弃磁盘上未使用的块。 此功能在 Azure 磁盘上可用, 如果您创建大型文件, 然后将其删除, 则可以节省资金。 了解如何在 Azure 文档中[打开此功能](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure?azure-portal=true)。

## <a name="summary"></a>摘要

在这里, 你创建了一个数据磁盘并将其附加到你的 VM。 您使用自定义脚本扩展在虚拟机上运行预生成的 Bash 脚本, 以使该过程更具可重复项。 Bash 脚本对磁盘进行分区、格式化和装入, 以便您的 web 服务器可以写入磁盘。

现在你已在 VM 上准备了数据磁盘, 让我们更好地了解你可以创建的各种类型的磁盘。 主要决定是选择标准存储还是高级存储。