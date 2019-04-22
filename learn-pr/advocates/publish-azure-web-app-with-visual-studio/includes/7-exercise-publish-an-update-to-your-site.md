你的 Alpine 滑雪房子 web 应用已准备好并在运行, 但现在你需要将其显示给老板。 您需要更新网站并将这些更新发布到 Azure。

## <a name="update-your-web-app"></a>更新 web 应用程序

### <a name="replace-the-boilerplate-code"></a>替换样本代码

1. 在 "**页面**" 文件夹中, 打开 "**关于. cshtml** " 文件。

1. 在代码的底部, 找到`<p> Use this area to provide additional information. </p>`。

1. 将此样本文字替换`<p>Welcome to the Alpine Ski House!</p>`为。

1. 保存该文件。

1. 打开**About.cshtml.cs**文件。

1. 将`Message`字符串替换为说**Alpine 滑雪房子是东北的首要滑雪峰。**

1. 保存该文件。

### <a name="publish-your-updates"></a>发布更新

1. 在 "解决方案资源管理器" 中, 右键单击项目。

1. 选择 "**发布**"。 应具有包含 [网站]-web deploy 的选项。

1. 选择您的网站, Visual Studio 会将您所做的更改发送到 Azure。

### <a name="view-your-changes"></a>查看所做的更改

发布所做的更改后, Visual Studio 将在浏览器中打开该网站。 导航到 "**关于**" 页, 并查看您所做的更改已反映出来。

## <a name="congrats"></a>Congrats!

您已成功使用 Visual Studio 2017 更新 web 应用程序。
