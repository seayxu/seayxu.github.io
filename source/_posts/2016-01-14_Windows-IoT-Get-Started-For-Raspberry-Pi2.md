---
title: 树莓派(Raspberry Pi2)Windows IoT入门
date: 2016-01-14 23:32:55
categories:
- Raspberry Pi
- Windows IoT
tags:
- Windows IoT
- Raspberry Pi 2
- 树莓派
---


##  [设置电脑][0]
### 在电脑上设置 Visual Studio 2015

若要设置 Windows 10 IoT 核心版开发电脑，首先需要安装以下内容：

1. **请确保运行的是 Windows 10（版本 10240）的公共版本或更高版本**。可从[此处][d1]升级。如果已经运行 Windows 10，可通过单击“开始”按钮、键入“winver”并点击 Enter，查找当前版本号。

2. 在[此处][d2]**安装** Visual Studio Community 2015。可从[此处][d3]下载 Visual Studio `Professional 2015` 和 Visual Studio `Enterprise` 2015。

	**注意：** 如果选择安装不同版本的 VS 2015，请确保执行“自定义”安装，并依次选中“通用 Windows 应用开发工具”->“工具和 Windows SDK”复选框。

3. 通过依次选择“帮助”>“关于 Microsoft Visual Studio”**验证** Visual Studio **安装**。“Visual Studio”的所需版本是 `14.0.23107.0 D14Rel`。“用于通用 Windows 应用的 Visual Studio 工具”的所需版本是 `14.0.23121.00 D14OOB`。

4. 确保已按照[这些说明][a0]启用了**开发人员模式**。


## [设置你的设备][1]

### 需要具备的条件

1. **运行 Windows 10 的电脑**（在上一步中已准备就绪）

2. **Raspberry Pi 2**

3. **5V 微型 USB 电源** - 使用至少 1.0A 电流。如果计划使用多个高耗电 USB 外围设备，请改用电流较高的电源 (>2.0A)。

4. **8GB 微型 SD 卡** - 类 10 或更高。（我们建议使用[这个][a1]或[这个][a2]）

5. **HDMI 电缆和监视器**

6. **以太网电缆**

7. **微型 SD 卡读卡器**（因为大多数内部 SD 卡读卡器均会出现问题，所以我们建议使用外部 USB 卡读卡器，例如[这个][a3]或[这个][a4]）

### 安装 Windows 10 IoT 核心版工具

1. 从 Microsoft 下载中心[下载][d4]用于 Raspberry Pi 2 的 ISO。

2. 将 ISO 保存到本地文件夹

	![][a5]

3. 双击 ISO（IoT 核心版 RPi.iso）。它将自动将其本身作为虚拟驱动器进行装载，以便你可以访问内容。

	![][a6]

4. 安装 Windows_10_IoT_Core_RPi2.msi。安装完成后，flash.ffu 将位于 C:\Program Files (x86)\Microsoft IoT\FFU\RaspberryPi2

	![][a7]

5. 完成后将弹出虚拟 CD

### 将 Windows 10 IoT Core Insider Preview 映像放置在 SD 卡上

1. 将微型 SD 卡插入 SD 卡读卡器。

2. 使用 IoTCoreImageHelper.exe 切换 SD 卡。从“开始”菜单搜索“WindowsIoT”，并选择快捷方式“WindowsIoTImageHelper”

	![][a8]

3. 该工具将按照显示方式枚举设备。选择希望切换的 SD 卡，然后提供 FFU 的位置并切换映像。
	![][a9]

4. 单击任务栏中的“安全删除硬件”图标，然后选择你的 USB SD 读卡器以将其从系统中安全删除。如果未正确执行此操作，可能导致映像损坏。

  **注意**： 如果希望在使用完 Windows 10 IoT 核心版后将其从 SD 卡中删除，请参阅标题为**如何从 SD 卡中删除 Windows 10 IoT 核心版？**的[常见问题][a10]部分。

  **注意**： IoTCoreImageHelper.exe 是推荐用来切换 SD 卡的工具。但是，说明可用于直接使用 [DISM 命令][a11]行工具

### 连接电路板

1. 插入已准备的**微型 SD 卡**（插槽在如下所示的电路板的另一侧）。

2. **将网络电缆**从本地网络连接到电路板上的以太网端口。请确保开发电脑在同一网络上。

  **注意**： 如果没有本地有线网络，请参阅[此处][a12]获取其他连接选项。

3. **将 HDMI 监视器连接到**电路板上的 HDMI 端口。

4. **将电源连接到**开发板上的微型 USB 端口。

	![][a13]

### 启动 Windows 10 IoT 核心版

1. 连接电源后，Windows 10 IoT 核心版将自动启动。这可能需要几分钟时间。

2. 启动设备后，DefaultApp 将启动并显示 RPi2 的 IP 地址。

	![][a14]

3. 遵循[此处的 PowerShell 文档][a15]，使用 PowerShell 连接到正在运行的设备。也可按照[此处][a16]的说明使用 SSH 连接到设备。

4. **强烈推荐**更新管理员帐户的默认密码。若要执行此操作，请在 PowerShell 连接中发出以下命令：

  使用强密码替换 ` [new password] `：

  ```
  net user Administrator [new password]
  ```

  此操作完成后，将需要使用 psSession 和新凭据重新建立当前会话。

### 其他资源
* [受支持的外围接口和设备][a17]

## [开发][2]

### Blinky 示例

我们将创建一个简单的 LED 闪烁应用并将 LED 连接到你的 Windows 10 IoT Core 设备。

这是一个有外设的示例。若要更好地了解什么是有外设的模式以及如何将你的设备配置为有外设，请按照[此处][a18]的说明操作。

另外，还请注意 GPIO API 仅在 Windows 10 IoT Core 上可用，因此该示例无法在你的桌面上运行。

在 Visual Studio 中加载项目

你可以通过在[此处][d5]下载所有示例的 zip 并导航到 `samples-develop\Blinky`，查找此示例的源代码。示例代码可采用 C++ 或 C# 提供，但此处的文档仅详细介绍了 C# 变体。在磁盘上创建文件夹的副本，然后从 Visual Studio 中打开项目。

#### 将 LED 连接到你的 Windows IoT 设备

你将会需要一些组件：

* 一个 LED（你喜欢的任意一种颜色）

* 一个 220 Ω 电阻器

* 一块试验板和几根连接线

	![][a19]

#### 适用于 Raspberry Pi 2 (RPi2)

我们要将 LED 的一端连接到 RPi2 上的 GPIO 5（JP3 扩展头上的引脚 29），将另一端连接到电阻器，并将电阻器连接到 RPi2 上的 3.3 伏电源。请注意 LED 的正负极非常重要。请确保将较短的腿 (-) 连接到 GPIO 5 并将较长的腿 (+) 连接到电阻器，否则它不会点亮。

下面是 RPi2 的引出线：

![][a20]

*使用 [Fritzing][3] 制作的图像*

下面是使用电路组装的试验板可能样子的一个示例：

![][a21]

*使用 [Fritzing][3] 制作的图像*

#### 适用于 MinnowBoard Max (MBM)

我们要将 LED 的一端连接到 MBM 上的 GPIO 5（JP1 扩展头上的引脚 18），将另一端连接到电阻器，并将电阻器连接到 MBM 上的 3.3 伏电源。请注意 LED 的正负极非常重要。请确保将较短的腿 (-) 连接到 GPIO 5 并将较长的腿 (+) 连接到电阻器，否则它不会点亮。

以下是 MBM 上的 JP1 连接器：

![][a22]

*使用 [Fritzing][3] 制作的图像*

下面是使用电路组装的试验板可能样子的一个示例：

![][a23]

*使用 [Fritzing][3] 制作的图像*

#### 部署你的应用

1. 应用程序在 Visual Studio 中打开后，在工具栏下拉列表中设置体系结构。如果针对 MinnowBoard Max 进行生成，请选择 `x86`。如果针对 Raspberry Pi 2 进行生成，请选择 `ARM`。

2. 接下来，在 Visual Studio 工具栏中，单击` Local Machine `下拉列表并选择 `Remote Machine`

	![][a24]

3. 此时，Visual Studio 将显示“远程连接”对话框。如果以前使用过 [PowerShell][a25] 设置设备的唯一名称，可在此处输入该名称（在此示例中，我们使用的是 my-device）。否则，使用 Windows IoT 核心版设备的 IP 地址。输入设备名称/IP 后，选择 `None` 进行 Windows 身份验证，然后单击“选择”。

	![][a26]

4. 可通过导航到项目属性（在解决方案资源管理器中选择“属性”）并在左侧选择 Debug 选项卡来验证或修改这些值：

	![项目属性调试选项卡][a27]

完成所有设置后，你应可以在 Visual Studio 中按 F5。Blinky 应用将会部署并在 Windows IoT 设备上启动，此时你应会看到 LED 与屏幕上的模拟图像同步闪烁。

![][a28]

恭喜你！ 你已控制了 Windows IoT 设备上的一个 GPIO 引脚！

#### 我们来看看代码

此示例的代码相当简单。我们使用了一个计时器，每当调用“Tick”事件时，都会切换 LED 的状态。

##### 计时器代码

下面说明如何使用 C# 语言设置计时器：

``` cs
public MainPage()
{
    // ...

    this.timer = new DispatcherTimer();
    this.timer.Interval = TimeSpan.FromMilliseconds(500);
    this.timer.Tick += Timer_Tick;
    this.timer.Start();

    // ...
}

private void Timer_Tick(object sender, object e)
{
    FlipLED();
}
```

##### 初始化 GPIO 引脚

为了驱动 GPIO 引脚，首先我们需要对其进行初始化。以下是 C# 代码（请注意我们如何在 Windows.Devices.Gpio 命名空间中利用新 WinRT 类）：

``` cs
using Windows.Devices.Gpio;

private void InitGPIO()
{
    var gpio = GpioController.GetDefault();

    // Show an error if there is no GPIO controller
    if (gpio == null)
    {
        pin = null;
        GpioStatus.Text = "There is no GPIO controller on this device.";
        return;
    }

    pin = gpio.OpenPin(LED_PIN);

    // Show an error if the pin wasn't initialized properly
    if (pin == null)
    {
        GpioStatus.Text = "There were problems initializing the GPIO pin.";
        return;
    }

    pin.Write(GpioPinValue.High);
    pin.SetDriveMode(GpioPinDriveMode.Output);

    GpioStatus.Text = "GPIO pin initialized correctly.";
}
```

让让我们稍稍细分一下此过程：

*  首先，我们使用 `GpioController.GetDefault()` 获取 GPIO 控制器。

* 如果设备没有 GPIO 控制器，则此函数将返回 `null`。

* 然后，我们尝试通过使用 `LED_PIN` 值调用 `GpioController.OpenPin()` 来打开引脚。

* 获取 `pin` 后，我们会使用 `GpioPin.Write()` 函数将它设置为默认的关闭状态（高）。

* 我们还使用了 `GpioPin.SetDriveMode()` 函数将 `pin` 设置为以输出模式运行。

##### 修改 GPIO 引脚的状态

在具有` GpioOutputPin` 实例的访问权限后，没有必要再通过更改引脚状态来打开或关闭 LED。

若要打开 LED，只需将值 `GpioPinValue.Low` 写入引脚：

```
this.pin.Write(GpioPinValue.Low);
```

当然，写入 `GpioPinValue.High` 便会关闭 LED：

```
this.pin.Write(GpioPinValue.High);
```

记得我们已将 LED 的另一端连接到了 3.3 伏电源，因此，我们需要将引脚驱动到低位，使电流通过 LED。

>本文来源:[`微软Windows IoT官网`][4]

[0]:http://ms-iot.github.io/content/zh-CN/win10/SetupPCRPI.htm
[1]:http://ms-iot.github.io/content/zh-CN/win10/SetupRPI.htm
[2]:http://ms-iot.github.io/content/zh-CN/win10/samples/Blinky.htm
[3]:http://fritzing.org/
[4]:http://ms-iot.github.io/content/zh-CN/GetStarted.htm

[a0]:https://msdn.microsoft.com/library/windows/apps/xaml/dn706236.aspx
[a1]:http://www.amazon.com/gp/product/B00IVPU786
[a2]:http://www.amazon.com/SanDisk-Ultra-Micro-SDHC-16GB/dp/9966573445
[a3]:http://www.amazon.com/dp/B009D79VH4
[a4]:http://www.amazon.com/dp/B0096FB5CW
[a5]:http://ms-iot.github.io/content/images/SetupRPI/Iso.PNG
[a6]:http://ms-iot.github.io/content/images/SetupRPI/MSI.PNG
[a7]:http://ms-iot.github.io/content/images/SetupRPI/rpiffu.PNG
[a8]:http://ms-iot.github.io/content/images/ImagerHelperSearch.PNG
[a9]:http://ms-iot.github.io/content/images/SetupRPI/ImageHelper.PNG
[a10]:http://ms-iot.github.io/content/zh-CN/Faqs.htm
[a11]:http://ms-iot.github.io/content/zh-CN/win10/samples/DISM.htm
[a12]:http://ms-iot.github.io/content/zh-CN/win10/ConnectToDevice.htm
[a13]:http://ms-iot.github.io/content/images/rpi2.png
[a14]:http://ms-iot.github.io/content/images/DefaultAppRpi2.png
[a15]:http://ms-iot.github.io/content/zh-CN/win10/samples/PowerShell.htm
[a16]:http://ms-iot.github.io/content/zh-CN/win10/samples/SSH.htm
[a17]:http://ms-iot.github.io/content/zh-CN/win10/SupportedInterfaces.htm
[a18]:http://ms-iot.github.io/content/zh-CN/win10/HeadlessMode.htm
[a19]:http://ms-iot.github.io/content/images/Blinky/components.png
[a20]:http://ms-iot.github.io/content/images/PinMappings/RP2_Pinout.png
[a21]:http://ms-iot.github.io/content/images/Blinky/breadboard_assembled_rpi2.png
[a22]:http://ms-iot.github.io/content/images/PinMappings/MBM_Pinout.png
[a23]:http://ms-iot.github.io/content/images/Blinky/breadboard_assembled.png
[a24]:http://ms-iot.github.io/content/images/AppDeployment/cs-remote-machine-debugging.png
[a25]:http://ms-iot.github.io/content/zh-CN/win10/samples/PowerShell.htm
[a26]:http://ms-iot.github.io/content/images/AppDeployment/cs-remote-connections.PNG
[a27]:http://ms-iot.github.io/content/images/AppDeployment/cs-debug-project-properties.PNG
[a28]:http://ms-iot.github.io/content/images/Blinky/blinky-screenshot.png

[d1]:http://www.microsoft.com/zh-CN/software-download/windows10
[d2]:http://go.microsoft.com/fwlink/?LinkID=534599
[d3]:https://www.visualstudio.com/vs-2015-product-editions
[d4]:http://go.microsoft.com/fwlink/?LinkId=616847
[d5]:https://github.com/ms-iot/samples/archive/develop.zip
