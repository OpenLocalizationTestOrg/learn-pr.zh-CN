在为财务分析员创建 VM 时, 通常会包含一个 web 服务器, 该服务器为分析者提供仪表板以可视化和收集运行结果。 使用资源管理器模板来引入虚拟机是一个好的开端。 但如何扩展模板以在 VM 中配置 web 服务器软件？

使用 Azure CLI 将虚拟机配置为运行 web 服务器只需要几个基本命令。 但在以下情况下会发生什么情况:

* 您需要连续创建和删除 vm？
* 您的部署需要其他组件 (如存储和网络), 从而增加了复杂性？

通过 Azure CLI 管理各个资源是一个很出色的开端。 但它很快会变得单调乏味且容易出错, 因为您仍需要将资源正确地连接在一起。 您需要一个更自动化的解决方案。

在这里, 你将检查 VM web 服务器的要求, 并了解如何生成可添加到模板中的资源。

> [!NOTE]
> 您在此页面上看到的代码和命令用于说明。 现在, 只需继续操作。 您不需要修改任何文件或运行任何命令。

## <a name="whats-the-custom-script-extension"></a>自定义脚本扩展名是什么？

自定义脚本扩展是在 Azure 虚拟机上下载和运行脚本的简单方法。 它只是在虚拟机启动并运行后配置虚拟机的多种方法之一。

你可以将脚本存储在 Azure 存储或公共位置 (如 GitHub) 中。 您可以手动运行脚本, 也可以将其作为更自动化的部署的一部分运行。 在这里, 你将定义即将添加到资源管理器模板中的资源。 资源将使用自定义脚本扩展从 GitHub 下载 PowerShell 脚本, 并在您的 VM 上执行该脚本。 该脚本启用 IIS WebServerRole 功能并配置基本主页。

## <a name="how-do-i-extend-a-resource-manager-template"></a>如何扩展资源管理器模板？

您的资源管理器模板将创建一个 Windows VM。 在虚拟机启动时, 还可以通过几种方法来扩展模板, 并启用 IIS。

扩展模板的一种方法是创建多个模板, 每个模板定义一段系统。 然后, 将它们_链接_或_嵌套_在一起, 以生成更完整的系统。 创建您自己的模板时, 可以构建一个较小、更精细的模板的库, 并将它们与您所需的方式相结合。

另一种方法是修改现有模板以满足您的需求。 你将在此模块中执行此操作, 因为这通常是开始编写你自己的模板的最快方法。

## <a name="build-the-template-resource"></a>生成模板资源

在这里, 你将了解如何使用自定义脚本扩展作为示例来构建模板资源。 将参考文档用作起始点, 然后定义所需的资源属性。

让我们先查看你的要求。

### <a name="gather-requirements"></a>收集要求

下面简要介绍了您希望通过模板实现的功能。

1. 创建虚拟机。
1. 通过网络防火墙打开端口80。
1. 在 VM 上安装和配置 web 服务器软件。

上一部件中使用的资源管理器模板已涵盖前两个要求。 第三, 让我们先看一看 Azure CLI 命令, 我们可以从命令行手动运行, 以便使用自定义脚本扩展在 VM 上启用 IIS。

```azurecli
az vm extension set \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --vm-name SimpleWinVM \
  --name CustomScriptExtension \
  --publisher Microsoft.Compute \
  --version 1.9 \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-iis.ps1"]}' \
  --protected-settings '{"commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"}'
```

此命令使用自定义脚本扩展在您的 VM 上运行安装 IIS 的 PowerShell 脚本。 如果你愿意, 可以从单独的浏览器选项卡[检查 PowerShell 脚本](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-iis.ps1?azure-portal=true)。

您需要一种方法来映射此命令以使用资源管理器模板语法。 上面`az vm extension set`显示的示例是您在命令行中输入的命令。 您需要的是模板格式的声明性 JSON。

### <a name="locate-the-resource-schema"></a>查找资源架构

若要了解如何在模板中使用自定义脚本扩展, 一种方法是按示例学习。 例如, 你可能会发现一个 Azure 快速入门模板执行类似操作, 并根据你的需要对其进行调整。

另一种方法是在[参考文档](https://docs.microsoft.com/azure/templates?azure-portal=true)中查找所需的资源。 在这种情况下, 搜索文档会显示[Microsoft。计算 virtualMachines/extension 模板参考](https://docs.microsoft.com/azure/templates/Microsoft.Compute/2018-10-01/virtualMachines/extensions?azure-portal=true)。

您可以先将架构复制到临时文档, 如下所示。

```json
{
  "name": "string",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-10-01",
  "location": "string",
  "tags": {},
  "properties": {
    "publisher": "string",
    "type": "string",
    "typeHandlerVersion": "string",
    "autoUpgradeMinorVersion": boolean,
    "settings": {},
    "protectedSettings": {},
    "instanceView": {
      "name": "string",
      "type": "string",
      "typeHandlerVersion": "string",
      "substatuses": [
        {
          "code": "string",
          "level": "string",
          "displayStatus": "string",
          "message": "string",
          "time": "string"
        }
      ],
      "statuses": [
        {
          "code": "string",
          "level": "string",
          "displayStatus": "string",
          "message": "string",
          "time": "string"
        }
      ]
    }
  }
}
```

### <a name="specify-required-properties"></a>指定所需属性

架构显示您可以提供的所有属性。 有些属性是必需的。其他选项是可选的。 您可以从确定所有必需属性开始。 请在 "参考" 页面上的架构定义下找到这些。

下面是必需的参数。

* `name`
* `type`
* `apiVersion`
* `location`
* `properties`

删除所有不需要的参数后, 资源定义可能如下所示。

```json
{
  "name": "[concat(variables('vmName'), '/', 'ConfigureIIS')]",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-06-01",
  "location": "[parameters('location')]",
  "properties": { }
}
```

`type`和`apiVersion`属性的值直接来自文档。 `properties`是必需的, 但现在可以是空的。

您知道现有 VM 模板具有一个名为`location`的参数。 本示例使用内置`parameters`函数来读取该值。

该`name`属性遵循特殊约定。 此示例使用内置`concat`函数连接或组合多个字符串。 完整的字符串包含 VM 名称, 后跟一个斜杠`/`字符, 后跟您选择的名称 (这里是 "ConfigureIIS")。 VM 名称可帮助模板标识要在其上运行脚本的 VM 资源。

### <a name="specify-additional-properties"></a>指定其他属性

接下来, 您可以添加所需的任何其他属性。 参照 CLI 示例之前, 您需要脚本文件的位置或 URI, 以及要在 VM 上执行的用于运行该脚本的 PowerShell 命令的位置 (或 URI)。 作为建议的做法, 还可以包含资源的发布者名称、类型和版本。

参考本文档, 您需要使用 "点" 表示法中显示的这些值。

* `properties.publisher`
* `properties.type`
* `properties.typeHandlerVersion`
* `properties.autoUpgradeMinorVersion`
* `properties.settings.fileUris`
* `properties.protectedSettings.commandToExecute`

现在, 您的自定义脚本扩展资源如下所示。

```json
{
  "name": "[concat(variables('vmName'), '/', 'ConfigureIIS')]",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-06-01",
  "location": "[parameters('location')]",
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.9",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-iis.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"
    }
  }
}
```

### <a name="specify-dependent-resources"></a>指定依存资源

在虚拟机可用之前, 不能运行自定义脚本扩展。 所有模板资源都提供`dependsOn`属性。 此属性可帮助资源管理器确定应用资源的正确顺序。

下面是添加`dependsOn`属性后模板资源可能的外观。

```json
{
  "name": "[concat(variables('vmName'), '/', 'ConfigureIIS')]",
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "apiVersion": "2018-06-01",
  "location": "[parameters('location')]",
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.9",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-iis.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"
    }
  },
  "dependsOn": [
    "[resourceId('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ]
}
```

括号`[ ]`语法意味着可以提供在应用此资源之前必须存在的资源列表 (一个或一组)。

有多种方法可以定义资源相关性。 您可以提供它的名称, 如 "SimpleWinVM"、全名 (包括其命名空间、类型和名称), 例如 "SimpleWinVM/virtualMachines/", 或按其资源 ID。

此示例使用内置`resourceId`函数获取虚拟机的资源 ID (使用其完整名称)。 这有助于阐明所引用的资源, 并有助于避免在多个资源具有相似名称时出现歧义。

现有模板提供了一个`vmName`定义 VM 名称的变量。 本示例使用内置`variables`函数进行读取。

## <a name="summary"></a>摘要

现在, 你已拥有在模板中定义自定义脚本扩展资源所需的一切。 在下一部分中, 你将扩展模板以使用它。