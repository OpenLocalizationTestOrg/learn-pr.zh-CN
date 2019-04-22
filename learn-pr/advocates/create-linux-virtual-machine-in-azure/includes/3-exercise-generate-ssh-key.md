在 Azure 中创建 Linux 虚拟机之前, 我们将需要考虑远程访问。 我们希望能够登录到 Linux web 服务器来配置软件并执行维护。 管理 Azure 中托管的 Linux vm 的默认方法是 SSH。

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-ssh"></a>什么是 SSH？

安全命令行管理程序 (SSH) 是一种加密连接协议, 允许通过不安全的连接进行安全登录。 SSH 允许您使用网络连接从远程位置连接到终端命令行管理程序。

有两种方法可用于对 SSH 连接进行身份验证:**用户名和密码**或**ssh 密钥对**。

> [!TIP]
> 虽然 ssh 提供加密连接, 但使用 ssh 连接的密码会使 VM 容易受到密码的强力攻击。 使用 SSH 连接到 Linux VM 的更安全和首选方法是公钥-私钥对 (也称为 SSH 密钥)。

使用 SSH 密钥对, 可以在没有密码的情况下登录到基于 Linux 的 Azure 虚拟机。 如果您仅计划从少数计算机登录到 VM, 这是一种更安全的方法。 如果您需要能够从各种位置访问 Linux VM, 则用户名和密码组合可能是更好的方法。 SSH 密钥对分为两个部分: 公钥和私钥。

* 公钥放置在您的 Linux VM 或任何其他要用于公钥加密的服务上。 这可与任何人共享。

* 私钥是你在建立 SSH 连接时向你的 Linux VM 验证你的身份所使用的**密钥**。 请考虑此机密信息, 并像对待密码或任何其他隐私数据一样保护这一点。

您可以使用相同的单一公用密钥对来访问多个 Azure 虚拟机和服务。

## <a name="create-the-ssh-key-pair"></a>创建 SSH 密钥对

在 Linux、Windows 10 和 MacOS 上, 您可以使用内置`ssh-keygen`命令生成 SSH 公钥和私钥文件。

> [!TIP]
> Windows 10 包括包含**秋季创建者更新**的 SSH 客户端。 早期版本的 Windows 需要额外的软件来使用 SSH;[有关完整详细信息, 请查看文档](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows)。 此外, 还可以安装适用于 Windows 的 Linux 子系统并获取相同的功能。

> [!NOTE]
> 我们将使用 azure 云命令行管理程序, 它会将生成的密钥存储在你的专用存储帐户中的 Azure 中。 如果愿意, 也可以直接在本地命令行管理程序中键入这些命令。 如果采用此方法, 您将需要在整个模块中调整说明, 以反映本地会话。

[!include[](../../../includes/azure-sandbox-activate.md)]

下面是为 Azure VM 生成密钥对所需的最少命令。 这将创建 ssh 协议 2 (ssh-2) RSA 公用-私有密钥对。 最小长度为 2048, 但对于此学习模块, 我们将使用4096。

在云命令行管理程序中键入以下命令:

```bash
ssh-keygen -t rsa -b 4096
```

该工具将提示输入文件名和可选密码。 在本练习中, 只需采用默认值即可。 它将创建两个文件`id_rsa` : `id_rsa.pub`和在`~/.ssh`目录中。 文件将被覆盖 (如果文件存在)。 您可以使用多个选项来提供文件名或密码短语以避免出现提示。

### <a name="private-key-passphrase"></a>私钥密码

你可以选择在生成私钥时提供密码。 这是使用密钥时必须输入的密码。 此密码用于访问专用 SSH 密钥文件, 而不是用户帐户密码。

当您将密码短语添加到 SSH 密钥时, 它会使用128位 AES 加密私钥, 以便私钥在没有解密密码的情况下毫无用处。

> [!IMPORTANT]
> **强烈**建议您添加密码。 如果攻击者 stole 您的私钥, 并且该密钥没有密码, 则他们将能够使用该私钥登录到具有相应公钥的任何服务器。 如果密码保护私钥, 则该攻击者不能使用该密钥。 这为 Azure 上的基础结构提供了额外的安全层。

## <a name="use-the-ssh-key-pair-with-an-azure-linux-vm"></a>将 SSH 密钥对与 Azure Linux VM 结合使用

生成密钥对后, 可以在 Azure 中将其与 Linux VM 一起使用。 您可以在创建 vm 期间提供公钥, 也可以在创建虚拟机之后添加该公钥。

您可以使用以下命令查看 Azure 云命令行管理程序中文件的内容:

```bash
cat ~/.ssh/id_rsa.pub
```

它将是一个单独的行, 看起来类似于以下内容:

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

复制此值, 以便您可以在下一个练习中使用它。

### <a name="use-the-ssh-key-when-creating-a-linux-vm"></a>创建 Linux VM 时使用 SSH 密钥

若要在创建新的 Linux VM 时应用 SSH 密钥, 您需要复制公钥的内容, 并将其提供给 azure 门户,_或_将公钥文件提供给 azure CLI 或 azure PowerShell 命令。 我们将在创建 Linux VM 时使用此方法。

### <a name="add-the-ssh-key-to-an-existing-linux-vm"></a>将 SSH 密钥添加到现有 Linux VM

如果已创建 VM, 则可以使用`ssh-copy-id`命令将公钥安装到 Linux 虚拟机上。 为 SSH 授权密钥后, 它会在不使用密码的情况下授予对服务器的访问权限, 但是, 如果您设置一个, 仍会提示您输入密钥的密码。

例如, 如果我们有一个名为*myserver*的 Linux VM 与用户*azureuser*, 我们可以使用以下命令来安装公钥文件, 并使用密钥向用户授权:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```

现在我们已拥有公钥, 我们将切换到 Azure 门户并创建 Linux VM。
