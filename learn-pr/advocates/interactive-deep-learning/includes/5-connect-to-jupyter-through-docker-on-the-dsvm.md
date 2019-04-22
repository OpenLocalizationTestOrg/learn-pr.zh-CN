<span data-ttu-id="f9cfb-101">现在, 你已启动并运行数据科学虚拟机, 你决定培训你的第一个深入学习模型。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-101">Now that you have your Data Science Virtual Machine up and running, you decide to train your first deep learning model.</span></span> <span data-ttu-id="f9cfb-102">您想要与服务器上的所有其他内容隔离运行实验。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-102">You want to run your experiments in isolation from everything else on your server.</span></span> <span data-ttu-id="f9cfb-103">若要执行此操作, 请在 Docker 容器中运行它们。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-103">To do that, you run them within a Docker container.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="f9cfb-104">使用 ssh 连接到 VM</span><span class="sxs-lookup"><span data-stu-id="f9cfb-104">Connect to the VM with ssh</span></span>

<span data-ttu-id="f9cfb-105">请确保你仍通过 ssh 连接到 VM。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-105">Make sure you're still connected to your VM through ssh.</span></span> <span data-ttu-id="f9cfb-106">如果不是, 只需再次运行此命令以远程返回到虚拟机。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-106">If not, just run this command again to remote back into the virtual machine.</span></span>

1. <span data-ttu-id="f9cfb-107">在 Azure 云命令行管理程序中执行以下命令以登录到 VM。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-107">Execute the following command in Azure Cloud Shell to sign into the VM.</span></span>

    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 
    
    <span data-ttu-id="f9cfb-108">将`<USERNAME>`替换为你在创建 VM 时定义的管理员帐户名称。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-108">Replace  `<USERNAME>` with the admin account name you defined when creating the VM.</span></span> <span data-ttu-id="f9cfb-109">将`<IP>`替换为您在上一个练习中保存的 VM 的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-109">Replace `<IP>` with the IP address of the VM you saved in the preceding exercise.</span></span>  

1. <span data-ttu-id="f9cfb-110">出现提示时, 请输入管理员帐户的密码以完成登录过程。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-110">When prompted, enter your password for the admin account to complete the sign-in process.</span></span>

## <a name="run-a-jupyter-notebook-server-in-a-docker-container-in-the-vm"></a><span data-ttu-id="f9cfb-111">在 VM 中的 Docker 容器中运行 Jupyter 笔记本服务器</span><span class="sxs-lookup"><span data-stu-id="f9cfb-111">Run a Jupyter Notebook server in a Docker container in the VM</span></span>

> [!NOTE]
> <span data-ttu-id="f9cfb-112">由于我们的 VM 只有管理员或 root 帐户, 因此我们必须使用来运行所有 Docker 命令作为根元素`sudo`</span><span class="sxs-lookup"><span data-stu-id="f9cfb-112">Since we only have an admin, or root, account on our VM, we have to run all Docker commands as root using `sudo`</span></span>

1. <span data-ttu-id="f9cfb-113">若要查看 VM 上存在哪些 Docker 容器, 请在命令提示符处运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-113">To see what Docker containers exist on the VM, run the following command at the command prompt.</span></span>

    ```azurecli 
    sudo docker ps
    ```

1. <span data-ttu-id="f9cfb-114">在命令提示符处运行以下命令, 为我们的实验创建一个新容器。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-114">Run the following command at the command prompt to create a new container for our experiments.</span></span>

    ```azurecli 
    sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
    'conda install jupyter matplotlib -y &&\
    curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
    ``` 

    <span data-ttu-id="f9cfb-115">此命令将运行相当长的一段时间。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-115">This command will run for quite a while.</span></span> <span data-ttu-id="f9cfb-116">因此, 尽管我们有一些时间, 我们还是讨论了该命令的功能。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-116">So, while we have some time, let's discuss what the command does.</span></span> 
    - <span data-ttu-id="f9cfb-117">`docker run`在新容器中运行命令。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-117">`docker run` runs a command in a new container.</span></span> <span data-ttu-id="f9cfb-118">正在使用的 Docker 图像为 pytorch/pytorch。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-118">The Docker image being used is pytorch/pytorch.</span></span> <span data-ttu-id="f9cfb-119">它首先根据指定的映像创建一个可写容器层, 然后使用指定的命令启动它。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-119">It first creates a writeable container layer over the specified image, and then starts it using the specified command.</span></span>
    - <span data-ttu-id="f9cfb-120">`--rm`将在容器退出后将其删除。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-120">`--rm` will remove the container once it exits.</span></span> <span data-ttu-id="f9cfb-121">如果要保持容器不变, 请删除此参数。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-121">If you want to keep the container around, drop this argument.</span></span> 
    - <span data-ttu-id="f9cfb-122">`--entrypoint 'bin/sh'`将图像的默认入口点覆盖为 Bash 命令行管理程序</span><span class="sxs-lookup"><span data-stu-id="f9cfb-122">`--entrypoint 'bin/sh'` overwrites the default entry point of the image to be the Bash shell</span></span>
    - <span data-ttu-id="f9cfb-123">`-c`定义在启动容器时要运行的命令。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-123">`-c` defines what command to run when the container starts.</span></span> <span data-ttu-id="f9cfb-124">在这种情况下, 它运行三个命令:</span><span class="sxs-lookup"><span data-stu-id="f9cfb-124">In this case, it's running three commands:</span></span>
        - <span data-ttu-id="f9cfb-125">安装 Jupyter 和 matplotlib</span><span class="sxs-lookup"><span data-stu-id="f9cfb-125">Installs Jupyter and matplotlib</span></span>
        - <span data-ttu-id="f9cfb-126">将笔记本 (cifar10_tutorial ipynb) 从 pytorch.org 复制到名为的容器中的文件`first_pytorch_classifier.ipynb`</span><span class="sxs-lookup"><span data-stu-id="f9cfb-126">Copies a notebook (cifar10_tutorial.ipynb) from pytorch.org to a file in the container called `first_pytorch_classifier.ipynb`</span></span>
        - <span data-ttu-id="f9cfb-127">以与前面的练习相同的方式在容器中启动笔记本服务器。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-127">Starts the notebook server in the container in the same way as the preceding exercise.</span></span>  <span data-ttu-id="f9cfb-128">未启动任何浏览器, 允许通过 root 访问笔记本并侦听所有端口。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-128">No browser is started, allow the notebook to be accessed by root and listen on all ports.</span></span> 
    
    <span data-ttu-id="f9cfb-129">笔记本服务器侦听该容器的所有端口。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-129">The notebook server listens on all ports for that container.</span></span> <span data-ttu-id="f9cfb-130">但是, 流量将如何来自容器外部？</span><span class="sxs-lookup"><span data-stu-id="f9cfb-130">But, how will traffic come from outside the container?</span></span> <span data-ttu-id="f9cfb-131">参数`-p 8888:8888`将容器的`8888`端口绑定到主机上的 TCP 端口8888。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-131">The `-p 8888:8888` argument binds port `8888` of the container to TCP port 8888 on the host machine.</span></span> <span data-ttu-id="f9cfb-132">因此, 通过端口8888传入 VM 的流量将由容器选取。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-132">So, traffic coming to the VM over port 8888 will be picked up by the container.</span></span> 

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a><span data-ttu-id="f9cfb-133">从远程浏览器连接到 Jupyter 笔记本服务器</span><span class="sxs-lookup"><span data-stu-id="f9cfb-133">Connect to the Jupyter Notebook server from a remote browser</span></span> 

<span data-ttu-id="f9cfb-134">在容器中运行 Jupyter 笔记本后, 您将看到类似于以下消息的消息。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-134">Once the Jupyter notebook is running in the container, you'll  see a message similar to the following message.</span></span> 

> <span data-ttu-id="f9cfb-135">*首次连接时, 将此 URL 复制/粘贴到浏览器中, 以使用令牌登录: http://(5b8783e7911d 或 127.0.0.1): 8888/?token = {sometoken}*</span><span class="sxs-lookup"><span data-stu-id="f9cfb-135">*Copy/paste this URL into your browser when you connect for the first time, to login with a token: http://(5b8783e7911d or 127.0.0.1):8888/?token={sometoken}*</span></span>

1. <span data-ttu-id="f9cfb-136">将 URL 的**http://(5b8783e7911d 或 127.0.0.1)** 部分替换为完全限定的域名 (FQDN) 或 VM 的 IP 地址, 并导航到浏览器的新选项卡中的地址。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-136">Replace the **http://(5b8783e7911d or 127.0.0.1)** part of the URL with the Fully Qualified Domain Name (FQDN) or the IP address of the VM and navigate to the address in a new tab of your browser.</span></span>

    ![<span data-ttu-id="f9cfb-137">显示 Jupyter 笔记本仪表板的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-137">Screenshot showing Jupyter Notebooks dashboard.</span></span> ](../media/notebook-in-docker.png)

    > [!TIP]
    > <span data-ttu-id="f9cfb-138">您可以使用以下命令获取 VM 的 FQDN 和 IP 地址:</span><span class="sxs-lookup"><span data-stu-id="f9cfb-138">You can get the FQDN and IP address of your VM with the following command:</span></span>
    > 
    > `az vm show -d --name <HOSTNAME> --resource-group <rgn>[sandbox resource group name]</rgn> --output table`
    >
    > <span data-ttu-id="f9cfb-139">请务必将`<HOSTNAME>`替换为你为 VM 提供的名称。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-139">Remember to replace `<HOSTNAME>` with the name you gave your VM.</span></span> 
    
    <span data-ttu-id="f9cfb-140">这次我们只会看到单个笔记本。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-140">This time we only see a single notebook.</span></span> <span data-ttu-id="f9cfb-141">这是因为我们位于容器中, 仅复制到此笔记本中。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-141">That's because we're in a container and only copied down this notebook.</span></span> <span data-ttu-id="f9cfb-142">在下一个练习中, 我们将试用此笔记本。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-142">In the next exercise, we'll experiment with this notebook.</span></span> 
    
    > [!TIP]
    > <span data-ttu-id="f9cfb-143">不要立即关闭笔记本服务器。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-143">Don't shut down the notebook server just yet.</span></span> <span data-ttu-id="f9cfb-144">我们将在下一个`first_pytorch_classifier.ipynb`练习中查看笔记本。</span><span class="sxs-lookup"><span data-stu-id="f9cfb-144">We'll look at the `first_pytorch_classifier.ipynb` notebook in the next exercise.</span></span>