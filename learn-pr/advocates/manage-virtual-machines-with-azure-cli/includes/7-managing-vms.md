在运行虚拟机的过程中, 您需要执行的主要任务之一是启动和停止它们。

## <a name="stopping-a-vm"></a>停止 VM

可以使用`vm stop`命令停止正在运行的虚拟机。 您必须为 VM 传递名称和资源组或唯一 ID:

```azurecli
az vm stop -n SampleVM -g <rgn>[sandbox resource group name]</rgn>
```

我们可以通过尝试 ping 公共 IP 地址、使用`ssh`或通过`vm get-instance-view`命令来验证它是否已停止。 这一最终方法返回相同的基本数据`vm show` , 但包含有关实例本身的详细信息。 尝试在 Azure 云命令行管理程序中键入以下命令, 以查看 VM 的当前运行状态:

```azurecli
az vm get-instance-view -n SampleVM -g <rgn>[sandbox resource group name]</rgn> --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

此命令应返回`VM stopped`结果。

## <a name="starting-a-vm"></a>启动 VM

我们可以通过`vm start`命令反向执行。

```azurecli
az vm start -n SampleVM -g <rgn>[sandbox resource group name]</rgn>
```

此命令将启动已停止的 VM。 我们可以通过`vm get-instance-view`查询验证它, 现在应返回`VM running`。

## <a name="restarting-a-vm"></a>重新启动 VM

最后, 如果我们已进行了需要使用`vm restart`命令重新启动的更改, 则可以重新启动 VM。 如果希望 Azure CLI `--no-wait`立即返回, 而不等待 VM 重新启动, 则可以添加标志。

