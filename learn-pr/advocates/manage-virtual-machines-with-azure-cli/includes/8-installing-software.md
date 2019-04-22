我们要在虚拟机上尝试的最后一件事是安装 web 服务器。 要安装的最简单的程序包之一`nginx`是。

## <a name="install-nginx-web-server"></a>安装 NGINX web 服务器

1. 查找 Linux 虚拟机的公共 IP 地址。 请记住, 可以使用`vm list-ip-addresses`命令进行查找。

1. 接下来, 打开`ssh`到计算机的连接, 如我们对其进行测试时执行的操作。 请记住, 你将需要传入管理员名称 ("**aldis**")。

1. 在提供的命令行管理程序中, 执行以下命令`nginx`以安装 web 服务器。

```bash
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. 退出安全命令行管理程序。

```bash
exit
```

## <a name="retrieve-our-default-page"></a>检索默认页面

1. 在 Azure 云命令行管理`curl`程序中, 使用从 Linux web 服务器读取默认页面。 或者, 您可以打开一个新的浏览器选项卡并浏览到公用 IP 地址。

```azurecli
curl 40.83.165.85
```

它将会失败, 因为 Linux 虚拟机不会通过内置`http`防火墙公开端口 80 ()。 幸运的是, Azure CLI 具有如下所示的`vm open-port`命令:。 

1. 在云命令行管理程序中键入以下命令以打开端口 80:

```azurecli
az vm open-port --port 80 --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM
```

将需要一段时间来添加网络规则并通过防火墙打开端口。 再`curl`试一次。 这次它应返回数据。 您也可以在浏览器中查看页面。

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
