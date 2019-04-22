<span data-ttu-id="3a7d6-101">现在是时候在 Azure 中运行应用程序了。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="3a7d6-102">我们需要创建 Azure 应用服务应用程序, 将其设置为托管标识和电子仓库配置, 并部署我们的代码。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-102">We need to create an Azure App Service app, set it up with a managed identity and our vault configuration, and deploy our code.</span></span>

## <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="3a7d6-103">创建应用服务计划和应用</span><span class="sxs-lookup"><span data-stu-id="3a7d6-103">Create the App Service plan and app</span></span>

<span data-ttu-id="3a7d6-104">创建应用服务应用程序的过程分为两个步骤: 首先创建*计划*, 然后再创建*应用程序*。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-104">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="3a7d6-105">*计划*名称只需要在订阅中是唯一的, 因此您可以使用我们使用的相同名称: **keyvault-plan**。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-105">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="3a7d6-106">应用程序名称必须是全局唯一的, 因此需要选择自己的名称。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-106">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span> <span data-ttu-id="3a7d6-107">使用在创建保管库时使用的相同位置。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-107">Use the same location you used when creating the vault.</span></span>

<span data-ttu-id="3a7d6-108">在 Azure 云命令行管理程序中, 运行以下命令来创建应用服务计划:</span><span class="sxs-lookup"><span data-stu-id="3a7d6-108">In Azure Cloud Shell, run the following to create an App Service plan:</span></span>

```azurecli
az appservice plan create \
    --name keyvault-exercise-plan \
    --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="3a7d6-109">接下来, 运行以下命令以创建使用刚创建的 App Service 计划的 Web 应用程序:</span><span class="sxs-lookup"><span data-stu-id="3a7d6-109">Next, run the following command to create the Web App that uses the App Service plan you just created:</span></span>

::: zone pivot="csharp"

```azurecli
az webapp create \
    --plan keyvault-exercise-plan \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

::: zone-end

::: zone pivot="javascript"

```azurecli
az webapp create \
    --plan keyvault-exercise-plan \
    --runtime "node|10.6" \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

::: zone-end

## <a name="add-configuration-to-the-app"></a><span data-ttu-id="3a7d6-110">向应用程序添加配置</span><span class="sxs-lookup"><span data-stu-id="3a7d6-110">Add configuration to the app</span></span>

::: zone pivot="csharp"

<span data-ttu-id="3a7d6-111">若要部署到 Azure, 我们将按照应用服务最佳实践, 将 VaultName 配置放在应用程序设置中, 而不是配置文件中。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-111">For deploying to Azure, we'll follow the App Service best practice of putting the VaultName configuration in an application setting instead of a configuration file.</span></span> <span data-ttu-id="3a7d6-112">运行以下命令以创建应用程序设置:</span><span class="sxs-lookup"><span data-stu-id="3a7d6-112">Run this command to create the application setting:</span></span>

```azurecli
az webapp config appsettings set \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name> \
    --settings 'VaultName=<your-unique-vault-name>'
```

::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="3a7d6-113">若要部署到 Azure, 我们将按照应用服务最佳实践, 将 VaultName 配置放在应用程序设置中, 而不是配置文件中。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-113">For deploying to Azure, we'll follow the App Service best practice of putting the VaultName configuration in an application setting instead of a configuration file.</span></span> <span data-ttu-id="3a7d6-114">我们还`SCM_DO_BUILD_DURING_DEPLOYMENT`将设置为`true` , 以便应用服务在服务器上还原应用程序包并创建运行应用程序所需的配置。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-114">We'll also set the `SCM_DO_BUILD_DURING_DEPLOYMENT` setting to `true` so that App Service restores our application's packages on the server and creates the necessary configuration to run the app.</span></span> <span data-ttu-id="3a7d6-115">运行以下命令以创建应用程序设置:</span><span class="sxs-lookup"><span data-stu-id="3a7d6-115">Run this command to create the application settings:</span></span>

```azurecli
az webapp config appsettings set \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name> \
    --settings 'VaultName=<your-unique-vault-name>' 'SCM_DO_BUILD_DURING_DEPLOYMENT=true'
```

::: zone-end

## <a name="enable-managed-identity"></a><span data-ttu-id="3a7d6-116">启用托管标识</span><span class="sxs-lookup"><span data-stu-id="3a7d6-116">Enable managed identity</span></span>

<span data-ttu-id="3a7d6-117">在应用程序上启用托管标识是一个单命令&mdash;运行此操作, 以便在您的应用程序上启用它:</span><span class="sxs-lookup"><span data-stu-id="3a7d6-117">Enabling managed identity on an app is a one-liner &mdash; run this to enable it on your app:</span></span>

```azurecli
az webapp identity assign \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

<span data-ttu-id="3a7d6-118">从结果的 JSON 输出中复制**principalId**值。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-118">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="3a7d6-119">PrincipalId 是 Azure Active Directory 中的应用程序新标识的唯一 ID, 我们将在下一步中使用它。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-119">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

## <a name="grant-access-to-the-vault"></a><span data-ttu-id="3a7d6-120">授予对保管库的访问权限</span><span class="sxs-lookup"><span data-stu-id="3a7d6-120">Grant access to the vault</span></span>

<span data-ttu-id="3a7d6-121">部署之前的最后一步是将密钥保管库权限分配给应用程序的托管标识。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-121">The last step before deploying is to assign Key Vault permissions to your app's managed identity.</span></span> <span data-ttu-id="3a7d6-122">在下面的命令中, 使用从上一步中复制的**principalId**值作为**对象 id**的值。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-122">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span> <span data-ttu-id="3a7d6-123">运行此命令将授予**Get**和**List**访问权限:</span><span class="sxs-lookup"><span data-stu-id="3a7d6-123">Running this command will grant **Get** and **List** access:</span></span>

```azurecli
az keyvault set-policy \
    --secret-permissions get list \
    --name <your-unique-vault-name> \
    --object-id <your-managed-identity-principleid>
```

## <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="3a7d6-124">部署应用程序并试用</span><span class="sxs-lookup"><span data-stu-id="3a7d6-124">Deploy the app and try it out</span></span>

::: zone pivot="csharp"

<span data-ttu-id="3a7d6-125">已设置你的所有配置, 你已准备好部署!</span><span class="sxs-lookup"><span data-stu-id="3a7d6-125">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="3a7d6-126">下面的命令将网站发布到`pub`文件夹, 将其压缩到`site.zip`, 并将 zip 部署到 App Service。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-126">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="3a7d6-127">如果你还不`cd`在那里, 你将需要返回到 KeyVaultDemoApp 目录。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-127">You'll need to `cd` back to the KeyVaultDemoApp directory if you're not still there.</span></span>

```azurecli
dotnet publish -o pub
zip -j site.zip pub/*

az webapp deployment source config-zip \
    --src site.zip \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="3a7d6-128">已设置你的所有配置, 你已准备好部署!</span><span class="sxs-lookup"><span data-stu-id="3a7d6-128">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="3a7d6-129">下面的命令会将应用程序压缩到`site.zip`应用服务中并将其部署到应用服务中。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-129">The below commands will zip up your app into `site.zip` and deploy it to App Service.</span></span> <span data-ttu-id="3a7d6-130">我们从`node_modules` zip 中排除, 因为应用服务将在我们部署时自动还原它们。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-130">We exclude `node_modules` from the zip because App Service will restore them automatically when we deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="3a7d6-131">如果你还不`cd`在那里, 你将需要返回到 KeyVaultDemoApp 目录。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-131">You'll need to `cd` back to the KeyVaultDemoApp directory if you're not still there.</span></span>

```azurecli
zip site.zip * -x node_modules/

az webapp deployment source config-zip \
    --src site.zip \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

::: zone-end

<span data-ttu-id="3a7d6-132">部署可能需要一分钟或两分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-132">The deployment may take a minute or two to complete.</span></span> <span data-ttu-id="3a7d6-133">获得指示网站已部署的结果后, 在浏览器中`https://<your-unique-app-name>.azurewebsites.net/api/SecretTest`打开。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-133">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="3a7d6-134">应用程序将在服务器上首次启动, 但在此之后, 您应该会看到机密值**reindeer_flotilla**。</span><span class="sxs-lookup"><span data-stu-id="3a7d6-134">The app will take a moment to start up for the first time on the server, but once it does, you should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="3a7d6-135">您的应用程序已完成并部署!</span><span class="sxs-lookup"><span data-stu-id="3a7d6-135">Your app is finished and deployed!</span></span>