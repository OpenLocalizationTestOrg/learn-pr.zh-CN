若要帮助您了解对容器实例进行故障排除的基本方法, 请在此处执行一些基本操作, 例如:

* 提取容器日志
* 查看容器事件
* 附加到容器实例

## <a name="create-a-container"></a>创建容器

运行以下`az container create`命令以创建基本容器。

```azurecli
az container create \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name mycontainer \
  --image microsoft/sample-aks-helloworld \
  --ports 80 \
  --ip-address Public \
  --location eastus
```

**microsoft/aks-helloworld**图像运行显示基本网页的 web 服务器。

## <a name="get-logs-from-your-container-instance"></a>从容器实例中获取日志

运行以下`az container logs`命令, 查看容器的正在运行的应用程序的输出。

```azurecli
az container logs \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name mycontainer
```

您将看到类似于以下内容的输出。

```output
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
Running inside /app/prestart.sh, you could add migrations to this file, e.g.:

#! /usr/bin/env bash

# Let the DB start
sleep 10;
# Run migrations
alembic upgrade head
```

## <a name="get-container-events"></a>获取容器事件

此`az container attach`命令提供容器启动期间的诊断信息。 一旦容器启动, 它还会将标准输出和标准错误流写入到本地终端。

运行`az container attach`以附加到容器。

```azurecli
az container attach \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name mycontainer
```

您将看到类似于以下内容的输出。

```output
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-09-21 23:48:14+00:00) pulling image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:09+00:00) Successfully pulled image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:12+00:00) Created container
(count: 1) (last timestamp: 2018-09-21 23:49:13+00:00) Started container

Start streaming logs:
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
```

> [!TIP]
> 输入<kbd>Ctrl + C</kbd>断开与附加容器的连接。

## <a name="execute-a-command-in-your-container"></a>在容器中执行命令

在诊断和解决问题时, 您可能需要直接在正在运行的容器上运行命令。

1. 若要查看此操作, 请运行以下`az container exec`命令以在容器中启动交互式会话。

    ```azurecli
    az container exec \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --exec-command /bin/sh
    ```

    此时, 您可以有效地在容器内工作。

1. 运行`ls`命令以显示工作目录的内容。

    ```output
    # ls
    __pycache__  main.py  prestart.sh  static  templates  uwsgi.ini
    ```

1. 如果愿意, 你可以进一步探索系统。 完成后, 运行`exit`命令以停止交互式会话。

## <a name="monitor-cpu-and-memory-usage-on-your-container"></a>监视容器上的 CPU 和内存使用情况

在这里, 你将了解如何监视容器上的 CPU 和内存使用率。

1. 运行以下`az container show`命令以获取 Azure 容器实例的 id, 并将 id 存储在 Bash 变量中。

    ```azurecli
    CONTAINER_ID=$(az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --query id \
      --output tsv)
    ```

1. 运行`az monitor metrics list`命令以检索 CPU 使用情况信息。

    ```azurecli
    az monitor metrics list \
      --resource $CONTAINER_ID \
      --metric CPUUsage \
      --output table
    ```

    记下`--metric`该参数。 在这里, **CPUUsage**指定检索 CPU 使用率。

    您将看到类似于此的输出。

    ```output
    Timestamp            Name              Average
    -------------------  ------------  -----------
    2018-08-20 21:39:00  CPU Usage
    2018-08-20 21:40:00  CPU Usage
    2018-08-20 21:41:00  CPU Usage
    2018-08-20 21:42:00  CPU Usage
    2018-08-20 21:43:00  CPU Usage      0.375
    2018-08-20 21:44:00  CPU Usage      0.875
    2018-08-20 21:45:00  CPU Usage      1
    2018-08-20 21:46:00  CPU Usage      3.625
    2018-08-20 21:47:00  CPU Usage      1.5
    2018-08-20 21:48:00  CPU Usage      2.75
    2018-08-20 21:49:00  CPU Usage      1.625
    2018-08-20 21:50:00  CPU Usage      0.625
    2018-08-20 21:51:00  CPU Usage      0.5
    2018-08-20 21:52:00  CPU Usage      0.5
    2018-08-20 21:53:00  CPU Usage      0.5
    ```

1. 运行此`az monitor metrics list`命令可检索内存使用情况信息。

    ```azurecli
    az monitor metrics list \
      --resource $CONTAINER_ID \
      --metric MemoryUsage \
      --output table
    ```

    在这里, 您**** 可以指定 MemoryUsage `--metric`参数以检索内存使用情况信息。

    您将看到类似于此的输出。

    ```output
    Timestamp            Name              Average
    -------------------  ------------  -----------
    2018-08-20 21:43:00  Memory Usage
    2018-08-20 21:44:00  Memory Usage  0.0
    2018-08-20 21:45:00  Memory Usage  15917056.0
    2018-08-20 21:46:00  Memory Usage  16744448.0
    2018-08-20 21:47:00  Memory Usage  16842752.0
    2018-08-20 21:48:00  Memory Usage  17190912.0
    2018-08-20 21:49:00  Memory Usage  17506304.0
    2018-08-20 21:50:00  Memory Usage  17702912.0
    2018-08-20 21:51:00  Memory Usage  17965056.0
    2018-08-20 21:52:00  Memory Usage  18509824.0
    2018-08-20 21:53:00  Memory Usage  18649088.0
    2018-08-20 21:54:00  Memory Usage  18845696.0
    2018-08-20 21:55:00  Memory Usage  19181568.0
    ```

还可以通过 Azure 门户获取 CPU 和内存信息。 若要查看 CPU 和内存使用情况信息的直观表示形式, 请导航到容器实例的 "Azure 门户概述" 页。

![azure 容器实例的 azure 门户视图 CPU 和内存使用情况信息](../media/6-cpu-memory.png)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
