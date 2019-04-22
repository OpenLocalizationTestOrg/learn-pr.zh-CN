作为贵公司的软件开发人员, 您有机会扩大技能并成为内部的 AI 团队的一部分。 在你向你提升此激动人心的新角色时, 你仍需要执行日常工作。 您的团队的高级 AI 工程师已告知您一些有用的 Jupyter 笔记本, 这些笔记本具有基于 PyTorch 的实验室来培训图像分类模型。 令人兴奋的内容, 但您不想将一组框架安装到 dev 远程测试机组中。 而是决定创建基于数据科学虚拟机 (DSVM) 图像的虚拟机。 

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-the-azure-cli"></a>什么是 Azure CLI

azure CLI 是 Microsoft 的用于管理 Azure 资源的跨平台命令行工具。 它可用于 macOS、Linux 和 Windows, 也可用于使用[Azure 云命令行](https://docs.microsoft.com/azure/cloud-shell/overview)管理程序的浏览器。 我们完全覆盖了在使用**CLI 模块控制 Azure 服务时**使用此工具。

## <a name="managing-deployments"></a>管理部署

azure CLI 包含用于管理`az group deployment` Azure 资源管理器部署的命令。 我们可以提供几个子命令来完成特定任务。 最常见的包括:

| 子命令 | 说明 |
|-------------|-------------|
| `create` | 启动部署。 |
| `list` | 获取资源组的所有部署。 |
| `export` | 导出用于部署的模板。 |

有关可用部署命令的完整列表, 请参阅[az group deployment command reference](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)

我们将使用`az group deployment create`预配虚拟机。

## <a name="create-a-json-deployment-parameters-file"></a>创建 JSON 部署参数文件

我们要使用 Azure 资源管理器模板创建虚拟机。 模板定义要预配的 Linux DSVM 映像。 我们需要为模板提供一些参数, 如我们要使用的 VM 大小、管理员用户名和密码以及我们的计算机的主机名。 

1. 在此单元右侧的 Azure 云命令行管理程序中执行以下命令:

    ```azurecli
    code .
    ```
    <!-- TODO add a link to official doc that explains the built-in editor when it becomes available -->
    此命令将在内置编辑器中打开和清空文件。 

1. 将下面的 JSON 代码片段粘贴到代码编辑器中的空文件中。

    ```json
    { 
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
         "adminUsername": { "value" : "<USERNAME>"},
         "adminPassword": { "value" : "<PASSWORD>"},
         "vmName": { "value" : "<HOSTNAME>"},
         "vmSize": { "value" : "Standard_DS2_v2"},
      }
    }
    ```

1. 更新在编辑器中粘贴的 JSON 中的以下参数:

    |参数  |当前值  |您的值  |
    |---------|---------|---------|
    |adminUsername     |  `<USERNAME>`       |    为此新计算机的管理员用户选择一个名称, 例如, *azuser*。     |
    |adminPassword     |  `<PASSWORD>`       |   为此管理员用户帐户选择密码。 若要了解有关密码要求的详细信息, 请参阅[有关 Linux 虚拟机的常见问题](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)     |
    |vmName     |   `<HOSTNAME>`      |  选择新虚拟机的名称。 您的名称必须以字母开头, 并且只能包含小写字母和数字。 请尝试选择一个唯一的名称, 例如, 其中包含你的缩写和出生年份。 |
    |vmSize     |  Standard_DS2_v2       |  此 VM 大小在此练习中将正常运行, 但你可以随意进行更改。 此处的可用 vm 大小列表可在此处找到[Azure 中的 Linux 虚拟机的大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)       |

1. 选择编辑器右上部的三个省略号 (**...**), 然后从菜单中选择 "**保存**", 以将文件保存为`parameter_file.json`并关闭文本编辑器。

    > [!IMPORTANT]
    > 请记住您为 adminUsername、adminPassword 和 vmName 选择的值。 我们将在此练习中再次使用它们。

## <a name="create-a-resource-group"></a>创建资源组 

> [!IMPORTANT]
> 通常情况下, 您需要在所选的区域中创建资源组。 但是, 当前正在提供的沙盒会话提供了要使用的资源组。 此会话的资源组为**<rgn>[沙盒资源组名称]</rgn>**。

## <a name="deploy-the-dsvm-to-your-resource-group"></a>将 DSVM 部署到您的资源组

现在, 我们有一个资源组, 并且已在名`parameter_file.json`为的文件中为 DSVM 资源管理器模板定义了参数。 我们将运行`az group deployment create`下一步来设置虚拟机。

1. 在 Azure 云命令行管理程序中执行以下命令:

    ```azurecli
    az group deployment create \
    --resource-group  <rgn>[sandbox resource group name]</rgn> \
    --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json \
    --parameters parameter_file.json
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    该命令使用资源管理器模板和我们的参数在资源组中创建虚拟机。 

2. 部署虚拟机需要几分钟时间才能完成。 控制台在操作` - Running ..`完成之前会显示, 而不是其他内容。 操作完成后, 会将 JSON 响应输出到屏幕。 滚动到 JSON 的底部, 并检查字段 **"provisioningState"** 的值是否已*成功*。

    > [!TIP]
    > 如果您收到一条错误, 指出 DNS 记录已被另一个公共 IP 使用, 请尝试**** `parameter_file.json`将 vmName 更改为另一个唯一的名称。

3. 执行以下命令以获取有关 vm 的信息, 并用您`<HOSTNAME>`为 VM 定义的主机名称替换。

    ```azurecli
    az vm show -d \
    --name <HOSTNAME> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --output table
    ```

    此命令将显示 VM 的状态。 **PowerState**字段应指示*运行的虚拟机*。 在本练习后面的部分中, 我们将使用**PublicIps**字段中的 IP 地址连接到 VM。 我们还可以使用此处的 " **fqdn** " 字段中显示的完全限定的域名 (FQDN) 进行连接。

!! 您已创建并部署基于 DSVM 映像的 Linux VM。

## <a name="open-the-vm-to-ssh-traffic-on-port-22"></a>在端口22上打开 VM 到 ssh 流量

默认情况下, 我们的虚拟机不会打开任何端口。 我们的目标是远程连接、启动 Jupyter 笔记本服务器并在计算机上运行其他本地命令。 若要使用安全命令行管理程序 (SSH) 协议将远程登录到 VM, 我们需要打开端口。 端口22是 ssh 的默认端口。  

1. 在 Azure 云命令行管理程序中执行以下`<HOSTNAME>`命令, 并将其替换为安装过程中为虚拟机提供的名称。 

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 22 \
    --priority 900
    ```

此命令最长可能需要一分钟才能完成。 命令完成后, 它会将 JSON 响应返回到命令行。 检查字段 **"provisioningState"** 的值是否已*成功*。 我们将测试 ssh 是否很快工作, 但首先让我们打开一个更多的端口。

## <a name="open-the-vm-to-access-the-jupyter-notebook-server-remotely"></a>打开 VM 以远程访问 Jupyter 笔记本服务器

如前所述, DSVM 映像是预安装的软件、工具和示例, 可帮助你使用数据科学、机器学习和深入学习项目。 Jupyter 与示例笔记本一起安装在映像中。 我们想要在 VM 上启动一个 Jupyter 笔记本服务器, 然后从我们的本地计算机远程连接到该笔记本服务器。 默认情况下, 笔记本服务器在端口8888上运行。 若要远程访问服务器, 我们需要在虚拟机上打开该端口。 

1. 在 Azure 云命令行管理程序中执行以下`<HOSTNAME>`命令, 并将其替换为在安装过程中为 DSVM 虚拟机提供的名称。

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 8888 \
    --priority 901
    ```

同样, 此命令最长可能需要一分钟才能完成。 命令完成后, 它会将 JSON 响应返回到命令行。 检查字段 **"provisioningState"** 的值是否已*成功*。  

## <a name="connect-to-the-vm-with-secure-shell-ssh"></a>使用安全命令行管理程序 (ssh) 连接到 VM

1. 在 Azure 云命令行管理程序中执行以下命令, 以查找 VM 的公共 IP 地址。 将`<HOSTNAME>`替换为您在安装过程中为 DSVM 虚拟机提供的名称。

    ```azurecli
    az vm list-ip-addresses \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --output table
    ```

1. 在云命令行管理程序中执行以下命令, 以登录到 VM。 将`<USERNAME>`替换为您在本练习开始时选择的用户名。 将`<IP>`替换为上一步的**PublicIPAddresses**列中的值。

    例如, 如果您选择的用户名为*azuser* , 而 PublicIPAddresses 的值为 33.165.103.23, 则此命令将会读取:
    
    `ssh azuser@33.165.103.23`
    
    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 

1. 出现提示时, 请输入您在本练习开始时选择的管理员用户的密码。 成功登录后, 提示应更改为格式`username@hostname`, 例如。 `azuser@js1982`

下一步是在虚拟机上启动 Jupyter 笔记本服务器并远程打开笔记本。

## <a name="start-the-jupyter-notebook-server-on-the-vm"></a>启动 VM 上的 Jupyter 笔记本服务器

VM 的`~/notebooks`文件夹中有一组笔记本。 假定您仍通过 SSH 会话登录, 请启动笔记本服务器并打开其中一个笔记本以确保一切正常工作。


1. 在 VM 的命令提示符处运行以下命令:

    ```bash
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

> [!CAUTION]
> 在此练习中, 对笔记本服务器的访问`http://`发生。 如果要在公用中运行笔记本服务器, 应对其进行保护。 有关保护笔记本服务器的详细信息, 请参阅官方 Jupyter 文档 online。 

在上面的命令中, 我们使用`jupyter notebook`命令启动 Jupyter 笔记本服务器。 我们提供了三个重要的命令行参数。 请记住, 我们是通过控制台远程登录到此计算机的。 笔记本在浏览器中提供。 

 - `--ip=0.0.0.0`默认情况下, 笔记本服务器在 127.0.0.1: 8888 处本地运行, 并且只能从 localhost 访问。 您可以使用http://127.0.0.1:8888从本地浏览器访问笔记本服务器。 将 "IP 地址" 设置为0.0.0.0 将告知服务器侦听所有 ip 上的流量。 如果笔记本服务器以0.0.0.0 监听, 则可以通过主机的 IP 地址访问它。  
 - `--no-browser`由于我们要通过 internet 从另一台计算机连接到笔记本, 因此我们将笔记本服务器配置为不打开浏览器, 这是默认行为。 
 - `--allow-root`在本练习中, 我们仅在 VM 上拥有管理员帐户, 因此我们希望能够以根身份运行笔记本。

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a>从远程浏览器连接到 Jupyter 笔记本服务器

当上述命令在 VM 上运行时, 笔记本服务器将启动, 控制台将显示 URL, 以便您在浏览器中使用。 

![在控制台中显示运行笔记本服务器的消息的屏幕截图, 其中包含从主机访问服务器的 URL](../media/notebook-url.png)

1. 复制笔记本服务器显示在您喜爱的浏览器的地址栏中的 URL。 您还可以单击 URL 以在默认浏览器中打开。 

    你将收到 "无法访问网站" 消息, 因为你提供的 URL 是从主机到笔记本服务器的连接。

1. 若要远程访问服务器, 请将 URL 中的主机名替换为先前保存的 VM 的 IP 地址。 

    下面是一个示例笔记本服务器 URL。

    ́http//**ab-dsvm-4**: 8888/?token = {某个令牌} ́

    在这种情况下, 我们会将**ab-4**替换为计算机的 IP 地址 dsvm。 如果我们的 IP 地址`52.175.199.43`为, 则 URL 将变为:

    ́http://**52.175.199.43**: 8888/?token = {某个令牌} ́

    请确保`:8888`URL 中保留了端口地址。

    > [!TIP]
    > 如果不想使用 IP 地址, 则还可以使用窗体中的完全限定的服务器名称`<HOST NAME>.<REGION>.cloudapp.azure.com`

    下面的屏幕截图显示 Jupyter 仪表板在浏览器中的外观。

    ![显示 Jupyter 笔记本仪表板的屏幕截图。 ](../media/jupyter-in-browser.png)

1. 导航到 "**笔记本/IntroToJupyterPython** ", 然后选择它。 尝试此笔记本以验证所有内容是否按预期工作。

    !! 现在, 您运行的是基于 DSVM 的虚拟机, 可以使用 Jupyter 远程工作。 在本练习中, 我们运行的是在 VM 上安装的软件。 在下一个练习中, 我们会将软件隔离在 VM 上的容器中, 以便我们可以进行自信体验。

4. 完成笔记本后, 可以`Control-C`在云命令行管理程序中停止 Jupyter 服务器。
