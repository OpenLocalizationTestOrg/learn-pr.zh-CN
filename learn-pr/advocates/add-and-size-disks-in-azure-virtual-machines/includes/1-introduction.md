<span data-ttu-id="66e74-101">您是法律公司的系统架构师。</span><span class="sxs-lookup"><span data-stu-id="66e74-101">You're the system architect for a law firm.</span></span> <span data-ttu-id="66e74-102">该事务所要求你将关键系统迁移到 Azure。</span><span class="sxs-lookup"><span data-stu-id="66e74-102">The firm has asked you to migrate critical systems to Azure.</span></span> <span data-ttu-id="66e74-103">操作包括事例历史记录的数据库, 当前由本地 SQL server 托管, 并从桌面应用程序访问。</span><span class="sxs-lookup"><span data-stu-id="66e74-103">Operations include the database of case histories, currently hosted by an on-premises SQL server and accessed from a desktop application.</span></span> <span data-ttu-id="66e74-104">SQL server 还运行一些自定义的内部服务, 以执行数据库维护。</span><span class="sxs-lookup"><span data-stu-id="66e74-104">The SQL server also runs some custom in-house services to perform database maintenance.</span></span> <span data-ttu-id="66e74-105">您已决定基于 Azure 虚拟机 (vm) 的解决方案将允许您托管 SQL server 并继续使用自定义服务。</span><span class="sxs-lookup"><span data-stu-id="66e74-105">You've decided that a solution based on Azure virtual machines (VMs) will allow you to host your SQL server and continue using your custom services.</span></span> <span data-ttu-id="66e74-106">你将根据现有的本地服务器的内容创建 Azure 虚拟硬盘以方便迁移。</span><span class="sxs-lookup"><span data-stu-id="66e74-106">You'll create an Azure virtual hard disk based on the contents of your existing on-premises server to ease migration.</span></span>

<span data-ttu-id="66e74-107">在本模块中, 您将了解如何为在 Azure 中创建的 vm 构建最佳磁盘配置。</span><span class="sxs-lookup"><span data-stu-id="66e74-107">In this module, you'll learn how to architect the optimal disk configuration for the VMs you create in Azure.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="66e74-108">学习目标</span><span class="sxs-lookup"><span data-stu-id="66e74-108">Learning objectives</span></span>

<span data-ttu-id="66e74-109">在本模块中, 您将:</span><span class="sxs-lookup"><span data-stu-id="66e74-109">In this module, you will:</span></span>

- <span data-ttu-id="66e74-110">创建虚拟机 (VM)</span><span class="sxs-lookup"><span data-stu-id="66e74-110">Create a virtual machine (VM)</span></span>
- <span data-ttu-id="66e74-111">配置虚拟硬盘 (vhd) 并将其附加到现有 VM</span><span class="sxs-lookup"><span data-stu-id="66e74-111">Configure and attach virtual hard drives (VHDs) to an existing VM</span></span>
- <span data-ttu-id="66e74-112">确定是否需要高级磁盘</span><span class="sxs-lookup"><span data-stu-id="66e74-112">Determine whether you need premium disks</span></span>
- <span data-ttu-id="66e74-113">为 VM 调整磁盘大小</span><span class="sxs-lookup"><span data-stu-id="66e74-113">Resize disks for a VM</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66e74-114">先决条件</span><span class="sxs-lookup"><span data-stu-id="66e74-114">Prerequisites</span></span>

<span data-ttu-id="66e74-115">无</span><span class="sxs-lookup"><span data-stu-id="66e74-115">None</span></span>