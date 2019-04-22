<span data-ttu-id="04b78-101">若要帮助您了解对容器实例进行故障排除的基本方法, 请在此处执行一些基本操作, 例如:</span><span class="sxs-lookup"><span data-stu-id="04b78-101">To help you understand basic ways to troubleshoot container instances, here you'll perform some basic operations such as:</span></span>

* <span data-ttu-id="04b78-102">提取容器日志</span><span class="sxs-lookup"><span data-stu-id="04b78-102">Pulling container logs</span></span>
* <span data-ttu-id="04b78-103">查看容器事件</span><span class="sxs-lookup"><span data-stu-id="04b78-103">Viewing container events</span></span>
* <span data-ttu-id="04b78-104">附加到容器实例</span><span class="sxs-lookup"><span data-stu-id="04b78-104">Attaching to a container instance</span></span>

## <a name="create-a-container"></a><span data-ttu-id="04b78-105">创建容器</span><span class="sxs-lookup"><span data-stu-id="04b78-105">Create a container</span></span>

<span data-ttu-id="04b78-106">运行以下`az container create`命令以创建基本容器。</span><span class="sxs-lookup"><span data-stu-id="04b78-106">Run the following `az container create` command to create a basic container.</span></span>

```azurecli
az container create \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name mycontainer \
  --image microsoft/sample-aks-helloworld \
  --ports 80 \
  --ip-address Public \
  --location eastus
```

<span data-ttu-id="04b78-107">**microsoft/aks-helloworld**图像运行显示基本网页的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="04b78-107">The **microsoft/sample-aks-helloworld** image runs a web server that displays a basic web page.</span></span>

## <a name="get-logs-from-your-container-instance"></a><span data-ttu-id="04b78-108">从容器实例中获取日志</span><span class="sxs-lookup"><span data-stu-id="04b78-108">Get logs from your container instance</span></span>

<span data-ttu-id="04b78-109">运行以下`az container logs`命令, 查看容器的正在运行的应用程序的输出。</span><span class="sxs-lookup"><span data-stu-id="04b78-109">Run the following `az container logs` command to see the output from the container's running application.</span></span>

```azurecli
az container logs \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name mycontainer
```

<span data-ttu-id="04b78-110">您将看到类似于以下内容的输出。</span><span class="sxs-lookup"><span data-stu-id="04b78-110">You see output that resembles the following.</span></span>

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

## <a name="get-container-events"></a><span data-ttu-id="04b78-111">获取容器事件</span><span class="sxs-lookup"><span data-stu-id="04b78-111">Get container events</span></span>

<span data-ttu-id="04b78-112">此`az container attach`命令提供容器启动期间的诊断信息。</span><span class="sxs-lookup"><span data-stu-id="04b78-112">The `az container attach` command provides diagnostic information during container startup.</span></span> <span data-ttu-id="04b78-113">一旦容器启动, 它还会将标准输出和标准错误流写入到本地终端。</span><span class="sxs-lookup"><span data-stu-id="04b78-113">Once the container has started, it also writes standard output and standard error streams to your local terminal.</span></span>

<span data-ttu-id="04b78-114">运行`az container attach`以附加到容器。</span><span class="sxs-lookup"><span data-stu-id="04b78-114">Run `az container attach` to attach to your container.</span></span>

```azurecli
az container attach \
  --resource-group <rgn>[sandbox resource group name]</rgn> \
  --name mycontainer
```

<span data-ttu-id="04b78-115">您将看到类似于以下内容的输出。</span><span class="sxs-lookup"><span data-stu-id="04b78-115">You see output that resembles the following.</span></span>

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
> <span data-ttu-id="04b78-116">输入<kbd>Ctrl + C</kbd>断开与附加容器的连接。</span><span class="sxs-lookup"><span data-stu-id="04b78-116">Enter <kbd>Ctrl+C</kbd> to disconnect from your attached container.</span></span>

## <a name="execute-a-command-in-your-container"></a><span data-ttu-id="04b78-117">在容器中执行命令</span><span class="sxs-lookup"><span data-stu-id="04b78-117">Execute a command in your container</span></span>

<span data-ttu-id="04b78-118">在诊断和解决问题时, 您可能需要直接在正在运行的容器上运行命令。</span><span class="sxs-lookup"><span data-stu-id="04b78-118">As you diagnose and troubleshoot issues, you may need to run commands directly on your running container.</span></span>

1. <span data-ttu-id="04b78-119">若要查看此操作, 请运行以下`az container exec`命令以在容器中启动交互式会话。</span><span class="sxs-lookup"><span data-stu-id="04b78-119">To see this in action, run the following `az container exec` command to start an interactive session on your container.</span></span>

    ```azurecli
    az container exec \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --exec-command /bin/sh
    ```

    <span data-ttu-id="04b78-120">此时, 您可以有效地在容器内工作。</span><span class="sxs-lookup"><span data-stu-id="04b78-120">At this point, you are effectively working inside of the container.</span></span>

1. <span data-ttu-id="04b78-121">运行`ls`命令以显示工作目录的内容。</span><span class="sxs-lookup"><span data-stu-id="04b78-121">Run the `ls` command to display the contents of the working directory.</span></span>

    ```output
    # ls
    __pycache__  main.py  prestart.sh  static  templates  uwsgi.ini
    ```

1. <span data-ttu-id="04b78-122">如果愿意, 你可以进一步探索系统。</span><span class="sxs-lookup"><span data-stu-id="04b78-122">You can explore the system further if you wish.</span></span> <span data-ttu-id="04b78-123">完成后, 运行`exit`命令以停止交互式会话。</span><span class="sxs-lookup"><span data-stu-id="04b78-123">When you're done, run the `exit` command to stop the interactive session.</span></span>

## <a name="monitor-cpu-and-memory-usage-on-your-container"></a><span data-ttu-id="04b78-124">监视容器上的 CPU 和内存使用情况</span><span class="sxs-lookup"><span data-stu-id="04b78-124">Monitor CPU and memory usage on your container</span></span>

<span data-ttu-id="04b78-125">在这里, 你将了解如何监视容器上的 CPU 和内存使用率。</span><span class="sxs-lookup"><span data-stu-id="04b78-125">Here you'll see how to monitor CPU and memory usage on your container.</span></span>

1. <span data-ttu-id="04b78-126">运行以下`az container show`命令以获取 Azure 容器实例的 id, 并将 id 存储在 Bash 变量中。</span><span class="sxs-lookup"><span data-stu-id="04b78-126">Run the following `az container show` command to get the ID of your Azure container instance and store the ID in a Bash variable.</span></span>

    ```azurecli
    CONTAINER_ID=$(az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer \
      --query id \
      --output tsv)
    ```

1. <span data-ttu-id="04b78-127">运行`az monitor metrics list`命令以检索 CPU 使用情况信息。</span><span class="sxs-lookup"><span data-stu-id="04b78-127">Run the `az monitor metrics list` command to retrieve CPU usage information.</span></span>

    ```azurecli
    az monitor metrics list \
      --resource $CONTAINER_ID \
      --metric CPUUsage \
      --output table
    ```

    <span data-ttu-id="04b78-128">记下`--metric`该参数。</span><span class="sxs-lookup"><span data-stu-id="04b78-128">Note the `--metric` argument.</span></span> <span data-ttu-id="04b78-129">在这里, **CPUUsage**指定检索 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="04b78-129">Here, **CPUUsage** specifies to retrieve CPU usage.</span></span>

    <span data-ttu-id="04b78-130">您将看到类似于此的输出。</span><span class="sxs-lookup"><span data-stu-id="04b78-130">You see output similar to this.</span></span>

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

1. <span data-ttu-id="04b78-131">运行此`az monitor metrics list`命令可检索内存使用情况信息。</span><span class="sxs-lookup"><span data-stu-id="04b78-131">Run this `az monitor metrics list` command to retrieve memory usage information.</span></span>

    ```azurecli
    az monitor metrics list \
      --resource $CONTAINER_ID \
      --metric MemoryUsage \
      --output table
    ```

    <span data-ttu-id="04b78-132">在这里, 您\*\*\*\* 可以指定 MemoryUsage `--metric`参数以检索内存使用情况信息。</span><span class="sxs-lookup"><span data-stu-id="04b78-132">Here, you specify **MemoryUsage** for the `--metric` argument to retrieve memory usage information.</span></span>

    <span data-ttu-id="04b78-133">您将看到类似于此的输出。</span><span class="sxs-lookup"><span data-stu-id="04b78-133">You see output similar to this.</span></span>

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

<span data-ttu-id="04b78-134">还可以通过 Azure 门户获取 CPU 和内存信息。</span><span class="sxs-lookup"><span data-stu-id="04b78-134">CPU and memory information is also available through the Azure portal.</span></span> <span data-ttu-id="04b78-135">若要查看 CPU 和内存使用情况信息的直观表示形式, 请导航到容器实例的 "Azure 门户概述" 页。</span><span class="sxs-lookup"><span data-stu-id="04b78-135">To see a visual representation of CPU and memory usage information, navigate to the Azure portal overview page for your container instance.</span></span>

![azure 容器实例的 azure 门户视图 CPU 和内存使用情况信息](../media/6-cpu-memory.png)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
