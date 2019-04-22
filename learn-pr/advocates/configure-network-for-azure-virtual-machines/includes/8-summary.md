Azure 提供了三种用于设置虚拟网络的主要方法:

- Azure 虚拟网络
- Azure VPN 网关
- Azure ExpressRoute

Azure 虚拟网络可以连接相同区域内的虚拟机和虚拟机扩展集等资源, 使其能够进行通信。 azure 虚拟网络也可以连接到指定的 azure 服务终结点, 如 azure 存储、数据库和 web 应用。

Azure VPN 网关可以通过公共 Internet 启用与本地客户端或网络的通信, 或在不同的 Azure 区域中连接虚拟网络。 如果需要高度安全的专用路由, 可以使用 Azure ExpressRoute。 它创建到 Azure 数据中心的专用高带宽连接, 以实现最高级别的可靠性和安全性。

## <a name="cleanup"></a>清空

此模块中的交互式练习创建了两个资源`VpnGatewayDemo`组`vm-networks`和。 删除这些资源组以清理练习中创建的资源。