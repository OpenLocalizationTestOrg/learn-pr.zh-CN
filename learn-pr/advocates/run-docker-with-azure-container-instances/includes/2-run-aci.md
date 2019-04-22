在这里, 你将在 Azure 中创建容器, 并使用完全限定的域名 (FQDN) 将其公开到 Internet。

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="why-use-azure-container-instances"></a>为什么要使用 Azure 容器实例？

Azure 容器实例适用于可在独立容器中运行的方案, 包括简单的应用程序、任务自动化和生成作业。 以下是一些优点:

- **快速启动**: 以秒为单位启动容器。
- **每秒记帐**: 只有在运行容器时才会产生成本。
- **管理程序级安全性**: 将应用程序完全隔离为虚拟机中的。
- **自定义大小**: 指定 CPU 内核和内存的确切值。
- **永久性存储**: 将 Azure 文件共享直接装载到容器以检索和保留状态。
- **Linux 和 Windows**: 使用相同的 API 计划 Windows 和 Linux 容器。

对于需要完整容器业务流程的方案 (包括跨多个容器的服务发现、自动扩展和协调应用程序升级), 我们建议采用 Azure Kubernetes service (AKS)。

## <a name="create-a-container"></a>创建容器

您可以通过向`az container create`命令提供名称、Docker 图像和 Azure 资源组来创建容器。 您可以选择通过指定 DNS 名称标签将容器公开到 Internet。 在此示例中, 部署一个承载小型 web 应用程序的容器。 您还可以选择要放置图像的位置-你将使用**美国东部**地区, 但你可以从以下列表中将其更改为距你更近的位置。

<!-- TODO: fix region list so it's not hardcoded here -->
免费的沙盒允许您在 Azure 全局区域的子集内创建资源。 创建任何资源时, 请从以下列表中选择一个区域:

:::row:::
    :::column:::
        - westus2
        - southcentralus
        - centralus
        - eastus
        - westeurope
        - southeastasia
        - centralindia
    :::column-end:::
:::row-end:::

1. 提供一个 DNS 名称以将容器公开到 Internet。 您的 DNS 名称必须是唯一的。 若要了解学习目的, 请从云命令行管理程序中运行此命令, 以创建保存唯一名称的 Bash 变量。

    ```bash
    DNS_NAME_LABEL=aci-demo-$RANDOM
    ```

1. 运行以下`az container create`命令以启动容器实例。

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --image microsoft/aci-helloworld \
      --ports 80 \
      --dns-name-label $DNS_NAME_LABEL \
      --location eastus
    ```

    `$DNS_NAME_LABEL`指定您的 DNS 名称。 image name、 **microsoft/aci-helloworld**指的是承载在可运行基本 node.js web 应用程序的 docker 中心上的 docker 图像。

1. `az container create`命令完成后, 运行`az container show`以检查其状态。

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
      --out table
    ```

    你将看到容器的完全限定域名 (FQDN) 及其预配状态。 下面是一个示例。

    ```output
    FQDN                                    ProvisioningState
    --------------------------------------  -------------------
    aci-demo.eastus.azurecontainer.io       Succeeded
    ````

    如果你的容器处于 "**正在创建**" 状态, 请稍等几分钟, 然后再次运行该命令, 直到你看到 "**成功**" 状态。

1. 在浏览器中, 导航到容器的 FQDN 以查看它是否正在运行。 你会看到这一点。

    ![在浏览器中运行的示例 node.js 容器应用程序](../media/2-browser.png)

## <a name="summary"></a>摘要

在这里, 您创建了一个 Azure 容器实例来运行 web 服务器和应用程序。 你也可以使用容器实例的 FQDN 访问此应用程序。