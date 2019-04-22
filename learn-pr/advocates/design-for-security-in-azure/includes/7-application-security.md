与传统的本地部署相比, 在云平台上托管应用程序可提供多种优势。 云的共享责任模型将安全性移动到物理网络、生成和主机级别下, 在云提供程序的控制之下。 试图在此级别危害平台的攻击者将看到不断发生的返回, 而不是大量的投资和洞察力提供商在保护和监视其基础结构方面做出的努力。

因此, 攻击者可以更有效地实现云平台客户在应用程序级别引入的漏洞。 此外, 通过采用 Platform for Service (PaaS) 托管其应用程序, 客户可以从管理操作系统安全中释放资源, 并将其部署为加强应用程序代码并监视应用程序周围的标识外围环境。 在此单元中, 我们将讨论一些通过设计改进应用程序安全性的方法。

## <a name="scenario"></a>方案

Lamna 医疗保健客户需要通过联机 web 门户访问其个人医疗记录。 遵守健康保险便携性和责任法案 (HIPAA) 是必需的, 如果发生个人数据泄露, 则会将公司的财务处罚降低为严重风险。因此, 将与之交互的应用程序和个人数据的安全是极其重要的。

客户应用程序关注的主要方面是:

- 安全应用程序设计
- 数据安全性
- 标识和访问管理
- 终结点安全性

## <a name="security-development-lifecycle"></a>安全开发生命周期

可以在应用程序设计阶段使用 Microsoft[安全开发生命周期](https://www.microsoft.com/sdl)(SDL) 流程, 以确保在软件开发生命周期中加入安全问题。 设计应用程序时, 安全性和合规性问题更易于解决, 并且可以减少可能导致最终产品的安全缺陷的许多常见错误。 在软件开发旅程早期修复问题也远远低于成本。 软件项目可使用的 SDL SDL 步骤的典型顺序如下所示:

1. 方面

    - 核心安全培训

1. 要求

    - 定义要求和质量关口
    - 分析安全和隐私风险
 
1. Design

    - 攻击面分析
    - 威胁建模
 
1. 实现

    - 指定工具以确保可以测量代码质量
    - 强制实施禁止的 api 和函数
    - 执行静态代码分析
    - 扫描存储的机密存储库
 
1. 校验

    - 动态/Fuzz 测试
    - 验证威胁模型/攻击面
 
1. 7。2

    - 表单安全响应计划
    - 执行最终安全评审
    - 发布存档
 
1. 响应 

    - 执行威胁响应执行

![显示安全开发生命周期的 illustraton](../media/sdl.png)

SDL 的文化方面相当于一个过程或一组工具。 构建一个区域性, 其中安全是任何应用程序开发的主要焦点和要求会对组织在安全方面的能力的发展产生极大的努力。

<!-- Bear in mind that the migration of un-modified applications (especially COTS procured software systems) will not be able to perform many of the steps listed above.
 -->

## <a name="operational-security-assessment"></a>操作安全评估

部署应用程序后, 必须不断评估其安全状态, 确定如何缓解发现的任何问题, 并将知识反馈回软件开发周期。 执行此操作的深度是软件开发和运营团队的成熟度级别以及数据隐私要求的因素。

安全漏洞扫描软件服务可用于帮助自动化此过程并在定期节奏上评估安全问题, 而无需为团队带来成本高昂的手动过程 (如渗透测试)。

azure 安全中心是在默认情况下为所有 azure 订阅启用的免费服务, 与其他 azure 应用程序级别的服务 (如 Azure 应用程序网关和 azure Web 应用程序防火墙) 紧密集成。 通过分析这些服务中的日志, ASC 可以实时报告已知漏洞, 建议对其进行缓解, 甚至将其配置为在响应攻击时自动执行行动手册。

<!-- SDL culture
Key Vault / MSI
CSE = App  -> DB & App Storage
Mention approach of code scanning & SDL
Scanning for passwords - Git
 -->

## <a name="identity-as-the-perimeter"></a>标识作为外围设备

身份验证成为应用程序防御的第一行。 通过对会话进行身份验证和授权, 限制对 web 应用程序的访问可以大大减少受攻击面。 azure ad 和 azure ad B2C 提供了一种有效的方法来分担身份和访问完全管理的服务的责任。 Azure AD 条件访问策略、特权标识管理和标识保护控件进一步增强了客户阻止未经授权的访问和审核更改的能力。

## <a name="data-protection"></a>数据保护

如果不是针对 web 应用程序的所有攻击, 则客户数据是大多数情况下的目标。 在应用程序与其数据存储层之间, 数据的安全存储和传输是极其重要的。

Lamna 保健存储和访问特别敏感的患者医疗记录数据。 由美国国会在1996中代理的 HIPAA, 用于定义医疗保健提供商和雇主的电子医疗保健交易的国家标准。 Lamna 必须确保患者和授权方 (如其医生) 可以安全地访问医疗数据。

为了符合这些要求, Lamna 医疗保健已修改其应用程序, 以在 rest 和运输中对所有患者数据进行加密。 例如, 传输层安全性 (TLS) 用于对 web 应用程序和后端 SQL 数据库之间交换的数据进行加密。 在 SQL Server 中, 数据也使用透明数据加密 (TDE) 进行加密, 以确保即使环境受到威胁, 在没有正确解密密钥的情况下, 任何人都将无法使用数据。

若要加密存储在 blob 存储中的数据, 可以使用客户端加密来加密内存中的数据, 然后再将其写入存储服务。 支持此加密的库适用于 .net、Java 和 Python, 并支持将数据加密直接集成到应用程序中, 以增强数据完整性。

### <a name="secure-key-and-secret-storage"></a>安全密钥和密钥存储

将应用程序机密 (连接字符串、密码等) 和用于访问数据的应用程序中的加密密钥隔开是至关重要的。 加密密钥和应用程序机密永远不应存储在配置文件的应用程序代码中。 相反, 应使用一个安全存储 (如 Azure Key Vault)。 然后, 可以通过托管服务标识将对此敏感数据的访问限制为应用程序标识, 并且可以定期轮换密钥以限制加密密钥泄露情况的暴露。 客户还可以选择使用本地硬件安全模块 (HSM) 生成的自己的加密密钥, 甚至强制在单租户的离散 hsm 中实施 Azure Key Vault 实例。

<!-- ### Secure and immutable file storage

All Azure storage accounts are encrypted by default using Microsoft managed keys. Azure customers also have the ability to use their own encryption keys (BYOK) to encrypt blob, file and queue data so that even the hosting provider has no access to unencrypted data. Data immutability is often required for auditing purposes or when legal disputes call for data to be effectively frozen for a determined amount of time. Azure has recently introduced an [immutable data storage](https://docs.microsoft.com/azure/storage/blobs/storage-blob-immutable-storage) option known as Write-Once, Read many (WORM) for this scenario. -->
