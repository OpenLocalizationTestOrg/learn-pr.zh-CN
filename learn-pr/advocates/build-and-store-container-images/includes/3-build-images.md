<span data-ttu-id="02847-101">假设您的公司使用容器映像来管理计算工作负载。</span><span class="sxs-lookup"><span data-stu-id="02847-101">Suppose your company makes use of container images to manage compute workloads.</span></span> <span data-ttu-id="02847-102">您可以使用本地 Docker 工具生成容器图像。</span><span class="sxs-lookup"><span data-stu-id="02847-102">You use the local Docker tooling to build your container images.</span></span>

<span data-ttu-id="02847-103">现在, 你可以使用 Azure 容器注册表任务生成这些容器。</span><span class="sxs-lookup"><span data-stu-id="02847-103">You can now use Azure Container Registry Tasks to build these containers.</span></span> <span data-ttu-id="02847-104">容器注册表任务还允许在源代码提交时进行 DevOps 进程与自动生成的集成。</span><span class="sxs-lookup"><span data-stu-id="02847-104">Container Registry Tasks also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="02847-105">让我们使用 Azure 容器注册表任务自动创建容器映像。</span><span class="sxs-lookup"><span data-stu-id="02847-105">Let's automate the creation of a container image using Azure Container Registry Tasks.</span></span>

## <a name="create-a-container-image-with-azure-container-registry-tasks"></a><span data-ttu-id="02847-106">使用 Azure 容器注册表任务创建容器映像</span><span class="sxs-lookup"><span data-stu-id="02847-106">Create a container image with Azure Container Registry Tasks</span></span>

<span data-ttu-id="02847-107">标准 Dockerfile 提供了生成说明。</span><span class="sxs-lookup"><span data-stu-id="02847-107">A standard Dockerfile provides build instructions.</span></span> <span data-ttu-id="02847-108">通过 Azure 容器注册表任务, 您可以重复使用环境中当前的任何 Dockerfile, 包括多暂存版本。</span><span class="sxs-lookup"><span data-stu-id="02847-108">Azure Container Registry Tasks allows you to reuse any Dockerfile currently in your environment, including multi-staged builds.</span></span>

<span data-ttu-id="02847-109">我们将为我们的示例使用新的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="02847-109">We'll use a new Dockerfile for our example.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="02847-110">第一步是创建一个名为`Dockerfile`的新文件。</span><span class="sxs-lookup"><span data-stu-id="02847-110">The first step is to create a new file named `Dockerfile`.</span></span> <span data-ttu-id="02847-111">您可以使用任何文本编辑器来编辑文件。</span><span class="sxs-lookup"><span data-stu-id="02847-111">You can use any text editor to edit the file.</span></span> <span data-ttu-id="02847-112">在此示例中, 我们将使用云命令行管理程序编辑器。</span><span class="sxs-lookup"><span data-stu-id="02847-112">We'll use Cloud Shell Editor for this example.</span></span>

1. <span data-ttu-id="02847-113">在 "云命令行管理器" 窗口中输入以下命令以打开编辑器。</span><span class="sxs-lookup"><span data-stu-id="02847-113">Enter the following command into the Cloud Shell window to open the editor.</span></span>

    ```bash
    code
    ```

1. <span data-ttu-id="02847-114">复制以下内容编辑器。</span><span class="sxs-lookup"><span data-stu-id="02847-114">Copy the following contents editor.</span></span>

    ```bash
    FROM    node:9-alpine
    ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
    ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
    RUN     npm install
    EXPOSE  80
    CMD     ["node", "server.js"]
    ```

1. <span data-ttu-id="02847-115">使用组合键<kbd>Ctrl + s</kbd> (<kbd>Cmd + s</kbd> for Mac) 保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="02847-115">Use the key combination <kbd>Ctrl+S</kbd> (<kbd>Cmd+S</kbd> for Mac) to save your changes.</span></span> <span data-ttu-id="02847-116">在收到提示`Dockerfile`时对文件命名。</span><span class="sxs-lookup"><span data-stu-id="02847-116">Name the file `Dockerfile` when prompted.</span></span>

    <span data-ttu-id="02847-117">此配置将 node.js 应用程序添加到`node:9-alpine`映像中。</span><span class="sxs-lookup"><span data-stu-id="02847-117">This configuration adds a Node.js application to the `node:9-alpine` image.</span></span> <span data-ttu-id="02847-118">然后, 它将容器配置为通过*公开*指令为端口80上的应用程序提供服务。</span><span class="sxs-lookup"><span data-stu-id="02847-118">After that, it configures the container to serve the application on port 80 via the *EXPOSE* instruction.</span></span>

1. <span data-ttu-id="02847-119">运行以下 Azure CLI 命令, 以从 Dockerfile 生成容器映像。</span><span class="sxs-lookup"><span data-stu-id="02847-119">Run the following Azure CLI command to build the container image from the Dockerfile.</span></span> <span data-ttu-id="02847-120">*$ACR _name*是您在前面的单元中定义的用于保存您的容器注册表名称的变量。</span><span class="sxs-lookup"><span data-stu-id="02847-120">*$ACR_NAME* is the variable you defined in the preceding unit to hold your container registry name.</span></span>

    ```azurecli
    az acr build --registry $ACR_NAME --image helloacrtasks:v1 .
    ```

    > [!NOTE]
    > <span data-ttu-id="02847-121">不要忘记上述命令`.`末尾的时间段。</span><span class="sxs-lookup"><span data-stu-id="02847-121">Don't forget the period `.` at the end of the preceding command.</span></span> <span data-ttu-id="02847-122">它表示包含 docker 文件的源目录, 在这种情况下, 在我们的示例中为当前目录。</span><span class="sxs-lookup"><span data-stu-id="02847-122">It represents the source directory containing the docker file, which in our case is the current directory.</span></span> <span data-ttu-id="02847-123">由于未使用--file 参数指定文件的名称, 命令会在当前目录中查找名为 " **Dockerfile** " 的文件。</span><span class="sxs-lookup"><span data-stu-id="02847-123">Since we didn't specify the name of a file with the --file parameter, the command looks for a file called **Dockerfile** in our current directory.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="02847-124">验证图像</span><span class="sxs-lookup"><span data-stu-id="02847-124">Verify the image</span></span>

1. <span data-ttu-id="02847-125">在云命令行管理程序中运行以下命令, 以验证是否已创建映像并将其存储在注册表中。</span><span class="sxs-lookup"><span data-stu-id="02847-125">Run the following command in the Cloud Shell to verify that the image has been created and stored in the registry.</span></span>

    ```azurecli
    az acr repository list --name $ACR_NAME --output table
    ```

    <span data-ttu-id="02847-126">此命令的输出应类似于以下形式:</span><span class="sxs-lookup"><span data-stu-id="02847-126">The output from this command should look similar to the following:</span></span>
    
    ```console
    Result
    -------------
    helloacrtasks
    ```

<span data-ttu-id="02847-127">现`helloacrtasks`已准备好使用该图像。</span><span class="sxs-lookup"><span data-stu-id="02847-127">The `helloacrtasks` image is now ready to be used.</span></span>
