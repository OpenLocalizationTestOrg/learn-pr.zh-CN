<span data-ttu-id="53f1c-101">可以使用许多容器管理平台 (如 azure 容器实例、azure Kubernetes Service 和 Windows 或 Mac 的 Docker) 从 Azure 容器注册表中提取容器映像。</span><span class="sxs-lookup"><span data-stu-id="53f1c-101">Container images can be pulled from Azure Container Registry using many container management platforms, such as Azure Container Instances, Azure Kubernetes Service, and Docker for Windows or Mac.</span></span> <span data-ttu-id="53f1c-102">在这里, 我们将把映像部署到 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="53f1c-102">Here, we will deploy our image to an Azure Container Instance.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="53f1c-103">首先, 在云命令行管理程序中`ACR_NAME`用您的容器注册表名称 (例如, 而不是 "MyContainer" 生成值 "MyContainer") 创建一个变量。</span><span class="sxs-lookup"><span data-stu-id="53f1c-103">First, create a variable in the Cloud Shell named `ACR_NAME` with the name of your container registry in lowercase (for example, instead of "MyContainer" make the value "mycontainer").</span></span> <span data-ttu-id="53f1c-104">此变量在整个单元中使用。</span><span class="sxs-lookup"><span data-stu-id="53f1c-104">This variable is used throughout this unit.</span></span>

```azurecli
ACR_NAME=<acrName>
```

## <a name="about-registry-authentication"></a><span data-ttu-id="53f1c-105">关于注册表身份验证</span><span class="sxs-lookup"><span data-stu-id="53f1c-105">About registry authentication</span></span>

<span data-ttu-id="53f1c-106">Azure 容器注册表不支持未经身份验证的访问;对注册表的所有操作都需要登录。</span><span class="sxs-lookup"><span data-stu-id="53f1c-106">Azure Container Registry does not support unauthenticated access; all operations on a registry require a login.</span></span> <span data-ttu-id="53f1c-107">注册表支持两种类型的标识:</span><span class="sxs-lookup"><span data-stu-id="53f1c-107">Registries support two types of identities:</span></span>

- <span data-ttu-id="53f1c-108">**Azure Active Directory 标识**, 包括用户和服务主体。</span><span class="sxs-lookup"><span data-stu-id="53f1c-108">**Azure Active Directory identities**, including both user and service principals.</span></span> <span data-ttu-id="53f1c-109">对具有 Azure Active Directory 标识的注册表的访问是基于角色的, 可以为以下三个角色之一分配标识: **reader** (仅限拉取访问)、**参与者**(推送和拉取访问) 或**所有者**(拉取、推送和分配角色)其他用户)。</span><span class="sxs-lookup"><span data-stu-id="53f1c-109">Access to a registry with an Azure Active Directory identity is role-based, and identities can be assigned one of three roles: **reader** (pull access only), **contributor** (push and pull access), or **owner** (pull, push, and assign roles to other users).</span></span>
- <span data-ttu-id="53f1c-110">每个注册表中包含的**管理员帐户**。</span><span class="sxs-lookup"><span data-stu-id="53f1c-110">The **admin account** included with each registry.</span></span> <span data-ttu-id="53f1c-111">管理员帐户在默认情况下处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="53f1c-111">The admin account is disabled by default.</span></span>

<span data-ttu-id="53f1c-112">管理员帐户提供快速选项以尝试新的注册表。</span><span class="sxs-lookup"><span data-stu-id="53f1c-112">The admin account provides a quick option to try a new registry.</span></span> <span data-ttu-id="53f1c-113">启用帐户并在工作流和需要访问的应用程序中使用其用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="53f1c-113">You enable the account and use its username and password in workflows and apps that need access.</span></span> <span data-ttu-id="53f1c-114">确认注册表按照预期方式工作后, 应禁用管理员帐户并以独占方式使用 Azure Active Directory 标识, 以确保注册表的安全性。</span><span class="sxs-lookup"><span data-stu-id="53f1c-114">Once you have confirmed that the registry works as expected, you should disable the admin account and use Azure Active Directory identities exclusively to ensure the security of your registry.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53f1c-115">仅使用注册表管理员帐户进行早期测试和探索, 不要共享用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="53f1c-115">Only use the registry admin account for early testing and exploration, and do not share the username and password.</span></span> <span data-ttu-id="53f1c-116">禁用管理员帐户, 并仅使用 Azure Active Directory 标识的基于角色的访问, 以最大限度地提高注册表的安全性。</span><span class="sxs-lookup"><span data-stu-id="53f1c-116">Disable the admin account and use only role-based access with Azure Active Directory identities to maximize the security of your registry.</span></span>

## <a name="enable-the-registry-admin-account"></a><span data-ttu-id="53f1c-117">启用注册表管理帐户</span><span class="sxs-lookup"><span data-stu-id="53f1c-117">Enable the registry admin account</span></span>

<span data-ttu-id="53f1c-118">在本练习中, 我们将启用注册表管理员帐户, 并使用它将图像从命令行部署到 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="53f1c-118">In this exercise, we will enable the registry admin account and use it to deploy your image to an Azure Container Instance from the command line.</span></span>

<span data-ttu-id="53f1c-119">运行以下命令, 在注册表中启用管理员帐户并检索其用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="53f1c-119">Run the following commands to enable the admin account on your registry and retrieve its username and password.</span></span>

```azurecli
az acr update -n $ACR_NAME --admin-enabled true
az acr credential show --name $ACR_NAME
```

<span data-ttu-id="53f1c-120">输出如下所示。</span><span class="sxs-lookup"><span data-stu-id="53f1c-120">The output is similar to below.</span></span> <span data-ttu-id="53f1c-121">记录的`username`和的值`password`。</span><span class="sxs-lookup"><span data-stu-id="53f1c-121">Take note of the `username` and the value for `password`.</span></span>

```output
{  
  "passwords": [
    {
      "name": "password",
      "value": "aaaaa"
    },
    {
      "name": "password2",
      "value": "bbbbb"
    }
  ],
  "username": "ccccc"
}
```

## <a name="deploy-a-container-with-azure-cli"></a><span data-ttu-id="53f1c-122">使用 Azure CLI 部署容器</span><span class="sxs-lookup"><span data-stu-id="53f1c-122">Deploy a container with Azure CLI</span></span>

1. <span data-ttu-id="53f1c-123">执行以下`az container create`命令以部署容器实例。</span><span class="sxs-lookup"><span data-stu-id="53f1c-123">Execute the following `az container create` command to deploy a container instance.</span></span> <span data-ttu-id="53f1c-124">在`<username>`以下`<password>`命令中将和替换为您的注册表的管理员用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="53f1c-124">Replace `<username>` and `<password>` in the following command with your registry's admin username and password.</span></span>

    ```azurecli
    az container create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name acr-tasks \
        --image $ACR_NAME.azurecr.io/helloacrtasks:v1 \
        --registry-login-server $ACR_NAME.azurecr.io \
        --ip-address Public \
        --location eastus \
        --registry-username <username> \
        --registry-password <password>
    ```

1. <span data-ttu-id="53f1c-125">使用以下命令获取 Azure 容器实例的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="53f1c-125">Get the IP address of the Azure container instance using the following command.</span></span>

    ```azurecli
    az container show --resource-group  <rgn>[sandbox resource group name]</rgn> --name acr-tasks --query ipAddress.ip --output table
    ```

1. <span data-ttu-id="53f1c-126">打开浏览器并导航到容器的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="53f1c-126">Open a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="53f1c-127">如果已正确配置所有内容, 您应该会看到以下结果:</span><span class="sxs-lookup"><span data-stu-id="53f1c-127">If everything has been configured correctly, you should see the following results:</span></span>

![具有文本 Hello World 的示例 web 应用程序](../media/hello.png)