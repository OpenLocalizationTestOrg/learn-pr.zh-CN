在此单元中, 您将向 Artworks 项目添加 Picasso、Pollock 和 Rembrandt 的著名 paintings 的图像。 你将标记图像, 以便自定义视觉服务可以学习将一个艺术家与另一个艺术家区分开来。

1. 在我们创建的**Artworks**项目中, 选择侧面板中**+****标记**右侧的加号 ()。

     ![突出显示了加号的 Artworks 项目左侧面板的屏幕截图。](../media/2-add-tags.png)

1. 将显示一个名为 **"名称" 的**对话框。 在 "标记名称" 字段中键入*painting* , 然后选择 "**保存**"。 此操作将在标记列表中创建标记*绘画*。 让我们再添加一些。 

1. 重复步骤1和步骤 2, 添加值为*Picasso*、 *Pollock*和*Rembrandt*的标记。 完成后, 标记列表看起来就像以下形式。

    ![列出在上述步骤中创建的所有标记的 "标记" 部分的屏幕截图](../media/2-tag-list.png)

    正如您所看到的, 项目中使用每个标记标记的图像数量为零。 让我们将一些图像添加到项目并为其分配标签。

1. 下载包含此模块的图像资源的[cvs-resources](https://github.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/raw/master/cvs-resources.zip) , 并将其解压缩到本地计算机。 

1. 返回门户中, 选择 "**添加图像**" 以将图像添加到项目中。

    ![突出显示 "添加图像" 按钮的 Artworks 项目的屏幕截图](../media/2-portal-click-add-images.png)

1. 在您在步骤4中本地下载的 " **cvs 资源**" 文件夹中, 导航到 "Artists\Picasso" 文件夹。

1. 选择 "Artists\Picasso" 中的所有文件, 然后选择 "**打开**"。

    ![选定了所有图像文件且突出显示 "打开" 按钮的 Picasso 文件夹的屏幕截图 ](../media/2-fe-browse-picasso-01.png)

1. 此时将显示 "**图像上载**" 对话框, 并显示正在上载的所有图像的缩略图。 选择 "**我的标记**" 字段, 这将打开一个标记下拉列表, 您可以分配这些图像。

    ![显示 Picasso 图像缩略图和 "我的标记" 下拉列表中所有标记的 "图像上载" 对话框的屏幕截图](../media/2-upload-picasso-tags.png)

1. 选择 "标签" "*画图*" 和 " *Picasso* ", 然后选择 "**上传7个文件**" 完成上载。 

1. 确认您上载的图像现在位于 Artworks 项目中, 并且已更新标签列表, 以表明我们已通过*Picasso*和*涂色*标记了七个图像。

    ![显示上载的图像的 Artworks 项目的屏幕截图。 在左侧面板中的 "标记" 下选择 "Picasso" 和 "涂色" 标记。](../media/2-portal-tagged-01.png)

1. 使用七个 Picasso 图像, 自定义的远景服务可执行一份相当于通过 Picasso 识别 paintings 的作业。 但如果现在已对模型进行了培训, 它只会了解 Picasso 的外观, 并且无法识别其他艺术家的 paintings。 下一步是通过另一个艺术家上传一些 paintings。 

1. 选择 "**添加图像**", 并在模块资源中选择 "Artists\Rembrandt" 文件夹中的所有图像。 使用标签 "painting" 和 "Rembrandt" (不是 "Picasso") 标记它们, 然后选择 "**上传6个文件**" 以将它们上载到项目中。

    ![显示 Rembrandt 图像缩略图以及选定的绘画和 Rembrandt 标记的 "图像上载" 对话框的屏幕截图](../media/2-upload-rembrandt.png)

1. 确认 Rembrandt 图像显示在项目中的 Picasso 图像旁边, 并且标记列表中显示 "Rembrandt"。

    ![显示上载的图像的 Artworks 项目的屏幕截图。在左侧面板中的 "标记" 下选择 "Picasso"、"Rembrandt" 和 "涂色" 标记。](../media/2-portal-tagged-02.png)

1. 现在, 通过 enigmatic 艺术家杰克逊 Pollock 添加 paintings, 以使自定义视觉服务也能识别 Pollock paintings。 在模块资源中选择 "Artists\Pollock" 文件夹中的所有图像, 使用术语 "painting" 和 "Pollock" 对其进行标记, 并将它们上载到项目中。

在上传带标签的图像后, 下一步是使用这些图像来培训模型, 以便它可以区分 paintings (通过 Picasso、Rembrandt 和 Pollock), 还可以确定绘图是否是由这些著名的艺术家之一来工作的。