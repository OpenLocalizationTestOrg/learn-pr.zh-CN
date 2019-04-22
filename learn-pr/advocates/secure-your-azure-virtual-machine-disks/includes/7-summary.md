azure 提供了存储服务加密 (SSE) 和 azure 磁盘加密 (ADE), 以确保 azure 虚拟磁盘的安全。 这些技术协同工作以提供强大的256位加密, 作为保护 Azure VM 磁盘的纵深防御方法的一部分。 必须完成 Azure 磁盘加密先决条件, 才能启用磁盘加密。 Azure 磁盘加密先决条件配置脚本可以自动执行此过程。 对新 vm 启用加密时, 可以使用 Azure 资源管理器模板。 这样可确保在部署点对数据进行加密, 而不留下任何漏洞。

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>其他资源

- [Azure VM 磁盘加密故障排除](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-tsg)
- [如何在 Azure 中加密 Linux 虚拟机](https://docs.microsoft.com/azure/virtual-machines/linux/encrypt-disks)
- [Azure 磁盘加密概述](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-overview)
- [Azure 磁盘加密支持哪些 Linux 分布？](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-faq#bkmk_LinuxOSSupport)。
- [GitHub 上的资源管理器模板](https://github.com/Azure/azure-quickstart-templates)