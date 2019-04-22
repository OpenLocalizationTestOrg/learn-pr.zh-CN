azure 将 VHD 映像存储为 Azure 存储帐户中的页面 blob。 使用托管磁盘时, Azure 会按代表管理存储-它是选择托管磁盘的最佳原因之一。

创建 VM 时, 它会选择 OS 磁盘的大小。 根据您选择的图像的具体大小。 在 Linux 中, 通常约为 30 gb, 在 Windows 上约为 127 gb。

你可以添加数据磁盘以提供额外的存储空间, 但你可能还希望扩展现有磁盘-可能是旧应用程序无法跨驱动器拆分其数据, 或者你正在将物理电脑驱动器迁移到 Azure 并需要更大的 OS 驱动器。

> [!NOTE]
> 您只能将磁盘大小调整为_较大_大小。 不支持缩小托管磁盘。

更改磁盘的大小还可以更改磁盘的级别 (例如, 从 P10 到 P20)。 请注意, 这可能会对性能升级有好处, 但在您上移到高级层时, 成本也会更高。

## <a name="vm-size-versus-disk-size"></a>VM 大小与磁盘大小

创建 vm 时选择的 VM 大小决定了它可以分配多少个资源。 对于 storage, 大小控制可添加到 VM 的磁盘数以及每个磁盘的最大大小。

如前所述, 某些 VM 大小仅支持标准存储驱动器-限制 i/o 性能。

如果发现您需要的存储空间超过您的 VM 大小允许的数量, 则可以更改 VM 大小。 我们将在 " [Azure 虚拟机模块简介](/learn/modules/intro-to-azure-virtual-machines?azure-portal=true)" 中介绍该主题。

## <a name="expanding-a-disk-using-the-azure-cli"></a>使用 Azure CLI 扩展磁盘

> [!WARNING]
> 始终确保在执行磁盘大小调整操作之前备份数据!

无法在运行的虚拟机上执行 vhd 上的操作。 第一步是通过`az vm deallocate`提供虚拟机名称和资源组名称来停止和取消分配 vm。

取消分配 vm 与仅_停止_vm 不同, 它将释放相关的计算资源, 并允许 Azure 对虚拟化的硬件进行配置更改。

> [!NOTE]
> 请勿立即运行这些命令。 将在下一部分中练习此过程。

```azurecli
az vm deallocate \
  --resource-group <resource-group-name> \
  --name <vm-name>
```

接下来, 要调整磁盘大小, 请`az disk update`使用, 传递磁盘名称、资源组名称和新请求的大小。 扩展托管磁盘时, 指定的大小将映射到最接近的托管磁盘大小。

```azurecli
az disk update \
  --resource-group <resource-group-name> \
  --name <disk-name> \
  --size-gb 200
```

最后, 运行`az vm start`以重新启动 VM。

```azurecli
az vm start \
  --resource-group <resource-group-name> \
  --name <vm-name>
```

## <a name="expanding-a-disk-using-the-azure-portal"></a>使用 Azure 门户扩展磁盘

您还可以通过 Azure 门户扩展磁盘。

1. 使用 vm 的 "**概述**" 页上工具栏中的 "**停止**" 按钮停止 VM。

1. 在 "**设置**" 部分中单击 "**磁盘**"。

1. 选择要调整大小的数据磁盘。

    ![显示要编辑的 VHD 的虚拟机的磁盘部分的屏幕截图](../media/5-portal-disks.png)

1. 在 "磁盘详细信息" 中, __ 键入大于当前大小的大小。 您还可以在此处从 Premium 更改为标准 (反之亦然)。 这些设置将调整您的性能, 如 "预测 IOPS" 部分所示。

    ![显示 "新大小" 字段并突出显示 "VHD 编辑" 屏幕的屏幕截图](../media/5-resize-disk.png)

1. 单击 "**保存**" 以保存所做的更改。

1. 重新启动 VM。


### <a name="expanding-the-partition"></a>扩展分区

就像添加新的数据磁盘一样, 展开的磁盘在您扩展分区和文件系统之前不会添加任何可用空间。 必须使用可供 VM 使用的 OS 工具来完成此操作。

在 Windows 上, 您可以使用磁盘管理器工具或`diskpart`命令行工具。

在 Linux 上, 您可以`parted`使用`resize2fs`和。 您将在下一部分中执行此操作。