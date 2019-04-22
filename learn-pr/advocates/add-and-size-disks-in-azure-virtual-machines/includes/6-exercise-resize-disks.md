假设您低估了一些上载文件的大小, 以及您的上传磁盘空间不足的情况。 您决定将空间从 64 gb 加倍到 128 gb。

在这里, 你将练习在以前的单元中学习的过程。

## <a name="resize-the-data-disk"></a>调整数据磁盘的大小

若要调整磁盘大小, 您需要该磁盘的 ID 或名称。 在这种情况下, 您已经知道名称, **uploadDataDisk1**。 但如果你不记得, 或者是由其他人创建的, 则可以运行`az disk list`以查找名称。

1. 运行`az disk list`以打印资源组中的托管磁盘列表。 如果同一资源组中有多个虚拟机, 则此列表可能包含其他磁盘。

    ```azurecli
    az disk list \
      --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
      --output table
    ```

    您会看到名为**uploadDataDisk1**的磁盘。

    ```output
    Name                                                        Gb
    ----------------------------------------------------------  ----
    support-web-vm01_OsDisk_1_141859cb21d64b85b9db3f70f0f5e851  30
    uploadDataDisk1                                             64
    ```

1. 运行以下`az vm deallocate`命令来停止和取消分配 VM。 这不会删除 VM, 但会将其置于可修改虚拟磁盘的状态。

    ```azurecli
    az vm deallocate --name support-web-vm01
    ```

1. 运行`az disk update`以将磁盘大小调整为 128 GB。

    ```azurecli
    az disk update --name uploadDataDisk1 --size-gb 128
    ```

1. 运行`az vm start`以重新启动 VM。

    ```azurecli
    az vm start --name support-web-vm01
    ```

    但我们尚未完成。 VM 上的操作系统尚无法使用额外的空间。 这是在下一节中完成的。

## <a name="expand-the-disk-partition"></a>展开磁盘分区

最后一步是告诉操作系统有关可用空间。 就像您之前执行的分区和格式步骤一样, 此过程与扩展物理、内部部署磁盘的过程相同。

1. 虽然您可以为 vm 保留一个固定的公共 ip 地址, 但默认情况下, vm 会在取消分配并重新启动时收到新的公用 ip 地址。 运行以下`az vm show`命令以使用 VM 的新公共 IP 地址更新 Bash 变量。

    ```azurecli
    ipaddress=$(az vm show --name support-web-vm01 -d --query [publicIps] --o tsv)
    ```

1. 正如您之前所做`lsblk`的那样, 请通过 SSH 在 VM 上运行以了解其当前状态。

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    您可以看到磁盘`sdc/sdc1`大小为 64 GB。

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk 
    └─sdb1   8:17   0   14G  0 part /mnt
    sdc      8:32   0  128G  0 disk 
    └─sdc1   8:33   0   64G  0 part /uploads
    sda      8:0    0   30G  0 disk 
    └─sda1   8:1    0   30G  0 part /
    ```

1. 与您以前对磁盘初始化的方式类似, 运行此`az vm extension set`命令, 通过执行我们创建的预设的 Bash 脚本来帮助您, 在 VM 上告知有关新可用空间的操作系统。

    ```azurecli
    az vm extension set \
      --vm-name support-web-vm01 \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/resize-data-disk.sh"]}' \
      --protected-settings '{"commandToExecute": "./resize-data-disk.sh"}'
    ```

    运行命令时, 可以从单独的浏览器选项卡[检查 Bash 脚本](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-add-and-size-disks-in-azure-virtual-machines/master/resize-data-disk.sh?azure-portal=true)(如果需要)。

    总而言之, 脚本:

    * 卸载磁盘`/dev/sdc1`。
    * 将分区1的大小调整为 128 GB。
    * 验证分区一致性。
    * 调整文件系统的大小。
    * Remounts 将驱动器`/dev/sdc1`重新安装到装入点`/uploads`。

1. 若要验证配置, 请`lsblk`再次在你的 VM 上运行 SSH。

    ```bash
    ssh azureuser@$ipaddress lsblk
    ```

    这次, 您会看到磁盘`sdc/sdc1`已扩展, 以适应磁盘大小的增长。

    ```output
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0    14G  0 disk 
    └─sdb1   8:17   0    14G  0 part /mnt
    sdc      8:32   0   128G  0 disk 
    └─sdc1   8:33   0 119.2G  0 part /uploads
    sda      8:0    0    30G  0 disk 
    └─sda1   8:1    0    30G  0 part /
    ```

1. 作为最后的验证步骤, 请通过 SSH 在 VM `df`上运行操作系统的实用工具, 以证明 OS 可以正确地进行查看。

    ```bash
    ssh azureuser@$ipaddress df -h
    ```

    您会看到驱动器的大小为 128 GB。

    ```output
    Filesystem      Size  Used Avail Use% Mounted on
    udev            3.4G     0  3.4G   0% /dev
    tmpfs           697M  8.6M  689M   2% /run
    /dev/sda1        30G  1.4G   28G   5% /
    tmpfs           3.5G     0  3.5G   0% /dev/shm
    tmpfs           5.0M     0  5.0M   0% /run/lock
    tmpfs           3.5G     0  3.5G   0% /sys/fs/cgroup
    /dev/sdb1        14G   35M   13G   1% /mnt
    /dev/sdc1        63G   52M   60G   1% /uploads
    tmpfs           697M     0  697M   0% /run/user/1000
    ```