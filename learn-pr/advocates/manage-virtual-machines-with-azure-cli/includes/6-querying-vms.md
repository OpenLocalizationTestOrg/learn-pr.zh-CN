现在已创建虚拟机, 我们可以通过其他命令获取有关它的信息。

让我们从开始`vm list`。

```azurecli
az vm list
```

此命令将返回此订阅中定义的_所有_虚拟机。 可以通过`--resource-group`参数将输出筛选为特定的资源组。 

## <a name="output-types"></a>输出类型
请注意, 目前为止完成的所有命令的默认响应类型为 JSON。 这非常适合脚本编写-但大多数人都会发现它难以阅读。 您可以通过`--output`标志更改任何响应的输出样式。 例如, 在 Azure 云命令行管理程序中尝试以下命令, 以查看不同的输出样式。

```azurecli
az vm list --output table
```

除了`table`, 您还可以指定`json` (默认值)、 `jsonc` (colorized JSON) 或`tsv` (以表格分隔的值)。 使用上面的命令尝试几个变体以查看差异。

## <a name="getting-the-ip-address"></a>获取 IP 地址

另一个有用的`vm list-ip-addresses`命令是, 它将列出 VM 的公用 IP 地址和专用 IP 地址。 如果它们发生更改, 或者在创建过程中未捕获它们, 则可以随时检索它们。

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

这将返回:

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!TIP]
> 请注意, 我们使用的是`--output`标志的简写语法。 `-o` 大多数 Azure CLI 命令参数可以缩短为单短划线和字母。 例如, `--name`可以将其缩短为`-n`和`--resource-group` `-g`。 这对于键入很方便, 但建议在脚本中使用完整选项名称以清楚起见。 有关每个命令的详细信息, 请查看文档。

## <a name="getting-vm-details"></a>获取 VM 详细信息

我们可以使用`vm show`命令按名称或 ID 获取有关特定虚拟机的更多详细信息。

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM
```

这将返回一个相当大的 JSON 块, 其中包含有关 vm 的所有种类的信息, 包括附加的存储设备、网络接口以及虚拟机连接到的资源的所有对象 id。 同样, 我们可以更改为表格格式, 但这将忽略几乎所有有趣的数据。 相反, 我们可以转到用于 JSON 的内置查询语言 (称为 " [JMESPath](http://jmespath.org/)")。

## <a name="adding-filters-to-queries-with-jmespath"></a>使用 JMESPath 向查询添加筛选器

JMESPath 是一种围绕 JSON 对象构建的工业标准查询语言。 最简单的查询是指定在 JSON 对象中选择密钥的_标识符_。

例如, 给定对象:

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

我们可以使用查询`people`返回`people`数组的值的数组。 如果只想要_一个_人, 我们可以使用索引器。 例如, `people[1]`将返回:

```json
{
    "name": "Barney",
    "age": 25
}
```

我们还可以根据某些条件添加特定的限定符, 以返回对象的子集。 例如, 添加限定符`people[?age > '25']`将返回:

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

最后, 我们可以通过添加 select: `people[?age > '25'].[name]`返回仅返回名称来限制结果:

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

JMESQuery 有几个其他有趣的查询功能。 当你有时间时, 请查看[JMESPath.org](http://jmespath.org/)网站上提供的[联机教程](http://jmespath.org/tutorial.html)。

## <a name="filtering-our-azure-cli-queries"></a>筛选我们的 Azure CLI 查询

通过对 JMES 查询的基本了解, 我们可以将文件提供程序添加到查询返回的数据中`vm show` , 如命令。 例如, 我们可以检索管理员用户名称:

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "osProfile.adminUsername"
```

我们可以获取分配给我们的 VM 的大小:

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query hardwareProfile.vmSize
```

或者, 若要检索网络接口的所有 id, 可以使用查询:

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

此查询技术将适用于任何 Azure CLI 命令, 并可用于从命令行中提取特定的数据位。 它也适用于脚本, 例如, 可以从 Azure 帐户中提取值并将其存储在环境或脚本变量中。 如果决定使用此方法, 则要添加的有用标志是`--output tsv`参数 (可以缩短为`-o tsv`)。 这将返回以制表符分隔的值中的结果, 这些值仅包含实际数据值和选项卡分隔符。

例如,

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

返回文本:`/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`
