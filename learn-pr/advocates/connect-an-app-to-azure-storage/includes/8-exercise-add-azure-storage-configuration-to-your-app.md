::: zone pivot="csharp"
<span data-ttu-id="9e0e6-101">让我们将 .net core 应用程序的支持添加到配置文件中, 以检索连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-101">Let's add support to our .NET core application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="9e0e6-102">我们将首先添加必要的管道来管理 JSON 文件中的配置。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-102">We'll start by adding the necessary plumbing to manage configuration in a JSON file.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="9e0e6-103">创建 JSON 配置文件</span><span class="sxs-lookup"><span data-stu-id="9e0e6-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="9e0e6-104">`cd`如果尚不存在, 则为 PhotoSharingApp 目录。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-104">`cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="9e0e6-105">使用命令`touch`行中的工具创建一个名为**appsettings**的文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-105">Use the `touch` tool on the command line to create a file named **appsettings.json**.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="9e0e6-106">在编辑器中打开项目。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-106">Open the project in an editor.</span></span> <span data-ttu-id="9e0e6-107">如果您在本地工作, 请使用您的 "选择" 编辑器。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-107">If you are working locally, use your editor of choice.</span></span> <span data-ttu-id="9e0e6-108">建议使用**Visual Studio Code**, 这是一个可扩展的跨平台 IDE。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-108">We recommend **Visual Studio Code**, which is an extensible cross-platform IDE.</span></span> <span data-ttu-id="9e0e6-109">如果使用的是云命令行管理程序, 我们建议使用云命令行管理程序编辑器。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-109">If you are working in the Cloud Shell, we recommend the Cloud Shell editor.</span></span> <span data-ttu-id="9e0e6-110">以下命令适用于这两种情况。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-110">The following command works for both.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="9e0e6-111">在编辑器中选择 " **appsettings** " 文件, 并添加以下文本。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-111">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="9e0e6-112">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-112">Save the file.</span></span> <span data-ttu-id="9e0e6-113">在云命令行管理程序编辑器中, 在右上角有一个菜单, 其中包含常见的文件操作。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-113">In the Cloud Shell editor, there is a menu in the top right corner that has common file operations.</span></span>

    ```json
    {
      "StorageAccountConnectionString": "<value>"
    }
    ```

1. <span data-ttu-id="9e0e6-114">现在, 我们需要获取存储帐户连接字符串, 并将其放入应用程序的配置中。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-114">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span> <span data-ttu-id="9e0e6-115">在云命令行管理程序中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-115">In Cloud Shell run the following command.</span></span>

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. <span data-ttu-id="9e0e6-116">复制从该命令返回的连接字符串, 并将**appsettings**文件`"<value>"`中的替换为此连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-116">Copy the connection string that is returned from that command, and replace `"<value>"` in the **appsettings.json** file with this connection string.</span></span> <span data-ttu-id="9e0e6-117">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-117">Save the file.</span></span>

1. <span data-ttu-id="9e0e6-118">接下来, 在编辑器中打开项目文件 (**PhotoSharingApp**)。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-118">Next, open the project file (**PhotoSharingApp.csproj**) in the editor.</span></span>

1. <span data-ttu-id="9e0e6-119">添加以下配置块以将新文件包含在项目中, 并将其复制到输出文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-119">Add the following configuration block to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="9e0e6-120">这样可确保在编译/生成应用程序时, 将应用程序配置文件放在输出目录中。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-120">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. <span data-ttu-id="9e0e6-121">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-121">Save the file.</span></span> <span data-ttu-id="9e0e6-122">(请务必执行此操作, 否则在下面添加包时, 会丢失所做的更改!)</span><span class="sxs-lookup"><span data-stu-id="9e0e6-122">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="9e0e6-123">添加对读取 JSON 配置文件的支持</span><span class="sxs-lookup"><span data-stu-id="9e0e6-123">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="9e0e6-124">.net Core 应用程序需要其他 NuGet 包才能读取 JSON 配置文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-124">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="9e0e6-125">在窗口的命令提示符部分, 添加对**Microsoft extension. Json** NuGet 包的引用。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-125">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="9e0e6-126">添加代码以读取配置文件</span><span class="sxs-lookup"><span data-stu-id="9e0e6-126">Add code to read the configuration file</span></span>

<span data-ttu-id="9e0e6-127">至此, 我们已经添加了启用读取配置所需的库, 我们需要在控制台应用程序中启用该功能。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-127">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="9e0e6-128">在编辑器中选择 " **Program.cs** "。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-128">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="9e0e6-129">文件顶部有一个**使用系统;** 行。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-129">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="9e0e6-130">在该行下方, 添加以下代码行:</span><span class="sxs-lookup"><span data-stu-id="9e0e6-130">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="9e0e6-131">将**Main**方法的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-131">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="9e0e6-132">此代码会将配置系统初始化为从**appsettings**文件中读取。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-132">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

<span data-ttu-id="9e0e6-133">您的**Program.cs**文件现在应如下所示:</span><span class="sxs-lookup"><span data-stu-id="9e0e6-133">Your **Program.cs** file should now look like the following:</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace PhotoSharingApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
        }
    }
}
```

::: zone-end

::: zone pivot="javascript"

<span data-ttu-id="9e0e6-134">让我们将 node.js 应用程序的支持添加到配置文件中, 以检索连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-134">Let's add support to our Node.js application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="9e0e6-135">我们将首先添加必要的管道来管理 JavaScript 文件中的配置。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-135">We'll start by adding the necessary plumbing to manage configuration from our JavaScript file.</span></span>

## <a name="create-a-env-configuration-file"></a><span data-ttu-id="9e0e6-136">创建一个 env 配置文件</span><span class="sxs-lookup"><span data-stu-id="9e0e6-136">Create a .env configuration file</span></span>

1. <span data-ttu-id="9e0e6-137">确保您在项目的正确工作目录中。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-137">Make sure you are in the correct working directory for your project.</span></span>

1. <span data-ttu-id="9e0e6-138">使用命令`touch`行中的工具创建名为 **. env**的文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-138">Use the `touch` tool on the command line to create a file named **.env**.</span></span>

    ```bash
    touch .env
    ```

1. <span data-ttu-id="9e0e6-139">在云命令行管理程序编辑器中打开项目。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-139">Open the project in the Cloud Shell editor.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="9e0e6-140">选择编辑器中的 " **env** " 文件, 并添加以下文本。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-140">Select the **.env** file in the editor and add the following text.</span></span> 

    > [!TIP]
    > <span data-ttu-id="9e0e6-141">您可能需要单击代码中的 "刷新" 按钮才能查看新文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-141">You may need to click the refresh button in code to see the new files.</span></span>
    
    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > <span data-ttu-id="9e0e6-142">**AZURE_STORAGE_CONNECTION_STRING**值是一个硬编码的环境变量, 用于存储 api 以查找访问密钥。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-142">The **AZURE_STORAGE_CONNECTION_STRING** value is a hard-coded environment variable used for Storage APIs to look up access keys.</span></span> <span data-ttu-id="9e0e6-143">如果愿意, 您可以使用自己的名称, 但必须在您的`BlobService` node.js 应用程序中创建对象时提供该名称。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-143">You can use your own name if you prefer, but you must supply the name when you create the `BlobService` object in your Node.js app.</span></span>

1. <span data-ttu-id="9e0e6-144">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-144">Save the file.</span></span>

1. <span data-ttu-id="9e0e6-145">现在, 我们需要获取存储帐户连接字符串, 并将其放入应用程序的配置中。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-145">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span> <span data-ttu-id="9e0e6-146">在云命令行管理程序中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-146">In Cloud Shell run the following command.</span></span>

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --query connectionString \
        --name <name>
    ```

1. <span data-ttu-id="9e0e6-147">复制从该命令返回的连接字符串, 减去引号, 并在**env**文件中`<value>`使用此连接字符串进行替换。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-147">Copy the connection string that is returned from that command, minus the quotes, and replace `<value>` in the **.env** file with this connection string.</span></span>

1. <span data-ttu-id="9e0e6-148">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-148">Save the file.</span></span>

## <a name="add-support-to-read-an-environment-configuration-file"></a><span data-ttu-id="9e0e6-149">添加对读取环境配置文件的支持</span><span class="sxs-lookup"><span data-stu-id="9e0e6-149">Add support to read an environment configuration file</span></span>

<span data-ttu-id="9e0e6-150">node.js 应用可以包括支持通过添加**dotenv**包从**env**文件中读取。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-150">Node.js apps can include support to read from the **.env** file by adding the **dotenv** package.</span></span>

1. <span data-ttu-id="9e0e6-151">在窗口的命令提示符部分, 使用`npm`将依赖项添加到**dotenv**包。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-151">In the command prompt section of the window, add a dependency to the  **dotenv** package using `npm`.</span></span>

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="9e0e6-152">添加代码以读取配置文件</span><span class="sxs-lookup"><span data-stu-id="9e0e6-152">Add code to read the configuration file</span></span>

<span data-ttu-id="9e0e6-153">至此, 我们已经添加了启用读取配置所需的库, 我们需要在应用程序中启用此功能。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-153">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our application.</span></span>

1. <span data-ttu-id="9e0e6-154">在编辑器中选择 " **.js** "。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-154">Select **index.js** in the editor.</span></span>

1. <span data-ttu-id="9e0e6-155">在文件的顶部, 存在`#!/usr/bin/env node`一行。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-155">At the top of the file, a `#!/usr/bin/env node` line is present.</span></span> <span data-ttu-id="9e0e6-156">在该行下方, 添加一个`require`用于加载**dotenv**包的语句。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-156">Underneath that line, add a `require` statement to load the **dotenv** package.</span></span> <span data-ttu-id="9e0e6-157">这将使在您的**env**文件中定义的环境变量可用于该程序。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-157">This will make environment variables defined in our **.env** file available to the program.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    // ... more code follows
    ```
::: zone-end

<span data-ttu-id="9e0e6-158">现在, 我们已将所有的连接好, 我们可以开始添加代码以使用我们的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="9e0e6-158">Now that we have that all wired up, we can start adding code to use our storage account.</span></span>
