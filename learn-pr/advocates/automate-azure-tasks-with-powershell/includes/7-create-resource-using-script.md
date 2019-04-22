<span data-ttu-id="79a57-101">复杂或重复性的任务通常会花费大量的管理时间。</span><span class="sxs-lookup"><span data-stu-id="79a57-101">Complex or repetitive tasks often take a great deal of administrative time.</span></span> <span data-ttu-id="79a57-102">组织更愿意自动执行这些任务, 以降低成本并避免错误。</span><span class="sxs-lookup"><span data-stu-id="79a57-102">Organizations prefer to automate these tasks to reduce costs and avoid errors.</span></span>

<span data-ttu-id="79a57-103">这在客户关系管理 (CRM) 公司的示例中非常重要。</span><span class="sxs-lookup"><span data-stu-id="79a57-103">This is important in the Customer Relationship Management (CRM) company example.</span></span> <span data-ttu-id="79a57-104">其中, 您在需要连续删除和重新创建的多个 Linux 虚拟机 (vm) 上测试您的软件。</span><span class="sxs-lookup"><span data-stu-id="79a57-104">There, you test your software on multiple Linux Virtual Machines (VMs) that you need to continuously delete and recreate.</span></span> <span data-ttu-id="79a57-105">您希望使用 PowerShell 脚本自动创建 vm, 而不是像我们刚刚这样做时手动创建。</span><span class="sxs-lookup"><span data-stu-id="79a57-105">You want to use a PowerShell script to automate the creation of the VMs vs. creating them manually each time like we just did.</span></span>

<span data-ttu-id="79a57-106">除了创建虚拟机的核心操作之外, 还可以为脚本提供一些额外要求。</span><span class="sxs-lookup"><span data-stu-id="79a57-106">Beyond the core operation of creating a VM you have a few additional requirements for your script.</span></span> 
- <span data-ttu-id="79a57-107">您将创建多个虚拟机, 因此您需要将创建放在一个循环中</span><span class="sxs-lookup"><span data-stu-id="79a57-107">You will create multiple VMs, so you want to put the creation inside a loop</span></span>
- <span data-ttu-id="79a57-108">您需要在三个不同的资源组中创建虚拟机, 因此资源组的名称应作为参数传递给脚本</span><span class="sxs-lookup"><span data-stu-id="79a57-108">You need to create VMs in three different resource groups, so the name of the resource group should be passed to the script as a parameter</span></span>

<span data-ttu-id="79a57-109">在本节中, 您将了解如何编写和执行符合这些要求的 Azure PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="79a57-109">In this section, you will see how to write and execute an Azure PowerShell script that meets these requirements.</span></span>

## <a name="what-is-a-powershell-script"></a><span data-ttu-id="79a57-110">什么是 PowerShell 脚本？</span><span class="sxs-lookup"><span data-stu-id="79a57-110">What is a PowerShell script?</span></span>
<span data-ttu-id="79a57-111">PowerShell 脚本是包含命令和控件构造的文本文件。</span><span class="sxs-lookup"><span data-stu-id="79a57-111">A PowerShell script is a text file containing commands and control constructs.</span></span> <span data-ttu-id="79a57-112">命令是对 cmdlet 的调用。</span><span class="sxs-lookup"><span data-stu-id="79a57-112">The commands are invocations of cmdlets.</span></span> <span data-ttu-id="79a57-113">控件构造是由 PowerShell 提供的编程功能, 如循环、变量、参数、注释等。</span><span class="sxs-lookup"><span data-stu-id="79a57-113">The control constructs are programming features like loops, variables, parameters, comments, etc. supplied by PowerShell.</span></span>

<span data-ttu-id="79a57-114">PowerShell 脚本文件的文件扩展名为 **. ps1** 。</span><span class="sxs-lookup"><span data-stu-id="79a57-114">PowerShell script files have a **.ps1** file extension.</span></span> <span data-ttu-id="79a57-115">您可以使用任何文本编辑器创建和保存这些文件。</span><span class="sxs-lookup"><span data-stu-id="79a57-115">You can create and save these files with any text editor.</span></span> 

> [!TIP]
> <span data-ttu-id="79a57-116">如果要在 windows 下编写 PowerShell 脚本, 可以使用 windows PowerShell 集成脚本环境 (ISE)。</span><span class="sxs-lookup"><span data-stu-id="79a57-116">If you’re writing PowerShell scripts under Windows, you can use the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="79a57-117">此编辑器提供了一些功能, 如语法着色和可用 cmdlet 的列表。</span><span class="sxs-lookup"><span data-stu-id="79a57-117">This editor provides features such as syntax coloring and a list of available cmdlets.</span></span>
>
<span data-ttu-id="79a57-118">下面的屏幕截图显示了 Windows PowerShell 集成脚本环境 (ISE), 并提供了连接到 azure 的示例脚本, 并在 azure 中创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="79a57-118">The following screenshot shows the Windows PowerShell Integrated Scripting Environment (ISE) with a sample script to connect to Azure and create a virtual machine in Azure.</span></span>

>![Windows PowerShell 集成脚本环境的屏幕截图, 其中包含用于创建在编辑窗口中打开的虚拟机的脚本。](../media/7-windows-powershell-ise-screenshot.png)

<span data-ttu-id="79a57-120">编写脚本后, 通过传递以点和反斜杠开头的文件的名称, 从 PowerShell 命令行执行该脚本:</span><span class="sxs-lookup"><span data-stu-id="79a57-120">Once you have written the script, execute it from the PowerShell command line by passing the name of the file preceded by a dot and a backslash:</span></span>

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a><span data-ttu-id="79a57-121">PowerShell 技术</span><span class="sxs-lookup"><span data-stu-id="79a57-121">PowerShell techniques</span></span>
<span data-ttu-id="79a57-122">PowerShell 具有在典型编程语言中发现的许多功能。</span><span class="sxs-lookup"><span data-stu-id="79a57-122">PowerShell has many features found in typical programming languages.</span></span> <span data-ttu-id="79a57-123">您可以定义变量、使用分支和循环、捕获命令行参数、写入函数、添加注释等等。</span><span class="sxs-lookup"><span data-stu-id="79a57-123">You can define variables, use branches and loops, capture command-line parameters, write functions, add comments, and so on.</span></span> <span data-ttu-id="79a57-124">我们将需要脚本的三个功能: 变量、循环和参数。</span><span class="sxs-lookup"><span data-stu-id="79a57-124">We will need three features for our script: variables, loops, and parameters.</span></span>

### <a name="variables"></a><span data-ttu-id="79a57-125">Variables</span><span class="sxs-lookup"><span data-stu-id="79a57-125">Variables</span></span>
<span data-ttu-id="79a57-126">正如您在最后一个单位中看到的那样, PowerShell 支持变量。</span><span class="sxs-lookup"><span data-stu-id="79a57-126">As you saw in the last unit, PowerShell supports variables.</span></span> <span data-ttu-id="79a57-127">使用**$** 声明变量并**=** 分配值。</span><span class="sxs-lookup"><span data-stu-id="79a57-127">Use **$** to declare a variable and **=** to assign a value.</span></span> <span data-ttu-id="79a57-128">例如：</span><span class="sxs-lookup"><span data-stu-id="79a57-128">For example:</span></span>

```powershell
$loc = "East US"
$iterations = 3
```

<span data-ttu-id="79a57-129">变量可以包含对象。</span><span class="sxs-lookup"><span data-stu-id="79a57-129">Variables can hold objects.</span></span> <span data-ttu-id="79a57-130">例如, 以下定义将**adminCredential**变量设置为**Get Credential** cmdlet 返回的对象。</span><span class="sxs-lookup"><span data-stu-id="79a57-130">For example, the following definition sets the **adminCredential** variable to the object returned by the **Get-Credential** cmdlet.</span></span>

```powershell
$adminCredential = Get-Credential
```

<span data-ttu-id="79a57-131">若要获取存储在变量中的值, 请**$** 使用前缀及其名称, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="79a57-131">To obtain the value stored in a variable, use the **$** prefix and its name as shown below:</span></span> 

```powershell
$loc = "East US"
New-AzResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a><span data-ttu-id="79a57-132">陷入</span><span class="sxs-lookup"><span data-stu-id="79a57-132">Loops</span></span>
<span data-ttu-id="79a57-133">PowerShell 具有多个循环: **For**, **Do .。。While**,**为 .。。** 等。</span><span class="sxs-lookup"><span data-stu-id="79a57-133">PowerShell has several loops: **For**, **Do...While**, **For...Each**, and so on.</span></span> <span data-ttu-id="79a57-134">**for**循环是满足我们需求的最佳匹配, 因为我们将按固定次数执行 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="79a57-134">The **For** loop is the best match for our needs because we will execute a cmdlet a fixed number of times.</span></span>

<span data-ttu-id="79a57-135">下面显示了核心语法;本示例为两次迭代运行, 并每次打印**i**的值。</span><span class="sxs-lookup"><span data-stu-id="79a57-135">The core syntax is shown below; the example runs for two iterations and prints the value of **i** each time.</span></span> <span data-ttu-id="79a57-136">比较运算符是为 "小于"、 **-le** "小于或等于"、"等于"、"等于" \*\*\*\* 、"不相等" 等\*\*\*\* 写入 **-lt** 。</span><span class="sxs-lookup"><span data-stu-id="79a57-136">The comparison operators are written **-lt** for "less than", **-le** for "less than or equal", **eq** for "equal", **ne** for "not equal", etc.</span></span>

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a><span data-ttu-id="79a57-137">参数</span><span class="sxs-lookup"><span data-stu-id="79a57-137">Parameters</span></span>
<span data-ttu-id="79a57-138">当您执行脚本时, 可以在命令行上传递参数。</span><span class="sxs-lookup"><span data-stu-id="79a57-138">When you execute a script, you can pass arguments on the command line.</span></span> <span data-ttu-id="79a57-139">您可以为每个参数提供名称, 以帮助脚本提取值。</span><span class="sxs-lookup"><span data-stu-id="79a57-139">You can provide names for each parameter to help the script extract the values.</span></span> <span data-ttu-id="79a57-140">例如：</span><span class="sxs-lookup"><span data-stu-id="79a57-140">For example:</span></span>

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

<span data-ttu-id="79a57-141">在脚本中, 将值捕获到变量中。</span><span class="sxs-lookup"><span data-stu-id="79a57-141">Inside the script, you capture the values into variables.</span></span> <span data-ttu-id="79a57-142">在此示例中, 参数按名称进行匹配:</span><span class="sxs-lookup"><span data-stu-id="79a57-142">In this example, the parameters are matched by name:</span></span>

```powershell
param([string]$location, [int]$size)
```

<span data-ttu-id="79a57-143">您可以省略命令行中的名称。</span><span class="sxs-lookup"><span data-stu-id="79a57-143">You can omit the names from the command line.</span></span> <span data-ttu-id="79a57-144">例如：</span><span class="sxs-lookup"><span data-stu-id="79a57-144">For example:</span></span>

```powershell
.\setupEnvironment.ps1 5 "East US"
```

<span data-ttu-id="79a57-145">在脚本中, 您依赖于在参数未命名时进行匹配的位置:</span><span class="sxs-lookup"><span data-stu-id="79a57-145">Inside the script, you rely on position for matching when the parameters are unnamed:</span></span>

```powershell
param([int]$size, [string]$location)
```

<span data-ttu-id="79a57-146">我们可以将这些参数作为输入, 并使用循环从给定的参数创建一组虚拟机。</span><span class="sxs-lookup"><span data-stu-id="79a57-146">We could take these parameters as input, and use a loop to create a set of VMs from the given parameters.</span></span> <span data-ttu-id="79a57-147">我们将尝试下一步。</span><span class="sxs-lookup"><span data-stu-id="79a57-147">We'll try that next.</span></span>

<span data-ttu-id="79a57-148">PowerShell 和 Azure powershell 的组合为你提供了自动化 Azure 所需的所有工具。</span><span class="sxs-lookup"><span data-stu-id="79a57-148">The combination of PowerShell and Azure PowerShell gives you all the tools you need to automate Azure.</span></span> <span data-ttu-id="79a57-149">在我们的 CRM 示例中, 我们将能够使用参数创建多个 Linux 虚拟机, 以保持脚本为泛型和循环以避免重复的代码。</span><span class="sxs-lookup"><span data-stu-id="79a57-149">In our CRM example, we will be able to create multiple Linux VMs using a parameter to keep the script generic and a loop to avoid repeated code.</span></span> <span data-ttu-id="79a57-150">这意味着, 现在可以在单个步骤中执行以前的复杂操作。</span><span class="sxs-lookup"><span data-stu-id="79a57-150">This means that a formerly complex operation can now be executed in a single step.</span></span>