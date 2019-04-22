请记住将应用程序从本地迁移到 Azure 的方案。 此体系结构可能类似于什么？ 您的组织有一个不重要的应用程序, 这是一个不错的候选人试用。它是一种编写的应用程序, 用于解决在挑选午餐时遇到的常见问题。

试想一下, 一组朋友或同事最后一次进入午餐。 你是否发现很容易做出决定, 或者你是否需要花费大量时间来尝试了解每个人在说 "我喜欢所有内容" 时的真正意义？ 让我们根据可帮助您解决此问题的三层体系结构来部署应用程序。 此应用程序允许你提供午餐建议, 每个人都可以对其首选选择进行投票。

我们为此应用程序创建了一个模板, 该模板将每个层部署为 Azure 资源, 然后部署实际代码。 这是在 Linux 服务器上部署的 ASP.NET 核心 MVC 应用程序, 但无论底层操作系统平台或 SDK 如何, 都可以使用此体系结构样式。

下面是对使用此模板部署的内容的高级别可视化。

![要在此单位中部署的 N 层体系结构的可视化效果](../media/3-n-tier-simple.svg)

## <a name="deploy-an-n-tier-architecture"></a>部署 N 层体系结构

1. 运行以下命令以启动部署。 该`az group deployment create`命令将使用所指定的模板文件和参数将部署启动到沙盒资源组中。 此外, 还可以指定从`head /dev/urandom | tr -dc A-Za-z0-9 | head -c 32`命令生成的随机32字符字符串作为 password 参数。

    完成部署大约需要5分钟。

    ```azurecli
    az group deployment create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --template-uri  https://raw.githubusercontent.com/MicrosoftDocs/mslearn-n-tier-architecture/master/Deployment/azuredeploy.json \
      --parameters password="$(head /dev/urandom | tr -dc A-Za-z0-9 | head -c 32)"
    ```

## <a name="view-deployed-resources-and-test-the-application"></a>查看已部署的资源并测试应用程序

部署完成后, 测试应用程序。 运行以下命令, 该命令将返回应用程序的 URL。

```azurecli
az group deployment show \
  --output table \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name azuredeploy \
  --query properties.outputs.webSiteUrl
```

打开 web 浏览器并访问网站。 您会看到一个框, 可在其中添加食物选项。 添加选项后, 单击它即可添加投票。

![示例投票应用程序的屏幕截图](../media/3-lunch.png)

## <a name="three-tiers-of-whats-for-lunch"></a>三层 "午餐的用途是什么？"

此应用程序以其复杂性为单位特意精简。 它是一个有趣的应用程序, 但仍说明了三层体系结构。 该模板创建两台虚拟机 (vm)、Azure SQL 数据库以及支持这些资源所需的资源, 如磁盘、nic 和虚拟网络。 它还部署代码以在每个层上运行应用程序。 我们部署的虚拟网络具有两个子网, 一个用于表示层, 一个用于应用层, 为每个层提供一个安全边界。 

我们还将标记作为部署的一部分应用于资源, 以反映该资源支持的层 (`tier:presentation`、 `tier:application`、 `tier:data`)。 标记是一种将元数据应用于 Azure 资源的方法, 在这种情况下, 我们可以轻松筛选每个层的资源。

让我们深入了解一下每一层。 下面是我们刚刚部署的资源的详细可视化。

![要在此单位中部署的 N 层体系结构的可视化效果](../media/3-n-tier-deployment.svg)

### <a name="presentation-tier"></a>表示层

运行以下命令以列出表示层资源。

```azurecli
az resource list --tag tier=presentation --output table
```

在我们引用的三层体系结构中, 这表示的是表示层。 负责 web 界面的代码已部署在此层上, 它提供 UI 并直接处理用户请求。 此层仅与用户的网站的演示文稿相关。 它不具有对数据的直接访问权限, 并且不包含业务逻辑。

我们部署了一个名为 " **demo-web 虚拟机**" 的 web 服务器, 该服务器运行的是正在访问的网站。 服务器具有一个带有公用 IP 地址的网络接口, 即 " **demo**-web-vm-nic **-pip**", 这是我们之前检索到的 IP 地址。 它还有一个网络安全组**演示-nsg**, 仅允许从 internet 入站端口 80 (HTTP) 流量。 这将限制仅对网站的访问权限, 并阻止通过恶意使用的不必要的端口进行访问。 此层通过 HTTP 与表示层通信, 以满足对用户的请求。

### <a name="application-tier"></a>应用层

运行以下命令以列出应用层资源。

```azurecli
az resource list --tag tier=application --output table
```

应用程序层已部署在一个名为 **.biz-vm**的虚拟机上, 该虚拟机正在运行业务逻辑。 它还具有网络接口 .biz- **nic**, 但此网络接口仅具有专用 IP 地址, 而不提供到服务器的直接入站连接的任何机制。 它还具有网络安全组 **.biz-nsg**, 仅允许从表示层的子网访问。

该层是应用程序访问数据的管道。 公开在此服务器上部署表示层调用的 API 的代码。 此处不存储任何数据, 用户无法直接访问此服务器。 若要访问数据并满足用户请求, 此层通过 t-sql 命令与数据层进行通信。

在此层的应用程序中, 有一个简单的业务逻辑示例。 有对午餐建议的服务器端验证, 将它们与可接受的值列表进行比较。 如果您尝试在此列表中添加未包含的内容, 则不会接受该列表, 并将使用有效的午餐选项返回一条消息。

### <a name="data-tier"></a>数据层

运行以下命令以列出数据层资源。

```azurecli
az resource list --tag tier=data --output table
```

数据层是一个 Azure SQL 数据库服务器, **dbserver-abc123** (我们为全局唯一性的服务器名称添加一个随机字符串)。 此服务器将应用程序的数据存储在名为**demo-sqldb**的数据库中。 此应用程序层仅关注数据存储, 并提供访问它的方法, 在此示例中, 应用程序对数据库执行 t-sql。 我们不会在此层处理任何业务逻辑, 也不会对用户进行任何数据呈现。

此层通过 VNet 服务终结点公开端口1433之间的连接。 VNet 服务终结点是一种将 PaaS 服务 (如 Azure SQL Database) 连接到子网并限制仅连接到该子网中的资源的机制。

这也是使用 Platform as 服务 (PaaS) 服务取代基础结构作为服务 (IaaS) 虚拟机以运行应用程序层的示例。 N 层应用程序通常被认为是基于 VM 的应用程序, 但这并不是必需的。 通过使用 PaaS 服务取代虚拟机, 您将降低成本、提高安全性并降低管理要求。