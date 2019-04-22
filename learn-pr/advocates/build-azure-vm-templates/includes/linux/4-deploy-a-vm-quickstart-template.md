在这里, 你将部署在上一部分中研究过的快速入门模板。 快速入门模板将显示基本的虚拟机配置。

在执行此操作之前, 让我们先简单回顾一下部署过程。

[!include[](../../../../includes/azure-sandbox-activate.md)]

## <a name="how-do-i-deploy-a-resource-manager-template"></a>如何部署资源管理器模板？

您可以使用自动化脚本工具 (例如 azure CLI、azure PowerShell) 甚至 azure REST api 和喜欢的编程语言从模板部署资源。 您还可以通过 visual studio、visual studio Code 和 Azure 门户部署你的模板。 很快, 你将使用云命令行管理程序中的 Azure CLI 部署资源管理器模板。

### <a name="verifying-a-template"></a>验证模板

在运行模板之前, 您可能需要先验证它。

最好的第一步是使用_linter_处理模板, 这是一种验证模板的 JSON 语法是否正确的工具。 您可以找到在命令行、浏览器或您喜爱的代码编辑器中运行的 JSON linting 工具。

> [!TIP]
> Visual Studio Code 提供了许多[内置功能](https://code.visualstudio.com/docs/languages/json?azure-portal=true), 使您可以更轻松地使用 JSON 文件。 你的常用编辑器可能会提供类似的内置功能或插件。

下一步是将模板可视化。 通过[Azure 资源管理器可视化工具](http://armviz.io?azure-portal=true), 您可以上传资源管理器模板, 并以图形方式查看您的资源与其他项之间的关系。 您可以检查此可视化效果, 以验证是否正确设置了部署并满足您的要求。

最后, 您可以从 azure CLI 或 azure PowerShell 执行测试部署。 测试部署不会创建任何资源, 但它会为您提供有关部署运行时所发生情况的反馈。 你将很快执行测试部署, 以了解操作过程。

## <a name="creating-resources-in-azure"></a>在 Azure 中创建资源

通常, 我们要做的第一件事是创建一个_资源组_来保留我们需要创建的所有内容。 这使我们能够管理所有虚拟机、磁盘、网络接口以及构成作为一个整体的解决方案的其他元素。 我们可以使用 Azure CLI 创建包含`az group create`命令的资源组。 `--name`在我们的订阅中让其具有唯一名称, 并`--location`告知 Azure 我们希望在默认情况下放置资源的世界领域。

由于我们处于免费的 Azure 沙盒环境中, 因此您无需执行此步骤, 而是使用预创建的资源组**<rgn>[资源组名称]</rgn>**。

## <a name="create-template-parameters"></a>创建模板参数

回想一下, 资源管理器模板划分为多个部分, 其中一个是**参数**。

在模板的开头附近, 您会看到一个名为`parameters`的节。 本部分将定义这五个参数:

* `adminUsername`
* `adminPassword`
* `dnsLabelPrefix`
* `ubuntuOSVersion`
* `location`

![模板的 parameters 部分的源代码, 突出显示每个参数名称](../../media/4-armviz-params-linux.png)

这两个参数&ndash; `ubuntuOSVersion`中`location` &ndash;的两个, 它们都具有默认值。 的默认值`ubuntuOSVersion`为 "16.04.0-LTS", 其默认值`location`为父资源组的位置。

让我们将这些参数保留为其默认值。 对于其余的三个参数, 您有两个选项:

1. 提供 JSON 文件中的值。
1. 提供值作为命令行参数。

为便于学习, 您将提供值作为命令行参数。 若要使模板易于部署, 首先需要将这些值存储为 Bash 变量。

1. 从云命令行管理程序创建用户名。 对于此示例, 我们使用**azureuser**。

    ```bash
    USERNAME=azureuser
    ```

1. 运行**openssl**实用工具以生成随机密码。

    ```bash
    PASSWORD=$(openssl rand -base64 32)
    ```

    生成随机密码的方式有很多种。 您选择的方法取决于您的工作流和要求。 此方法使用**openssl**实用工具生成32随机字节, 而 base64 则对输出进行编码。 Base64 编码可确保结果仅包含可打印字符。

1. 生成唯一的 DNS 标签前缀。

    ```bash
    DNS_LABEL_PREFIX=mydeployment-$RANDOM
    ```

    DNS 标签前缀必须是唯一的。 DNS 标签前缀以 "mydeployment" 开头, 后跟一个随机数字。 `$RANDOM`是一个 Bash 函数, 它生成随机正整数。

    在实践中, 您将选择符合要求的 DNS 标签前缀。

## <a name="validate-and-launch-the-template"></a>验证并启动模板

参数准备就绪后, 您就拥有启动模板所需的一切。

作为最后的验证步骤, 你将首先验证模板语法是否正确。

1. 在云命令行管理`az group deployment validate`程序中, 运行以验证模板。

    ```azurecli
    az group deployment validate \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json" \
      --parameters adminUsername=$USERNAME \
      --parameters adminPassword=$PASSWORD \
      --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
    ```

    `--template-uri`参数指向 GitHub 上的模板。 模板的文件名为**azuredeploy.json**。 稍后, 您将了解如何在本地文件系统上验证和运行模板。

    您看到一个较大的 JSON 块作为输出, 这会告知您模板已通过验证。

    Azure 资源管理器填写模板参数, 并检查模板是否会在你的订阅中成功运行。

    如果验证失败, 您将在输出中看到失败的详细说明。

1. 运行`az group deployment create`以部署模板。

    ```azurecli
    az group deployment create \
      --name MyDeployment \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json" \
      --parameters adminUsername=$USERNAME \
      --parameters adminPassword=$PASSWORD \
      --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
    ```

    此命令与前面的命令类似, 但还包含`--name`用于为您的部署指定名称的参数。

    此命令需要2-3 分钟才能完成。 在您等待时, 现在我们来[仔细看看此模板的源代码](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-simple-linux/azuredeploy.json?azure-portal=true)是个好的时间。 请记住, 在阅读现有模板和创建自己的模板时, 资源管理器模板的内容将变得越来越熟悉。

    部署完成后, 您会看到另一个较大的 JSON 块作为描述部署的输出。

## <a name="verify-the-deployment"></a>验证部署

部署成功。 但让我们仅运行几个命令来验证。

1. 运行`az group deployment show`以验证部署。

    ```azurecli
    az group deployment show \
      --name MyDeployment \
      --resource-group <rgn>[sandbox resource group name]</rgn>
    ```

    你将看到与之前相同的 JSON 块。 如果你需要有关部署的这些详细信息, 你可以稍后再运行此命令。 输出的结构为 JSON, 以便更轻松地将其加入其他可用于跟踪部署和云使用的工具。

1. 运行`az vm list`以查看哪些虚拟机正在运行。

    ```azurecli
    az vm list \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --output table
    ```

    您的输出与此类似。 您的区域显示在 "**位置**" 列下。

    ```bash
    Name        ResourceGroup                         Location        Zones
    ----------  ------------------------------------  --------------  -------
    MyUbuntuVM  <rgn>[sandbox resource group name]</rgn>  southcentralus
    ```

    请记住, 模板将名称命名为 VM "MyUbuntuVM"。 在这里, 你会看到你的资源组中存在此 VM。
