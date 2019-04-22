Azure 容器注册表是基于开放源代码 Docker 注册表2.0 的托管 Docker 注册表服务。 容器注册表是私有的, 托管在 Azure 中, 允许您生成、存储和管理所有类型的容器部署的图像。

可以使用 Docker cli 或 Azure cli 将容器映像推送和提取到容器注册表中。 Azure 门户集成允许你直观地检查容器注册表中的容器图像。 在分布式环境中, 容器注册表地域复制功能可用于将容器映像分发到多个 Azure 数据中心以用于本地化的分发。

除了存储容器图像之外, azure 容器注册表任务还可以在 azure 中构建容器映像。 任务使用标准 Dockerfile 在 Azure 容器注册表中创建和存储容器图像, 而无需本地 Docker 工具。 使用 Azure 容器注册表任务, 您可以根据需要生成或完全自动化使用 DevOps 过程和工具生成的容器映像。

## <a name="learning-objectives"></a>学习目标

在本模块中, 您将:

- 部署 Azure 容器注册表
- 使用 Azure 容器注册表任务生成容器映像
- 将容器部署到 Azure 容器实例
- 将容器映像复制到多个 Azure 数据中心

## <a name="prerequisites"></a>先决条件  

- 无