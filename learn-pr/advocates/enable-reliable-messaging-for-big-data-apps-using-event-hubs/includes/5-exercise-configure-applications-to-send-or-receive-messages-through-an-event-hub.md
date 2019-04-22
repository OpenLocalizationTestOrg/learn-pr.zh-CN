<span data-ttu-id="44b00-101">现在, 您可以为事件中心配置发布者和使用者应用程序了。</span><span class="sxs-lookup"><span data-stu-id="44b00-101">You're now ready to configure your publisher and consumer applications for your Event Hub.</span></span>

<span data-ttu-id="44b00-102">在此单元中, 您将配置这些应用程序以通过事件中心发送或接收邮件。</span><span class="sxs-lookup"><span data-stu-id="44b00-102">In this unit, you'll configure these applications to send or receive messages through your Event Hub.</span></span> <span data-ttu-id="44b00-103">这些应用程序存储在 GitHub 存储库中。</span><span class="sxs-lookup"><span data-stu-id="44b00-103">These applications are stored in a GitHub repository.</span></span>

<span data-ttu-id="44b00-104">您将配置两个单独的应用程序;一个充当邮件发件人 (**SimpleSend**), 另一个充当邮件接收器 (**EventProcessorSample**)。</span><span class="sxs-lookup"><span data-stu-id="44b00-104">You'll configure two separate applications; one acts as the message sender (**SimpleSend**), the other as the message receiver (**EventProcessorSample**).</span></span> <span data-ttu-id="44b00-105">这些是 Java 应用程序, 使您能够在浏览器中执行所有操作。</span><span class="sxs-lookup"><span data-stu-id="44b00-105">These are Java applications, which enable you to do everything within the browser.</span></span> <span data-ttu-id="44b00-106">但是, 任何平台 (如 .net) 都需要相同的配置。</span><span class="sxs-lookup"><span data-stu-id="44b00-106">However, the same configuration is needed for any platform, such as .NET.</span></span>

## <a name="create-a-general-purpose-standard-storage-account"></a><span data-ttu-id="44b00-107">创建常规用途的标准存储帐户</span><span class="sxs-lookup"><span data-stu-id="44b00-107">Create a general-purpose, standard storage account</span></span>

<span data-ttu-id="44b00-108">您将在此单元中配置的 Java 接收器应用程序将邮件存储在 Azure Blob 存储中。</span><span class="sxs-lookup"><span data-stu-id="44b00-108">The Java receiver application, that you'll configure in this unit, stores messages in Azure Blob Storage.</span></span> <span data-ttu-id="44b00-109">Blob 存储需要一个存储帐户。</span><span class="sxs-lookup"><span data-stu-id="44b00-109">Blob Storage requires a storage account.</span></span>

1. <span data-ttu-id="44b00-110">使用`storage account create`命令创建存储帐户 (常规用途 V2)。</span><span class="sxs-lookup"><span data-stu-id="44b00-110">Create a storage account (general-purpose V2) using the `storage account create` command.</span></span> <span data-ttu-id="44b00-111">请记住, 我们设置了默认资源组和位置, 因此, 即使通常_需要_这些参数, 也可以将其保留下来。</span><span class="sxs-lookup"><span data-stu-id="44b00-111">Remember we set a default resource group and location, so even though those parameters are normally _required_, we can leave them off.</span></span>

    |<span data-ttu-id="44b00-112">参数</span><span class="sxs-lookup"><span data-stu-id="44b00-112">Parameter</span></span>      |<span data-ttu-id="44b00-113">说明</span><span class="sxs-lookup"><span data-stu-id="44b00-113">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="44b00-114">--名称 (必需)</span><span class="sxs-lookup"><span data-stu-id="44b00-114">--name (required)</span></span>  | <span data-ttu-id="44b00-115">存储帐户的名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-115">A name for your storage account.</span></span> |
    |<span data-ttu-id="44b00-116">--资源-组 (必需)</span><span class="sxs-lookup"><span data-stu-id="44b00-116">--resource-group (required)</span></span>  |<span data-ttu-id="44b00-117">资源组所有者。</span><span class="sxs-lookup"><span data-stu-id="44b00-117">The resource group owner.</span></span> <span data-ttu-id="44b00-118">我们将使用预创建的沙盒资源组。</span><span class="sxs-lookup"><span data-stu-id="44b00-118">We'll use the pre-created sandbox resource group.</span></span>|
    |<span data-ttu-id="44b00-119">--位置 (可选)</span><span class="sxs-lookup"><span data-stu-id="44b00-119">--location (optional)</span></span>    |<span data-ttu-id="44b00-120">如果您希望存储帐户与资源组的位置相对应, 可选位置。</span><span class="sxs-lookup"><span data-stu-id="44b00-120">An optional location if you want the storage account in a specific place vs. the resource group location.</span></span>|

    <span data-ttu-id="44b00-121">将存储帐户名称设置为变量。</span><span class="sxs-lookup"><span data-stu-id="44b00-121">Set the storage account name into a variable.</span></span> <span data-ttu-id="44b00-122">它必须由所有小写字母、数字和允许使用连字符分隔符组成。</span><span class="sxs-lookup"><span data-stu-id="44b00-122">It must be composed of all lower-case letters, numbers, with hyphen separators allowed.</span></span> <span data-ttu-id="44b00-123">它在 Azure 中也必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="44b00-123">It also must be unique within Azure.</span></span>

    ```azurecli
    STORAGE_NAME=[name]
    ```

    <span data-ttu-id="44b00-124">然后, 使用此命令创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="44b00-124">Then use this command to create the storage account.</span></span>

    ```azurecli
    az storage account create --name $STORAGE_NAME --sku Standard_RAGRS --encryption blob
    ```

    > [!TIP]
    > <span data-ttu-id="44b00-125">如果存储帐户创建失败, 请更改环境变量, 然后重试。</span><span class="sxs-lookup"><span data-stu-id="44b00-125">If the storage account creation fails, change your environment variable and try again.</span></span>

1. <span data-ttu-id="44b00-126">使用`account keys list`命令列出与存储帐户关联的所有访问键。</span><span class="sxs-lookup"><span data-stu-id="44b00-126">List all the access keys associated with your storage account using the `account keys list` command.</span></span> <span data-ttu-id="44b00-127">它采用您的帐户名称和资源组 (默认)。</span><span class="sxs-lookup"><span data-stu-id="44b00-127">It takes your account name and the resource group (which is defaulted).</span></span>

    ```azurecli
    az storage account keys list --account-name $STORAGE_NAME
    ```

     <span data-ttu-id="44b00-128">将列出与你的存储帐户关联的访问密钥。</span><span class="sxs-lookup"><span data-stu-id="44b00-128">Access keys associated with your storage account are listed.</span></span> <span data-ttu-id="44b00-129">复制并保存**项**的值, 以供将来使用。</span><span class="sxs-lookup"><span data-stu-id="44b00-129">Copy and save the value of **key** for future use.</span></span> <span data-ttu-id="44b00-130">你将需要此密钥来访问你的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="44b00-130">You'll need this key to access your storage account.</span></span>

1. <span data-ttu-id="44b00-131">使用以下命令查看存储帐户的连接字符串:</span><span class="sxs-lookup"><span data-stu-id="44b00-131">View the connections string for your storage account using the following command:</span></span>

    ```azurecli
    az storage account show-connection-string -n $STORAGE_NAME
    ```

    <span data-ttu-id="44b00-132">此命令返回存储帐户的连接详细信息。</span><span class="sxs-lookup"><span data-stu-id="44b00-132">This command returns the connection details for the storage account.</span></span> <span data-ttu-id="44b00-133">复制并保存**connectionString**的_值_。</span><span class="sxs-lookup"><span data-stu-id="44b00-133">Copy and save the _value_ of **connectionString**.</span></span> <span data-ttu-id="44b00-134">其外观应类似于以下内容:</span><span class="sxs-lookup"><span data-stu-id="44b00-134">It should look something like:</span></span>

    ```output
    "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=storage_account_name;AccountKey=VZjXuMeuDqjCkT60xX6L5fmtXixYuY2wiPmsrXwYHIhwo736kSAUAj08XBockRZh7CZwYxuYBPe31hi8XfHlWw=="
    ```

1. 使用以下命令在存储帐户中创建名为**messages**的容器。 <span data-ttu-id="44b00-136">使用在上一步中复制的**connectionString** :</span><span class="sxs-lookup"><span data-stu-id="44b00-136">Use the **connectionString** you copied in the previous step:</span></span>

    ```azurecli
    az storage container create -n messages --connection-string "<connection string here>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a><span data-ttu-id="44b00-137">克隆事件中心 GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="44b00-137">Clone the Event Hubs GitHub repository</span></span>

<span data-ttu-id="44b00-138">使用以下步骤将事件中心 GitHub 存储库克隆到`git`。</span><span class="sxs-lookup"><span data-stu-id="44b00-138">Use the following steps to clone the Event Hubs GitHub repository with `git`.</span></span> <span data-ttu-id="44b00-139">您可以在云命令行管理程序中执行此权限。</span><span class="sxs-lookup"><span data-stu-id="44b00-139">You can execute this right in the Cloud Shell.</span></span>

1. <span data-ttu-id="44b00-140">你将在此单元中构建的应用程序的源文件位于[GitHub 存储库](https://github.com/Azure/azure-event-hubs)中。</span><span class="sxs-lookup"><span data-stu-id="44b00-140">The source files for the applications that you'll build in this unit are located in a [GitHub repository](https://github.com/Azure/azure-event-hubs).</span></span> <span data-ttu-id="44b00-141">使用以下命令来确保您位于云命令行管理程序的主目录中, 然后克隆此存储库:</span><span class="sxs-lookup"><span data-stu-id="44b00-141">Use the following commands to make sure that you are in your home directory in Cloud Shell, and then to clone this repository:</span></span>

    ```bash
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    <span data-ttu-id="44b00-142">将存储库克隆到主文件夹中。</span><span class="sxs-lookup"><span data-stu-id="44b00-142">The repository is cloned to your home folder.</span></span>

## <a name="edit-simplesendjava"></a><span data-ttu-id="44b00-143">编辑 SimpleSend</span><span class="sxs-lookup"><span data-stu-id="44b00-143">Edit SimpleSend.java</span></span>

<span data-ttu-id="44b00-144">我们打算使用内置的云命令行管理程序代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="44b00-144">We're going to use the built-in Cloud Shell Code editor.</span></span> <span data-ttu-id="44b00-145">这基于摩纳哥编辑器, 类似于 Visual Studio Code, 但完全在线。</span><span class="sxs-lookup"><span data-stu-id="44b00-145">This is based on the Monaco editor and is similar to Visual Studio Code, but completely online.</span></span>

<span data-ttu-id="44b00-146">我们将使用编辑器修改 SimpleSend 应用程序, 并添加事件中心命名空间、事件中心名称、共享访问策略名称和主键。</span><span class="sxs-lookup"><span data-stu-id="44b00-146">We'll use the editor to modify the SimpleSend application and add your Event Hubs namespace, Event Hub name, shared access policy name, and primary key.</span></span> <span data-ttu-id="44b00-147">主命令显示在编辑器窗口的底部。</span><span class="sxs-lookup"><span data-stu-id="44b00-147">The main commands are displayed at the bottom of the editor window.</span></span> 

<span data-ttu-id="44b00-148">您需要使用<kbd>ctrl + O</kbd>写出您的编辑, 然后<kbd>输入</kbd>以确认输出文件名, 然后使用<kbd>Ctrl + X</kbd>退出编辑器。</span><span class="sxs-lookup"><span data-stu-id="44b00-148">You'll need to write out your edits using <kbd>Ctrl+O</kbd>, and then <kbd>ENTER</kbd> to confirm the output file name, and exit the editor using <kbd>Ctrl+X</kbd>.</span></span> <span data-ttu-id="44b00-149">或者, 编辑器具有 "..."所有编辑命令的上/右角中的菜单。</span><span class="sxs-lookup"><span data-stu-id="44b00-149">Alternatively, the editor has a "..." menu in the top/right corner for all the editing commands.</span></span>

1. <span data-ttu-id="44b00-150">转到 " **SimpleSend** " 文件夹。</span><span class="sxs-lookup"><span data-stu-id="44b00-150">Change to the **SimpleSend** folder.</span></span>

    ```bash
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. <span data-ttu-id="44b00-151">在当前文件夹中打开代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="44b00-151">Open the code editor in the current folder.</span></span> <span data-ttu-id="44b00-152">这将显示左侧的文件列表和右侧的编辑器空间。</span><span class="sxs-lookup"><span data-stu-id="44b00-152">This will show a list of files on the left and an editor space on the right.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="44b00-153">从 "文件" 列表中选择 " **SimpleSend** " 文件以将其打开。</span><span class="sxs-lookup"><span data-stu-id="44b00-153">Open the **SimpleSend.java** file by selecting it from the file list.</span></span>

1. <span data-ttu-id="44b00-154">在编辑器中, 找到并替换以下字符串:</span><span class="sxs-lookup"><span data-stu-id="44b00-154">In the editor, locate and replace the following strings:</span></span>

    - <span data-ttu-id="44b00-155">`"Your Event Hubs namespace name"`使用事件中心命名空间的名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-155">`"Your Event Hubs namespace name"` with the name of your Event Hub namespace.</span></span>
    - <span data-ttu-id="44b00-156">`"Your Event Hub"`事件中心的名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-156">`"Your Event Hub"` with the name of your Event Hub.</span></span>
    - <span data-ttu-id="44b00-157">`"Your policy name"`使用**RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="44b00-157">`"Your policy name"` with **RootManageSharedAccessKey**.</span></span>
    - <span data-ttu-id="44b00-158">`"Your primary SAS key"`使用您之前保存的事件中心命名空间的**primaryKey**键的值。</span><span class="sxs-lookup"><span data-stu-id="44b00-158">`"Your primary SAS key"` with the value of the **primaryKey** key for your Event Hub namespace that you saved earlier.</span></span>
 
    > [!TIP]
    > <span data-ttu-id="44b00-159">与终端窗口不同, 编辑器可以对操作系统使用典型的复制/粘贴键盘加速键。</span><span class="sxs-lookup"><span data-stu-id="44b00-159">Unlike the terminal window, the editor can use typical copy/paste keyboard accelerator keys for your OS.</span></span>

    <span data-ttu-id="44b00-160">如果您忘记了其中的部分, 您可以切换到编辑器下方的 "终端" 窗口, 并使用`echo`该命令列出一个环境变量。</span><span class="sxs-lookup"><span data-stu-id="44b00-160">If you've forgotten some of them, you can switch down to the terminal window below the editor and use the `echo` command to list out one of the environment variables.</span></span> <span data-ttu-id="44b00-161">例如：</span><span class="sxs-lookup"><span data-stu-id="44b00-161">For example:</span></span>

    ```bash
    echo $NS_NAME
    ```
    <span data-ttu-id="44b00-162">创建事件中心命名空间时, 将创建一个名为 " **RootManageSharedAccessKey** " 的256位 SAS 密钥, 该密钥具有对命名空间授予 "发送"、"侦听" 和 "管理" 权限的关联主键和辅助密钥的关联对。</span><span class="sxs-lookup"><span data-stu-id="44b00-162">When you create an Event Hubs namespace, a 256-bit SAS key called **RootManageSharedAccessKey** is created that has an associated pair of primary and secondary keys that grant send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="44b00-163">在上面的单元中, 使用 azure CLI 命令显示密钥, 您还可以通过在 azure 门户中打开事件中心命名空间的 "**共享访问策略**" 页来查找此项。</span><span class="sxs-lookup"><span data-stu-id="44b00-163">In the previous unit, you displayed the key using an Azure CLI command, and you can also find this key by opening the **Shared access policies** page for your Event Hubs namespace in the Azure portal.</span></span>

1. <span data-ttu-id="44b00-164">通过 "..." 保存**SimpleSend**菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="44b00-164">Save **SimpleSend.java** either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="44b00-165">通过 "..." 关闭编辑器。菜单或加速键<kbd>CTRL + Q</kbd>。</span><span class="sxs-lookup"><span data-stu-id="44b00-165">Close the editor through the "..." menu, or the accelerator key <kbd>CTRL+Q</kbd>.</span></span>

## <a name="use-maven-to-build-simplesendjava"></a><span data-ttu-id="44b00-166">使用 Maven 生成 SimpleSend</span><span class="sxs-lookup"><span data-stu-id="44b00-166">Use Maven to build SimpleSend.java</span></span>

<span data-ttu-id="44b00-167">现在, 您将使用**mvn**命令生成 Java 应用程序。</span><span class="sxs-lookup"><span data-stu-id="44b00-167">You'll now build the Java application using **mvn** commands.</span></span>

1. <span data-ttu-id="44b00-168">将更改回主**SimpleSend**文件夹。</span><span class="sxs-lookup"><span data-stu-id="44b00-168">Change back to the main **SimpleSend** folder.</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. <span data-ttu-id="44b00-169">构建 Java SimpleSend 应用程序。</span><span class="sxs-lookup"><span data-stu-id="44b00-169">Build the Java SimpleSend application.</span></span> <span data-ttu-id="44b00-170">这将确保应用程序使用事件中心的连接详细信息:</span><span class="sxs-lookup"><span data-stu-id="44b00-170">This ensures that your application  uses the connection details for your Event Hub:</span></span>

    ```bash
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="44b00-171">生成过程可能需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="44b00-171">The build process may take several minutes to complete.</span></span> <span data-ttu-id="44b00-172">在继续之前, 请确保您看到 **[INFO] 生成成功**消息。</span><span class="sxs-lookup"><span data-stu-id="44b00-172">Ensure that you see the **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![发件人应用程序的生成结果](../media/5-sender-build.png)

## <a name="edit-eventprocessorsamplejava"></a><span data-ttu-id="44b00-174">编辑 EventProcessorSample</span><span class="sxs-lookup"><span data-stu-id="44b00-174">Edit EventProcessorSample.java</span></span>

<span data-ttu-id="44b00-175">现在, 您将配置**接收器**(也称为**订阅者**或**使用者**) 应用程序, 以从事件中心中插入数据。</span><span class="sxs-lookup"><span data-stu-id="44b00-175">You'll now configure a **receiver** (also known as **subscribers** or **consumers**) application to ingest data from your Event Hub.</span></span>

<span data-ttu-id="44b00-176">对于接收器应用程序, 可以使用两种方法;**EventHubReceiver**和**EventProcessorHost**。</span><span class="sxs-lookup"><span data-stu-id="44b00-176">For the receiver application, two methods are available; **EventHubReceiver** and **EventProcessorHost**.</span></span> <span data-ttu-id="44b00-177">EventProcessorHost 建立在 EventHubReceiver 的基础之上, 但提供比 EventHubReceiver 更简单的编程接口。</span><span class="sxs-lookup"><span data-stu-id="44b00-177">EventProcessorHost is built on top of EventHubReceiver, but provides simpler programmatic interface than EventHubReceiver.</span></span> <span data-ttu-id="44b00-178">EventProcessorHost 可以使用相同的存储帐户跨 EventProcessorHost 的多个实例自动分发邮件分区。</span><span class="sxs-lookup"><span data-stu-id="44b00-178">EventProcessorHost can automatically distribute message partitions across multiple instances of EventProcessorHost using the same storage account.</span></span>

<span data-ttu-id="44b00-179">在此单元中, 您将使用 EventProcessorHost 方法。</span><span class="sxs-lookup"><span data-stu-id="44b00-179">In this unit, you’ll use the EventProcessorHost method.</span></span> <span data-ttu-id="44b00-180">您将编辑 EventProcessorSample 应用程序, 以添加事件中心命名空间、事件中心名称、共享访问策略名称和主键、存储帐户名称、连接字符串和容器名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-180">You'll edit the EventProcessorSample application to add your Event Hubs namespace, Event Hub name, shared access policy name and primary key, storage account name, connection string, and container name.</span></span>

1. <span data-ttu-id="44b00-181">使用以下命令切换到**EventProcessorSample**文件夹:</span><span class="sxs-lookup"><span data-stu-id="44b00-181">Change to the **EventProcessorSample** folder using the following command:</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. <span data-ttu-id="44b00-182">打开代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="44b00-182">Open the code editor.</span></span>

    ```bash
    code .
    ```
    
1. <span data-ttu-id="44b00-183">选择 " **EventProcessorSample** " 文件。</span><span class="sxs-lookup"><span data-stu-id="44b00-183">Select the **EventProcessorSample.java** file.</span></span>

1. <span data-ttu-id="44b00-184">在编辑器中查找并替换以下字符串:</span><span class="sxs-lookup"><span data-stu-id="44b00-184">Locate and replace the following strings in the editor:</span></span>

    - <span data-ttu-id="44b00-185">`----ServiceBusNamespaceName----`使用事件中心命名空间的名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-185">`----ServiceBusNamespaceName----` with the name of your Event Hubs namespace.</span></span>
    - <span data-ttu-id="44b00-186">`----EventHubName----`事件中心的名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-186">`----EventHubName----` with the name of your Event Hub.</span></span>
    - <span data-ttu-id="44b00-187">`----SharedAccessSignatureKeyName----`使用**RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="44b00-187">`----SharedAccessSignatureKeyName----` with **RootManageSharedAccessKey**.</span></span>
    - <span data-ttu-id="44b00-188">`----SharedAccessSignatureKey----`使用您之前保存的事件中心命名空间的**primaryKey**键的值。</span><span class="sxs-lookup"><span data-stu-id="44b00-188">`----SharedAccessSignatureKey----` with the value of the **primaryKey** key for your Event Hubs namespace that you saved earlier.</span></span>
    - <span data-ttu-id="44b00-189">`----AzureStorageConnectionString----`您之前保存的存储帐户连接字符串。</span><span class="sxs-lookup"><span data-stu-id="44b00-189">`----AzureStorageConnectionString----` with your storage account connection string that you saved earlier.</span></span>
    - <span data-ttu-id="44b00-190">`----StorageContainerName----`**邮件**。</span><span class="sxs-lookup"><span data-stu-id="44b00-190">`----StorageContainerName----` with **messages**.</span></span>
    - <span data-ttu-id="44b00-191">`----HostNamePrefix----`存储帐户的名称。</span><span class="sxs-lookup"><span data-stu-id="44b00-191">`----HostNamePrefix----` with the name of your storage account.</span></span>

1. <span data-ttu-id="44b00-192">通过 "..." 保存**EventProcessorSample**菜单或加速键 (Windows 和 Linux 上的<kbd>Ctrl + s</kbd> 、macOS 上的<kbd>Cmd + s</kbd> )。</span><span class="sxs-lookup"><span data-stu-id="44b00-192">Save **EventProcessorSample.java** either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="44b00-193">关闭编辑器。</span><span class="sxs-lookup"><span data-stu-id="44b00-193">Close the editor.</span></span>

## <a name="use-maven-to-build-eventprocessorsamplejava"></a><span data-ttu-id="44b00-194">使用 Maven 生成 EventProcessorSample</span><span class="sxs-lookup"><span data-stu-id="44b00-194">Use Maven to build EventProcessorSample.java</span></span>

1. <span data-ttu-id="44b00-195">使用以下命令切换到主**EventProcessorSample**文件夹:</span><span class="sxs-lookup"><span data-stu-id="44b00-195">Change to the main **EventProcessorSample** folder using the following command:</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. <span data-ttu-id="44b00-196">使用以下命令生成 Java SimpleSend 应用程序。</span><span class="sxs-lookup"><span data-stu-id="44b00-196">Build the Java SimpleSend application using the following command.</span></span> <span data-ttu-id="44b00-197">这将确保应用程序使用事件中心的连接详细信息:</span><span class="sxs-lookup"><span data-stu-id="44b00-197">This ensures that your application uses the connection details for your Event Hub:</span></span>

    ```bash
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="44b00-198">生成过程可能需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="44b00-198">The build process may take several minutes to complete.</span></span> <span data-ttu-id="44b00-199">在继续之前, 请确保您看到 **[INFO] 生成成功**消息。</span><span class="sxs-lookup"><span data-stu-id="44b00-199">Ensure that you see a **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![接收器应用程序的生成结果](../media/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a><span data-ttu-id="44b00-201">启动发件人和收件人应用</span><span class="sxs-lookup"><span data-stu-id="44b00-201">Start the sender and receiver apps</span></span>

1. <span data-ttu-id="44b00-202">通过使用**java**命令并指定一个 .jar 包, 从命令行运行 java 应用程序。</span><span class="sxs-lookup"><span data-stu-id="44b00-202">Run Java application from the command line by using the **java** command, and specifying a .jar package.</span></span> <span data-ttu-id="44b00-203">使用以下命令启动 SimpleSend 应用程序:</span><span class="sxs-lookup"><span data-stu-id="44b00-203">Use the following commands to start the SimpleSend application:</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="44b00-204">如果看到 "**发送完成 ...**", 请按<kbd>enter</kbd>。</span><span class="sxs-lookup"><span data-stu-id="44b00-204">When you see **Send Complete...**, press <kbd>ENTER</kbd>.</span></span>

    ```output
    jar-with-dependencies.jar
    SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    SLF4J: Defaulting to no-operation (NOP) logger implementation
    SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    2018-09-18T19:42:15.146Z: Send Complete...
    ```

1. <span data-ttu-id="44b00-205">使用以下命令启动 EventProcessorSample 应用程序。</span><span class="sxs-lookup"><span data-stu-id="44b00-205">Start the EventProcessorSample application using the following command.</span></span>

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="44b00-206">当邮件停止显示到控制台时, 按<kbd>enter</kbd>或<kbd>CTRL + C</kbd>结束该程序。</span><span class="sxs-lookup"><span data-stu-id="44b00-206">When messages stop being displayed to the console, press <kbd>ENTER</kbd> or <kbd>CTRL+C</kbd> to end the program.</span></span>

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

## <a name="summary"></a><span data-ttu-id="44b00-207">摘要</span><span class="sxs-lookup"><span data-stu-id="44b00-207">Summary</span></span>

<span data-ttu-id="44b00-208">现在, 已将发件人应用程序配置为可以向事件中心发送邮件。</span><span class="sxs-lookup"><span data-stu-id="44b00-208">You've now configured a sender application ready to send messages to your Event Hub.</span></span> <span data-ttu-id="44b00-209">您还配置了一个接收器应用程序, 可以从事件中心接收邮件。</span><span class="sxs-lookup"><span data-stu-id="44b00-209">You've also configured a receiver application ready to receive messages from your Event Hub.</span></span>