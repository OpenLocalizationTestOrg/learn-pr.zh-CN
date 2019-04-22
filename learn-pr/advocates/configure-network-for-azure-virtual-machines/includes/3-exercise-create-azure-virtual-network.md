在本练习中, 你将在 Microsoft Azure 中创建虚拟网络。 然后, 创建两个虚拟机, 并使用虚拟网络将虚拟机和 Internet 连接到 Internet。

> [!IMPORTANT]
> 此模块中的练习需要完整的 Azure 订阅。 练习是可选的, 不需要完成此模块。 参加本模块中的交互式练习将会向你用来完成它们的 Azure 订阅收取费用。  通过尽可能快地清除所创建的资源, 可以最大限度地减少费用。 清理方向在最后单位中。

## <a name="log-in-to-your-subscription-with-the-azure-cli"></a>使用 Azure CLI 登录到你的订阅

本第一个练习将使用 Azure CLI。 如果你有 Azure CLI 的本地安装, 请不要使用它&mdash; 。请确保使用`az account`登录到要使用的订阅。 如果不是, 可以登录到[shell.azure.com](https://shell.azure.com)上的 Azure 帐户, 并从那里使用命令行管理程序。

> [!NOTE]
> 如果使用的是 CloudShell 环境, 请选择**Bash**命令行管理程序选项。 如果您在本地或在云中使用 PowerShell, 则需要通过更改`""`为`'""'`将空字符串正确地传递到命令中来对所有空参数进行转义。 如果不这样做, PowerShell 不会传递空字符串, 并且将从命令中收到一个错误, 指示它缺少参数。

## <a name="create-a-resource-group"></a>创建资源组

首先, 创建一个资源组, 以包含您将在此模块中创建的所有资源。 将其`vm-networks`命名。

```azurecli
az group create --name vm-networks
```

## <a name="create-a-virtual-network"></a>创建虚拟网络

若要创建虚拟网络, 请输入以下命令, 然后按 enter。

```azurecli
az network vnet create \
    --name myVnet \
    --resource-group vm-networks \
    --subnet-name default
```

## <a name="create-two-virtual-machines"></a>创建两台虚拟机

所有 Azure 虚拟机都已连接到虚拟网络。 如果使用 Azure CLI 创建虚拟机, 但未指定现有虚拟网络的名称, 则 CLI 将根据位置和子网的可用性搜索相应虚拟网络的目标资源组。 如果找不到匹配项, 则会自动创建一个新的虚拟网络。

在这里, 我们创建两个虚拟机, 而不指定任何虚拟网络信息。 默认网络规范与的`myVnet`属性相匹配, 因此 CLI 将自动找到并使用它。

1. 若要创建第一台虚拟机, 请执行以下命令, 创建具有可通过端口 3389 (远程桌面) 访问的公共 IP 地址的 Windows VM。 这将创建一个名为`dataProcStage1`的 Windows 2016 数据中心虚拟机。

    ```azurecli
    az vm create \
        --name dataProcStage1 \
        --resource-group vm-networks \
        --admin-username "DataAdmin" \
        --image Win2016Datacenter
    ```

1. 在提示符处为你的密码提供值。 请记住, 请记下此密码, 因为稍后你将需要它来访问服务器。

1. 从创建您的 VM 复制返回的 JSON 中的**publicIpAddress**值, 以便以后可以使用它。

1. 现在, 你将创建第二个 VM。 此 VM 将被命名`dataProcStage2` , 并且不会有公用 IP 地址。

    ```azurecli
    az vm create \
        --name dataProcStage2 \
        --resource-group vm-networks \
        --public-ip-address "" \
        --admin-username "DataAdmin" \
        --image Win2016Datacenter
    ```

## <a name="connect-to-dataprocstage1-using-remote-desktop"></a>使用远程桌面连接到 dataProcStage1

1. 打开 "远程桌面", `dataProcStage1`并使用前面步骤中提到的公共 IP 地址连接到。

1. 使用您创建的用户名`DataAdmin`和密码登录到远程计算机。

1. 在远程会话中, 打开 Windows 命令提示符, 然后运行以下命令:

    ```cmd
    ping dataProcStage2 -4
    ```

1. 在结果中, 您将看到所有请求`dataProcStage2`超时。这是因为中`dataProcStage2`的默认 Windows 防火墙配置会阻止它响应 ping。

## <a name="connect-to-dataprocstage2-using-remote-desktop"></a>使用远程桌面连接到 dataProcStage2

你将`dataProcStage2`使用新的远程桌面会话配置 Windows 防火墙。 但是, 你将无法从你的`dataProcStage2`桌面进行访问。 撤回, `dataProcStage2`不具有公共 IP 地址。 您将使用的`dataProcStage1`远程桌面连接到。 `dataProcStage2`

1. 在`dataProcStage1`远程会话中, 打开 "远程桌面"。

1. 按名称`dataProcStage2`连接到。 根据默认网络配置, `dataProcStage1`可以解析`dataProcStage2`使用计算机名称的地址。

1. 使用您创建`dataProcStage2`的用户名`DataAdmin`和密码登录到。

1. 在`dataProcStage2`上, 单击 "开始" 菜单, 键入**Firewall**, 然后按 enter。 将显示 "**高级安全 Windows 防火墙**" 控制台。

1. 在左侧窗格中, 单击 "**入站规则**"。

1. 在右侧窗格中, 向下滚动, 右键单击 "**文件和打印机共享 (回显请求-icmpv4-in)**", 然后单击 "**启用规则**"。

1. 切换回`dataProcStage1`远程会话, 并在命令提示符处运行以下命令。

    ```cmd
    ping dataProcStage2 -4
    ```

1. `dataProcStage2`响应四个答复, 演示两个虚拟机之间的连接。

您已成功创建虚拟网络, 创建了连接到该虚拟网络的两个虚拟机, 连接到其中一个 vm 并在同一虚拟网络中显示到其他 vm 的网络连接。 您可以使用 azure 虚拟网络连接 azure 网络中的资源。 但是, 这些资源必须位于相同的资源组和订阅中。 接下来, 我们将看一下 VPN 网关, 它使你能够在不同的资源组、订阅甚至地理区域中连接虚拟网络。
