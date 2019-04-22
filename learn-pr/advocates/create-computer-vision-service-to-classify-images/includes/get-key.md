## <a name="get-an-access-key"></a>获取访问键

如果尚未执行此操作, 请在 Azure 云命令行管理程序中运行以下命令, 以将 API 访问密钥存储`key`在名为的变量中。 我们将在后续调用中使用此变量。

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
