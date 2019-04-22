## <a name="creating-key-vaults-for-your-applications"></a><span data-ttu-id="d60cc-101">为应用程序创建密钥保管库</span><span class="sxs-lookup"><span data-stu-id="d60cc-101">Creating Key Vaults for your applications</span></span>

<span data-ttu-id="d60cc-102">好的做法是为每个应用程序的每个部署环境创建一个单独的电子仓库, 例如开发、测试和生产。</span><span class="sxs-lookup"><span data-stu-id="d60cc-102">Good practice is to create a separate vault for each deployment environment of each of your applications, such as development, test, and production.</span></span> <span data-ttu-id="d60cc-103">可以使用保管库跨多个应用共享机密信息, 但是攻击者获取对电子仓库的读取访问权限会随着保管库中的密码数量的增加而受到影响。</span><span class="sxs-lookup"><span data-stu-id="d60cc-103">It's possible to use vaults to share secrets across multiple apps, but the impact of an attacker gaining read access to a vault increases with the number of secrets in the vault.</span></span>

> [!TIP]
> <span data-ttu-id="d60cc-104">如果在应用程序的不同环境中对机密使用相同的名称, 则应用程序中必须更改的特定于环境的配置是保管库 URL。</span><span class="sxs-lookup"><span data-stu-id="d60cc-104">If you use the same names for secrets across different environments for an application, the only environment-specific configuration that has to change in your app is the vault URL.</span></span>

<span data-ttu-id="d60cc-105">创建电子仓库不需要初始配置。</span><span class="sxs-lookup"><span data-stu-id="d60cc-105">Creating a vault requires no initial configuration.</span></span> <span data-ttu-id="d60cc-106">将自动向你的用户标识授予完整的机密管理权限集, 你可以立即开始添加机密。</span><span class="sxs-lookup"><span data-stu-id="d60cc-106">Your user identity is automatically granted the full set of secret management permissions and you can start adding secrets immediately.</span></span> <span data-ttu-id="d60cc-107">一旦拥有一个保管库, 就可以从任何 azure 管理接口 (包括 azure 门户、azure CLI 和 azure PowerShell) 中添加和管理密码。</span><span class="sxs-lookup"><span data-stu-id="d60cc-107">Once you have a vault, adding and managing secrets can be done from any Azure administrative interface, including the Azure portal, the Azure CLI, and Azure PowerShell.</span></span> <span data-ttu-id="d60cc-108">将应用程序设置为使用保管库时, 需要为其分配正确的权限;我们将在下一个单元中看到。</span><span class="sxs-lookup"><span data-stu-id="d60cc-108">When you set up your application to use the vault, you'll need to assign the correct permissions to it; we'll see that in the next unit.</span></span>

## <a name="vault-authentication-and-permissions"></a><span data-ttu-id="d60cc-109">保管库身份验证和权限</span><span class="sxs-lookup"><span data-stu-id="d60cc-109">Vault authentication and permissions</span></span>

<span data-ttu-id="d60cc-110">azure Key Vault 的 API 使用 azure Active Directory 对用户和应用程序进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="d60cc-110">Azure Key Vault's API uses Azure Active Directory to authenticate users and applications.</span></span> <span data-ttu-id="d60cc-111">保管库访问策略以*操作*为依据, 并跨整个保管库应用。</span><span class="sxs-lookup"><span data-stu-id="d60cc-111">Vault access policies are based on *actions*, and are applied across an entire vault.</span></span> <span data-ttu-id="d60cc-112">例如, 对保管库具有**Get** (读取机密值)、**列表**(所有机密的列表名称) 和**Set** (创建或更新机密值) 权限的应用程序能够创建机密、列出所有机密名称以及获取和设置所有机密该保管库中的值。</span><span class="sxs-lookup"><span data-stu-id="d60cc-112">For example, an application with **Get** (read secret values), **List** (list names of all secrets), and **Set** (create or update secret values) permissions to a vault is able to create secrets, list all secret names, and get and set all secret values in that vault.</span></span>

<span data-ttu-id="d60cc-113">对保管库执行的*所有*操作都需要进行&mdash;身份验证和授权, 无法授予任何类型的匿名访问权限。</span><span class="sxs-lookup"><span data-stu-id="d60cc-113">*All* actions performed on a vault require authentication and authorization &mdash; there is no way to grant any kind of anonymous access.</span></span>

> [!TIP]
> <span data-ttu-id="d60cc-114">授予对开发人员和应用的保管库访问权限时, 仅授予所需的最少权限集。</span><span class="sxs-lookup"><span data-stu-id="d60cc-114">When granting vault access to developers and apps, grant only the minimum set of permissions needed.</span></span> <span data-ttu-id="d60cc-115">权限限制有助于避免由代码错误导致的意外, 并降低被盗用的凭据或恶意代码注入到应用中的影响。</span><span class="sxs-lookup"><span data-stu-id="d60cc-115">Permissions restrictions help avoid accidents caused by code bugs and reduce the impact of stolen credentials or malicious code injected into your app.</span></span>

<span data-ttu-id="d60cc-116">开发人员通常只需要具有对开发环境电子仓库的**Get**和**List**权限。</span><span class="sxs-lookup"><span data-stu-id="d60cc-116">Developers will usually only need **Get** and **List** permissions to a development-environment vault.</span></span> <span data-ttu-id="d60cc-117">潜在客户或高级开发人员需要对保管库的完全访问权限, 以便在必要时更改和添加密码。</span><span class="sxs-lookup"><span data-stu-id="d60cc-117">A lead or senior developer will need full permissions to the vault to change and add secrets when necessary.</span></span> <span data-ttu-id="d60cc-118">对生产环境电子仓库的完全权限通常是为高级操作人员预留的。</span><span class="sxs-lookup"><span data-stu-id="d60cc-118">Full permissions to production-environment vaults are typically reserved for senior operations staff.</span></span>

<span data-ttu-id="d60cc-119">对于应用程序, 通常只需要**获取**权限。</span><span class="sxs-lookup"><span data-stu-id="d60cc-119">For apps, often only **Get** permissions are required.</span></span> <span data-ttu-id="d60cc-120">某些应用可能需要**列表**, 具体取决于应用的实施方式。</span><span class="sxs-lookup"><span data-stu-id="d60cc-120">Some apps may require **List** depending on the way the app is implemented.</span></span> <span data-ttu-id="d60cc-121">本模块的练习中将实现的应用程序需要**List**权限, 因为它使用它从保管库中读取机密信息的方法。</span><span class="sxs-lookup"><span data-stu-id="d60cc-121">The app we'll implement in this module's exercise requires the **List** permission because of the technique it uses to read secrets from the vault.</span></span>

<span data-ttu-id="d60cc-122">鉴于公司遇到应用程序机密的所有问题, 管理人员都要求您创建一个小型初学者应用程序, 以便在右侧路径上设置其他开发人员。</span><span class="sxs-lookup"><span data-stu-id="d60cc-122">Given all the trouble the company's been having with application secrets, management has asked you to create a small starter app to set the other developers on the right path.</span></span> <span data-ttu-id="d60cc-123">应用需要演示尽可能简单和安全地管理机密的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="d60cc-123">The app needs to demonstrate best practices for managing secrets as simply and securely as possible.</span></span>

## <a name="create-the-vault-and-store-the-secret-in-it"></a><span data-ttu-id="d60cc-124">创建保管库并将机密存储在其中</span><span class="sxs-lookup"><span data-stu-id="d60cc-124">Create the vault and store the secret in it</span></span>

<span data-ttu-id="d60cc-125">若要开始, 你将创建一个保管库并存储一个密码。</span><span class="sxs-lookup"><span data-stu-id="d60cc-125">To start, you'll create a vault and store one secret.</span></span>

### <a name="create-the-vault"></a><span data-ttu-id="d60cc-126">创建保管库</span><span class="sxs-lookup"><span data-stu-id="d60cc-126">Create the vault</span></span>

<span data-ttu-id="d60cc-127">首先, 我们将创建电子仓库并将我们的机密存储在其中。</span><span class="sxs-lookup"><span data-stu-id="d60cc-127">First, we'll create the vault and store our secret in it.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="d60cc-128">**密钥保管库名称必须是全局唯一的, 因此需要选取一个唯一的名称**。</span><span class="sxs-lookup"><span data-stu-id="d60cc-128">**Key Vault names must be globally unique, so you'll need to pick a unique name**.</span></span> <span data-ttu-id="d60cc-129">保管库名称的长度必须为3-24 个字符, 并且仅包含字母数字字符和短划线。</span><span class="sxs-lookup"><span data-stu-id="d60cc-129">Vault names must be 3-24 characters long and contain only alphanumeric characters and dashes.</span></span> <span data-ttu-id="d60cc-130">记下你选择的保管库名称, 因为在本练习中你将需要它。</span><span class="sxs-lookup"><span data-stu-id="d60cc-130">Make a note of the vault name you choose, as you'll need it throughout this exercise.</span></span>

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="d60cc-131">在云命令行管理程序中运行以下命令, 以创建您的保管库。</span><span class="sxs-lookup"><span data-stu-id="d60cc-131">Run the following command in the Cloud Shell to create your vault.</span></span>

```azurecli
az keyvault create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-vault-name>
```

<span data-ttu-id="d60cc-132">完成后, 你将看到描述新的保管库的 JSON 输出。</span><span class="sxs-lookup"><span data-stu-id="d60cc-132">When it finishes, you'll see JSON output describing the new vault.</span></span>

> [!TIP]
> <span data-ttu-id="d60cc-133">该命令使用了名为**<rgn>[沙盒资源组]</rgn>** 的预先创建的资源组。</span><span class="sxs-lookup"><span data-stu-id="d60cc-133">The command used the pre-created resource group named **<rgn>[sandbox Resource Group]</rgn>**.</span></span> <span data-ttu-id="d60cc-134">使用自己的订阅时, 需要创建新的资源组, 或使用以前创建的现有资源组。</span><span class="sxs-lookup"><span data-stu-id="d60cc-134">When working with your own subscription, you would want to either create a new resource group, or use an existing one you have previously created.</span></span>

### <a name="add-the-secret"></a><span data-ttu-id="d60cc-135">添加密码</span><span class="sxs-lookup"><span data-stu-id="d60cc-135">Add the secret</span></span>

<span data-ttu-id="d60cc-136">现在, 添加密码: 我们的秘密将被命名为**SecretPassword** , 值为**reindeer_flotilla**。</span><span class="sxs-lookup"><span data-stu-id="d60cc-136">Now add the secret: our secret will be named **SecretPassword** with a value of **reindeer_flotilla**.</span></span>

```azurecli
az keyvault secret set \
    --name SecretPassword \
    --value reindeer_flotilla \
    --vault-name <your-unique-vault-name>
```

<span data-ttu-id="d60cc-137">我们将很快为应用程序编写代码, 但首先我们需要了解有关应用程序如何向保管库进行身份验证的一些信息。</span><span class="sxs-lookup"><span data-stu-id="d60cc-137">We'll write the code for our application shortly, but first we need to learn a little bit about how our app is going to authenticate to a vault.</span></span>