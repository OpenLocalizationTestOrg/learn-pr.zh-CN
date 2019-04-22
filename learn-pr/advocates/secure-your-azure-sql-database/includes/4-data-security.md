<span data-ttu-id="b5fbe-101">_marketplaceDb_数据库存储敏感信息, 如物理地址、电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-101">The _marketplaceDb_ database stores information that is sensitive, such as physical addresses, email addresses, and phone numbers.</span></span> <span data-ttu-id="b5fbe-102">如果暴露, 恶意攻击者可利用此漏洞危害我们的业务或我们的客户。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-102">If exposed, this could be used by malicious attackers to harm our business or our customers.</span></span> <span data-ttu-id="b5fbe-103">让我们来看看如何使用加密和数据掩码来增强数据库的安全性。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-103">Let's look at how we can use encryption and data masking to enhance the security of our database.</span></span>

## <a name="tls-network-encryption"></a><span data-ttu-id="b5fbe-104">TLS 网络加密</span><span class="sxs-lookup"><span data-stu-id="b5fbe-104">TLS network encryption</span></span>

<span data-ttu-id="b5fbe-105">Azure SQL 数据库将对所有连接始终强制执行传输层安全性 (TLS) 加密, 这样可确保在数据库和客户端之间的 "传输" 中加密所有数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-105">Azure SQL Database enforces Transport Layer Security (TLS) encryption at all times for all connections, which ensures all data is encrypted "in transit" between the database and the client.</span></span> <span data-ttu-id="b5fbe-106">通过使用 TLS 加密, 可以确保可能截获应用程序服务器和数据库之间的流量的任何人都无法读取数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-106">By using TLS encryption, you can ensure that anyone who may have intercepted the traffic between the app server and database would not be able to read the data.</span></span> <span data-ttu-id="b5fbe-107">TLS 加密是通过 internet 进行安全通信的标准, 在这种情况下, 可以确保进出 Azure SQL 数据库的网络流量在默认情况下是安全的。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-107">TLS encryption is a standard of securing traffic over the internet, and in this case ensures your network traffic to and from your Azure SQL database is secure by default.</span></span>

## <a name="transparent-data-encryption"></a><span data-ttu-id="b5fbe-108">透明数据加密</span><span class="sxs-lookup"><span data-stu-id="b5fbe-108">Transparent data encryption</span></span>

<span data-ttu-id="b5fbe-109">Azure SQL Database 使用透明数据加密 (TDE) 保护静态数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-109">Azure SQL Database protects your data at rest using transparent data encryption (TDE).</span></span> <span data-ttu-id="b5fbe-110">TDE 对数据库、关联备份和事务日志文件执行实时加密和解密, 而不需要对应用程序进行更改。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-110">TDE performs real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span> <span data-ttu-id="b5fbe-111">使用数据库加密密钥, 透明数据加密会对页面级别的数据执行实时 i/o 加密和解密。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-111">Using a database encryption key, transparent data encryption performs real-time I/O encryption and decryption of the data at the page level.</span></span> <span data-ttu-id="b5fbe-112">每个页面在读取到内存中时进行解密, 然后在写入磁盘之前进行加密。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-112">Each page is decrypted when it's read into memory and then encrypted before being written to disk.</span></span>

<span data-ttu-id="b5fbe-113">默认情况下, 将为所有新部署的 Azure SQL 数据库启用 TDE。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-113">By default, TDE is enabled for all newly deployed Azure SQL databases.</span></span> <span data-ttu-id="b5fbe-114">检查数据加密是否尚未关闭, 并且较旧的 Azure SQL Server 数据库可能未启用 TDE, 这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-114">It's important to check that data encryption hasn’t been turned off, and older Azure SQL Server databases may not have TDE enabled.</span></span>

<span data-ttu-id="b5fbe-115">我们来看一下门户, 其中 TDE 是在我们的_marketplaceDb_数据库上配置的。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-115">Let's take a look in the portal at where TDE is configured on our _marketplaceDb_ database.</span></span>

1. <span data-ttu-id="b5fbe-116">使用与激活沙盒时相同的帐户登录[Azure 门户](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-116">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="b5fbe-117">在门户顶部的搜索栏中, 搜索 " **marketplaceDb**", 然后选择门户中的 "数据库"。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-117">In the search bar at the top of the portal, search for **marketplaceDb**, then select the database in the portal.</span></span>

1. <span data-ttu-id="b5fbe-118">在左侧菜单中的 "**安全性**" 部分, 选择 "**透明数据加密**" 选项。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-118">In the left menu, in the **Security** section, select the **Transparent data encryption** option.</span></span>

1. <span data-ttu-id="b5fbe-119">在 "数据加密" 选项中, 验证是否已将**数据加密**设置为 **"开"**。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-119">In the data encryption option, verify that **Data encryption** is set to **On**.</span></span> <span data-ttu-id="b5fbe-120">您还应看到加密状态为 "已**加密**"。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-120">You should also see an encryption status of **Encrypted**.</span></span>

<span data-ttu-id="b5fbe-121">由于默认情况下会对新数据库进行加密, 因此我们可以确保在创建数据库后, 将在磁盘上加密数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-121">Since new databases are encrypted by default, we can be sure that our data is encrypted on disk from as soon as we create the database.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fbe-122">azure 包含一个名为 azure security Center 的内置服务, 可让你了解环境的安全性 (包括 Azure SQL 数据库)。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-122">Azure includes a built in service called Azure Security Center that gives you visibility into the security of your environment, including Azure SQL databases.</span></span> <span data-ttu-id="b5fbe-123">Azure 安全中心将标记未在其上启用 TDE 的任何数据库, 从而使您能够报告并采取措施来保护您的数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-123">Azure Security Center will flag any databases that don't have TDE enabled on them, giving you the ability to report and take action to secure your data.</span></span>

## <a name="dynamic-data-masking"></a><span data-ttu-id="b5fbe-124">动态数据掩码</span><span class="sxs-lookup"><span data-stu-id="b5fbe-124">Dynamic data masking</span></span>

<span data-ttu-id="b5fbe-125">当我们在上一个单元中运行查询时, 您可能会注意到数据库中的某些信息是敏感的;有一些电话号码、电子邮件地址和其他信息, 我们可能不希望让对数据具有访问权限的每个人完全显示这些信息。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-125">You might have noticed when we ran our query in the previous unit that some of the information in the database is sensitive; there are phone numbers, email addresses, and other information that we may not want to fully display to everyone with access to the data.</span></span>

<span data-ttu-id="b5fbe-126">或许我们不希望用户能够看到完整的电话号码或电子邮件地址, 但我们仍希望让客户服务代表提供可供客户服务代表识别客户的数据的一部分。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-126">Maybe we don't want our users to be able to see the full phone number or email address, but we'd still like to make a portion of the data available for customer service representatives to identify a customer.</span></span> <span data-ttu-id="b5fbe-127">通过使用 Azure SQL 数据库的动态数据掩码功能, 我们可以限制向用户显示的数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-127">By using the dynamic data masking feature of Azure SQL Database, we can limit the data that is displayed to the user.</span></span> <span data-ttu-id="b5fbe-128">动态数据掩码是一种基于策略的安全功能, 可隐藏对指定数据库字段的查询结果集中的敏感数据, 而数据库中的数据不会发生更改。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-128">Dynamic data masking is a policy-based security feature that hides the sensitive data in the result set of a query over designated database fields, while the data in the database is not changed.</span></span>

<span data-ttu-id="b5fbe-129">数据掩码规则包含要对其应用掩码的列, 以及应如何屏蔽数据。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-129">Data masking rules consist of the column to apply the mask to, and how the data should be masked.</span></span> <span data-ttu-id="b5fbe-130">您可以创建自己的掩码格式, 或使用其中一个标准掩码, 例如:</span><span class="sxs-lookup"><span data-stu-id="b5fbe-130">You can create your own masking format, or use one of the standard masks such as:</span></span>

- <span data-ttu-id="b5fbe-131">默认值, 它显示的是该数据类型的默认值。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-131">Default value, which displays the default value for that data type instead.</span></span>
- <span data-ttu-id="b5fbe-132">信用卡值, 仅显示数字的后四个数字, 将所有其他数字转换为小写字母 x。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-132">Credit card value, which only shows the last four digits of the number, converting all other numbers to lower case x’s.</span></span>
- <span data-ttu-id="b5fbe-133">电子邮件, 它会隐藏电子邮件帐户名称的域名和除第一个字符之外的所有字符。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-133">Email, which hides the domain name and all but the first character of the email account name.</span></span>
- <span data-ttu-id="b5fbe-134">数字, 用于指定值范围之间的随机数字。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-134">Number, which specifies a random number between a range of values.</span></span> <span data-ttu-id="b5fbe-135">例如, 在信用卡到期月和年中, 可以选择从1到12的随机月数, 并将年范围设置为2018到3000。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-135">For example, on the credit card expiry month and year, you could select random months from 1 to 12 and set the year range from 2018 to 3000.</span></span>
- <span data-ttu-id="b5fbe-136">自定义字符串。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-136">Custom string.</span></span> <span data-ttu-id="b5fbe-137">这使您可以设置从数据的开头公开的字符数、从数据末尾公开的字符数以及为其余数据重复的字符数。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-137">This allows you to set the number of characters exposed from the start of the data, the number of characters exposed from the end of the data, and the characters to repeat for the remainder of the data.</span></span>

<span data-ttu-id="b5fbe-138">查询列时, 数据库管理员仍将看到原始值, 但非管理员将看到掩码值。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-138">When querying the columns, database administrators will still see the original values, but non-administrators will see the masked values.</span></span> <span data-ttu-id="b5fbe-139">您可以通过将其他用户添加到 "从掩码列表中排除的 SQL 用户" 来查看非屏蔽版本。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-139">You can allow other users to see the non-masked versions by adding them to the SQL users excluded from masking list.</span></span>

<span data-ttu-id="b5fbe-140">让我们来看看这在我们的_marketplaceDb_数据库中是如何工作的。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-140">Let's take a look at how this would work in our _marketplaceDb_ database.</span></span>

1. <span data-ttu-id="b5fbe-141">仍在_marketplaceDb_ "数据库" 面板的门户中, 在左侧菜单中的 "**安全性**" 部分, 选择 " **Dyanmic 数据掩码**"。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-141">While still in the portal on the _marketplaceDb_ database panel, in the **Security** section in the left menu select **Dyanmic Data Masking**.</span></span>

    <span data-ttu-id="b5fbe-142">掩码规则屏幕显示现有动态数据掩码的列表, 以及可能应用了动态数据掩码的列的建议。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-142">The Masking rules screen shows a list of existing dynamic data masks, and recommendations for columns that should potentially have a dynamic data mask applied.</span></span>

    ![显示示例数据库的各个数据库列的建议掩码列表的 Azure 门户屏幕截图。](../media/4-view-recommended-masked-columns.png)

1. <span data-ttu-id="b5fbe-144">让我们为仅显示最后四位数字的电话号码添加一个掩码。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-144">Let's add a mask for the phone number that only displays the last four digits.</span></span> <span data-ttu-id="b5fbe-145">单击顶部的 " **+ 添加掩码**" 按钮以打开 "**添加掩码规则**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-145">Click the **+ Add mask** button at the top to open the **Add masking rule** dialog.</span></span>

1. <span data-ttu-id="b5fbe-146">选择下列值。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-146">Select the following values.</span></span>

    | <span data-ttu-id="b5fbe-147">_設定_</span><span class="sxs-lookup"><span data-stu-id="b5fbe-147">_Setting_</span></span>                | <span data-ttu-id="b5fbe-148">_値_</span><span class="sxs-lookup"><span data-stu-id="b5fbe-148">_Value_</span></span>                                 |
    | ------------------------ | --------------------------------------- |
    | <span data-ttu-id="b5fbe-149">**架构**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-149">**Schema**</span></span>               | <span data-ttu-id="b5fbe-150">SalesLT</span><span class="sxs-lookup"><span data-stu-id="b5fbe-150">SalesLT</span></span>                                 |
    | <span data-ttu-id="b5fbe-151">**Table**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-151">**Table**</span></span>                | <span data-ttu-id="b5fbe-152">客户</span><span class="sxs-lookup"><span data-stu-id="b5fbe-152">Customer</span></span>                                |
    | <span data-ttu-id="b5fbe-153">**Column**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-153">**Column**</span></span>               | <span data-ttu-id="b5fbe-154">电话 (nvarchar)</span><span class="sxs-lookup"><span data-stu-id="b5fbe-154">Phone (nvarchar)</span></span>                        |
    | <span data-ttu-id="b5fbe-155">**掩码字段格式**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-155">**Masking field format**</span></span> | <span data-ttu-id="b5fbe-156">自定义字符串 (前缀 [填充] 后缀)</span><span class="sxs-lookup"><span data-stu-id="b5fbe-156">Custom string (prefix [padding] suffix)</span></span> |
    | <span data-ttu-id="b5fbe-157">**公开的前缀**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-157">**Exposed Prefix**</span></span>       | <span data-ttu-id="b5fbe-158">0</span><span class="sxs-lookup"><span data-stu-id="b5fbe-158">0</span></span>                                       |
    | <span data-ttu-id="b5fbe-159">**填充字符串**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-159">**Padding String**</span></span>       | <span data-ttu-id="b5fbe-160">XXX-XXX-</span><span class="sxs-lookup"><span data-stu-id="b5fbe-160">XXX-XXX-</span></span>                                |
    | <span data-ttu-id="b5fbe-161">**公开的后缀**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-161">**Exposed Suffix**</span></span>       | <span data-ttu-id="b5fbe-162">4</span><span class="sxs-lookup"><span data-stu-id="b5fbe-162">4</span></span>                                       |

    <span data-ttu-id="b5fbe-163">单击 "**添加**" 以添加掩码规则。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-163">Click **Add** to add the masking rule.</span></span>

    ![显示要添加掩码规则的值的 Azure 门户屏幕截图。](../media/4-add-masking-rule.png)

1. <span data-ttu-id="b5fbe-165">让我们再为电子邮件地址添加一个更多的。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-165">Let's add one more for the email address.</span></span> <span data-ttu-id="b5fbe-166">再次单击顶部的 " **+ 添加掩码**" 按钮, 打开 "**添加掩码规则**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-166">Click the **+ Add mask** button at the top again to open up the **Add masking rule** dialog.</span></span>

    | <span data-ttu-id="b5fbe-167">_設定_</span><span class="sxs-lookup"><span data-stu-id="b5fbe-167">_Setting_</span></span>                | <span data-ttu-id="b5fbe-168">_値_</span><span class="sxs-lookup"><span data-stu-id="b5fbe-168">_Value_</span></span>                                 |
    | ------------------------ | --------------------------------------- |
    | <span data-ttu-id="b5fbe-169">**架构**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-169">**Schema**</span></span>               | <span data-ttu-id="b5fbe-170">SalesLT</span><span class="sxs-lookup"><span data-stu-id="b5fbe-170">SalesLT</span></span>                                 |
    | <span data-ttu-id="b5fbe-171">**Table**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-171">**Table**</span></span>                | <span data-ttu-id="b5fbe-172">客户</span><span class="sxs-lookup"><span data-stu-id="b5fbe-172">Customer</span></span>                                |
    | <span data-ttu-id="b5fbe-173">**Column**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-173">**Column**</span></span>               | <span data-ttu-id="b5fbe-174">EmailAddress (nvarchar)</span><span class="sxs-lookup"><span data-stu-id="b5fbe-174">EmailAddress (nvarchar)</span></span>                 |
    | <span data-ttu-id="b5fbe-175">**掩码字段格式**</span><span class="sxs-lookup"><span data-stu-id="b5fbe-175">**Masking field format**</span></span> | <span data-ttu-id="b5fbe-176">电子邮件 (aXXX@XXX.com)</span><span class="sxs-lookup"><span data-stu-id="b5fbe-176">Email (aXXX@XXX.com)</span></span>                    |

    <span data-ttu-id="b5fbe-177">单击 "**添加**" 以添加掩码规则。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-177">Click **Add** to add the masking rule.</span></span>

1. <span data-ttu-id="b5fbe-178">每个新掩码都将添加到掩码规则列表中。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-178">Each new mask will be added to the masking rules list.</span></span> <span data-ttu-id="b5fbe-179">单击 "**保存**" 按钮以应用掩码。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-179">Click the **Save** button to apply the masks.</span></span>

<span data-ttu-id="b5fbe-180">我们来看看这是如何更改我们的查询的。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-180">Let's take a look at how this changes our query.</span></span>

1. <span data-ttu-id="b5fbe-181">现在, 让我们重新登录到数据库, 但作为_ApplicationUser_用户。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-181">Now let's log back in to the database, but as the _ApplicationUser_ user.</span></span>

    ```bash
    sqlcmd -S tcp:server<12345>.database.windows.net,1433 -d marketplaceDb -U 'ApplicationUser' -P '<password>' -N -l 30
    ```

1. <span data-ttu-id="b5fbe-182">运行以下查询。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-182">Run the following query.</span></span>

    ```sql
    SELECT FirstName, LastName, EmailAddress, Phone FROM SalesLT.Customer;
    GO
    ```

    <span data-ttu-id="b5fbe-183">查看如何对输出进行屏蔽。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-183">Look at how the output has been masked.</span></span>

    ```output
    FirstName     LastName      EmailAddress         Phone
    ------------- ------------- -------------------- ------------
    Orlando       Gee           oXXX@XXXX.com        XXX-XXX-0173
    Keith         Harris        kXXX@XXXX.com        XXX-XXX-0127
    Donna         Carreras      dXXX@XXXX.com        XXX-XXX-0130
    Janet         Gates         jXXX@XXXX.com        XXX-XXX-0173
    ...
    ```

<span data-ttu-id="b5fbe-184">使用我们创建的掩码规则, 我们的数据将采用我们指定的格式进行屏蔽。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-184">With the masking rules we created, our data is masked with format that we've specified.</span></span> <span data-ttu-id="b5fbe-185">这允许我们的客户服务代表使用其电话号码的后四位数字来验证客户, 但不需要从代表视图中隐藏完整号码和客户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="b5fbe-185">This allows our customer service reps to verify a customer with the last four digits of their phone number, but hides the full number and the customer's email address from reps view.</span></span>