在本模块中, 我们编写了一个脚本来自动创建多个虚拟机。 尽管脚本相对较短, 但在从 PowerShell 中组合循环、变量和函数时, 可以使用 Azure PowerShell 中的 cmdlet 来查看潜在的功能。

Azure powershell 是具有 PowerShell 体验的管理员的一种好的自动化选择。 清理语法和功能强大的脚本语言的组合还可以考虑, 即使您是在 PowerShell 中的新功能。 这种自动化的耗时和易出错的任务应有助于减少管理时间和提高质量。

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

当您在自己的订阅中运行时, 可以使用下面的 PowerShell cmdlet 删除资源组 (以及所有相关资源)。

```powershell
Remove-AzResourceGroup -Name MyResourceGroupName
```

当系统询问您确认删除操作时, 回答 **"是"**, 或者您可以`-Force`添加参数以跳过提示。 此命令可能需要几分钟的时间才能完成。