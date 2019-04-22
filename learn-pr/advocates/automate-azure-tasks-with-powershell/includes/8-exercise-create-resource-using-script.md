在此单元中, 你将继续使用一个构成 Linux 管理员工具的公司的示例。 请记住, 您计划使用 Linux 虚拟机以让潜在客户测试您的软件。 您有资源组准备好了, 现在是时候创建虚拟机了。

你的公司已在大型 Linux 商业展览上为展台付费。 您规划一个演示区域, 其中包含每个连接到单独 Linux VM 的终端。 在每天结束时, 您想要删除并重新创建虚拟机, 以便它们每天在上午开始进行刷新。 如果在您厌倦时手动创建 vm, 则会容易出错。 您希望编写 PowerShell 脚本以自动执行 VM 创建过程。

## <a name="write-a-script-that-creates-virtual-machines"></a>编写用于创建虚拟机的脚本

请在右侧的云命令行管理程序中执行以下步骤, 以编写脚本:

1. 切换到云命令行管理程序中的主文件夹。

    ```powershell
    cd $HOME\clouddrive
    ```

1. 创建一个名为**ConferenceDailyReset**的新文本文件。

    ```powershell
    touch "./ConferenceDailyReset.ps1"
    ```

1. 打开集成编辑器并选择**ConferenceDailyReset**文件。

    ```powershell
    code "./ConferenceDailyReset.ps1"
    ```
    > [!TIP]
    > 集成云命令行管理程序还支持 vim、nano 和 emacs (如果您希望使用其中一个编辑器)。

1. 首先, 在变量中捕获输入参数。 在脚本中添加以下行:

    ```powershell
    param([string]$resourceGroup)
    ```

    > [!NOTE]
    > 通常情况下, 您必须使用您的凭据通过 Azure 进行`Connect-AzAccount`身份验证, 并且可以在脚本中执行此操作。 但是, 在云命令行管理程序环境中, 您将已经过身份验证, 因此这是不必要的。

1. 为 VM 的管理员帐户提示输入用户名和密码, 并将结果捕获到变量中:

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. 创建一个执行三次的循环:

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

1. 在循环正文中, 为每个 VM 创建一个名称, 并将其存储在一个变量中, 并将其输出到控制台:

    ```powershell
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    ```

1. 接下来, 使用`$vmName`变量创建 VM:

   ```powershell
   New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
   ```

1. 保存该文件。 您可以使用 "..."编辑器右上角的菜单。 还有用于保存的常用加速键。

已完成的脚本应如下所示:

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a>执行脚本

通过 "..." 关闭编辑器。上下文菜单。

1. 执行脚本。

    ```powershell
    .\ConferenceDailyReset.ps1 <rgn>[sandbox resource group name]</rgn>
    ```
    
脚本将需要几分钟的时间才能完成。 完成后, 通过查看您在资源组中现在所拥有的资源来验证它是否成功运行:

```powershell
Get-AzResource -ResourceType Microsoft.Compute/virtualMachines
```

您应该会看到三个虚拟机, 每个虚拟机具有唯一的名称。

您编写了一个脚本, 该脚本可自动创建由 script 参数指示的资源组中的三个虚拟机。 该脚本非常简短且简单, 但自动化了需要很长时间才能通过门户手动完成的过程。