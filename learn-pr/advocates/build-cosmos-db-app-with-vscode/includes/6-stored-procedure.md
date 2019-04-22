数据库中的多个文档经常需要同时更新。 此单元讨论如何从您的 .net 控制台应用程序创建、注册和运行存储过程。

## <a name="create-a-stored-procedure-in-your-app"></a>在应用程序中创建存储过程

在此存储过程中, 订单**id**(包含订单中所有项目的列表) 用于计算订单总计。 订单总计是按照订单中项目的总和、客户拥有的任何红利 (片尾) 更少的, 并将任何优惠券代码考虑出来。

1. 在 Visual Studio Code 中, 在 " **Azure: Cosmos DB** " 选项卡中, 展开 azure Cosmos DB account > **Users** > **WebCustomers** , 然后右键单击 "**存储过程**", 然后单击 "**创建存储过程**"。

1. 在屏幕顶部的文本框中, 键入`UpdateOrderTotal`并按 enter, 为存储过程指定一个名称。

1. 在 " **Azure: Cosmos DB** " 选项卡中, 展开 "**存储过程**", 然后单击 " **UpdateOrderTotal**"。

    默认情况下, 将提供检索第一项的存储过程。

1. 若要从应用程序运行此默认存储过程, 请将以下代码添加到**Program.cs**文件中。

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
        Console.WriteLine("Stored procedure complete");
    }
    ```

1. 现在复制以下代码, 并将其粘贴到`await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` **BasicOperations**方法中的行之前。

    ```csharp
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中, 运行以下命令以使用存储过程运行示例。

    ```bash
    dotnet run
    ```

控制台显示输出, 指示已完成存储过程。
