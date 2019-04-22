由于贵公司处理高度敏感的数据, 并拥有大量要存储在 Azure 中的信息, 因此对通过公共 Internet 连接的安全性和可靠性有一些顾虑。 该公司不愿意将批发迁移到 Azure, 除非它可以演示更高级别的连接性、安全性和可靠性。

在这里, 我们将超越通过 Internet 运行的连接, 以直接转到 Azure 数据中心的专用线路。

## <a name="azure-expressroute"></a>Azure ExpressRoute

microsoft Azure ExpressRoute 使组织能够通过连接提供程序实现的专用连接将本地网络扩展到 Microsoft 云中。 这种排列意味着, 与 Azure 数据中心的连接不会通过 Internet 进行, 而是通过专用链接进行。 ExpressRoute 还促进了与其他 Microsoft 基于云的服务 (如 Office 365 和 Dynamics 365) 的有效连接。

ExpressRoute 提供的优势包括:

- 速度更快, 从 50 Mbps 到 10 Gbps, 使用动态带宽扩展

- 较低延迟

- 通过内置的对等更高的可靠性

- 高度安全

ExpressRoute 带来了许多进一步的好处, 例如:

- 与所有受支持的 Azure 服务的连接

- 与所有区域的全局连接 (需要高级附加项)

- 动态路由边界网关协议

- 连接正常运行时间的服务级别协议 (sla)

- Skype for business 的服务质量 (QoS)

此外, 还提供了 ExpressRoute premium 加载项, 它提供了更多好处, 如增加路由限制、全局服务连接和每个电路增加的虚拟网络链路。

## <a name="expressroute-connectivity-models"></a>ExpressRoute 连接模型

可以通过以下机制连接到 ExpressRoute:

- IP VPN 网络 (任意对任意)

- 通过以太网交换的虚拟交叉连接

- 点到点以太网连接

 ExpressRoute 功能和功能在上述所有连接模型中都完全相同。

### <a name="what-is-layer-3-connectivity"></a>什么是第3层连接？

Microsoft 使用行业标准的动态路由协议 (BGP) 在你的本地网络、Azure 中的实例和 Microsoft 公用地址之间的 exchange 路由。 我们为不同的流量配置文件为你的网络建立了多个 BGP 会话。

### <a name="any-to-any-ipvpn-networks"></a>"任意对任意" (IPVPN) 网络

IPVPN 提供程序通常在托管的第3层连接上提供分支机构和公司数据中心之间的连接。 在 ExpressRoute 中, Azure 数据中心看起来好像是另一个分支机构。

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a>通过以太网交换的虚拟交叉连接

如果你的组织与云 exchange 设施共同存在, 则你可以请求与 Microsoft 云的交叉连接, 但提供商的以太网交换。 与 Microsoft 云的这些跨连接可在第2层或第3层托管连接上运行, 如网络 OSI 模型中所示。

### <a name="point-to-point-ethernet-connection"></a>点到点以太网连接

点对点以太网链接可以在你的本地数据中心或分支之间为 Microsoft 云提供第2层或托管的第3层连接。

## <a name="how-expressroute-works"></a>ExpressRoute 的工作原理

Azure ExpressRoute 使用 ExpressRoute 电路和路由域的组合来提供到 Microsoft 云的高带宽连接。

### <a name="what-are-expressroute-circuits"></a>什么是 ExpressRoute 电路

ExpressRoute 电路是你的本地基础结构与 Microsoft 云之间的逻辑连接。 虽然某些组织出于冗余原因而使用多个连接提供程序, 但连接提供程序实现了该连接。 每个电路的固定带宽为50、100、200 Mbps 或 500 mbps 或 1 gbps 或 10 Gbps, 这些电路中的每一个都映射到一个连接提供程序和一个对等位置。 此外, 每个 ExpressRoute 电路都具有默认配额和限制。

ExpressRoute 电路与网络连接或网络设备不等效。 每个电路由 GUID (称为_服务_或_s 键_) 定义。 此密钥提供了 Microsoft、连接提供程序和组织之间的连接链接-它不是加密机密。 每个 s 键都具有到 Azure ExpressRoute 电路的一对一映射。

每个电路最长可包含三个 peerings, 这是为实现冗余而配置的一对 BGP 会话。 它们是:

- Azure 专用
- Azure 公共
- word

### <a name="routing-domains"></a>路由域

然后, expressroute 电路映射到路由域, 每个 expressroute 电路包含多个路由域。 这些域与上面列出的三个 peerings 相同。 在主动-主动配置中, 每对路由器都具有相同的配置, 从而提供高可用性。 azure public 和 azure 私有对等名称代表 IP 寻址方案。

#### <a name="azure-private-peering"></a>Azure 专用对等

azure 专用对连接到 azure 计算服务 (例如, 虚拟机和与虚拟网络一起部署的云服务)。 就安全性而言, 专用对等域只是将本地网络扩展到 Azure 中。 然后, 在该网络和任何 Azure 虚拟网络之间启用双向连接, 使 azure VM IP 地址在内部网络中可见。

> [!NOTE]
> 只能将一个虚拟网络连接到专用对等域。

#### <a name="azure-public-peering"></a>Azure 公共对等

azure 公共对等启用与公用 IP 地址 (如 azure 存储、azure SQL 数据库和 azure web 服务) 上可用的服务的专用连接。 通过公共对等, 您可以连接到这些服务公用 IP 地址, 而无需通过 Internet 路由流量。 连接始终从您的 WAN 连接到 Azure, 而不是其他方面。 这也是一种全或无方法, 因为您无法选择您想启用公共对等的服务。

> [!NOTE]
> 对于 Azure PaaS 服务, 建议使用 Microsoft 对等, 而不是公共对等。

#### <a name="microsoft-peering"></a>Microsoft 对等

Microsoft 对等支持与基于云的 SaaS 产品 (如 Office 365 和 Dynamics 365) 的连接。 此对等选项在公司的 WAN 和 Microsoft 云服务之间提供双向连接。

### <a name="expressroute-health"></a>ExpressRoute 运行状况

与 Microsoft Azure 中的大多数功能一样, 您可以监视 ExpressRoute 连接以确保它们的执行满意。 监视涵盖以下方面:

- 可用率
- 与虚拟网络的连接
- 带宽利用率

此监视活动的关键工具是网络性能监视器, 尤其是 ExpressRoute 的 NPM。

azure ExpressRoute 用于在你的内部部署中或在 colocation 环境中创建 azure 数据中心和基础结构之间的专用连接。 ExpressRoute 连接不通过公共 internet, 它们提供更高的可靠性、更快的速度和比典型的 Internet 连接更低的延迟。
