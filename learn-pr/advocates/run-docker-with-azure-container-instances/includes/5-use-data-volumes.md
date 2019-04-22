<span data-ttu-id="31bd4-101">默认情况下, Azure 容器实例是无状态的。</span><span class="sxs-lookup"><span data-stu-id="31bd4-101">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="31bd4-102">如果容器崩溃或停止, 则它的所有状态都将丢失。</span><span class="sxs-lookup"><span data-stu-id="31bd4-102">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="31bd4-103">若要在容器的生存期之外保留状态, 必须从外部存储装入卷。</span><span class="sxs-lookup"><span data-stu-id="31bd4-103">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span>

<span data-ttu-id="31bd4-104">在这里, 你将向 azure 容器实例装载 azure 文件共享, 以便稍后存储数据并对其进行访问。</span><span class="sxs-lookup"><span data-stu-id="31bd4-104">Here, you'll mount an Azure file share to an Azure container instance to you can store data and access it later.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="31bd4-105">创建 Azure 文件共享</span><span class="sxs-lookup"><span data-stu-id="31bd4-105">Create an Azure file share</span></span>

<span data-ttu-id="31bd4-106">在这里, 你将创建一个存储帐户和一个文件共享, 稍后你将对 Azure 容器实例进行访问。</span><span class="sxs-lookup"><span data-stu-id="31bd4-106">Here you'll create a storage account and a file share that you'll later make accessible to an Azure container instance.</span></span>

1. <span data-ttu-id="31bd4-107">您的存储帐户需要一个唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="31bd4-107">Your storage account requires a unique name.</span></span> <span data-ttu-id="31bd4-108">若要了解学习目的, 请运行以下命令, 在 Bash 变量中存储唯一名称。</span><span class="sxs-lookup"><span data-stu-id="31bd4-108">For learning purposes, run the following command to store a unique name in a Bash variable.</span></span>

    ```bash
    STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
    ```

1. <span data-ttu-id="31bd4-109">运行以下`az storage account create`命令以创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="31bd4-109">Run the following `az storage account create` command to create your storage account.</span></span>

    ```azurecli
    az storage account create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $STORAGE_ACCOUNT_NAME \
      --sku Standard_LRS \
      --location eastus
    ```

1. <span data-ttu-id="31bd4-110">运行以下命令, 将存储帐户连接字符串放置在名为`AZURE_STORAGE_CONNECTION_STRING`的环境变量中。</span><span class="sxs-lookup"><span data-stu-id="31bd4-110">Run the following command to place the storage account connection string into an environment variable named `AZURE_STORAGE_CONNECTION_STRING`.</span></span>

    ```azurecli
    export AZURE_STORAGE_CONNECTION_STRING=$(az storage account show-connection-string \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $STORAGE_ACCOUNT_NAME \
      --output tsv)
    ```

    <span data-ttu-id="31bd4-111">`AZURE_STORAGE_CONNECTION_STRING`是 Azure CLI 可理解的特殊环境变量。</span><span class="sxs-lookup"><span data-stu-id="31bd4-111">`AZURE_STORAGE_CONNECTION_STRING` is a special environment variable that's understood by the Azure CLI.</span></span> <span data-ttu-id="31bd4-112">此`export`部分将使此变量可供稍后运行的其他 CLI 命令访问。</span><span class="sxs-lookup"><span data-stu-id="31bd4-112">The `export` part makes this variable accessible to other CLI commands you'll run shortly.</span></span>

1. <span data-ttu-id="31bd4-113">运行此命令以在存储帐户中创建名为**aci-share-demo**的文件共享。</span><span class="sxs-lookup"><span data-stu-id="31bd4-113">Run this command to create a file share, named **aci-share-demo**, in the storage account.</span></span>

    ```azurecli
    az storage share create --name aci-share-demo
    ```

## <a name="get-storage-credentials"></a><span data-ttu-id="31bd4-114">获取存储凭据</span><span class="sxs-lookup"><span data-stu-id="31bd4-114">Get storage credentials</span></span>

<span data-ttu-id="31bd4-115">若要在 azure 容器实例中将 Azure 文件共享安装为卷, 您需要以下三个值:</span><span class="sxs-lookup"><span data-stu-id="31bd4-115">To mount an Azure file share as a volume in Azure Container Instances, you need these three values:</span></span>

* <span data-ttu-id="31bd4-116">存储帐户名称</span><span class="sxs-lookup"><span data-stu-id="31bd4-116">The storage account name</span></span>
* <span data-ttu-id="31bd4-117">共享名称</span><span class="sxs-lookup"><span data-stu-id="31bd4-117">The share name</span></span>
* <span data-ttu-id="31bd4-118">存储帐户访问密钥</span><span class="sxs-lookup"><span data-stu-id="31bd4-118">The storage account access key</span></span>

<span data-ttu-id="31bd4-119">您已具有前两个值。</span><span class="sxs-lookup"><span data-stu-id="31bd4-119">You already have the first two values.</span></span> <span data-ttu-id="31bd4-120">存储帐户名称存储在`STORAGE_ACCOUNT_NAME` Bash 变量中。</span><span class="sxs-lookup"><span data-stu-id="31bd4-120">The storage account name is stored in the `STORAGE_ACCOUNT_NAME` Bash variable.</span></span> <span data-ttu-id="31bd4-121">您在上一步中指定了**aci-share-demo**作为共享名称。</span><span class="sxs-lookup"><span data-stu-id="31bd4-121">You specified **aci-share-demo** as the share name in the previous step.</span></span> <span data-ttu-id="31bd4-122">在这里, 你将获得存储&mdash;帐户访问密钥的剩余值。</span><span class="sxs-lookup"><span data-stu-id="31bd4-122">Here you'll get the remaining value &mdash; the storage account access key.</span></span>

1. <span data-ttu-id="31bd4-123">运行以下命令以获取存储帐户密钥。</span><span class="sxs-lookup"><span data-stu-id="31bd4-123">Run the following command to get the storage account key.</span></span>

    ```azurecli
    STORAGE_KEY=$(az storage account keys list \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --account-name $STORAGE_ACCOUNT_NAME \
      --query "[0].value" \
      --output tsv)
    ```

    <span data-ttu-id="31bd4-124">结果存储在名为`STORAGE_KEY`的 Bash 变量中。</span><span class="sxs-lookup"><span data-stu-id="31bd4-124">The result is stored in a Bash variable named `STORAGE_KEY`.</span></span>

1. <span data-ttu-id="31bd4-125">作为可选步骤, 请将存储密钥打印到控制台。</span><span class="sxs-lookup"><span data-stu-id="31bd4-125">As an optional step, print the storage key to the console.</span></span>

    ```bash
    echo $STORAGE_KEY
    ```

## <a name="deploy-a-container-and-mount-the-file-share"></a><span data-ttu-id="31bd4-126">部署容器并装入文件共享</span><span class="sxs-lookup"><span data-stu-id="31bd4-126">Deploy a container and mount the file share</span></span>

<span data-ttu-id="31bd4-127">若要在容器中将 Azure 文件共享装载为卷, 请在创建容器时指定共享和卷装入点。</span><span class="sxs-lookup"><span data-stu-id="31bd4-127">To mount an Azure file share as a volume in a container, you specify the share and volume mount point when you create the container.</span></span>

1. <span data-ttu-id="31bd4-128">运行此`az container create`命令可创建一个装载`/aci/logs/`到文件共享的容器。</span><span class="sxs-lookup"><span data-stu-id="31bd4-128">Run this `az container create` command to create a container that mounts `/aci/logs/` to your file share.</span></span>

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

1. <span data-ttu-id="31bd4-129">运行`az container show`以获取容器的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="31bd4-129">Run `az container show` to get your container's public IP address.</span></span>

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-files \
      --query ipAddress.ip \
      --output tsv
    ```

1. <span data-ttu-id="31bd4-130">在浏览器中, 导航到容器的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="31bd4-130">From a browser, navigate to your container's IP address.</span></span> <span data-ttu-id="31bd4-131">你会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="31bd4-131">You see this.</span></span>

    ![Azure 容器实例文件共享演示](../media/5-files-ui.png)

1. <span data-ttu-id="31bd4-133">在表单中输入一些文本, 然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="31bd4-133">Enter some text into the form and click **Submit**.</span></span> <span data-ttu-id="31bd4-134">此操作将创建一个文件, 其中包含您在 Azure 文件共享中输入的文本。</span><span class="sxs-lookup"><span data-stu-id="31bd4-134">This action creates a file that contains the text you entered in the Azure file share.</span></span>

1. <span data-ttu-id="31bd4-135">运行此`az storage file list`命令可显示文件共享中包含的文件。</span><span class="sxs-lookup"><span data-stu-id="31bd4-135">Run this `az storage file list` command to display the files that are contained in your file share.</span></span>

    ```azurecli
    az storage file list -s aci-share-demo -o table
    ```

1. <span data-ttu-id="31bd4-136">运行`az storage file download`以将文件下载到你的云命令行管理程序会话。</span><span class="sxs-lookup"><span data-stu-id="31bd4-136">Run `az storage file download` to download a file to your Cloud Shell session.</span></span> <span data-ttu-id="31bd4-137">将\*\* \<filename\> \*\*替换为在上一步中显示的某个文件。</span><span class="sxs-lookup"><span data-stu-id="31bd4-137">Replace **\<filename\>** with one of the files that appeared in the previous step.</span></span>

    ```azurecli
    az storage file download -s aci-share-demo -p <filename>
    ```

1. <span data-ttu-id="31bd4-138">运行`cat`命令以打印文件的内容。</span><span class="sxs-lookup"><span data-stu-id="31bd4-138">Run the `cat` command to print the contents of the file.</span></span>

    ```azurecli
    cat <filename>
    ```

<span data-ttu-id="31bd4-139">请记住, 当容器退出时, 数据仍然存在。</span><span class="sxs-lookup"><span data-stu-id="31bd4-139">Remember that your data persists when your container exits.</span></span> <span data-ttu-id="31bd4-140">您可以将文件共享安装到其他容器实例, 以使其可供其使用。</span><span class="sxs-lookup"><span data-stu-id="31bd4-140">You can mount your file share to other container instances to make that data available to them.</span></span>
