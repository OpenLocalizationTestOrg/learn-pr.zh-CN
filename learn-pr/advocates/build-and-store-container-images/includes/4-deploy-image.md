可以使用许多容器管理平台 (如 azure 容器实例、azure Kubernetes Service 和 Windows 或 Mac 的 Docker) 从 Azure 容器注册表中提取容器映像。 在这里, 我们将把映像部署到 Azure 容器实例。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

首先, 在云命令行管理程序中`ACR_NAME`用您的容器注册表名称 (例如, 而不是 "MyContainer" 生成值 "MyContainer") 创建一个变量。 此变量在整个单元中使用。

```azurecli
ACR_NAME=<acrName>
```

## <a name="about-registry-authentication"></a>关于注册表身份验证

Azure 容器注册表不支持未经身份验证的访问;对注册表的所有操作都需要登录。 注册表支持两种类型的标识:

- **Azure Active Directory 标识**, 包括用户和服务主体。 对具有 Azure Active Directory 标识的注册表的访问是基于角色的, 可以为以下三个角色之一分配标识: **reader** (仅限拉取访问)、**参与者**(推送和拉取访问) 或**所有者**(拉取、推送和分配角色)其他用户)。
- 每个注册表中包含的**管理员帐户**。 管理员帐户在默认情况下处于禁用状态。

管理员帐户提供快速选项以尝试新的注册表。 启用帐户并在工作流和需要访问的应用程序中使用其用户名和密码。 确认注册表按照预期方式工作后, 应禁用管理员帐户并以独占方式使用 Azure Active Directory 标识, 以确保注册表的安全性。

> [!IMPORTANT]
> 仅使用注册表管理员帐户进行早期测试和探索, 不要共享用户名和密码。 禁用管理员帐户, 并仅使用 Azure Active Directory 标识的基于角色的访问, 以最大限度地提高注册表的安全性。

## <a name="enable-the-registry-admin-account"></a>启用注册表管理帐户

在本练习中, 我们将启用注册表管理员帐户, 并使用它将图像从命令行部署到 Azure 容器实例。

运行以下命令, 在注册表中启用管理员帐户并检索其用户名和密码。

```azurecli
az acr update -n $ACR_NAME --admin-enabled true
az acr credential show --name $ACR_NAME
```

输出如下所示。 记录的`username`和的值`password`。

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

## <a name="deploy-a-container-with-azure-cli"></a>使用 Azure CLI 部署容器

1. 执行以下`az container create`命令以部署容器实例。 在`<username>`以下`<password>`命令中将和替换为您的注册表的管理员用户名和密码。

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

1. 使用以下命令获取 Azure 容器实例的 IP 地址。

    ```azurecli
    az container show --resource-group  <rgn>[sandbox resource group name]</rgn> --name acr-tasks --query ipAddress.ip --output table
    ```

1. 打开浏览器并导航到容器的 IP 地址。 如果已正确配置所有内容, 您应该会看到以下结果:

![具有文本 Hello World 的示例 web 应用程序](../media/hello.png)