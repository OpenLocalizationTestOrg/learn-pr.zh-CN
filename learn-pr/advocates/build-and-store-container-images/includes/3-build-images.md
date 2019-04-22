假设您的公司使用容器映像来管理计算工作负载。 您可以使用本地 Docker 工具生成容器图像。

现在, 你可以使用 Azure 容器注册表任务生成这些容器。 容器注册表任务还允许在源代码提交时进行 DevOps 进程与自动生成的集成。

让我们使用 Azure 容器注册表任务自动创建容器映像。

## <a name="create-a-container-image-with-azure-container-registry-tasks"></a>使用 Azure 容器注册表任务创建容器映像

标准 Dockerfile 提供了生成说明。 通过 Azure 容器注册表任务, 您可以重复使用环境中当前的任何 Dockerfile, 包括多暂存版本。

我们将为我们的示例使用新的 Dockerfile。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

第一步是创建一个名为`Dockerfile`的新文件。 您可以使用任何文本编辑器来编辑文件。 在此示例中, 我们将使用云命令行管理程序编辑器。

1. 在 "云命令行管理器" 窗口中输入以下命令以打开编辑器。

    ```bash
    code
    ```

1. 复制以下内容编辑器。

    ```bash
    FROM    node:9-alpine
    ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
    ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
    RUN     npm install
    EXPOSE  80
    CMD     ["node", "server.js"]
    ```

1. 使用组合键<kbd>Ctrl + s</kbd> (<kbd>Cmd + s</kbd> for Mac) 保存所做的更改。 在收到提示`Dockerfile`时对文件命名。

    此配置将 node.js 应用程序添加到`node:9-alpine`映像中。 然后, 它将容器配置为通过*公开*指令为端口80上的应用程序提供服务。

1. 运行以下 Azure CLI 命令, 以从 Dockerfile 生成容器映像。 *$ACR _name*是您在前面的单元中定义的用于保存您的容器注册表名称的变量。

    ```azurecli
    az acr build --registry $ACR_NAME --image helloacrtasks:v1 .
    ```

    > [!NOTE]
    > 不要忘记上述命令`.`末尾的时间段。 它表示包含 docker 文件的源目录, 在这种情况下, 在我们的示例中为当前目录。 由于未使用--file 参数指定文件的名称, 命令会在当前目录中查找名为 " **Dockerfile** " 的文件。

## <a name="verify-the-image"></a>验证图像

1. 在云命令行管理程序中运行以下命令, 以验证是否已创建映像并将其存储在注册表中。

    ```azurecli
    az acr repository list --name $ACR_NAME --output table
    ```

    此命令的输出应类似于以下形式:
    
    ```console
    Result
    -------------
    helloacrtasks
    ```

现`helloacrtasks`已准备好使用该图像。
