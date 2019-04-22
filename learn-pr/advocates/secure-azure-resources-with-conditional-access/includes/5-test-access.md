<span data-ttu-id="05e9a-101">在前面的练习中, 我们创建了一个目录, 创建了一个用户和组, 然后在访问 azure 门户时创建了需要 Azure 多重身份验证的条件访问规则。</span><span class="sxs-lookup"><span data-stu-id="05e9a-101">In the previous exercises, we created a directory, created a user and group, and then created a conditional access rule that requires Azure Multi-Factor Authentication when accessing the Azure portal.</span></span> <span data-ttu-id="05e9a-102">现在, 我们将测试是否可以访问我们的资源。</span><span class="sxs-lookup"><span data-stu-id="05e9a-102">Now, we'll test if we can access our resources.</span></span>

## <a name="test-access-to-resources"></a><span data-ttu-id="05e9a-103">测试对资源的访问</span><span class="sxs-lookup"><span data-stu-id="05e9a-103">Test access to resources</span></span>

<span data-ttu-id="05e9a-104">您知道您的用户将使用 MyApps 门户登录并访问其所有 SaaS 应用程序, 因此, 我们将对此进行测试。</span><span class="sxs-lookup"><span data-stu-id="05e9a-104">You know that your users will sign in and access all their SaaS applications using the MyApps portal, so this is what we'll test.</span></span>

1. <span data-ttu-id="05e9a-105">打开 InPrivate 浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="05e9a-105">Open an InPrivate browser window.</span></span>

1. <span data-ttu-id="05e9a-106">浏览到https://myapps.microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="05e9a-106">Browse to https://myapps.microsoft.com.</span></span>

1. <span data-ttu-id="05e9a-107">以在单元3中创建的用户登录。</span><span class="sxs-lookup"><span data-stu-id="05e9a-107">Sign in as the user that we created in Unit 3.</span></span>

   * <span data-ttu-id="05e9a-108">请注意, 您登录到门户时不需要多重身份验证。</span><span class="sxs-lookup"><span data-stu-id="05e9a-108">Notice that you're signed in to the portal without requiring Multi-Factor Authentication.</span></span>

1. <span data-ttu-id="05e9a-109">在同一个浏览器窗口中, https://portal.azure.com浏览到。</span><span class="sxs-lookup"><span data-stu-id="05e9a-109">In the same browser window, browse to https://portal.azure.com.</span></span>

   * <span data-ttu-id="05e9a-110">请注意, 现在需要提供详细信息来保证帐户安全。</span><span class="sxs-lookup"><span data-stu-id="05e9a-110">Notice that you're now required to provide more information to keep your account secure.</span></span> <span data-ttu-id="05e9a-111">此中断是由于我们创建了条件访问策略而导致的 Azure 多重身份验证启动。</span><span class="sxs-lookup"><span data-stu-id="05e9a-111">This interrupt is Azure Multi-Factor Authentication kicking in because of the conditional access policy we created.</span></span> <span data-ttu-id="05e9a-112">您可以在此时停止, 并关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="05e9a-112">You can stop at this point and close the browser window.</span></span>