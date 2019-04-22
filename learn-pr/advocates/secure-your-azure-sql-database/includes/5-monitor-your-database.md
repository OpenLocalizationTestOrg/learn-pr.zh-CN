<span data-ttu-id="2104f-101">设想您会收到来自贵公司的安全管理员的警报, 指出网络中检测到潜在的安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="2104f-101">Imagine you receive an alert from your company's security administrator that a potential security breach has been detected on your network.</span></span> <span data-ttu-id="2104f-102">怀疑未经授权的个人可能已通过恶意活动访问您的数据库。</span><span class="sxs-lookup"><span data-stu-id="2104f-102">It's suspected that an unauthorized individual may have accessed your database through malicious activity.</span></span> <span data-ttu-id="2104f-103">如何跟踪此问题？</span><span class="sxs-lookup"><span data-stu-id="2104f-103">How would you track this down?</span></span> <span data-ttu-id="2104f-104">您知道您需要积极监控数据库是否有可疑的活动, 但您可以采取什么操作才能了解数据库中发生的情况, 同时还能防止恶意活动发生吗？</span><span class="sxs-lookup"><span data-stu-id="2104f-104">You know you need to be actively monitoring your database for suspicious activity, but what can you do to not only gain visibility into what's happening in your database, but to also prevent malicious activity from occurring?</span></span>

<span data-ttu-id="2104f-105">Azure SQL 数据库具有内置功能, 可帮助您跟踪数据库中发生的情况, 并将监视并在发现恶意活动时向您发出警报。</span><span class="sxs-lookup"><span data-stu-id="2104f-105">Azure SQL Database has built-in features that can help you track what's happening in your database, and will monitor and alert you if malicious activity is identified.</span></span>

## <a name="azure-sql-database-auditing"></a><span data-ttu-id="2104f-106">Azure SQL 数据库审核</span><span class="sxs-lookup"><span data-stu-id="2104f-106">Azure SQL Database auditing</span></span>

<span data-ttu-id="2104f-107">通过启用审核, 可存储数据库中发生的操作, 以供以后检查或让自动化工具对它们进行分析。</span><span class="sxs-lookup"><span data-stu-id="2104f-107">By enabling auditing, operations that occur on the database are stored for later inspection or to have automated tools analyze them.</span></span> <span data-ttu-id="2104f-108">审核还可用于合规性管理或了解您的数据库的使用方式。</span><span class="sxs-lookup"><span data-stu-id="2104f-108">Auditing is also used for compliance management or understanding how your database is used.</span></span> <span data-ttu-id="2104f-109">如果您想要在 azure SQL 数据库上使用 azure 威胁检测, 也需要进行审核。</span><span class="sxs-lookup"><span data-stu-id="2104f-109">Auditing is also required if you wish to use Azure threat detection on your Azure SQL database.</span></span>

<span data-ttu-id="2104f-110">审核日志将写入到您指定的 Azure Blob 存储帐户中的附加 blob。</span><span class="sxs-lookup"><span data-stu-id="2104f-110">Audit logs are written to Append Blobs in an Azure Blob storage account that you designate.</span></span> <span data-ttu-id="2104f-111">可以在服务器级别或数据库级别应用审核策略。</span><span class="sxs-lookup"><span data-stu-id="2104f-111">Audit policies can be applied at the server-level or database-level.</span></span> <span data-ttu-id="2104f-112">启用后, 可以使用 Azure 门户查看日志, 或将其发送到 Log Analytics 或 Event Hub 以进行进一步处理和分析。</span><span class="sxs-lookup"><span data-stu-id="2104f-112">Once enabled, you can use the Azure portal to view the logs, or send them to Log Analytics or Event Hub for further processing and analysis.</span></span>

<span data-ttu-id="2104f-113">我们来看看您在系统上设置审核需要执行的步骤。</span><span class="sxs-lookup"><span data-stu-id="2104f-113">Let's look at the steps you take to set up auditing on your system.</span></span>

1. <span data-ttu-id="2104f-114">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="2104f-114">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="2104f-115">在门户顶部的搜索栏中, 搜索 " **server<12345>**", 然后在门户中选择服务器。</span><span class="sxs-lookup"><span data-stu-id="2104f-115">In the search bar at the top of the portal, search for **server<12345>**, then select the server in the portal.</span></span>

1. <span data-ttu-id="2104f-116">在左侧菜单中的 "**安全性**" 部分, 选择 "**审核**" 选项。</span><span class="sxs-lookup"><span data-stu-id="2104f-116">In the left menu, in the **Security** section, select the **Auditing** option.</span></span>

1. <span data-ttu-id="2104f-117">审核在默认情况下处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="2104f-117">Auditing is turned off by default.</span></span> <span data-ttu-id="2104f-118">若要在数据库服务器上启用它, 请点击 " **on** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="2104f-118">To enable it on your database server, tap the **ON** button.</span></span>

1. <span data-ttu-id="2104f-119">选择 "打开" 按钮后, 选中 "**存储**" 复选框, 然后单击 "**存储详细信息**" 以定义存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2104f-119">Once the ON button is selected, select the **Storage** checkbox, then click **Storage details** to define the storage account.</span></span>

1. <span data-ttu-id="2104f-120">在 "**存储设置**" 对话框中, 您可以选择一个现有存储帐户, 也可以创建新的存储帐户以存储您的审核。</span><span class="sxs-lookup"><span data-stu-id="2104f-120">In the **Storage settings** dialog, you can select an existing storage account or create a new storage account to store your audits.</span></span> <span data-ttu-id="2104f-121">存储帐户必须配置为使用与服务器相同的区域。</span><span class="sxs-lookup"><span data-stu-id="2104f-121">The storage account must be configured to use the same region as your server.</span></span> <span data-ttu-id="2104f-122">在这种情况下, 我们将定义新的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2104f-122">In this case, we'll define a new storage account.</span></span> <span data-ttu-id="2104f-123">单击 "**存储帐户**", 这将打开 "**创建存储帐户**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="2104f-123">Click **Storage account**, which will then open up the **Create storage account** dialog.</span></span> <span data-ttu-id="2104f-124">将存储帐户`server<12345>auditing`的名称替换`<12345>`为逻辑服务器名称中的数字。</span><span class="sxs-lookup"><span data-stu-id="2104f-124">Name the storage account `server<12345>auditing` replacing the `<12345>` with the number from your logical server name.</span></span> <span data-ttu-id="2104f-125">保留其余选项的默认值, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="2104f-125">Leave the rest of the options at their defaults and select **OK**.</span></span> <span data-ttu-id="2104f-126">返回到 "**存储设置**" 对话框中, 保留默认值, 然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="2104f-126">Back in the **Storage settings** dialog, leave the defaults and click **OK**.</span></span>

1. <span data-ttu-id="2104f-127">单击工具栏中的 "**保存**" 按钮以保存所做的更改并在数据库服务器上启用审核。</span><span class="sxs-lookup"><span data-stu-id="2104f-127">Click the **Save** button in the toolbar to save your changes and enable auditing on your database server.</span></span>

<span data-ttu-id="2104f-128">现在, 我们将生成一些审核记录, 并查看你可以预期的内容。</span><span class="sxs-lookup"><span data-stu-id="2104f-128">Now let's generate some audit records and take a look at what you can expect.</span></span>

1. <span data-ttu-id="2104f-129">让我们以_ApplicationUser_用户的形式重新登录到数据库。</span><span class="sxs-lookup"><span data-stu-id="2104f-129">Let's log back in to the database as the _ApplicationUser_ user.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U 'ApplicationUser' -P '<password>' -N -l 30
    ```

1. <span data-ttu-id="2104f-130">运行以下查询。</span><span class="sxs-lookup"><span data-stu-id="2104f-130">Run the following query.</span></span>

    ```sql
    SELECT FirstName, LastName, EmailAddress, Phone FROM SalesLT.Customer;
    GO
    ```

1. <span data-ttu-id="2104f-131">返回到 sql server 上的门户, 在左侧菜单中选择 " **SQL 数据库**", 然后选择 " _marketplace_ " 数据库。</span><span class="sxs-lookup"><span data-stu-id="2104f-131">Back in the portal on your SQL server, select **SQL databases** in the left menu and select the _marketplace_ database.</span></span>

1. <span data-ttu-id="2104f-132">在您的_marketplace_数据库的左侧菜单中的 "**安全性**" 部分, 选择 "**审核**"。</span><span class="sxs-lookup"><span data-stu-id="2104f-132">In the left menu on your _marketplace_ database, in the **Security** section select **Auditing**.</span></span>

1. <span data-ttu-id="2104f-133">由于我们在服务器级别启用了审核, 你应该会看到此处启用了审核。</span><span class="sxs-lookup"><span data-stu-id="2104f-133">Since we enabled auditing at the server-level, you should see that it's enabled here.</span></span> <span data-ttu-id="2104f-134">选择顶部菜单栏中的 "**查看审核日志**" 以查看日志。</span><span class="sxs-lookup"><span data-stu-id="2104f-134">Select **View audit logs** in the top menu bar to view the logs.</span></span>

1. <span data-ttu-id="2104f-135">您应该会看到一个或多个具有**主体名称**为_ApplicationUser_和**事件类型**为 "**批处理已完成**" 的审核记录。</span><span class="sxs-lookup"><span data-stu-id="2104f-135">You should see one or more audit records with **PRINCIPAL NAME** of _ApplicationUser_ and **EVENT TYPE** of **BATCH COMPLETED**.</span></span> <span data-ttu-id="2104f-136">其中一个应包含刚执行的查询的详细信息。</span><span class="sxs-lookup"><span data-stu-id="2104f-136">One of them should contain the details of the query you just executed.</span></span> <span data-ttu-id="2104f-137">你可能还会看到其他事件, 例如身份验证失败和成功。</span><span class="sxs-lookup"><span data-stu-id="2104f-137">You might also see other events such as authentication failures and success.</span></span> <span data-ttu-id="2104f-138">选择 "任意记录" 可查看事件的完整详细信息。</span><span class="sxs-lookup"><span data-stu-id="2104f-138">Select any record to see the full details of the event.</span></span>

![显示审核日志中的事件的示例](../media/5-audit-log.png)

<span data-ttu-id="2104f-140">这些操作将在数据库服务器级别配置审核, 并将其应用于服务器上的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="2104f-140">These actions configure the audits at the database server level and will apply to all databases on the server.</span></span> <span data-ttu-id="2104f-141">您还可以在数据库级别配置审核。</span><span class="sxs-lookup"><span data-stu-id="2104f-141">You can also configure auditing at a database level.</span></span>

<span data-ttu-id="2104f-142">让我们看一下利用这些日志提高数据库安全性的另一项功能。</span><span class="sxs-lookup"><span data-stu-id="2104f-142">Let's take a look at another feature that leverages these logs to increase the security of your database.</span></span>

## <a name="advanced-threat-protection-for-azure-sql-database"></a><span data-ttu-id="2104f-143">Azure SQL 数据库的高级威胁防护</span><span class="sxs-lookup"><span data-stu-id="2104f-143">Advanced Threat Protection for Azure SQL Database</span></span>

<span data-ttu-id="2104f-144">高级威胁防护系统分析审核日志, 以查找针对您的数据库的潜在问题和威胁。</span><span class="sxs-lookup"><span data-stu-id="2104f-144">The Advanced Threat Protection system analyzes audit logs to look for potential problems and threats against your database.</span></span> <span data-ttu-id="2104f-145">它包括用于发现和分类敏感数据的功能、呈现和缓解潜在的数据库漏洞以及检测可能指示对数据库的威胁的反常活动。</span><span class="sxs-lookup"><span data-stu-id="2104f-145">It includes functionality for discovering and classifying sensitive data, surfacing and mitigating potential database vulnerabilities, and detecting anomalous activities that could indicate a threat to your database.</span></span> <span data-ttu-id="2104f-146">它提供了用于启用和管理这些功能的单一转到位置。</span><span class="sxs-lookup"><span data-stu-id="2104f-146">It provides a single go-to location for enabling and managing these capabilities.</span></span> <span data-ttu-id="2104f-147">只需要单击一次, 即可在整个数据库服务器上启用 ATP, 并将其应用于服务器上的所有数据库。</span><span class="sxs-lookup"><span data-stu-id="2104f-147">With one click, you can enable ATP on your entire database server, applying to all databases on the server.</span></span>

### <a name="setup-and-configuration"></a><span data-ttu-id="2104f-148">设置和配置</span><span class="sxs-lookup"><span data-stu-id="2104f-148">Setup and configuration</span></span>

<span data-ttu-id="2104f-149">让我们对数据库启用高级威胁防护。</span><span class="sxs-lookup"><span data-stu-id="2104f-149">Let's enable Advanced Threat Protection on our database.</span></span> <span data-ttu-id="2104f-150">高级威胁防护是服务器级别的设置, 因此我们将从此处开始。</span><span class="sxs-lookup"><span data-stu-id="2104f-150">Advanced Threat Protection is a server-level setting, so we'll start there.</span></span>

1. <span data-ttu-id="2104f-151">返回门户, 导航到您的 SQL server。</span><span class="sxs-lookup"><span data-stu-id="2104f-151">Back in the portal, navigate to your SQL server.</span></span> <span data-ttu-id="2104f-152">在门户顶部的搜索栏中, 搜索 " **server<12345>**", 然后选择 "服务器"。</span><span class="sxs-lookup"><span data-stu-id="2104f-152">In the search bar at the top of the portal, search for **server<12345>**, then select the server.</span></span>

1. <span data-ttu-id="2104f-153">在左侧菜单中的 "**安全性**" 部分, 选择 "**高级威胁防护**" 选项。</span><span class="sxs-lookup"><span data-stu-id="2104f-153">In the left menu, in the **Security** section, select the **Advanced Threat Protection** option.</span></span>

1. <span data-ttu-id="2104f-154">单击 "**打开**" 按钮以启用高级威胁防护。</span><span class="sxs-lookup"><span data-stu-id="2104f-154">Click the **ON** button to enable Advanced Threat Protection.</span></span>

1. <span data-ttu-id="2104f-155">您可以选择将通知电子邮件的传递位置定义为以分号分隔的电子邮件地址列表。</span><span class="sxs-lookup"><span data-stu-id="2104f-155">You can optionally define where notification emails will be delivered as a list of semicolon separated email addresses.</span></span> <span data-ttu-id="2104f-156">默认情况下会启用**电子邮件服务和协同管理员**, 以将威胁发送给服务管理员。</span><span class="sxs-lookup"><span data-stu-id="2104f-156">**Email service and co-administrators** are enabled by default to send the threats to the service administrators.</span></span>

1. <span data-ttu-id="2104f-157">您可以选择为已收到警报的可疑查询的历史记录指定一个存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2104f-157">You can optionally specify a storage account for historical logging of suspicious queries that have been alerted on.</span></span> <span data-ttu-id="2104f-158">这不是启用高级威胁防护的必要条件, 但对历史跟踪很有用。</span><span class="sxs-lookup"><span data-stu-id="2104f-158">It is not a requirement for enabling Advanced Threat Protection, but can be useful for historical tracking.</span></span> <span data-ttu-id="2104f-159">单击 "**存储详细信息**" 打开 "**存储设置**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="2104f-159">Click **Storage details** to open up the **Storage settings** dialog.</span></span>

1. <span data-ttu-id="2104f-160">在 "**选择存储帐户**" 对话框中, 选择您在上一节中创建的**server<12345>auditing**存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2104f-160">In the **Choose storage account** dialog, select the **server<12345>auditing** storage account you created in the previous section.</span></span> <span data-ttu-id="2104f-161">将其他设置保留为默认值, 然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="2104f-161">Leave the other settings at the default and click **OK**.</span></span>

1. <span data-ttu-id="2104f-162">最后, 选择**威胁检测类型**以快速查看这些类型。</span><span class="sxs-lookup"><span data-stu-id="2104f-162">Finally, select **Threat Detection types** to take a quick look at those.</span></span> <span data-ttu-id="2104f-163">首选选项是 "All", 这是默认设置。</span><span class="sxs-lookup"><span data-stu-id="2104f-163">The preferred option is All, which is the default setting.</span></span>

    <span data-ttu-id="2104f-164">"**全部**" 表示以下值:</span><span class="sxs-lookup"><span data-stu-id="2104f-164">**All** represents the following values:</span></span>
    - <span data-ttu-id="2104f-165">出现 sql 注入攻击的 sql 注入报告;</span><span class="sxs-lookup"><span data-stu-id="2104f-165">SQL injection reports where SQL injections attacks have occurred;</span></span>
    - <span data-ttu-id="2104f-166">sql 注入漏洞报告可能出现 sql 注入的情况。并</span><span class="sxs-lookup"><span data-stu-id="2104f-166">SQL injection vulnerability reports where the possibility of a SQL injection is likely; and</span></span>
    - <span data-ttu-id="2104f-167">反常客户端登录查看异常的登录, 并可能导致问题, 例如, 潜在的攻击者获取访问权限。</span><span class="sxs-lookup"><span data-stu-id="2104f-167">Anomalous client login looks at logins that are irregular and could be cause for concern, such as a potential attacker gaining access.</span></span>

1. <span data-ttu-id="2104f-168">单击 "**保存**" 按钮以应用更改并在服务器上启用高级威胁防护。</span><span class="sxs-lookup"><span data-stu-id="2104f-168">Click the **Save** button to apply the changes and enable Advanced Threat Protection on your server.</span></span>

<span data-ttu-id="2104f-169">我们还需要启用一个数据库级设置, 这就是漏洞评估。</span><span class="sxs-lookup"><span data-stu-id="2104f-169">There is one database-level setting that we'll want to enable as well, and that's the Vulnerability Assessment.</span></span>

1. <span data-ttu-id="2104f-170">导航到您的*marketplace*数据库。</span><span class="sxs-lookup"><span data-stu-id="2104f-170">Navigate to your *marketplace* database.</span></span> <span data-ttu-id="2104f-171">在门户顶部的搜索栏中, 搜索 " **marketplace**", 然后选择门户中的 "数据库"。</span><span class="sxs-lookup"><span data-stu-id="2104f-171">In the search bar at the top of the portal, search for **marketplace**, then select the database in the portal.</span></span>

1. <span data-ttu-id="2104f-172">在左侧菜单中的 "**安全性**" 部分, 选择 "**高级威胁防护**" 选项。</span><span class="sxs-lookup"><span data-stu-id="2104f-172">In the left menu, in the **Security** section, select the **Advanced Threat Protection** option.</span></span>

1. <span data-ttu-id="2104f-173">在 "**漏洞评估**" 框中, 您应该会看到一条消息, 指出 "单击此处可配置存储扫描结果的存储帐户"。</span><span class="sxs-lookup"><span data-stu-id="2104f-173">In the **Vulnerability Assessment** box, you should see a message that says "Click to configure a storage account for storing scan results".</span></span> <span data-ttu-id="2104f-174">若要启用此功能, 您需要执行此操作, 请继续操作, 然后单击进行配置。</span><span class="sxs-lookup"><span data-stu-id="2104f-174">You'll need to do this to enable this feature, so go ahead and click to configure.</span></span>

1. <span data-ttu-id="2104f-175">在 "**选择存储帐户**" 对话框中, 选择您在上一节中创建的**server<12345>auditing**存储帐户。</span><span class="sxs-lookup"><span data-stu-id="2104f-175">In the **Choose storage account** dialog, select the **server<12345>auditing** storage account you created in the previous section.</span></span>

1. <span data-ttu-id="2104f-176">您还可以启用**定期定期扫描**, 以将漏洞评估配置为每周运行一次自动扫描。</span><span class="sxs-lookup"><span data-stu-id="2104f-176">You can also turn on **periodic recurring scans** to configure Vulnerability Assessment to run automatic scans once per week.</span></span> <span data-ttu-id="2104f-177">扫描结果摘要将发送到您提供的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="2104f-177">A scan result summary is sent to the email address(es) you provide.</span></span> <span data-ttu-id="2104f-178">在这种情况下, 我们会将其**关闭**。</span><span class="sxs-lookup"><span data-stu-id="2104f-178">In this case, we'll leave this **OFF**.</span></span> <span data-ttu-id="2104f-179">继续执行, 然后单击顶部的 "**保存**" 以保存设置并启用漏洞评估。</span><span class="sxs-lookup"><span data-stu-id="2104f-179">Go ahead and click **Save** at the top to save your settings and enable Vulnerability Assessment.</span></span>

1. <span data-ttu-id="2104f-180">回到 "主要漏洞评估" 面板中, 继续执行, 然后单击 "**扫描**" 以启动数据库扫描。</span><span class="sxs-lookup"><span data-stu-id="2104f-180">Back in the main Vulnerability Assessment panel, go ahead and click **Scan** to initiate a scan of your database.</span></span> <span data-ttu-id="2104f-181">完成后, 你将看到提高数据库安全性的建议。</span><span class="sxs-lookup"><span data-stu-id="2104f-181">When it's complete, you'll see recommendations to enhance the security of your database.</span></span>

<span data-ttu-id="2104f-182">启用高级威胁防护后, 您将在数据库级别查看详细信息和结果。</span><span class="sxs-lookup"><span data-stu-id="2104f-182">Once Advanced Threat Protection is enabled, you'll view details and results at a database level.</span></span>

<span data-ttu-id="2104f-183">你将收到电子邮件通知, 因为检测到安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="2104f-183">You'll receive email notifications as vulnerabilities are detected.</span></span> <span data-ttu-id="2104f-184">该电子邮件将概述所发生的情况以及要采取的操作。</span><span class="sxs-lookup"><span data-stu-id="2104f-184">The email will outline what occurred and the actions to take.</span></span>

![来自高级威胁防护的示例通知警告](../media/5-email-with-warning.png)

### <a name="data-discovery--classification"></a><span data-ttu-id="2104f-186">数据发现 & 分类</span><span class="sxs-lookup"><span data-stu-id="2104f-186">Data Discovery & Classification</span></span>

<span data-ttu-id="2104f-187">单击 "**数据发现 & 分类**" 面板。</span><span class="sxs-lookup"><span data-stu-id="2104f-187">Click on the **Data Discovery & Classification** panel.</span></span>

<span data-ttu-id="2104f-188">"数据发现 & 分类" 面板显示了需要保护的表中的列。</span><span class="sxs-lookup"><span data-stu-id="2104f-188">The Data Discovery & Classification panel shows columns within your tables that need to be protected.</span></span> <span data-ttu-id="2104f-189">某些列可能包含敏感信息, 或者可能被视为属于不同的国家或地区。</span><span class="sxs-lookup"><span data-stu-id="2104f-189">Some of the columns may have sensitive information or may be considered classified in different countries or regions.</span></span>

![数据发现 & 分类](../media/5-data-discovery-and-classification.png)

<span data-ttu-id="2104f-191">如果有任何列需要配置保护, 则会显示一条消息。</span><span class="sxs-lookup"><span data-stu-id="2104f-191">A message will be displayed if any columns need protection configured.</span></span> <span data-ttu-id="2104f-192">此邮件的格式如下所示: *"我们找到了10个包含分类建议的列"*。</span><span class="sxs-lookup"><span data-stu-id="2104f-192">This message will be formatted like *"We have found 10 columns with classification recommendations"*.</span></span> <span data-ttu-id="2104f-193">您可以单击文本以查看建议。</span><span class="sxs-lookup"><span data-stu-id="2104f-193">You can click on the text to view the recommendations.</span></span>

<span data-ttu-id="2104f-194">通过单击列旁边的复选标记选择要分类的列, 或者选中架构标头左侧的复选框。</span><span class="sxs-lookup"><span data-stu-id="2104f-194">Select the columns that you want to classify by clicking the checkmark next to the column, or select the checkbox to the left of the schema header.</span></span> <span data-ttu-id="2104f-195">选择 "接受所选建议" 选项以应用分类建议。</span><span class="sxs-lookup"><span data-stu-id="2104f-195">Select the Accept selected recommendations options to apply the classification recommendations.</span></span>

<span data-ttu-id="2104f-196">接下来, 您将编辑列, 然后定义数据库的信息类型和敏感度标签。</span><span class="sxs-lookup"><span data-stu-id="2104f-196">Next, you'll edit the columns and then define the information type and the sensitivity label for the database.</span></span> <span data-ttu-id="2104f-197">单击 "保存" 按钮以保存更改。</span><span class="sxs-lookup"><span data-stu-id="2104f-197">Click on the Save button to save the changes.</span></span>

<span data-ttu-id="2104f-198">如果你已成功管理建议, 则不应列出活动建议。</span><span class="sxs-lookup"><span data-stu-id="2104f-198">No active recommendations should be listed once you've managed the recommendations successfully.</span></span>

### <a name="vulnerability-assessment"></a><span data-ttu-id="2104f-199">漏洞评估</span><span class="sxs-lookup"><span data-stu-id="2104f-199">Vulnerability Assessment</span></span>

<span data-ttu-id="2104f-200">单击**漏洞评估**面板中的。</span><span class="sxs-lookup"><span data-stu-id="2104f-200">Click on the **Vulnerability Assessment** panel.</span></span>

![漏洞评估仪表板](../media/5-vulnerability-assessment-dashboard.png)

<span data-ttu-id="2104f-202">漏洞评估列出了数据库的配置问题以及相关的风险。</span><span class="sxs-lookup"><span data-stu-id="2104f-202">The Vulnerability Assessment lists configuration issues on your database and the associated risk.</span></span> <span data-ttu-id="2104f-203">例如, 在上面的图像中, 您可以看到需要设置的服务器级别的防火墙。</span><span class="sxs-lookup"><span data-stu-id="2104f-203">For example, in the image above, you can see the server-level firewall needs to be set up.</span></span>

<span data-ttu-id="2104f-204">单击 "漏洞评估" 面板以查看完整的漏洞列表。</span><span class="sxs-lookup"><span data-stu-id="2104f-204">Click on the Vulnerability Assessment panel to review a full list of vulnerabilities.</span></span> <span data-ttu-id="2104f-205">在这里, 可以单击每个单独的漏洞。</span><span class="sxs-lookup"><span data-stu-id="2104f-205">From here, you can click on each individual vulnerability.</span></span>

<span data-ttu-id="2104f-206">在 "漏洞" 页面上, 您将看到详细信息, 如风险级别、应用于的数据库、安全漏洞的说明以及建议的用于修复问题的补救措施。</span><span class="sxs-lookup"><span data-stu-id="2104f-206">On the vulnerability page you will see the details such as the risk level, which database it applies to, a description of the vulnerability, and the recommended remediation to fix the issue.</span></span> <span data-ttu-id="2104f-207">应用修正以修复问题。</span><span class="sxs-lookup"><span data-stu-id="2104f-207">Apply the remediation to fix the issue or issues.</span></span> <span data-ttu-id="2104f-208">请务必解决所有漏洞。</span><span class="sxs-lookup"><span data-stu-id="2104f-208">Make sure to address all the vulnerabilities.</span></span>

### <a name="threat-detection"></a><span data-ttu-id="2104f-209">威胁检测</span><span class="sxs-lookup"><span data-stu-id="2104f-209">Threat Detection</span></span>

<span data-ttu-id="2104f-210">单击 "**威胁检测**" 面板。</span><span class="sxs-lookup"><span data-stu-id="2104f-210">Click on the **Threat Detection** panel.</span></span>

<span data-ttu-id="2104f-211">这将显示检测到的威胁的列表。</span><span class="sxs-lookup"><span data-stu-id="2104f-211">This displays a list of detected threats.</span></span> <span data-ttu-id="2104f-212">例如, 在此列表中, 可能存在一种潜在的 SQL 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="2104f-212">For example, in this list you one potential SQL injection attacks.</span></span>

![威胁检测](../media/5-threat-detection-dashboard.png)

 <span data-ttu-id="2104f-214">按照建议解决任何问题。</span><span class="sxs-lookup"><span data-stu-id="2104f-214">Address any issues by following the recommendations.</span></span> <span data-ttu-id="2104f-215">对于诸如 SQL 注入警告这样的问题, 您将能够查看查询并向后工作, 以在代码中执行查询。</span><span class="sxs-lookup"><span data-stu-id="2104f-215">For issues such as the SQL injection warnings, you'll be able to look at the query and work backward to where the query is being executed in code.</span></span> <span data-ttu-id="2104f-216">一旦找到, 您应重写代码, 这样它就不再有问题了。</span><span class="sxs-lookup"><span data-stu-id="2104f-216">Once found, you should rewrite the code so it will no longer have the issue.</span></span>