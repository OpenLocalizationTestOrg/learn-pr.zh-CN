<span data-ttu-id="fac0e-101">Azure IoT Central 是一个完全受管理的内容 Internet (IoT) 解决方案, 使您可以轻松地连接、监控和管理您的全局 IoT 资产。</span><span class="sxs-lookup"><span data-stu-id="fac0e-101">Azure IoT Central is a fully managed Internet of Things (IoT) solution that makes it easy to connect, monitor, and manage your global IoT assets.</span></span>

<span data-ttu-id="fac0e-102">在这里, 你将遵循将远程咖啡计算机连接到 Azure IoT Central 以监视和管理问题的方案。</span><span class="sxs-lookup"><span data-stu-id="fac0e-102">Here, you'll follow the scenario in which a remote coffee machine is connected to Azure IoT Central for monitoring and management of issues.</span></span> <span data-ttu-id="fac0e-103">您可以监视遥测 (如水源和湿度)、观察计算机的状态、设置最佳温度、接收保修状态和发送命令。</span><span class="sxs-lookup"><span data-stu-id="fac0e-103">You can monitor telemetry such as water temperature and humidity, observe the state of your machine, set optimal temperature, receive warranty status, and send commands.</span></span> <span data-ttu-id="fac0e-104">如果在室温在预期范围之外时保修已过期, 则会将 IoT 中心发来的电子邮件发送到客户端的维护部门, 以进行进一步操作。</span><span class="sxs-lookup"><span data-stu-id="fac0e-104">If the warranty is expired when the water temperature is outside the expected range, an email from IoT Central is sent to the client’s maintenance department for further action.</span></span>

<span data-ttu-id="fac0e-105">首先, 在 Azure IoT Central 中创建一个设备, 用于定义可与 IoT 设备交换的数据和命令。</span><span class="sxs-lookup"><span data-stu-id="fac0e-105">You'll begin by a creating a device in Azure IoT Central that defines the data and commands that can be exchanged with the IoT device.</span></span>

<span data-ttu-id="fac0e-106">在本模块中, 您将:</span><span class="sxs-lookup"><span data-stu-id="fac0e-106">In this module, you will:</span></span>
  - <span data-ttu-id="fac0e-107">创建 Azure IoT 中心自定义应用程序</span><span class="sxs-lookup"><span data-stu-id="fac0e-107">Create an Azure IoT Central custom application</span></span>
  - <span data-ttu-id="fac0e-108">创建和定义设备模板</span><span class="sxs-lookup"><span data-stu-id="fac0e-108">Create and define your device template</span></span>
  - <span data-ttu-id="fac0e-109">将咖啡机模拟器连接到 Azure IoT Central 中的应用程序</span><span class="sxs-lookup"><span data-stu-id="fac0e-109">Connect a coffee machine simulator to your application in Azure IoT Central</span></span>
  - <span data-ttu-id="fac0e-110">验证连接和数据流</span><span class="sxs-lookup"><span data-stu-id="fac0e-110">Validate your connection and data flow</span></span>
  - <span data-ttu-id="fac0e-111">配置维护通知的规则</span><span class="sxs-lookup"><span data-stu-id="fac0e-111">Configure rules for maintenance notifications</span></span>
 
## <a name="sign-in-to-azure-iot-central"></a><span data-ttu-id="fac0e-112">登录到 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="fac0e-112">Sign in to Azure IoT Central</span></span>
<span data-ttu-id="fac0e-113">在此单元中, 登录 IoT Central 以创建新的自定义应用程序。</span><span class="sxs-lookup"><span data-stu-id="fac0e-113">In this unit, you sign in to IoT Central to create a new custom application.</span></span> <span data-ttu-id="fac0e-114">7天试用足以完成此模块。</span><span class="sxs-lookup"><span data-stu-id="fac0e-114">A 7-day trial is sufficient to complete this module.</span></span> 

1. <span data-ttu-id="fac0e-115">导航到 "Azure IoT 中央[应用程序管理器](https://aka.ms/iotcentral?azure-portal=true)" 页。</span><span class="sxs-lookup"><span data-stu-id="fac0e-115">Navigate to the Azure IoT Central [Application Manager](https://aka.ms/iotcentral?azure-portal=true) page.</span></span> 

1. <span data-ttu-id="fac0e-116">在 "登录" 页面上, 输入用于访问 Microsoft 帐户的电子邮件地址和密码。</span><span class="sxs-lookup"><span data-stu-id="fac0e-116">On the sign-in page, enter the email address and password that you use to access your Microsoft account.</span></span>

## <a name="create-a-new-custom-application"></a><span data-ttu-id="fac0e-117">创建新的自定义应用程序</span><span class="sxs-lookup"><span data-stu-id="fac0e-117">Create a new custom application</span></span>

1. <span data-ttu-id="fac0e-118">若要创建新的 Azure IoT 中心应用程序, 请选择 "**新建应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="fac0e-118">To create a new Azure IoT Central application, choose **New Application**.</span></span> 

1. <span data-ttu-id="fac0e-119">在 "**创建应用程序**" 页上:</span><span class="sxs-lookup"><span data-stu-id="fac0e-119">On the **Create Application** page:</span></span> 
    * <span data-ttu-id="fac0e-120">为付款计划选择 "**免费**"</span><span class="sxs-lookup"><span data-stu-id="fac0e-120">Choose **Free** for the payment plan</span></span>
    * <span data-ttu-id="fac0e-121">选择 "**自定义应用程序**" 作为应用程序模板</span><span class="sxs-lookup"><span data-stu-id="fac0e-121">Select **Custom Application** as the application template</span></span>
    * <span data-ttu-id="fac0e-122">选择友好的应用程序名称, 如 "**咖啡 Maker 01-a** "</span><span class="sxs-lookup"><span data-stu-id="fac0e-122">Choose a friendly application name, like **Coffee Maker 01-A**</span></span>
    * <span data-ttu-id="fac0e-123">(可选) 编辑 URL-如果所选的名称已在使用中, 则需要此项。</span><span class="sxs-lookup"><span data-stu-id="fac0e-123">(Optionally) edit the URL - this will be required if the name you selected is already in use</span></span>
    * <span data-ttu-id="fac0e-124">选择 "**创建**</span><span class="sxs-lookup"><span data-stu-id="fac0e-124">Choose **Create**</span></span>
