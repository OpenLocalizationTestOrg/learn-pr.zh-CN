<span data-ttu-id="82993-101">我们用于`Debian`创建虚拟机的图像。</span><span class="sxs-lookup"><span data-stu-id="82993-101">We used `Debian` for the image to create the virtual machine.</span></span> <span data-ttu-id="82993-102">Azure 具有几个可用于创建虚拟机的标准 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="82993-102">Azure has several standard VM images you can use to create a virtual machine.</span></span> 

## <a name="listing-images"></a><span data-ttu-id="82993-103">列出图像</span><span class="sxs-lookup"><span data-stu-id="82993-103">Listing images</span></span>

<span data-ttu-id="82993-104">您可以使用以下命令获取可用虚拟机映像的列表。</span><span class="sxs-lookup"><span data-stu-id="82993-104">You can get a list of the available VM images using the following command.</span></span> 

```azurecli
az vm image list --output table
```

<span data-ttu-id="82993-105">这将输出属于 Azure CLI 内置的脱机列表的最热门图像。</span><span class="sxs-lookup"><span data-stu-id="82993-105">This will output the most popular images that are part of an offline list built into the Azure CLI.</span></span> <span data-ttu-id="82993-106">但是, Azure Marketplace 中有_数百_个可用的图像选项。</span><span class="sxs-lookup"><span data-stu-id="82993-106">However, there are _hundreds_ of image options available in the Azure Marketplace.</span></span> 

## <a name="getting-all-images"></a><span data-ttu-id="82993-107">获取所有图像</span><span class="sxs-lookup"><span data-stu-id="82993-107">Getting all images</span></span>

<span data-ttu-id="82993-108">您可以通过向命令中添加`--all`标志来获取完整列表。</span><span class="sxs-lookup"><span data-stu-id="82993-108">You can get a full list by adding the `--all` flag to the command.</span></span> <span data-ttu-id="82993-109">由于 Marketplace 中的图像列表非常大, 因此使用`--publisher` `--sku`或`–-offer`选项筛选列表非常有用。</span><span class="sxs-lookup"><span data-stu-id="82993-109">Since the list of images in the Marketplace is very large, it is helpful to filter the list with the `--publisher`, `--sku` or `–-offer` options.</span></span>

<span data-ttu-id="82993-110">例如, 尝试以下命令以查看_所有_可用的 Wordpress 图像:</span><span class="sxs-lookup"><span data-stu-id="82993-110">For example, try the following command to see _all_ Wordpress images available:</span></span>

```azurecli
az vm image list --sku Wordpress --output table --all
```

<span data-ttu-id="82993-111">或此命令查看由 Microsoft 提供的所有图像:</span><span class="sxs-lookup"><span data-stu-id="82993-111">Or this command to see all images provided by Microsoft:</span></span>

```azurecli
az vm image list --publisher Microsoft --output table --all
```

## <a name="location-specific-images"></a><span data-ttu-id="82993-112">特定位置的图像</span><span class="sxs-lookup"><span data-stu-id="82993-112">Location-specific images</span></span>

<span data-ttu-id="82993-113">某些图像仅在某些位置可用。</span><span class="sxs-lookup"><span data-stu-id="82993-113">Some images are only available in certain locations.</span></span> <span data-ttu-id="82993-114">尝试向命令`--location [location]`中添加标志, 以将结果限定为您要在其中创建虚拟机的区域中可用的结果。</span><span class="sxs-lookup"><span data-stu-id="82993-114">Try adding the `--location [location]` flag to the command to scope the results to ones available in the region where you want to create the virtual machine.</span></span> <span data-ttu-id="82993-115">例如, 在 Azure 云命令行管理程序中键入以下命令, 以获取`eastus`区域中可用图像的列表。</span><span class="sxs-lookup"><span data-stu-id="82993-115">For example, type the following into Azure Cloud Shell to get a list of images available in the `eastus` region.</span></span>

```azurecli
az vm image list --location eastus --output table
```

<span data-ttu-id="82993-116">请尝试检查其他 Azure 沙箱可用位置中的部分图像:</span><span class="sxs-lookup"><span data-stu-id="82993-116">Try checking some of the images in the other Azure sandbox available locations:</span></span>

[!include[](../../../includes/azure-sandbox-regions-note.md)]

> [!TIP]
> <span data-ttu-id="82993-117">这些是由 Azure 提供的标准映像。</span><span class="sxs-lookup"><span data-stu-id="82993-117">These are the standard images that are provided by Azure.</span></span> <span data-ttu-id="82993-118">请记住, 您还可以[创建和上传自己的自定义图像](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images), 以根据独特的配置或不太常见的操作系统版本或操作系统分布来创建虚拟机。</span><span class="sxs-lookup"><span data-stu-id="82993-118">Keep in mind that you can also [create and upload your own custom images](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) to create VMs based on unique configurations or less common versions or distributions of an operating system.</span></span>

<span data-ttu-id="82993-119">你的命令窗口可能已满。现在, 你`clear`可以键入以根据需要清除屏幕。</span><span class="sxs-lookup"><span data-stu-id="82993-119">Your command window is probably full now, you can type `clear` to clear the screen if you like.</span></span>