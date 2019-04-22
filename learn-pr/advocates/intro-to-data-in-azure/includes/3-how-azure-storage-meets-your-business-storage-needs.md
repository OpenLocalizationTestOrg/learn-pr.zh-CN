了解 Azure 数据存储的优势, 您可以了解它提供了存储学习门户的最佳选择。 现在, 让我们详细了解这些优势和选项, 以了解它如何满足您的业务需求。

## <a name="how-azure-data-storage-can-meet-your-business-storage-needs"></a>Azure 数据存储如何满足你的业务存储需求

Azure 提供了多个存储选项, 可满足特定类型的数据存储需求。

:::row:::
  :::column:::
    ![Azure SQL 数据库](../media/3-azure-sql-db.png)
  :::column-end:::
    :::column span="3":::  
**Azure SQL 数据库**

Azure sql 数据库是基于最新稳定版本的 Microsoft SQL Server 数据库引擎的关系数据库作为服务 (DaaS)。 SQL 数据库是高性能、可靠、完全管理且安全的数据库。 您可以使用它以您选择的编程语言生成数据驱动的应用程序和网站, 而无需管理基础结构。

您可以使用 Azure 数据库迁移服务以最少停机时间迁移现有的 SQL Server 数据库。 该服务使用*Microsoft 数据迁移助手*生成评估报告, 这些报告提供的建议可帮助您在执行迁移之前完成所需的更改。 评估并执行所需的任何补救措施后, 即可开始迁移过程。 Azure 数据库迁移服务执行所有必需的步骤。 您只需更改应用程序中的连接字符串即可。 

下图显示了在线学习门户应用场景中将存储在 Azure SQL 数据库中的数据类型。

![显示用于存储学生信息 (如脚本、证书和研究资料) 的 Azure SQL 的插图。](../media/3-Azure_SQL.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Cosmos DB](../media/3-cosmos-db.png)
  :::column-end:::
    :::column span="3":::  
**Azure Cosmos DB**

Azure Cosmos DB 是一个全局分布式数据库服务。 它支持架构较少的数据, 使您能够构建高度响应且**始终**支持不断变化的数据的应用程序。 您可以使用此功能存储世界各地的用户进行更新和维护的数据。 下图显示了一个示例 Azure Cosmos DB 数据库, 该数据库用于存储遍布全球的人员访问的数据。

![该图显示了在联机培训方案中用于存储课程目录的 Azure Cosmos DB 的使用情况。 在这里, Azure Cosmos DB 是一个很好的选择, 因为该目录由管理员更新, 并由世界各地的学生访问。](../media/3-Azure_cosmos_db.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Blob 存储](../media/3-azure-blob-storage.png)
  :::column-end:::
    :::column span="3":::  
**Azure Blob 存储**

Azure Blob 存储是非*结构化*的, 这意味着它可以保留的数据类型没有任何限制。 blob 具有高可伸缩性, 应用程序使用 blob 的方式与处理磁盘上的文件 (如读取和写入数据) 的方式非常相似。 Blob 存储可以管理成千上万个同步上载、大量的视频数据、持续增长的日志文件, 并且可以通过 internet 连接从任意位置访问它们。 

blob 不限于常见的文件格式。 blob 可以包含从科学乐器流出的二进制数据的 gb 数、另一个应用程序的加密消息, 或者要开发的应用程序的自定义格式的数据。

借助 Azure Blob 存储, 可以将大型视频或音频文件直接传输到来自世界各地的用户浏览器。 Blob 存储还可用于存储备份、灾难恢复和存档的数据。 它能够存储虚拟机的最大数据量为 8 TB。 下图显示了 Azure blob 存储的示例用法。

![显示用于存储和流式传输视频或音频文件的 Azure blob 存储的插图。](../media/3-Azure_blob.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Data Lake 存储 Gen2](../media/3-azure-data-lake.png)
  :::column-end:::
    :::column span="3":::  
**Azure Data Lake 存储 Gen2**

data Lake 功能允许您对数据使用情况执行分析并准备报告。 Data Lake 是一个存储结构化和非结构化数据的大型存储库。

**Azure Data Lake Storage Gen2**将对象存储的可伸缩性和成本优势与大型数据文件系统功能的可靠性和性能结合在一起。 下图显示了 Azure Data Lake 如何存储你的所有业务数据, 并使其可供分析。

![展示了 Azure data Lake 在准备和存储数据以供分析工具使用的角色的插图。 Azure Data Lake 可以处理各种输入类型, 如关系、视频或传感器数据。](../media/3-Data_lake_store_concept.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure 文件](../media/3-azure-files.png)
  :::column-end:::
    :::column span="3":::  
**Azure 文件**

Azure 文件在云中提供了可通过行业标准服务器消息块 (SMB) 协议访问的完全管理文件共享。 Azure 文件共享可以通过云或 Windows、Linux 和 macOS 的本地部署同时安装。 在 Azure 虚拟机或云服务中运行的应用程序可以装入文件存储共享以访问文件数据, 就像桌面应用程序将装入一个典型的 SMB 共享一样。 任意数量的 Azure 虚拟机或角色都可以同时装入和访问文件存储共享。 典型的使用方案是在世界各地、诊断数据或应用程序数据共享中共享文件。 

下图显示了用于在两个地理位置之间共享数据的 Azure 文件。 Azure 文件使用服务器消息块 (SMB) 协议, 以确保在静态和传输过程中对数据进行加密。

![显示 Azure 文件的文件共享功能的说明。 ](../media/3-Azure_Files.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure 队列](../media/3-azure-queue.png)
  :::column-end:::
    :::column span="3":::  
**Azure 队列**

Azure 队列存储是一项用于存储大量可从世界各地访问的邮件的服务。

Azure 队列存储可用于帮助构建灵活的应用程序和独立的功能, 以便在大型工作负载中实现更好的持久性。 当应用程序组件被分离时, 它们可以独立扩展。 队列存储提供了异步邮件排队以在应用程序组件之间进行通信, 无论这些组件是在云中运行, 还是在桌面上、在本地, 还是在移动设备上。

通常情况下, 有一个或多个发件人组件和一个或多个接收器组件。 发件人组件将邮件添加到队列, 而收件人组件则从队列前端检索邮件以进行处理。 下图显示了多个发件人应用程序将邮件添加到 Azure 队列和检索邮件的一个接收器应用程序。

![显示 Azure 队列存储的高级别体系结构的插图](../media/3-Azure_Queue.png)

您可以使用队列存储执行以下操作:

- 创建工作积压工作并在不同的 Azure web 服务器之间传递邮件。
- 在不同的 web 服务器/基础结构之间分布负载和管理猝发流量。
- 当多个用户同时访问您的数据时, 生成组件故障的恢复能力。

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![磁盘存储](../media/3-azure-standard-storage.png)
  :::column-end:::
    :::column span="3":::  
**磁盘存储**

磁盘存储为虚拟机、应用程序和其他要访问和使用的服务提供磁盘, 与在本地应用场景中的操作方式类似。 磁盘存储允许永久存储数据, 并从附加的虚拟硬盘访问数据。 磁盘可以由 Azure 管理或非托管, 因此由用户管理和配置。 使用磁盘存储的典型方案是, 如果要将读取和写入数据的应用程序抬起和转换为永久性磁盘, 或者如果您要存储的数据不是从磁盘连接到的虚拟机外部访问的, 则为。 

磁盘具有多种不同的大小和性能级别, 从固态驱动器 (ssd) 到传统旋转硬盘 (hdd), 性能能力各不相同。

在使用 vm 时, 您可以使用标准 SSD 和 HDD 磁盘来实现较低的关键工作负载, 并为任务关键型生产应用程序提供高级 SSD 磁盘。 Azure 磁盘已始终如一地提供了企业级耐用性, 具有业界领先的零% 年度故障率。 下图显示了使用单独磁盘存储不同数据的 Azure 虚拟机。

![图中显示了虚拟机内的两个磁盘, 一个存储操作系统, 一个用于存储数据。](../media/3-Azure_disks.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![存储层](../media/3-storage-tiers.png)
  :::column-end:::
    :::column span="3":::  
**存储层**

Azure 为 blob 对象存储提供了三个存储层:

1. **热存储层**: 针对存储经常访问的数据而进行了优化。

1. **酷存储层**: 针对在至少30天内不经常访问和存储的数据进行了优化。

1. **存档存储层**: 对于至少有180天的较少访问和存储的数据, 具有灵活的延迟要求。

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![加密和复制](../media/3-azure-storage-encryption.png)
  :::column-end:::
    :::column span="3":::  
**加密和复制**

Azure 通过加密和复制功能为你的数据提供安全性和高可用性。

#### <a name="encryption-for-storage-services"></a>存储服务的加密

您的资源可使用以下加密类型:

1. 用于静态数据的**Azure 存储服务加密 (SSE)** 可帮助您保护数据, 以满足组织的安全和法规遵从性要求。 在存储数据之前对其进行加密, 并在检索数据之前对其进行解密。 加密和解密对用户是透明的。

1. **客户端加密**是指客户端库已加密数据的位置。 Azure 将数据存储在静态的加密状态, 然后在检索过程中对其进行解密。

#### <a name="replication-for-storage-availability"></a>存储可用性复制

在创建存储帐户时设置复制类型。 复制功能可确保你的数据持久且始终可用。 Azure 提供了区域和地理位置复制以保护数据免受自然灾害和其他本地灾难 (如火灾或洪水) 的攻击。

  :::column-end:::
:::row-end:::
