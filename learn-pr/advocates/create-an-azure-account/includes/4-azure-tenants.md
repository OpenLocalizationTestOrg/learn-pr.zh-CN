如你所见, 你的 azure 帐户是一个全局唯一实体, 可让你访问 Azure 订阅和服务。 使用 azure Active Directory (azure AD) 对你的帐户进行身份验证。 Azure AD 是一种新式标识提供程序, 它支持多个身份验证协议, 以保护云中的应用程序和服务。 

> [!IMPORTANT]
> Azure AD 与__ Windows Active Directory 不同。 windows Active Directory 重点关注 Windows 桌面和服务器的安全。 相比之下, Azure AD 都是关于基于 web 的身份验证标准 (如 OpenID 和 OAuth) 的。

在 Azure AD 中注册的用户、应用程序和其他实体并不都是 lumped 一个全局服务。 而是将 Azure AD 划分为单独的_租户_。 租户是一个专用的、独立的 Azure Active Directory 服务实例, 由组织拥有和管理。 当你注册 microsoft 云服务订阅 (如 microsoft Azure、microsoft Intune 或 Office 365) 时, 将自动为你的组织创建 Azure AD 的专用实例。

当遇到 Azure AD 租户时, 个人、团队、公司或任何其他人员组&mdash;不会拥有 "组织" 租户的具体定义。 租户通常与公司相关联。 如果使用与现有租户不关联的电子邮件地址注册 Azure, 注册过程将引导您完成创建由您完全拥有的租户的过程。

> [!TIP]
> 你用于登录 Azure 的电子邮件地址可与多个租户关联。 如果你有 Azure 帐户, 并且使用 Microsoft 学习的 azure 沙盒来完成练习, 你可能会看到这一点。 在 Azure 门户中, 一次只能查看属于一个租户的资源。 若要切换租户, 请查看门户顶部的 "**书籍和筛选器**" 图标的资源, 并在 "**切换目录**" 部分中选择一个不同的租户。

Azure AD 租户和订阅具有多对一的信任关系: 租户可与多个 Azure 订阅关联, 但每个订阅仅与一个租户关联。 此结构允许组织管理多个订阅并在其包含的所有资源中设置安全规则。

下面是有关帐户、订阅、租户和资源如何协同工作的简单表示。

![显示两个不同的 Azure AD 租户的插图。 一个租户有两个订阅, 每个订阅都链接到一组 Azure 资源。 另一个租户有一个链接到一组不同的 Azure 资源的订阅。](../media/4-azure-ad-tenant.png)

请注意, 每个 Azure AD 租户都有一个_帐户所有者_。 这是负责计费的原始 Azure 帐户。 你可以将其他用户添加到租户, 甚至邀请来自其他 Azure AD 租户的来宾访问订阅中的资源。