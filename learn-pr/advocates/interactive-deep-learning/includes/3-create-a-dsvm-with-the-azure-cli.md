<span data-ttu-id="c953e-101">作为贵公司的软件开发人员, 您有机会扩大技能并成为内部的 AI 团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="c953e-101">As a software developer at your company, you've the opportunity to grow your skills and become part of the in-house AI team.</span></span> <span data-ttu-id="c953e-102">在你向你提升此激动人心的新角色时, 你仍需要执行日常工作。</span><span class="sxs-lookup"><span data-stu-id="c953e-102">While you ramp-up on this exciting new role, you still have your day job to do.</span></span> <span data-ttu-id="c953e-103">您的团队的高级 AI 工程师已告知您一些有用的 Jupyter 笔记本, 这些笔记本具有基于 PyTorch 的实验室来培训图像分类模型。</span><span class="sxs-lookup"><span data-stu-id="c953e-103">The senior AI engineer on your team has told you about some useful Jupyter notebooks that have PyTorch-based labs to train an image classification model.</span></span> <span data-ttu-id="c953e-104">令人兴奋的内容, 但您不想将一组框架安装到 dev 远程测试机组中。</span><span class="sxs-lookup"><span data-stu-id="c953e-104">Exciting stuff, but you don't want to install a set of frameworks onto your dev rig.</span></span> <span data-ttu-id="c953e-105">而是决定创建基于数据科学虚拟机 (DSVM) 图像的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c953e-105">Instead, you decide to create a virtual machine based on the Data Science Virtual Machine (DSVM) image.</span></span> 

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="c953e-106">什么是 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c953e-106">What is the Azure CLI</span></span>

<span data-ttu-id="c953e-107">azure CLI 是 Microsoft 的用于管理 Azure 资源的跨平台命令行工具。</span><span class="sxs-lookup"><span data-stu-id="c953e-107">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="c953e-108">它可用于 macOS、Linux 和 Windows, 也可用于使用[Azure 云命令行](https://docs.microsoft.com/azure/cloud-shell/overview)管理程序的浏览器。</span><span class="sxs-lookup"><span data-stu-id="c953e-108">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span> <span data-ttu-id="c953e-109">我们完全覆盖了在使用**CLI 模块控制 Azure 服务时**使用此工具。</span><span class="sxs-lookup"><span data-stu-id="c953e-109">We have complete coverage of using this tool in the **Control Azure services with the CLI** module.</span></span>

## <a name="managing-deployments"></a><span data-ttu-id="c953e-110">管理部署</span><span class="sxs-lookup"><span data-stu-id="c953e-110">Managing deployments</span></span>

<span data-ttu-id="c953e-111">azure CLI 包含用于管理`az group deployment` Azure 资源管理器部署的命令。</span><span class="sxs-lookup"><span data-stu-id="c953e-111">The Azure CLI includes the `az group deployment` command to manage Azure Resource Manager deployments.</span></span> <span data-ttu-id="c953e-112">我们可以提供几个子命令来完成特定任务。</span><span class="sxs-lookup"><span data-stu-id="c953e-112">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="c953e-113">最常见的包括:</span><span class="sxs-lookup"><span data-stu-id="c953e-113">The most common include:</span></span>

| <span data-ttu-id="c953e-114">子命令</span><span class="sxs-lookup"><span data-stu-id="c953e-114">Subcommand</span></span> | <span data-ttu-id="c953e-115">说明</span><span class="sxs-lookup"><span data-stu-id="c953e-115">Description</span></span> |
|-------------|-------------|
| `create` | <span data-ttu-id="c953e-116">启动部署。</span><span class="sxs-lookup"><span data-stu-id="c953e-116">Start a deployment.</span></span> |
| `list` | <span data-ttu-id="c953e-117">获取资源组的所有部署。</span><span class="sxs-lookup"><span data-stu-id="c953e-117">Get all the deployments for a resource group.</span></span> |
| `export` | <span data-ttu-id="c953e-118">导出用于部署的模板。</span><span class="sxs-lookup"><span data-stu-id="c953e-118">Export the template used for a deployment.</span></span> |

<span data-ttu-id="c953e-119">有关可用部署命令的完整列表, 请参阅[az group deployment command reference](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)</span><span class="sxs-lookup"><span data-stu-id="c953e-119">For a complete list of available deployment commands, see the [az group deployment command reference](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)</span></span>

<span data-ttu-id="c953e-120">我们将使用`az group deployment create`预配虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c953e-120">We'll use `az group deployment create` to provision our virtual machine.</span></span>

## <a name="create-a-json-deployment-parameters-file"></a><span data-ttu-id="c953e-121">创建 JSON 部署参数文件</span><span class="sxs-lookup"><span data-stu-id="c953e-121">Create a JSON deployment parameters file</span></span>

<span data-ttu-id="c953e-122">我们要使用 Azure 资源管理器模板创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c953e-122">We're going to create our VM using an Azure Resource Manager template.</span></span> <span data-ttu-id="c953e-123">模板定义要预配的 Linux DSVM 映像。</span><span class="sxs-lookup"><span data-stu-id="c953e-123">The template defines the Linux DSVM image we want to provision.</span></span> <span data-ttu-id="c953e-124">我们需要为模板提供一些参数, 如我们要使用的 VM 大小、管理员用户名和密码以及我们的计算机的主机名。</span><span class="sxs-lookup"><span data-stu-id="c953e-124">We need to supply some parameters to the template, such as the VM size we want to use, the admin username and password, and the host name of our machine.</span></span> 

1. <span data-ttu-id="c953e-125">在此单元右侧的 Azure 云命令行管理程序中执行以下命令:</span><span class="sxs-lookup"><span data-stu-id="c953e-125">Execute the following command in Azure Cloud Shell to the right of this unit:</span></span>

    ```azurecli
    code .
    ```
    <!-- TODO add a link to official doc that explains the built-in editor when it becomes available -->
    <span data-ttu-id="c953e-126">此命令将在内置编辑器中打开和清空文件。</span><span class="sxs-lookup"><span data-stu-id="c953e-126">This command opens and empty file in the built-in editor.</span></span> 

1. <span data-ttu-id="c953e-127">将下面的 JSON 代码片段粘贴到代码编辑器中的空文件中。</span><span class="sxs-lookup"><span data-stu-id="c953e-127">Paste the following JSON snippet into the empty file in the code editor.</span></span>

    ```json
    { 
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
         "adminUsername": { "value" : "<USERNAME>"},
         "adminPassword": { "value" : "<PASSWORD>"},
         "vmName": { "value" : "<HOSTNAME>"},
         "vmSize": { "value" : "Standard_DS2_v2"},
      }
    }
    ```

1. <span data-ttu-id="c953e-128">更新在编辑器中粘贴的 JSON 中的以下参数:</span><span class="sxs-lookup"><span data-stu-id="c953e-128">Update the following parameters in the JSON you pasted in the editor:</span></span>

    |<span data-ttu-id="c953e-129">参数</span><span class="sxs-lookup"><span data-stu-id="c953e-129">Parameter</span></span>  |<span data-ttu-id="c953e-130">当前值</span><span class="sxs-lookup"><span data-stu-id="c953e-130">Current value</span></span>  |<span data-ttu-id="c953e-131">您的值</span><span class="sxs-lookup"><span data-stu-id="c953e-131">Your value</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="c953e-132">adminUsername</span><span class="sxs-lookup"><span data-stu-id="c953e-132">adminUsername</span></span>     |  `<USERNAME>`       |    <span data-ttu-id="c953e-133">为此新计算机的管理员用户选择一个名称, 例如, *azuser*。</span><span class="sxs-lookup"><span data-stu-id="c953e-133">Choose a name for the admin user of this new machine, such as, *azuser*.</span></span>     |
    |<span data-ttu-id="c953e-134">adminPassword</span><span class="sxs-lookup"><span data-stu-id="c953e-134">adminPassword</span></span>     |  `<PASSWORD>`       |   <span data-ttu-id="c953e-135">为此管理员用户帐户选择密码。</span><span class="sxs-lookup"><span data-stu-id="c953e-135">Choose a password for this admin user account.</span></span> <span data-ttu-id="c953e-136">若要了解有关密码要求的详细信息, 请参阅[有关 Linux 虚拟机的常见问题](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)</span><span class="sxs-lookup"><span data-stu-id="c953e-136">To learn more about password requirements, see [Frequently asked question about Linux Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)</span></span>     |
    |<span data-ttu-id="c953e-137">vmName</span><span class="sxs-lookup"><span data-stu-id="c953e-137">vmName</span></span>     |   `<HOSTNAME>`      |  <span data-ttu-id="c953e-138">选择新虚拟机的名称。</span><span class="sxs-lookup"><span data-stu-id="c953e-138">Choose a name for the new virtual machine.</span></span> <span data-ttu-id="c953e-139">您的名称必须以字母开头, 并且只能包含小写字母和数字。</span><span class="sxs-lookup"><span data-stu-id="c953e-139">Your name must begin with a letter and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="c953e-140">请尝试选择一个唯一的名称, 例如, 其中包含你的缩写和出生年份。</span><span class="sxs-lookup"><span data-stu-id="c953e-140">Try to choose a unique name, such as one that includes your initials and your birth year.</span></span> |
    |<span data-ttu-id="c953e-141">vmSize</span><span class="sxs-lookup"><span data-stu-id="c953e-141">vmSize</span></span>     |  <span data-ttu-id="c953e-142">Standard_DS2_v2</span><span class="sxs-lookup"><span data-stu-id="c953e-142">Standard_DS2_v2</span></span>       |  <span data-ttu-id="c953e-143">此 VM 大小在此练习中将正常运行, 但你可以随意进行更改。</span><span class="sxs-lookup"><span data-stu-id="c953e-143">This VM size will work fine for this exercise, but you are free to change it.</span></span> <span data-ttu-id="c953e-144">此处的可用 vm 大小列表可在此处找到[Azure 中的 Linux 虚拟机的大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)</span><span class="sxs-lookup"><span data-stu-id="c953e-144">A list of available vm sizes can be found here [Sizes for Linux virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)</span></span>       |

1. <span data-ttu-id="c953e-145">选择编辑器右上部的三个省略号 (**...**), 然后从菜单中选择 "**保存**", 以将文件保存为`parameter_file.json`并关闭文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="c953e-145">Select the three ellipses (**...**) to the top right of the editor and then select **Save** from the menu to save the file as `parameter_file.json` and close the text editor.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c953e-146">请记住您为 adminUsername、adminPassword 和 vmName 选择的值。</span><span class="sxs-lookup"><span data-stu-id="c953e-146">Remember the values you chose for adminUsername, adminPassword and vmName.</span></span> <span data-ttu-id="c953e-147">我们将在此练习中再次使用它们。</span><span class="sxs-lookup"><span data-stu-id="c953e-147">We'll use them again in this exercise.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="c953e-148">创建资源组</span><span class="sxs-lookup"><span data-stu-id="c953e-148">Create a resource group</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c953e-149">通常情况下, 您需要在所选的区域中创建资源组。</span><span class="sxs-lookup"><span data-stu-id="c953e-149">Normally you'd create a resource group in a region of your choice.</span></span> <span data-ttu-id="c953e-150">但是, 当前正在提供的沙盒会话提供了要使用的资源组。</span><span class="sxs-lookup"><span data-stu-id="c953e-150">However, the sandbox session you are currently in supplies a resource group for you to use.</span></span> <span data-ttu-id="c953e-151">此会话的资源组为**<rgn>[沙盒资源组名称]</rgn>**。</span><span class="sxs-lookup"><span data-stu-id="c953e-151">Your resource group for this session is **<rgn>[sandbox resource group name]</rgn>**.</span></span>

## <a name="deploy-the-dsvm-to-your-resource-group"></a><span data-ttu-id="c953e-152">将 DSVM 部署到您的资源组</span><span class="sxs-lookup"><span data-stu-id="c953e-152">Deploy the DSVM to your resource group</span></span>

<span data-ttu-id="c953e-153">现在, 我们有一个资源组, 并且已在名`parameter_file.json`为的文件中为 DSVM 资源管理器模板定义了参数。</span><span class="sxs-lookup"><span data-stu-id="c953e-153">We now have a resource group and have defined parameters for the DSVM Resource Manager template in a file called `parameter_file.json`.</span></span> <span data-ttu-id="c953e-154">我们将运行`az group deployment create`下一步来设置虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c953e-154">We'll run the `az group deployment create` next to provision our virtual machine.</span></span>

1. <span data-ttu-id="c953e-155">在 Azure 云命令行管理程序中执行以下命令:</span><span class="sxs-lookup"><span data-stu-id="c953e-155">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    az group deployment create \
    --resource-group  <rgn>[sandbox resource group name]</rgn> \
    --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json \
    --parameters parameter_file.json
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    <span data-ttu-id="c953e-156">该命令使用资源管理器模板和我们的参数在资源组中创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="c953e-156">The command uses the Resource Manager template and our parameters to create the virtual machine in our resource group.</span></span> 

2. <span data-ttu-id="c953e-157">部署虚拟机需要几分钟时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="c953e-157">Deploying a virtual machine takes a few minutes to complete.</span></span> <span data-ttu-id="c953e-158">控制台在操作` - Running ..`完成之前会显示, 而不是其他内容。</span><span class="sxs-lookup"><span data-stu-id="c953e-158">The console displays ` - Running ..` and not much else until the operation completes.</span></span> <span data-ttu-id="c953e-159">操作完成后, 会将 JSON 响应输出到屏幕。</span><span class="sxs-lookup"><span data-stu-id="c953e-159">When the operation finishes, a JSON response is output to the screen.</span></span> <span data-ttu-id="c953e-160">滚动到 JSON 的底部, 并检查字段 **"provisioningState"** 的值是否已*成功*。</span><span class="sxs-lookup"><span data-stu-id="c953e-160">Scroll to the bottom of the JSON and check that the field **"provisioningState"** has the value *Succeeded*.</span></span>

    > [!TIP]
    > <span data-ttu-id="c953e-161">如果您收到一条错误, 指出 DNS 记录已被另一个公共 IP 使用, 请尝试\*\*\*\* `parameter_file.json`将 vmName 更改为另一个唯一的名称。</span><span class="sxs-lookup"><span data-stu-id="c953e-161">If you get an error stating that the DNS record is already used by another public IP, try changing **vmName** in `parameter_file.json` to another name that's unique.</span></span>

3. <span data-ttu-id="c953e-162">执行以下命令以获取有关 vm 的信息, 并用您`<HOSTNAME>`为 VM 定义的主机名称替换。</span><span class="sxs-lookup"><span data-stu-id="c953e-162">Execute the following command to get information about the VM, replacing `<HOSTNAME>` with the host name you defined for your VM.</span></span>

    ```azurecli
    az vm show -d \
    --name <HOSTNAME> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --output table
    ```

    <span data-ttu-id="c953e-163">此命令将显示 VM 的状态。</span><span class="sxs-lookup"><span data-stu-id="c953e-163">This command displays the status of the VM.</span></span> <span data-ttu-id="c953e-164">**PowerState**字段应指示*运行的虚拟机*。</span><span class="sxs-lookup"><span data-stu-id="c953e-164">The **PowerState** field should say *VM running*.</span></span> <span data-ttu-id="c953e-165">在本练习后面的部分中, 我们将使用**PublicIps**字段中的 IP 地址连接到 VM。</span><span class="sxs-lookup"><span data-stu-id="c953e-165">Later in this exercise, we'll connect to the VM using the IP address in the **PublicIps** field.</span></span> <span data-ttu-id="c953e-166">我们还可以使用此处的 " **fqdn** " 字段中显示的完全限定的域名 (FQDN) 进行连接。</span><span class="sxs-lookup"><span data-stu-id="c953e-166">We could also connect using the Fully Qualified Domain Name (FQDN) displayed here in the **Fqdns** field.</span></span>

<span data-ttu-id="c953e-167">!!</span><span class="sxs-lookup"><span data-stu-id="c953e-167">Congratulations!</span></span> <span data-ttu-id="c953e-168">您已创建并部署基于 DSVM 映像的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="c953e-168">You've created and deployed a Linux VM based on the DSVM image.</span></span>

## <a name="open-the-vm-to-ssh-traffic-on-port-22"></a><span data-ttu-id="c953e-169">在端口22上打开 VM 到 ssh 流量</span><span class="sxs-lookup"><span data-stu-id="c953e-169">Open the VM to ssh traffic on port 22</span></span>

<span data-ttu-id="c953e-170">默认情况下, 我们的虚拟机不会打开任何端口。</span><span class="sxs-lookup"><span data-stu-id="c953e-170">By default, our VM doesn't have any ports open.</span></span> <span data-ttu-id="c953e-171">我们的目标是远程连接、启动 Jupyter 笔记本服务器并在计算机上运行其他本地命令。</span><span class="sxs-lookup"><span data-stu-id="c953e-171">Our goal is to connect remotely, start a Jupyter Notebook server and run other local commands on the machine.</span></span> <span data-ttu-id="c953e-172">若要使用安全命令行管理程序 (SSH) 协议将远程登录到 VM, 我们需要打开端口。</span><span class="sxs-lookup"><span data-stu-id="c953e-172">To remote into the VM using the Secure Shell (SSH) protocol, we need to open a port.</span></span> <span data-ttu-id="c953e-173">端口22是 ssh 的默认端口。</span><span class="sxs-lookup"><span data-stu-id="c953e-173">Port 22 is the default port for ssh.</span></span>  

1. <span data-ttu-id="c953e-174">在 Azure 云命令行管理程序中执行以下`<HOSTNAME>`命令, 并将其替换为安装过程中为虚拟机提供的名称。</span><span class="sxs-lookup"><span data-stu-id="c953e-174">Execute the following command in Azure Cloud Shell, replacing `<HOSTNAME>` with the name you gave your virtual machine during setup.</span></span> 

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 22 \
    --priority 900
    ```

<span data-ttu-id="c953e-175">此命令最长可能需要一分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="c953e-175">This command can take up to a minute to complete.</span></span> <span data-ttu-id="c953e-176">命令完成后, 它会将 JSON 响应返回到命令行。</span><span class="sxs-lookup"><span data-stu-id="c953e-176">When the command finishes, it returns a JSON response to the command line.</span></span> <span data-ttu-id="c953e-177">检查字段 **"provisioningState"** 的值是否已*成功*。</span><span class="sxs-lookup"><span data-stu-id="c953e-177">Check that the field **"provisioningState"** has the value *Succeeded*.</span></span> <span data-ttu-id="c953e-178">我们将测试 ssh 是否很快工作, 但首先让我们打开一个更多的端口。</span><span class="sxs-lookup"><span data-stu-id="c953e-178">We'll test that ssh works shortly, but first let's open one more port.</span></span>

## <a name="open-the-vm-to-access-the-jupyter-notebook-server-remotely"></a><span data-ttu-id="c953e-179">打开 VM 以远程访问 Jupyter 笔记本服务器</span><span class="sxs-lookup"><span data-stu-id="c953e-179">Open the VM to access the Jupyter Notebook server remotely</span></span>

<span data-ttu-id="c953e-180">如前所述, DSVM 映像是预安装的软件、工具和示例, 可帮助你使用数据科学、机器学习和深入学习项目。</span><span class="sxs-lookup"><span data-stu-id="c953e-180">As mentioned previously, the DSVM image comes pre-installed with software, tools, and samples to help you with your data science, machine learning, and deep learning projects.</span></span> <span data-ttu-id="c953e-181">Jupyter 与示例笔记本一起安装在映像中。</span><span class="sxs-lookup"><span data-stu-id="c953e-181">Jupyter is installed in the image, along with sample notebooks.</span></span> <span data-ttu-id="c953e-182">我们想要在 VM 上启动一个 Jupyter 笔记本服务器, 然后从我们的本地计算机远程连接到该笔记本服务器。</span><span class="sxs-lookup"><span data-stu-id="c953e-182">We want to start a Jupyter notebook server on the VM and then remotely connect to the notebook server from our local machine.</span></span> <span data-ttu-id="c953e-183">默认情况下, 笔记本服务器在端口8888上运行。</span><span class="sxs-lookup"><span data-stu-id="c953e-183">By default, the notebook server runs on port 8888.</span></span> <span data-ttu-id="c953e-184">若要远程访问服务器, 我们需要在虚拟机上打开该端口。</span><span class="sxs-lookup"><span data-stu-id="c953e-184">To access the server remotely, we need to open that port on our VM.</span></span> 

1. <span data-ttu-id="c953e-185">在 Azure 云命令行管理程序中执行以下`<HOSTNAME>`命令, 并将其替换为在安装过程中为 DSVM 虚拟机提供的名称。</span><span class="sxs-lookup"><span data-stu-id="c953e-185">Execute the following command in Azure Cloud Shell, replacing `<HOSTNAME>` with the name you gave your DSVM virtual machine during setup.</span></span>

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 8888 \
    --priority 901
    ```

<span data-ttu-id="c953e-186">同样, 此命令最长可能需要一分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="c953e-186">Again, this command can take up to a minute to complete.</span></span> <span data-ttu-id="c953e-187">命令完成后, 它会将 JSON 响应返回到命令行。</span><span class="sxs-lookup"><span data-stu-id="c953e-187">When the command finishes, it returns a JSON response to the command line.</span></span> <span data-ttu-id="c953e-188">检查字段 **"provisioningState"** 的值是否已*成功*。</span><span class="sxs-lookup"><span data-stu-id="c953e-188">Check that the field **"provisioningState"** has the value *Succeeded*.</span></span>  

## <a name="connect-to-the-vm-with-secure-shell-ssh"></a><span data-ttu-id="c953e-189">使用安全命令行管理程序 (ssh) 连接到 VM</span><span class="sxs-lookup"><span data-stu-id="c953e-189">Connect to the VM with Secure Shell (ssh)</span></span>

1. <span data-ttu-id="c953e-190">在 Azure 云命令行管理程序中执行以下命令, 以查找 VM 的公共 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="c953e-190">Execute the following command in Azure Cloud Shell to find the public IP address of the VM.</span></span> <span data-ttu-id="c953e-191">将`<HOSTNAME>`替换为您在安装过程中为 DSVM 虚拟机提供的名称。</span><span class="sxs-lookup"><span data-stu-id="c953e-191">Replace `<HOSTNAME>` with the name you gave your DSVM virtual machine during setup.</span></span>

    ```azurecli
    az vm list-ip-addresses \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --output table
    ```

1. <span data-ttu-id="c953e-192">在云命令行管理程序中执行以下命令, 以登录到 VM。</span><span class="sxs-lookup"><span data-stu-id="c953e-192">Execute the following command in the Cloud Shell to sign into the VM.</span></span> <span data-ttu-id="c953e-193">将`<USERNAME>`替换为您在本练习开始时选择的用户名。</span><span class="sxs-lookup"><span data-stu-id="c953e-193">Replace `<USERNAME>` with the username you chose at the start of this exercise.</span></span> <span data-ttu-id="c953e-194">将`<IP>`替换为上一步的**PublicIPAddresses**列中的值。</span><span class="sxs-lookup"><span data-stu-id="c953e-194">Replace `<IP>`  with the value from the **PublicIPAddresses** column of the previous step.</span></span>

    <span data-ttu-id="c953e-195">例如, 如果您选择的用户名为*azuser* , 而 PublicIPAddresses 的值为 33.165.103.23, 则此命令将会读取:</span><span class="sxs-lookup"><span data-stu-id="c953e-195">For example, if the username you chose was *azuser* and the PublicIPAddresses had a value of 33.165.103.23, then this command would read:</span></span>
    
    `ssh azuser@33.165.103.23`
    
    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 

1. <span data-ttu-id="c953e-196">出现提示时, 请输入您在本练习开始时选择的管理员用户的密码。</span><span class="sxs-lookup"><span data-stu-id="c953e-196">When prompted, enter the password for the admin user you chose at the start of this exercise.</span></span> <span data-ttu-id="c953e-197">成功登录后, 提示应更改为格式`username@hostname`, 例如。 `azuser@js1982`</span><span class="sxs-lookup"><span data-stu-id="c953e-197">When you've signed in successfully, your prompt should change to the format `username@hostname`, for example, `azuser@js1982`.</span></span>

<span data-ttu-id="c953e-198">下一步是在虚拟机上启动 Jupyter 笔记本服务器并远程打开笔记本。</span><span class="sxs-lookup"><span data-stu-id="c953e-198">The next step is to start the Jupyter notebook server on our VM and open a notebook remotely.</span></span>

## <a name="start-the-jupyter-notebook-server-on-the-vm"></a><span data-ttu-id="c953e-199">启动 VM 上的 Jupyter 笔记本服务器</span><span class="sxs-lookup"><span data-stu-id="c953e-199">Start the Jupyter notebook server on the VM</span></span>

<span data-ttu-id="c953e-200">VM 的`~/notebooks`文件夹中有一组笔记本。</span><span class="sxs-lookup"><span data-stu-id="c953e-200">There's a set of notebooks in the `~/notebooks` folder of your VM.</span></span> <span data-ttu-id="c953e-201">假定您仍通过 SSH 会话登录, 请启动笔记本服务器并打开其中一个笔记本以确保一切正常工作。</span><span class="sxs-lookup"><span data-stu-id="c953e-201">Assuming you are still logged in through an SSH session,  start the notebook server and open one of these notebooks to make sure everything is working.</span></span>


1. <span data-ttu-id="c953e-202">在 VM 的命令提示符处运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="c953e-202">Run the following command at the command prompt of your VM:</span></span>

    ```bash
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

> [!CAUTION]
> <span data-ttu-id="c953e-203">在此练习中, 对笔记本服务器的访问`http://`发生。</span><span class="sxs-lookup"><span data-stu-id="c953e-203">Access to the notebook server in this exercise happens over `http://`.</span></span> <span data-ttu-id="c953e-204">如果要在公用中运行笔记本服务器, 应对其进行保护。</span><span class="sxs-lookup"><span data-stu-id="c953e-204">If you want to run a notebook server in public, you should secure it.</span></span> <span data-ttu-id="c953e-205">有关保护笔记本服务器的详细信息, 请参阅官方 Jupyter 文档 online。</span><span class="sxs-lookup"><span data-stu-id="c953e-205">For more information about securing a notebook server, see the official Jupyter documentation online.</span></span> 

<span data-ttu-id="c953e-206">在上面的命令中, 我们使用`jupyter notebook`命令启动 Jupyter 笔记本服务器。</span><span class="sxs-lookup"><span data-stu-id="c953e-206">In the preceding command, we start the Jupyter Notebook server with the `jupyter notebook` command.</span></span> <span data-ttu-id="c953e-207">我们提供了三个重要的命令行参数。</span><span class="sxs-lookup"><span data-stu-id="c953e-207">We supply three important command-line arguments.</span></span> <span data-ttu-id="c953e-208">请记住, 我们是通过控制台远程登录到此计算机的。</span><span class="sxs-lookup"><span data-stu-id="c953e-208">Remember, we're logged into this machine remotely through a console.</span></span> <span data-ttu-id="c953e-209">笔记本在浏览器中提供。</span><span class="sxs-lookup"><span data-stu-id="c953e-209">Notebooks are served in a browser.</span></span> 

 - <span data-ttu-id="c953e-210">`--ip=0.0.0.0`默认情况下, 笔记本服务器在 127.0.0.1: 8888 处本地运行, 并且只能从 localhost 访问。</span><span class="sxs-lookup"><span data-stu-id="c953e-210">`--ip=0.0.0.0` By default, a notebook server runs locally at 127.0.0.1:8888 and is accessible only from localhost.</span></span> <span data-ttu-id="c953e-211">您可以使用http://127.0.0.1:8888从本地浏览器访问笔记本服务器。</span><span class="sxs-lookup"><span data-stu-id="c953e-211">You can access the notebook server from the browser locally using http://127.0.0.1:8888.</span></span> <span data-ttu-id="c953e-212">将 "IP 地址" 设置为0.0.0.0 将告知服务器侦听所有 ip 上的流量。</span><span class="sxs-lookup"><span data-stu-id="c953e-212">Setting the IP Address to 0.0.0.0 tells the server to listen for traffic on all IPs.</span></span> <span data-ttu-id="c953e-213">如果笔记本服务器以0.0.0.0 监听, 则可以通过主机的 IP 地址访问它。</span><span class="sxs-lookup"><span data-stu-id="c953e-213">If the notebook server listens on 0.0.0.0, it will be reachable through the IP address of the host machine.</span></span>  
 - <span data-ttu-id="c953e-214">`--no-browser`由于我们要通过 internet 从另一台计算机连接到笔记本, 因此我们将笔记本服务器配置为不打开浏览器, 这是默认行为。</span><span class="sxs-lookup"><span data-stu-id="c953e-214">`--no-browser`  Because we want to connect to the notebook from another computer over the internet, we configure the notebook server to not open the browser, which is the default behavior.</span></span> 
 - <span data-ttu-id="c953e-215">`--allow-root`在本练习中, 我们仅在 VM 上拥有管理员帐户, 因此我们希望能够以根身份运行笔记本。</span><span class="sxs-lookup"><span data-stu-id="c953e-215">`--allow-root`  In this exercise, we only have an admin account on the VM, so  we want to be able to run notebooks as root.</span></span>

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a><span data-ttu-id="c953e-216">从远程浏览器连接到 Jupyter 笔记本服务器</span><span class="sxs-lookup"><span data-stu-id="c953e-216">Connect to the Jupyter Notebook server from a remote browser</span></span>

<span data-ttu-id="c953e-217">当上述命令在 VM 上运行时, 笔记本服务器将启动, 控制台将显示 URL, 以便您在浏览器中使用。</span><span class="sxs-lookup"><span data-stu-id="c953e-217">When the above command runs on the VM, the notebook server starts and the console displays a URL for you to use in a browser.</span></span> 

![在控制台中显示运行笔记本服务器的消息的屏幕截图, 其中包含从主机访问服务器的 URL](../media/notebook-url.png)

1. <span data-ttu-id="c953e-219">复制笔记本服务器显示在您喜爱的浏览器的地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="c953e-219">Copy the URL the notebook server displays into the address bar of your favorite browser.</span></span> <span data-ttu-id="c953e-220">您还可以单击 URL 以在默认浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="c953e-220">You can also click on the URL to open in your default browser.</span></span> 

    <span data-ttu-id="c953e-221">你将收到 "无法访问网站" 消息, 因为你提供的 URL 是从主机到笔记本服务器的连接。</span><span class="sxs-lookup"><span data-stu-id="c953e-221">You will receive a "Site can't be reached" message because the URL you were given is the connection to the notebook server from the host machine.</span></span>

1. <span data-ttu-id="c953e-222">若要远程访问服务器, 请将 URL 中的主机名替换为先前保存的 VM 的 IP 地址。</span><span class="sxs-lookup"><span data-stu-id="c953e-222">To access the server remotely,  replace the hostname in the URL with the IP address of the VM you saved earlier.</span></span> 

    <span data-ttu-id="c953e-223">下面是一个示例笔记本服务器 URL。</span><span class="sxs-lookup"><span data-stu-id="c953e-223">Here's a sample notebook server URL.</span></span>

    <span data-ttu-id="c953e-224">́http//**ab-dsvm-4**: 8888/?token = {某个令牌} ́</span><span class="sxs-lookup"><span data-stu-id="c953e-224">´http://**ab-dsvm-4**:8888/?token={some token}´</span></span>

    <span data-ttu-id="c953e-225">在这种情况下, 我们会将**ab-4**替换为计算机的 IP 地址 dsvm。</span><span class="sxs-lookup"><span data-stu-id="c953e-225">In this case, we would replace **ab-dsvm-4** with IP address of the machine.</span></span> <span data-ttu-id="c953e-226">如果我们的 IP 地址`52.175.199.43`为, 则 URL 将变为:</span><span class="sxs-lookup"><span data-stu-id="c953e-226">If our IP address is `52.175.199.43`, then the URL becomes:</span></span>

    <span data-ttu-id="c953e-227">́http://**52.175.199.43**: 8888/?token = {某个令牌} ́</span><span class="sxs-lookup"><span data-stu-id="c953e-227">´http://**52.175.199.43**:8888/?token={some token}´</span></span>

    <span data-ttu-id="c953e-228">请确保`:8888`URL 中保留了端口地址。</span><span class="sxs-lookup"><span data-stu-id="c953e-228">Make sure `:8888`, the port address, is kept in the URL.</span></span>

    > [!TIP]
    > <span data-ttu-id="c953e-229">如果不想使用 IP 地址, 则还可以使用窗体中的完全限定的服务器名称`<HOST NAME>.<REGION>.cloudapp.azure.com`</span><span class="sxs-lookup"><span data-stu-id="c953e-229">If you don't want to use the IP address, you can also use the fully qualified name of your server which is in the form `<HOST NAME>.<REGION>.cloudapp.azure.com`</span></span>

    <span data-ttu-id="c953e-230">下面的屏幕截图显示 Jupyter 仪表板在浏览器中的外观。</span><span class="sxs-lookup"><span data-stu-id="c953e-230">The following  screenshot shows what the Jupyter dashboard looks like in your browser.</span></span>

    ![<span data-ttu-id="c953e-231">显示 Jupyter 笔记本仪表板的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c953e-231">Screenshot showing Jupyter Notebooks dashboard.</span></span> ](../media/jupyter-in-browser.png)

1. <span data-ttu-id="c953e-232">导航到 "**笔记本/IntroToJupyterPython** ", 然后选择它。</span><span class="sxs-lookup"><span data-stu-id="c953e-232">Navigate to **notebooks/IntroToJupyterPython.ipynb** and select it.</span></span> <span data-ttu-id="c953e-233">尝试此笔记本以验证所有内容是否按预期工作。</span><span class="sxs-lookup"><span data-stu-id="c953e-233">Try out this notebook to verify everything  works as expected.</span></span>

    <span data-ttu-id="c953e-234">!!</span><span class="sxs-lookup"><span data-stu-id="c953e-234">Congratulations!</span></span> <span data-ttu-id="c953e-235">现在, 您运行的是基于 DSVM 的虚拟机, 可以使用 Jupyter 远程工作。</span><span class="sxs-lookup"><span data-stu-id="c953e-235">You now have a running DSVM-based virtual machine running and can work remotely with Jupyter.</span></span> <span data-ttu-id="c953e-236">在本练习中, 我们运行的是在 VM 上安装的软件。</span><span class="sxs-lookup"><span data-stu-id="c953e-236">In this exercise, we're running the software that was installed on the VM.</span></span> <span data-ttu-id="c953e-237">在下一个练习中, 我们会将软件隔离在 VM 上的容器中, 以便我们可以进行自信体验。</span><span class="sxs-lookup"><span data-stu-id="c953e-237">In the next exercise, we'll isolate the software in a container on the VM so we can experiment with confidence.</span></span>

4. <span data-ttu-id="c953e-238">完成笔记本后, 可以`Control-C`在云命令行管理程序中停止 Jupyter 服务器。</span><span class="sxs-lookup"><span data-stu-id="c953e-238">When you have finished with the notebook, you can stop the Jupyter server with `Control-C` in the Cloud Shell.</span></span>
