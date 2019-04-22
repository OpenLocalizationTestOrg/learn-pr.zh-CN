你已创建所有必需的 Azure 函数, 并已将其部署! 让我们将 Azure 函数与可宽延时间连接, 并创建一个可宽延的斜杠命令以调用 Azure 函数, 并在可宽延时间窗口中显示生成的 mojified 图像。 

## <a name="create-a-slack-app"></a>创建可宽延时间应用

斜杠命令作为可宽延时间应用 (也称为 "可宽延时间" bot) 的一部分存在。 

1. [创建可宽延时间应用](https://api.slack.com/apps/new?azure-portal=true)。
2. 选择一个**应用程序名称**, 并将其与您在此模块开始时创建的**工作区**相关联, 然后选择 "**创建应用程序**"。

    ![创建可宽延时间应用。](../media/8.create-slack-app.png)

3. 转到 "可宽延时间" 应用, 并创建一个斜杠命令。 在`slash Commands`菜单项上选择。

    ![创建可宽延时间应用程序屏幕。 对话框要求提供应用名称和开发可宽延时间工作区。](../media/8.slash-commands.png)

4. 选择 "**新建命令**"。

    - 在 "**命令**" 字段中为您的斜杠命令提供所需的任何名称。
    - 在 "**请求 URL** " 字段中输入 Azure function app 公共 URL。 对于在`mojifier-slack-function-app`上一个单元中使用的, 我们的函数应用程序公共`https://mojifier-slack-function-app.azurewebsites.net`URL 为。 追加`/api/RespondToSlackCommand`到 URL。
    - 添加**简短说明**和**用法提示**。

    选择 "**保存**"。

    ![斜杠命令](../media/8.create-slash-command.png)

5. 如果成功, 您应该会看到斜线命令显示在**斜线命令**列表中。

    ![斜杠命令显示在所有斜杠命令的列表中。 此列表中仅显示了 mojifier。](../media/8.create-slash-commands-success.png)

6. 若要实现此操作, 需要在工作区中安装可宽延时间应用。 在菜单中选择 "**基本信息**"。

7. 展开 "**将应用安装到工作区**", 然后选择 "**将应用程序安装到工作区**"。

   ![将应用程序安装到工作区在可宽延 API 页中的 "可宽延时间的应用程序" 菜单下列出。](../media/8.install-app-to-workspace.png)

8. 如果需要, 请**授权**你的应用。

   ![将应用程序身份验证到工作区间隙屏幕将显示 "授权" 或 "取消" 选项。](../media/8.authenticate-slack-app.png)

## <a name="try-it-out"></a>试用

你已经创建了斜杠命令并将其连接到部署的 Azure 函数。 现在, 您可以对其进行测试。

1. 打开 "可宽延时间" 工作区。
2. 打开聊天窗口并键入`/mojify`。 如果你已将应用程序命名为其他内容, 请改为输入该命令。
3. 如果一切正常, 您应看到`mojify`一个选项。

   ![在文本上方弹出斜杠命令菜单。 它将应用程序名称显示为 Mojifier, 并将命令显示为 "/mojify images of 人脸", 并显示说明 "将联系人的面孔替换为表情符号" 的说明。](../media/8.slack-check-mojify.png)

4. 输入`/mojify`并添加图像 URL。

   ![可宽延时间命令正在运行并 mojified 提供的图像 URL。 在图像中的人脸直接显示一个表情符号。](../media/8.slack-type-mojify.png)
