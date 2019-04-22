复杂或重复性的任务通常会花费大量的管理时间。 组织更愿意自动执行这些任务, 以降低成本并避免错误。

这在客户关系管理 (CRM) 公司的示例中非常重要。 其中, 您在需要连续删除和重新创建的多个 Linux 虚拟机 (vm) 上测试您的软件。 您希望使用 PowerShell 脚本自动创建 vm, 而不是像我们刚刚这样做时手动创建。

除了创建虚拟机的核心操作之外, 还可以为脚本提供一些额外要求。 
- 您将创建多个虚拟机, 因此您需要将创建放在一个循环中
- 您需要在三个不同的资源组中创建虚拟机, 因此资源组的名称应作为参数传递给脚本

在本节中, 您将了解如何编写和执行符合这些要求的 Azure PowerShell 脚本。

## <a name="what-is-a-powershell-script"></a>什么是 PowerShell 脚本？
PowerShell 脚本是包含命令和控件构造的文本文件。 命令是对 cmdlet 的调用。 控件构造是由 PowerShell 提供的编程功能, 如循环、变量、参数、注释等。

PowerShell 脚本文件的文件扩展名为 **. ps1** 。 您可以使用任何文本编辑器创建和保存这些文件。 

> [!TIP]
> 如果要在 windows 下编写 PowerShell 脚本, 可以使用 windows PowerShell 集成脚本环境 (ISE)。 此编辑器提供了一些功能, 如语法着色和可用 cmdlet 的列表。
>
下面的屏幕截图显示了 Windows PowerShell 集成脚本环境 (ISE), 并提供了连接到 azure 的示例脚本, 并在 azure 中创建虚拟机。

>![Windows PowerShell 集成脚本环境的屏幕截图, 其中包含用于创建在编辑窗口中打开的虚拟机的脚本。](../media/7-windows-powershell-ise-screenshot.png)

编写脚本后, 通过传递以点和反斜杠开头的文件的名称, 从 PowerShell 命令行执行该脚本:

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a>PowerShell 技术
PowerShell 具有在典型编程语言中发现的许多功能。 您可以定义变量、使用分支和循环、捕获命令行参数、写入函数、添加注释等等。 我们将需要脚本的三个功能: 变量、循环和参数。

### <a name="variables"></a>Variables
正如您在最后一个单位中看到的那样, PowerShell 支持变量。 使用**$** 声明变量并**=** 分配值。 例如：

```powershell
$loc = "East US"
$iterations = 3
```

变量可以包含对象。 例如, 以下定义将**adminCredential**变量设置为**Get Credential** cmdlet 返回的对象。

```powershell
$adminCredential = Get-Credential
```

若要获取存储在变量中的值, 请**$** 使用前缀及其名称, 如下所示: 

```powershell
$loc = "East US"
New-AzResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a>陷入
PowerShell 具有多个循环: **For**, **Do .。。While**,**为 .。。** 等。 **for**循环是满足我们需求的最佳匹配, 因为我们将按固定次数执行 cmdlet。

下面显示了核心语法;本示例为两次迭代运行, 并每次打印**i**的值。 比较运算符是为 "小于"、 **-le** "小于或等于"、"等于"、"等于" **** 、"不相等" 等**** 写入 **-lt** 。

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a>参数
当您执行脚本时, 可以在命令行上传递参数。 您可以为每个参数提供名称, 以帮助脚本提取值。 例如：

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

在脚本中, 将值捕获到变量中。 在此示例中, 参数按名称进行匹配:

```powershell
param([string]$location, [int]$size)
```

您可以省略命令行中的名称。 例如：

```powershell
.\setupEnvironment.ps1 5 "East US"
```

在脚本中, 您依赖于在参数未命名时进行匹配的位置:

```powershell
param([int]$size, [string]$location)
```

我们可以将这些参数作为输入, 并使用循环从给定的参数创建一组虚拟机。 我们将尝试下一步。

PowerShell 和 Azure powershell 的组合为你提供了自动化 Azure 所需的所有工具。 在我们的 CRM 示例中, 我们将能够使用参数创建多个 Linux 虚拟机, 以保持脚本为泛型和循环以避免重复的代码。 这意味着, 现在可以在单个步骤中执行以前的复杂操作。