假设您的公司将多台服务器部署为其云转换的一部分。 在部署过程中, 必须对 VM 磁盘进行加密, 因此在磁盘易受攻击时没有任何时间。 您希望自动执行此过程, 并且必须修改 Azure 资源管理器模板以自动启用加密。

在这里, 我们将介绍如何使用 Azure 资源管理器模板自动为新的 Windows 虚拟机启用加密。

## <a name="what-are-azure-resource-manager-templates"></a>什么是 Azure 资源管理器模板？

资源管理器模板是用于定义要部署到 Azure 的一组资源的 JSON 文件。 你可以从头开始编写它们, 对于某些 Azure 资源 (包括 vm), 你可以使用 azure 门户生成这些资源。 您需要完成手动 VM 部署所需的信息, 但不是将 VM 部署到 Azure, 而是保存该模板。 然后, 您可以_重用_该模板来创建该特定的 VM 配置。

[文档中提供了一些示例模板](https://azure.microsoft.com/resources/templates), 可自动执行各种管理任务。 事实上, 我们可以使用其中一个模板来加密我们刚才手动执行的虚拟机。

![显示 Azure 模板的屏幕截图](../media/5-browse-templates.png)

## <a name="using-github-templates"></a>使用 GitHub 模板

实际模板源存储在 GitHub 中。 您可以浏览 GitHub 中的模板并从页面向 Azure 部署。

![在突出显示了 "部署到 Azure" 按钮时显示 GitHub 模板的屏幕截图](../media/5-deploy-from-github.png)

部署模板后, Azure 将显示所需输入域的列表。

![显示 Azure 门户中的模板的屏幕截图](../media/5-fill-in-template.png)

然后, 您可以执行模板来创建、修改或删除资源。

### <a name="running-templates-in-the-azure-portal"></a>在 Azure 门户中运行模板

如果您已经知道要使用的模板, 或者您已在 Azure 帐户中保存了模板, 则可以使用**创建资源** > **模板部署**资源在门户中查找和运行定义的模板。 您可以按名称搜索模板, 编辑模板以更改参数或行为, 并在 GUI 中执行模板权限。

### <a name="running-templates-from-the-command-line"></a>从命令行运行模板

给定模板的 URL, 您可以使用 Azure PowerShell 执行它。 例如, 我们可以使用以下 PowerShell 命令运行磁盘加密模板:

```powershell
New-AzResourceGroupDeployment `
    -Name encrypt-disk `
    -ResourceGroupName <resource-group-name> `
    -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

或者, 如果您更喜欢使用该`group deployment create`命令, 也可以使用 Azure CLI。

```azurecli
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> \ 
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

