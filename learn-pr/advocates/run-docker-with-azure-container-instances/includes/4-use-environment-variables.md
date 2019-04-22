<span data-ttu-id="b1ffb-101">使用环境变量可以动态配置容器运行的应用程序或脚本。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-101">Environment variables enable you to dynamically configure the application or script the container runs.</span></span> <span data-ttu-id="b1ffb-102">您可以使用 azure CLI、PowerShell 或 azure 门户在创建容器时设置变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-102">You can use the Azure CLI, PowerShell, or the Azure portal to set variables when you create the container.</span></span> <span data-ttu-id="b1ffb-103">使用受保护的环境变量, 可以防止敏感信息在容器的输出中显示。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-103">Secured environment variables enable you to prevent sensitive information from displaying in the container's output.</span></span>

<span data-ttu-id="b1ffb-104">在这里, 你将创建一个 azure Cosmos DB 实例, 并使用环境变量将连接信息传递给 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-104">Here, you'll create an Azure Cosmos DB instance and use environment variables to pass the connection information to an Azure container instance.</span></span> <span data-ttu-id="b1ffb-105">容器中的应用程序使用变量来写入和读取 Cosmos DB 中的数据。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-105">An application in the container uses the variables to write and read data from Cosmos DB.</span></span> <span data-ttu-id="b1ffb-106">您将创建环境变量和安全环境变量, 以便您可以看到它们之间的差异。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-106">You will create both an environment variable and a secured environment variable so you can see the difference between them.</span></span>

## <a name="deploy-azure-cosmos-db"></a><span data-ttu-id="b1ffb-107">部署 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b1ffb-107">Deploy Azure Cosmos DB</span></span>

1. <span data-ttu-id="b1ffb-108">当您部署 Azure Cosmos DB 时, 请提供一个唯一的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-108">When you deploy Azure Cosmos DB, you provide a unique database name.</span></span> <span data-ttu-id="b1ffb-109">若要了解学习目的, 请从云命令行管理程序中运行此命令, 以创建保存唯一名称的 Bash 变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-109">For learning purposes, run this command from Cloud Shell to create a Bash variable that holds a unique name.</span></span>

    ```bash
    COSMOS_DB_NAME=aci-cosmos-db-$RANDOM
    ```

1. <span data-ttu-id="b1ffb-110">运行此`az cosmosdb create`命令以创建你的 Azure Cosmos DB 实例。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-110">Run this `az cosmosdb create` command to create your Azure Cosmos DB instance.</span></span>

    ```azurecli
    COSMOS_DB_ENDPOINT=$(az cosmosdb create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $COSMOS_DB_NAME \
      --query documentEndpoint \
      --output tsv)
    ```

    <span data-ttu-id="b1ffb-111">此命令可能需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-111">This command can take a few minutes to complete.</span></span>

    <span data-ttu-id="b1ffb-112">`$COSMOS_DB_NAME`指定唯一的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-112">`$COSMOS_DB_NAME` specifies your unique database name.</span></span> <span data-ttu-id="b1ffb-113">该命令将打印您的数据库的终结点地址。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-113">The command prints the endpoint address for your database.</span></span> <span data-ttu-id="b1ffb-114">此命令会将此地址保存到 Bash 变量`COSMOS_DB_ENDPOINT`中。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-114">Here, the command saves this address to the Bash variable `COSMOS_DB_ENDPOINT`.</span></span>

1. <span data-ttu-id="b1ffb-115">运行`az cosmosdb list-keys`以获取 Azure Cosmos DB 连接密钥, 并将其存储在名为`COSMOS_DB_MASTERKEY`的 Bash 变量中。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-115">Run `az cosmosdb list-keys` to get the Azure Cosmos DB connection key and store it in a Bash variable named `COSMOS_DB_MASTERKEY`.</span></span>

    ```azurecli
    COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name $COSMOS_DB_NAME \
      --query primaryMasterKey \
      --output tsv)
    ```

## <a name="deploy-a-container-that-works-with-your-database"></a><span data-ttu-id="b1ffb-116">部署与您的数据库配合使用的容器</span><span class="sxs-lookup"><span data-stu-id="b1ffb-116">Deploy a container that works with your database</span></span>

<span data-ttu-id="b1ffb-117">在这里, 你将创建可在 azure Cosmos DB 实例中读取和写入记录的 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-117">Here you'll create an Azure container instance that can read from and write records to your Azure Cosmos DB instance.</span></span>

<span data-ttu-id="b1ffb-118">您在上一部分中创建的两个环境`COSMOS_DB_ENDPOINT`变量`COSMOS_DB_MASTERKEY`, 并保留连接到 Azure Cosmos DB 实例所需的值。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-118">The two environment variables you created in the last part, `COSMOS_DB_ENDPOINT` and `COSMOS_DB_MASTERKEY`, hold the values you need to connect to the Azure Cosmos DB instance.</span></span>

1. <span data-ttu-id="b1ffb-119">运行以下`az container create`命令以创建容器。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-119">Run the following `az container create` command to create the container.</span></span>

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo \
      --image microsoft/azure-vote-front:cosmosdb \
      --ip-address Public \
      --location eastus \
      --environment-variables \
        COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
        COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
    ```

    <span data-ttu-id="b1ffb-120">**microsoft/azure-投票-前面: cosmosdb**是指运行虚拟投票应用程序的 Docker 图像。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-120">**microsoft/azure-vote-front:cosmosdb** refers to a Docker image that runs a fictitious voting app.</span></span>

    <span data-ttu-id="b1ffb-121">记下`--environment-variables`该参数。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-121">Note the `--environment-variables` argument.</span></span> <span data-ttu-id="b1ffb-122">此参数指定在容器启动时传递给容器的环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-122">This argument specifies environment variables that are passed to the container when the container starts.</span></span> <span data-ttu-id="b1ffb-123">容器图像配置为查找这些环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-123">The container image is configured to look for these environment variables.</span></span> <span data-ttu-id="b1ffb-124">在这里, 将传递 Azure Cosmos DB 终结点及其连接密钥的名称。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-124">Here, you pass the name of the Azure Cosmos DB endpoint and its connection key.</span></span>

1. <span data-ttu-id="b1ffb-125">运行`az container show`以获取容器的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-125">Run `az container show` to get your container's public IP address.</span></span>

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo \
      --query ipAddress.ip \
      --output tsv
    ```

1. <span data-ttu-id="b1ffb-126">在浏览器中, 导航到容器的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-126">From a browser, navigate to your container's IP address.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b1ffb-127">有时, 容器需要一分钟或两分钟才能完全启动并能够接收连接。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-127">Sometimes containers take a minute or two to fully start up and be able to receive connections.</span></span> <span data-ttu-id="b1ffb-128">如果在浏览器中导航到 IP 地址时没有响应, 请稍等片刻, 然后刷新页面。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-128">If there's no response when you navigate to the IP address in your browser, wait a few moments and refresh the page.</span></span>

    <span data-ttu-id="b1ffb-129">在应用程序可用后, 您会看到此情况。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-129">Once the app is available, you see this.</span></span>

    ![具有两种选择、猫或狗的 Azure 投票应用程序。](../media/4-azure-vote.png)

    <span data-ttu-id="b1ffb-131">尝试为猫或狗转换投票。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-131">Try casting a vote for cats or dogs.</span></span> <span data-ttu-id="b1ffb-132">每个投票存储在 Azure Cosmos DB 实例中。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-132">Each vote is stored in your Azure Cosmos DB instance.</span></span>

## <a name="use-secured-environment-variables-to-hide-connection-information"></a><span data-ttu-id="b1ffb-133">使用安全环境变量隐藏连接信息</span><span class="sxs-lookup"><span data-stu-id="b1ffb-133">Use secured environment variables to hide connection information</span></span>

<span data-ttu-id="b1ffb-134">在前面的部分中, 您使用了两个环境变量来创建容器。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-134">In the previous part, you used two environment variables to create your container.</span></span> <span data-ttu-id="b1ffb-135">默认情况下, 可以通过 Azure 门户和纯文本形式的命令行工具访问这些环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-135">By default, these environment variables are accessible through the Azure portal and command-line tools in plain text.</span></span>

<span data-ttu-id="b1ffb-136">在此部分中, 你将了解如何防止敏感信息 (如连接密钥) 以纯文本格式显示。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-136">In this part, you'll learn how to prevent sensitive information, such as connection keys, from being displayed in plain text.</span></span>

1. <span data-ttu-id="b1ffb-137">让我们先查看操作中的当前行为。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-137">Let's start by seeing the current behavior in action.</span></span> <span data-ttu-id="b1ffb-138">运行以下`az container show`命令以显示容器的环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-138">Run the following `az container show` command to display your container's environment variables.</span></span>

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo \
      --query containers[0].environmentVariables
    ```

    <span data-ttu-id="b1ffb-139">您会发现这两个值都显示为纯文本。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-139">You see that both values appear in plain text.</span></span> <span data-ttu-id="b1ffb-140">下面是一个示例。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-140">Here's an example.</span></span>

    ```json
    [
      {
        "name": "COSMOS_DB_ENDPOINT",
        "secureValue": null,
        "value": "https://aci-cosmos.documents.azure.com:443/"
      },
      {
        "name": "COSMOS_DB_MASTERKEY",
        "secureValue": null,
        "value": "Xm5BwdLlCllBvrR26V00000000S2uOusuglhzwkE7dOPMBQ3oA30n3rKd8PKA13700000000095ynys863Ghgw=="
      }
    ]
    ```

    <span data-ttu-id="b1ffb-141">虽然这些值不会通过投票应用程序显示给用户, 但为了确保敏感信息 (如连接密钥) 不以纯文本格式存储, 这是一种很好的安全做法。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-141">Although these values don't appear to your users through the voting application, it's a good security practice to ensure that sensitive information, such as connection keys, are not stored in plain text.</span></span>

    <span data-ttu-id="b1ffb-142">安全环境变量阻止清除文本输出。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-142">Secure environment variables prevent clear text output.</span></span> <span data-ttu-id="b1ffb-143">若要使用安全环境变量, 请使用`--secure-environment-variables`参数而不是`--environment-variables`参数。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-143">To use secure environment variables, you use the `--secure-environment-variables` argument instead of the `--environment-variables` argument.</span></span>

1. <span data-ttu-id="b1ffb-144">运行以下命令以创建一个名为**aci-secure**的第二个容器, 该容器使用安全环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-144">Run the following command to create a second container, named **aci-demo-secure**, that makes use of secured environment variables.</span></span>

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-secure \
      --image microsoft/azure-vote-front:cosmosdb \
      --ip-address Public \
      --location eastus \
      --secure-environment-variables \
        COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
        COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
    ```

    <span data-ttu-id="b1ffb-145">请注意`--secure-environment-variables`参数的用法。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-145">Note the use of the `--secure-environment-variables` argument.</span></span>

1. <span data-ttu-id="b1ffb-146">运行以下`az container show`命令以显示容器的环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-146">Run the following `az container show` command to display your container's environment variables.</span></span>

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name aci-demo-secure \
      --query containers[0].environmentVariables
    ```

    <span data-ttu-id="b1ffb-147">此时, 您会看到您的环境变量不以纯文本格式显示。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-147">This time, you see that your environment variables do not appear in plain text.</span></span>

    ```json
    [
      {
        "name": "COSMOS_DB_ENDPOINT",
        "secureValue": null,
        "value": null
      },
      {
        "name": "COSMOS_DB_MASTERKEY",
        "secureValue": null,
        "value": null
      }
    ]
    ```

    <span data-ttu-id="b1ffb-148">事实上, 环境变量的值根本不会出现。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-148">In fact, the values of your environment variables do not appear at all.</span></span> <span data-ttu-id="b1ffb-149">这是正常的, 因为这些值指的是敏感信息。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-149">That's OK because these values refer to sensitive information.</span></span> <span data-ttu-id="b1ffb-150">在这里, 您只需知道环境变量存在。</span><span class="sxs-lookup"><span data-stu-id="b1ffb-150">Here, all you need to know is that the environment variables exist.</span></span>
