新式应用程序中存在的大量代码是由您选择的库和依赖项: 开发人员。 这是一种节省时间和资金的常见做法。 但是, 缺点是你现在负责此代码, 即使其他人在你的项目中使用它也是如此。 如果研究工具 (或更糟的情况) 发现其中一种第三方库中的漏洞, 则在应用中可能也会存在相同的缺陷。

使用具有已知漏洞的组件是我们行业中的一大问题。 这样做有一个问题, 那就是 OWASP 的最重要的 web 应用程序漏洞的[前十个列表](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), 在 #9 几年中保持不变。

## <a name="track-known-security-vulnerabilities"></a>跟踪已知安全漏洞

我们在发现问题时了解的问题。 保留我们的库和依赖项 (在我们的列表中 #4, 我们将为我们提供帮助, 但最好跟踪可能影响应用程序的已标识漏洞。

> [!IMPORTANT]
> 当系统具有已知的漏洞时, 可能会有更多的漏洞可供用户用来攻击这些系统的代码。 如果已公开利用漏洞, 则对任何受影响的系统进行即时更新至关重要。

**Mitre**是一个维护[常见漏洞和泄密列表](https://cve.mitre.org)的非盈利组织。 此列表是应用、库和框架中可公开搜索的已知 cybersecurity 漏洞集。 **如果在 CVE 数据库中找到库或组件, 则它存在已知漏洞**。

当产品或组件中发现安全漏洞时, 安全社区会提交问题。 将为每个发布的问题分配一个 ID, 并包含发现的日期、该漏洞的说明, 以及有关该问题的已发布变通办法或供应商声明的参考。

### <a name="how-to-verify-if-you-have-known-vulnerabilities-in-your-3rd-party-components"></a>如何验证你的第三方组件中是否存在已知漏洞

你可以将每日任务放入手机, 以查看此列表, 但为我们带来的幸运是, 许多工具都存在, 让我们能够验证我们的依赖是否易受攻击。 您可以对基本代码运行这些工具, 或者更好地将其添加到 CI/CD 管道, 以在开发过程中自动检查问题。

- 具有[Jenkins 插件](https://wiki.jenkins.io/display/JENKINS/OWASP+Dependency-Check+Plugin)的[OWASP 依赖项检查](https://www.owasp.org/index.php/OWASP_Dependency_Check)
- [OWASP SonarQube](https://www.owasp.org/index.php/OWASP_SonarQube_Project)
- [Snyk](https://snyk.io), 对于 GitHub 中的开放源存储库是免费的
- 许多企业使用的[黑色](https://www.blackducksoftware.com)的方式
- 仅为 Ruby [RubySec](https://rubysec.com)咨询数据库
- [撤出](https://github.com/retirejs/retire.js/)用于验证 JavaScript 库是否已过期的工具。可用作各种工具 (包括[Burp 套件](https://www.portswigger.net)) 的插件

某些专门用于静态代码分析的工具也可用于执行此分析。

- [Roslyn 安全防护](https://dotnet-security-guard.github.io)
- [Puma 扫描](https://pumascan.com)
- [PT 应用程序检查器](https://www.ptsecurity.com/ww-en/products/ai/)
- [Apache Maven 依赖插件](https://maven.apache.org/plugins/maven-dependency-plugin/)
- [源清除](https://www.sourceclear.com)
- [Sonatype](https://ossindex.sonatype.org)
- [节点安全平台](https://nodesecurity.io)
- [WhiteSource](https://www.whitesourcesoftware.com/what-is-whitesource/)
- [Hdiv](https://hdivsecurity.com)
- [还有更多 .。。](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)

有关使用易受攻击的组件所涉及的风险的详细信息, 请访问专用于本主题的[OWASP 页面](https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities)。

## <a name="summary"></a>摘要

当您将库或其他第三方组件用作应用程序的一部分时, 也会考虑它们可能具有的任何风险。 降低此风险的最佳方式是确保仅使用没有已知漏洞的组件。
