<span data-ttu-id="2204e-101">在此单元中, 您将向 Artworks 项目添加 Picasso、Pollock 和 Rembrandt 的著名 paintings 的图像。</span><span class="sxs-lookup"><span data-stu-id="2204e-101">In this unit, you'll add images of famous paintings by Picasso, Pollock, and Rembrandt to the Artworks project.</span></span> <span data-ttu-id="2204e-102">你将标记图像, 以便自定义视觉服务可以学习将一个艺术家与另一个艺术家区分开来。</span><span class="sxs-lookup"><span data-stu-id="2204e-102">You'll tag the images so the Custom Vision Service can learn to differentiate one artist from another.</span></span>

1. <span data-ttu-id="2204e-103">在我们创建的**Artworks**项目中, 选择侧面板中**+\*\*\*\*标记**右侧的加号 ()。</span><span class="sxs-lookup"><span data-stu-id="2204e-103">In the **Artworks** project that we created, select the plus sign (**+**) to the right of **Tags** in the side panel.</span></span>

     ![突出显示了加号的 Artworks 项目左侧面板的屏幕截图。](../media/2-add-tags.png)

1. <span data-ttu-id="2204e-105">将显示一个名为 **"名称" 的**对话框。</span><span class="sxs-lookup"><span data-stu-id="2204e-105">A dialog called **Name the tag** is displayed.</span></span> <span data-ttu-id="2204e-106">在 "标记名称" 字段中键入*painting* , 然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="2204e-106">Type *painting* into the tag name field and select **Save**.</span></span> <span data-ttu-id="2204e-107">此操作将在标记列表中创建标记*绘画*。</span><span class="sxs-lookup"><span data-stu-id="2204e-107">This operation creates the tag *painting* in the tag list.</span></span> <span data-ttu-id="2204e-108">让我们再添加一些。</span><span class="sxs-lookup"><span data-stu-id="2204e-108">Let's add some more.</span></span> 

1. <span data-ttu-id="2204e-109">重复步骤1和步骤 2, 添加值为*Picasso*、 *Pollock*和*Rembrandt*的标记。</span><span class="sxs-lookup"><span data-stu-id="2204e-109">Repeat steps 1 and 2 to add tags with the values *Picasso*, *Pollock*, and *Rembrandt*.</span></span> <span data-ttu-id="2204e-110">完成后, 标记列表看起来就像以下形式。</span><span class="sxs-lookup"><span data-stu-id="2204e-110">The tag list will look like the following when you are finished.</span></span>

    ![列出在上述步骤中创建的所有标记的 "标记" 部分的屏幕截图](../media/2-tag-list.png)

    <span data-ttu-id="2204e-112">正如您所看到的, 项目中使用每个标记标记的图像数量为零。</span><span class="sxs-lookup"><span data-stu-id="2204e-112">As you can see, the number of images in our project that are tagged with each of these tags is zero.</span></span> <span data-ttu-id="2204e-113">让我们将一些图像添加到项目并为其分配标签。</span><span class="sxs-lookup"><span data-stu-id="2204e-113">Let's add some images to our project and assign tags.</span></span>

1. <span data-ttu-id="2204e-114">下载包含此模块的图像资源的[cvs-resources](https://github.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/raw/master/cvs-resources.zip) , 并将其解压缩到本地计算机。</span><span class="sxs-lookup"><span data-stu-id="2204e-114">Download [cvs-resources.zip](https://github.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/raw/master/cvs-resources.zip) which contains image resources for this module and unzip it to your local machine.</span></span> 

1. <span data-ttu-id="2204e-115">返回门户中, 选择 "**添加图像**" 以将图像添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="2204e-115">Back in the portal, select **Add images** to add images to the project.</span></span>

    ![突出显示 "添加图像" 按钮的 Artworks 项目的屏幕截图](../media/2-portal-click-add-images.png)

1. <span data-ttu-id="2204e-117">在您在步骤4中本地下载的 " **cvs 资源**" 文件夹中, 导航到 "Artists\Picasso" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="2204e-117">In the **cvs-resources** folder that you downloaded locally in step 4, navigate to the "Artists\Picasso" folder.</span></span>

1. <span data-ttu-id="2204e-118">选择 "Artists\Picasso" 中的所有文件, 然后选择 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="2204e-118">Select all of the files in "Artists\Picasso", and then select **Open**.</span></span>

    ![<span data-ttu-id="2204e-119">选定了所有图像文件且突出显示 "打开" 按钮的 Picasso 文件夹的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="2204e-119">Screenshot of the Picasso folder with all the image files selected and the Open button highlighted</span></span> ](../media/2-fe-browse-picasso-01.png)

1. <span data-ttu-id="2204e-120">此时将显示 "**图像上载**" 对话框, 并显示正在上载的所有图像的缩略图。</span><span class="sxs-lookup"><span data-stu-id="2204e-120">The **Image upload** dialog appears and displays thumbnails of all the images we are uploading.</span></span> <span data-ttu-id="2204e-121">选择 "**我的标记**" 字段, 这将打开一个标记下拉列表, 您可以分配这些图像。</span><span class="sxs-lookup"><span data-stu-id="2204e-121">Select the **My Tags** field, which opens a dropdown of the tags you can assign these images.</span></span>

    ![显示 Picasso 图像缩略图和 "我的标记" 下拉列表中所有标记的 "图像上载" 对话框的屏幕截图](../media/2-upload-picasso-tags.png)

1. <span data-ttu-id="2204e-123">选择 "标签" "*画图*" 和 " *Picasso* ", 然后选择 "**上传7个文件**" 完成上载。</span><span class="sxs-lookup"><span data-stu-id="2204e-123">Select the tags *painting* and *Picasso* and then select **Upload 7 files** to finish the upload.</span></span> 

1. <span data-ttu-id="2204e-124">确认您上载的图像现在位于 Artworks 项目中, 并且已更新标签列表, 以表明我们已通过*Picasso*和*涂色*标记了七个图像。</span><span class="sxs-lookup"><span data-stu-id="2204e-124">Confirm that the images you uploaded are now in the Artworks project, and that the tag list has been updated to show that we've tagged seven images with *Picasso* and *painting*.</span></span>

    ![显示上载的图像的 Artworks 项目的屏幕截图。](../media/2-portal-tagged-01.png)

1. <span data-ttu-id="2204e-127">使用七个 Picasso 图像, 自定义的远景服务可执行一份相当于通过 Picasso 识别 paintings 的作业。</span><span class="sxs-lookup"><span data-stu-id="2204e-127">With seven Picasso images, the Custom Vision Service can do a decent job of identifying paintings by Picasso.</span></span> <span data-ttu-id="2204e-128">但如果现在已对模型进行了培训, 它只会了解 Picasso 的外观, 并且无法识别其他艺术家的 paintings。</span><span class="sxs-lookup"><span data-stu-id="2204e-128">But if you trained the model right now, it would only understand what a Picasso looks like, and it wouldn't be able to identify paintings by other artists.</span></span> <span data-ttu-id="2204e-129">下一步是通过另一个艺术家上传一些 paintings。</span><span class="sxs-lookup"><span data-stu-id="2204e-129">The next step is to upload some paintings by another artist.</span></span> 

1. <span data-ttu-id="2204e-130">选择 "**添加图像**", 并在模块资源中选择 "Artists\Rembrandt" 文件夹中的所有图像。</span><span class="sxs-lookup"><span data-stu-id="2204e-130">Select **Add images** and select all of the images in the "Artists\Rembrandt" folder in the module resources.</span></span> <span data-ttu-id="2204e-131">使用标签 "painting" 和 "Rembrandt" (不是 "Picasso") 标记它们, 然后选择 "**上传6个文件**" 以将它们上载到项目中。</span><span class="sxs-lookup"><span data-stu-id="2204e-131">Tag them with the labels "painting" and "Rembrandt" (not "Picasso"), and select **Upload 6 files** to upload them to the project.</span></span>

    ![显示 Rembrandt 图像缩略图以及选定的绘画和 Rembrandt 标记的 "图像上载" 对话框的屏幕截图](../media/2-upload-rembrandt.png)

1. <span data-ttu-id="2204e-133">确认 Rembrandt 图像显示在项目中的 Picasso 图像旁边, 并且标记列表中显示 "Rembrandt"。</span><span class="sxs-lookup"><span data-stu-id="2204e-133">Confirm that the Rembrandt images appear alongside the Picasso images in the project, and that "Rembrandt" appears in the list of tags.</span></span>

    ![显示上载的图像的 Artworks 项目的屏幕截图。在左侧面板中的 "标记" 下选择 "Picasso"、"Rembrandt" 和 "涂色" 标记。](../media/2-portal-tagged-02.png)

1. <span data-ttu-id="2204e-135">现在, 通过 enigmatic 艺术家杰克逊 Pollock 添加 paintings, 以使自定义视觉服务也能识别 Pollock paintings。</span><span class="sxs-lookup"><span data-stu-id="2204e-135">Now add paintings by the enigmatic artist Jackson Pollock to enable the Custom Vision Service to recognize Pollock paintings, too.</span></span> <span data-ttu-id="2204e-136">在模块资源中选择 "Artists\Pollock" 文件夹中的所有图像, 使用术语 "painting" 和 "Pollock" 对其进行标记, 并将它们上载到项目中。</span><span class="sxs-lookup"><span data-stu-id="2204e-136">Select all of the images in the "Artists\Pollock" folder in the module resources, tag them with the terms "painting" and "Pollock", and upload them to the project.</span></span>

<span data-ttu-id="2204e-137">在上传带标签的图像后, 下一步是使用这些图像来培训模型, 以便它可以区分 paintings (通过 Picasso、Rembrandt 和 Pollock), 还可以确定绘图是否是由这些著名的艺术家之一来工作的。</span><span class="sxs-lookup"><span data-stu-id="2204e-137">With the tagged images uploaded, the next step is to train the model with these images so it can distinguish between paintings by Picasso, Rembrandt, and Pollock, as well as determine whether a painting is a work by one of these famous artists.</span></span>