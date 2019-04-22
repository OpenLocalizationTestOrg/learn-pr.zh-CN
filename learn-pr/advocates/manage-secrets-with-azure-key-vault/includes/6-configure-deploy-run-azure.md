现在是时候在 Azure 中运行应用程序了。 我们需要创建 Azure 应用服务应用程序, 将其设置为托管标识和电子仓库配置, 并部署我们的代码。

## <a name="create-the-app-service-plan-and-app"></a>创建应用服务计划和应用

创建应用服务应用程序的过程分为两个步骤: 首先创建*计划*, 然后再创建*应用程序*。

*计划*名称只需要在订阅中是唯一的, 因此您可以使用我们使用的相同名称: **keyvault-plan**。 应用程序名称必须是全局唯一的, 因此需要选择自己的名称。 使用在创建保管库时使用的相同位置。

在 Azure 云命令行管理程序中, 运行以下命令来创建应用服务计划:

```azurecli
az appservice plan create \
    --name keyvault-exercise-plan \
    --resource-group <rgn>[sandbox resource group name]</rgn>
```

接下来, 运行以下命令以创建使用刚创建的 App Service 计划的 Web 应用程序:

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

## <a name="add-configuration-to-the-app"></a>向应用程序添加配置

::: zone pivot="csharp"

若要部署到 Azure, 我们将按照应用服务最佳实践, 将 VaultName 配置放在应用程序设置中, 而不是配置文件中。 运行以下命令以创建应用程序设置:

```azurecli
az webapp config appsettings set \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name> \
    --settings 'VaultName=<your-unique-vault-name>'
```

::: zone-end

::: zone pivot="javascript"

若要部署到 Azure, 我们将按照应用服务最佳实践, 将 VaultName 配置放在应用程序设置中, 而不是配置文件中。 我们还`SCM_DO_BUILD_DURING_DEPLOYMENT`将设置为`true` , 以便应用服务在服务器上还原应用程序包并创建运行应用程序所需的配置。 运行以下命令以创建应用程序设置:

```azurecli
az webapp config appsettings set \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name> \
    --settings 'VaultName=<your-unique-vault-name>' 'SCM_DO_BUILD_DURING_DEPLOYMENT=true'
```

::: zone-end

## <a name="enable-managed-identity"></a>启用托管标识

在应用程序上启用托管标识是一个单命令&mdash;运行此操作, 以便在您的应用程序上启用它:

```azurecli
az webapp identity assign \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

从结果的 JSON 输出中复制**principalId**值。 PrincipalId 是 Azure Active Directory 中的应用程序新标识的唯一 ID, 我们将在下一步中使用它。

## <a name="grant-access-to-the-vault"></a>授予对保管库的访问权限

部署之前的最后一步是将密钥保管库权限分配给应用程序的托管标识。 在下面的命令中, 使用从上一步中复制的**principalId**值作为**对象 id**的值。 运行此命令将授予**Get**和**List**访问权限:

```azurecli
az keyvault set-policy \
    --secret-permissions get list \
    --name <your-unique-vault-name> \
    --object-id <your-managed-identity-principleid>
```

## <a name="deploy-the-app-and-try-it-out"></a>部署应用程序并试用

::: zone pivot="csharp"

已设置你的所有配置, 你已准备好部署! 下面的命令将网站发布到`pub`文件夹, 将其压缩到`site.zip`, 并将 zip 部署到 App Service。

> [!NOTE]
> 如果你还不`cd`在那里, 你将需要返回到 KeyVaultDemoApp 目录。

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

已设置你的所有配置, 你已准备好部署! 下面的命令会将应用程序压缩到`site.zip`应用服务中并将其部署到应用服务中。 我们从`node_modules` zip 中排除, 因为应用服务将在我们部署时自动还原它们。

> [!NOTE]
> 如果你还不`cd`在那里, 你将需要返回到 KeyVaultDemoApp 目录。

```azurecli
zip site.zip * -x node_modules/

az webapp deployment source config-zip \
    --src site.zip \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name <your-unique-app-name>
```

::: zone-end

部署可能需要一分钟或两分钟才能完成。 获得指示网站已部署的结果后, 在浏览器中`https://<your-unique-app-name>.azurewebsites.net/api/SecretTest`打开。 应用程序将在服务器上首次启动, 但在此之后, 您应该会看到机密值**reindeer_flotilla**。

您的应用程序已完成并部署!