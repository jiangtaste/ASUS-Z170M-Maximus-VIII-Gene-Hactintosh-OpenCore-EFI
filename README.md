# 华硕Maximus-VIII-Gene / M8G 黑苹果OpenCore EFI

先给OpenCore项目组100个赞（👍👍👍👍👍 * 20），OpenCore的折腾体验比起Clover好太多了。

## 更新说明

**2020.11.16**

1. 更新：Opencore升级至0.6.3，顺便更新了Kexts到最新版本；
2. 更新：支持MacOS Big Sur / MacOs 11 正式版，可无痛直接升级；
3. 修改：使用iMac19,1机型(其实效果差不多)。

使用说明：此次更新内容放入EFI-iMac19,1目录，下载后修改目录名为EFI，放入你的启动分区中（EFI分区）。Config.plist中PlatformInfo -> Generic 下MLB，SystemSerialNumber, SystemUUID三项已做随机处理，如你需要稳定使用，请自行使用Hackintool或Opencore cofnigurator生成后自行替换，参照“修改PlatformInfo说明.png"。

**2020.4.18**

1. 修改：将i5 6500对应的EFI更名位EFI-iMac17,1；
2. 新增：添加i5 8600K 核显版本，对应目录EFI-Macmini8,1；
3. 新增：添加i5 8600K + RX570版本，对应目录位EFI-iMac19,2。

使用：下载后，拷贝自己配置对应的EFI-XXX目录，更名为EFI放入你的启动分区根目录即可。如果作为稳定使用，请自行修改Config.plist中PlatformInfo -> Generic 下MLB，SystemSerialNumber, SystemUUID三项（可使用Hackintool生成），参照“修改PlatformInfo说明.png"

说明1：八九代的CPU都可使用的，有独显用iMac，无独显用Macmin。
说明2: iMac机型我使用了iMac19,2机型，对应21.5寸4K屏幕的白果。使用iMac19,1对应的27寸5K屏幕也是完全OK的，这个看自己喜好。ß

**2020.3.7**

1. 更新: OpenCore至0.5.6，顺便更新了Kexts至最新版本
2. 修复: 完成USB端口定制
3. 修复: 苹果开机原生快捷键可以使用了
4. 修复: 10.15.x系统下睡眠一段时间后被自动唤醒的BUG。（使用OpenCore官方提供的Kernel Patch）

因OpenCore升级后config.plist文件变动较多，请勿同其他版本混用。

## 补充说明

近日有小伙伴咨询魔改BIOS加8，9代CPU能否黑苹果的问题，简单说：支持。

我目前使用的也是魔改BIOS，只是CPU还是6代i5（还在观望i5 9600k的价格）。

如果你是8，9代CPU，记得修改SM机型到iMac19,1，另外注意下自己的核显型号，可能需要在DeviceProperties部分注入核显ID，资料请参照黑果小兵的博客。

## 概况

OpenCore版本：`0.5.6`

MacOS版本：`10.15.4`
ß
SM机型：`iMac19,2`

完美度程度：`99.9%`


## 能完美工作的部分

1. 完美睡眠唤醒，包括手动睡眠（Apple -> 睡眠）和定时睡眠（节能设置面板）
2. 原生电源管理，CPU完美变频，无需加载额外SSDT.aml（加载SSDT偏节能模式，CPU常在默频及以下工作，不加载则性能模式，更容易工作在默频和睿频。使用Inter Power Gadget观察，不一定严谨）
3. AirDrop，Continuity/Handoff，AirPlay完美工作
4. iMessage，Facetime，App Store完美工作
5. USB 3.0 及接口充电完美工作
6. USB 3.1，USB 3.1 Type C 及接口充电工作，但不完美
7. 声卡完美工作，包括HDMI和DP声音输出
8. 核显硬解及4K输出完美工作
9. USB已经定制好了，屏蔽了网线口那一排的两个USB3.0端口。

## 不（完美）工作的部分

无

## 配置单
 组件 | 配置 
----|----
CPU | 英特尔i5 8600K
主板 | ASUS MAXIMUS VIII GENE mATX z170
显卡1 | Inter UHD 630
显卡2 | 蓝宝石（Sapphire）超白金RX570 4GB
内存 | 芝奇幻光戟 2 * 16 GB DDR4 3000
无线 | 博通Broadcom 4331CD 802.11AC PCI-E接口
蓝牙 | 博通Broadcom 4331CD 4.0
硬盘1 | 英特尔 760P 256GB NVME接口
硬盘2 | 英特尔 545S 256GB SATA接口
机箱 | 迎光（IN WIN） 301 白色

## 为何选择Opencore（简称OC）

出于好奇尝试OC后，觉得OC已经具备了稳定使用的条件:

1. 清晰的配置说明。虽说OC没有Clover那样的图形化配置工具，准确说是因为还在beta版的原因没有稳定可用的图形化配置工具，但官方以及网上提供了详尽的配置参数说明文档。参照文档使用ProperTree一项一项的配置下来，你几乎能得到一份可用的config.plist配置文件。不想Clover那样抓瞎的配置，完了还存在多处冲突配置。注：Xcode 11版本编辑config.plist存在bug，不建议使用Xcode编辑配置文件。
2. 性能。不得不说OC引导的开关机速度相比Clover那是快了一大截呀。用Clover引导开机时，总怀疑我的电脑配置是不是太老旧了。
3. 便捷性。使用Clover，升级OS时，可能需要升级Clover才能继续使用。如果clover开启了快速引导（跳过倒计时），更新OS时可能遇到启动项未自动切换到安装更新的分区上而无法正确安装更新。这些问题OC很好的解决了，你甚至可以在系统偏好甚至中的启动磁盘里选择你想要的系统进行启动。
4. OC支持Boot Camp安装window。你可以在这里直选bootcamp windows启动，就像白果那样。（注：只是从windows不能便捷的切换到macOS，你需手动切换启动macOS，当然你可以像白果那样启动时按住option/esc进入启动项选择菜单，可惜我贴出的EFI配置中这项功能尚无法正常工作，所以我只能使用主板的F8选择硬盘来切换双系统）

## BIOS设定

**Extreme Tweeker​**
- AI Overclocker Tuner > X.M.P.​
- Extreme Tweeking > Enable​

**Advanced Items​**
- System Agent (SA) Configuration > VT-d > Disable​
- PCH Configuration > IOAPIC 24-119 > Disabled​
- USB Configuration > Legacy USB Support > Auto​
- USB Configuration > Keyboard and Mouse Simulation > Disabled
- APM Configuration > Power on by PCI - E/PCI > Disabled​
- Execute Disable Bit > Enable
- CFG Lock > Disabled

**Boot Menu​**
- Fast Boot > Disabled​
- Boot Logo Display > Disabled​
- Secure Boot > OS Type > Other OS​
- Above 4G decoding > Enable
- CSM > Disabled

保存并重启

## 制作安装U盘及安装系统简要说明
具体流程自行搜索，以下列出建议要点及流程
1. 在苹果商店下载苹果官方的原版镜像，尽量不用三方懒人包；
2. 参照网上教程将使用镜像提供的命令将镜像写入U盘中（最好是8G以上的USB3.0的U盘，安装速度会快一点）；
3. 将我提供的EFI文件夹拷贝至制作好的安装U盘的EFI分区中（可使用hackintool挂载EFI分区），这样引导器和安装U盘于一体，方便使用。注：某些U盘可能不存在EFI分区，此时可以将另外的U盘格式化为FAT格式并命名为EFI，拷贝我提供的EFI文件夹至此U盘（仅做引导）；
4. 重启，确保BIOS启动第一项为上述安装U盘或启动U盘（自行根据具体情况选择）；
5. 在OC的启动项选择界面，选择Install字样的项（就是上述制作的安装U盘的名字）；
6. 后续的流程应该是一条龙服务了，就像白果一样。

## EFI内容简述: 0.5.3版本

我的配置中对ACPI的部分定制的稍多，其他地方基本未做特别的修改。如果你是ASUS MAXIMUS VIII GENE mATX z170这块主板，显卡属于免驱的。无论其他配件如何，应该能直接使用的。

**ACPI项**

变色龙及Clover时代的ACPI搞得我头大，定制DSDT.aml时一头雾水，只能狂打能找到的所有补丁，参照资料过时且操作繁琐，具体什么效果也没研究清除。现在更倾向于下述的hotpatch的方式来打ACPI补丁，效果明了，思路清晰。我使用的补丁如下：

补丁 | 作用 | 必须
----|----|----
SSDT-PNLF.aml | WhateverGreen.kext包配套提供的补丁，一般用于笔记本亮度调节；（当初用Clover时，不知为何必须应用此补丁才能去紫条，你可以尝试不应用此补丁） | 可选
SSDT-EC.aml | USB相关的修复，USB定制也会生成此补丁。加载后USB才能完美工作 | 必须
SSDT-USBX.aml | USB充电相关的修复 | 必须
SSDT-PLUG-_PR.CPU0.aml | XCPM电源管理补丁。加载后可实现CPU完美变频和节能5项；
SSDT-SBUS.aml | 具体效果未知，但参照大佬们的资料，这块主板需打此补丁以更接近白果 | 必须
SSDT-HPET_RTC_TIMR.aml | 整合修复HPET_RTC_TIMR三个模块，具体效果未知，但必打此补丁，不打可能遇到重启，关机异常等问题 | 必须
SSDT-ALS0.aml, SSDT-DMAC.aml, SSDT-MCHC.aml, SSDT-MEM2.aml, SSDT-PMCR.aml | 添加缺失的硬件。这几个没有实际作用，打不打都不影响系统稳定。系统报告中将多出几个硬件信息（假的），使之更像白果。 | 可选

上述补丁外，无需再打其他任何补丁，亦不需要DSDT.aml了。尚有2处可进一步折腾：
1. 使用更节能的SSDT.aml来变频；（我挺满意现在的原生变频，性能强劲）
2. ~~定制USBPorts。（我未研究成功，索性解锁USB端口限制驱动所有USB端口）~~

**Drivers**

这个驱动主要是用于OC，与系统无关。其作用是让OC具有某种能力。我们需要使用的如下：

驱动 | 作用 | 必须
----|----|----
ApfsDriverLoader.efi | 让OC能识别APFS分区 | 必须
FwRuntimeServices.efi | 内存寻址补丁，未深入了解这个，反正就是黑果必须得有这货 | 必须
VirtualSmc.efi | 传感器依赖 | 必须
UsbKbDxe.efi | 让OC能使用苹果原生快捷键 | 可选
VBoxHfs.efi | 让OC能识别HFS分区，还有个HFSplus.efi效果一样，二选一 | 必须

我的版本中只需以上Drivers即可。若你需要OC具有更多能力，请自行查阅资料完善。

**Kexts**

Kexts主要用于驱动某些硬件，如声卡，网卡，显卡等等。

Kext| 作用 | 必须
----|----|----
Lilu.kext|Acidanthera驱动全家桶的底层依赖|必须
AppleALC.kext|驱动声卡, 依赖Lilu.kext|必须
InterMausi.kext|驱动有线网卡, 依赖Lilu.kext|必须
WhateverGreen.kext|驱动核显/修正显卡相关小问题, 依赖Lilu.kext|必须
VirtualSMC.kext|传感器驱动依赖|必须
HibernationFixup.kext|我用来修正无法定时睡眠的小问题|必须
USBInjectAll.kext|配合config.plist中XhciPortLimit=true来驱动所有USB端口|必须
NoTouchID.kext|避免输入框检测是否含有TouchID硬件，避免输入框卡顿|建议引入
SMCProcessor.kext|处理器传感器|可选
SMCSuperIO.kext|IO传感器|可选

**Config**

以下仅列出相对于sample.plist，我为提高我的硬件兼容性而修改了的配置项做说明，默认项自行查阅文档理解：

模块|子模块|项|说明|补充
----|----|----|----|----
Booter|Quirks|DisableSigleUser|禁用单用户，常见苹果文档|默认为false，我设为True，你根据自己需要调整
Booter|Quirks|ProvideCustomSlide|因前边未使用slide相关设置，此处也需禁用|默认为True，我设为false
DeviceProperties|Add|PciRoot(0x0)/Pci(0x1f,0x3)|此项用于注入声卡layoutid，我顺便注入了device-id|默认设备位置在PciRoot(0x0)/Pci(0x1b,0x0)，我的声卡位置在PciRoot(0x0)/Pci(0x1f,0x3)，默认layoutid为1，我使用1也能驱动声卡，但使用IOregisterExplore查看是，显示layoutid为7，所以我这里也使用7。
Kerner|Quirks|ThirdPartyDrives|开启SATA接口SSD硬盘的trim功能，提高SSD寿命|我有一块SATA接口的SSD，所以开启了此项，若果你只有NVME接口的SSD，系统默认开启了trim功能，此项可设为false
Kerner|Quirks|XhciPortLimit|解除系统最多15个USB端口的限制，那种USB3.0一般算两个端口，所以很容易超过15个端口的限制|因为我未成功定制USB端口，所以我打开了此项开驱动所有USB端口
Kerner|Quirks|DisableIoMapper|禁用vt-d|我们在BIOS里已经禁用vt-d了，这里我们选择NO就行了
Misc|Boot|HibernateMode|休眠模式相关（非睡眠）|为了兼容性好，我试试auto
Misc|Boot|PollAppleHotKeys|是否开启一些苹果原生热键功能，包括Cmd+K;Cmd+S|我选的是yes。如果你开机发现键盘无法选择，也选NO，并且删除OC/Drivers下的UsbKbDxe.efi
Misc|Boot|ShowPicker|是否显示OC启动项选择器|默认为True，我使用False来跳过这个界面加快启动。我提供的EFI中此项为True，方便安装系统时选择启动项，装完系统驱动调试完美后，将此项设为false来提升开机启动体验
Misc|Debug|DisplayLevel|日志等级|默认2147483650，我选0，关闭日志
Misc|Debug|Target|日志展示方式|默认3，我选0，不展示日志
Misc|Security|AllowNvramReset|允许重置NVRAM|默认False，我选True。我们的主板支持原生NVRAM，开启这项方便在OC开机启动项选择列表中便捷充值NVRAM
Misc|Security|RequireSignature|FileVault相关|默认tue，我选false。选true无法引导
Misc|Security|RequireVault|FileVault相关|默认tue，我选false。选true无法引导
Misc|Security|ScanPolicy|设置引导扫描的磁盘或文件类型|默认983299，我选0。扫描所有
NVRAM|7C436110-AB2A-4BBB-A880-FE41995C9F82|boot-args|引导参数|我去掉了-v（哆嗦模式）
PlatformInfo|Generic|SystemProductName|机型选择|我使用iMac17.1。我提供的文件未加入机型相关，你自行使用macinfo工具生成Generic下需要的所有信息
UEFI|Drivers|--|OC需加载的驱动|我加载了我前文Driver提到的efi文件
UEFI|Quirks|ProvideConsoleGop|开启后修复启动二阶段前一直黑屏的问题|默认false，我选true

注：有一些未提到的改动，无伤大雅，我自己也尚未清除打开或关闭会有什么不同的效果，就没列入上文。还请自行查阅文档深研。
