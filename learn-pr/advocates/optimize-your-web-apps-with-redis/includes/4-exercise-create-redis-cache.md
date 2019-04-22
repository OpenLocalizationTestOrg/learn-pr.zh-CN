让我们创建一个用于 Redis 实例的 Azure 缓存, 以存储和返回常用的值。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-redis-cache-in-azure"></a>在 Azure 中创建 Redis 缓存

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 单击 "**创建资源**", 单击 "**数据库**", 然后单击 " **Redis Cache**"。

    下面的屏幕截图显示了 Azure 门户上各种数据库资源选项中的 Redis 缓存位置。

    ![显示 Azure 门户数据库选项的屏幕截图, 其中突出显示了创建资源、数据库和 Redis 缓存选项。](../media/4-create-a-cache-1.png)

### <a name="configure-your-cache"></a>配置缓存

在缓存上应用以下设置。

1. **DNS 名称:** 创建一个全局唯一名称, 例如**ContosoSportsApp [nnn]**, 其中`[nnn]`的 where 将替换为随机数字。

1. **订阅:** 选择 "Concierge" 订阅。

1. **资源组:** 为资源组选择 " <rgn>[沙盒资源组名称]</rgn> "。

1. **位置:** 通常情况下, 应选择靠近您的客户的位置-在此示例中, 这种情况下为东海岸。

    [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]

5. **定价层:** 选择 "**基本 c0**"。 这是您可以使用的最低层。 生产应用程序可能需要存储更多数据, 并利用一些高级功能 (如群集), 这将需要更高的层次选择。

1. 单击"创建"。 Azure 将为您创建和部署 Redis 缓存实例。

    > [!IMPORTANT]
    > 通常情况下, Redis 缓存资源将在 Azure 门户中快速创建并查看, 但缓存本身在几分钟内将不可用。 接下来的步骤演示如何检查缓存的状态。

## <a name="verify-your-data"></a>验证数据

您可以使用 Azure 门户中的**控制台**功能, 在创建 Redis 缓存实例后向其发出命令。

1. 完成部署后, 通过**通知**弹出窗口找到 Redis 缓存, 或者通过选择左侧**** 边栏中的 "筛选器" 框并使用左侧的 "筛选器" 框选择 Redis 缓存实例。 或者, 也可以使用顶部的搜索框并键入缓存的名称。

1. 选择您的 Redis 缓存实例。

1. 检查 "状态" 字段的值。 在状态为 "正在运行" 之前, 缓存未准备就绪。 您可能需要等待几分钟, 然后才能继续。

1. 在缓存运行后, 单击**概述**边栏`>_ Console`上的工具栏上的 Redis 缓存中的按钮。 这将打开一个 Redis 控制台, 使您可以输入低级 Redis 命令。 请尝试以下部分:

    ```console
    ping
    ```

    ```output
    PONG
    ```

    ```console
    set test one
    ```

    ```output
    OK
    ```

    ```console
    get test
    ```

    ```output
    "one"
    ```

通过顶部的痕迹导航栏切换回**概述**面板, 或使用滚动条将视图向后滑回到左侧。

## <a name="retrieve-the-access-keys-and-host-name"></a>检索访问键和主机名

1. 选择 "**设置** > **访问密钥**"。

1. 将**主连接字符串 (StackExchange)** 复制到安全位置, 在下一个练习中将需要它。

    此项将主键和主机名包含在完整的连接字符串中, 以供在要使用的**StackExchange**程序包的应用程序设置中使用。

接下来, 我们来了解一些可用于询问缓存的命令。