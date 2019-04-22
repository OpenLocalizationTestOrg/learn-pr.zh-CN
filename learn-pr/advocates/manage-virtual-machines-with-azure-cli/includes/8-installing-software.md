<span data-ttu-id="9881f-101">我们要在虚拟机上尝试的最后一件事是安装 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9881f-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="9881f-102">要安装的最简单的程序包之一`nginx`是。</span><span class="sxs-lookup"><span data-stu-id="9881f-102">One of the easiest packages to install is `nginx`.</span></span>

## <a name="install-nginx-web-server"></a><span data-ttu-id="9881f-103">安装 NGINX web 服务器</span><span class="sxs-lookup"><span data-stu-id="9881f-103">Install NGINX web server</span></span>

1. <span data-ttu-id="9881f-104">查找 Linux 虚拟机的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="9881f-104">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="9881f-105">请记住, 可以使用`vm list-ip-addresses`命令进行查找。</span><span class="sxs-lookup"><span data-stu-id="9881f-105">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

1. <span data-ttu-id="9881f-106">接下来, 打开`ssh`到计算机的连接, 如我们对其进行测试时执行的操作。</span><span class="sxs-lookup"><span data-stu-id="9881f-106">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="9881f-107">请记住, 你将需要传入管理员名称 ("**aldis**")。</span><span class="sxs-lookup"><span data-stu-id="9881f-107">Remember you will need to pass in the admin name ("**aldis**").</span></span>

1. <span data-ttu-id="9881f-108">在提供的命令行管理程序中, 执行以下命令`nginx`以安装 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9881f-108">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```bash
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. <span data-ttu-id="9881f-109">退出安全命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="9881f-109">Exit the Secure Shell.</span></span>

```bash
exit
```

## <a name="retrieve-our-default-page"></a><span data-ttu-id="9881f-110">检索默认页面</span><span class="sxs-lookup"><span data-stu-id="9881f-110">Retrieve our default page</span></span>

1. <span data-ttu-id="9881f-111">在 Azure 云命令行管理`curl`程序中, 使用从 Linux web 服务器读取默认页面。</span><span class="sxs-lookup"><span data-stu-id="9881f-111">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="9881f-112">或者, 您可以打开一个新的浏览器选项卡并浏览到公用 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="9881f-112">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 40.83.165.85
```

<span data-ttu-id="9881f-113">它将会失败, 因为 Linux 虚拟机不会通过内置`http`防火墙公开端口 80 ()。</span><span class="sxs-lookup"><span data-stu-id="9881f-113">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="9881f-114">幸运的是, Azure CLI 具有如下所示的`vm open-port`命令:。</span><span class="sxs-lookup"><span data-stu-id="9881f-114">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

1. <span data-ttu-id="9881f-115">在云命令行管理程序中键入以下命令以打开端口 80:</span><span class="sxs-lookup"><span data-stu-id="9881f-115">Type the following into Cloud Shell to open port 80:</span></span>

```azurecli
az vm open-port --port 80 --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM
```

<span data-ttu-id="9881f-116">将需要一段时间来添加网络规则并通过防火墙打开端口。</span><span class="sxs-lookup"><span data-stu-id="9881f-116">It will take a moment to add the network rule and open the port through the firewall.</span></span> <span data-ttu-id="9881f-117">再`curl`试一次。</span><span class="sxs-lookup"><span data-stu-id="9881f-117">Try `curl` again.</span></span> <span data-ttu-id="9881f-118">这次它应返回数据。</span><span class="sxs-lookup"><span data-stu-id="9881f-118">This time it should return data.</span></span> <span data-ttu-id="9881f-119">您也可以在浏览器中查看页面。</span><span class="sxs-lookup"><span data-stu-id="9881f-119">You can see the page in a browser as well.</span></span>

```output
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx on Debian!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx on Debian!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working on Debian. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a></p>

<p>
      Please use the <tt>reportbug</tt> tool to report bugs in the
      nginx package with Debian. However, check <a
      href="http://bugs.debian.org/cgi-bin/pkgreport.cgi?ordering=normal;archive=0;src=nginx;repeatmerged=0">existing
      bug reports</a> before reporting a new bug.
</p>

<p><em>Thank you for using debian and nginx.</em></p>


</body>
</html>
```
