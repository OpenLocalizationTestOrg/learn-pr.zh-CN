在 Azure 容器实例中部署容器的方便性和速度非常适合于执行仅运行一次的任务, 如图像呈现或生成和测试应用程序。

使用可配置的重新启动策略, 您可以指定在其进程完成时停止容器。 由于容器实例由第二个实例计费, 因此仅对执行任务的容器运行时所使用的计算资源进行计费。

## <a name="what-are-container-restart-policies"></a>什么是容器重启策略？

Azure 容器实例具有三个重新启动策略选项:

| 重新启动策略   | 说明 |
| ---------------- | :---------- |
| **都** | 容器组中的容器始终会重新启动。 此策略对长时间运行的任务 (如 web 服务器) 有意义。 这是在创建容器时未指定重新启动策略时应用的**默认**设置。 |
| **永不** | 容器组中的容器永远不会重新启动。 容器仅运行一次。 |
| **OnFailure** | 只有在容器中执行的进程失败时 (当它以非零退出代码结束时), 才会重新启动容器组中的容器。 至少运行一次容器。 此策略适用于运行短生存期任务的容器。 |

## <a name="run-a-container-to-completion"></a>运行要完成的容器

若要查看 "重新启动策略" 操作, 请从**microsoft/aci-wordcount** Docker 图像创建一个容器实例, 并指定**OnFailure**重新启动策略。 此容器运行一个用于分析 Shakespeare 的 Hamlet 文本的 Python 脚本, 将10个最常用的词写入标准输出, 然后退出。

1. 运行此`az container create`命令以启动容器。

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer-restart-demo \
      --image microsoft/aci-wordcount:latest \
      --restart-policy OnFailure \
      --location eastus
    ```

    Azure 容器实例启动容器, 然后在其进程 (在此示例中为脚本) 退出时将其停止。 当 Azure 容器实例停止其重新启动策略**从不**或**OnFailure**的容器时, 容器的状态设置为 "已**终止**"。

1. 运行`az container show`以检查容器的状态。

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer-restart-demo \
      --query containers[0].instanceView.currentState.state
    ```

    重复命令, 直到它达到**终止**状态。

1. 查看容器的日志以检查输出。 若要执行此操作`az container logs` , 请运行, 如下所示。

    ```azurecli
    az container logs \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer-restart-demo
    ```

    你会看到这一点。

    ```json
    [('the', 990),
     ('and', 702),
     ('of', 628),
     ('to', 610),
     ('I', 544),
     ('you', 495),
     ('a', 453),
     ('my', 441),
     ('in', 399),
     ('HAMLET', 386)]
    ```