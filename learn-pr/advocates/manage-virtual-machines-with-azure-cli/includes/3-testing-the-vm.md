<span data-ttu-id="c3031-101">创建虚拟机时, 将为其分配可通过 Internet 访问的公共 ip 地址, 以及在 Azure 数据中心内使用的专用 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="c3031-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="c3031-102">您可以从以下`create`命令中获取两个返回的 JSON 块中的值:</span><span class="sxs-lookup"><span data-stu-id="c3031-102">You get both of those values in the returning JSON block from the `create` command:</span></span>

```json
{
   ...
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
   ...
}
```

## <a name="connecting-to-the-vm-with-ssh"></a><span data-ttu-id="c3031-103">使用 SSH 连接到 VM</span><span class="sxs-lookup"><span data-stu-id="c3031-103">Connecting to the VM with SSH</span></span>

<span data-ttu-id="c3031-104">通过公用 IP 地址, 我们可以使用安全命令行管理程序 (`ssh`) 工具快速测试 Linux VM 是否已启动并正在运行。</span><span class="sxs-lookup"><span data-stu-id="c3031-104">With the public IP address we can quickly test that the Linux VM is up and running using the Secure Shell (`ssh`) tool.</span></span> <span data-ttu-id="c3031-105">请记住, 我们将管理员名称设置`aldis`为, 因此必须指定。</span><span class="sxs-lookup"><span data-stu-id="c3031-105">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span> <span data-ttu-id="c3031-106">请务必从正在运行的实例中使用__ 公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="c3031-106">Make sure to use the public IP address from _your_ running instance.</span></span>

```azurecli
ssh <public-ip-address> -l aldis
```

> [!NOTE]
> <span data-ttu-id="c3031-107">由于在 VM 创建过程中生成了 SSH 密钥对, 因此不需要密码。</span><span class="sxs-lookup"><span data-stu-id="c3031-107">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="c3031-108">当您首次在 VM 中命令行管理程序时, 它将向您提供有关主机的真实性的提示。</span><span class="sxs-lookup"><span data-stu-id="c3031-108">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="c3031-109">这是因为我们将直接 (而不是主机名) 击中 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="c3031-109">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="c3031-110">回答 "是" 将把 IP 保存为有效的连接主机, 并允许连接继续进行。</span><span class="sxs-lookup"><span data-stu-id="c3031-110">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```output
The authenticity of host '40.83.165.85 (40.83.165.85)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '40.83.165.85' (RSA) to the list of known hosts.
```

<span data-ttu-id="c3031-111">然后, 你将看到一个远程命令行管理程序, 你可以在其中输入 Linux 命令。</span><span class="sxs-lookup"><span data-stu-id="c3031-111">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="c3031-112">在实践中尝试一些命令, 并在完成后, 注销命令行管理程序 (键入`logout`或`exit`在命令行管理程序中)。</span><span class="sxs-lookup"><span data-stu-id="c3031-112">Try a few commands as practice and when you are finished, sign out of the shell (type `logout` or `exit` in the shell).</span></span>