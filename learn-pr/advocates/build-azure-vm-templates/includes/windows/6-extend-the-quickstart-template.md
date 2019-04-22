<span data-ttu-id="85ab8-101">现在, 您已定义在 VM 上配置 IIS 的自定义脚本扩展的模板资源, 让我们将其添加到现有 VM 模板并运行它。</span><span class="sxs-lookup"><span data-stu-id="85ab8-101">Now that you've defined the template resource for the Custom Script Extension that configures IIS on your VM, let's add it to the existing VM template and run it.</span></span>

<span data-ttu-id="85ab8-102">IIS 配置将如下所示。</span><span class="sxs-lookup"><span data-stu-id="85ab8-102">Here's what the IIS configuration will look like.</span></span>

![显示生成的 IIS 配置的 web 浏览器](../../media/6-browser-windows.png)

## <a name="build-the-template"></a><span data-ttu-id="85ab8-104">生成模板</span><span class="sxs-lookup"><span data-stu-id="85ab8-104">Build the template</span></span>

<span data-ttu-id="85ab8-105">在这里, 你将下载模板并进行修改。</span><span class="sxs-lookup"><span data-stu-id="85ab8-105">Here you'll download the template and modify it.</span></span>

1. <span data-ttu-id="85ab8-106">从云命令行管理`curl`程序中, 运行以下载以前从 GitHub 中使用的模板。</span><span class="sxs-lookup"><span data-stu-id="85ab8-106">From Cloud Shell, run `curl` to download the template you used previously from GitHub.</span></span>

    ```bash
    curl https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json > azuredeploy.json
    ```

1. <span data-ttu-id="85ab8-107">通过云命令行管理程序编辑器打开**azuredeploy.json** 。</span><span class="sxs-lookup"><span data-stu-id="85ab8-107">Open **azuredeploy.json** through the Cloud Shell editor.</span></span>

    ```bash
    code azuredeploy.json
    ```

1. <span data-ttu-id="85ab8-108">在文件中, 找到 " `resources` " 部分。</span><span class="sxs-lookup"><span data-stu-id="85ab8-108">In the file, locate the `resources` section.</span></span> <span data-ttu-id="85ab8-109">将您在上一部分中构建的自定义脚本扩展资源添加到此部分的顶部, 然后保存该文件。</span><span class="sxs-lookup"><span data-stu-id="85ab8-109">Add the Custom Script Extension resource you built in the previous part to the top of this section, then save the file.</span></span>

    <span data-ttu-id="85ab8-110">以下是用于复习的代码。</span><span class="sxs-lookup"><span data-stu-id="85ab8-110">Here's the code as a refresher.</span></span>

    ```json
    {
      "name": "[concat(variables('vmName'),'/', 'ConfigureIIS')]",
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
    },
    ```

    <span data-ttu-id="85ab8-111">请注意, `,`结尾处的逗号字符是分隔资源所需的。</span><span class="sxs-lookup"><span data-stu-id="85ab8-111">Note the comma `,` character at the end, which is needed to separate resources.</span></span> <span data-ttu-id="85ab8-112">定义资源的顺序无关紧要, 但为了简单起见, 您将其添加到顶部。</span><span class="sxs-lookup"><span data-stu-id="85ab8-112">The order you define resources doesn't matter, but here you add it to the top for simplicity.</span></span>

    <span data-ttu-id="85ab8-113">如果您停滞或想要比较你的工作, 可以从 GitHub 下载生成的文件。</span><span class="sxs-lookup"><span data-stu-id="85ab8-113">If you get stuck or want to compare your work, you can download the resulting file from GitHub.</span></span>

    ```bash
    curl https://raw.githubusercontent.com/MicrosoftDocs/mslearn-build-azure-vm-templates/master/windows/azuredeploy.json > azuredeploy.json
    ```

    <span data-ttu-id="85ab8-114">你已完成编辑文件。</span><span class="sxs-lookup"><span data-stu-id="85ab8-114">You're all done editing files.</span></span> <span data-ttu-id="85ab8-115">确保您已将更改保存到**azuredeploy.json** , 然后关闭编辑器。</span><span class="sxs-lookup"><span data-stu-id="85ab8-115">Ensure that you saved changes to **azuredeploy.json** and then close the editor.</span></span>

    <span data-ttu-id="85ab8-116">若要关闭编辑器, 请单击角上的省略号, 然后选择 "**关闭编辑器**"。</span><span class="sxs-lookup"><span data-stu-id="85ab8-116">To close the editor, click the ellipses in the corner and then select **Close Editor**.</span></span>

## <a name="verify-the-template"></a><span data-ttu-id="85ab8-117">验证模板</span><span class="sxs-lookup"><span data-stu-id="85ab8-117">Verify the template</span></span>

<span data-ttu-id="85ab8-118">在这里, 你将从 CLI 中验证模板。</span><span class="sxs-lookup"><span data-stu-id="85ab8-118">Here you'll validate the template from the CLI.</span></span>

<span data-ttu-id="85ab8-119">实际上, 在运行测试部署之前, 您可能会运行不起毛的测试或通过 Azure 资源管理器可视化工具运行您的模板。</span><span class="sxs-lookup"><span data-stu-id="85ab8-119">In practice, you might run lint tests or run your template through the Azure Resource Manager Visualizer before you run a test deployment.</span></span>

<span data-ttu-id="85ab8-120">与您之前所做的操作相似`az group deployment validate` , 请运行以验证您的模板。</span><span class="sxs-lookup"><span data-stu-id="85ab8-120">Similar to what you did previously, run `az group deployment validate` to validate your template.</span></span>

```azurecli
az group deployment validate \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --template-file azuredeploy.json \
  --parameters adminUsername=$USERNAME \
  --parameters adminPassword=$PASSWORD \
  --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
```

<span data-ttu-id="85ab8-121">请注意, 这次您使用`--template-file`的是参数, `--template-uri`而不是, 因为您引用的是本地文件。</span><span class="sxs-lookup"><span data-stu-id="85ab8-121">Notice that this time you use the `--template-file` argument, and not `--template-uri`, because you are referencing a local file.</span></span>

<span data-ttu-id="85ab8-122">如果您看到错误, 请返回到上一部分或将您的代码与[参考实现](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-build-azure-vm-templates/master/windows/azuredeploy.json?azure-portal=true)进行比较。</span><span class="sxs-lookup"><span data-stu-id="85ab8-122">If you see errors, refer back to the previous part or compare your code to the [reference implementation](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-build-azure-vm-templates/master/windows/azuredeploy.json?azure-portal=true).</span></span>

## <a name="deploy-the-template"></a><span data-ttu-id="85ab8-123">部署模板</span><span class="sxs-lookup"><span data-stu-id="85ab8-123">Deploy the template</span></span>

<span data-ttu-id="85ab8-124">在这里, 你将运行一个类似于之前运行的命令来部署模板的命令。</span><span class="sxs-lookup"><span data-stu-id="85ab8-124">Here you'll run a command that's similar to the one you ran earlier to deploy the template.</span></span> <span data-ttu-id="85ab8-125">由于尚未修改任何现有资源&ndash; , 因此该 VM 的网络设置或存储帐户&ndash;资源管理器不会对这些资源执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="85ab8-125">Because you haven't modified any existing resources &ndash; the VM, its network settings, or the storage account &ndash; Resource Manager won't take any action on those resources.</span></span> <span data-ttu-id="85ab8-126">它只会应用您刚刚添加的资源, 该资源将运行在您的 VM 上安装 IIS 的自定义脚本扩展。</span><span class="sxs-lookup"><span data-stu-id="85ab8-126">It will only apply the resource you just added that runs the Custom Script Extension that installs IIS on your VM.</span></span>

<span data-ttu-id="85ab8-127">运行`az group deployment create`以更新部署。</span><span class="sxs-lookup"><span data-stu-id="85ab8-127">Run `az group deployment create` to update your deployment.</span></span>

```azurecli
az group deployment create \
  --name MyDeployment \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --template-file azuredeploy.json \
  --parameters adminUsername=$USERNAME \
  --parameters adminPassword=$PASSWORD \
  --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
```

<span data-ttu-id="85ab8-128">此外, 请注意, 这次您使用`--template-file`的是参数, 因为您引用的是本地文件。</span><span class="sxs-lookup"><span data-stu-id="85ab8-128">Again, notice that this time you use the `--template-file` argument because you are referencing a local file.</span></span>

<span data-ttu-id="85ab8-129">此命令需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="85ab8-129">The command takes a couple minutes to complete.</span></span> <span data-ttu-id="85ab8-130">您会看到一个作为输出的大型 JSON 块, 其中介绍了部署。</span><span class="sxs-lookup"><span data-stu-id="85ab8-130">You see a large block of JSON as output, which describes the deployment.</span></span>

## <a name="verify-the-deployment"></a><span data-ttu-id="85ab8-131">验证部署</span><span class="sxs-lookup"><span data-stu-id="85ab8-131">Verify the deployment</span></span>

<span data-ttu-id="85ab8-132">部署成功, 让我们来看看操作的结果配置。</span><span class="sxs-lookup"><span data-stu-id="85ab8-132">The deployment succeeded, so let's see the resulting configuration in action.</span></span>

1. <span data-ttu-id="85ab8-133">运行`az vm show`以获取 VM 的 IP 地址, 并将结果存储在 Bash 变量中。</span><span class="sxs-lookup"><span data-stu-id="85ab8-133">Run `az vm show` to get the VM's IP address and store the result in a Bash variable.</span></span>

    ```azurecli
    IPADDRESS=$(az vm show \
      --name SimpleWinVM \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --show-details \
      --query [publicIps] \
      --output tsv)
    ```

1. <span data-ttu-id="85ab8-134">运行`curl`以访问您的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="85ab8-134">Run `curl` to access your web server.</span></span>

    ```bash
    curl $IPADDRESS
    ```

    <span data-ttu-id="85ab8-135">你会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="85ab8-135">You see this.</span></span>

    ```html
    <html><body><h2>Welcome to Azure! My name is SimpleWinVM.</h2></body></html>
    ```

1. <span data-ttu-id="85ab8-136">在单独的浏览器选项卡中, 导航到您的网站。</span><span class="sxs-lookup"><span data-stu-id="85ab8-136">From a separate browser tab, navigate to your web site.</span></span>

    <span data-ttu-id="85ab8-137">首先, 打印 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="85ab8-137">First, print the IP address.</span></span>

    ```bash
    echo $IPADDRESS
    ```

    <span data-ttu-id="85ab8-138">从单独的浏览器选项卡导航到您看到的 IP 地址。你会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="85ab8-138">Navigate to the IP address you see from a separate browser tab. You see this.</span></span>

    ![显示生成的 IIS 配置的 web 浏览器](../../media/6-browser-windows.png)

<span data-ttu-id="85ab8-140">出色的工作!</span><span class="sxs-lookup"><span data-stu-id="85ab8-140">Great work!</span></span> <span data-ttu-id="85ab8-141">自定义脚本扩展资源就绪后, 您可以扩展部署以执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="85ab8-141">With the Custom Script Extension resource in place, you're able to extend your deployment to do more.</span></span>