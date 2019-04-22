<span data-ttu-id="eb3f8-101">在本模块中, 您学习了如何使用 Azure Blob 存储来存储 web 应用程序数据。</span><span class="sxs-lookup"><span data-stu-id="eb3f8-101">In this module, you learned how to use Azure Blob storage to store web application data.</span></span> <span data-ttu-id="eb3f8-102">我们讨论了在 web 应用程序中创建使用 Blob 存储的策略的相关提示, 以及如何使用 Azure 存储 SDK for .net Core 对 blob 进行写入和读取。</span><span class="sxs-lookup"><span data-stu-id="eb3f8-102">We discussed tips for creating a strategy to use Blob storage in a web app and how to use the Azure Storage SDK for .NET Core to write to and read from blobs.</span></span> <span data-ttu-id="eb3f8-103">我们创建的应用程序接受来自用户的上载文件, 并将其存储在 Blob 存储中, 并使其可供下载。</span><span class="sxs-lookup"><span data-stu-id="eb3f8-103">The app we made accepts uploaded files from users, stores them in Blob storage, and makes them available for download.</span></span>

[!include[](../../../includes/azure-sandbox-cleanup.md)]

<span data-ttu-id="eb3f8-104">若要清理云命令行管理程序存储, `mslearn-store-data-in-azure`请删除该目录。</span><span class="sxs-lookup"><span data-stu-id="eb3f8-104">To clean up your Cloud Shell storage, delete the `mslearn-store-data-in-azure` directory.</span></span>

<!---TODO: Remove further reading
## Further reading

- **Securely storing secrets like connection strings**: The most robust end-to-end solution for storing secret configuration values is Azure Key Vault. See [here](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) for information about using Key Vault in an ASP.NET Core application. Alternatively, you can safely store connection strings in App Service application settings and use the [ASP.NET Core Secret Manager tool](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) to support developer environments.
- [Uploading large files with streaming in ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
- [Blob concurrency: AccessConditions and blob leases](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
- [Granting limited access to Azure Storage object with shared access signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Indexing Blob storage with Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
- [Container and blob name restrictions](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)
--->