:::row:::
  :::column:::
    ![表示 Azure 容器的图像](../media/4-azure-containers.png)
  :::column-end:::
  :::column span="3":::
如果要在单个虚拟机上运行应用程序的多个实例, 则容器是极好的选择。 容器 orchestrator 可以根据需要启动、停止和扩展应用程序实例。
  :::column-end:::
:::row-end:::

容器旨在进行轻型、创建、横向扩展和停止。 此设计允许您快速响应需求或失败的变化。

容器的另一个优势是, 您可以在单个 VM 主机上运行多个独立的应用程序。 由于容器受保护和隔离, 因此不需要每个应用程序都具有单独的虚拟机。

#### <a name="vms-versus-containers"></a>vm 与容器

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuaq]

## <a name="containers-in-azure"></a>Azure 中的容器

azure 支持 Docker 容器, 可以通过多种方式管理 azure 中的容器。

- Azure 容器实例 (ACI)
- Azure Kubernetes Service (AKS)

### <a name="azure-container-instances"></a>Azure 容器实例

azure 容器实例 (ACI) 提供了在 Azure 中运行容器的速度最快且最简单的方法。 您无需管理任何虚拟机或配置任何其他服务。 它是一个 PaaS 产品, 允许您上载并直接执行容器。 

### <a name="azure-kubernetes-service"></a>Azure Kubernetes 服务

自动执行和管理大量容器以及与大量容器交互的任务称为 "业务流程"。 对于具有多个容器的分布式体系结构的容器, Azure Kubernetes Service (AKS) 是一个完整的业务流程服务。 

#### <a name="what-is-kubernetes"></a>什么是 Kubernetes？

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuX]

### <a name="using-containers-in-your-solutions"></a>在解决方案中使用容器

容器通常用于创建使用_microservice 体系结构_的解决方案。 这是将解决方案分解为较小的独立部分的位置。 例如, 您可以将网站拆分为承载前端的容器、另一个托管的后端和第三个存储。 这使您可以将应用程序的各个部分分隔成可独立进行维护、扩展或更新的逻辑部分。

#### <a name="what-is-a-microservice"></a>什么是 microservice？

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yual]

设想你的网站后端已达到容量, 但前端和存储不会产生压力。 您可以单独扩展后端以提高性能, 也可以决定使用不同的存储服务。 或者, 甚至可以替换存储容器, 而不会影响应用程序的其余部分。