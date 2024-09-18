# 华硕 Maximus-VIII-Gene / M8G 黑苹果 OpenCore EFI

先给 OpenCore 项目组 100 个赞（👍👍👍👍👍 \* 20），OpenCore 的折腾体验比起 Clover 好太多了。

## 更新说明

**2024.9.19**

1. 更新：Opencore 升级只 1.0.0，顺便更新了 Kexts 到最新版本
2. 更新：完美支持 Ventura，Sonoma 中无线网卡需额外破解
3. 修改：仅保留 iMac19,1 机型

**2020.11.16**

1. 更新：Opencore 升级至 0.6.3，顺便更新了 Kexts 到最新版本；
2. 更新：支持 MacOS Big Sur / MacOs 11 正式版，可无痛直接升级；
3. 修改：使用 iMac19,1 机型(其实效果差不多)。

使用说明：此次更新内容放入 EFI-iMac19,1 目录，下载后修改目录名为 EFI，放入你的启动分区中（EFI 分区）。Config.plist 中 PlatformInfo -> Generic 下 MLB，SystemSerialNumber, SystemUUID 三项已做随机处理，如你需要稳定使用，请自行使用 Hackintool 或 Opencore cofnigurator 生成后自行替换，参照“修改 PlatformInfo 说明.png"。

**2020.4.18**

1. 修改：将 i5 6500 对应的 EFI 更名位 EFI-iMac17,1；
2. 新增：添加 i5 8600K 核显版本，对应目录 EFI-Macmini8,1；
3. 新增：添加 i5 8600K + RX570 版本，对应目录位 EFI-iMac19,2。

使用：下载后，拷贝自己配置对应的 EFI-XXX 目录，更名为 EFI 放入你的启动分区根目录即可。如果作为稳定使用，请自行修改 Config.plist 中 PlatformInfo -> Generic 下 MLB，SystemSerialNumber, SystemUUID 三项（可使用 Hackintool 生成），参照“修改 PlatformInfo 说明.png"

说明 1：八九代的 CPU 都可使用的，有独显用 iMac，无独显用 Macmin。
说明 2: iMac 机型我使用了 iMac19,2 机型，对应 21.5 寸 4K 屏幕的白果。使用 iMac19,1 对应的 27 寸 5K 屏幕也是完全 OK 的，这个看自己喜好。ß

**2020.3.7**

1. 更新: OpenCore 至 0.5.6，顺便更新了 Kexts 至最新版本
2. 修复: 完成 USB 端口定制
3. 修复: 苹果开机原生快捷键可以使用了
4. 修复: 10.15.x 系统下睡眠一段时间后被自动唤醒的 BUG。（使用 OpenCore 官方提供的 Kernel Patch）

因 OpenCore 升级后 config.plist 文件变动较多，请勿同其他版本混用。

## 概况

OpenCore 版本：`1.0.0`

MacOS 版本：`13.6.8`
ß
SM 机型：`iMac19,1`

完美度程度：`99.9%`

## 魔改 BIOS

魔改 BIOS 加 8，9 代 CPU 能完美支持黑苹果。我用的 i5-8600k，无需额外配置完美适配。

## 能完美工作的部分

1. 完美睡眠唤醒，包括手动睡眠（Apple -> 睡眠）和定时睡眠（节能设置面板）
2. 原生电源管理，CPU 完美变频，无需加载额外 SSDT.aml（加载 SSDT 偏节能模式，CPU 常在默频及以下工作，不加载则性能模式，更容易工作在默频和睿频。使用 Inter Power Gadget 观察，不一定严谨）
3. AirDrop，Continuity/Handoff，AirPlay 完美工作
4. iMessage，Facetime，App Store 完美工作
5. USB 3.0 及接口充电完美工作
6. USB 3.1，USB 3.1 Type C 及接口充电工作完美
7. 声卡完美工作，包括 HDMI 和 DP 声音输出
8. 核显硬解及 4K 输出完美工作
9. USB 完美定制

## 不（完美）工作的部分

无

## 配置单

| 组件   | 配置                                       |
| ------ | ------------------------------------------ |
| CPU    | 英特尔 i5 8600K                            |
| 主板   | ASUS MAXIMUS VIII GENE mATX z170           |
| 显卡 1 | Inter UHD 630                              |
| 显卡 2 | 蓝宝石（Sapphire）超白金 RX590 8GB         |
| 内存   | 芝奇幻光戟 2 \* 16 GB DDR4 3000            |
| 无线   | 博通 Broadcom 94360CD2 802.11AC PCI-E 接口 |
| 蓝牙   | 博通 Broadcom 94360CD2 4.0                 |
| 硬盘 1 | 英特尔 760P 256GB NVME 接口                |
| 硬盘 2 | 英特尔 545S 256GB SATA 接口                |
| 机箱   | 迎光（IN WIN） 301 白色                    |

## 为何选择 Opencore（简称 OC）

出于好奇尝试 OC 后，觉得 OC 已经具备了稳定使用的条件:

1. 清晰的配置说明。虽说 OC 没有 Clover 那样的图形化配置工具，准确说是因为还在 beta 版的原因没有稳定可用的图形化配置工具，但官方以及网上提供了详尽的配置参数说明文档。参照文档使用 ProperTree 一项一项的配置下来，你几乎能得到一份可用的 config.plist 配置文件。不想 Clover 那样抓瞎的配置，完了还存在多处冲突配置。注：Xcode 11 版本编辑 config.plist 存在 bug，不建议使用 Xcode 编辑配置文件。
2. 性能。不得不说 OC 引导的开关机速度相比 Clover 那是快了一大截呀。用 Clover 引导开机时，总怀疑我的电脑配置是不是太老旧了。
3. 便捷性。使用 Clover，升级 OS 时，可能需要升级 Clover 才能继续使用。如果 clover 开启了快速引导（跳过倒计时），更新 OS 时可能遇到启动项未自动切换到安装更新的分区上而无法正确安装更新。这些问题 OC 很好的解决了，你甚至可以在系统偏好甚至中的启动磁盘里选择你想要的系统进行启动。
4. OC 支持 Boot Camp 安装 window。你可以在这里直选 bootcamp windows 启动，就像白果那样。（注：只是从 windows 不能便捷的切换到 macOS，你需手动切换启动 macOS，当然你可以像白果那样启动时按住 option/esc 进入启动项选择菜单，可惜我贴出的 EFI 配置中这项功能尚无法正常工作，所以我只能使用主板的 F8 选择硬盘来切换双系统）

## BIOS 设定

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

## 制作安装 U 盘及安装系统简要说明

具体流程自行搜索，以下列出建议要点及流程

1. 在苹果商店下载苹果官方的原版镜像，尽量不用三方懒人包；
2. 参照网上教程将使用镜像提供的命令将镜像写入 U 盘中（最好是 8G 以上的 USB3.0 的 U 盘，安装速度会快一点）；
3. 将我提供的 EFI 文件夹拷贝至制作好的安装 U 盘的 EFI 分区中（可使用 hackintool 挂载 EFI 分区），这样引导器和安装 U 盘于一体，方便使用。注：某些 U 盘可能不存在 EFI 分区，此时可以将另外的 U 盘格式化为 FAT 格式并命名为 EFI，拷贝我提供的 EFI 文件夹至此 U 盘（仅做引导）；
4. 重启，确保 BIOS 启动第一项为上述安装 U 盘或启动 U 盘（自行根据具体情况选择）；
5. 在 OC 的启动项选择界面，选择 Install 字样的项（就是上述制作的安装 U 盘的名字）；
6. 后续的流程应该是一条龙服务了，就像白果一样。

## EFI 内容简述

以下内容未完全更新，随着 OC 版本的更新，部分文件有细微升级变化，但本质都一样，只是实现的原理和细节有些未差别，供参考。

我的配置中对 ACPI 的部分定制的稍多，其他地方基本未做特别的修改。如果你是 ASUS MAXIMUS VIII GENE mATX z170 这块主板，显卡属于免驱的。无论其他配件如何，应该能直接使用的。

**ACPI 项**

变色龙及 Clover 时代的 ACPI 搞得我头大，定制 DSDT.aml 时一头雾水，只能狂打能找到的所有补丁，参照资料过时且操作繁琐，具体什么效果也没研究清除。现在更倾向于下述的 hotpatch 的方式来打 ACPI 补丁，效果明了，思路清晰。我使用的补丁如下：

| 补丁                                                                      | 作用                                                                                                                                        | 必须 |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ---- |
| SSDT-PNLF.aml                                                             | WhateverGreen.kext 包配套提供的补丁，一般用于笔记本亮度调节；（当初用 Clover 时，不知为何必须应用此补丁才能去紫条，你可以尝试不应用此补丁） | 可选 |
| SSDT-EC.aml                                                               | USB 相关的修复，USB 定制也会生成此补丁。加载后 USB 才能完美工作                                                                             | 必须 |
| SSDT-USBX.aml                                                             | USB 充电相关的修复                                                                                                                          | 必须 |
| SSDT-PLUG-\_PR.CPU0.aml                                                   | XCPM 电源管理补丁。加载后可实现 CPU 完美变频和节能 5 项；                                                                                   |
| SSDT-SBUS.aml                                                             | 具体效果未知，但参照大佬们的资料，这块主板需打此补丁以更接近白果                                                                            | 必须 |
| SSDT-HPET_RTC_TIMR.aml                                                    | 整合修复 HPET_RTC_TIMR 三个模块，具体效果未知，但必打此补丁，不打可能遇到重启，关机异常等问题                                               | 必须 |
| SSDT-ALS0.aml, SSDT-DMAC.aml, SSDT-MCHC.aml, SSDT-MEM2.aml, SSDT-PMCR.aml | 添加缺失的硬件。这几个没有实际作用，打不打都不影响系统稳定。系统报告中将多出几个硬件信息（假的），使之更像白果。                            | 可选 |

上述补丁外，无需再打其他任何补丁，亦不需要 DSDT.aml 了。尚有 2 处可进一步折腾：

1. 使用更节能的 SSDT.aml 来变频；（我挺满意现在的原生变频，性能强劲）

**Drivers**

这个驱动主要是用于 OC，与系统无关。其作用是让 OC 具有某种能力。我们需要使用的如下：

| 驱动                  | 作用                                                       | 必须 |
| --------------------- | ---------------------------------------------------------- | ---- |
| ApfsDriverLoader.efi  | 让 OC 能识别 APFS 分区                                     | 必须 |
| FwRuntimeServices.efi | 内存寻址补丁，未深入了解这个，反正就是黑果必须得有这货     | 必须 |
| VirtualSmc.efi        | 传感器依赖                                                 | 必须 |
| UsbKbDxe.efi          | 让 OC 能使用苹果原生快捷键                                 | 可选 |
| VBoxHfs.efi           | 让 OC 能识别 HFS 分区，还有个 HFSplus.efi 效果一样，二选一 | 必须 |

我的版本中只需以上 Drivers 即可。若你需要 OC 具有更多能力，请自行查阅资料完善。

**Kexts**

Kexts 主要用于驱动某些硬件，如声卡，网卡，显卡等等。

| Kext               | 作用                                        | 必须 |
| ------------------ | ------------------------------------------- | ---- |
| Lilu.kext          | Acidanthera 驱动全家桶的底层依赖            | 必须 |
| AppleALC.kext      | 驱动声卡, 依赖 Lilu.kext                    | 必须 |
| InterMausi.kext    | 驱动有线网卡, 依赖 Lilu.kext                | 必须 |
| WhateverGreen.kext | 驱动核显/修正显卡相关小问题, 依赖 Lilu.kext | 必须 |
| VirtualSMC.kext    | 传感器驱动依赖                              | 必须 |
| USBPorts.kext      | 端口定制，引入时可将 XhciPortLimit=false    | 必须 |
| SMCProcessor.kext  | 处理器传感器                                | 可选 |
| SMCSuperIO.kext    | IO 传感器                                   | 可选 |

**Config**

以下仅列出相对于 sample.plist，我为提高我的硬件兼容性而修改了的配置项做说明，默认项自行查阅文档理解：

| 模块             | 子模块                               | 项                         | 说明                                                                                          | 补充                                                                                                                                                                                                       |
| ---------------- | ------------------------------------ | -------------------------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Booter           | Quirks                               | DisableSigleUser           | 禁用单用户，常见苹果文档                                                                      | 默认为 false，我设为 True，你根据自己需要调整                                                                                                                                                              |
| Booter           | Quirks                               | ProvideCustomSlide         | 因前边未使用 slide 相关设置，此处也需禁用                                                     | 默认为 True，我设为 false                                                                                                                                                                                  |
| DeviceProperties | Add                                  | PciRoot(0x0)/Pci(0x1f,0x3) | 此项用于注入声卡 layoutid，我顺便注入了 device-id                                             | 默认设备位置在 PciRoot(0x0)/Pci(0x1b,0x0)，我的声卡位置在 PciRoot(0x0)/Pci(0x1f,0x3)，默认 layoutid 为 1，我使用 1 也能驱动声卡，但使用 IOregisterExplore 查看是，显示 layoutid 为 7，所以我这里也使用 7。 |
| Kerner           | Quirks                               | ThirdPartyDrives           | 开启 SATA 接口 SSD 硬盘的 trim 功能，提高 SSD 寿命                                            | 我有一块 SATA 接口的 SSD，所以开启了此项，若果你只有 NVME 接口的 SSD，系统默认开启了 trim 功能，此项可设为 false                                                                                           |
| Kerner           | Quirks                               | XhciPortLimit              | 解除系统最多 15 个 USB 端口的限制，那种 USB3.0 一般算两个端口，所以很容易超过 15 个端口的限制 | 因为我未成功定制 USB 端口，所以我打开了此项开驱动所有 USB 端口                                                                                                                                             |
| Kerner           | Quirks                               | DisableIoMapper            | 禁用 vt-d                                                                                     | 我们在 BIOS 里已经禁用 vt-d 了，这里我们选择 NO 就行了                                                                                                                                                     |
| Misc             | Boot                                 | HibernateMode              | 休眠模式相关（非睡眠）                                                                        | 为了兼容性好，我试试 auto                                                                                                                                                                                  |
| Misc             | Boot                                 | PollAppleHotKeys           | 是否开启一些苹果原生热键功能，包括 Cmd+K;Cmd+S                                                | 我选的是 yes。如果你开机发现键盘无法选择，也选 NO，并且删除 OC/Drivers 下的 UsbKbDxe.efi                                                                                                                   |
| Misc             | Boot                                 | ShowPicker                 | 是否显示 OC 启动项选择器                                                                      | 默认为 True，我使用 False 来跳过这个界面加快启动。我提供的 EFI 中此项为 True，方便安装系统时选择启动项，装完系统驱动调试完美后，将此项设为 false 来提升开机启动体验                                        |
| Misc             | Debug                                | DisplayLevel               | 日志等级                                                                                      | 默认 2147483650，我选 0，关闭日志                                                                                                                                                                          |
| Misc             | Debug                                | Target                     | 日志展示方式                                                                                  | 默认 3，我选 0，不展示日志                                                                                                                                                                                 |
| Misc             | Security                             | AllowNvramReset            | 允许重置 NVRAM                                                                                | 默认 False，我选 True。我们的主板支持原生 NVRAM，开启这项方便在 OC 开机启动项选择列表中便捷充值 NVRAM                                                                                                      |
| Misc             | Security                             | RequireSignature           | FileVault 相关                                                                                | 默认 tue，我选 false。选 true 无法引导                                                                                                                                                                     |
| Misc             | Security                             | RequireVault               | FileVault 相关                                                                                | 默认 tue，我选 false。选 true 无法引导                                                                                                                                                                     |
| Misc             | Security                             | ScanPolicy                 | 设置引导扫描的磁盘或文件类型                                                                  | 默认 983299，我选 0。扫描所有                                                                                                                                                                              |
| NVRAM            | 7C436110-AB2A-4BBB-A880-FE41995C9F82 | boot-args                  | 引导参数                                                                                      | 我去掉了-v（哆嗦模式）                                                                                                                                                                                     |
| PlatformInfo     | Generic                              | SystemProductName          | 机型选择                                                                                      | 我使用 iMac17.1。我提供的文件未加入机型相关，你自行使用 macinfo 工具生成 Generic 下需要的所有信息                                                                                                          |
| UEFI             | Drivers                              | --                         | OC 需加载的驱动                                                                               | 我加载了我前文 Driver 提到的 efi 文件                                                                                                                                                                      |
| UEFI             | Quirks                               | ProvideConsoleGop          | 开启后修复启动二阶段前一直黑屏的问题                                                          | 默认 false，我选 true                                                                                                                                                                                      |

注：有一些未提到的改动，无伤大雅，我自己也尚未清除打开或关闭会有什么不同的效果，就没列入上文。还请自行查阅文档深研。
