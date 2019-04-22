<span data-ttu-id="c900e-101">在这里, 将安装 node.js, 即表示首字母缩写词中的**N** 。</span><span class="sxs-lookup"><span data-stu-id="c900e-101">Here you'll install Node.js, the **N** in the MEAN acronym.</span></span> <span data-ttu-id="c900e-102">与 MongoDB 一样, node.js 是开放源代码。</span><span class="sxs-lookup"><span data-stu-id="c900e-102">Like MongoDB, Node.js is open source.</span></span> 

<span data-ttu-id="c900e-103">node.js 将充当 web 应用程序的服务器端主机, 并处理入站 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="c900e-103">Node.js will act as the server-side host for your web application and handle inbound HTTP traffic.</span></span> <span data-ttu-id="c900e-104">node.js 还提供了一种与 MongoDB 安装进行通信的方法, 稍后将会看到。</span><span class="sxs-lookup"><span data-stu-id="c900e-104">Node.js also provides you with a way to communicate with your MongoDB installation, which you'll see later.</span></span>

## <a name="what-versions-of-nodejs-are-available"></a><span data-ttu-id="c900e-105">有哪些版本的 node.js？</span><span class="sxs-lookup"><span data-stu-id="c900e-105">What versions of Node.js are available?</span></span>

<span data-ttu-id="c900e-106">可以通过两种方式获取 node.js:</span><span class="sxs-lookup"><span data-stu-id="c900e-106">You can get Node.js in two ways:</span></span>

- <span data-ttu-id="c900e-107">长期**支持 (LTS)** -LTS 通常被视为更稳定, 建议用于大多数用户和生产环境。</span><span class="sxs-lookup"><span data-stu-id="c900e-107">**Long Term Support (LTS)** - LTS is generally considered to be more stable and is recommended for most users and for production environments.</span></span>
- <span data-ttu-id="c900e-108">**current**适用于那些想要试用最新功能的人员。</span><span class="sxs-lookup"><span data-stu-id="c900e-108">**Current** - Current is for those who want to experiment with the latest features.</span></span> <span data-ttu-id="c900e-109">由于它可能会导致发布之间发生重大更改, 因此不建议在生产环境中进行更改。</span><span class="sxs-lookup"><span data-stu-id="c900e-109">Because it can introduce breaking changes between releases, it's not recommended for production environments.</span></span>

<span data-ttu-id="c900e-110">在这里, 你将使用 node.js LTS。</span><span class="sxs-lookup"><span data-stu-id="c900e-110">Here you'll use Node.js LTS.</span></span>

## <a name="how-do-i-install-nodejs"></a><span data-ttu-id="c900e-111">如何安装 node.js？</span><span class="sxs-lookup"><span data-stu-id="c900e-111">How do I install Node.js?</span></span>

<span data-ttu-id="c900e-112">与 MongoDB 一样, 您可以在 Windows、macOS 和 Linux 上运行 node.js。</span><span class="sxs-lookup"><span data-stu-id="c900e-112">Like MongoDB, you can run Node.js on Windows, macOS, and Linux.</span></span> <span data-ttu-id="c900e-113">node.js 还支持基于 Unix 的操作系统, 如 SunOS 和 AIX。</span><span class="sxs-lookup"><span data-stu-id="c900e-113">Node.js also supports Unix-based operating systems such as SunOS and AIX.</span></span>

<span data-ttu-id="c900e-114">就像 MongoDB 一样, 你将注册 node.js 存储库, 以便`apt`能够找到该包。</span><span class="sxs-lookup"><span data-stu-id="c900e-114">Just as with MongoDB, here you'll register the Node.js repository so that `apt` can locate the package.</span></span>

<span data-ttu-id="c900e-115">回想一下你正在使用 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="c900e-115">Recall that you're working with an Ubuntu VM.</span></span> <span data-ttu-id="c900e-116">稍后, 您可以[查看安装指南](https://nodejs.org/en/download/package-manager?azure-portal=true), 了解如何在你喜爱的平台上安装 node.js。</span><span class="sxs-lookup"><span data-stu-id="c900e-116">Later, you can [check out the installation guide](https://nodejs.org/en/download/package-manager?azure-portal=true) to learn how to install Node.js on your favorite platform.</span></span>

## <a name="install-nodejs"></a><span data-ttu-id="c900e-117">安装 node.js</span><span class="sxs-lookup"><span data-stu-id="c900e-117">Install Node.js</span></span>

<span data-ttu-id="c900e-118">在这里, 将安装 node.js。</span><span class="sxs-lookup"><span data-stu-id="c900e-118">Here you'll install Node.js.</span></span> <span data-ttu-id="c900e-119">与 MongoDB 一样, 此过程涉及注册 node.js 存储库, 以便`apt`能够查找该包。</span><span class="sxs-lookup"><span data-stu-id="c900e-119">As with MongoDB, the process involves registering the Node.js repository so that `apt` can locate the package.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c900e-120">在这里, 你将从 SSH 连接工作到你在本模块前面创建的 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="c900e-120">Here, you'll work from the SSH connection to the Ubuntu VM that you created earlier in this module.</span></span>

1. <span data-ttu-id="c900e-121">注册 node.js 存储库, 以便程序包管理器可以找到程序包, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="c900e-121">Register the Node.js repository so the package manager can locate the packages, like this.</span></span>

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. <span data-ttu-id="c900e-122">安装 node.js 包。</span><span class="sxs-lookup"><span data-stu-id="c900e-122">Install the Node.js package.</span></span>

    ```bash
    sudo apt-get install -y Node.js
    ```

1. <span data-ttu-id="c900e-123">运行`node -v`以验证安装。</span><span class="sxs-lookup"><span data-stu-id="c900e-123">Run `node -v` to verify the installation.</span></span>

    ```bash
    node -v
    ```

    <span data-ttu-id="c900e-124">输出显示, 您具有 node.js 的最新 LTS 版本。</span><span class="sxs-lookup"><span data-stu-id="c900e-124">The output shows that you have the latest LTS version of Node.js.</span></span>

## <a name="exit-your-ssh-session"></a><span data-ttu-id="c900e-125">退出 SSH 会话</span><span class="sxs-lookup"><span data-stu-id="c900e-125">Exit your SSH session</span></span>

<span data-ttu-id="c900e-126">你现在已经在 VM 上直接完成了操作。</span><span class="sxs-lookup"><span data-stu-id="c900e-126">You're all done working directly on the VM for now.</span></span> <span data-ttu-id="c900e-127">运行`exit`以将 SSH 会话保留到 VM。</span><span class="sxs-lookup"><span data-stu-id="c900e-127">Run `exit` to leave the SSH session to your VM.</span></span>

```bash
exit
```

<span data-ttu-id="c900e-128">你现在将回到云 Shell 会话。</span><span class="sxs-lookup"><span data-stu-id="c900e-128">You're now back at your Cloud Shell session.</span></span>