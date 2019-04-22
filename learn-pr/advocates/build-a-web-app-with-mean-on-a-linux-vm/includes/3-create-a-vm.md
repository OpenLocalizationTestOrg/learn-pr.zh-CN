与大多数应用程序框架一样, 您可以在许多不同的环境中运行您的平均堆栈应用程序。 您可以在服务器机房、VM 或容器上的物理计算机上运行应用程序。

在这里, 你将在 Azure 上运行的 VM 上运行你的应用程序。 均值支持许多不同的操作系统。 为了便于学习, 您将使用 Ubuntu Linux。

## <a name="create-an-ubuntu-linux-vm"></a>创建 Ubuntu Linux 虚拟机

[!include[](../../../includes/azure-sandbox-activate.md)]

通常情况下, 先创建_资源组_, 然后再在 Azure 上创建其他资源。 资源组将相关资源分组。 Azure 沙盒为你提供了资源组。 当您在自己的 Azure 订阅中工作时, 请使用以下命令在你附近的位置创建资源组。

```azurecli
az group create \
  --name <resource-group-name> \
  --location <resource-group-location>
```

1. 从云命令行管理程序`az vm create`中, 运行命令以创建 Ubuntu VM。

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name MeanStack \
      --image UbuntuLTS \
      --admin-username azureuser \
      --generate-ssh-keys
    ```

    此命令大约需要两分钟才能完成。 命令完成后, 你将看到类似于此的输出。

    ```json
    {
      "fqdns": "",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/MeanStack",
      "location": "eastus",
      "macAddress": "00-0D-3A-1E-1B-3B",
      "powerState": "VM running",
      "privateIpAddress": "10.0.0.5",
      "publicIpAddress": "104.211.9.245",
      "resourceGroup": "<rgn>[sandbox resource group name]</rgn>",
      "zones": ""
    }
    ```

    VM 的名称为 "MeanStack"。 你将在将来的命令中使用此名称来标识你要使用的 VM。

1. 打开 VM 上的端口 80, 以允许传入的 HTTP 流量到您稍后创建的 web 应用程序。

    ```azurecli
    az vm open-port \
      --port 80 \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name MeanStack
    ```

1. 创建到你的 VM 的 SSH 连接。

    尽管`az vm create`命令的输出显示你的 VM 的公共 IP 地址, 但你可能会发现将地址存储在 Bash 变量中非常有用。

    从运行`az vm show`。 此命令将 IP 地址保存在名为`ipaddress`的 Bash 变量中。

    ```azurecli
    ipaddress=$(az vm show \
      --name MeanStack \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --show-details \
      --query [publicIps] \
      --output tsv)
    ```

    连接到你的 VM, 如下所示。

    ```bash
    ssh azureuser@$ipaddress
    ```

    出现提示时, 回答 "是" 以在本地保存 VM 的标识, 以便将来的连接受到信任。

    保持 SSH 连接处于打开状态。 你将使用它在下一部分中配置软件。

## <a name="summary"></a>摘要

使用 Ubuntu VM 准备就绪后, 即可安装平均堆栈的每个组件。 首先, 你将安装 MongoDB。