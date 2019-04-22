默认情况下, Azure 容器实例是无状态的。 如果容器崩溃或停止, 则它的所有状态都将丢失。 若要在容器的生存期之外保留状态, 必须从外部存储装入卷。

在这里, 你将向 azure 容器实例装载 azure 文件共享, 以便稍后存储数据并对其进行访问。

## <a name="create-an-azure-file-share"></a>创建 Azure 文件共享

在这里, 你将创建一个存储帐户和一个文件共享, 稍后你将对 Azure 容器实例进行访问。

1. 您的存储帐户需要一个唯一的名称。 若要了解学习目的, 请运行以下命令, 在 Bash 变量中存储唯一名称。

    ```bash
    STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
    ```

1. 运行以下`az storage account create`命令以创建存储帐户。

    ```azurecli
    az storage account create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $STORAGE_ACCOUNT_NAME \
      --sku Standard_LRS \
      --location eastus
    ```

1. 运行以下命令, 将存储帐户连接字符串放置在名为`AZURE_STORAGE_CONNECTION_STRING`的环境变量中。

    ```azurecli
    export AZURE_STORAGE_CONNECTION_STRING=$(az storage account show-connection-string \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $STORAGE_ACCOUNT_NAME \
      --output tsv)
    ```

    `AZURE_STORAGE_CONNECTION_STRING`是 Azure CLI 可理解的特殊环境变量。 此`export`部分将使此变量可供稍后运行的其他 CLI 命令访问。

1. 运行此命令以在存储帐户中创建名为**aci-share-demo**的文件共享。

    ```azurecli
    az storage share create --name aci-share-demo
    ```

## <a name="get-storage-credentials"></a>获取存储凭据

若要在 azure 容器实例中将 Azure 文件共享安装为卷, 您需要以下三个值:

* 存储帐户名称
* 共享名称
* 存储帐户访问密钥

您已具有前两个值。 存储帐户名称存储在`STORAGE_ACCOUNT_NAME` Bash 变量中。 您在上一步中指定了**aci-share-demo**作为共享名称。 在这里, 你将获得存储&mdash;帐户访问密钥的剩余值。

1. 运行以下命令以获取存储帐户密钥。

    ```azurecli
    STORAGE_KEY=$(az storage account keys list \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --account-name $STORAGE_ACCOUNT_NAME \
      --query "[0].value" \
      --output tsv)
    ```

    结果存储在名为`STORAGE_KEY`的 Bash 变量中。

1. 作为可选步骤, 请将存储密钥打印到控制台。

    ```bash
    echo $STORAGE_KEY
    ```

## <a name="deploy-a-container-and-mount-the-file-share"></a>部署容器并装入文件共享

若要在容器中将 Azure 文件共享装载为卷, 请在创建容器时指定共享和卷装入点。

1. 运行此`az container create`命令可创建一个装载`/aci/logs/`到文件共享的容器。

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-files \
      --image microsoft/aci-hellofiles \
      --location eastus \
      --ports 80 \
      --ip-address Public \
      --azure-file-volume-account-name $STORAGE_ACCOUNT_NAME \
      --azure-file-volume-account-key $STORAGE_KEY \
      --azure-file-volume-share-name aci-share-demo \
      --azure-file-volume-mount-path /aci/logs/
    ```

1. 运行`az container show`以获取容器的公共 IP 地址。

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-files \
      --query ipAddress.ip \
      --output tsv
    ```

1. 在浏览器中, 导航到容器的 IP 地址。 你会看到这一点。

    ![Azure 容器实例文件共享演示](../media/5-files-ui.png)

1. 在表单中输入一些文本, 然后单击 "**提交**"。 此操作将创建一个文件, 其中包含您在 Azure 文件共享中输入的文本。

1. 运行此`az storage file list`命令可显示文件共享中包含的文件。

    ```azurecli
    az storage file list -s aci-share-demo -o table
    ```

1. 运行`az storage file download`以将文件下载到你的云命令行管理程序会话。 将** \<filename\> **替换为在上一步中显示的某个文件。

    ```azurecli
    az storage file download -s aci-share-demo -p <filename>
    ```

1. 运行`cat`命令以打印文件的内容。

    ```azurecli
    cat <filename>
    ```

请记住, 当容器退出时, 数据仍然存在。 您可以将文件共享安装到其他容器实例, 以使其可供其使用。
