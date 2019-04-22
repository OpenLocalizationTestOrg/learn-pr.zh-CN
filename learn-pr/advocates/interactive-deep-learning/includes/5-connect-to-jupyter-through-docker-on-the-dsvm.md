现在, 你已启动并运行数据科学虚拟机, 你决定培训你的第一个深入学习模型。 您想要与服务器上的所有其他内容隔离运行实验。 若要执行此操作, 请在 Docker 容器中运行它们。

## <a name="connect-to-the-vm-with-ssh"></a>使用 ssh 连接到 VM

请确保你仍通过 ssh 连接到 VM。 如果不是, 只需再次运行此命令以远程返回到虚拟机。

1. 在 Azure 云命令行管理程序中执行以下命令以登录到 VM。

    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 
    
    将`<USERNAME>`替换为你在创建 VM 时定义的管理员帐户名称。 将`<IP>`替换为您在上一个练习中保存的 VM 的 IP 地址。  

1. 出现提示时, 请输入管理员帐户的密码以完成登录过程。

## <a name="run-a-jupyter-notebook-server-in-a-docker-container-in-the-vm"></a>在 VM 中的 Docker 容器中运行 Jupyter 笔记本服务器

> [!NOTE]
> 由于我们的 VM 只有管理员或 root 帐户, 因此我们必须使用来运行所有 Docker 命令作为根元素`sudo`

1. 若要查看 VM 上存在哪些 Docker 容器, 请在命令提示符处运行以下命令。

    ```azurecli 
    sudo docker ps
    ```

1. 在命令提示符处运行以下命令, 为我们的实验创建一个新容器。

    ```azurecli 
    sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
    'conda install jupyter matplotlib -y && pip install torchvision &&\
    curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
    ``` 

    此命令将运行相当长的一段时间。 因此, 尽管我们有一些时间, 我们还是讨论了该命令的功能。 
    - `docker run`在新容器中运行命令。 正在使用的 Docker 图像为 pytorch/pytorch。 它首先根据指定的映像创建一个可写容器层, 然后使用指定的命令启动它。
    - `--rm`将在容器退出后将其删除。 如果要保持容器不变, 请删除此参数。 
    - `--entrypoint 'bin/sh'`将图像的默认入口点覆盖为 Bash 命令行管理程序
    - `-c`定义在启动容器时要运行的命令。 在这种情况下, 它运行三个命令:
        - 安装 Jupyter 和 matplotlib
        - 将笔记本 (cifar10_tutorial ipynb) 从 pytorch.org 复制到名为的容器中的文件`first_pytorch_classifier.ipynb`
        - 以与前面的练习相同的方式在容器中启动笔记本服务器。  未启动任何浏览器, 允许通过 root 访问笔记本并侦听所有端口。 
    
    笔记本服务器侦听该容器的所有端口。 但是, 流量将如何来自容器外部？ 参数`-p 8888:8888`将容器的`8888`端口绑定到主机上的 TCP 端口8888。 因此, 通过端口8888传入 VM 的流量将由容器选取。 

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a>从远程浏览器连接到 Jupyter 笔记本服务器 

在容器中运行 Jupyter 笔记本后, 您将看到类似于以下消息的消息。 

> *首次连接时, 将此 URL 复制/粘贴到浏览器中, 以使用令牌登录: http://(5b8783e7911d 或 127.0.0.1): 8888/?token = {sometoken}*

1. 将 URL 的**http://(5b8783e7911d 或 127.0.0.1)** 部分替换为完全限定的域名 (FQDN) 或 VM 的 IP 地址, 并导航到浏览器的新选项卡中的地址。

    ![显示 Jupyter 笔记本仪表板的屏幕截图。 ](../media/notebook-in-docker.png)

    > [!TIP]
    > 您可以使用以下命令获取 VM 的 FQDN 和 IP 地址:
    > 
    > `az vm show -d --name <HOSTNAME> --resource-group <rgn>[sandbox resource group name]</rgn> --output table`
    >
    > 请务必将`<HOSTNAME>`替换为你为 VM 提供的名称。 
    
    这次我们只会看到单个笔记本。 这是因为我们位于容器中, 仅复制到此笔记本中。 在下一个练习中, 我们将试用此笔记本。 
    
    > [!TIP]
    > 不要立即关闭笔记本服务器。 我们将在下一个`first_pytorch_classifier.ipynb`练习中查看笔记本。