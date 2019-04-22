创建虚拟机时, 将为其分配可通过 Internet 访问的公共 ip 地址, 以及在 Azure 数据中心内使用的专用 ip 地址。 您可以从以下`create`命令中获取两个返回的 JSON 块中的值:

```json
{
   ...
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
   ...
}
```

## <a name="connecting-to-the-vm-with-ssh"></a>使用 SSH 连接到 VM

通过公用 IP 地址, 我们可以使用安全命令行管理程序 (`ssh`) 工具快速测试 Linux VM 是否已启动并正在运行。 请记住, 我们将管理员名称设置`aldis`为, 因此必须指定。 请务必从正在运行的实例中使用__ 公共 IP 地址。

```azurecli
ssh <public-ip-address> -l aldis
```

> [!NOTE]
> 由于在 VM 创建过程中生成了 SSH 密钥对, 因此不需要密码。 当您首次在 VM 中命令行管理程序时, 它将向您提供有关主机的真实性的提示。 
> 
> 这是因为我们将直接 (而不是主机名) 击中 IP 地址。 回答 "是" 将把 IP 保存为有效的连接主机, 并允许连接继续进行。

```output
The authenticity of host '40.83.165.85 (40.83.165.85)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '40.83.165.85' (RSA) to the list of known hosts.
```

然后, 你将看到一个远程命令行管理程序, 你可以在其中输入 Linux 命令。

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

在实践中尝试一些命令, 并在完成后, 注销命令行管理程序 (键入`logout`或`exit`在命令行管理程序中)。