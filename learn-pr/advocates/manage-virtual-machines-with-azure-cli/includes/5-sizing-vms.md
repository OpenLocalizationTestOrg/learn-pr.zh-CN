虚拟机的大小必须适合预期工作。 如果没有正确的内存或 CPU 量的 VM 在负载或运行速度太慢, 则无法有效。 

## <a name="pre-defined-vm-sizes"></a>预定义的 VM 大小

创建虚拟机时, 可以提供_vm 大小_值, 用于确定将专门用于虚拟机的计算资源量。 这包括从 Azure 提供给虚拟机的 CPU、GPU 和内存。

Azure 为 Linux 和 Windows 定义一组预定义的 VM 大小, 以根据预期的使用情况进行选择。 

| 类型 | 大小 | 说明 |
|------|-------|-------------|
| 常规用途   | Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7 | 平衡 CPU 与内存的平衡。 适用于开发/测试和中小型应用程序和数据解决方案。 |
| 计算优化 | Fs、F | CPU 内存较高。 适用于中型流量的应用程序、网络设备和批处理过程。 |
| 内存优化  | Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D   | 高内存到核心。 非常适合关系数据库、大中型缓存和内存中的分析。 |
| 存储优化 | ! | 高磁盘吞吐量和 IO。 是大型数据、SQL 和 NoSQL 数据库的理想选择。 |
| 已优化 GPU | NV、NC | 专用虚拟机针对较重的图形呈现和视频编辑。 |
| 高性能 | H, A8-11 | 具有可选高吞吐量网络接口 (RDMA) 的最强大的 CPU 虚拟机。 | 

可用大小根据您要在其中创建虚拟机的区域而变化。 您可以使用`vm list-sizes`命令获取可用大小的列表。 请尝试将此内容键入到 Azure 云命令行管理程序:

```azurecli
az vm list-sizes --location eastus --output table
```

以下是简短的响应`eastus`:

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

## <a name="specifying-a-size-during-vm-creation"></a>在创建 VM 期间指定大小

我们在创建虚拟机时未指定大小, 因此 Azure 选择了默认的常规用途大小为 us `Standard_DS1_v2`。 但是, 可以使用`vm create` `--size`参数将大小指定为命令的一部分。 例如, 可以使用以下命令创建16核虚拟机:

```azurecli
az vm create --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM2 \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

> [!WARNING]
> 您的订阅层对可以创建多少个资源以及这些资源的总大小[强制实施限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)。 例如, 您可以使用20个带即点即用订阅的**虚拟 cpu** , 并且每个免费的层仅有**4 个 vCPUs** 。 当您超过此限制时, Azure CLI 将告知您**配额已超出**错误。 如果您在自己的付费订阅中遇到此错误, 您可以请求通过[免费的联机请求](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-quota-errors)提升与付费订阅关联的限制 (最高为 10000 vCPUs!)。

## <a name="resizing-an-existing-vm"></a>调整现有虚拟机的大小
如果工作负载发生变化, 或者在创建时其大小不正确, 则还可以调整现有 VM 的大小。 在请求调整大小之前, 必须检查 VM 所属的群集中是否提供了所需的大小。 可以使用以下`vm list-vm-resize-options`命令执行此操作:

```azurecli
az vm list-vm-resize-options --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --output table
```

这将返回资源组中所有可用的大小配置的列表。 如果我们所需的大小在群集中不可用, __ 但在区域中可用, 则可以取消[分配 VM](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate)。 此命令将停止运行中的 VM 并将其从当前群集中删除, 而不会丢失任何资源。 然后, 可以调整它的大小, 这将在大小配置可用的新群集中重新创建 VM。

> [!NOTE]
> Azure 沙盒仅限于少数几个 VM 大小。 在免费的 Microsoft 学习订阅中不允许大多数可能性。

若要调整虚拟机的大小, `vm resize`请使用命令。 例如, 我们可能会发现, 我们的 VM 是我们希望 it 执行的任务的 underpowered。 我们可以将它增大到 DS3_v2 层, 在其中有 4 vCores 和14G 内存的情况。 在云命令行管理程序中键入以下命令:

```azurecli
az vm resize --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --size Standard_DS3_v2
```

此命令将需要几分钟的时间来减小 VM 的资源, 完成后, 将返回新的 JSON 配置。