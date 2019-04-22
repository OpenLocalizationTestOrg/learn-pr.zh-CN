<span data-ttu-id="96b54-101">您需要确保您可以使用跨公共 Internet 的加密隧道将环境中的客户端或站点连接到 Azure。</span><span class="sxs-lookup"><span data-stu-id="96b54-101">You want to ensure that you can connect clients or sites within your environment into Azure using encrypted tunnels across the public Internet.</span></span> <span data-ttu-id="96b54-102">在此单位中, 您将创建一个点到站点 VPN 网关, 然后从客户端计算机连接到该网关。</span><span class="sxs-lookup"><span data-stu-id="96b54-102">In this unit, you'll create a point-to-site VPN gateway, and then connect to that gateway from your client computer.</span></span> <span data-ttu-id="96b54-103">你将使用本机 Azure 证书身份验证连接来实现安全性。</span><span class="sxs-lookup"><span data-stu-id="96b54-103">You'll use native Azure certificate authentication connections for security.</span></span>

<span data-ttu-id="96b54-104">您将执行以下过程:</span><span class="sxs-lookup"><span data-stu-id="96b54-104">You will carry out the following process:</span></span>

1. <span data-ttu-id="96b54-105">创建 RouteBased VPN 网关。</span><span class="sxs-lookup"><span data-stu-id="96b54-105">Create a RouteBased VPN gateway.</span></span>

1. <span data-ttu-id="96b54-106">为进行身份验证而上载根证书的公钥。</span><span class="sxs-lookup"><span data-stu-id="96b54-106">Upload the public key for a root certificate for authentication purposes.</span></span>

1. <span data-ttu-id="96b54-107">从根证书生成客户端证书, 然后在每台将连接到虚拟网络以进行身份验证的客户端计算机上安装客户端证书。</span><span class="sxs-lookup"><span data-stu-id="96b54-107">Generate a client certificate from the root certificate, and then install the client certificate on each client computer that will connect to the virtual network for authentication purposes.</span></span>

1. <span data-ttu-id="96b54-108">创建 VPN 客户端配置文件, 其中包含客户端连接到虚拟网络所需的信息。</span><span class="sxs-lookup"><span data-stu-id="96b54-108">Create VPN client configuration files, which contain the necessary information for the client to connect to the virtual network.</span></span>

## <a name="setup"></a><span data-ttu-id="96b54-109">安装程序</span><span class="sxs-lookup"><span data-stu-id="96b54-109">Setup</span></span>

<span data-ttu-id="96b54-110">若要完成此模块, 你将使用本地 Windows 10 计算机上的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="96b54-110">To complete this module, you will use Azure PowerShell from your local Windows 10 computer.</span></span>

<span data-ttu-id="96b54-111">我们将首先设置创建虚拟网络时要使用的变量。</span><span class="sxs-lookup"><span data-stu-id="96b54-111">We'll start by setting up variables to be used when we create a virtual network.</span></span> <span data-ttu-id="96b54-112">打开新的 PowerShell 会话并创建以下变量:</span><span class="sxs-lookup"><span data-stu-id="96b54-112">Open a new PowerShell session and create the following variables:</span></span>

```PowerShell
$VNetName  = "VNetData"
$FESubName = "FrontEnd"
$BESubName = "Backend"
$GWSubName = "GatewaySubnet"
$VNetPrefix1 = "192.168.0.0/16"
$VNetPrefix2 = "10.254.0.0/16"
$FESubPrefix = "192.168.1.0/24"
$BESubPrefix = "10.254.1.0/24"
$GWSubPrefix = "192.168.200.0/26"
$VPNClientAddressPool = "172.16.201.0/24"
$ResourceGroup = "VpnGatewayDemo"
$Location = "East US"
$GWName = "VNetDataGW"
$GWIPName = "VNetDataGWPIP"
$GWIPconfName = "gwipconf"
```

## <a name="configure-a-virtual-network"></a><span data-ttu-id="96b54-113">配置虚拟网络</span><span class="sxs-lookup"><span data-stu-id="96b54-113">Configure a virtual network</span></span>

1. <span data-ttu-id="96b54-114">创建资源组。</span><span class="sxs-lookup"><span data-stu-id="96b54-114">Create a resource group.</span></span>

    ```PowerShell
    New-AzResourceGroup -Name $ResourceGroup -Location $Location
    ```

1. <span data-ttu-id="96b54-115">为虚拟网络创建子网配置。</span><span class="sxs-lookup"><span data-stu-id="96b54-115">Create subnet configurations for the virtual network.</span></span> <span data-ttu-id="96b54-116">它们具有名称**前端、后端**和**GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="96b54-116">These have the name **FrontEnd, BackEnd**, and **GatewaySubnet**.</span></span> <span data-ttu-id="96b54-117">所有这些子网都存在于虚拟网络前缀中。</span><span class="sxs-lookup"><span data-stu-id="96b54-117">All of these subnets exist within the virtual network prefix.</span></span>

    ```PowerShell
    $fesub = New-AzVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
    $besub = New-AzVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
    $gwsub = New-AzVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
    ```

1. <span data-ttu-id="96b54-118">接下来, 使用子网值和静态 DNS 服务器创建虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="96b54-118">Next, create the virtual network using the subnet values and a static DNS server.</span></span>

    ```PowerShell
    New-AzVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroup -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
    ```

1. <span data-ttu-id="96b54-119">现在, 为此网络指定您刚刚创建的变量。</span><span class="sxs-lookup"><span data-stu-id="96b54-119">Now specify the variables for this network that you have just created.</span></span>

    ```PowerShell
    $vnet = Get-AzVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroup
    $subnet = Get-AzVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    ```

1. <span data-ttu-id="96b54-120">请求动态分配的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="96b54-120">Request a dynamically assigned public IP address.</span></span>

    ```PowerShell
    $pip = New-AzPublicIpAddress -Name $GWIPName -ResourceGroupName $ResourceGroup -Location $Location -AllocationMethod Dynamic
    $ipconf = New-AzVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
    ```

## <a name="create-the-vpn-gateway"></a><span data-ttu-id="96b54-121">创建 VPN 网关</span><span class="sxs-lookup"><span data-stu-id="96b54-121">Create the VPN gateway</span></span>

<span data-ttu-id="96b54-122">创建此 VPN 网关时:</span><span class="sxs-lookup"><span data-stu-id="96b54-122">When creating this VPN gateway:</span></span>

- <span data-ttu-id="96b54-123">GatewayType 必须是 Vpn</span><span class="sxs-lookup"><span data-stu-id="96b54-123">GatewayType must be Vpn</span></span>
- <span data-ttu-id="96b54-124">VpnType 必须是 RouteBased</span><span class="sxs-lookup"><span data-stu-id="96b54-124">VpnType must be RouteBased</span></span>

> [!NOTE]
> <span data-ttu-id="96b54-125">请注意, 这部分练习可能需要长达45分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="96b54-125">Note that this part of the exercise can take up to 45 minutes to complete.</span></span>

1. <span data-ttu-id="96b54-126">若要创建 VPN 网关, 请运行以下命令, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="96b54-126">To create the VPN gateway, run the following command and press Enter.</span></span>

    ```PowerShell
    New-AzVirtualNetworkGateway -Name $GWName -ResourceGroupName $ResourceGroup `
      -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
      -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
    ```

1. <span data-ttu-id="96b54-127">等待命令输出显示。</span><span class="sxs-lookup"><span data-stu-id="96b54-127">Wait for the command output to appear.</span></span>

## <a name="add-the-vpn-client-address-pool"></a><span data-ttu-id="96b54-128">添加 VPN 客户端地址池</span><span class="sxs-lookup"><span data-stu-id="96b54-128">Add the VPN client address pool</span></span>

1. <span data-ttu-id="96b54-129">运行以下命令并按 enter 键。</span><span class="sxs-lookup"><span data-stu-id="96b54-129">Run the following command and press Enter.</span></span>

    ```PowerShell
    $Gateway = Get-AzVirtualNetworkGateway -ResourceGroupName $ResourceGroup -Name $GWName
    Set-AzVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
    ```

1. <span data-ttu-id="96b54-130">等待命令输出显示。</span><span class="sxs-lookup"><span data-stu-id="96b54-130">Wait for the command output to appear.</span></span>

## <a name="generate-a-client-certificate"></a><span data-ttu-id="96b54-131">生成客户端证书</span><span class="sxs-lookup"><span data-stu-id="96b54-131">Generate a client certificate</span></span>

<span data-ttu-id="96b54-132">在 Azure 上创建的网络基础结构, 我们需要在本地计算机上创建自签名客户端证书。</span><span class="sxs-lookup"><span data-stu-id="96b54-132">With the network infrastructure created on Azure, we need to create a self-signed client certificate on our local machine.</span></span> <span data-ttu-id="96b54-133">这在大多数操作系统上都可以这样做, 但我们将介绍如何在 windows 10 上使用 Azure powershell 模块和 Windows**证书管理器**实用工具生成客户端证书。</span><span class="sxs-lookup"><span data-stu-id="96b54-133">This can be done similarly on most operating systems, but we will cover how to generate your client certificate on Windows 10 using PowerShell with the Azure PowerShell module and the Windows **Certificate Manager** utility.</span></span>

1. <span data-ttu-id="96b54-134">我们的第一步是创建自签名根证书。</span><span class="sxs-lookup"><span data-stu-id="96b54-134">Our first step is to create the self-signed root certificate.</span></span> <span data-ttu-id="96b54-135">运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="96b54-135">Run the following command.</span></span>

    ```PowerShell
    $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
    -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
    ```

1. <span data-ttu-id="96b54-136">接下来, 生成由新的根证书签名的客户端证书。</span><span class="sxs-lookup"><span data-stu-id="96b54-136">Next, generate a client certificate signed by your new root certificate.</span></span>

    ```PowerShell
    New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
    -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
    ```

<span data-ttu-id="96b54-137">生成证书后, 我们需要导出根证书的公钥。</span><span class="sxs-lookup"><span data-stu-id="96b54-137">With our certificates generated, we need to export our root certificate's public key.</span></span>

1. <span data-ttu-id="96b54-138">从`certmgr` PowerShell 运行以打开证书管理器。</span><span class="sxs-lookup"><span data-stu-id="96b54-138">Run `certmgr` from PowerShell to open the Certificate Manager.</span></span>

1. <span data-ttu-id="96b54-139">导航到 "**个人** > **证书**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-139">Navigate to **Personal** > **Certificates**.</span></span> <span data-ttu-id="96b54-140">查找并右键单击列表中的**P2SRootCert**证书, 并选择 "**所有任务** > **导出 ...**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-140">Find and right-click the **P2SRootCert** certificate in the list and select **All tasks** > **Export...**.</span></span>

1. <span data-ttu-id="96b54-141">在 "证书导出向导" 中, 单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-141">In the Certificate Export Wizard, click **Next**.</span></span>

1. <span data-ttu-id="96b54-142">确保选中 "不 **, 不导出私钥**", 然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-142">Ensure that **No, do not export the private key** is selected, and then click **Next**.</span></span>

1. <span data-ttu-id="96b54-143">在 "**导出文件格式**" 页上, 确保以**64 编码的 x.509 (。CER)** , 然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-143">On the **Export File Format** page, ensure that **Base-64 encoded X.509 (.CER)** is selected, and then click **Next**.</span></span>

1. <span data-ttu-id="96b54-144">在 "**要导出的文件**" 页\*\*\*\* 上的 "文件名" 下, 导航到要记住的位置并将该文件另存为**P2SRootCert**, 然后单击 "下一步"。</span><span class="sxs-lookup"><span data-stu-id="96b54-144">In the **File to Export** page, under **File name**, navigate to a location you'll remember and save the file as **P2SRootCert.cer**, and then click Next.</span></span>

1. <span data-ttu-id="96b54-145">在 "**正在完成证书导出向导**" 页上, 单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-145">On the **Completing the Certificate Export Wizard** page, click **Finish**.</span></span>

1. <span data-ttu-id="96b54-146">在 "**证书导出向导**" 消息框中, 单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="96b54-146">On the **Certificate Export Wizard** message box, click **OK**.</span></span>

## <a name="upload-the-root-certificate-public-key-information"></a><span data-ttu-id="96b54-147">上传根证书公钥信息</span><span class="sxs-lookup"><span data-stu-id="96b54-147">Upload the root certificate public key information</span></span>

1. <span data-ttu-id="96b54-148">在 PowerShell 窗口中, 执行以下命令来声明证书名称的变量:</span><span class="sxs-lookup"><span data-stu-id="96b54-148">In the PowerShell window, execute the following command to declare a variable for the certificate name:</span></span>

    ```PowerShell
    $P2SRootCertName = "P2SRootCert.cer"
    ```

1. <span data-ttu-id="96b54-149">将`<cert-path>`占位符替换为您的根证书的导出位置, 并执行以下命令:</span><span class="sxs-lookup"><span data-stu-id="96b54-149">Replace the `<cert-path>` placeholder with the export location of your root certificate and execute the following command:</span></span>

    ```PowerShell
    $filePathForCert = "<cert-path>\P2SRootCert.cer"
    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
    $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
    $p2srootcert = New-AzVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
    ```

1. <span data-ttu-id="96b54-150">在设置组名称后, 使用以下命令将证书上传到 Azure。</span><span class="sxs-lookup"><span data-stu-id="96b54-150">With the group name set, upload the certificate to Azure with the following command.</span></span>

    ```PowerShell
    Add-AzVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname $GWName -ResourceGroupName $ResourceGroup -PublicCertData $CertBase64
    ```

    <span data-ttu-id="96b54-151">Azure 现在将此证书识别为虚拟网络的受信任根证书。</span><span class="sxs-lookup"><span data-stu-id="96b54-151">Azure will now recognize this certificate as a trusted root certificate for our virtual network.</span></span>

## <a name="configure-the-native-vpn-client"></a><span data-ttu-id="96b54-152">配置本机 VPN 客户端</span><span class="sxs-lookup"><span data-stu-id="96b54-152">Configure the native VPN client</span></span>

1. <span data-ttu-id="96b54-153">执行以下命令以在中创建 VPN 客户端配置文件。ZIP 格式。</span><span class="sxs-lookup"><span data-stu-id="96b54-153">Execute the following command to create VPN client configuration files in .ZIP format.</span></span>

    ```PowerShell
    $profile = New-AzVpnClientConfiguration -ResourceGroupName $ResourceGroup -Name $GWName -AuthenticationMethod "EapTls"
    $profile.VPNProfileSASUrl
    ```

1. <span data-ttu-id="96b54-154">复制此命令的输出中返回的 URL, 并将其粘贴到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="96b54-154">Copy the URL returned in the output from this command and paste it into your browser.</span></span> <span data-ttu-id="96b54-155">你的浏览器应开始下载。ZIP 文件。</span><span class="sxs-lookup"><span data-stu-id="96b54-155">Your browser should start downloading a .ZIP file.</span></span> <span data-ttu-id="96b54-156">提取存档内容并将其放在合适的位置。</span><span class="sxs-lookup"><span data-stu-id="96b54-156">Extract the archive contents and put them in a suitable location.</span></span>

    > [!NOTE]
    > <span data-ttu-id="96b54-157">某些浏览器最初将尝试阻止下载此 ZIP 文件作为危险下载。</span><span class="sxs-lookup"><span data-stu-id="96b54-157">Some browsers will initially attempt to block downloading this ZIP file as a dangerous download.</span></span> <span data-ttu-id="96b54-158">您将需要在浏览器中覆盖此内容, 以便能够提取存档内容。</span><span class="sxs-lookup"><span data-stu-id="96b54-158">You will need to override this in your browser to be able to extract the archive contents.</span></span>

1. <span data-ttu-id="96b54-159">在提取的文件夹中, 导航到 " **WindowsAmd64** " 文件夹 (适用于64位 Windows 计算机) 或 " **WindowsX86** " 文件夹 (针对32位计算机)。</span><span class="sxs-lookup"><span data-stu-id="96b54-159">In the extracted folder, navigate to either the **WindowsAmd64** folder (for 64-bit Windows computers) or the **WindowsX86** folder (for 32-bit computers).</span></span>

    > [!NOTE]
    > <span data-ttu-id="96b54-160">如果要在非 Windows 计算机上配置 VPN, 可以使用**通用**文件夹中的证书和设置文件。</span><span class="sxs-lookup"><span data-stu-id="96b54-160">If you want to configure a VPN on a non-Windows machine, you can use the certificate and settings files from the **Generic** folder.</span></span>

1. <span data-ttu-id="96b54-161">双击**VpnClientSetup {体系结构} .exe**文件, 并反映您的`{architecture}`体系结构。</span><span class="sxs-lookup"><span data-stu-id="96b54-161">Double-click on the **VpnClientSetup{architecture}.exe** file, with `{architecture}` reflecting your architecture.</span></span>

1. <span data-ttu-id="96b54-162">在 " **Windows 保护电脑**" 屏幕中, 单击 "**详细信息**", 然后单击 "**仍然运行**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-162">In the **Windows protected your PC** screen, click **More info**, and then click **Run anyway**.</span></span>

1. <span data-ttu-id="96b54-163">在 "**用户帐户控制**" 对话框中, 单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="96b54-163">In the **User Account Control** dialog box, click **Yes**.</span></span>

1. <span data-ttu-id="96b54-164">在 " **VNetData** " 对话框中, 单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="96b54-164">In the **VNetData** dialog box, click **Yes**.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="96b54-165">连接到 Azure</span><span class="sxs-lookup"><span data-stu-id="96b54-165">Connect to Azure</span></span>

1. <span data-ttu-id="96b54-166">按 Windows 键, 键入**设置**, 然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="96b54-166">Press the Windows key, type **Settings** and press Enter.</span></span>

1. <span data-ttu-id="96b54-167">在 "**设置**" 窗口中, 单击 "**网络和 Internet**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-167">In the **Settings** window, click **Network and Internet**.</span></span>

1. <span data-ttu-id="96b54-168">在左侧窗格中, 单击 " **VPN**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-168">In the left-hand pane, click **VPN**.</span></span>

1. <span data-ttu-id="96b54-169">在右侧窗格中, 单击 " **VNetData**", 然后单击 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-169">In the right-hand pane, click **VNetData**, and then click **Connect**.</span></span>

1. <span data-ttu-id="96b54-170">在 "VNetData" 窗口中, 单击 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-170">In the VNetData window, click **Connect**.</span></span>

1. <span data-ttu-id="96b54-171">在下一个 VNetData 窗口中, 单击 "**继续**"。</span><span class="sxs-lookup"><span data-stu-id="96b54-171">In the next VNetData window, click **Continue**.</span></span>

1. <span data-ttu-id="96b54-172">在 "**用户帐户控制**" 消息框中, 单击 **"是"**。</span><span class="sxs-lookup"><span data-stu-id="96b54-172">In the **User Account Control** message box, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="96b54-173">如果这些步骤不起作用, 您可能需要重新启动计算机。</span><span class="sxs-lookup"><span data-stu-id="96b54-173">If these steps do not work, you may need to restart your computer.</span></span>

## <a name="verify-your-connection"></a><span data-ttu-id="96b54-174">验证连接</span><span class="sxs-lookup"><span data-stu-id="96b54-174">Verify your connection</span></span>

1. <span data-ttu-id="96b54-175">在新的 Windows 命令提示符处, `IPCONFIG /ALL`运行。</span><span class="sxs-lookup"><span data-stu-id="96b54-175">In a new Windows command prompt, run `IPCONFIG /ALL`.</span></span>

1. <span data-ttu-id="96b54-176">在 PPP 适配器 VNetData 下复制 IP 地址, 或将其写下来。</span><span class="sxs-lookup"><span data-stu-id="96b54-176">Copy the IP address under PPP adapter VNetData, or write it down.</span></span>

1. <span data-ttu-id="96b54-177">确认 IP 地址在**172.16.201.0/24 的 VPNClientAddressPool 范围**中。</span><span class="sxs-lookup"><span data-stu-id="96b54-177">Confirm that IP address is in the **VPNClientAddressPool range of 172.16.201.0/24**.</span></span>

1. <span data-ttu-id="96b54-178">您已成功建立到 Azure VPN 网关的连接。</span><span class="sxs-lookup"><span data-stu-id="96b54-178">You have successfully made a connection to the Azure VPN gateway.</span></span>

<span data-ttu-id="96b54-179">你只需设置 VPN 网关, 便可在 Azure 中对虚拟网络进行加密客户端连接。</span><span class="sxs-lookup"><span data-stu-id="96b54-179">You just set up a VPN gateway, allowing you to make an encrypted client connection to a virtual network in Azure.</span></span> <span data-ttu-id="96b54-180">此方法非常适于客户端计算机和较小的站点到站点连接。</span><span class="sxs-lookup"><span data-stu-id="96b54-180">This approach is great with client computers and smaller site-to-site connections.</span></span>