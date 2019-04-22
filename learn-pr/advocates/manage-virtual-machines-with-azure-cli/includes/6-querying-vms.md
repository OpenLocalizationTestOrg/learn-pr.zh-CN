<span data-ttu-id="e9db8-101">现在已创建虚拟机, 我们可以通过其他命令获取有关它的信息。</span><span class="sxs-lookup"><span data-stu-id="e9db8-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="e9db8-102">让我们从开始`vm list`。</span><span class="sxs-lookup"><span data-stu-id="e9db8-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="e9db8-103">此命令将返回此订阅中定义的_所有_虚拟机。</span><span class="sxs-lookup"><span data-stu-id="e9db8-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="e9db8-104">可以通过`--resource-group`参数将输出筛选为特定的资源组。</span><span class="sxs-lookup"><span data-stu-id="e9db8-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="e9db8-105">输出类型</span><span class="sxs-lookup"><span data-stu-id="e9db8-105">Output types</span></span>
<span data-ttu-id="e9db8-106">请注意, 目前为止完成的所有命令的默认响应类型为 JSON。</span><span class="sxs-lookup"><span data-stu-id="e9db8-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="e9db8-107">这非常适合脚本编写-但大多数人都会发现它难以阅读。</span><span class="sxs-lookup"><span data-stu-id="e9db8-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="e9db8-108">您可以通过`--output`标志更改任何响应的输出样式。</span><span class="sxs-lookup"><span data-stu-id="e9db8-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="e9db8-109">例如, 在 Azure 云命令行管理程序中尝试以下命令, 以查看不同的输出样式。</span><span class="sxs-lookup"><span data-stu-id="e9db8-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="e9db8-110">除了`table`, 您还可以指定`json` (默认值)、 `jsonc` (colorized JSON) 或`tsv` (以表格分隔的值)。</span><span class="sxs-lookup"><span data-stu-id="e9db8-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="e9db8-111">使用上面的命令尝试几个变体以查看差异。</span><span class="sxs-lookup"><span data-stu-id="e9db8-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="e9db8-112">获取 IP 地址</span><span class="sxs-lookup"><span data-stu-id="e9db8-112">Getting the IP address</span></span>

<span data-ttu-id="e9db8-113">另一个有用的`vm list-ip-addresses`命令是, 它将列出 VM 的公用 IP 地址和专用 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="e9db8-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="e9db8-114">如果它们发生更改, 或者在创建过程中未捕获它们, 则可以随时检索它们。</span><span class="sxs-lookup"><span data-stu-id="e9db8-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="e9db8-115">这将返回:</span><span class="sxs-lookup"><span data-stu-id="e9db8-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!TIP]
> <span data-ttu-id="e9db8-116">请注意, 我们使用的是`--output`标志的简写语法。 `-o`</span><span class="sxs-lookup"><span data-stu-id="e9db8-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="e9db8-117">大多数 Azure CLI 命令参数可以缩短为单短划线和字母。</span><span class="sxs-lookup"><span data-stu-id="e9db8-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="e9db8-118">例如, `--name`可以将其缩短为`-n`和`--resource-group` `-g`。</span><span class="sxs-lookup"><span data-stu-id="e9db8-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="e9db8-119">这对于键入很方便, 但建议在脚本中使用完整选项名称以清楚起见。</span><span class="sxs-lookup"><span data-stu-id="e9db8-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="e9db8-120">有关每个命令的详细信息, 请查看文档。</span><span class="sxs-lookup"><span data-stu-id="e9db8-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="e9db8-121">获取 VM 详细信息</span><span class="sxs-lookup"><span data-stu-id="e9db8-121">Getting VM details</span></span>

<span data-ttu-id="e9db8-122">我们可以使用`vm show`命令按名称或 ID 获取有关特定虚拟机的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="e9db8-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM
```

<span data-ttu-id="e9db8-123">这将返回一个相当大的 JSON 块, 其中包含有关 vm 的所有种类的信息, 包括附加的存储设备、网络接口以及虚拟机连接到的资源的所有对象 id。</span><span class="sxs-lookup"><span data-stu-id="e9db8-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="e9db8-124">同样, 我们可以更改为表格格式, 但这将忽略几乎所有有趣的数据。</span><span class="sxs-lookup"><span data-stu-id="e9db8-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="e9db8-125">相反, 我们可以转到用于 JSON 的内置查询语言 (称为 " [JMESPath](http://jmespath.org/)")。</span><span class="sxs-lookup"><span data-stu-id="e9db8-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="e9db8-126">使用 JMESPath 向查询添加筛选器</span><span class="sxs-lookup"><span data-stu-id="e9db8-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="e9db8-127">JMESPath 是一种围绕 JSON 对象构建的工业标准查询语言。</span><span class="sxs-lookup"><span data-stu-id="e9db8-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="e9db8-128">最简单的查询是指定在 JSON 对象中选择密钥的_标识符_。</span><span class="sxs-lookup"><span data-stu-id="e9db8-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="e9db8-129">例如, 给定对象:</span><span class="sxs-lookup"><span data-stu-id="e9db8-129">For example, given the object:</span></span>

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

<span data-ttu-id="e9db8-130">我们可以使用查询`people`返回`people`数组的值的数组。</span><span class="sxs-lookup"><span data-stu-id="e9db8-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="e9db8-131">如果只想要_一个_人, 我们可以使用索引器。</span><span class="sxs-lookup"><span data-stu-id="e9db8-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="e9db8-132">例如, `people[1]`将返回:</span><span class="sxs-lookup"><span data-stu-id="e9db8-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="e9db8-133">我们还可以根据某些条件添加特定的限定符, 以返回对象的子集。</span><span class="sxs-lookup"><span data-stu-id="e9db8-133">We can also add specific qualifiers that would return a subset of the objects based on some criteria.</span></span> <span data-ttu-id="e9db8-134">例如, 添加限定符`people[?age > '25']`将返回:</span><span class="sxs-lookup"><span data-stu-id="e9db8-134">For example, adding the qualifier `people[?age > '25']` would return:</span></span>

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

<span data-ttu-id="e9db8-135">最后, 我们可以通过添加 select: `people[?age > '25'].[name]`返回仅返回名称来限制结果:</span><span class="sxs-lookup"><span data-stu-id="e9db8-135">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

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

<span data-ttu-id="e9db8-136">JMESQuery 有几个其他有趣的查询功能。</span><span class="sxs-lookup"><span data-stu-id="e9db8-136">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="e9db8-137">当你有时间时, 请查看[JMESPath.org](http://jmespath.org/)网站上提供的[联机教程](http://jmespath.org/tutorial.html)。</span><span class="sxs-lookup"><span data-stu-id="e9db8-137">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="e9db8-138">筛选我们的 Azure CLI 查询</span><span class="sxs-lookup"><span data-stu-id="e9db8-138">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="e9db8-139">通过对 JMES 查询的基本了解, 我们可以将文件提供程序添加到查询返回的数据中`vm show` , 如命令。</span><span class="sxs-lookup"><span data-stu-id="e9db8-139">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="e9db8-140">例如, 我们可以检索管理员用户名称:</span><span class="sxs-lookup"><span data-stu-id="e9db8-140">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="e9db8-141">我们可以获取分配给我们的 VM 的大小:</span><span class="sxs-lookup"><span data-stu-id="e9db8-141">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="e9db8-142">或者, 若要检索网络接口的所有 id, 可以使用查询:</span><span class="sxs-lookup"><span data-stu-id="e9db8-142">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="e9db8-143">此查询技术将适用于任何 Azure CLI 命令, 并可用于从命令行中提取特定的数据位。</span><span class="sxs-lookup"><span data-stu-id="e9db8-143">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="e9db8-144">它也适用于脚本, 例如, 可以从 Azure 帐户中提取值并将其存储在环境或脚本变量中。</span><span class="sxs-lookup"><span data-stu-id="e9db8-144">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="e9db8-145">如果决定使用此方法, 则要添加的有用标志是`--output tsv`参数 (可以缩短为`-o tsv`)。</span><span class="sxs-lookup"><span data-stu-id="e9db8-145">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="e9db8-146">这将返回以制表符分隔的值中的结果, 这些值仅包含实际数据值和选项卡分隔符。</span><span class="sxs-lookup"><span data-stu-id="e9db8-146">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="e9db8-147">例如,</span><span class="sxs-lookup"><span data-stu-id="e9db8-147">As an example,</span></span>

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="e9db8-148">返回文本:`/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="e9db8-148">returns the text: `/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
