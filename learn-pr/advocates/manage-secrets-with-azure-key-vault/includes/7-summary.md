在此模块中, 你保护了 Azure Key Vault 中的应用程序机密配置。 我们的应用程序代码使用托管标识对保管库进行身份验证, 并自动将密码从保管库加载到内存中启动时。

[!include[](../../../includes/azure-sandbox-cleanup.md)]

若要清理云命令行管理程序存储`KeyVaultDemoApp` , 请删除该目录。

## <a name="next-steps"></a>后续步骤

如果这是真正的应用程序, 接下来该怎么办？

- 将您的所有应用程序机密放入您的保管库! 在配置文件中, 不再有任何理由要这样做。
- 继续开发应用程序。 你的生产环境全部已设置, 因此, 在将来对其进行部署时, 无需重复所有设置。
- 若要支持开发, 请创建一个包含相同名称但值不同的机密的开发环境电子仓库。 向开发团队授予权限, 并在应用程序的开发环境配置文件中配置保管库名称。 配置取决于您的实现: 对于 ASP.NET Core `AddAzureKeyVault` , 将自动检测 Visual Studio 和 Azure CLI 的本地安装, 并使用在这些应用程序中配置的 azure 凭据登录并访问保管库。 对于 node.js, 可以创建具有对保管库的权限的开发环境服务主体, 并使用`loginWithServicePrincipalSecret`应用程序进行身份验证。
- 出于用户验收测试的目的, 创建其他环境。
- 将独立的电子仓库分布在不同的订阅和/或资源组中, 以将它们隔离。
- 向相应的人员授予对其他环境保管库的访问权限。

## <a name="further-reading"></a>进一步阅读

- [密钥存储库文档](https://docs.microsoft.com/azure/key-vault/)
- [有关 AddAzureKeyVault 及其高级选项的详细信息](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)
- [本教程](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application)将指导您`KeyVaultClient`如何使用, 包括使用客户端密钥 (而不是使用托管标识) 手动向 Azure Active Directory 进行身份验证。
- [Azure resources token service 文档的托管标识](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol), 用于自己实施身份验证工作流。