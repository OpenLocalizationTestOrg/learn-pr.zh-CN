现在, 您已定义在 VM 上配置 Nginx 的自定义脚本扩展的模板资源, 让我们将其添加到现有 VM 模板并运行它。

Nginx 配置将如下所示。

![显示生成的 Nginx 配置的 web 浏览器](../../media/6-browser-linux.png)

## <a name="build-the-template"></a>生成模板

在这里, 你将下载模板并进行修改。

1. 从云命令行管理`curl`程序中, 运行以下载以前从 GitHub 中使用的模板。

    ```bash
    curl https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json > azuredeploy.json
    ```

1. 通过云命令行管理程序编辑器打开**azuredeploy.json** 。

    ```bash
    code azuredeploy.json
    ```

1. 在文件中, 找到 " `resources` " 部分。 将您在上一部分中构建的自定义脚本扩展资源添加到此部分的顶部, 然后保存该文件。

    以下是用于复习的代码。

    ```json
    {
      "name": "[concat(variables('vmName'),'/', 'ConfigureNginx')]",
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "apiVersion": "2018-06-01",
      "location": "[parameters('location')]",
      "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "customScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "fileUris": [
            "https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"
          ]
        },
        "protectedSettings": {
           "commandToExecute": "./configure-nginx.sh"
        }
      },
      "dependsOn": [
        "[resourceId('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
      ]
    },
    ```

    请注意, `,`结尾处的逗号字符是分隔资源所需的。 定义资源的顺序无关紧要, 但为了简单起见, 您将其添加到顶部。

    如果您停滞或想要比较你的工作, 可以从 GitHub 下载生成的文件。

    ```bash
    curl https://raw.githubusercontent.com/MicrosoftDocs/mslearn-build-azure-vm-templates/master/linux/azuredeploy.json > azuredeploy.json
    ```

    你已完成编辑文件。 确保您已将更改保存到**azuredeploy.json** , 然后关闭编辑器。

    若要关闭编辑器, 请单击角上的省略号, 然后选择 "**关闭编辑器**"。

## <a name="verify-the-template"></a>验证模板

在这里, 你将从 CLI 中验证模板。

实际上, 在运行测试部署之前, 您可能会运行不起毛的测试或通过 Azure 资源管理器可视化工具运行您的模板。

与您之前所做的操作相似`az group deployment validate` , 请运行以验证您的模板。

```azurecli
az group deployment validate \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --template-file azuredeploy.json \
  --parameters adminUsername=$USERNAME \
  --parameters adminPassword=$PASSWORD \
  --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
```

请注意, 这次您使用`--template-file`的是参数, `--template-uri`而不是, 因为您引用的是本地文件。

如果您看到错误, 请返回到上一部分或将您的代码与[参考实现](https://raw.githubusercontent.com/MicrosoftDocs/mslearn-build-azure-vm-templates/master/linux/azuredeploy.json?azure-portal=true)进行比较。

## <a name="deploy-the-template"></a>部署模板

在这里, 你将运行一个类似于之前运行的命令来部署模板的命令。 由于尚未修改任何现有资源&ndash; , 因此该 VM 的网络设置或存储帐户&ndash;资源管理器不会对这些资源执行任何操作。 它只会应用您刚刚添加的资源, 该资源将运行在您的 VM 上安装 Nginx 的自定义脚本扩展。

运行`az group deployment create`以更新部署。

```azurecli
az group deployment create \
  --name MyDeployment \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --template-file azuredeploy.json \
  --parameters adminUsername=$USERNAME \
  --parameters adminPassword=$PASSWORD \
  --parameters dnsLabelPrefix=$DNS_LABEL_PREFIX
```

此外, 请注意, 这次您使用`--template-file`的是参数, 因为您引用的是本地文件。

此命令需要几分钟的时间才能完成。 您会看到一个作为输出的大型 JSON 块, 其中介绍了部署。

## <a name="verify-the-deployment"></a>验证部署

部署成功, 让我们来看看操作的结果配置。

1. 运行`az vm show`以获取 VM 的 IP 地址, 并将结果存储在 Bash 变量中。

    ```azurecli
    IPADDRESS=$(az vm show \
      --name MyUbuntuVM \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --show-details \
      --query [publicIps] \
      --output tsv)
    ```

1. 运行`curl`以访问您的 web 服务器。

    ```bash
    curl $IPADDRESS
    ```

    你会看到这一点。

    ```html
    <html><body><h2>Welcome to Azure! My name is MyUbuntuVM.</h2></body></html>
    ```

1. 在单独的浏览器选项卡中, 导航到您的网站。

    首先, 打印 IP 地址。

    ```bash
    echo $IPADDRESS
    ```

    从单独的浏览器选项卡导航到您看到的 IP 地址。你会看到这一点。

    ![显示生成的 Nginx 配置的 web 浏览器](../../media/6-browser-linux.png)

出色的工作! 自定义脚本扩展资源就绪后, 您可以扩展部署以执行更多操作。