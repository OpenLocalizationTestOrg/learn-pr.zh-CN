<span data-ttu-id="254d3-101">你决定在任何人访问 azure 门户时, 部署 azure AD 并使用条件访问策略, 以使 azure 要求进行多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="254d3-101">You decide to deploy Azure AD and use conditional access policies that Azure require Multi-Factor Authentication when anyone accesses the Azure portal.</span></span> <span data-ttu-id="254d3-102">您需要创建一个目录, 并就地获取临时许可证。</span><span class="sxs-lookup"><span data-stu-id="254d3-102">You need to create a directory and get temporary licenses in place.</span></span>

## <a name="launch-lab-and-sign-in-to-the-azure-portal"></a><span data-ttu-id="254d3-103">启动实验室并登录到 Azure 门户</span><span class="sxs-lookup"><span data-stu-id="254d3-103">Launch lab and sign in to the Azure portal</span></span>

1. <span data-ttu-id="254d3-104">单击上面的链接以启动实验室。</span><span class="sxs-lookup"><span data-stu-id="254d3-104">Click the link above to launch the lab.</span></span>

> [!NOTE]
> <span data-ttu-id="254d3-105">启动实验室后, 您需要登录的用户名和密码位于说明旁边的 "**资源**" 选项卡上。</span><span class="sxs-lookup"><span data-stu-id="254d3-105">After launching the lab, the username and password you need to sign in with is located on the **Resources** tab next to the instructions.</span></span>

![显示带有选择框的 Azure 门户沙盒登录项的屏幕截图对 "资源" 选项卡和正确的 "登录" 选项进行了强调](../media/3-sandbox-login.png)

<span data-ttu-id="254d3-107">记下用户名末尾的号码, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="254d3-107">Make a note of the number at the end of the username, as shown below.</span></span> <span data-ttu-id="254d3-108">在本练习的后面部分, 您将需要该数字。</span><span class="sxs-lookup"><span data-stu-id="254d3-108">You will need that number later in this exercise.</span></span>

![显示带有选择框的 Azure 门户沙盒实验室资源的屏幕截图将注意力引起在用户名末尾的编号中](../media/3-user-number.png)

<span data-ttu-id="254d3-110">如果你想要从头开始使用此实验室, 可在任何时候退出实验室沙盒, 并使用上面的链接创建新的沙盒沙盒。</span><span class="sxs-lookup"><span data-stu-id="254d3-110">If at any time during this lab when you want to start over, you can exit the Lab Sandbox and create a fresh one with the link above.</span></span>

## <a name="create-a-directory"></a><span data-ttu-id="254d3-111">创建目录</span><span class="sxs-lookup"><span data-stu-id="254d3-111">Create a directory</span></span>

<span data-ttu-id="254d3-112">您将为沙盒门户中的第一个顾问创建一个新的 Active Directory, 在其中可以进行测试, 而无需担心影响生产用户。</span><span class="sxs-lookup"><span data-stu-id="254d3-112">You will create a new Active Directory for First Up Consultants in the Sandbox Portal, where you can test without fear of impacting production users.</span></span> <span data-ttu-id="254d3-113">如果你更喜欢在自己的 Azure 帐户和订阅上执行此练习, 请立即登录[azure 门户](https://portal.azure.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="254d3-113">If you'd prefer doing this exercise on your own Azure account and subscription, log into the [Azure portal](https://portal.azure.com?azure-portal=true) now.</span></span> <span data-ttu-id="254d3-114">请注意, 这样做可能会影响您的现有帐户和订阅帐单。</span><span class="sxs-lookup"><span data-stu-id="254d3-114">Be advised that doing so may impact your existing account and subscription billing.</span></span> <span data-ttu-id="254d3-115">仅当您确定这些含义时才选择此选项。</span><span class="sxs-lookup"><span data-stu-id="254d3-115">Choose this option only if you are certain of the implications.</span></span> <span data-ttu-id="254d3-116">建议使用实验室沙盒环境。</span><span class="sxs-lookup"><span data-stu-id="254d3-116">We recommend using the Lab Sandbox environment.</span></span>

1. <span data-ttu-id="254d3-117">在左侧导航窗格中, 单击 "**创建资源** > **标识** > **Azure Active Directory**"。</span><span class="sxs-lookup"><span data-stu-id="254d3-117">In the left navigation pane, click **Create a resource** > **Identity** > **Azure Active Directory**.</span></span>

1. <span data-ttu-id="254d3-118">在 "**创建目录**边栏" 中, 为**组织名称**和**初始域名**提供以下值:</span><span class="sxs-lookup"><span data-stu-id="254d3-118">In the **Create directory** blade, provide the following values for the **Organization name** and **Initial domain name**:</span></span>

   1. <span data-ttu-id="254d3-119">组织名称: `First Up Consultants`。</span><span class="sxs-lookup"><span data-stu-id="254d3-119">Organization Name: `First Up Consultants`.</span></span>
   2. <span data-ttu-id="254d3-120">初始域名: `firstupconsultants<XXXXXXX>`其中<XXXXXXX> , 您之前对其进行了说明的编号将显示在用户名后面, 如上面的屏幕截图中所示。</span><span class="sxs-lookup"><span data-stu-id="254d3-120">Initial Domain Name: `firstupconsultants<XXXXXXX>` where <XXXXXXX> is the number you previously made a note of that appears after the username, as shown in the screenshot above.</span></span>

1. <span data-ttu-id="254d3-121">等待创建目录。</span><span class="sxs-lookup"><span data-stu-id="254d3-121">Wait for the directory to be created.</span></span> <span data-ttu-id="254d3-122">记下完整的域名, 如下所示。</span><span class="sxs-lookup"><span data-stu-id="254d3-122">Make a note of the full domain name, as shown below.</span></span> <span data-ttu-id="254d3-123">单击链接以切换到新目录。</span><span class="sxs-lookup"><span data-stu-id="254d3-123">Click the link to switch to the new directory.</span></span>

![显示创建具有选择框的 Active Directory 的屏幕截图对域名和要单击的链接的位置的关注](../media/3-create-directory.png)

## <a name="get-trial-licenses"></a><span data-ttu-id="254d3-125">获取试用许可证</span><span class="sxs-lookup"><span data-stu-id="254d3-125">Get trial licenses</span></span>

<span data-ttu-id="254d3-126">若要使用条件访问和多重身份验证等功能, 您至少需要试用许可证。</span><span class="sxs-lookup"><span data-stu-id="254d3-126">To use features like conditional access and Multi-Factor Authentication, you will need at least a trial license.</span></span> <span data-ttu-id="254d3-127">下面的步骤将引导您完成如何启用试用许可证:</span><span class="sxs-lookup"><span data-stu-id="254d3-127">The following steps walk you through how to enable a trial license:</span></span>

1. <span data-ttu-id="254d3-128">在 "Azure AD**概述**" 窗格中, 单击 "**开始免费试用**" 链接。</span><span class="sxs-lookup"><span data-stu-id="254d3-128">In the Azure AD **Overview** pane, click the **Start a free trial** link.</span></span>

1. <span data-ttu-id="254d3-129">在 " **Azure AD 高级 P2**" 项下, 单击 "**免费试用**", 然后单击 "**激活**"。</span><span class="sxs-lookup"><span data-stu-id="254d3-129">Under the item **Azure AD Premium P2**, click **Free trial**, and then click **Activate**.</span></span>

## <a name="create-a-test-user"></a><span data-ttu-id="254d3-130">创建测试用户</span><span class="sxs-lookup"><span data-stu-id="254d3-130">Create a test user</span></span>

<span data-ttu-id="254d3-131">我们需要通过用户来测试此事情。</span><span class="sxs-lookup"><span data-stu-id="254d3-131">We're going to need to test this out with a user.</span></span> <span data-ttu-id="254d3-132">Isabella Simonsen (团队的另一个成员) 有 volunteered 来帮助你。她将需要目录中的帐户, 因此我们将通过这些步骤来创建她的帐户。</span><span class="sxs-lookup"><span data-stu-id="254d3-132">Isabella Simonsen (another member of your team) has volunteered to help you out. She will need an account in the directory, so we will go through the steps to create her account.</span></span>

1. <span data-ttu-id="254d3-133">浏览到**Azure Active Directory** > **用户**。</span><span class="sxs-lookup"><span data-stu-id="254d3-133">Browse to **Azure Active Directory** > **Users**.</span></span>

1. <span data-ttu-id="254d3-134">单击 "**新建用户**"。</span><span class="sxs-lookup"><span data-stu-id="254d3-134">Click **New user**.</span></span>

1. <span data-ttu-id="254d3-135">使用以下用户名创建名为**Isabella Simonsen**的用户:</span><span class="sxs-lookup"><span data-stu-id="254d3-135">Create a user named **Isabella Simonsen** with a user name of:</span></span>

   `Isabella@firstupconsultants<XXXXXXX>.onmicrosoft.com`

   <span data-ttu-id="254d3-136">与创建的域中的 @ 后面的域匹配, 并在上面的*Create a directory*部分中注明。</span><span class="sxs-lookup"><span data-stu-id="254d3-136">Match the domain after the @ with the domain you created and noted in the *Create a directory* section above.</span></span>

1. <span data-ttu-id="254d3-137">选中此复选框可显示用户的**密码**。</span><span class="sxs-lookup"><span data-stu-id="254d3-137">Check the box to **Show Password** for the user.</span></span> <span data-ttu-id="254d3-138">记下密码, 以便稍后在测试时使用它。</span><span class="sxs-lookup"><span data-stu-id="254d3-138">Make a note of the password so you can use it later when testing.</span></span>

1. <span data-ttu-id="254d3-139">单击"创建"。</span><span class="sxs-lookup"><span data-stu-id="254d3-139">Click **Create**.</span></span>

## <a name="create-a-pilot-group"></a><span data-ttu-id="254d3-140">创建试点组</span><span class="sxs-lookup"><span data-stu-id="254d3-140">Create a pilot group</span></span>

<span data-ttu-id="254d3-141">我们将向一组用户分配所创建的策略, 但我们需要为此策略创建一个组。</span><span class="sxs-lookup"><span data-stu-id="254d3-141">We will be assigning the policy that we create to a group of users, but we need to create a group for this policy.</span></span> <span data-ttu-id="254d3-142">以下步骤可帮助您为试点部署创建安全组。</span><span class="sxs-lookup"><span data-stu-id="254d3-142">The following steps help you create a security group for the pilot deployment.</span></span>

1. <span data-ttu-id="254d3-143">浏览到**Azure Active Directory** > **组**。</span><span class="sxs-lookup"><span data-stu-id="254d3-143">Browse to **Azure Active Directory** > **Groups**.</span></span>

1. <span data-ttu-id="254d3-144">单击 "**新建组**"。</span><span class="sxs-lookup"><span data-stu-id="254d3-144">Click **New group**.</span></span>

1. <span data-ttu-id="254d3-145">组类型**安全性**。</span><span class="sxs-lookup"><span data-stu-id="254d3-145">Group type **Security**.</span></span>

1. <span data-ttu-id="254d3-146">组名称 " **CA-AzurePortal**"。</span><span class="sxs-lookup"><span data-stu-id="254d3-146">Group name **CA-MFA-AzurePortal**.</span></span>

1. <span data-ttu-id="254d3-147">**分配**的成员资格类型并单击 "成员" 链接 (在下图中标记为 "1")。</span><span class="sxs-lookup"><span data-stu-id="254d3-147">Membership type **Assigned** and click the Members link (labeled "1" in the diagram below).</span></span>

1. <span data-ttu-id="254d3-148">选择在上一步中创建的用户 (在下图中标记为 "2"), 然后选择 "**选择**" (标记为 "3")。</span><span class="sxs-lookup"><span data-stu-id="254d3-148">Select the user that we created in the previous step (labeled "2" in the diagram below) and choose **Select** (labeled "3).</span></span>

1. <span data-ttu-id="254d3-149">单击下图中的 "**创建**" (标记为 "4")。</span><span class="sxs-lookup"><span data-stu-id="254d3-149">Click **Create** (labeled "4" in the diagram below).</span></span>

![显示创建具有选择框的 Active Directory 组的屏幕截图对前面的步骤进行了关注](../media/3-group-blade.png)

<span data-ttu-id="254d3-151">在此单元中, 你学习了如何在 Azure 门户中创建试用许可的目录、测试用户和试点组。</span><span class="sxs-lookup"><span data-stu-id="254d3-151">In this unit, you learned how to create a trial licensed directory, a test user, and a pilot group in the Azure portal.</span></span>