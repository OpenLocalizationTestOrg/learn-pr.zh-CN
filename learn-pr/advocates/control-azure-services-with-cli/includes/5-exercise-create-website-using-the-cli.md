接下来, 我们将使用 Azure CLI 创建资源组, 然后将 web 应用程序部署到此资源组中。

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="using-a-resource-group"></a>使用资源组

当您使用自己的计算机和 Azure 订阅时, 您需要使用`az login`命令首次登录 Azure。 这在云命令行管理程序环境中是不必要的。

接下来, 通常使用`az group create`命令为所有相关的 Azure 资源创建资源组, 但这些练习已为您创建了一个资源组。 为您的资源组使用**<rgn>[沙盒资源组名称]</rgn>** 。

1. 您可以请求 Azure CLI 列出表中的所有资源组。 在免费的 Azure 沙箱中应该只有一台。

    ```azurecli
    az group list --output table
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. 在执行更多 Azure 开发的过程中, 您可以最终处理几个资源组。 如果组列表中有多个项, 则可以通过添加一个`--query`选项来筛选返回值。 尝试此命令:

    ```azurecli
    az group list --query "[?name == '<rgn>[sandbox resource group name]</rgn>']"
    ```

    使用**JMESPath** (它是用于 JSON 请求的标准查询语言) 对查询进行了格式化。 您可以在中了解有关此强大的筛选<http://jmespath.org/>器语言的详细信息。 我们还将更深入地介绍了如何在**Azure CLI 模块中管理虚拟机**的查询。

### <a name="steps-to-create-a-service-plan"></a>创建服务计划的步骤

在运行使用 azure 应用服务的 Web 应用程序时, 会为应用使用的 azure 计算资源付费, 这取决于与 Web 应用关联的应用服务计划。 服务计划确定用于应用数据中心的区域、使用的 vm 数量和定价层。

1. 创建应用服务计划以运行您的应用程序。 以下命令未指定定价层或 VM 实例详细信息, 因此默认情况下, 你将获得具有1个**小型**VM 实例的**基本**计划。

    > [!WARNING]
    > app 和 plan 的名称必须是_唯一_的, 因此, 请将后缀添加到名称中, 并`<unique>`将以下命令中的文本替换为一组数字、缩写或其他文本段, 以确保它在所有 Azure 中都是唯一的。

    对于`--location`参数, 请使用以下位置值之一。

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --location <location>
    ```

    此命令可能需要几分钟才能完成。

1. 通过在表中列出所有计划, 确认已成功创建服务计划。

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>创建 web 应用程序的步骤

接下来, 您将在服务计划中创建 web 应用程序。 您可以同时部署代码, 但对于我们的示例, 我们将以单独的步骤执行此操作。

1. 创建 web 应用程序, 提供上面创建的计划的名称。 **就像计划一样, 应用名称必须是唯一**的, 将`<unique>`标记替换为一些文本, 使名称在全局范围内是唯一的。

    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --plan popupappplan-<unique>
    ```

1. 通过在表中列出所有应用来验证是否已成功创建应用程序。

    ```azurecli
    az webapp list --output table
    ```

1. 记下表中列出的**DefaultHostName** , 然后将其记录。这是新网站可访问的 web 地址。 Azure 将使你的网站通过`azurewebsites.net`域中的唯一应用程序名称提供。 例如, 如果我的应用程序名称是 "popupwebapp-mslearn123", 则我的网站 URL 将`http://popupwebapp-mslearn123.azurewebsites.net`为:。

1. 您的网站有一个由 Azure 创建的 "快速入门" 页面, 您可以在浏览器中或通过卷查看, 只需使用**DefaultHostName**:

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
### <a name="steps-to-deploy-code-from-github"></a>部署 GitHub 中的代码的步骤

1. 最后一步是将 GitHub 存储库中的代码部署到 web 应用。 让我们使用一个显示 "HelloWorld!" 的 Azure 示例 Github 存储库中提供的简单 PHP 页面。 执行时。 请确保使用您创建的 web 应用名称。

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. 部署后, 通过浏览器或卷再次进入您的网站。

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
    页面显示 "Hello World!"

    ```output
    Hello World!
    ```

本练习演示了交互式 Azure CLI 会话的典型模式。 您首先使用标准命令创建新的资源组。 然后, 使用一组命令将资源 (在此示例中为 web 应用) 部署到此资源组中。 这组命令可以轻松地组合到命令行管理程序脚本中, 并在每次需要创建相同的资源时执行。