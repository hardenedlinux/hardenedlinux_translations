# 附录 A Awesome Firmware Security

[https://github.com/PreOS-Security/awesome-firmware-security/](https://github.com/PreOS-Security/awesome-firmware-security/)

良好固件安全（Awesome Firmware Security）是一个关于平台固件资源的精选列表，其关注焦点是安全性和测试。它由 PreOS Security 创建。

**免责声明**：固件也是软件，但是即使您能够删除并且重新安装您的硬盘上的软件，当您处理固件时有可能使您的系统变砖。谨慎操作，并且自行承担风险。

**注记**：物联网/嵌入式操作系统的安全性并未被添加进来，除非它们刚好和平台安全性发生重叠，诸如 Intel AMT、AMD PSP、Redfish、IPMI、BMC、OpenBMC 等。已经有一些关于物联网/嵌入式操作系统的良好列表，例如 Awesome IoT。

## 技术和术语

这些技术中的每一项就其自身而言都是极好的，并且我们将会在某个时机为其制作一份独立的良好列表。此时，它们构成了我们的索引。

* [ACPICA](https://acpica.org)——ACPI 组件架构项目（ACPICA）提供了一系列跨平台的 ACPI 工具，诸如 acpidump
* [ACPI](http://uefi.org/acpi/)——ACPI 是一种平台固件技术，它最初是要用于替代即插即用、MP 和高级电源管理。UEFI 论坛拥有其规范并且维护一份与 ACPI 相关的文档的良好列表
* [ACPICA](https://acpica.org)——ACPI 组件架构项目（ACPICA）提供了一种参考实现以及一系列跨平台的 ACPI 工具，诸如 acpidump
* [ARC](https://en.wikipedia.org/wiki/Advanced_RISC_Computing)——ARC（高级计算环境）是一种用于早期的非 Intel 系统上的 Windows NT 的平台固件技术。ARC 的设计影响到了 UEFI 的设计：由变量指向位于一个硬盘分区上的固件镜像、
* [BIOS](https://en.wikipedia.org/wiki/BIOS)——BIOS 是一种最初用于基于 Intel 的 IBM PC 的平台固件技术。它是一种 8086 实模式技术。Intel 曾经表示它们将会在 2020 年结束基于 BIOS 的平台固件的生命周期，代之以 UEFI。Intel 和少数 IBV 拥有闭源的 BIOS 实现。BIOS 曾经是微软 Windows PC 的主要固件技术，直到 Windows 开始强制要求 UEFI
* [SeaBIOS](https://seabios.org)——主要的开源 BIOS 实现
* [coreboot](https://coreboot.org)——coreboot 是一种最初称为 LinuxBIOS 的平台固件技术。它可以加载诸如 SeaBIOS、UEFI 及其他负载，广泛应用于嵌入式系统。coreboot 被用于 Google ChromeOS 系统，并且启用 coreboot 验证启动以获得更多安全性
* [直接内存访问](https://en.wikipedia.org/wiki/Direct_memory_access)——DMA 允许某些硬件子系统，最为明显的是 PCIe 以访问主系统的内存，独立于中央处理器（CPU）。它可以被诸如 PCIleech 等恶意硬件攻击。主要的防护机制是 iommu 硬件和操作系统支持
* [Heads](https://github.com/osresearch/heads)——Heads 是一种平台启动固件，它包括一个作为 coreboot 或者 LinuxBoot ROM 的负载而运行的最小化 Linux 以提供一种安全、灵活的启动环境
* [独立 BIOS 厂商](https://en.wikipedia.org/wiki/BIOS#Vendors_and_products)——独立 BIOS 厂商（IBV）为 OEM/ODM 提供集成式固件解决方案。随着 UEFI 取代 BIOS，某些 IBV 现在改称自己为 IFV（独立固件厂商）。某些 OEM 仍然将其消费者级别的设备固件外包给 IBV，而为其商用级设备制作自己的固件。范例包括：
    * [AMI](https://ami.com)
    * [Insyde](https://www.insyde.com/)
    * [Phoenix](https://www.phoenix.com/)
* [Intel Boot Guard](https://en.wikipedia.org/wiki/Intel_vPro#Intel_Boot_Guard)——Intel Boot Guard 是一种固件安全技术，它在 UEFI 安全启动发生之前帮助保护启动过程。一旦 Boot Guard 被启用，它将不能被禁用，并且将会阻止安装诸如 coreboot 等替代固件
* [JTAG](https://en.wikipedia.org/wiki/JTAG)——JTAG 是芯片的硬件接口以允许访问固件。它被固件工程师用于开发，以及被邪恶女仆攻击者在厂商在其消费者设备中将 JTAG 接口遗留为暴露状态时使用
* [LAVA](https://validation.linaro.org/)——LAVA 是一种自动化的验证架构，主要目的是测试基于 ARM 设备上的 Linux 内核构建的系统的部署，特别是对于 ARMv7 及更新的设备
* [LinuxBoot](https://www.linuxboot.org/)——LinuxBoot 是一种平台固件启动技术，它将诸如 UEFI DXE 阶段的特定固件功能替换为 Linux 内核和运行时
* [管理模式](https://www.uefi.org/sites/default/files/resources/UEFI_Plugfest_March_2016_AMI.pdf)——管理模式是 UEFI 所使用的词语，用以指代 Intel SMM 和 ARM TrustZone，即 CPU 的一种特权执行模式
* 管理系统实现于一块独立的处理器上，并且通常是在专用网络接口上，以有利于带外访问和控制。在诸如 Intel ME 和 AMD PSP 等某些情况下，管理处理器和主 CPU 位于同一块裸晶上。这些系统通常使用一种完全嵌入式的操作系统，诸如 BSD 或者 Linux
* [AMD PSP](https://en.wikipedia.org/wiki/AMD_Platform_Security_Processor)——AMD PSP（平台安全处理器）是 AMD 系统上的一块安全处理器，它可以运行诸如 fTPM 等固件应用程序
* [苹果 T2](https://www.apple.com/imac-pro/)——用于 iMac Pro 的加密存储和安全启动的系统管理控制器、影像信号处理器、固态硬盘控制器和安全飞地（secure enclave）
* [基板管理控制器](https://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface#Baseboard_management_controller)——BMC 是用于管理服务器固件，包括应用更新的接口。OpenBMC 是主要的开源 BMC 实现
* [DASH](http://www.dmtf.org/standards/dash/)——DMTF DASH 是一组用于台式机的带外固件管理规范。Intel AMT 是一种符合 DASH 的实现，AMD SIMFIRE 也是
* [Intel AMT](https://software.intel.com/en-us/articles/developing-for-intel-active-management-technology-amt)——Intel AMT 是 Intel 系统上的一种平台固件管理技术，它作为应用程序运行于 Intel ME 处理器上。AMT 提供诸如远程 KVM、电源控制、裸机操作系统恢复与重建镜像以及远程预警等服务
* [Intel ME](https://en.wikipedia.org/wiki/Intel_Management_Engine)——Intel ME 是 Intel 系统上的一块管理和安全处理器，它可以运行 Intel 主动管理技术（AMT）、高级风扇速度控制、Boot Guard 和安全启动、通过局域网的串口以及基于固件的 TPM（fTPM）。它看似运行一种 MINIX 的变体
* [IPMI](https://www.intel.com/content/www/us/en/servers/ipmi/ipmi-home.html)——IPMI 是一种平台固件管理技术，通常位于 Intel 或者 AMD 的服务器系统上。通常被实现为一种嵌入式的 Linux 系统。尽管广泛使用，IPMI 的现代替代品是 Redfish
* [OpenBMC](https://github.com/openbmc/openbmc)——OpenBMC 项目是一个用于拥有 BMC 的嵌入式设备的 Linux 发行版
* [Redfish](http://dmtf.org/standards/redfish/)——DMTF Redfish 是一种带外固件管理技术，用于取代 IPMI
* [SMASH](http://dmtf.org/standards/smash/)——DMTF SMASH 是一组用户服务器的带外固件管理规范，与 DASH 相似
* [测定启动](https://firmware.intel.com/blog/security-technologies-and-minnowboard-max)——Intel 的技术，使用 TCG TPM 来保护启动过程
* [微码](https://en.wikipedia.org/wiki/Microcode)——微码是一种用于 CPU 的固件形式，系统需要微码更新，如同它们需要平台固件更新以及操作系统更新那样
* [NIST](https://csrc.nist.gov/)——一家为美国政府服务的标准制定实体。它拥有若干关于固件的设计和操作安全性的文档、书籍和培训
* [原始设备制造商](https://en.wikipedia.org/wiki/Original_equipment_manufacturer)——一家 OEM 构建并销售原始硬件
* [原始设计制造商](https://en.wikipedia.org/wiki/Original_design_manufacturer)——一家 ODM 构建硬件并且将其销售给 OEM
* [操作系统厂商](https://en.wikipedia.org/wiki/Operating_system)——OSV 是一家操作系统厂商，它包括固件/操作系统的交互
* [选项 ROM](https://en.wikipedia.org/wiki/Option_ROM)——选项 ROM，又称为扩展 ROM、OpROM、XROM，是一块 PCI/PCIe 设备上的固件 blob。选项 ROM 是来自 BIOS 时代的术语，当时一块板卡将会与 BIOS 平台固件挂钩，并且为新的板卡添加额外功能。选项 ROM 是位于该板卡的闪存中的 BIOS/UEFI 驱动程序。一块板卡可能需要多种驱动程序，分别用于每一种架构以及每一种平台固件类型（BIOS+x86\_64、BIOS+ARM、UEFI+x86\_64、UEFI+ARM 等）。选项 ROM 并不构成这样的设备上的全部固件，由于用于诸如 RAID 或者 TCP 工作量卸载等设备功能的操作固件可能是与之完全分离的
* [PCIe](https://pcisig.com/)——PCIe 是 PC 主板的接口。PCIe 设备的固件包括选项 ROM。此设备可能拥有一块对于系统主板不可见的处理器，难以完全信任 PCIe 硬件
* [安全启动](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#Secure_boot)——安全启动是一个经常与 UEFI 安全启动相关联的词语，后者是 UEFI 的一种可选安全特性，用于帮助防护启动过程，它并不需要 TPM。除了 UEFI 以外，其他固件技术也会使用安全启动这一词语，有时是小写。苹果的基于 EFI 的安全启动实现不同于用于 Windows/Linux 系统的安全启动技术
* [SMM](https://en.wikipedia.org/wiki/System_Management_Mode)——系统管理模式（SMM）是 Intel 和 AMD 系统中的一种处理器模式，区别于实模式和不同的保护模式，它赋予了对于处理器的完全控制权。由 SMM 托管的应用程序，诸如恶意软件，对于通常的基于保护模式的代码不可见
* [SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus)——SPI 是一种用于访问固件的接口。它在开发过程中被厂商使用，并且也可以被攻击者使用，如果它在消费者产品中仍然保持开启状态
* [可信执行环境](https://en.wikipedia.org/wiki/Trusted_execution_environment)——也称为安全执行环境（SEE）。它是虚拟机监视器或者其他技术的一个范例，通过限制固件以使其更加安全。ARM TrustZone 是 SEE 的一个范例
* [雷电](https://www.intel.com/content/www/us/en/io/thunderbolt/thunderbolt-technology-general.html)——由 Intel 和苹果开发的一种外部外设硬件接口，它合并了 PCIe、DisplayPort 和直流电源
* [Tianocore](https://tianocore.org/)——Tianocore 是 UEFI 论坛的开源实现的起源，厂商将其代码同闭源驱动程序以及增值代码一起使用
* [TrustZone](https://www.arm.com/products/security-on-arm/trustzone)——TrustZone（TZ）是用于 ARM 系统的一种固件安全技术，它是一种形式的 TEE/SEE，后者被 UEFI 称为管理模式
* [TPM](http://www.trustedcomputinggroup.org/)——TPM 是众多平台固件实现的可信根，诸如 Intel/AMD 的 BIOS 和 UEFI 系统。TPM 由可信计算小组（Trustworthy Computing Group，TCG）定义。有独立的 TPM 芯片，也有称为 fTPM 的“软”固件 TPM 实现，它们由诸如 Intel ME、AMD PSP 等实现
* [可信启动](https://trustedcomputinggroup.org/trusted-boot/)——可信启动是一种来自可信计算小组的固件安全技术，它使用 TPM 来帮助防护启动过程
* [可信计算小组](http://www.trustedcomputinggroup.org/)——可信计算小组（Trustworthy Computing Group，TCG）是一个业界贸易组织，它控制着 TPM 及其相关规范
* [U-Boot](https://www.denx.de/wiki/U-Boot/)——U-Boot 可以加载诸如 SeaBIOS、UEFI 等其他负载。U-Boot 和 coreboot 广泛应用于嵌入式系统
* [UEFI](https://uefi.org)——UEFI 是一种最初由 Intel 创建，现在被 Intel、AMD、ARM 及其他系统所使用的平台固件技术，它最初是为 Intel Itanium 而设计并且作为 BIOS 的替代品的。UEFI 也是 EFI。基于 UEFI 的平台固件技术通常也称为 BIOS，其中的老旧 BIOS 称为传统模式（Legacy Mode）或者 CSM（兼容性支持模式，Compatibility Support Mode）
* [UEFI DBX](https://www.uefi.org/revocationlistfile)——UEFI DBX UEFI 安全启动黑名单文件包含最新的 UEFI 安全启动 PKI 黑名单/过期密钥。检查您的厂商文档以查看您的系统厂商的工具如何工作以获取并应用此文件到您的系统；如果厂商并未提供工具，请要求它们提供
* [UEFI 论坛](https://uefi.org/)——UEFI 论坛是一个业界贸易组织，它控制着 UEFI 和 ACPI 规范以及 UEFI SCT 测试，并且提供开源的 UEFI 实现 Tianocore
* [USB](http://www.usb.org)——通用串行总线（USB）是一种用于外部外设的业界标准。USB 设备可以被配置为多种设备，并且诸如 Hak5 的 Rubber Ducky 等恶意 USB 硬件可以戏弄天真的操作系统
* [验证启动](https://source.android.com/security/verifiedboot/)——验证启动是一项来自 coreboot 的固件安全技术，它帮助防护启动过程，大致相当于安全启动
* [Android 验证启动](https://source.android.com/security/verifiedboot/)——Android 版本的验证启动
* [ChromeOS 验证启动](https://www.chromium.org/chromium-os/chromiumos-design-docs/verified-boot)——ChromiumOS 和 ChromeOS 版本的验证启动

---

## 威胁

* [BadBIOS](https://en.wikipedia.org/wiki/BadBIOS)——BadBIOS 是由 Dragos 报告的疑似固件恶意软件
* [邪恶女仆攻击](https://theinvisiblethings.blogspot.com/2011/09/anti-evil-maid.html)——邪恶女仆攻击也许是最广为人知的固件攻击。在这里，受害者将其 sstem 置于无人值守状态，并且攻击者拥有一段可以物理访问该系统的时间，以供其安装固件层级的恶意软件。例如，某人外出晚餐时将其笔记本留在酒店客房，而攻击者装扮成酒店客房服务人员
* [Hacking Team 的 UEFI 恶意软件](https://attack.mitre.org/wiki/Software/S0047)——Hacking Team 是一家向政府和其他实体出售漏洞的公司。在它们提供的东西当中有一种面向 Windows PC 的基于 UEFI 的固件攻击。Hacking Team 的恶意软件是为数不多的已知的被 CHIPSEC 列入黑名单的公开 UEFI
* [Fish2 IPMI 安全](http://www.fish2.com/ipmi/)——关于不良和/或不安全的 IPMI 实现的信息编译
* [PCI Leech](https://github.com/ufrisk/pcileech/)——PCILeech 是一种基于 PCI 的恶意硬件，用于攻击系统的 PCI 接口。防御措施是 iommu 配合操作系统的 iommu 支持
* [Rowhammer](https://en.wikipedia.org/wiki/Row_hammer)——Rowhammer 是一种针对系统的新型基于内存的安全攻击。防御方法是 ECC 内存
* [ThinkPwn](https://github.com/Cr4sh/ThinkPwn)——ThinkPwn 是一种最初以 ThinkPad 系统为目标的 UEFI 恶意软件 PoC。ThinkPwn 恶意软件是为数不多的已知的被 CHIPSEC 列入黑名单的公开 UEFI。thinkpwn.efi 包含在 FPMurphy 的 UEFI Utilities 之中。一个恶意软件二进制文件藏在其他有用工具之中，如需使用这些工具则请小心
* [USB Rubber Ducky](https://hakshop.com/products/usb-rubber-ducky-deluxe)——Rubber Ducky 是恶意 USB 硬件的一个范例，它使得使用者去配置系统，以戏弄天真的操作系统，使其认为它是任意数量的设备

---

## 工具

**免责声明**：阅读关于固件的内容是一件事，但是使用这些工具可能是危险的，您可能使您的设备变砖——谨慎操作并且自行承担风险。

### 开源的

**注记**：出于安全性的目的，开源软件是可审计和可验证的。但要注意，处理固件比处理那些安装在硬盘上的您可以删除和重新安装的软件更加危险。您可能使您的系统变砖！谨慎操作并且自行承担风险。

* [ACPICA 工具](https://acpica.org/downloads)——提供工具和 ACPI 的一种参考实现
* [acpidump](https://acpica.org/)——来自 ACPICA 的跨平台、存在于操作系统中的（OS-present）工具以转储并且诊断 ACPI 表
* [BIOS 实现测试套件](https://biosbits.org/)——Intel BIOS 实现测试套件（BITS）提供了一个可启动的预操作系统（pre-OS）环境以测试 BIOS，特别是它们对 Intel 处理器、硬件和技术的初始化。它包括一个编译为原生 BIOS 应用程序的 CPython
* [DarwinDumper](https://bitbucket.org/blackosx/darwindumper)——DarwinDumper 是一个开源项目，它是一系列脚本和工具，以提供一种便捷的方法来快速采集关于您的 OS X 系统的系统概要
* [Eclipse UEFI EDK2 向导插件](https://github.com/ffmmjj/uefi_edk2_wizards_plugin)——此 Eclipse 插件帮助 EDK2 开发者使用带有 CDT 的 Eclipse 集成开发环境以进行 UEFI 开发
* [EFIgy](https://efigy.io)——Duo Security 的 EDIgy 是一个以苹果 Mac 为中心的开源工具，以检查系统是否拥有最新的 EFI 固件
* [Firmadyne](https://github.com/firmadyne/firmadyne)——Firmadyne 是一个自动化的可扩展系统，用于对基于 Linux 的嵌入式固件进行模拟和动态分析
* [Firmware.re](http://firmware.re/)——Firmware.RE 是一个免费的服务，它可以解包、扫描并且分析几乎任何固件包，并且有助于快速监测漏洞、后门和所有类型的嵌入式恶意软件
* [GRUB](https://www.gnu.org/software/grub/)——GRUB 是一种多重启动的引导程序。它被编译为 BIOS 或者 UEFI 应用程序
* [Linux Shim](https://github.com/rhboot/shim)——Shim 是一种 UEFI 引导程序，它会加载另一个 UEFI 引导程序，可能具有不同的许可证，或者由其他厂商签名。有多种已公开的 Shim 分叉
* [Fedora 关于 UEFI 安全启动 Shim 的指南](https://docs-old.fedoraproject.org/en-US/Fedora/18/html/UEFI_Secure_Boot_Guide/sect-UEFI_Secure_Boot_Guide-Implementation_of_UEFI_Secure_Boot-Shim.html)
* [Linux Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt)——Linux 内核可以被如此构建，以使得它同时是 BIOS 和 UEFI 引导程序
* [CHIPSEC](https://github.com/chipsec/chipsec)——CHIPSEC 是一种由 Intel 创建的安全工具，以测试 Intel BIOS/UEFI 的安全状态。它是当前唯一能够检查多种公开的固件安全漏洞的工具
* [eficheck](https://apple.com)——很遗憾，缺少指向它的一个良好的链接，由于此工具仅存于最近版本的 macOS 中，并且没有在 [https://apple.com](https://apple.com) 以文档形式记载。它可以验证 UEFI 完整性和安全性
* [固件测试套件](https://launchpad.net/fwts)——固件测试套件（FWTS）是由 Ubuntu Linux OSV，Canonical 创建的一系列固件测试工具，以帮助测试系统中将会导致 Ubuntu 出现问题的缺陷。FWTS 是用于多种技术的数十种测试的套件。UEFI 论坛推荐 FWTS 作为主要的 ACPI 测试资源。FWTS 是一个用于 Linux 的命令行工具，并且包括可选的 CURSES UI 以及可选的 FWTS-live live 启动发行版。FWTS 包含在 Intel 的 LUV Linux 发行版中
* [FlashROM](https://flashrom.org/Flashrom)——FlashROM 是一个以 Linux/BSD 为中心的工具，用于识别、读取、写入、验证和擦除闪存芯片。它被设计为烧录主板、网卡、显卡、存储控制器其他不同编程设备上的 BIOS/EFI/coreboot/固件/选项 ROM 镜像等。有对于 Windows 的部分支持
* [黄金镜像](https://en.wikipedia.org/wiki/System_image)——黄金镜像是厂商的原始固件二进制文件。这一词语也被用于操作系统镜像。更好的厂商提供镜像和工具以便将使用过的硬件或是购自灰色市场的硬件重置为一种已知状态。在信任任何下载到的二进制文件，诸如黄金镜像之前，它应该同散列值进行比对。大多数厂商并不提供它们的镜像的散列值
* [Linux UEFI Validation](https://01.org/linux-uefi-validation)——LUV 是一种由 Intel 创建的 Linux 发行版以测试 OEM 的 UEFI 实现。它捆绑了 CHIPSEC、FWTS 及其他固件测试。LUV 可通过 LUV-live 的二进制形式获得，这是一个 live 启动的发行版
* [Linux 厂商固件服务](https://fwupd.org/)——也称为 LVFS 或者 fwupd，是一种用于 Linux OEM 的固件更新服务，它极好地提供了一种标准化的系统。使用它的 OEM 正在严肃地对待 Linux 的兼容性和安全性。在微软 Windows 上，一种类似的机制通过 Windows Update 来工作
* [微软 Windows Update](https://en.wikipedia.org/wiki/Windows_Update)——令人惊讶的是——Windows Update 是极好的！除了提供操作系统软件层级的更新以外，Windows Update 还可以通过标准化的胶囊提供固件更新。这些更新必须被固件/硬件厂商验证，并且可以被 EV 签名
* [Pawn](https://github.com/google/pawn)——Google Pawn 是一种以 Linux 为中心的在线固件工具，它可以将平台固件镜像转储为文件，以供以后进行离线分析
* [PhoenixTool](https://forums.mydigitallife.net/threads/13194/)——PhoenixTool 是一种第三方免费软件以操作（U）EFI 和少数基于传统 BIOS 的固件 blob
* [rEFInd](http://www.rodsbooks.com/refind/)——rEFInd 是 rEFIt 的继任者，一种允许您选择多种操作系统的 UEFI 引导程序
* [RU.EFI](https://github.com/JamesAmiTw/ru-uefi/)——RU.EFI 是一种拥有多种功能的第三方免费固件工具，它以类似 MS-DOS 或者 UEFI Shell 工具的方式工作
* [RWEverything](http://rweverything.com/)——RWEverything（RWE）是一种拥有多种功能的第三方免费固件工具。此工具工作在 Windows 上。如果 CHIPSEC 的 Windows 内核驱动程序未被加载，则 CHIPSEC 工具可以使用 RWE 内核驱动程序
* [Sandsifter](https://github.com/xoreaxeaxeax/sandsifter)——Sandsifter 是一种 x86 模糊测试工具
* [UEFI Utilities](https://github.com/fpmurphy/UEFI-Utilities-2018)——UEFI Utilities 是一系列 UEFI Shell 工具的集合，以提供系统诊断信息（它也包含一份 ThinkPwn.efi 副本，当心）
* [UEFI 固件语法解释器](https://github.com/theopolis/uefi-firmware-parser)——UEFI 固件语法解释器检查固件 blob，主要是 UEFI 的固件 blob
* [UEFITool](https://github.com/LongSoft/UEFITool)——UEFITool 是一种对固件 blob 进行语法检查的图形用户界面程序，主要是对于 UEFI 固件 blob。除了 UEFITool Qt 图形用户界面工具以外，UEFITool 源代码项目也包括若干非图形用户界面的命令行工具，包括 UEFIDump。注意，UEFITool 拥有两棵源代码树，master 和新引擎
* [Visual UEFI](https://github.com/ionescu007/VisualUefi)——Visual UEFI 是 Visual Studio 的一种插件，使得 Visual Studio 用户能够进行 UEFI EDK2 开发而无需知道 EDK2 的构建过程细节，而这种构建过程与 Visual Studio 并不相似
* [zenfish IPMI 工具](https://github.com/zenfish/ipmi)——由 SATAN fame 的 Dan Farmer 提供的 IPMI 安全测试工具

### 闭源的

**特别注记**：闭源软件是不可审计的，也不是可验证地安全的。恶意软件存在的风险较高，而对于固件，使您的系统变砖的风险总是存在。可能有潜在地“良好”的工具，但是这个列表并不成为使用建议。谨慎操作并且自行承担风险。

## 文档、书籍和培训

* [Beyond BIOS](https://www.degruyter.com/view/product/484468)——Beyond BIOS: Developing with the Unified Extensible Firmware Interface（超越 BIOS：利用统一可扩展固件接口进行开发），第三版，这是由 Intel 和其他 UEFI 论坛成员创作的关于 UEFI 的书籍。最初由 Intel 出版社出版
* [Darkreading Firmware Security Tips](https://www.darkreading.com/iot/5-tips-for-protecting-firmware-from-attacks/d/d-id/1325604)——这篇含有来自 Intel 的 CHIPSEC 团队的输入内容的文章给出了对于固件安全的基本高级指南。从这篇文章开始，然后再深入研究 NIST 文档
* [Firmware Security Blog](https://firmwaresecurity.com)——关于固件安全和开发的新闻和信息的开源，其关注焦点是以 UEFI 为中心的平台固件（**免责声明**：awesome-firmware 的作者之一，以及 PreOS Security 的雇员之一是此 Firmware Security 博主）
* [Firmware Security Twitter List](https://twitter.com/JacobTorrey/lists/firmware-security)——Jacob Torrey 在 Twitter 上托管此列表，它包含众多核心固件安全研究人员
* [Hardware Security Training](https://hardwaresecurity.training/)——Hardware Security Training 公司是多种硬件/固件安全培训人员的集合
* [Harnessing the UEFI Shell](https://www.degruyter.com/view/product/484477)——Harnessing the UEFI Shell: Moving Platform Beyond DOS（治理 UEFI Shell：推进平台超越 DOS），第二版，由 Intel 及其他 UEFI 论坛成员创作的关于 UEFI 的书籍，最初由 Intel 出版社出版
* [Intel Security Training](https://github.com/advanced-threat-research/firmware-security-training)——由位于 Intel Security 的 Intel 高级威胁研究（ATR）团队的 CHIPSEC 团队提供的培训。其文档是关于 Intel 硬件/固件安全威胁的信息的极好的来源，其关注焦点为 UEFI 及其相关技术
* [IPMI Security Best Practices](http://www.fish2.com/ipmi/bp.pdf)——来自 Dan Farmer 的 IPMI 最佳安全实践。它需要更新。其大部分内容也可适用于 Redfish 或者任何 OOB 管理技术
* [Linux Foundation Workstation Security](https://github.com/lfit/itpol)——Linux 基金会拥有一系列用于 Linux 系统的 IT 策略，它包括某些固件安全指南
* [Linux on UEFI](http://www.rodsbooks.com/linux-uefi/)——Linux on UEFI Roderick W. Smith 拥有一部带有关于 UEFI 和 Linux 的信息的在线书籍，展示了如何使用多种引导程序
* [Low Level PC Attack Papers](http://www.timeglider.com/timeline/5ca2daa6078caaf4)——关于硬件/固件安全研究的极好的时间表
* [NIST](https://csrc.nist.gov/)——固件指南文档。它们是极好的。从 SP 800-193 开始
    * [SP 800-147](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-147.pdf)：一部比较老旧的文档，它主要面向 BIOS
    * [SP 800-147b](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-147B.pdf)：对 SP 800-147 的补充，特别针对服务器
    * [SP 800-155](https://csrc.nist.gov/csrc/media/publications/sp/800-155/draft/documents/draft-sp800-155_dec2011.pdf)：注意，此文档仍处于草案状态，但已经非常可用
    * [SP 800-193](https://csrc.nist.gov/CSRC/media/Publications/sp/800-193/draft/documents/sp800-193-draft.pdf)：注意，此文档仍处于草案状态，但已经非常可用，并且是所有文档当中最新的。从这里开始
* [NSA Common Criteria for PC BIOS Protection](https://www.niap-ccevs.org/Profile/Info.cfm?PPID=306&id=306)——这是关于 PC 固件的标准保护概要（PP）的 2013 年的通用判据。它解决了这样一种主要威胁：一位对手将会更改或者替换一台 PC 客户端设备的 BIOS 并且以一种持久的方式攻击 PC 客户端环境。并没有任何固件解决方案能够满足此概要，但是对此威胁模型的解读是有用的知识背景
* [One-Stop Shop for UEFI Links](https://github.com/uefitech/resources/blob/master/README.md)——由 UEFI 技术社区维护的关于 UEFI/BIOS 规范和工具的一站式解决方案
* [Open Security Training Intro to BIOS & SMM](http://opensecuritytraining.info/IntroBIOS.html)——关于 BIOS 和 SMM 的课程材料的介绍
* [Rootkits and Bootkits](https://nostarch.com/rootkits)——这是当时唯一关于固件安全性的书籍，由固件安全专家编写

