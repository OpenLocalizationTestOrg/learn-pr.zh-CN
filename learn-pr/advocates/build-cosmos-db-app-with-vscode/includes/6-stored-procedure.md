<span data-ttu-id="c5578-101">数据库中的多个文档经常需要同时更新。</span><span class="sxs-lookup"><span data-stu-id="c5578-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="c5578-102">此单元讨论如何从您的 .net 控制台应用程序创建、注册和运行存储过程。</span><span class="sxs-lookup"><span data-stu-id="c5578-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="c5578-103">在应用程序中创建存储过程</span><span class="sxs-lookup"><span data-stu-id="c5578-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="c5578-104">在此存储过程中, 订单**id**(包含订单中所有项目的列表) 用于计算订单总计。</span><span class="sxs-lookup"><span data-stu-id="c5578-104">In this stored procedure, the **OrderId**, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="c5578-105">订单总计是按照订单中项目的总和、客户拥有的任何红利 (片尾) 更少的, 并将任何优惠券代码考虑出来。</span><span class="sxs-lookup"><span data-stu-id="c5578-105">The order total is calculated from the sum of the items in the order, less any dividends (credits) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="c5578-106">在 Visual Studio Code 中, 在 " **Azure: Cosmos DB** " 选项卡中, 展开 azure Cosmos DB account > **Users** > **WebCustomers** , 然后右键单击 "**存储过程**", 然后单击 "**创建存储过程**"。</span><span class="sxs-lookup"><span data-stu-id="c5578-106">In Visual Studio Code, in the **Azure: Cosmos DB** tab, expand your Azure Cosmos DB account > **Users** > **WebCustomers** and then right-click **Stored Procedures** and then click **Create Stored Procedure**.</span></span>

1. <span data-ttu-id="c5578-107">在屏幕顶部的文本框中, 键入`UpdateOrderTotal`并按 enter, 为存储过程指定一个名称。</span><span class="sxs-lookup"><span data-stu-id="c5578-107">In the text box at the top of the screen, type `UpdateOrderTotal` and press Enter to give the stored procedure a name.</span></span>

1. <span data-ttu-id="c5578-108">在 " **Azure: Cosmos DB** " 选项卡中, 展开 "**存储过程**", 然后单击 " **UpdateOrderTotal**"。</span><span class="sxs-lookup"><span data-stu-id="c5578-108">In the **Azure: Cosmos DB** tab, expand **Stored Procedures** and click **UpdateOrderTotal**.</span></span>

    <span data-ttu-id="c5578-109">默认情况下, 将提供检索第一项的存储过程。</span><span class="sxs-lookup"><span data-stu-id="c5578-109">By default, a stored procedure that retrieves the first item is provided.</span></span>

1. <span data-ttu-id="c5578-110">若要从应用程序运行此默认存储过程, 请将以下代码添加到**Program.cs**文件中。</span><span class="sxs-lookup"><span data-stu-id="c5578-110">To run this default stored procedure from your application, add the following code to the **Program.cs** file.</span></span>

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
        Console.WriteLine("Stored procedure complete");
    }
    ```

1. <span data-ttu-id="c5578-111">现在复制以下代码, 并将其粘贴到`await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` **BasicOperations**方法中的行之前。</span><span class="sxs-lookup"><span data-stu-id="c5578-111">Now copy the following code and paste it before the `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` line in the **BasicOperations** method.</span></span>

    ```csharp
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="c5578-112">在集成终端中, 运行以下命令以使用存储过程运行示例。</span><span class="sxs-lookup"><span data-stu-id="c5578-112">In the integrated terminal, run the following command to run the sample with the stored procedure.</span></span>

    ```bash
    dotnet run
    ```

<span data-ttu-id="c5578-113">控制台显示输出, 指示已完成存储过程。</span><span class="sxs-lookup"><span data-stu-id="c5578-113">The console displays output indicating that the stored procedure was completed.</span></span>
