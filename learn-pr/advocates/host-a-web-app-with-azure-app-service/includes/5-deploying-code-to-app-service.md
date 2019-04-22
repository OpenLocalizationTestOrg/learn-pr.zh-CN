现在, 我们来看看如何将应用程序部署到应用服务。

## <a name="what-is-automated-deployment"></a>什么是自动部署？

自动部署或持续集成是一种以快速重复模式推送新功能和 bug 修复的过程, 对最终用户影响最小。

Azure 支持直接从多个源进行自动部署。 可以使用以下选项:

- **Visual Studio Team Services (VSTS)**: 可以将您的代码推送到 VSTS、在云中生成代码、运行测试、从代码中生成版本, 最后将代码推送到 Azure Web 应用。

- **GitHub**: Azure 支持直接从 GitHub 进行自动部署。 将 GitHub 存储库连接到 Azure 以实现自动部署时, 将自动为您部署在 GitHub 上推送到生产分支的任何更改。

- **Bitbucket**: 在其与 GitHub 的相似之处, 您可以使用 Bitbucket 配置自动部署。

- **OneDrive**: 您可以使用应用服务连接 onedrive 帐户, 以便在您更改 OneDrive 帐户上的任何文件时, Azure 将自动检测它并在 web 应用程序文件中提取任何更改。 对于静态网站, 这是一个很好的选择。 这将使你感觉你正在处理的本地文件系统在 Azure 上平稳且即时地反映所有更改。

- **收存箱**: 类似于 OneDrive, 您可以将 web 应用程序文件托管在 Dropbox 帐户中, 并让它们自动推送并通过 web 应用进行部署。

- **外部存储库**: 可以使用任何外部 Git 存储库配置自动部署。

### <a name="non-automated-deployment-to-azure"></a>到 Azure 的非自动部署

您可以使用几个选项手动将您的代码推送到 Azure:

- **ftp/S**: ftp 或 FTPS 是将代码推送到任何宿主环境的传统方法。 尽管不建议再这样做, 但仍可以使用它。

- **Web Deploy/IDE**: 您可以使用 Visual Studio IDE 将 Web 应用发布到 Azure。 Visual Studio 发布机制可以利用 Web Deploy 技术将您的代码推送到 Azure。

- **Git**: Azure 为你的应用程序维护**本地 Git 存储库**。 您可以将您的代码直接**提交**给它。

## <a name="summary"></a>摘要

Azure 提供了多种方法来上传代码, 以帮助它更好地满足当前工作流的需要。