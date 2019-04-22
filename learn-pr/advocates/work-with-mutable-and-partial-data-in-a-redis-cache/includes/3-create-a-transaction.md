首先, 创建 Redis 的 Azure 缓存实例, 然后创建一个简单的事务, 将两个数据值插入到缓存中。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-cache-for-redis"></a>为 Redis 创建 Azure 缓存

让我们先通过 azure CLI 为 Redis 创建 azure 缓存。 使用浏览器窗口右侧的云命令行管理程序与 Azure 进行交互。

我们将使用`az redis create`命令为 Redis 创建新的 Azure 缓存。 它需要多个参数。 下面列出了最常见的内容 (若要获取完整列表, 请查看文档)。

> [!div class="mx-tableFixed"]
> | 参数 | 说明 |
> |-----------|-------------|
> | `--name`    | 缓存的名称-这必须全局唯一且由字母、数字和短划线组成。 |
> | `--resource-group` | 使用预创建的资源组**<rgn>[沙盒资源组名称]</rgn>**, 它是 Azure 沙箱的一部分。 |
> | `--location` | 指定缓存应位于的位置。 通常情况下, 您需要选择靠近数据使用者的位置。 在这种情况下, 您仅限于在 Azure 沙盒中提供的位置。 选择最接近的一个。 |
> | `--size` | Redis 的 Azure 缓存大小。 有效值为 [C0、C1、C2、C3、C4、C5、C6、P1、P2、P3、P4]。 |
> | `--sku` | Redis SKU 的 Azure 缓存。 有效值为 [Basic, Standard, Premium]。 |

### <a name="select-a-location"></a>选择位置
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. 使用以下选项创建缓存:
    - 大小: C0
    - SKU: 基本

1. 下面是一个示例命令行。 请务必将`[name]`参数替换为唯一的名称。 如果需要与美国东部区域不同的区域, 可以替换该位置。

    ```azurecli
    REDIS_NAME=[name]

    az redis create \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location eastus \
        --vm-size C0 \
        --sku Basic
    ```

## <a name="create-a-net-core-console-application"></a>创建 .net Core 控制台应用程序

接下来, 创建一个 .net Core 控制台应用程序, 该应用程序将用于将数据值插入到 Redis 的 Azure 缓存中。

1. 使用窗口右侧的集成云命令行管理程序创建新的 .net Core 应用程序。 将其命名为 "RedisData"。

    ```bash
    cd ~
    dotnet new console --name RedisData
    ```

1. 更改为您的应用程序创建的新目录。

    ```bash
    cd RedisData
    ```

1. 生成并运行应用程序-它应输出 "Hello World!"

    ```bash
    dotnet run
    ```

## <a name="add-the-servicestackredis-nuget-package"></a>添加 Redis NuGet 包 ServiceStack

至此, 我们已拥有控制台应用程序, 我们需要添加**ServiceStack** NuGet 包。 这将允许我们在 c # 中连接到适用于 Redis 的 Azure 缓存并发出命令。

1. 使用终端命令行管理程序添加 NuGet 程序包**ServiceStack Redis** 。

    ```bash
    dotnet add package ServiceStack.Redis
    ```

1. 再次生成并运行应用程序以确保所有编译都能进行编译。 它仍应输出 "Hello World!"

## <a name="get-your-azure-cache-for-redis-connection-string"></a>获取 Redis 连接字符串的 Azure 缓存

若要连接到 Redis 的 Azure 缓存, 您需要一个包含您的密码和 URL 的连接字符串。 **ServiceStack**具有其自己的连接字符串格式: `[password]@[hostname]:[sslport]?ssl=true`。

你可以使用 Azure 门户或命令行检索你的密码。 由于我们在 "通过将只读数据缓存到 Redis" 模块中使用了 "优化 web 应用程序" 中的门户方法, 因此我们在这里使用这一方法。

使用`az redis list-keys`命令获取访问键。 运行这些命令以获取主键, 将其存储在名`REDIS_KEY`为的变量中, 并显示该主键:

```azurecli
REDIS_KEY=$(az redis list-keys \
    --name "$REDIS_NAME" \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query primaryKey \
    --output tsv)

echo $REDIS_KEY
```

接下来, 运行此命令以将连接字符串放在一起, 并在命令行中显示它。 请注意, 主机名是后跟的缓存的名称`.redis.cache.windows.net`, 端口是**6380**, 是默认的 Redis SSL 端口。

```bash
echo "$REDIS_KEY"@"$REDIS_NAME".redis.cache.windows.net:6380?ssl=true
```

将连接字符串复制到您将&mdash;在下一步中使用的剪贴板。

## <a name="add-the-connection-string-to-your-app"></a>将连接字符串添加到应用程序

1. 从应用程序文件夹中打开云命令行管理程序编辑器。

    ```bash
    cd ~/RedisData
    code .
    ```

1. 选择 " **Program.cs** " 源文件。

1. 在`Program`类中创建以下字段, 并将连接字符串粘贴为值。

    ```csharp
    static string redisConnectionString = "<connection string>";
    ```

    下面是一个示例:

    ```csharp
    static string redisConnectionString = "ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6380?ssl=true";
    ```

## <a name="insert-two-data-values-into-your-azure-cache-for-redis"></a>将两个数据值插入到 Redis 的 Azure 缓存中

最后, 我们要将数据添加到 Redis 的 Azure 缓存中。

1. 将以下`using`语句添加到**Program.cs**文件的顶部。

    ```csharp
    using ServiceStack.Redis;
    ```

1. 将`Main`方法的内容替换为以下代码。 这将使用事务来添加两个值。

    ```csharp
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    if (transactionResult)
    {
        Console.WriteLine("Transaction committed");
    }
    else
    {
        Console.WriteLine("Transaction failed to commit");
    }
    ```

1. 在生成和运行应用程序之前, 请进行检查以确保已完全预配 Redis 缓存。 在完成后`az redis create` , 有时可能需要几分钟时间。 运行以下命令以检查状态。

    ```azurecli
    az redis show \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --query provisioningState
    ```

    如果状态为`Creating`, 请尝试在几分钟内再次检查。 完成后, `Succeeded`它将显示。

1. 运行应用程序, 并验证控制台是否显示**事务已提交**。

    ```bash
    dotnet run
    ```

## <a name="verify-your-data"></a>验证数据

若要结束, 我们将验证我们添加的数据是否在 Redis 的 Azure 缓存中。

1. 使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。

1. 通过选择左侧侧栏中的 "**所有资源**", 然后使用左侧的 "筛选器" 框为 Redis 实例选择 azure 缓存, 找到 Redis 的 azure 缓存。 或者, 也可以使用顶部的搜索框, 并键入缓存的名称。

1. 为 Redis 实例选择 Azure 缓存。

1. 在用于 Redis 的 Azure 缓存的**概述**刀片中, 选择 "**控制台**"。 这将打开 Redis 控制台的 Azure 缓存, 使您可以为 Redis 命令输入低级别 Azure 缓存。

1. 运行命令`get MyKey1`。 验证返回的值是否为**MyValue1**。

1. 运行命令`get MyKey2`。 验证返回的值是否为**MyValue2**。

    ![Redis 控制台的 Azure 缓存的屏幕截图, 显示 MyKey1 和 MyKey2 的值。](../media/4-redis-console.png)