许可是可以显著影响你的云支出的另一个领域。 让我们来看看可降低许可成本的方法。

## <a name="linux-vs-windows"></a>Linux 与 Windows

您部署的许多 Azure 服务都可以选择在 Windows 或 Linux 上运行。 在某些情况下, 产品的成本可能因您选择的 OS 而异。 在您有选择的地方, 并且您的应用程序不依赖于基础操作系统, 因此比较定价以确定是否可以节省资金的方法非常有用。

## <a name="azure-hybrid-benefit-for-windows-server"></a>适用于 Windows Server 的 Azure 混合优势

许多客户已投入使用 Windows Server 许可证, 希望在 Azure 上重新使用这一投资。 azure 混合权益为客户提供了将这些许可证用于 Azure 上的虚拟机的权利。 这意味着您不会为 Windows Server 许可证付费, 而是将按 Linux 费率付费。

若要获得对此权益的资格, 您的 Windows 许可证必须包含在软件保证中。 还将应用以下准则:

- 每个双处理器许可证或每组16核许可证都有权拥有最多8个核心的两个实例或一个最多16个内核的实例。
- Standard Edition 许可证仅可在本地使用或在 Azure 中使用。 这意味着您不能对 Azure VM 和本地计算机使用相同的许可证。
- Datacenter Edition 优势允许在本地和 Azure 中同时使用, 因此许可证将涵盖两台运行的 Windows 计算机。

> [!NOTE]
> 大多数客户通常由核心许可提供, 因此您将使用该模型进行计算。 如果你对拥有的许可证有任何疑问, 请联系你的许可证经销商或你的 Microsoft 帐户团队。

应用优势非常简单。 可以随时使用现有 vm 或在部署时为新的虚拟机启用和禁用。 混合优势 (尤其是与保留实例结合使用时) 可提供显著的许可证节省。

## <a name="azure-hybrid-benefit-for-sql-server"></a>SQL Server 的 Azure 混合优势

SQL Server 的 Azure 混合优势可帮助您最大限度地提高当前许可投资的价值, 并加快迁移到云的速度。 sql server 的 azure 混合优势是基于 Azure 的优势, 使您能够将 SQL server 许可证与活动软件保障结合使用, 以支付降低的速率。

即使 Azure 资源处于活动状态, 也可以使用此权益, 但降低的速度仅会从您在门户中选择它的时间应用。 不会向追溯颁发任何信用。

### <a name="azure-sql-database-vcore-based-options"></a>基于 vCore 的 Azure SQL 数据库选项

对于 azure SQL 数据库, azure 混合优势的工作原理如下:

- 如果每个核心许可证的标准版许可证具有活动的软件保证, 则可以在通用服务层中为您在本地拥有的每一个许可证核心获取一个 vCore。
- 如果您拥有具有活动软件保证的每个核心许可证的 Enterprise Edition, 则可以在业务关键型服务层中为您在本地拥有的每一个许可证核心获取一个 vCore。 请注意, 针对业务关键型服务层的 SQL Server 的 Azure 混合优势仅适用于拥有企业版许可证的客户。
- 如果您具有具有活动的软件保证的每个核心许可证的高虚拟化企业版许可证, 则可以在通用服务层中为您在本地拥有的每一个许可证核心获取四个 vCores。 这是仅适用于 Azure SQL 数据库的独特虚拟化优势。

下图显示了在每个服务层中提供的基于 vCore 的选项, 这些选项具有针对 SQL Server 许可证的 Azure 混合优势。

![图中显示了如何使用 Azure 混合优势最大限度地提高现有的 SQL server 许可证值的示例。](../media/5-sql-tradein-value.png)

对于 azure 虚拟机中的 SQL Server, azure 混合优势的工作原理如下:

- 如果您拥有具有活动软件保证的每个核心许可证的 Enterprise edition, 则您可以在 Azure 虚拟机中获取 SQL Server enterprise edition 的一种核心, 其中包含内部部署的每个许可证核心。
- 如果每个核心许可证具有活动的软件保证, 则可以在 Azure 虚拟机中获取 SQL Server standard edition 的一个核心, 其中包含内部部署的每个许可证核心。

这可能会对使用 SQL Server 工作负荷的 Azure 支出产生显著影响。

## <a name="use-devtest-subscription-offers"></a>使用开发/测试订阅提供

[企业开发/测试](https://azure.microsoft.com/offers/ms-azr-0148p/)和即[用即点即用开发/测试](https://azure.microsoft.com/offers/ms-azr-0023p/)提供的好处是, 您可以利用此优势在非生产环境中节省成本。 此好处为您提供了几个折扣, 最适用于 Windows 工作负载, 从而消除了许可证费用, 并且仅在虚拟机的 Linux 比率上付费。 这也适用于 SQL Server 以及 Visual Studio 订阅 (以前称为 MSDN) 中涵盖的任何其他 Microsoft 软件。 

此好处有几个要求, 其中一种是仅针对非生产工作负载, 另一种是这些环境中的任何用户 (不包括测试人员) 必须在 Visual Studio 订阅下进行介绍。 简言之, 对于非生产工作负载, 这使您可以节省 Windows、SQL Server 和其他 Microsoft 虚拟机工作负载的成本。

以下是每个优惠的完整详细信息。 如果您是企业协议的客户, 您想要利用企业开发/测试服务, 如果您是没有企业协议的客户, 而是使用 PAYG 帐户, 则可以利用随使用付费的开发/测试提供。

## <a name="bring-your-own-sql-server-license"></a>引入你自己的 SQL Server 许可证

如果您是企业协议的客户并且已经在 SQL Server 许可证中获得了投资, 并且它们已作为将资源移动到 azure 的一部分进行了释放, 则可以预配将**您自己的许可证**(BYOL) 映像从 azure Marketplace 中移出, 从而为您提供能够利用这些未使用的许可证并降低 Azure VM 的成本。 您始终可以通过设置 Windows VM 并手动安装 SQL Server 来执行此操作, 但这将通过利用 Microsoft 认证的图像简化了创建过程。 在市场中搜索**BYOL**以查找这些图像。

![显示 SQL Server 的 BYOL 选项的 Azure 门户屏幕截图。](../media/5-byol-sql-server.png)

> [!IMPORTANT]
> 需要企业协议订阅才能使用这些经过认证的 BYOL 图像。

## <a name="use-sql-server-developer-edition"></a>使用 SQL Server 开发人员版

很多人都不知道 SQL Server 开发人员版是**nonproduction 使用**的免费产品。 开发版具有企业版中的所有相同功能, 但对于 nonproduction 工作负荷, 您可以显著节省许可成本。

查找 Azure Marketplace 的开发人员版 SQL server 映像, 并将其用于开发或测试目的, 以在这些情况下消除 sql Server 的额外成本。

> [!TIP]
> 若要获取完整的许可信息, 请查看所[记录的定价指南](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance)。

## <a name="use-constrained-instance-sizes-for-database-workloads"></a>对数据库工作负荷使用受约束的实例大小

许多客户对内存、存储或 i/o 带宽有较高要求, 但 CPU 核心计数较低。 根据此常见的请求, Microsoft 已在新大小中提供了最常见的 VM 大小 (DS、ES、GS 和 MS), 这些大小将 vCPU 计数限制为原始 VM 大小的一个半或四分之一, 同时保持相同的内存、存储和 i/o 带宽。

| VM 大小 | vCPUs | 不足 | 最大磁盘 | 最大 i/o 吞吐量 | 每年 SQL Server 企业版许可成本 | 每年总成本 (计算 + 许可) |
|---------|-------|--------|-----------|--------------------|-----------------------------------------------|---------------------------|
| Standard_DS14v2   | 位 | 112 GB | 32 | 51200 IOPS 或 768 MB/秒 |           |           |
| Standard_DS14-4v2 | **4**  | 112 GB | 32 | 51200 IOPS 或 768 MB/秒 | 低 75% | 低 57% |
| Standard_GS5      | 32 | 448    | 64 | 80000 IOPS 或 2 GB/秒   |           |           |
| Standard_GS5-8    | **utf-8**  | 448    | 64 | 80000 IOPS 或 2 GB/秒   | 低 75% | 低 42% |

由于 SQL Server 和 Oracle 等数据库产品是按 CPU 许可的, 因此这使客户能够将许可成本降低到 75%, 但仍保持数据库的高性能。