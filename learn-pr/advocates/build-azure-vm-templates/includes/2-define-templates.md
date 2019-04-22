如果你已使用 azure 一段时间, 你可能听说过 azure 资源管理器。 让我们查看资源管理器的角色并定义构成资源管理器模板的内容。

## <a name="whats-azure-resource-manager"></a>什么是 Azure 资源管理器？

Azure 资源管理器是用于管理和组织云资源的接口。 请考虑使用资源管理器作为部署云资源的方法。

如果你熟悉 Azure 资源组, 则知道它们允许你将相关资源集视为一个单元。 资源管理器组织的资源组可让您在一次操作中部署、管理和删除所有资源。

考虑您为分析师运行的财务模型。 若要运行模型, 可能需要一个或多个虚拟机、存储数据的数据库和虚拟网络以在所有内容之间实现连接。 使用资源管理器, 可以将这些资产部署到相同的资源组中, 并管理和监视它们。 完成后, 可以通过一次操作删除资源组中的所有资源。

### <a name="what-are-resource-manager-templates"></a>什么是资源管理器模板？

资源管理器_模板_精确定义部署中的所有资源管理器资源。 您可以将资源管理器模板作为单个操作部署到资源组中。

资源管理器模板是一个 JSON 文件, 它成为_声明性自动化_的一种形式。 声明性自动化意味着您可以定义所需的资源, 但不_是_创建_方式_。 换句话说, 您可以定义所需的内容, 并且它是资源管理者的责任, 以确保正确部署资源。

您可以将声明性自动化视为类似于 web 浏览器显示 HTML 文件的方式。 HTML 文件描述页面__ 上显示的元素, 但不说明_如何_显示这些元素。 "如何" 是 web 浏览器的责任。

> [!NOTE]
> 你可能会听到其他人将资源管理器模板作为 "ARM 模板" 引用。 我们更喜欢使用完整名称 "Azure 资源管理器模板" 或 "资源管理器模板"。

## <a name="why-use-resource-manager-templates"></a>为什么要使用资源管理器模板？

使用资源管理器模板可使部署速度更快且更具可重复。 例如, 您不再需要在门户中创建虚拟机, 请等待其完成, 然后创建下一个 vm, 依此类推。 资源管理器负责处理整个部署。

以下是要考虑的其他一些好处。

* **模板提高一致性**

    资源管理器模板为您和其他人提供了一种用于描述您的部署的公共语言。 无论用于部署模板的工具或 SDK 是什么, 模板内的结构、格式和表达式都保持不变。

* **模板可帮助快速进行复杂部署**

    使用模板, 可以按正确的顺序部署多个资源。 例如, 您不希望在创建 OS 磁盘或网络接口之前部署虚拟机。 资源管理器将映射每个资源及其从属资源, 并首先创建从属资源。 依赖关系映射有助于确保按照正确的顺序执行部署。

* **模板减少了手动且容易出错的任务**

    手动创建和连接资源可能需要很长时间, 同时也很容易出错。 资源管理器可确保每次都以相同的方式进行部署。

* **模板是代码**

    模板通过代码表达你的要求。 将模板视为可像任何其他软件一样共享、测试和版本化的_代码的基础结构_类型。 此外, 由于模板是代码, 因此您可以创建可遵循的 "纸张踪迹"。 模板代码记录部署。 大多数用户在某种类型的修订控件 (如 Git) 下维护其模板。 更改模板时, 其修订历史记录还记录了模板 (和您的部署) 在一段时间内的发展方式。

* **模板促进重用**

    模板可以包含模板运行时填写的参数。 参数可以定义用户名、密码、域名等。 使用模板参数, 可以创建基础结构的多个版本, 如暂存和生产, 但仍能利用完全相同的模板。

* **模板为 linkable**

    可以将资源管理器模板链接在一起, 使模板本身成为模块式。 您可以编写用于定义解决方案的一部分的小型模板, 并将它们组合起来以创建一个完整的系统。

您的财务分析师运行的模型是唯一的, 但您可以在底层基础结构中看到模式。 例如, 大多数模型都需要数据库来存储数据。 许多模型都使用相同的编程语言、框架和操作系统来执行详细信息。 您可以定义用于描述每个组件 (计算、存储、网络等) 的模板, 并将它们组合起来以满足每个分析者的特定需求。

## <a name="whats-in-a-resource-manager-template"></a>资源管理器模板中的内容有哪些？

> [!NOTE]
> 在这里, 你将看到几个代码示例, 让你了解每个节的构造方式。 如果你看到的内容对你&mdash;不熟悉, 请不要担心, 你将能够阅读其他人的模板, 并在你获得与他们的实践体验时编写自己的体验。

您可能已使用 JSON 或 JavaScript 对象表示法, 以在服务器和 web 应用程序之间发送数据。 JSON 也是描述如何配置应用程序和基础结构的常用方法。 

JSON 使我们能够将存储为对象 (如虚拟机) 的数据表示为文本。 JSON 文档实质上是键值对的集合。 每个键都是一个字符串;其值可以是字符串、数字、布尔表达式、值列表或对象 (是其他键值对的集合)。

资源管理器模板可包含以下部分。 这些节使用 json 表示法表示, 但与 json 语言本身无关。

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "functions": [  ],
    "resources": [  ],
    "outputs": {  }
}
```
让我们更详细了解一下其中的每个部分。

### <a name="parameters"></a>参数

您可以在此处指定模板运行时可配置的值。 例如, 您可能允许模板的用户指定用户名、密码或域名。

下面的示例展示了一个 VM 的&ndash;用户名的两个参数, 一个用于其密码。

```json
"parameters": {
  "adminUsername": {
    "type": "string",
    "metadata": {
      "description": "Username for the Virtual Machine."
    }
  },
  "adminPassword": {
    "type": "securestring",
    "metadata": {
      "description": "Password for the Virtual Machine."
    }
  }
}
```

### <a name="variables"></a>Variables 

您可以在此处定义在整个模板中使用的值。 变量有助于使模板更易于维护。 例如, 您可以将一个存储帐户名称定义一次作为变量, 并在整个模板中使用该变量。 如果存储帐户名称发生更改, 则只需更新变量。

下面的示例展示了几个描述 VM 的网络功能的变量。

```json
"variables": {
  "nicName": "myVMNic",
  "addressPrefix": "10.0.0.0/16",
  "subnetName": "Subnet",
  "subnetPrefix": "10.0.0.0/24",
  "publicIPAddressName": "myPublicIP",
  "virtualNetworkName": "MyVNET"
}
```

### <a name="functions"></a>函数

您可以在此处定义不希望在整个模板中重复的过程。 与变量一样, 函数可帮助使模板更易于维护。 下面的示例创建一个函数, 以创建一个可在创建具有全局唯一命名要求的资源时使用的唯一名称。

```json
"functions": [
  {
    "namespace": "contoso",
    "members": {
      "uniqueName": {
        "parameters": [
          {
            "name": "namePrefix",
            "type": "string"
          }
        ],
        "output": {
          "type": "string",
          "value": "[concat(toLower(parameters('namePrefix')), uniqueString(resourceGroup().id))]"
        }
      }
    }
  }
],
```

### <a name="resources"></a>中心

在此部分中, 可以定义构成部署的 Azure 资源。

下面的示例展示了如何创建公用 IP 地址资源。

```json
{
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIPAddressName')]",
  "location": "[parameters('location')]",
  "apiVersion": "2018-08-01",
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('dnsLabelPrefix')]"
    }
  }
}
```

在这里, 资源的类型为`Microsoft.Network/publicIPAddresses`。 将从 "变量" 部分读取其名称, 并从 "参数" 部分读取其位置 (或 Azure 区域)。

由于资源类型可以随着时间的推移`apiVersion`而更改, 因此请参考要使用的资源类型的版本。 随着资源类型的演化和变化, 您可以修改模板以在准备就绪时使用最新的功能。

### <a name="outputs"></a>产出

您可以在此处定义模板运行时想要接收的任何信息。 例如, 你可能想要在部署运行之前接收你不知道的&ndash; VM 的 IP 地址或 FQDN 信息。

下面的示例展示了一个名为 "hostname" 的输出。 FQDN 值是从 VM 的公共 IP 地址设置中读取的。

```json
"outputs": {
  "hostname": {
    "type": "string",
    "value": "[reference(variables('publicIPAddressName')).dnsSettings.fqdn]"
  }
}
```

## <a name="how-do-i-write-a-resource-manager-template"></a>如何编写资源管理器模板？

编写资源管理器模板有多种方法。 虽然您可以从头开始编写模板, 但从现有模板开始, 并根据您的需要对其进行修改是很常见的。

下面是可以获取初学者模板的几种方法:

* 使用 Azure 门户创建基于现有资源组中的资源的模板。
* 从你或你的团队构建的用于类似用途的模板开始。
* 从 Azure 快速入门模板开始。 你将在下一部分中了解如何操作。

无论采用何种方法, 编写模板都涉及使用文本编辑器。 您可以引入常用编辑器, 但 Visual Studio Code 的[Azure 资源管理器工具扩展](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools&azure-portal=true)是专门为创建模板的任务而设计的。 通过此扩展, 可以更轻松地导航模板代码并为许多常见任务提供自动完成。

在您浏览和编写模板时, 您将需要[参考文档](https://docs.microsoft.com/azure/templates?azure-portal=true), 以了解哪些资源类型可用以及如何使用它们。