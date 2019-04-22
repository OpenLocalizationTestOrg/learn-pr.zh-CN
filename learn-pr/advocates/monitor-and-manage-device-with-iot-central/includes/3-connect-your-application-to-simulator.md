[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="37c63-101">在实践中, 你将 Azure IoT Central 连接到物理设备 (即 IoT 已启用的咖啡计算机)。</span><span class="sxs-lookup"><span data-stu-id="37c63-101">In practice, you will connect Azure IoT Central to a physical device, i.e. an IoT enabled coffee machine.</span></span> <span data-ttu-id="37c63-102">在这里, 你将使用 node.js 应用程序 simualate 设备, 并将其连接到 Azure IoT 中央应用程序。</span><span class="sxs-lookup"><span data-stu-id="37c63-102">Here, you'll simualate a device with a Node.js application and connect it to the Azure IoT Central application.</span></span> <span data-ttu-id="37c63-103">模拟的咖啡店中的遥测度量将发送到 IoT Central, 以进行监控和分析。</span><span class="sxs-lookup"><span data-stu-id="37c63-103">Telemetry measurements from the simulated coffee machine are sent to IoT Central for monitoring and analysis.</span></span>

![显示咖啡机的插图。](../media/3-coffee-machine.png) 

## <a name="add-the-coffee-machine-in-iot-central"></a><span data-ttu-id="37c63-105">在 IoT 中心中添加咖啡机</span><span class="sxs-lookup"><span data-stu-id="37c63-105">Add the coffee machine in IoT Central</span></span> 
<span data-ttu-id="37c63-106">若要将咖啡机添加到应用程序中, 请使用在上一个设备中创建的**已连接的 "咖啡 Maker** " 设备模板。</span><span class="sxs-lookup"><span data-stu-id="37c63-106">To add your coffee machine to your application, you use the **Connected Coffee Maker** device template you created in the previous unit.</span></span>

1. <span data-ttu-id="37c63-107">若要添加新设备, 请在左侧导航菜单中选择 "**设备资源管理器**"。</span><span class="sxs-lookup"><span data-stu-id="37c63-107">To add a new device, choose **Device Explorer** in the left navigation menu.</span></span>

    <span data-ttu-id="37c63-108">若要开始连接咖啡机, 请依次选择 " **+ 新建**"、"**真实**" 和 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="37c63-108">To start connecting your coffee machine, choose **+ New**, **Real**, and then **Create**.</span></span> <span data-ttu-id="37c63-109">完成后, 您将看到使用相同的连接咖啡模板创建的设备列表。</span><span class="sxs-lookup"><span data-stu-id="37c63-109">When you're finished, you see a list of devices you've created using the same Connected Coffee Maker template.</span></span>
   
    *   <span data-ttu-id="37c63-110">当您选择 " **+ 新建**", 然后单击 "**真实**" 时, 已连接的咖啡 Maker 将添加到列表中。</span><span class="sxs-lookup"><span data-stu-id="37c63-110">The Connected Coffee Maker is added to the list when you choose **+ New** and then **Real**.</span></span> 
    *   <span data-ttu-id="37c63-111">已连接的咖啡 Maker (模拟) 由 IoT Central 自动创建, 用于测试目的。</span><span class="sxs-lookup"><span data-stu-id="37c63-111">The Connected Coffee Maker (Simulate) is automatically created by IoT Central for testing purposes.</span></span> 

1.  <span data-ttu-id="37c63-112">(可选) 您可以通过在其名称中追加 "Real" 一词来区分新添加的咖啡机。</span><span class="sxs-lookup"><span data-stu-id="37c63-112">Optionally, you can differentiate the newly added coffee machine by appending the word “Real” in its name.</span></span> <span data-ttu-id="37c63-113">若要重命名新设备, 请选择设备并在 "名称" 字段中编辑名称。</span><span class="sxs-lookup"><span data-stu-id="37c63-113">To rename your new device, choose the device and edit the name in the name field.</span></span> 

    ![带有 "连接此设备" 选项的 "连接的咖啡 maker 设备模板" 屏幕截图突出显示。](../media/3-connect-device-a.png) 

    <span data-ttu-id="37c63-115">请注意下一节中的 "**连接此设备**以用于连接咖啡机" 的位置。</span><span class="sxs-lookup"><span data-stu-id="37c63-115">Note the location of **Connect this device** for connecting your coffee machine in the next section.</span></span> <span data-ttu-id="37c63-116">现在, 屏幕会显示 "缺少数据", 因为您尚未连接到咖啡机。</span><span class="sxs-lookup"><span data-stu-id="37c63-116">For now, the screen displays "Missing Data" because you haven't connected to the coffee machine.</span></span> <span data-ttu-id="37c63-117">建立连接后, 实际遥测开始填充屏幕。</span><span class="sxs-lookup"><span data-stu-id="37c63-117">The real telemetry begins to populate the screen once the connection is made.</span></span> 
 
## <a name="generate-connection-string-for-the-coffee-machine-from-your-application"></a><span data-ttu-id="37c63-118">从应用程序生成咖啡机的连接字符串</span><span class="sxs-lookup"><span data-stu-id="37c63-118">Generate connection string for the coffee machine from your application</span></span>
<span data-ttu-id="37c63-119">您可以在设备上运行的代码中嵌入真实咖啡机的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="37c63-119">You embed the connection string for your real coffee machine in the code that runs on the device.</span></span> <span data-ttu-id="37c63-120">通过连接字符串, 咖啡计算机可以安全地连接到 Azure IoT 中心应用程序。</span><span class="sxs-lookup"><span data-stu-id="37c63-120">The connection string enables the coffee machine to connect securely to your Azure IoT Central application.</span></span> <span data-ttu-id="37c63-121">每个设备实例都有一个唯一的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="37c63-121">Every device instance has a unique connection string.</span></span> <span data-ttu-id="37c63-122">在接下来的步骤中, 将生成连接字符串, 这是创建 node.js 应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="37c63-122">In the next steps, you generate the connection string as part of creating your node.js application.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="37c63-123">创建一个 node.js 应用程序</span><span class="sxs-lookup"><span data-stu-id="37c63-123">Create a Node.js application</span></span>
<span data-ttu-id="37c63-124">下面的步骤演示如何创建一个客户端应用程序来实现向应用程序中添加的咖啡机。</span><span class="sxs-lookup"><span data-stu-id="37c63-124">The following steps show you how to create a client application that implements the coffee machine you added to the application.</span></span>

> [!TIP]
> <span data-ttu-id="37c63-125">在本练习中, 我们将在 Azure 云命令行管理程序中创建应用程序, 以便无需在本地计算机上安装任何内容。</span><span class="sxs-lookup"><span data-stu-id="37c63-125">In this exercise, we'll create the app in the Azure Cloud Shell so that you don't have to install anything on your local machine.</span></span> 

1. <span data-ttu-id="37c63-126">在 Azure 云命令行管理程序中执行以下命令, `coffee-maker`以创建文件夹并导航到该文件夹:</span><span class="sxs-lookup"><span data-stu-id="37c63-126">Execute the following command in the Azure Cloud Shell to create a `coffee-maker` folder and navigate to it:</span></span>

    ```azurecli
    mkdir ~/coffee-maker
    cd ~/coffee-maker
    ```

1. <span data-ttu-id="37c63-127">在云`coffee-maker`命令行管理程序中的文件夹中, 执行以下命令以安装 DPS 密钥生成器:</span><span class="sxs-lookup"><span data-stu-id="37c63-127">From the `coffee-maker` folder in Cloud Shell, execute the following command to install the DPS key generator:</span></span> 

   ```azurecli
    npm install dps-keygen
   ```
    <span data-ttu-id="37c63-128">此命令将 keygen 包安装到本地文件夹中`coffee-maker`。</span><span class="sxs-lookup"><span data-stu-id="37c63-128">This command installs the dps-keygen package to our local folder, `coffee-maker`.</span></span> <span data-ttu-id="37c63-129">由于我们没有权限`-g`安装为全局包, 因此我们忽略了该选项。</span><span class="sxs-lookup"><span data-stu-id="37c63-129">We leave out the `-g` option because we don't have permissions to install as a global package.</span></span>

    <!-- TODO: Add more information about the DPS key generator and what it's used for -->
 
1. <span data-ttu-id="37c63-130">在云命令行管理程序中执行以下命令, 从 GitHub 下载 DPS 连接字符串实用工具:</span><span class="sxs-lookup"><span data-stu-id="37c63-130">Execute the following command in the Cloud Shell to download the DPS connection string utility from GitHub:</span></span> 

    ```azurecli
    wget https://github.com/Azure/dps-keygen/blob/master/bin/linux/dps_cstr?raw=true -O dps_cstr 
    ```

    > [!NOTE]
    > <span data-ttu-id="37c63-131">我们下载了 Linux 版本的**dps_cstr** , 因为我们正在云命令行管理程序中运行。</span><span class="sxs-lookup"><span data-stu-id="37c63-131">We downloaded the Linux version of **dps_cstr** because we're running in the Cloud Shell.</span></span>

1. <span data-ttu-id="37c63-132">执行以下命令以提供`dps_cstr` "执行" 权限:</span><span class="sxs-lookup"><span data-stu-id="37c63-132">Execute the following command to give `dps_cstr` execute permissions:</span></span>

    ```azurecli
    chmod +x dps_cstr
    ```

    <span data-ttu-id="37c63-133">若要为设备生成连接字符串, 我们需要 Azure IoT 中心门户中的三部分信息:</span><span class="sxs-lookup"><span data-stu-id="37c63-133">To generate a connection string for our device, we need three pieces of information from the Azure IoT Central portal:</span></span>
    - <span data-ttu-id="37c63-134">**范围 ID**</span><span class="sxs-lookup"><span data-stu-id="37c63-134">**Scope ID**</span></span>
    - <span data-ttu-id="37c63-135">**设备 ID**</span><span class="sxs-lookup"><span data-stu-id="37c63-135">**Device ID**</span></span>
    - <span data-ttu-id="37c63-136">**主关键字**</span><span class="sxs-lookup"><span data-stu-id="37c63-136">**Primary Key**</span></span>

1. <span data-ttu-id="37c63-137">返回到 IoT 中心门户。</span><span class="sxs-lookup"><span data-stu-id="37c63-137">Return to the IoT Central portal.</span></span> <span data-ttu-id="37c63-138">在*已连接的咖啡制造商-真实*设备的设备屏幕上, 选择屏幕右上方的 "**连接**"。</span><span class="sxs-lookup"><span data-stu-id="37c63-138">On the device screen for the *Connected Coffee Maker - Real* device, select **Connect** in the top right of the screen.</span></span>

1. <span data-ttu-id="37c63-139">在打开的 "设备连接" 对话框中, 将 "值**范围 id**"、"**设备 id** " 和 "**主键**" 都保存到某个地方, 因为我们将在本练习的后面使用它们。</span><span class="sxs-lookup"><span data-stu-id="37c63-139">On the Device Connection dialog that opens, save the values **Scope ID**, **Device ID** and **Primary Key** somewhere, because we'll use them later in this exercise.</span></span> 

1. <span data-ttu-id="37c63-140">在云命令行管理程序中执行以下命令, 将 **<scope_id>**、 **<device_id>** 和 **<primary_key>** 替换为您在上一步中保存的值。</span><span class="sxs-lookup"><span data-stu-id="37c63-140">Execute the following command in the Cloud Shell, replacing **<scope_id>**, **<device_id>**, and **<primary_key>** with the values you saved in the last step.</span></span> 

   ```azurecli
   ./dps_cstr [scope_id] [device_id] [primary_key] > connection.txt
   ```
  
    <span data-ttu-id="37c63-141">此命令根据您赋予它的值生成一个连接字符串, 并将其写入我们已命名为 " **connection**" 的文件。</span><span class="sxs-lookup"><span data-stu-id="37c63-141">This command generates a connection string based on the values you gave it and writes them to a file that we've named **connection.txt**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="37c63-142">命令不`dps_cstr`在命令行管理程序的路径中。</span><span class="sxs-lookup"><span data-stu-id="37c63-142">The command `dps_cstr` is not in your PATH in the shell.</span></span> <span data-ttu-id="37c63-143">因此, 请务必致电它`./dps_cstr`</span><span class="sxs-lookup"><span data-stu-id="37c63-143">So, make sure to call it with `./dps_cstr`</span></span>

1. <span data-ttu-id="37c63-144">通过运行以下命令, 在云命令行管理程序中打开集成代码编辑器:</span><span class="sxs-lookup"><span data-stu-id="37c63-144">Open the integrated code editor in the Cloud Shell by running the following command:</span></span> 

    ```azurecli
    code
    ```
1. <span data-ttu-id="37c63-145">从编辑器的 "**文件**" 菜单中的文件列表中选择 "**连接 .txt** "。</span><span class="sxs-lookup"><span data-stu-id="37c63-145">Select **connection.txt** from the list of files in the **FILES** menu of the editor.</span></span>

1. <span data-ttu-id="37c63-146">验证**连接 .txt**是否包含以的开头的连接字符串``HostName=``。</span><span class="sxs-lookup"><span data-stu-id="37c63-146">Verify that **connection.txt** contains a connection string that starts with ``HostName=``.</span></span>

1. <span data-ttu-id="37c63-147">从编辑器右上角的菜单 ("...")\*\* 中选择 "**关闭**编辑器", 以关闭编辑器。</span><span class="sxs-lookup"><span data-stu-id="37c63-147">Close the editor by selecting **Close Editor** from the menu (*...*) at the top right of the editor.</span></span> 

1. <span data-ttu-id="37c63-148">在云命令行管理程序中执行以下命令, 以初始化`coffee-maker`文件夹中的节点 .js 项目:</span><span class="sxs-lookup"><span data-stu-id="37c63-148">Execute the following command in the Cloud Shell to initialize a Node.js project in our `coffee-maker` folder:</span></span>

    ```azurecli
    npm init
    ```
    > [!NOTE]
    > <span data-ttu-id="37c63-149">init 脚本提示您输入项目属性。</span><span class="sxs-lookup"><span data-stu-id="37c63-149">The init script prompts you to enter project properties.</span></span> <span data-ttu-id="37c63-150">在此练习中, 请按 enter 以使用所有默认值。</span><span class="sxs-lookup"><span data-stu-id="37c63-150">For this exercise, press ENTER to use all default values.</span></span>

1. <span data-ttu-id="37c63-151">若要安装必要的程序包, 请在`coffee-maker`文件夹中运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="37c63-151">To install the necessary packages, run the following command in our `coffee-maker` folder:</span></span>

    ```azurecli
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="37c63-152">执行以下命令以在云命令行管理程序中创建新文件:</span><span class="sxs-lookup"><span data-stu-id="37c63-152">Execute the following command to create a new file in the Cloud Shell:</span></span>

    ```azurecli
    touch coffeeMaker.js
    ```
1. <span data-ttu-id="37c63-153">通过在云命令行管理程序中的命令行执行以下操作来打开集成代码编辑器:</span><span class="sxs-lookup"><span data-stu-id="37c63-153">Open the integrated code editor by executing the following at the command line in the Cloud Shell:</span></span> 

     ```azurecli
    code
    ```
    
1. <span data-ttu-id="37c63-154">当代码编辑器打开时, 选择 "**文件**" 列表中的 "刷新" 按钮, 然后选择我们的新文件**咖啡壶**。</span><span class="sxs-lookup"><span data-stu-id="37c63-154">When the code editor opens, select the refresh button on the **FILES** list and select our new file **coffeeMaker.js**.</span></span> 

1. <span data-ttu-id="37c63-155">将以下代码复制并粘贴到空编辑器窗口中:</span><span class="sxs-lookup"><span data-stu-id="37c63-155">Copy and paste the following code into the empty editor window:</span></span>

    ```js
    "use strict";

    // Use the Azure IoT device SDK for devices that connect to Azure IoT Central
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;

    // Connection string (TODO: CHANGE HERE)
    const connectionString = `{your device connection string}`;

    // Global variables
    var client = clientFromConnectionString(connectionString);
    var optimalTemperature = 96;
    var cupState = true;
    var brewingState = false;
    var cupTimer = 20;
    var brewingTimer = 0;
    var maintenanceState = false;
    var warrantyState = Math.random() < 0.5?0:1;

    // Helper function to produce nice numbers (##.#)
    function niceNumber(value) 
    {
        var number = (Math.round(value * 10.0)).toString();
        return number.substr(0, 2) + '.' + number.substr(2, 1);
    }

    // Send device simulated telemetry measurements
    function sendTelemetry() 
    {   
        // Simulate the telemetry values
        var temperature = optimalTemperature + (Math.random() * 4) - 2;
        var humidity = 20 + (Math.random() * 80);
        
        // Cup timer - every 20 seconds randomly decide if the cup is present or not
        cupTimer--;
        
        if (cupTimer == 0)
        {
            cupTimer = 20;
            cupState = Math.random() < 0.5?false:true;
        }
        
        // Brewing timer
        if (brewingTimer > 0)
        {
            brewingTimer--;
            
            // Finished brewing
            if (brewingTimer == 0)
            {
                brewingState = false;
            }
        }
    
        // Create the data JSON package
        var data = JSON.stringify(
        { 
            waterTemperature: temperature, 
            airHumidity: humidity, 
        });

        // Create the message with the above defined data
        var message = new Message(data);
        
        // Set the state flags
        message.properties.add('stateCupDetected', cupState);
        message.properties.add('stateBrewing', brewingState);
        
        // Show the information in console
        var infoTemperature = niceNumber(temperature);
        var infoHumidity = niceNumber(humidity);
        var infoCup = cupState ? 'Y' :'N';
        var infoBrewing = brewingState ? 'Y':'N';
        var infoMaintenance = maintenanceState ? 'Y':'N';
        
        console.log('Telemetry send: Temperature: ' + infoTemperature + 
                    ' Humidity: ' + infoHumidity + '%' + 
                    ' Cup Detected: ' + infoCup + 
                    ' Brewing: ' + infoBrewing + 
                    ' Maintenance Mode: ' + infoMaintenance);
        
        // Send the message
        client.sendEvent(message, function (errorMessage) 
        {
            // Error
            if (errorMessage) 
            {
                console.log('Failed to send message to Azure IoT Hub: ${err.toString()}');
            }
        });
    }

    // Send device properties
    function sendDeviceProperties(deviceTwin) 
    {
        var properties = 
        {
            propertyWarrantyExpired: warrantyState
        };
        
        console.log(' * Property - Warranty State: ' + warrantyState.toString());
        
        deviceTwin.properties.reported.update(properties, (errorMessage) => 
            console.log(` * Sent device properties ` + (errorMessage ? `Error: ${errorMessage.toString()}` : `(success)`)));
    }

    // Optimal temperature setting
    var settings = 
    {
        'setTemperature': (newValue, callback) => 
        {
            setTimeout(() => 
            {
                optimalTemperature = newValue;
                callback(optimalTemperature, 'completed');
            }, 1000);
        }
    };

    // Handle settings changes that come from Azure IoT Central via the device twin.
    function handleSettings(deviceTwin) 
    {
        deviceTwin.on('properties.desired', function (desiredChange) 
        {
            // Iterate all settings looking for the defined one
            for (let setting in desiredChange) 
            {
                // Setting we defined
                if (settings[setting]) 
                {
                    // Console info
                    console.log(` * Received setting: ${setting}: ${desiredChange[setting].value}`);
                    
                    // Update 
                    settings[setting](desiredChange[setting].value, (newValue, status, message) => 
                    {
                        var patch = 
                        {
                            [setting]: 
                            {
                                value: newValue,
                                status: status,
                                desiredVersion: desiredChange.$version,
                                message: message
                            }
                        }
                        deviceTwin.properties.reported.update(patch, (err) => console.log(` * Sent setting update for ${setting} ` +
                        (err ? `error: ${err.toString()}` : `(success)`)));
                    });
                }
            }
        });
    }

    // Maintenance mode command
    function onCommandMaintenance(request, response) 
    {
        // Display console info
        console.log(' * Maintenance command received');

        // Console warning
        if (maintenanceState)
        {
            console.log(' - Warning: The device is already in the maintenance mode.');
        }
        
        // Set state
        maintenanceState = true;

        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    function onCommandStartBrewing(request, response) 
    {
        // Display console info
        console.log(' * Brewing command received');

        // Console warning
        if (brewingState == true)
        {
            console.log(' - Warning: The device is already brewing.');
        }
        
        if (cupState == false)
        {
            console.log(' - Warning: The cup has not been detected.');
        }
        
        if (maintenanceState == true)
        {
            console.log(' - Warning: The device is in maintenance state.');
        }
        
        // Set state - brew for 30 seconds
        if ((cupState == true) && (brewingState == false) && (maintenanceState == false))
        {
            brewingState = true;
            brewingTimer = 30;
        }
        
        // Respond
        response.send(200, 'Success', function (errorMessage) 
        {
            // Failure
            if (errorMessage) 
            {
                console.error('[IoT hub Client] Failed sending a method response:\n' + errorMessage.message);
            }
        });
    }

    // Handle device connection to Azure IoT Central
    var connectCallback = (errorMessage) => 
    {
        // Connection error
        if (errorMessage) 
        {
            console.log(`Device could not connect to Azure IoT Central: ${errorMessage.toString()}`);
        } 
        // Successfully connected
        else 
        {
            // Notify the user
            console.log('Device successfully connected to Azure IoT Central');

            // Send telemetry measurements to Azure IoT Central every 1 second.
            setInterval(sendTelemetry, 1000);
            
            // Set up device command callbacks
            client.onDeviceMethod('cmdSetMaintenance', onCommandMaintenance);
            client.onDeviceMethod('cmdStartBrewing', onCommandStartBrewing);
            
            // Get device twin from Azure IoT Central
            client.getTwin((errorMessage, deviceTwin) => 
            {
                // Failed to retrieve device twin
                if (errorMessage) 
                {
                    console.log(`Error getting device twin: ${errorMessage.toString()}`);
                } 
                // Success
                else 
                {
                    // Notify the user
                    console.log('Device Twin successfully retrieved from Azure IoT Central');
                
                    // Send device properties once on device startup
                    sendDeviceProperties(deviceTwin);
                    
                    // Apply device settings and handle changes to device settings
                    handleSettings(deviceTwin);
                }
            });
        }
    };

    // Start the device (connect it to Azure IoT Central)
    client.open(connectCallback);

    ```

    <span data-ttu-id="37c63-156">将在 node.js 中写入咖啡机。</span><span class="sxs-lookup"><span data-stu-id="37c63-156">Our coffee machine is written in Node.js.</span></span> <span data-ttu-id="37c63-157">它首先连接到 Azure IoT Central。</span><span class="sxs-lookup"><span data-stu-id="37c63-157">It first connects to Azure IoT Central.</span></span> <span data-ttu-id="37c63-158">然后, 应用将初始属性发送到 Azure IoT Central、同步设置、为维护和 brewing 注册两个命令处理程序, 最后启动计时器以每秒发送遥测信息。</span><span class="sxs-lookup"><span data-stu-id="37c63-158">Then the app sends initial properties to Azure IoT Central, synchronizes settings, registers two command handlers for maintenance and brewing, and finally starts the timer for sending the telemetry information every second.</span></span>

1.  <span data-ttu-id="37c63-159">使用之前创建`{your device connection string}`的连接字符串更新此代码顶部的占位符, 并将其保存在**connection**中。</span><span class="sxs-lookup"><span data-stu-id="37c63-159">Update the placeholder `{your device connection string}` at the top of this code with the connection string you created earlier and saved in **connection.txt**.</span></span> <span data-ttu-id="37c63-160">连接字符串以开头`HostName=`。</span><span class="sxs-lookup"><span data-stu-id="37c63-160">The connection string begins with `HostName=`.</span></span>

1. <span data-ttu-id="37c63-161">选择编辑器右上部`...`的三个点以展开编辑器菜单。</span><span class="sxs-lookup"><span data-stu-id="37c63-161">Select the three dots `...` to the top right of the editor to expand the editor menu.</span></span> <span data-ttu-id="37c63-162">然后, 选择 "**保存**" 以保存对 "咖啡壶" 所做的编辑。</span><span class="sxs-lookup"><span data-stu-id="37c63-162">Then select **Save** to save the edits we made to \`coffeeMaker.js'</span></span>

1. <span data-ttu-id="37c63-163">在云命令行管理器窗口中执行以下命令, 以启动应用程序:</span><span class="sxs-lookup"><span data-stu-id="37c63-163">Execute the following command in the Cloud Shell window to start the app:</span></span>

    ```azurecli
    node coffeeMaker.js
    ```
1. <span data-ttu-id="37c63-164">验证应用程序是否在云命令行管理器窗口中启动, 邮件*设备是否已成功连接到 Azure IoT Central*以及*遥测发送:* 消息。</span><span class="sxs-lookup"><span data-stu-id="37c63-164">Verify that the app starts in the Cloud Shell window with the message *Device successfully connected to Azure IoT Central* along with *Telemetry send:* messages.</span></span> <span data-ttu-id="37c63-165">!!</span><span class="sxs-lookup"><span data-stu-id="37c63-165">Congratulations!</span></span> <span data-ttu-id="37c63-166">你的应用已启动并正在运行并与 IoT 中心通信!</span><span class="sxs-lookup"><span data-stu-id="37c63-166">Your app is up and running and communicating with IoT Central!</span></span>