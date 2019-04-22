azure Active Directory (azure AD) 不只是云中的域控制器。 Azure AD 是一个多租户的、基于云的目录和标识管理服务。 它将核心目录服务、应用程序访问管理和标识保护结合到单个解决方案中。 azure ad 可以通过 azure ad Connect 与现有 Windows Server Active Directory 环境协同工作, 这使您可以利用现有的本地标识投资。

Azure AD 有四个版本。 在本练习中, 我们将重点介绍 Azure AD 高级 P1 和 P2 版本中的功能。

在本模块中, 我们将创建一个 Azure AD 目录, 其中所有用户和组都将处于活动状态, 类似于本地目录。

创建目录时, 我们的帐户将自动成为全局管理员。 具有全局管理员权限的帐户应受到管制, 因为它们具有对所有 Azure AD 管理功能的完全访问权限。 您可以拥有多个全局管理员, 但只有全局管理员才能将任何其他管理员角色分配给用户。

## <a name="how-can-azure-ad-help-you-protect-access-to-applications"></a>Azure AD 如何能够帮助你保护对应用程序的访问？

Azure AD Premium 包括多因素身份验证和条件访问策略等功能。 当这些功能一起使用时, 它们在保护对应用程序的访问时提供最多的粒度。

条件访问策略由以下内容组成:

- 用户或组
- 正在尝试访问的应用程序
- 要满足的控件, 例如多重身份验证

在此单元中, 你学习了 Azure AD 的基础知识, 以及可用于保护对应用程序的访问权限的功能。