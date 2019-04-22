现在, 您可以为事件中心配置发布者和使用者应用程序了。

在此单元中, 您将配置这些应用程序以通过事件中心发送或接收邮件。 这些应用程序存储在 GitHub 存储库中。

您将配置两个单独的应用程序;一个充当邮件发件人 (**SimpleSend**), 另一个充当邮件接收器 (**EventProcessorSample**)。 这些是 Java 应用程序, 使您能够在浏览器中执行所有操作。 但是, 任何平台 (如 .net) 都需要相同的配置。

## <a name="create-a-general-purpose-standard-storage-account"></a>创建常规用途的标准存储帐户

您将在此单元中配置的 Java 接收器应用程序将邮件存储在 Azure Blob 存储中。 Blob 存储需要一个存储帐户。

1. 使用`storage account create`命令创建存储帐户 (常规用途 V2)。 请记住, 我们设置了默认资源组和位置, 因此, 即使通常_需要_这些参数, 也可以将其保留下来。

    |参数      |说明|
    |---------------|-----------|
    |--名称 (必需)  | 存储帐户的名称。 |
    |--资源-组 (必需)  |资源组所有者。 我们将使用预创建的沙盒资源组。|
    |--位置 (可选)    |如果您希望存储帐户与资源组的位置相对应, 可选位置。|

    将存储帐户名称设置为变量。 它必须由所有小写字母、数字和允许使用连字符分隔符组成。 它在 Azure 中也必须是唯一的。

    ```azurecli
    STORAGE_NAME=[name]
    ```

    然后, 使用此命令创建存储帐户。

    ```azurecli
    az storage account create --name $STORAGE_NAME --sku Standard_RAGRS --encryption blob
    ```

    > [!TIP]
    > 如果存储帐户创建失败, 请更改环境变量, 然后重试。

1. 使用`account keys list`命令列出与存储帐户关联的所有访问键。 它采用您的帐户名称和资源组 (默认)。

    ```azurecli
    az storage account keys list --account-name $STORAGE_NAME
    ```

     将列出与你的存储帐户关联的访问密钥。 复制并保存**项**的值, 以供将来使用。 你将需要此密钥来访问你的存储帐户。

1. 使用以下命令查看存储帐户的连接字符串:

    ```azurecli
    az storage account show-connection-string -n $STORAGE_NAME
    ```

    此命令返回存储帐户的连接详细信息。 复制并保存**connectionString**的_值_。 其外观应类似于以下内容:

    ```output
    "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=storage_account_name;AccountKey=VZjXuMeuDqjCkT60xX6L5fmtXixYuY2wiPmsrXwYHIhwo736kSAUAj08XBockRZh7CZwYxuYBPe31hi8XfHlWw=="
    ```

1. 使用以下命令在存储帐户中创建名为**messages**的容器。 使用在上一步中复制的**connectionString** :

    ```azurecli
    az storage container create -n messages --connection-string "<connection string here>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a>克隆事件中心 GitHub 存储库

使用以下步骤将事件中心 GitHub 存储库克隆到`git`。 您可以在云命令行管理程序中执行此权限。

1. 你将在此单元中构建的应用程序的源文件位于[GitHub 存储库](https://github.com/Azure/azure-event-hubs)中。 使用以下命令来确保您位于云命令行管理程序的主目录中, 然后克隆此存储库:

    ```bash
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    将存储库克隆到主文件夹中。

## <a name="edit-simplesendjava"></a>编辑 SimpleSend

我们打算使用内置的云命令行管理程序代码编辑器。 这基于摩纳哥编辑器, 类似于 Visual Studio Code, 但完全在线。

我们将使用编辑器修改 SimpleSend 应用程序, 并添加事件中心命名空间、事件中心名称、共享访问策略名称和主键。 主命令显示在编辑器窗口的底部。 

您需要使用<kbd>ctrl + O</kbd>写出您的编辑, 然后<kbd>输入</kbd>以确认输出文件名, 然后使用<kbd>Ctrl + X</kbd>退出编辑器。 或者, 编辑器具有 "..."所有编辑命令的上/右角中的菜单。

1. 转到 " **SimpleSend** " 文件夹。

    ```bash
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. 在当前文件夹中打开代码编辑器。 这将显示左侧的文件列表和右侧的编辑器空间。

    ```bash
    code .
    ```

1. 从 "文件" 列表中选择 " **SimpleSend** " 文件以将其打开。

1. 在编辑器中, 找到并替换以下字符串:

    - `"Your Event Hubs namespace name"`使用事件中心命名空间的名称。
    - `"Your Event Hub"`事件中心的名称。
    - `"Your policy name"`使用**RootManageSharedAccessKey**。
    - `"Your primary SAS key"`使用您之前保存的事件中心命名空间的**primaryKey**键的值。
 
    > [!TIP]
    > 与终端窗口不同, 编辑器可以对操作系统使用典型的复制/粘贴键盘加速键。

    如果您忘记了其中的部分, 您可以切换到编辑器下方的 "终端" 窗口, 并使用`echo`该命令列出一个环境变量。 例如：

    ```bash
    echo $NS_NAME
    ```
    创建事件中心命名空间时, 将创建一个名为 " **RootManageSharedAccessKey** " 的256位 SAS 密钥, 该密钥具有对命名空间授予 "发送"、"侦听" 和 "管理" 权限的关联主键和辅助密钥的关联对。 在上面的单元中, 使用 azure CLI 命令显示密钥, 您还可以通过在 azure 门户中打开事件中心命名空间的 "**共享访问策略**" 页来查找此项。

1. 通过 "..." 保存**SimpleSend**菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

1. 通过 "..." 关闭编辑器。菜单或加速键<kbd>CTRL + Q</kbd>。

## <a name="use-maven-to-build-simplesendjava"></a>使用 Maven 生成 SimpleSend

现在, 您将使用**mvn**命令生成 Java 应用程序。

1. 将更改回主**SimpleSend**文件夹。

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. 构建 Java SimpleSend 应用程序。 这将确保应用程序使用事件中心的连接详细信息:

    ```bash
    mvn clean package -DskipTests
    ```

    生成过程可能需要几分钟的时间才能完成。 在继续之前, 请确保您看到 **[INFO] 生成成功**消息。

    ![发件人应用程序的生成结果](../media/5-sender-build.png)

## <a name="edit-eventprocessorsamplejava"></a>编辑 EventProcessorSample

现在, 您将配置**接收器**(也称为**订阅者**或**使用者**) 应用程序, 以从事件中心中插入数据。

对于接收器应用程序, 可以使用两种方法;**EventHubReceiver**和**EventProcessorHost**。 EventProcessorHost 建立在 EventHubReceiver 的基础之上, 但提供比 EventHubReceiver 更简单的编程接口。 EventProcessorHost 可以使用相同的存储帐户跨 EventProcessorHost 的多个实例自动分发邮件分区。

在此单元中, 您将使用 EventProcessorHost 方法。 您将编辑 EventProcessorSample 应用程序, 以添加事件中心命名空间、事件中心名称、共享访问策略名称和主键、存储帐户名称、连接字符串和容器名称。

1. 使用以下命令切换到**EventProcessorSample**文件夹:

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. 打开代码编辑器。

    ```bash
    code .
    ```
    
1. 选择 " **EventProcessorSample** " 文件。

1. 在编辑器中查找并替换以下字符串:

    - `----ServiceBusNamespaceName----`使用事件中心命名空间的名称。
    - `----EventHubName----`事件中心的名称。
    - `----SharedAccessSignatureKeyName----`使用**RootManageSharedAccessKey**。
    - `----SharedAccessSignatureKey----`使用您之前保存的事件中心命名空间的**primaryKey**键的值。
    - `----AzureStorageConnectionString----`您之前保存的存储帐户连接字符串。
    - `----StorageContainerName----`**邮件**。
    - `----HostNamePrefix----`存储帐户的名称。

1. 通过 "..." 保存**EventProcessorSample**菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。

1. 关闭编辑器。

## <a name="use-maven-to-build-eventprocessorsamplejava"></a>使用 Maven 生成 EventProcessorSample

1. 使用以下命令切换到主**EventProcessorSample**文件夹:

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. 使用以下命令生成 Java SimpleSend 应用程序。 这将确保应用程序使用事件中心的连接详细信息:

    ```bash
    mvn clean package -DskipTests
    ```

    生成过程可能需要几分钟的时间才能完成。 在继续之前, 请确保您看到 **[INFO] 生成成功**消息。

    ![接收器应用程序的生成结果](../media/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a>启动发件人和收件人应用

1. 通过使用**java**命令并指定一个 .jar 包, 从命令行运行 java 应用程序。 使用以下命令启动 SimpleSend 应用程序:

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. 如果看到 "**发送完成 ...**", 请按<kbd>enter</kbd>。

    ```output
    jar-with-dependencies.jar
    SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    SLF4J: Defaulting to no-operation (NOP) logger implementation
    SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    2018-09-18T19:42:15.146Z: Send Complete...
    ```

1. 使用以下命令启动 EventProcessorSample 应用程序。

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. 当邮件停止显示到控制台时, 按<kbd>enter</kbd>或<kbd>CTRL + C</kbd>结束该程序。

    ```output
    ...
    SAMPLE: Partition 0 checkpointing at 1064,19
    SAMPLE (3,1120,20): "Message 80"
    SAMPLE (3,1176,21): "Message 84"
    SAMPLE (3,1232,22): "Message 88"
    SAMPLE (3,1288,23): "Message 92"
    SAMPLE (3,1344,24): "Message 96"
    SAMPLE: Partition 3 checkpointing at 1344,24
    SAMPLE (2,1120,20): "Message 83"
    SAMPLE (2,1176,21): "Message 87"
    SAMPLE (2,1232,22): "Message 91"
    SAMPLE (2,1288,23): "Message 95"
    SAMPLE (2,1344,24): "Message 99"
    SAMPLE: Partition 2 checkpointing at 1344,24
    SAMPLE: Partition 1 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE (0,1120,20): "Message 81"
    SAMPLE (0,1176,21): "Message 85"
    SAMPLE: Partition 0 batch size was 10 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 got event batch
    SAMPLE (0,1232,22): "Message 89"
    SAMPLE (0,1288,23): "Message 93"
    SAMPLE (0,1344,24): "Message 97"
    SAMPLE: Partition 0 checkpointing at 1344,24
    SAMPLE: Partition 3 batch size was 8 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 2 batch size was 9 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    ```

## <a name="summary"></a>摘要

现在, 已将发件人应用程序配置为可以向事件中心发送邮件。 您还配置了一个接收器应用程序, 可以从事件中心接收邮件。