<span data-ttu-id="13e37-101">在 Azure 容器实例中部署容器的方便性和速度非常适合于执行仅运行一次的任务, 如图像呈现或生成和测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="13e37-101">The ease and speed of deploying containers in Azure Container Instances makes it a great fit for executing run-once tasks like image rendering or building and testing applications.</span></span>

<span data-ttu-id="13e37-102">使用可配置的重新启动策略, 您可以指定在其进程完成时停止容器。</span><span class="sxs-lookup"><span data-stu-id="13e37-102">With a configurable restart policy, you can specify that your containers are stopped when their processes have completed.</span></span> <span data-ttu-id="13e37-103">由于容器实例由第二个实例计费, 因此仅对执行任务的容器运行时所使用的计算资源进行计费。</span><span class="sxs-lookup"><span data-stu-id="13e37-103">Because container instances are billed by the second, you're charged only for the compute resources used while the container executing your task is running.</span></span>

## <a name="what-are-container-restart-policies"></a><span data-ttu-id="13e37-104">什么是容器重启策略？</span><span class="sxs-lookup"><span data-stu-id="13e37-104">What are container restart policies?</span></span>

<span data-ttu-id="13e37-105">Azure 容器实例具有三个重新启动策略选项:</span><span class="sxs-lookup"><span data-stu-id="13e37-105">Azure Container Instances has three restart-policy options:</span></span>

| <span data-ttu-id="13e37-106">重新启动策略</span><span class="sxs-lookup"><span data-stu-id="13e37-106">Restart policy</span></span>   | <span data-ttu-id="13e37-107">说明</span><span class="sxs-lookup"><span data-stu-id="13e37-107">Description</span></span> |
| ---------------- | :---------- |
| <span data-ttu-id="13e37-108">**都**</span><span class="sxs-lookup"><span data-stu-id="13e37-108">**Always**</span></span> | <span data-ttu-id="13e37-109">容器组中的容器始终会重新启动。</span><span class="sxs-lookup"><span data-stu-id="13e37-109">Containers in the container group are always restarted.</span></span> <span data-ttu-id="13e37-110">此策略对长时间运行的任务 (如 web 服务器) 有意义。</span><span class="sxs-lookup"><span data-stu-id="13e37-110">This policy makes sense for long-running tasks such as a web server.</span></span> <span data-ttu-id="13e37-111">这是在创建容器时未指定重新启动策略时应用的**默认**设置。</span><span class="sxs-lookup"><span data-stu-id="13e37-111">This is the **default** setting applied when no restart policy is specified at container creation.</span></span> |
| <span data-ttu-id="13e37-112">**永不**</span><span class="sxs-lookup"><span data-stu-id="13e37-112">**Never**</span></span> | <span data-ttu-id="13e37-113">容器组中的容器永远不会重新启动。</span><span class="sxs-lookup"><span data-stu-id="13e37-113">Containers in the container group are never restarted.</span></span> <span data-ttu-id="13e37-114">容器仅运行一次。</span><span class="sxs-lookup"><span data-stu-id="13e37-114">The containers run one time only.</span></span> |
| <span data-ttu-id="13e37-115">**OnFailure**</span><span class="sxs-lookup"><span data-stu-id="13e37-115">**OnFailure**</span></span> | <span data-ttu-id="13e37-116">只有在容器中执行的进程失败时 (当它以非零退出代码结束时), 才会重新启动容器组中的容器。</span><span class="sxs-lookup"><span data-stu-id="13e37-116">Containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code).</span></span> <span data-ttu-id="13e37-117">至少运行一次容器。</span><span class="sxs-lookup"><span data-stu-id="13e37-117">The containers are run at least once.</span></span> <span data-ttu-id="13e37-118">此策略适用于运行短生存期任务的容器。</span><span class="sxs-lookup"><span data-stu-id="13e37-118">This policy works well for containers that run short-lived tasks.</span></span> |

## <a name="run-a-container-to-completion"></a><span data-ttu-id="13e37-119">运行要完成的容器</span><span class="sxs-lookup"><span data-stu-id="13e37-119">Run a container to completion</span></span>

<span data-ttu-id="13e37-120">若要查看 "重新启动策略" 操作, 请从**microsoft/aci-wordcount** Docker 图像创建一个容器实例, 并指定**OnFailure**重新启动策略。</span><span class="sxs-lookup"><span data-stu-id="13e37-120">To see the restart policy in action, create a container instance from the **microsoft/aci-wordcount** Docker image and specify the **OnFailure** restart policy.</span></span> <span data-ttu-id="13e37-121">此容器运行一个用于分析 Shakespeare 的 Hamlet 文本的 Python 脚本, 将10个最常用的词写入标准输出, 然后退出。</span><span class="sxs-lookup"><span data-stu-id="13e37-121">This container runs a Python script that analyzes the text of Shakespeare's Hamlet, writes the 10 most common words to standard output, and then exits.</span></span>

1. <span data-ttu-id="13e37-122">运行此`az container create`命令以启动容器。</span><span class="sxs-lookup"><span data-stu-id="13e37-122">Run this `az container create` command to start the container.</span></span>

    ```azurecli
    az container create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer-restart-demo \
      --image microsoft/aci-wordcount:latest \
      --restart-policy OnFailure \
      --location eastus
    ```

    <span data-ttu-id="13e37-123">Azure 容器实例启动容器, 然后在其进程 (在此示例中为脚本) 退出时将其停止。</span><span class="sxs-lookup"><span data-stu-id="13e37-123">Azure Container Instances starts the container and then stops it when its process (a script, in this case) exits.</span></span> <span data-ttu-id="13e37-124">当 Azure 容器实例停止其重新启动策略**从不**或**OnFailure**的容器时, 容器的状态设置为 "已**终止**"。</span><span class="sxs-lookup"><span data-stu-id="13e37-124">When Azure Container Instances stops a container whose restart policy is **Never** or **OnFailure**, the container's status is set to **Terminated**.</span></span>

1. <span data-ttu-id="13e37-125">运行`az container show`以检查容器的状态。</span><span class="sxs-lookup"><span data-stu-id="13e37-125">Run `az container show` to check your container's status.</span></span>

    ```azurecli
    az container show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer-restart-demo \
      --query containers[0].instanceView.currentState.state
    ```

    <span data-ttu-id="13e37-126">重复命令, 直到它达到**终止**状态。</span><span class="sxs-lookup"><span data-stu-id="13e37-126">Repeat the command until it reaches the **Terminated** status.</span></span>

1. <span data-ttu-id="13e37-127">查看容器的日志以检查输出。</span><span class="sxs-lookup"><span data-stu-id="13e37-127">View the container's logs to examine the output.</span></span> <span data-ttu-id="13e37-128">若要执行此操作`az container logs` , 请运行, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="13e37-128">To do so, run `az container logs` like this.</span></span>

    ```azurecli
    az container logs \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name mycontainer-restart-demo
    ```

    <span data-ttu-id="13e37-129">你会看到这一点。</span><span class="sxs-lookup"><span data-stu-id="13e37-129">You see this.</span></span>

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