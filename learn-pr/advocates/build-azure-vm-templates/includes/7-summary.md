在此模块中, 定义了 Azure 资源管理器的含义以及资源管理器模板中的内容。

资源管理器模板是_声明性_的, 这__ 意味着您可以定义所需的资源, 并让资源管理器处理部署详细信息。

您使用现有的 Azure 快速入门模板来部署 VM。 快速入门模板是快速启动部署的绝佳方式。 它们还演示了您在创作自己的模板时可以学习的建议做法。

此外, 还扩展了快速入门模板以在 VM 上配置 web 服务器软件。 扩展现有模板是快速运行和了解这些组件如何组合在一起的一种极好的方法。

资源管理器模板也是可_组合_的。 在构建部署时, 可以编写较小的模板, 每个模板都可以定义系统的一部分, 然后将它们组合在一起, 以创建一个完整的系统。

考虑你在金融服务公司支持的分析师。 在构建资源管理器模板库时, 您将能够更快地为每个分析者组合部署。 在每个财务模型完成后, 只需运行一个 Azure CLI 命令即可销毁部署。

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="learn-more"></a>了解更多信息

要了解的一种很好的方法是这样做。 尝试编写可自动执行其中一个部署的资源管理器模板。

请参阅[Azure 文档中的资源管理器](https://docs.microsoft.com/azure/azure-resource-manager?azure-portal=true), 了解有关如何创建、部署、管理、审核和疑难解答模板的详细信息。

下面是一些资源, 这些资源更详细地介绍了本模块中所学的内容。

* [Azure 快速入门模板](https://azure.microsoft.com/resources/templates?azure-portal=true)
* [Azure 资源管理器可视化工具](http://armviz.io?azure-portal=true)
* [部署简单的 Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows?azure-portal=true)
* [部署简单的 Ubuntu Linux 虚拟机](https://azure.microsoft.com/resources/templates/101-vm-simple-linux?azure-portal=true)

以下是我们在此处未讨论的一些主题, 但你可能会对你浏览和构建自己的模板感兴趣。

* [使用 RBAC 和 Azure 资源管理器模板管理访问权限](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-template?azure-portal=true)
* [在 Azure 资源管理器模板中使用条件](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-tutorial-use-conditions?azure-portal=true)
* [在资源管理器模板部署中集成 Azure 密钥存储库](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-tutorial-use-key-vault?azure-portal=true)
* [创建链接的 Azure 资源管理器模板](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-tutorial-create-linked-templates?azure-portal=true)
* [使用 Azure 资源管理器模板的最佳实践](https://blogs.msdn.microsoft.com/mvpawardprogram/2018/05/01/azure-resource-manager?azure-portal=true)
* [使用 azure 资源管理器解决常见的 azure 部署错误](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-common-deployment-errors?azure-portal=true)

