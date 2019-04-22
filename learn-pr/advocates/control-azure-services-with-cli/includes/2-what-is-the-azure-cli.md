<span data-ttu-id="5e218-101">azure CLI 是一个命令行程序, 用于连接到 azure 并在 azure 资源上执行管理命令。</span><span class="sxs-lookup"><span data-stu-id="5e218-101">The Azure CLI is a command-line program to connect to Azure and execute administrative commands on Azure resources.</span></span> <span data-ttu-id="5e218-102">它在 Linux、macOS 和 Windows 上运行, 并允许管理员和开发人员通过终端或命令行提示符 (或 script!) 而不是 web 浏览器来执行其命令。</span><span class="sxs-lookup"><span data-stu-id="5e218-102">It runs on Linux, macOS, and Windows and allows administrators and developers to execute their commands through a terminal or command-line prompt (or script!) instead of a web browser.</span></span> <span data-ttu-id="5e218-103">例如, 若要重新启动虚拟机 (VM), 应使用类似如下的命令:</span><span class="sxs-lookup"><span data-stu-id="5e218-103">For example, to restart a virtual machine (VM), you would use a command like the following:</span></span>

 ```azurecli
 az vm restart -g MyResourceGroup -n MyVm
 ```

<span data-ttu-id="5e218-104">azure CLI 提供用于管理 Azure 资源的跨平台命令行工具, 并且可以在 Linux、Mac 或 Windows 计算机上本地安装。</span><span class="sxs-lookup"><span data-stu-id="5e218-104">The Azure CLI provides cross-platform command-line tools for managing Azure resources, and can be installed locally on Linux, Mac, or Windows computers.</span></span> <span data-ttu-id="5e218-105">也可以通过 azure 云命令行管理程序在浏览器中使用 azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5e218-105">The Azure CLI can also be used from a browser through the Azure Cloud Shell.</span></span> <span data-ttu-id="5e218-106">在这两种情况下, 可以交互使用, 也可以编写脚本。</span><span class="sxs-lookup"><span data-stu-id="5e218-106">In both cases, it can be used interactively or scripted.</span></span> <span data-ttu-id="5e218-107">为进行交互式使用, 您首先在 Windows 上或在 Linux 或 macOS 上启动一个命令行管理程序 (如 cmd.exe), 然后在命令行管理程序提示符处发出命令。</span><span class="sxs-lookup"><span data-stu-id="5e218-107">For interactive use, you first launch a shell such as cmd.exe on Windows or Bash on Linux or macOS and then issue the command at the shell prompt.</span></span> <span data-ttu-id="5e218-108">若要自动执行重复任务, 请使用所选命令行管理程序的脚本语法将 CLI 命令组合到命令行管理程序脚本中, 然后执行该脚本。</span><span class="sxs-lookup"><span data-stu-id="5e218-108">To automate repetitive tasks, you assemble the CLI commands into a shell script using the script syntax of your chosen shell and then execute the script.</span></span>

## <a name="how-to-install-the-azure-cli"></a><span data-ttu-id="5e218-109">如何安装 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e218-109">How to install the Azure CLI</span></span>

<span data-ttu-id="5e218-110">在 Linux 和 macOS 上, 使用程序包管理器安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5e218-110">On both Linux and macOS, you use a package manager to install the Azure CLI.</span></span> <span data-ttu-id="5e218-111">建议的程序包管理器因 OS 和分发而异:</span><span class="sxs-lookup"><span data-stu-id="5e218-111">The recommended package manager differs by OS and distribution:</span></span>

- <span data-ttu-id="5e218-112">Linux: **apt.-get** Ubuntu、 **yum** on Red Hat 和**zypper** on OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="5e218-112">Linux: **apt-get** on Ubuntu, **yum** on Red Hat, and **zypper** on OpenSUSE</span></span>
- <span data-ttu-id="5e218-113">Mac: **Homebrew**</span><span class="sxs-lookup"><span data-stu-id="5e218-113">Mac: **Homebrew**</span></span>

<span data-ttu-id="5e218-114">Azure CLI 在 Microsoft 存储库中可用, 因此你首先需要将该存储库添加到你的程序包管理器。</span><span class="sxs-lookup"><span data-stu-id="5e218-114">The Azure CLI is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

<span data-ttu-id="5e218-115">在 Windows 上, 您可以通过下载并运行 MSI 文件来安装 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5e218-115">On Windows, you install the Azure CLI by downloading and running an MSI file.</span></span>

## <a name="using-the-azure-cli-in-scripts"></a><span data-ttu-id="5e218-116">在脚本中使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e218-116">Using the Azure CLI in scripts</span></span>

<span data-ttu-id="5e218-117">如果要在脚本中使用 Azure CLI 命令, 则需要了解用于运行脚本的 "命令行管理程序" 或环境的任何问题。</span><span class="sxs-lookup"><span data-stu-id="5e218-117">If you want to use the Azure CLI commands in scripts, you need to be aware of any issues around the "shell" or environment used for running the script.</span></span> <span data-ttu-id="5e218-118">例如, 在 bash 命令行管理程序中, 设置变量时将使用以下语法:</span><span class="sxs-lookup"><span data-stu-id="5e218-118">For example, in a bash shell, the following syntax is used when setting variables:</span></span>

```azurecli
variable="value"
variable=integer
```

<span data-ttu-id="5e218-119">如果使用 PowerShell 环境运行 Azure CLI 脚本, 则需要对变量使用以下语法:</span><span class="sxs-lookup"><span data-stu-id="5e218-119">If you use a PowerShell environment for running Azure CLI scripts, you'll need to use this syntax for variables:</span></span>

```powershell
$variable="value"
$variable=integer
```

<span data-ttu-id="5e218-120">必须先安装 Azure CLI, 然后才能将其用于管理本地计算机中的 azure 资源。</span><span class="sxs-lookup"><span data-stu-id="5e218-120">The Azure CLI must be installed before it can be used to manage Azure resources from a local computer.</span></span> <span data-ttu-id="5e218-121">安装步骤因 Windows、Linux 和 macOS 而异, 但安装后, 这些命令在各个平台之间是常见的。</span><span class="sxs-lookup"><span data-stu-id="5e218-121">The installation steps vary for Windows, Linux, and macOS, but once installed, the commands are common across platforms.</span></span>
