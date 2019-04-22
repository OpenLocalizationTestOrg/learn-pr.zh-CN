<span data-ttu-id="de3c8-101">在运行虚拟机的过程中, 您需要执行的主要任务之一是启动和停止它们。</span><span class="sxs-lookup"><span data-stu-id="de3c8-101">One of the main tasks you'll want to do while running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="de3c8-102">停止 VM</span><span class="sxs-lookup"><span data-stu-id="de3c8-102">Stopping a VM</span></span>

<span data-ttu-id="de3c8-103">可以使用`vm stop`命令停止正在运行的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="de3c8-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="de3c8-104">您必须为 VM 传递名称和资源组或唯一 ID:</span><span class="sxs-lookup"><span data-stu-id="de3c8-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="de3c8-105">我们可以通过尝试 ping 公共 IP 地址、使用`ssh`或通过`vm get-instance-view`命令来验证它是否已停止。</span><span class="sxs-lookup"><span data-stu-id="de3c8-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="de3c8-106">这一最终方法返回相同的基本数据`vm show` , 但包含有关实例本身的详细信息。</span><span class="sxs-lookup"><span data-stu-id="de3c8-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="de3c8-107">尝试在 Azure 云命令行管理程序中键入以下命令, 以查看 VM 的当前运行状态:</span><span class="sxs-lookup"><span data-stu-id="de3c8-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g <rgn>[sandbox resource group name]</rgn> --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

<span data-ttu-id="de3c8-108">此命令应返回`VM stopped`结果。</span><span class="sxs-lookup"><span data-stu-id="de3c8-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="de3c8-109">启动 VM</span><span class="sxs-lookup"><span data-stu-id="de3c8-109">Starting a VM</span></span>

<span data-ttu-id="de3c8-110">我们可以通过`vm start`命令反向执行。</span><span class="sxs-lookup"><span data-stu-id="de3c8-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="de3c8-111">此命令将启动已停止的 VM。</span><span class="sxs-lookup"><span data-stu-id="de3c8-111">This command will start a stopped VM.</span></span> <span data-ttu-id="de3c8-112">我们可以通过`vm get-instance-view`查询验证它, 现在应返回`VM running`。</span><span class="sxs-lookup"><span data-stu-id="de3c8-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="de3c8-113">重新启动 VM</span><span class="sxs-lookup"><span data-stu-id="de3c8-113">Restarting a VM</span></span>

<span data-ttu-id="de3c8-114">最后, 如果我们已进行了需要使用`vm restart`命令重新启动的更改, 则可以重新启动 VM。</span><span class="sxs-lookup"><span data-stu-id="de3c8-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="de3c8-115">如果希望 Azure CLI `--no-wait`立即返回, 而不等待 VM 重新启动, 则可以添加标志。</span><span class="sxs-lookup"><span data-stu-id="de3c8-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

