让我们从最显而易见的任务入手: 创建 Azure 虚拟机。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="logins-subscriptions-and-resource-groups"></a>登录、订阅和资源组

你将在右侧的 Azure 云命令行管理程序中工作。 激活沙盒后, 你将通过 Microsoft 学习管理的免费订阅登录 Azure。 您不必登录 Azure, 也不必选择订阅-这将为您完成。 此外, 通常会创建一个_资源组_来保存新资源。 在此模块中, Azure 沙盒将为您创建一个资源组, 该资源组将用于执行所有命令。

## <a name="create-a-linux-vm-with-the-azure-cli"></a>使用 Azure CLI 创建 Linux VM

azure CLI 包括使用 Azure `vm`中的虚拟机的命令。 我们可以提供几个子命令来完成特定任务。 最常见的包括:

| 子命令 | 说明 |
|-------------|-------------|
| `create`    | 创建新的虚拟机 |
| `deallocate` | 解除分配虚拟机 |
| `delete` | 删除虚拟机 |
| `list` | 列出订阅中创建的虚拟机 |
| `open-port` | 为入站流量打开特定的网络端口 |
| `restart` | 重新启动虚拟机 |
| `show` | 获取虚拟机的详细信息 |
| `start` | 启动已停止的虚拟机 |
| `stop` | 停止正在运行的虚拟机 |
| `update` | 更新虚拟机的属性 |

> [!NOTE]
> 有关命令的完整列表, 可以查看[Azure CLI 参考文档](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)。

让我们从第一个开始: `az vm create`。 此命令用于在资源组中创建虚拟机。 您可以通过多个参数来配置新 VM 的所有方面。 必须提供的三个参数为:

> [!div class="mx-tableFixed"]
> | 参数 | 说明 |
> |-----------|-------------|
> | `resource-group` | 将拥有虚拟机的资源组, 请使用**<rgn>[沙盒资源组]</rgn>**。 |
> | `name` | 虚拟机的名称-在资源组中必须是唯一的。 |
> | `image` | 用于创建虚拟机的操作系统映像。 |
> | `location` | 要放置 VM 的区域。 通常情况下, 这将接近 VM 的使用者。 在本练习中, 请从以下列表中选择邻近的位置。 |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

此外, 在创建 VM 时添加`--verbose`标志以查看进度很有帮助。 

## <a name="create-a-linux-virtual-machine"></a>创建 Linux 虚拟机

让我们创建一个新的 Linux 虚拟机。 在 Azure 云命令行管理程序中执行以下命令, 以在 "West US" 位置创建 Debian Linux 计算机。 如果不是附近, 请更改位置。

```azurecli
az vm create --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --location westus --verbose 
```

[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


此命令将创建一个名**** `SampleVM`为的新 Debian Linux 虚拟机。 请注意, 在创建虚拟机时, Azure CLI 工具将等待。 您可以添加`--no-wait`选项以通知 azure CLI 工具立即返回, 并让 azure 继续在后台创建 VM。 如果要在脚本中执行命令, 这将非常有用。 稍后在脚本中, 使用`azure vm wait --name [vm-name]`命令等待 VM 完成创建。

如果你查看详细响应, 你还会看到`SampleVM`名称用于为 VM 命名各种依赖项。

```output
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

您可以使用可选参数`vm create`(如`--vnet-name`和`--public-ip-address-dns-name`) 替代这些自动生成的资源名称。

我们正在通过`admin-username`标记指定 **"aldis"** 的管理员帐户名称。 如果省略此名称, 则`vm create`该命令将使用您的_当前用户名_。 由于每个 OS 的帐户名称规则各不相同, 因此指定特定名称比较安全。 

> [!NOTE]
> 大多数图像不允许使用常见名称, 例如 "root" 和 "admin"。

我们也在使用此`generate-ssh-keys`标志。 此参数用于 Linux 分发, 并创建一对安全密钥, 以便我们可以使用该`ssh`工具远程访问虚拟机。 这两个文件放入您`.ssh`的计算机上的文件夹中, 在 VM 中。 如果目标文件夹中已有名为`id_rsa`的 SSH 密钥, 则将使用它, 而不是生成新密钥。

完成创建 VM 后, 你将获得一个 JSON 响应, 该响应包括 Azure 分配的虚拟机及其公用和专用 IP 地址的当前状态:

```json
{
  "fqdns": "",
  "id": "/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "westus",
  "macAddress": "00-0D-3A-58-F8-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
  "resourceGroup": "2568d0d0-efe3-4d04-a08f-df7f009f822a",
  "zones": ""
}
```
