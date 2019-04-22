<span data-ttu-id="bf7e9-101">对于大多数组织而言, 数据是最有价值和不可替代的资产。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-101">For most organizations, data is the most valuable and irreplaceable asset.</span></span> <span data-ttu-id="bf7e9-102">加密充当分层安全策略中的最新和最强的防御行为。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-102">Encryption serves as the last and strongest line of defense in a layered security strategy.</span></span> 

<span data-ttu-id="bf7e9-103">Contoso 发售知道, 加密是在其离开数据中心并存储在可能会受到攻击或被窃的移动设备上的唯一保护其数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-103">Contoso Shipping knows that encryption is the only protection its data has once it leaves the data center and is stored on mobile devices that could potentially be hacked or stolen.</span></span>

## <a name="what-is-encryption"></a><span data-ttu-id="bf7e9-104">什么是加密？</span><span class="sxs-lookup"><span data-stu-id="bf7e9-104">What is encryption?</span></span>

<span data-ttu-id="bf7e9-105">加密是使数据不可读和不可用的未经授权的查看器的过程。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-105">Encryption is the process of making data unreadable and unusable to unauthorized viewers.</span></span> <span data-ttu-id="bf7e9-106">若要使用或读取加密的数据, 必须对其进行*解密*, 这需要使用密钥。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-106">To use or read the encrypted data, it must be *decrypted*, which requires the use of a secret key.</span></span> <span data-ttu-id="bf7e9-107">有两种顶级加密类型:**对称**和**非对称**。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-107">There are two top-level types of encryption: **symmetric** and **asymmetric**.</span></span>

<span data-ttu-id="bf7e9-108">**对称加密**使用相同的密钥来加密和解密数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-108">**Symmetric encryption** uses the same key to encrypt and decrypt the data.</span></span> <span data-ttu-id="bf7e9-109">考虑桌面密码管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-109">Consider a desktop password manager application.</span></span> <span data-ttu-id="bf7e9-110">输入密码, 并使用你自己的个人密钥加密 (密钥通常是从你的主密码派生的)。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-110">You enter your passwords and they are encrypted with your own personal key (your key is often derived from your master password).</span></span> <span data-ttu-id="bf7e9-111">需要检索数据时, 使用相同的密钥, 并对数据进行解密。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-111">When the data needs to be retrieved, the same key is used, and the data is decrypted.</span></span>

<span data-ttu-id="bf7e9-112">**非对称加密**使用公钥和私钥对。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-112">**Asymmetric encryption** uses a public key and private key pair.</span></span> <span data-ttu-id="bf7e9-113">这两个密钥中的任何一个都可以加密, 但单个密钥无法解密其自己的加密数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-113">Either key can encrypt but a single key can't decrypt its own encrypted data.</span></span> <span data-ttu-id="bf7e9-114">若要进行解密, 您需要配对密钥。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-114">To decrypt, you need the paired key.</span></span> <span data-ttu-id="bf7e9-115">非对称加密用于传输层安全性 (TLS) (在 HTTPS 中使用) 和数据签名等事物。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-115">Asymmetric encryption is used for things like Transport Layer Security (TLS) (used in HTTPS) and data signing.</span></span>

<span data-ttu-id="bf7e9-116">对称加密和非对称加密都在妥善保护数据方面发挥了作用。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-116">Both symmetric and asymmetric encryption play a role in properly securing your data.</span></span> <span data-ttu-id="bf7e9-117">加密通常以两种方式进行:</span><span class="sxs-lookup"><span data-stu-id="bf7e9-117">Encryption is typically approached in two ways:</span></span> 

1. <span data-ttu-id="bf7e9-118">静态加密</span><span class="sxs-lookup"><span data-stu-id="bf7e9-118">Encryption at rest</span></span>
1. <span data-ttu-id="bf7e9-119">传输中的加密</span><span class="sxs-lookup"><span data-stu-id="bf7e9-119">Encryption in transit</span></span>

## <a name="encryption-at-rest"></a><span data-ttu-id="bf7e9-120">静态加密</span><span class="sxs-lookup"><span data-stu-id="bf7e9-120">Encryption at rest</span></span>

<span data-ttu-id="bf7e9-121">rest 上的数据是存储在物理介质上的数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-121">Data at rest is the data that has been stored on a physical medium.</span></span> <span data-ttu-id="bf7e9-122">它可以是存储在服务器磁盘上的数据、存储在数据库中的数据, 也可以是存储在存储帐户中的数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-122">This could be data stored on the disk of a server, data stored in a database, or data stored in a storage account.</span></span> <span data-ttu-id="bf7e9-123">无论采用何种存储机制, 静态数据的加密都可确保在没有解密的密钥和机密的情况下无法读取存储的数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-123">Regardless of the storage mechanism, encryption of data at rest ensures that the stored data is unreadable without the keys and secrets needed to decrypt it.</span></span> <span data-ttu-id="bf7e9-124">如果攻击者要获取带加密数据的硬驱, 并且没有对加密密钥的访问权限, 则攻击者将无法危害数据, 而不会带来极大的困难。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-124">If an attacker was to obtain a hard drive with encrypted data and did not have access to the encryption keys, the attacker would not compromise the data without great difficulty.</span></span>

<span data-ttu-id="bf7e9-125">加密的实际数据在组织的内容、使用情况和重要性方面有所不同。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-125">The actual data that is encrypted could vary in its content, usage, and importance to the organization.</span></span> <span data-ttu-id="bf7e9-126">这可能是由业务开发的商业、知识产权、企业开发的个人数据、企业存储的客户或员工的个人数据以及用于加密数据本身的密钥和机密的关键信息。.</span><span class="sxs-lookup"><span data-stu-id="bf7e9-126">This could be financial information critical to the business, intellectual property that has been developed by the business, personal data about customers or employees that the business stores, and even the keys and secrets used for the encryption of the data itself.</span></span>

<span data-ttu-id="bf7e9-127">下面的图表显示了已加密的客户数据可能与数据库中的相似之处。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-127">Here's a diagram that shows what encrypted customer data might look like as it sits in a database.</span></span>

![显示静态加密示例的插图。](../media/encryption-at-rest.png)

## <a name="encryption-in-transit"></a><span data-ttu-id="bf7e9-130">传输中的加密</span><span class="sxs-lookup"><span data-stu-id="bf7e9-130">Encryption in transit</span></span>

<span data-ttu-id="bf7e9-131">传输中的数据是主动从一个位置移动到另一个位置 (例如跨 internet 或通过专用网络) 的数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-131">Data in transit is the data actively moving from one location to another, such as across the internet or through a private network.</span></span> <span data-ttu-id="bf7e9-132">安全传输可由多个不同的层处理。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-132">Secure transfer can be handled by several different layers.</span></span> <span data-ttu-id="bf7e9-133">在通过网络发送应用层上的数据之前, 可以通过对其加密来实现。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-133">It could be done by encrypting the data at the application layer prior to sending it over a network.</span></span> <span data-ttu-id="bf7e9-134">HTTPS 是中转加密中的应用程序层的一个示例。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-134">HTTPS is an example of application layer in transit encryption.</span></span>

<span data-ttu-id="bf7e9-135">您还可以在网络层设置安全通道 (如虚拟专用网络 (VPN)), 以在两个系统之间传输数据。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-135">You can also set up a secure channel, like a virtual private network (VPN), at a network layer, to transmit data between two systems.</span></span>

<span data-ttu-id="bf7e9-136">在传输过程中加密数据保护来自外部观察器的数据, 并提供传输数据的机制, 同时限制暴露风险。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-136">Encrypting data in transit protects the data from outside observers and provides a mechanism to transmit data while limiting risk of exposure.</span></span>

<span data-ttu-id="bf7e9-137">此图显示了该过程。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-137">This diagram shows the process.</span></span> <span data-ttu-id="bf7e9-138">在这里, 客户数据在通过网络发送时进行加密。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-138">Here, customer data is encrypted as it's sent over the network.</span></span> <span data-ttu-id="bf7e9-139">只有收件人具有可将数据解密为可用表单的密钥。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-139">Only the receiver has the secret key that can decrypt the data to a usable form.</span></span>

![显示传输过程中加密示例的插图。](../media/encryption-in-transit.png)

## <a name="encryption-on-azure"></a><span data-ttu-id="bf7e9-143">Azure 上的加密</span><span class="sxs-lookup"><span data-stu-id="bf7e9-143">Encryption on Azure</span></span>

<span data-ttu-id="bf7e9-144">让我们看一下 Azure 允许您跨服务加密数据的一些方法。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-144">Let's take a look at some ways that Azure enables you to encrypt data across services.</span></span>

:::row:::
  :::column:::
    ![表示加密存储的图像](../media/4-encrypt-raw-storage.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="bf7e9-146">**加密原始存储**</span><span class="sxs-lookup"><span data-stu-id="bf7e9-146">**Encrypt raw storage**</span></span>

<span data-ttu-id="bf7e9-147">静态数据的**Azure 存储服务加密**可帮助您保护数据, 以满足组织的安全和合规性承诺。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-147">**Azure Storage Service Encryption** for data at rest helps you protect your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="bf7e9-148">使用此功能, azure 存储平台会在将数据保留到 azure 托管磁盘、azure Blob 存储、azure 文件或 azure 队列存储之前自动对数据进行加密, 并在检索之前对数据进行解密。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-148">With this feature, the Azure storage platform automatically encrypts your data before persisting it to Azure Managed Disks, Azure Blob storage, Azure Files, or Azure Queue storage, and decrypts the data before retrieval.</span></span> <span data-ttu-id="bf7e9-149">对使用服务的应用程序而言, 对加密、静态加密、解密和存储服务加密中的密钥管理的处理是透明的。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-149">The handling of encryption, encryption at rest, decryption, and key management in Storage Service Encryption is transparent to applications using the services.</span></span>

  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![表示加密虚拟机的图像](../media/4-encrypt-virtual-machines.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="bf7e9-151">**加密虚拟机磁盘**</span><span class="sxs-lookup"><span data-stu-id="bf7e9-151">**Encrypt virtual machine disks**</span></span>

<span data-ttu-id="bf7e9-152">Storage Service encryption 为写入物理磁盘的数据提供低级别加密保护, 但如何保护虚拟机的虚拟硬盘 (vhd)？</span><span class="sxs-lookup"><span data-stu-id="bf7e9-152">Storage Service Encryption provides low-level encryption protection for data written to physical disk, but how do you protect the virtual hard disks (VHDs) of virtual machines?</span></span> <span data-ttu-id="bf7e9-153">如果恶意攻击者获得了对你的 Azure 订阅的访问权限并获取了虚拟机的 vhd, 你如何确保他们无法访问存储的数据？</span><span class="sxs-lookup"><span data-stu-id="bf7e9-153">If malicious attackers gained access to your Azure subscription and got the VHDs of your virtual machines, how would you ensure they would be unable to access the stored data?</span></span>
  :::column-end:::
:::row-end:::

<span data-ttu-id="bf7e9-154">**Azure 磁盘加密**是一种可帮助您加密 Windows 和 Linux IaaS 虚拟机磁盘的功能。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-154">**Azure Disk Encryption** is a capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="bf7e9-155">Azure 磁盘加密利用 Windows 的行业标准 BitLocker 功能和 Linux 的 dm crypt 功能为 OS 和数据磁盘提供卷加密。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-155">Azure Disk Encryption leverages the industry-standard BitLocker feature of Windows and the dm-crypt feature of Linux to provide volume encryption for the OS and data disks.</span></span> <span data-ttu-id="bf7e9-156">此解决方案与 Azure Key Vault 集成, 可帮助您控制和管理磁盘加密密钥和密码 (您可以使用托管服务标识来访问密钥存储库)。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-156">The solution is integrated with Azure Key Vault to help you control and manage the disk encryption keys and secrets (and you can use managed service identities for accessing Key Vault).</span></span>

<span data-ttu-id="bf7e9-157">对于 Contoso 货运, 使用 vm 是第一次转向云的情况。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-157">For Contoso Shipping, using VMs was one of the first moves toward the cloud.</span></span> <span data-ttu-id="bf7e9-158">将所有 vhd 加密都是一种非常简单、低影响的方式, 以确保您能够确保贵公司的数据的安全。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-158">Having all the VHDs encrypted is a very easy, low-impact way to ensure that you are doing all you can to secure your company's data.</span></span>

:::row:::
  :::column:::
    ![表示加密数据库的图像](../media/4-encrypt-databases.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="bf7e9-160">**加密数据库**</span><span class="sxs-lookup"><span data-stu-id="bf7e9-160">**Encrypt databases**</span></span>

<span data-ttu-id="bf7e9-161">**透明数据加密 (TDE)** 可帮助保护 azure SQL 数据库和 azure 数据仓库不受恶意活动的威胁。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-161">**Transparent data encryption (TDE)** helps protect Azure SQL Database and Azure Data Warehouse against the threat of malicious activity.</span></span> <span data-ttu-id="bf7e9-162">它对数据库执行实时加密和解密, 关联的备份和事务日志文件不需要对应用程序进行更改。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-162">It performs real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span> <span data-ttu-id="bf7e9-163">默认情况下, 将为所有新部署的 Azure SQL 数据库实例启用 TDE。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-163">By default, TDE is enabled for all newly deployed Azure SQL Database instances.</span></span>

  :::column-end:::
:::row-end:::

<span data-ttu-id="bf7e9-164">TDE 通过使用名为数据库加密密钥的对称密钥来加密整个数据库的存储。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-164">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="bf7e9-165">默认情况下, Azure 为每个逻辑 SQL Server 实例提供唯一的加密密钥, 并处理所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-165">By default, Azure provides a unique encryption key per logical SQL Server instance and handles all the details.</span></span> <span data-ttu-id="bf7e9-166">使用 Azure key Vault 中存储的密钥 (如下所示) 也支持带您自己的密钥 (BYOK)。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-166">Bring your own key (BYOK) is also supported with keys stored in Azure Key Vault (see below).</span></span>

<span data-ttu-id="bf7e9-167">由于默认情况下启用 TDE, 因此您确信 Contoso 发售对存储在公司数据库中的数据进行了适当的保护。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-167">Because TDE is enabled by default, you are confident that Contoso Shipping has the proper protections in place for data stored in the company's databases.</span></span>

:::row:::
  :::column:::
    ![表示加密机密的图像](../media/4-encrypt-secrets.png)
  :::column-end:::
    :::column span="3":::  
<span data-ttu-id="bf7e9-169">**加密机密**</span><span class="sxs-lookup"><span data-stu-id="bf7e9-169">**Encrypt secrets**</span></span>

<span data-ttu-id="bf7e9-170">我们已发现加密服务都使用密钥来加密和解密数据, 因此我们如何确保密钥本身是安全的？</span><span class="sxs-lookup"><span data-stu-id="bf7e9-170">We've seen that the encryption services all use keys to encrypt and decrypt data, so how do we ensure that the keys themselves are secure?</span></span> <span data-ttu-id="bf7e9-171">公司还可能有需要安全存储的密码、连接字符串或其他敏感信息片段。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-171">Corporations may also have passwords, connection strings, or other sensitive pieces of information that they need to securely store.</span></span> <span data-ttu-id="bf7e9-172">在 azure 中, 我们可以使用**azure Key Vault**来保护我们的机密。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-172">In Azure, we can use **Azure Key Vault** to protect our secrets.</span></span>

  :::column-end:::
:::row-end:::

<span data-ttu-id="bf7e9-173">Azure Key Vault 是用于存储应用程序机密的集中式云服务。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-173">Azure Key Vault is a centralized cloud service for storing your application secrets.</span></span> <span data-ttu-id="bf7e9-174">密钥存储库通过将应用程序的机密保存在单个中心位置, 并提供安全访问、权限控制和访问日志功能, 来帮助您控制这些机密。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-174">Key Vault helps you control your applications' secrets by keeping them in a single, central location and by providing secure access, permissions control, and access logging capabilities.</span></span> <span data-ttu-id="bf7e9-175">它适用于各种情况:</span><span class="sxs-lookup"><span data-stu-id="bf7e9-175">It is useful for a variety of scenarios:</span></span>

- <span data-ttu-id="bf7e9-176">*机密管理*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-176">*Secrets management*.</span></span> <span data-ttu-id="bf7e9-177">您可以使用密钥存储库来安全地存储和严格控制对令牌、密码、证书、*应用程序编程接口*(API) 密钥和其他机密的访问。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-177">You can use Key Vault to securely store and tightly control access to tokens, passwords, certificates, *Application Programming Interface* (API) keys, and other secrets.</span></span>
- <span data-ttu-id="bf7e9-178">*密钥管理*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-178">*Key management*.</span></span> <span data-ttu-id="bf7e9-179">您还可以使用密钥存储库作为密钥管理解决方案。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-179">You also can use Key Vault as a key management solution.</span></span> <span data-ttu-id="bf7e9-180">使用密钥存储库, 可以更轻松地创建和控制用于加密数据的加密密钥。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-180">Key Vault makes it easier to create and control the encryption keys used to encrypt your data.</span></span>
- <span data-ttu-id="bf7e9-181">*证书管理*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-181">*Certificate management*.</span></span> <span data-ttu-id="bf7e9-182">利用密钥存储库, 您可以更轻松地为您的 Azure 设置、管理和部署公用和私人*安全套接字层/传输层安全性*(SSL/TLS) 证书, 以及内部连接的资源。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-182">Key Vault lets you provision, manage, and deploy your public and private *Secure Sockets Layer/ Transport Layer Security* (SSL/ TLS) certificates for your Azure, and internally connected, resources more easily.</span></span>
- <span data-ttu-id="bf7e9-183">*存储硬件安全模块支持的机密*(hsm)。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-183">*Store secrets backed by hardware security modules* (HSMs).</span></span> <span data-ttu-id="bf7e9-184">机密和密钥可通过软件或 FIPS 140-2 级别2验证的 hsm 进行保护。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-184">The secrets and keys can be protected either by software, or by FIPS 140-2 Level 2 validated HSMs.</span></span>

<span data-ttu-id="bf7e9-185">使用密钥存储库的好处包括:</span><span class="sxs-lookup"><span data-stu-id="bf7e9-185">The benefits of using Key Vault include:</span></span>

- <span data-ttu-id="bf7e9-186">*集中式应用程序密码*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-186">*Centralized application secrets*.</span></span> <span data-ttu-id="bf7e9-187">通过将存储用于应用程序机密, 可以控制分发, 并降低秘密可能意外泄露的机会。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-187">Centralizing storage for application secrets allows you to control their distribution, and reduces the chances that secrets may be accidentally leaked.</span></span>
- <span data-ttu-id="bf7e9-188">*安全存储的机密和密钥*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-188">*Securely stored secrets and keys*.</span></span> <span data-ttu-id="bf7e9-189">Azure 使用行业标准算法、密钥长度和 hsm, 并且访问需要正确的身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-189">Azure uses industry-standard algorithms, key lengths, and HSMs, and access requires proper authentication and authorization.</span></span>
- <span data-ttu-id="bf7e9-190">*监视访问和使用*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-190">*Monitor access and use*.</span></span> <span data-ttu-id="bf7e9-191">使用密钥存储库, 您可以监视和控制对公司密码的访问。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-191">Using Key Vault, you can monitor and control access to company secrets.</span></span>
- <span data-ttu-id="bf7e9-192">*简化了对应用程序密码的管理*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-192">*Simplified administration of application secrets*.</span></span> <span data-ttu-id="bf7e9-193">密钥存储库可以更轻松地从公共证书颁发机构 (ca) 注册和续订证书。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-193">Key Vault makes it easier to enroll and renew certificates from public Certificate Authorities (CAs).</span></span> <span data-ttu-id="bf7e9-194">您还可以扩展和复制区域中的内容, 并使用标准证书管理工具。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-194">You can also scale up and replicate content within regions, and use standard certificate management tools.</span></span>
- <span data-ttu-id="bf7e9-195">*与其他 Azure 服务集成*。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-195">*Integrate with other Azure services*.</span></span> <span data-ttu-id="bf7e9-196">你可以将关键保管库与存储帐户、容器注册表、事件中心和更多 Azure 服务集成。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-196">You can integrate Key Vault with storage accounts, container registries, event hubs and many more Azure services.</span></span>

<span data-ttu-id="bf7e9-197">由于可以向 azure AD 标识授予使用 azure Key Vault 密码的访问权限, 因此启用了托管服务标识的应用程序可以自动并无缝地获取所需的密码。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-197">Because Azure AD identities can be granted access to use Azure Key Vault secrets, applications with managed service identities enabled can automatically and seamlessly acquire the secrets they need.</span></span>

## <a name="summary"></a><span data-ttu-id="bf7e9-198">摘要</span><span class="sxs-lookup"><span data-stu-id="bf7e9-198">Summary</span></span>

<span data-ttu-id="bf7e9-199">您可能知道, 加密通常是攻击者的最后一层防御, 是用于保护系统的一种重要的层次方法。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-199">As you may know, encryption is often the last layer of defense from attackers and is an important piece of a layered approach to securing your systems.</span></span> <span data-ttu-id="bf7e9-200">Azure 提供了内置功能和服务, 可对数据进行加密和保护以防意外暴露。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-200">Azure provides built-in capabilities and services to encrypt and protect data from unintended exposure.</span></span> <span data-ttu-id="bf7e9-201">对存储在 Azure 服务中的客户数据的保护对于 Microsoft 来说是极其重要的, 并且应包括在任何设计中。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-201">Protection of customer data stored within Azure services is of paramount importance to Microsoft and should be included in any design.</span></span> <span data-ttu-id="bf7e9-202">基础服务 (如 azure 存储、azure 虚拟机、azure SQL 数据库和 Azure Key Vault) 可以通过加密来保护环境。</span><span class="sxs-lookup"><span data-stu-id="bf7e9-202">Foundational services such as Azure Storage, Azure Virtual Machines, Azure SQL Database, and Azure Key Vault can help secure your environment through encryption.</span></span>
