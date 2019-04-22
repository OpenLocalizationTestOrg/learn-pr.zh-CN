在此单元中, 你将使用 Azure 资源管理器模板来解密我们之前创建的 Windows VM。 我们在 Windows VM 上加密了 OS 驱动器。 但是, OS 驱动器上不包含任何机密信息, 因此我们可以将其保留为未加密。 让我们使用模板对 OS 驱动器进行解密。

## <a name="decrypt-a-vm-using-an-azure-resource-manager-template"></a>使用 Azure 资源管理器模板对 VM 进行解密

我们将使用 Microsoft 在 GitHub 上发布的模板, 该模板专门用于解密正在运行的 Windows VM。

1. 使用与激活沙盒时相同的帐户登录到[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 单击左侧边栏中**的 "创建资源**"。

1. 在搜索框中键入**模板**。

1. 从生成的列表中选择 "**模板部署**", 然后单击 "**创建**"。

    ![显示 "创建" 按钮选中的模板部署项目的屏幕截图](../media/6-create-template.png)

1. 在 "**选择模板**" 搜索框中, 开始键入 "201-解密", 并选择 "201-不解密-不使用 aad 的 windows-vm-不安装-aad" 模板。

    ![显示 "选择模板" 搜索框和自动完成的屏幕截图](../media/6-custom-deployment.png)

1. 单击 "**选择模板**" 以启动模板运行程序。

1. 在 "设置" 视图中, 输入以下信息:
    - 选择**订阅**的_Concierge 订阅_。
    - 选择沙盒资源组<rgn>沙盒 RG</rgn>。 这也将自动选择该区域。
    - 为**VM 名称**输入 "fmdata-vm01"。
    - 将**卷类型**保留为 "_全部_"。

1. 选中 "**我同意条款和条件**" 复选框。
1. 单击 "**购买**" 以运行模板。 请注意, 此按钮没有成本-它是一个标准按钮。

部署可能需要几分钟时间才能完成。

## <a name="verify-the-encryption-status-of-the-vm"></a>验证 VM 的加密状态

1. 在 Azure 门户的边栏中, 单击 "**虚拟机**", 然后选择您**的 VM fmdata-vm01**。 或者, 您可以从**所有资源**按名称搜索 VM。

1. 在**虚拟机**边栏上的 "**设置**" 下, 单击 "**磁盘**"。

1. 在**磁盘**边栏上, 请注意, OS 磁盘加密状态现已**禁用**。
