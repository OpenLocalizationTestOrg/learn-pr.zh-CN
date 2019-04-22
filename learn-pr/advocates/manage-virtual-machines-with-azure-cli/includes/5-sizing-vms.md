<span data-ttu-id="93dec-101">虚拟机的大小必须适合预期工作。</span><span class="sxs-lookup"><span data-stu-id="93dec-101">Virtual machines must be sized appropriately for the expected work.</span></span> <span data-ttu-id="93dec-102">如果没有正确的内存或 CPU 量的 VM 在负载或运行速度太慢, 则无法有效。</span><span class="sxs-lookup"><span data-stu-id="93dec-102">A VM without the correct amount of memory or CPU will fail under load or run too slowly to be effective.</span></span> 

## <a name="pre-defined-vm-sizes"></a><span data-ttu-id="93dec-103">预定义的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="93dec-103">Pre-defined VM sizes</span></span>

<span data-ttu-id="93dec-104">创建虚拟机时, 可以提供_vm 大小_值, 用于确定将专门用于虚拟机的计算资源量。</span><span class="sxs-lookup"><span data-stu-id="93dec-104">When you create a virtual machine, you can supply a _VM size_ value that will determine the amount of compute resources that will be devoted to the VM.</span></span> <span data-ttu-id="93dec-105">这包括从 Azure 提供给虚拟机的 CPU、GPU 和内存。</span><span class="sxs-lookup"><span data-stu-id="93dec-105">This includes CPU, GPU, and memory that are made available to the virtual machine from Azure.</span></span>

<span data-ttu-id="93dec-106">Azure 为 Linux 和 Windows 定义一组预定义的 VM 大小, 以根据预期的使用情况进行选择。</span><span class="sxs-lookup"><span data-stu-id="93dec-106">Azure defines a set of pre-defined VM sizes for Linux and Windows to choose from based on the expected usage.</span></span> 

| <span data-ttu-id="93dec-107">类型</span><span class="sxs-lookup"><span data-stu-id="93dec-107">Type</span></span> | <span data-ttu-id="93dec-108">大小</span><span class="sxs-lookup"><span data-stu-id="93dec-108">Sizes</span></span> | <span data-ttu-id="93dec-109">说明</span><span class="sxs-lookup"><span data-stu-id="93dec-109">Description</span></span> |
|------|-------|-------------|
| <span data-ttu-id="93dec-110">常规用途</span><span class="sxs-lookup"><span data-stu-id="93dec-110">General purpose</span></span>   | <span data-ttu-id="93dec-111">Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7</span><span class="sxs-lookup"><span data-stu-id="93dec-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="93dec-112">平衡 CPU 与内存的平衡。</span><span class="sxs-lookup"><span data-stu-id="93dec-112">Balanced CPU-to-memory.</span></span> <span data-ttu-id="93dec-113">适用于开发/测试和中小型应用程序和数据解决方案。</span><span class="sxs-lookup"><span data-stu-id="93dec-113">Ideal for dev/test and small to medium applications and data solutions.</span></span> |
| <span data-ttu-id="93dec-114">计算优化</span><span class="sxs-lookup"><span data-stu-id="93dec-114">Compute optimized</span></span> | <span data-ttu-id="93dec-115">Fs、F</span><span class="sxs-lookup"><span data-stu-id="93dec-115">Fs, F</span></span> | <span data-ttu-id="93dec-116">CPU 内存较高。</span><span class="sxs-lookup"><span data-stu-id="93dec-116">High CPU-to-memory.</span></span> <span data-ttu-id="93dec-117">适用于中型流量的应用程序、网络设备和批处理过程。</span><span class="sxs-lookup"><span data-stu-id="93dec-117">Good for medium-traffic applications, network appliances, and batch processes.</span></span> |
| <span data-ttu-id="93dec-118">内存优化</span><span class="sxs-lookup"><span data-stu-id="93dec-118">Memory optimized</span></span>  | <span data-ttu-id="93dec-119">Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D</span><span class="sxs-lookup"><span data-stu-id="93dec-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="93dec-120">高内存到核心。</span><span class="sxs-lookup"><span data-stu-id="93dec-120">High memory-to-core.</span></span> <span data-ttu-id="93dec-121">非常适合关系数据库、大中型缓存和内存中的分析。</span><span class="sxs-lookup"><span data-stu-id="93dec-121">Great for relational databases, medium to large caches, and in-memory analytics.</span></span> |
| <span data-ttu-id="93dec-122">存储优化</span><span class="sxs-lookup"><span data-stu-id="93dec-122">Storage optimized</span></span> | <span data-ttu-id="93dec-123">!</span><span class="sxs-lookup"><span data-stu-id="93dec-123">Ls</span></span> | <span data-ttu-id="93dec-124">高磁盘吞吐量和 IO。</span><span class="sxs-lookup"><span data-stu-id="93dec-124">High disk throughput and IO.</span></span> <span data-ttu-id="93dec-125">是大型数据、SQL 和 NoSQL 数据库的理想选择。</span><span class="sxs-lookup"><span data-stu-id="93dec-125">Ideal for big data, SQL, and NoSQL databases.</span></span> |
| <span data-ttu-id="93dec-126">已优化 GPU</span><span class="sxs-lookup"><span data-stu-id="93dec-126">GPU optimized</span></span> | <span data-ttu-id="93dec-127">NV、NC</span><span class="sxs-lookup"><span data-stu-id="93dec-127">NV, NC</span></span> | <span data-ttu-id="93dec-128">专用虚拟机针对较重的图形呈现和视频编辑。</span><span class="sxs-lookup"><span data-stu-id="93dec-128">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span> |
| <span data-ttu-id="93dec-129">高性能</span><span class="sxs-lookup"><span data-stu-id="93dec-129">High performance</span></span> | <span data-ttu-id="93dec-130">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="93dec-130">H, A8-11</span></span> | <span data-ttu-id="93dec-131">具有可选高吞吐量网络接口 (RDMA) 的最强大的 CPU 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="93dec-131">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> | 

<span data-ttu-id="93dec-132">可用大小根据您要在其中创建虚拟机的区域而变化。</span><span class="sxs-lookup"><span data-stu-id="93dec-132">The available sizes change based on the region you're creating the VM in.</span></span> <span data-ttu-id="93dec-133">您可以使用`vm list-sizes`命令获取可用大小的列表。</span><span class="sxs-lookup"><span data-stu-id="93dec-133">You can get a list of the available sizes using the `vm list-sizes` command.</span></span> <span data-ttu-id="93dec-134">请尝试将此内容键入到 Azure 云命令行管理程序:</span><span class="sxs-lookup"><span data-stu-id="93dec-134">Try typing this into Azure Cloud Shell:</span></span>

```azurecli
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="93dec-135">以下是简短的响应`eastus`:</span><span class="sxs-lookup"><span data-stu-id="93dec-135">Here's an abbreviated response for `eastus`:</span></span>

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

## <a name="specifying-a-size-during-vm-creation"></a><span data-ttu-id="93dec-136">在创建 VM 期间指定大小</span><span class="sxs-lookup"><span data-stu-id="93dec-136">Specifying a size during VM creation</span></span>

<span data-ttu-id="93dec-137">我们在创建虚拟机时未指定大小, 因此 Azure 选择了默认的常规用途大小为 us `Standard_DS1_v2`。</span><span class="sxs-lookup"><span data-stu-id="93dec-137">We didn't specify a size when we created our VM - so Azure selected a default general-purpose size for us of `Standard_DS1_v2`.</span></span> <span data-ttu-id="93dec-138">但是, 可以使用`vm create` `--size`参数将大小指定为命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="93dec-138">However, we can specify the size as part of the `vm create` command using the `--size` parameter.</span></span> <span data-ttu-id="93dec-139">例如, 可以使用以下命令创建16核虚拟机:</span><span class="sxs-lookup"><span data-stu-id="93dec-139">For example, you could use the following command to create a 16-core virtual machine:</span></span>

```azurecli
az vm create --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM2 \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

> [!WARNING]
> <span data-ttu-id="93dec-140">您的订阅层对可以创建多少个资源以及这些资源的总大小[强制实施限制](https://docs.microsoft.com/azure/azure-subscription-service-limits)。</span><span class="sxs-lookup"><span data-stu-id="93dec-140">Your subscription tier [enforces limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) on how many resources you can create, as well as the total size of those resources.</span></span> <span data-ttu-id="93dec-141">例如, 您可以使用20个带即点即用订阅的**虚拟 cpu** , 并且每个免费的层仅有**4 个 vCPUs** 。</span><span class="sxs-lookup"><span data-stu-id="93dec-141">For example, you are capped to **20 virtual CPUs** with the pay-as-you-go subscription, and only **4 vCPUs** for a free tier.</span></span> <span data-ttu-id="93dec-142">当您超过此限制时, Azure CLI 将告知您**配额已超出**错误。</span><span class="sxs-lookup"><span data-stu-id="93dec-142">The Azure CLI will let you know when you exceed this with a **Quota Exceeded** error.</span></span> <span data-ttu-id="93dec-143">如果您在自己的付费订阅中遇到此错误, 您可以请求通过[免费的联机请求](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-quota-errors)提升与付费订阅关联的限制 (最高为 10000 vCPUs!)。</span><span class="sxs-lookup"><span data-stu-id="93dec-143">If you hit this error in your own paid subscription, you can request to raise the limits associated with your paid subscription (up to 10,000 vCPUs!) through a [free online request](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-quota-errors).</span></span>

## <a name="resizing-an-existing-vm"></a><span data-ttu-id="93dec-144">调整现有虚拟机的大小</span><span class="sxs-lookup"><span data-stu-id="93dec-144">Resizing an existing VM</span></span>
<span data-ttu-id="93dec-145">如果工作负载发生变化, 或者在创建时其大小不正确, 则还可以调整现有 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="93dec-145">We can also resize an existing VM if the workload changes, or if it was incorrectly sized at creation.</span></span> <span data-ttu-id="93dec-146">在请求调整大小之前, 必须检查 VM 所属的群集中是否提供了所需的大小。</span><span class="sxs-lookup"><span data-stu-id="93dec-146">Before a resize is requested, we must check to see if the desired size is available in the cluster our VM is part of.</span></span> <span data-ttu-id="93dec-147">可以使用以下`vm list-vm-resize-options`命令执行此操作:</span><span class="sxs-lookup"><span data-stu-id="93dec-147">We can do this with the `vm list-vm-resize-options` command:</span></span>

```azurecli
az vm list-vm-resize-options --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --output table
```

<span data-ttu-id="93dec-148">这将返回资源组中所有可用的大小配置的列表。</span><span class="sxs-lookup"><span data-stu-id="93dec-148">This will return a list of all the possible size configurations available in the resource group.</span></span> <span data-ttu-id="93dec-149">如果我们所需的大小在群集中不可用, __ 但在区域中可用, 则可以取消[分配 VM](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate)。</span><span class="sxs-lookup"><span data-stu-id="93dec-149">If the size we want isn't available in our cluster, but _is_ available in the region, we can [deallocate the VM](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate).</span></span> <span data-ttu-id="93dec-150">此命令将停止运行中的 VM 并将其从当前群集中删除, 而不会丢失任何资源。</span><span class="sxs-lookup"><span data-stu-id="93dec-150">This command will stop the running VM and remove it from the current cluster without losing any resources.</span></span> <span data-ttu-id="93dec-151">然后, 可以调整它的大小, 这将在大小配置可用的新群集中重新创建 VM。</span><span class="sxs-lookup"><span data-stu-id="93dec-151">Then we can resize it, which will re-create the VM in a new cluster where the size configuration is available.</span></span>

> [!NOTE]
> <span data-ttu-id="93dec-152">Azure 沙盒仅限于少数几个 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="93dec-152">The Azure sandbox is limited to a few VM sizes.</span></span> <span data-ttu-id="93dec-153">在免费的 Microsoft 学习订阅中不允许大多数可能性。</span><span class="sxs-lookup"><span data-stu-id="93dec-153">Most of the possibilities are not allowed in the free Microsoft Learn subscription.</span></span>

<span data-ttu-id="93dec-154">若要调整虚拟机的大小, `vm resize`请使用命令。</span><span class="sxs-lookup"><span data-stu-id="93dec-154">To resize a VM, we use the `vm resize` command.</span></span> <span data-ttu-id="93dec-155">例如, 我们可能会发现, 我们的 VM 是我们希望 it 执行的任务的 underpowered。</span><span class="sxs-lookup"><span data-stu-id="93dec-155">For example, perhaps we find our VM is underpowered for the task we want it to perform.</span></span> <span data-ttu-id="93dec-156">我们可以将它增大到 DS3_v2 层, 在其中有 4 vCores 和14G 内存的情况。</span><span class="sxs-lookup"><span data-stu-id="93dec-156">We could bump it up a few levels to a DS3_v2 tier where it has 4 vCores and 14G of memory.</span></span> <span data-ttu-id="93dec-157">在云命令行管理程序中键入以下命令:</span><span class="sxs-lookup"><span data-stu-id="93dec-157">Type this command in Cloud Shell:</span></span>

```azurecli
az vm resize --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --size Standard_DS3_v2
```

<span data-ttu-id="93dec-158">此命令将需要几分钟的时间来减小 VM 的资源, 完成后, 将返回新的 JSON 配置。</span><span class="sxs-lookup"><span data-stu-id="93dec-158">This command will take a few minutes to reduce the resources of the VM, and once it's done, it will return a new JSON configuration.</span></span>