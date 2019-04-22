您需要确保您可以使用跨公共 Internet 的加密隧道将环境中的客户端或站点连接到 Azure。 在此单位中, 您将创建一个点到站点 VPN 网关, 然后从客户端计算机连接到该网关。 你将使用本机 Azure 证书身份验证连接来实现安全性。

您将执行以下过程:

1. 创建 RouteBased VPN 网关。

1. 为进行身份验证而上载根证书的公钥。

1. 从根证书生成客户端证书, 然后在每台将连接到虚拟网络以进行身份验证的客户端计算机上安装客户端证书。

1. 创建 VPN 客户端配置文件, 其中包含客户端连接到虚拟网络所需的信息。

## <a name="setup"></a>安装程序

若要完成此模块, 你将使用本地 Windows 10 计算机上的 Azure PowerShell。

我们将首先设置创建虚拟网络时要使用的变量。 打开新的 PowerShell 会话并创建以下变量:

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

## <a name="configure-a-virtual-network"></a>配置虚拟网络

1. 创建资源组。

    ```PowerShell
    New-AzResourceGroup -Name $ResourceGroup -Location $Location
    ```

1. 为虚拟网络创建子网配置。 它们具有名称**前端、后端**和**GatewaySubnet**。 所有这些子网都存在于虚拟网络前缀中。

    ```PowerShell
    $fesub = New-AzVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
    $besub = New-AzVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
    $gwsub = New-AzVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
    ```

1. 接下来, 使用子网值和静态 DNS 服务器创建虚拟网络。

    ```PowerShell
    New-AzVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroup -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
    ```

1. 现在, 为此网络指定您刚刚创建的变量。

    ```PowerShell
    $vnet = Get-AzVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroup
    $subnet = Get-AzVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    ```

1. 请求动态分配的公共 IP 地址。

    ```PowerShell
    $pip = New-AzPublicIpAddress -Name $GWIPName -ResourceGroupName $ResourceGroup -Location $Location -AllocationMethod Dynamic
    $ipconf = New-AzVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
    ```

## <a name="create-the-vpn-gateway"></a>创建 VPN 网关

创建此 VPN 网关时:

- GatewayType 必须是 Vpn
- VpnType 必须是 RouteBased

> [!NOTE]
> 请注意, 这部分练习可能需要长达45分钟才能完成。

1. 若要创建 VPN 网关, 请运行以下命令, 然后按 enter。

    ```PowerShell
    New-AzVirtualNetworkGateway -Name $GWName -ResourceGroupName $ResourceGroup `
      -Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
      -VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
    ```

1. 等待命令输出显示。

## <a name="add-the-vpn-client-address-pool"></a>添加 VPN 客户端地址池

1. 运行以下命令并按 enter 键。

    ```PowerShell
    $Gateway = Get-AzVirtualNetworkGateway -ResourceGroupName $ResourceGroup -Name $GWName
    Set-AzVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
    ```

1. 等待命令输出显示。

## <a name="generate-a-client-certificate"></a>生成客户端证书

在 Azure 上创建的网络基础结构, 我们需要在本地计算机上创建自签名客户端证书。 这在大多数操作系统上都可以这样做, 但我们将介绍如何在 windows 10 上使用 Azure powershell 模块和 Windows**证书管理器**实用工具生成客户端证书。

1. 我们的第一步是创建自签名根证书。 运行以下命令。

    ```PowerShell
    $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
    -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
    ```

1. 接下来, 生成由新的根证书签名的客户端证书。

    ```PowerShell
    New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
    -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 -KeyLength 2048 `
    -CertStoreLocation "Cert:\CurrentUser\My" `
    -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
    ```

生成证书后, 我们需要导出根证书的公钥。

1. 从`certmgr` PowerShell 运行以打开证书管理器。

1. 导航到 "**个人** > **证书**"。 查找并右键单击列表中的**P2SRootCert**证书, 并选择 "**所有任务** > **导出 ...**"。

1. 在 "证书导出向导" 中, 单击 "**下一步**"。

1. 确保选中 "不 **, 不导出私钥**", 然后单击 "**下一步**"。

1. 在 "**导出文件格式**" 页上, 确保以**64 编码的 x.509 (。CER)** , 然后单击 "**下一步**"。

1. 在 "**要导出的文件**" 页**** 上的 "文件名" 下, 导航到要记住的位置并将该文件另存为**P2SRootCert**, 然后单击 "下一步"。

1. 在 "**正在完成证书导出向导**" 页上, 单击 "**完成**"。

1. 在 "**证书导出向导**" 消息框中, 单击 **"确定"**。

## <a name="upload-the-root-certificate-public-key-information"></a>上传根证书公钥信息

1. 在 PowerShell 窗口中, 执行以下命令来声明证书名称的变量:

    ```PowerShell
    $P2SRootCertName = "P2SRootCert.cer"
    ```

1. 将`<cert-path>`占位符替换为您的根证书的导出位置, 并执行以下命令:

    ```PowerShell
    $filePathForCert = "<cert-path>\P2SRootCert.cer"
    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
    $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
    $p2srootcert = New-AzVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
    ```

1. 在设置组名称后, 使用以下命令将证书上传到 Azure。

    ```PowerShell
    Add-AzVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname $GWName -ResourceGroupName $ResourceGroup -PublicCertData $CertBase64
    ```

    Azure 现在将此证书识别为虚拟网络的受信任根证书。

## <a name="configure-the-native-vpn-client"></a>配置本机 VPN 客户端

1. 执行以下命令以在中创建 VPN 客户端配置文件。ZIP 格式。

    ```PowerShell
    $profile = New-AzVpnClientConfiguration -ResourceGroupName $ResourceGroup -Name $GWName -AuthenticationMethod "EapTls"
    $profile.VPNProfileSASUrl
    ```

1. 复制此命令的输出中返回的 URL, 并将其粘贴到浏览器中。 你的浏览器应开始下载。ZIP 文件。 提取存档内容并将其放在合适的位置。

    > [!NOTE]
    > 某些浏览器最初将尝试阻止下载此 ZIP 文件作为危险下载。 您将需要在浏览器中覆盖此内容, 以便能够提取存档内容。

1. 在提取的文件夹中, 导航到 " **WindowsAmd64** " 文件夹 (适用于64位 Windows 计算机) 或 " **WindowsX86** " 文件夹 (针对32位计算机)。

    > [!NOTE]
    > 如果要在非 Windows 计算机上配置 VPN, 可以使用**通用**文件夹中的证书和设置文件。

1. 双击**VpnClientSetup {体系结构} .exe**文件, 并反映您的`{architecture}`体系结构。

1. 在 " **Windows 保护电脑**" 屏幕中, 单击 "**详细信息**", 然后单击 "**仍然运行**"。

1. 在 "**用户帐户控制**" 对话框中, 单击 **"是"**。

1. 在 " **VNetData** " 对话框中, 单击 **"是"**。

## <a name="connect-to-azure"></a>连接到 Azure

1. 按 Windows 键, 键入**设置**, 然后按 enter。

1. 在 "**设置**" 窗口中, 单击 "**网络和 Internet**"。

1. 在左侧窗格中, 单击 " **VPN**"。

1. 在右侧窗格中, 单击 " **VNetData**", 然后单击 "**连接**"。

1. 在 "VNetData" 窗口中, 单击 "**连接**"。

1. 在下一个 VNetData 窗口中, 单击 "**继续**"。

1. 在 "**用户帐户控制**" 消息框中, 单击 **"是"**。

> [!NOTE]
> 如果这些步骤不起作用, 您可能需要重新启动计算机。

## <a name="verify-your-connection"></a>验证连接

1. 在新的 Windows 命令提示符处, `IPCONFIG /ALL`运行。

1. 在 PPP 适配器 VNetData 下复制 IP 地址, 或将其写下来。

1. 确认 IP 地址在**172.16.201.0/24 的 VPNClientAddressPool 范围**中。

1. 您已成功建立到 Azure VPN 网关的连接。

你只需设置 VPN 网关, 便可在 Azure 中对虚拟网络进行加密客户端连接。 此方法非常适于客户端计算机和较小的站点到站点连接。