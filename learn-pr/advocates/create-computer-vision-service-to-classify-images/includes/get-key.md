## <a name="get-an-access-key"></a><span data-ttu-id="5ccf1-101">获取访问键</span><span class="sxs-lookup"><span data-stu-id="5ccf1-101">Get an access key</span></span>

<span data-ttu-id="5ccf1-102">如果尚未执行此操作, 请在 Azure 云命令行管理程序中运行以下命令, 以将 API 访问密钥存储`key`在名为的变量中。</span><span class="sxs-lookup"><span data-stu-id="5ccf1-102">If you haven't done so already, run the following command in Azure Cloud Shell to store the API access key in a variable called `key`.</span></span> <span data-ttu-id="5ccf1-103">我们将在后续调用中使用此变量。</span><span class="sxs-lookup"><span data-stu-id="5ccf1-103">We'll use this variable in subsequent calls.</span></span>

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
