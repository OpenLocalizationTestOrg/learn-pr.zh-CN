<span data-ttu-id="f12b7-101">在本模块中, 我们编写了一个脚本来自动创建多个虚拟机。</span><span class="sxs-lookup"><span data-stu-id="f12b7-101">In this module, we wrote a script to automate the creation of multiple VMs.</span></span> <span data-ttu-id="f12b7-102">尽管脚本相对较短, 但在从 PowerShell 中组合循环、变量和函数时, 可以使用 Azure PowerShell 中的 cmdlet 来查看潜在的功能。</span><span class="sxs-lookup"><span data-stu-id="f12b7-102">Even though the script was relatively short, you can see the potential power when you combine loops, variables, and functions from PowerShell with cmdlets from Azure PowerShell.</span></span>

<span data-ttu-id="f12b7-103">Azure powershell 是具有 PowerShell 体验的管理员的一种好的自动化选择。</span><span class="sxs-lookup"><span data-stu-id="f12b7-103">Azure PowerShell is a good automation choice for admins with PowerShell experience.</span></span> <span data-ttu-id="f12b7-104">清理语法和功能强大的脚本语言的组合还可以考虑, 即使您是在 PowerShell 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="f12b7-104">The combination of clean syntax and a powerful scripting language also makes it worth considering even if you are new to PowerShell.</span></span> <span data-ttu-id="f12b7-105">这种自动化的耗时和易出错的任务应有助于减少管理时间和提高质量。</span><span class="sxs-lookup"><span data-stu-id="f12b7-105">This level of automation for time-consuming and error-prone tasks should help you reduce administrative time and increase quality.</span></span>

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

<span data-ttu-id="f12b7-106">当您在自己的订阅中运行时, 可以使用下面的 PowerShell cmdlet 删除资源组 (以及所有相关资源)。</span><span class="sxs-lookup"><span data-stu-id="f12b7-106">When you are running in your own subscription, you can use the following PowerShell cmdlet to delete the resource group (and all related resources).</span></span>

```powershell
Remove-AzResourceGroup -Name MyResourceGroupName
```

<span data-ttu-id="f12b7-107">当系统询问您确认删除操作时, 回答 **"是"**, 或者您可以`-Force`添加参数以跳过提示。</span><span class="sxs-lookup"><span data-stu-id="f12b7-107">When you are asked to confirm the delete, answer **Yes**, or you can add the `-Force` parameter to skip the prompt.</span></span> <span data-ttu-id="f12b7-108">此命令可能需要几分钟的时间才能完成。</span><span class="sxs-lookup"><span data-stu-id="f12b7-108">The command may take several minutes to complete.</span></span>