我们用于`Debian`创建虚拟机的图像。 Azure 具有几个可用于创建虚拟机的标准 VM 映像。 

## <a name="listing-images"></a>列出图像

您可以使用以下命令获取可用虚拟机映像的列表。 

```azurecli
az vm image list --output table
```

这将输出属于 Azure CLI 内置的脱机列表的最热门图像。 但是, Azure Marketplace 中有_数百_个可用的图像选项。 

## <a name="getting-all-images"></a>获取所有图像

您可以通过向命令中添加`--all`标志来获取完整列表。 由于 Marketplace 中的图像列表非常大, 因此使用`--publisher` `--sku`或`–-offer`选项筛选列表非常有用。

例如, 尝试以下命令以查看_所有_可用的 Wordpress 图像:

```azurecli
az vm image list --sku Wordpress --output table --all
```

或此命令查看由 Microsoft 提供的所有图像:

```azurecli
az vm image list --publisher Microsoft --output table --all
```

## <a name="location-specific-images"></a>特定位置的图像

某些图像仅在某些位置可用。 尝试向命令`--location [location]`中添加标志, 以将结果限定为您要在其中创建虚拟机的区域中可用的结果。 例如, 在 Azure 云命令行管理程序中键入以下命令, 以获取`eastus`区域中可用图像的列表。

```azurecli
az vm image list --location eastus --output table
```

请尝试检查其他 Azure 沙箱可用位置中的部分图像:

[!include[](../../../includes/azure-sandbox-regions-note.md)]

> [!TIP]
> 这些是由 Azure 提供的标准映像。 请记住, 您还可以[创建和上传自己的自定义图像](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images), 以根据独特的配置或不太常见的操作系统版本或操作系统分布来创建虚拟机。

你的命令窗口可能已满。现在, 你`clear`可以键入以根据需要清除屏幕。