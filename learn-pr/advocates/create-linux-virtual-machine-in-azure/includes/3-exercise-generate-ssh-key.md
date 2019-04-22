<span data-ttu-id="fefcc-101">在 Azure 中创建 Linux 虚拟机之前, 我们将需要考虑远程访问。</span><span class="sxs-lookup"><span data-stu-id="fefcc-101">Before we can create a Linux virtual machine in Azure, we will need to think about remote access.</span></span> <span data-ttu-id="fefcc-102">我们希望能够登录到 Linux web 服务器来配置软件并执行维护。</span><span class="sxs-lookup"><span data-stu-id="fefcc-102">We want to be able to sign in to our Linux web server to configure the software and perform maintenance.</span></span> <span data-ttu-id="fefcc-103">管理 Azure 中托管的 Linux vm 的默认方法是 SSH。</span><span class="sxs-lookup"><span data-stu-id="fefcc-103">The default approach to administering Linux VMs hosted in Azure is SSH.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-ssh"></a><span data-ttu-id="fefcc-104">什么是 SSH？</span><span class="sxs-lookup"><span data-stu-id="fefcc-104">What is SSH?</span></span>

<span data-ttu-id="fefcc-105">安全命令行管理程序 (SSH) 是一种加密连接协议, 允许通过不安全的连接进行安全登录。</span><span class="sxs-lookup"><span data-stu-id="fefcc-105">Secure Shell (SSH) is an encrypted connection protocol that allows secure sign-ins over unsecured connections.</span></span> <span data-ttu-id="fefcc-106">SSH 允许您使用网络连接从远程位置连接到终端命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="fefcc-106">SSH allows you to connect to a terminal shell from a remote location using a network connection.</span></span>

<span data-ttu-id="fefcc-107">有两种方法可用于对 SSH 连接进行身份验证:**用户名和密码**或**ssh 密钥对**。</span><span class="sxs-lookup"><span data-stu-id="fefcc-107">There are two approaches we can use to authenticate an SSH connection: **username and password**, or an **SSH key pair**.</span></span>

> [!TIP]
> <span data-ttu-id="fefcc-108">虽然 ssh 提供加密连接, 但使用 ssh 连接的密码会使 VM 容易受到密码的强力攻击。</span><span class="sxs-lookup"><span data-stu-id="fefcc-108">Although SSH provides an encrypted connection, using passwords with SSH connections leaves the VM vulnerable to brute-force attacks of passwords.</span></span> <span data-ttu-id="fefcc-109">使用 SSH 连接到 Linux VM 的更安全和首选方法是公钥-私钥对 (也称为 SSH 密钥)。</span><span class="sxs-lookup"><span data-stu-id="fefcc-109">A more secure and preferred method of connecting to a Linux VM with SSH is a public-private key pair, also known as SSH keys.</span></span>

<span data-ttu-id="fefcc-110">使用 SSH 密钥对, 可以在没有密码的情况下登录到基于 Linux 的 Azure 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="fefcc-110">With an SSH key pair, you can sign in to Linux-based Azure virtual machines without a password.</span></span> <span data-ttu-id="fefcc-111">如果您仅计划从少数计算机登录到 VM, 这是一种更安全的方法。</span><span class="sxs-lookup"><span data-stu-id="fefcc-111">This is a more secure approach if you only plan to sign in to the VM from a few computers.</span></span> <span data-ttu-id="fefcc-112">如果您需要能够从各种位置访问 Linux VM, 则用户名和密码组合可能是更好的方法。</span><span class="sxs-lookup"><span data-stu-id="fefcc-112">If you need to be able to access the Linux VM from a variety of locations, a username and password combination might be a better approach.</span></span> <span data-ttu-id="fefcc-113">SSH 密钥对分为两个部分: 公钥和私钥。</span><span class="sxs-lookup"><span data-stu-id="fefcc-113">There are two parts to an SSH key pair: a public key and a private key.</span></span>

* <span data-ttu-id="fefcc-114">公钥放置在您的 Linux VM 或任何其他要用于公钥加密的服务上。</span><span class="sxs-lookup"><span data-stu-id="fefcc-114">The public key is placed on your Linux VM or any other service that you wish to use with public-key cryptography.</span></span> <span data-ttu-id="fefcc-115">这可与任何人共享。</span><span class="sxs-lookup"><span data-stu-id="fefcc-115">This can be shared with anyone.</span></span>

* <span data-ttu-id="fefcc-116">私钥是你在建立 SSH 连接时向你的 Linux VM 验证你的身份所使用的**密钥**。</span><span class="sxs-lookup"><span data-stu-id="fefcc-116">The **private key** is what you present to verify your identity to your Linux VM when you make an SSH connection.</span></span> <span data-ttu-id="fefcc-117">请考虑此机密信息, 并像对待密码或任何其他隐私数据一样保护这一点。</span><span class="sxs-lookup"><span data-stu-id="fefcc-117">Consider this confidential information and protect this like you would a password or any other private data.</span></span>

<span data-ttu-id="fefcc-118">您可以使用相同的单一公用密钥对来访问多个 Azure 虚拟机和服务。</span><span class="sxs-lookup"><span data-stu-id="fefcc-118">You can use the same single public-private key pair to access multiple Azure VMs and services.</span></span>

## <a name="create-the-ssh-key-pair"></a><span data-ttu-id="fefcc-119">创建 SSH 密钥对</span><span class="sxs-lookup"><span data-stu-id="fefcc-119">Create the SSH key pair</span></span>

<span data-ttu-id="fefcc-120">在 Linux、Windows 10 和 MacOS 上, 您可以使用内置`ssh-keygen`命令生成 SSH 公钥和私钥文件。</span><span class="sxs-lookup"><span data-stu-id="fefcc-120">On Linux, Windows 10, and MacOS, you can use the built-in `ssh-keygen` command to generate the SSH public and private key files.</span></span>

> [!TIP]
> <span data-ttu-id="fefcc-121">Windows 10 包括包含**秋季创建者更新**的 SSH 客户端。</span><span class="sxs-lookup"><span data-stu-id="fefcc-121">Windows 10 includes an SSH client with the **Fall Creators Update**.</span></span> <span data-ttu-id="fefcc-122">早期版本的 Windows 需要额外的软件来使用 SSH;[有关完整详细信息, 请查看文档](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows)。</span><span class="sxs-lookup"><span data-stu-id="fefcc-122">Earlier versions of Windows require additional software to use SSH; [check the documentation for full details](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows).</span></span> <span data-ttu-id="fefcc-123">此外, 还可以安装适用于 Windows 的 Linux 子系统并获取相同的功能。</span><span class="sxs-lookup"><span data-stu-id="fefcc-123">Alternatively, you can install the Linux subsystem for Windows and get the same functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="fefcc-124">我们将使用 azure 云命令行管理程序, 它会将生成的密钥存储在你的专用存储帐户中的 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="fefcc-124">We will use Azure Cloud Shell, which will store the generated keys in Azure in your private storage account.</span></span> <span data-ttu-id="fefcc-125">如果愿意, 也可以直接在本地命令行管理程序中键入这些命令。</span><span class="sxs-lookup"><span data-stu-id="fefcc-125">You can also type these commands directly into your local shell if you prefer.</span></span> <span data-ttu-id="fefcc-126">如果采用此方法, 您将需要在整个模块中调整说明, 以反映本地会话。</span><span class="sxs-lookup"><span data-stu-id="fefcc-126">You will need to adjust the instructions throughout this module to reflect a local session if you take this approach.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="fefcc-127">下面是为 Azure VM 生成密钥对所需的最少命令。</span><span class="sxs-lookup"><span data-stu-id="fefcc-127">Here is the minimum command necessary to generate the key pair for an Azure VM.</span></span> <span data-ttu-id="fefcc-128">这将创建 ssh 协议 2 (ssh-2) RSA 公用-私有密钥对。</span><span class="sxs-lookup"><span data-stu-id="fefcc-128">This will create an SSH protocol 2 (SSH-2) RSA public-private key pair.</span></span> <span data-ttu-id="fefcc-129">最小长度为 2048, 但对于此学习模块, 我们将使用4096。</span><span class="sxs-lookup"><span data-stu-id="fefcc-129">The minimum length is 2048, but for the sake of this learning module we will use 4096.</span></span>

<span data-ttu-id="fefcc-130">在云命令行管理程序中键入以下命令:</span><span class="sxs-lookup"><span data-stu-id="fefcc-130">Type this command into Cloud Shell:</span></span>

```bash
ssh-keygen -t rsa -b 4096
```

<span data-ttu-id="fefcc-131">该工具将提示输入文件名和可选密码。</span><span class="sxs-lookup"><span data-stu-id="fefcc-131">The tool will prompt for file names and an optional passphrase.</span></span> <span data-ttu-id="fefcc-132">在本练习中, 只需采用默认值即可。</span><span class="sxs-lookup"><span data-stu-id="fefcc-132">For this exercise, just take the defaults.</span></span> <span data-ttu-id="fefcc-133">它将创建两个文件`id_rsa` : `id_rsa.pub`和在`~/.ssh`目录中。</span><span class="sxs-lookup"><span data-stu-id="fefcc-133">It will create two files: `id_rsa` and `id_rsa.pub` in the `~/.ssh` directory.</span></span> <span data-ttu-id="fefcc-134">文件将被覆盖 (如果文件存在)。</span><span class="sxs-lookup"><span data-stu-id="fefcc-134">The files will be overwritten if they exist.</span></span> <span data-ttu-id="fefcc-135">您可以使用多个选项来提供文件名或密码短语以避免出现提示。</span><span class="sxs-lookup"><span data-stu-id="fefcc-135">There are various options you can use to provide the file name or a passphrase to avoid the prompt.</span></span>

### <a name="private-key-passphrase"></a><span data-ttu-id="fefcc-136">私钥密码</span><span class="sxs-lookup"><span data-stu-id="fefcc-136">Private key passphrase</span></span>

<span data-ttu-id="fefcc-137">你可以选择在生成私钥时提供密码。</span><span class="sxs-lookup"><span data-stu-id="fefcc-137">You can optionally provide a passphrase while generating your private key.</span></span> <span data-ttu-id="fefcc-138">这是使用密钥时必须输入的密码。</span><span class="sxs-lookup"><span data-stu-id="fefcc-138">This is a password you must enter when you use the key.</span></span> <span data-ttu-id="fefcc-139">此密码用于访问专用 SSH 密钥文件, 而不是用户帐户密码。</span><span class="sxs-lookup"><span data-stu-id="fefcc-139">This passphrase is used to access the private SSH key file and is not the user account password.</span></span>

<span data-ttu-id="fefcc-140">当您将密码短语添加到 SSH 密钥时, 它会使用128位 AES 加密私钥, 以便私钥在没有解密密码的情况下毫无用处。</span><span class="sxs-lookup"><span data-stu-id="fefcc-140">When you add a passphrase to your SSH key, it encrypts the private key using 128-bit AES so that the private key is useless without the passphrase to decrypt it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fefcc-141">**强烈**建议您添加密码。</span><span class="sxs-lookup"><span data-stu-id="fefcc-141">It is **strongly** recommended that you add a passphrase.</span></span> <span data-ttu-id="fefcc-142">如果攻击者 stole 您的私钥, 并且该密钥没有密码, 则他们将能够使用该私钥登录到具有相应公钥的任何服务器。</span><span class="sxs-lookup"><span data-stu-id="fefcc-142">If an attacker stole your private key and that key did not have a passphrase, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span> <span data-ttu-id="fefcc-143">如果密码保护私钥, 则该攻击者不能使用该密钥。</span><span class="sxs-lookup"><span data-stu-id="fefcc-143">If a passphrase protects a private key, it cannot be used by that attacker.</span></span> <span data-ttu-id="fefcc-144">这为 Azure 上的基础结构提供了额外的安全层。</span><span class="sxs-lookup"><span data-stu-id="fefcc-144">This provides an additional layer of security for your infrastructure on Azure.</span></span>

## <a name="use-the-ssh-key-pair-with-an-azure-linux-vm"></a><span data-ttu-id="fefcc-145">将 SSH 密钥对与 Azure Linux VM 结合使用</span><span class="sxs-lookup"><span data-stu-id="fefcc-145">Use the SSH key pair with an Azure Linux VM</span></span>

<span data-ttu-id="fefcc-146">生成密钥对后, 可以在 Azure 中将其与 Linux VM 一起使用。</span><span class="sxs-lookup"><span data-stu-id="fefcc-146">Once you have the key pair generated, you can use it with a Linux VM in Azure.</span></span> <span data-ttu-id="fefcc-147">您可以在创建 vm 期间提供公钥, 也可以在创建虚拟机之后添加该公钥。</span><span class="sxs-lookup"><span data-stu-id="fefcc-147">You can supply the public key during the VM creation or add it after the VM has been created.</span></span>

<span data-ttu-id="fefcc-148">您可以使用以下命令查看 Azure 云命令行管理程序中文件的内容:</span><span class="sxs-lookup"><span data-stu-id="fefcc-148">You can view the contents of the file in Azure Cloud Shell with the following command:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="fefcc-149">它将是一个单独的行, 看起来类似于以下内容:</span><span class="sxs-lookup"><span data-stu-id="fefcc-149">It will be a single line and look something like:</span></span>

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

<span data-ttu-id="fefcc-150">复制此值, 以便您可以在下一个练习中使用它。</span><span class="sxs-lookup"><span data-stu-id="fefcc-150">Copy this value, so you can use it in the next exercise.</span></span>

### <a name="use-the-ssh-key-when-creating-a-linux-vm"></a><span data-ttu-id="fefcc-151">创建 Linux VM 时使用 SSH 密钥</span><span class="sxs-lookup"><span data-stu-id="fefcc-151">Use the SSH key when creating a Linux VM</span></span>

<span data-ttu-id="fefcc-152">若要在创建新的 Linux VM 时应用 SSH 密钥, 您需要复制公钥的内容, 并将其提供给 azure 门户,_或_将公钥文件提供给 azure CLI 或 azure PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="fefcc-152">To apply the SSH key while creating a new Linux VM, you will need to copy the contents of the public key and supply it to the Azure portal, _or_ supply the public key file to the Azure CLI or Azure PowerShell command.</span></span> <span data-ttu-id="fefcc-153">我们将在创建 Linux VM 时使用此方法。</span><span class="sxs-lookup"><span data-stu-id="fefcc-153">We'll use this approach when we create our Linux VM.</span></span>

### <a name="add-the-ssh-key-to-an-existing-linux-vm"></a><span data-ttu-id="fefcc-154">将 SSH 密钥添加到现有 Linux VM</span><span class="sxs-lookup"><span data-stu-id="fefcc-154">Add the SSH key to an existing Linux VM</span></span>

<span data-ttu-id="fefcc-155">如果已创建 VM, 则可以使用`ssh-copy-id`命令将公钥安装到 Linux 虚拟机上。</span><span class="sxs-lookup"><span data-stu-id="fefcc-155">If you have already created a VM, you can install the public key onto your Linux VM with the `ssh-copy-id` command.</span></span> <span data-ttu-id="fefcc-156">为 SSH 授权密钥后, 它会在不使用密码的情况下授予对服务器的访问权限, 但是, 如果您设置一个, 仍会提示您输入密钥的密码。</span><span class="sxs-lookup"><span data-stu-id="fefcc-156">Once the key has been authorized for SSH, it grants access to the server without a password, though you will still be prompted for the passphrase on the key if you set one.</span></span>

<span data-ttu-id="fefcc-157">例如, 如果我们有一个名为*myserver*的 Linux VM 与用户*azureuser*, 我们可以使用以下命令来安装公钥文件, 并使用密钥向用户授权:</span><span class="sxs-lookup"><span data-stu-id="fefcc-157">For example, if we had a Linux VM named *myserver* with a user *azureuser*, we could use the following command to install the public key file and authorize the user with the key:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```

<span data-ttu-id="fefcc-158">现在我们已拥有公钥, 我们将切换到 Azure 门户并创建 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="fefcc-158">Now that we have our public key, let's switch to the Azure portal and create a Linux VM.</span></span>
