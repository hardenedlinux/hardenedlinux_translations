# 附录 A——要求的总结

此附录包含了关于第 3 章中的系统 BIOS 实现的安全 BIOS 更新指导意见的总结。这些指导意见的本意是用于平台厂商设计、实现或者选择一种系统 BIOS 实现。读者应该查询此文档正文中的相关章节以获得深入描述这些指导意见的目的和上下文环境的额外的信息性文字。

## 1. BIOS 更新认证

* 1-A 认证 BIOS 更新机制应该被实现在 RTU 中（参见 2.5 节）
* 1-B RTU 的验证组件应该包含数字签名验证算法和一个密钥存储器。此密钥存储器应该包含用于验证 BIOS 更新镜像的签名的公钥或者该密钥的一种许可的密码学散列值 \[FIPS180-4\]，在后一种情况下，更新机制应该计算由 BIOS 更新镜像提供的公钥的散列值并且确保它与出现在密钥存储器中的某个散列值相匹配，然后才能使用提供的公钥来验证 BIOS 更新镜像的签名
* 1-C BIOS 镜像应该以符合 NIST SP800-89，关于获得数字签名应用程序的担保的建议 \[SP800-89\] 的方式签名，使用一种在 NIST FIPS186-4，数字签名标准 \[FIPS186-4\] 中具体说明的数字签名算法，它提供至少 112 位的安全强度，以符合 NIST SP800-131A，过渡：关于密码学算法和密钥长度的使用的过渡的建议 \[SP800-131A\] 的要求
* 1-D 认证更新机制应该确保 BIOS 更新镜像经过数字签名，并且该数字签名可以在更新 BIOS 之前使用某个已存储的密钥或者由 RTU 验证
* 1-E 恢复机制也应该使用认证更新机制，除非此恢复过程满足安全本地更新的指导意见
* 1-F 系统应该提供能够防止非授权地将 BIOS 更改至某个较早的认证版本的机制。

## 2. 安全本地更新（可选）

服务器可以可选地包括一种安全本地更新机制，在此，由物理存在授权 BIOS 更新镜像的安装，而无需使用认证更新机制。

* 2-A 安全本地更新机制应该通过要求管理员物理接触服务器本身以指导更新的方式来授权和认证 BIOS 更新镜像。

## 3. 完整性保护

* 3-A 在系统 BIOS 由 RTU 验证和启动过程中系统 BIOS 被执行之间，系统 BIOS 的完整性应该得到维持
* 3-B 包含 BIOS 的系统闪存存储器，除了存储于非易失性存储器中的由系统 BIOS 使用的配置数据以外，应该被保护以防止认证 BIOS 更新机制以外的修改
    * 3-B.i 如果被实施，BIOS 闪存保护应该先于执行 RTU 以外的代码被启用
    * 3-B.ii 如果被实施，BIOS 闪存保护应该只能通过某种授权的机制（例如系统重置）禁用的硬件机制来强制执行
* 3-C 如果 BIOS 闪存保护未被实施，则 BIOS 完整性应该先于每次执行被验证，利用 RTU 的验证组件来认证 BIOS 镜像
    * 3-C.i 如果验证失败，则系统应该引发恢复过程
    * 3-C.ii 引发恢复到某个受保护的合法的 BIOS 的自动恢复机制应该被支持
* 3-D 每个 RTU 都应该被保护起来以防止认证更新机制以外的修改
    * 3-D.i 确保 RTU 完整性的保护机制应该先于执行 RTU 以外的代码被启用
    * 3-D.ii RTU 完整性保护应该由只能通过授权的机制，例如系统重置来禁用的硬件机制强制执行

## 4. 不可绕过性

* 4-A 系统及其附带的系统组件和固件的设计应该保证没有任何机制可以安装并执行非法 BIOS 代码，除了通过物理介入以及安全本地更新机制以外
* 4-B 认证 BIOS 更新机制应该是在没有贯穿于安全本地更新机制的物理介入的情况下修改 RTU 的唯一机制
* 4-C 系统及其附带的系统组件和固件的设计应该保证没有任何机制可以允许宿主处理器或者任何其他系统组件绕过认证更新机制来更新 RTU，除了安全本地更新机制以外
* 4-D 尽管某个系统组件可能拥有对于系统闪存存储器的读取访问权限，它不应该能够直接修改 RTU，除非该组件被用作 RTU 本身。

## 5. 服务处理器

* 5-A 用作可信根以保护 BIOS 的服务处理器应该满足下列要求：
    * 5-A.i 针对 SP 代码、密码学密钥以及存储于 SP 闪存存储器中的静态数据的更新应该通过认证更新机制实现
    * 5-A.ii SP 环境应该被控制，以使得只有合法代码可以在 SP 上执行
    * 5-A.iii 用户同 SP 的交互应该要求授权
* 5-B 不用作可信根以保护 BIOS 的服务处理器应该满足下列要求：
    * 5-B.i SP 不应该拥有对于 BIOS 代码在其中验证或者执行的 BIOS 闪存存储器的直接写入访问权限
    * 5-B.ii SP 应该受到限制，使得它不能干涉 BIOS 更新过程，也不能干涉 BIOS 或者 RTU 代码在其中执行的内存

# 附录 B——更新机制 1 范例

此附录提供了关于更新机制 1 可以如何在一台服务器上实现的一个范例。更新机制 1 包括服务器运行时的认证 BIOS 更新。在此范例中，运行时 BIOS 更新由服务处理器（SP）执行。图 1：此范例的系统框图展示了 BIOS 闪存 SPI 控制器可被宿主和 SP 访问。宿主到 SPI 控制器的路径上可能需要额外的逻辑以防止宿主对 BIOS 闪存存储器的写入访问。此逻辑可以是芯片组内部的寄存器，也可以位于芯片组外部。由于它拥有对于系统闪存的写入访问权限，此范例中的 SP 环境必须是一种安全的、受保护的环境，如第 5 章所述。

> 图 1：更新机制 1 系统框图范例

在此范例中，系统 BIOS 在系统重置时被赋予对宿主 CPU 的控制权。所有 SPI 闪存部分在系统重置时被解锁。系统 BIOS 先于允许执行非可信代码（例如 Option ROM、引导程序）锁定宿主侧对于包含系统 BIOS 的系统闪存部分的写入访问权限。这种锁定是通过同逻辑的交互而实现的，以便将包含 BIOS 镜像的区域“锁定直到重置”。当此锁定被设置时，对此锁定寄存器的访问变为只读，以使得“锁定直到重置”的设置本身不能被修改。对于 BIOS 闪存部分的写入访问权限对于 SP 仍然可用。

当指导 BIOS 更新时，宿主上的系统管理软件可以同 SP 进行交互以便将某个候选更新镜像发送至 SP。或者，BIOS 更新镜像可以经过 SP 以太网通过带外通讯的方式到达 SP。SP，作为系统 BIOS 的 RTU，利用 SP 上的数字签名验证算法和密钥来验证 BIOS 更新镜像。如果此镜像合法，则即使是在宿主操作系统重启之后对 BIOS 闪存存储器仍然具有写入访问权限的 SP 可以通过同 BIOS 闪存存储器的 SPI 控制器进行交互而执行闪存更新。

# 附录 C——更新机制 2 范例

此附录提供了关于更新机制 2 可以如何在一台服务器上实现的一个范例。在此范例中，BIOS 更新镜像在启动过程中被验证和刷入，此时被实现为 BIOS 的一部分的 RTU 拥有对系统的控制权。图 2 展示了使用此种更新机制的服务器的一种系统框图范例。BIOS 闪存 SPI 控制器仅可由宿主访问。潜在的 BIOS 更新镜像存储于 SP 环境中。

> 图 2：更新机制 2 系统框图范例

在此范例中，如需引发 BIOS 更新，宿主上的系统管理软件可以同 SP 进行交互以发送 BIOS 更新镜像，使其存储于 SP 环境中用于之后 BIOS 的访问。或者，候选 BIOS 更新镜像可以经过 SP 以太网通过带外通讯的方式到达 SP。

被实现为系统 BIOS 的一部分的 RTU 在系统重置时获得宿主侧的控制权。所有 SPI 闪存部分在系统重置时被解锁。在系统闪存内部，RTU 并未与系统 BIOS 的剩余部分相分离，在执行非可信代码（例如 Option ROM）之前，系统 BIOS 就是 RTU。它与 SP 进行通讯以查找候选 BIOS 更新镜像。如果存在，它从 SP 中读取到宿主内存中（它在 RTU 执行期间仅可由系统 BIOS 写入）并且进行验证。如果此 BIOS 更新镜像合法，系统 BIOS 通过同 SPI 闪存控制器的交互来执行系统闪存更新。当 BIOS 更新结束时，系统 BIOS 强制系统重置并且重新启动以便从新的镜像执行。

如果 SP 指示候选 BIOS 更新镜像不存在，或者候选 BIOS 更新镜像验证失败，BIOS 通过同 SPI 控制器交互以便将包含 BIOS 镜像的区域“锁定直到重置”来锁定 BIOS 闪存存储器。当此锁定被设置时，对此 SPI 部分的锁定寄存器的访问变为只读，以使得“锁定直到重置”的设置本身不能被修改。此区域的锁定先于退出 BIOS 的 RTU 部分完成。

# 附录 D——更新机制 3 范例

此附录提供了关于更新机制 3 可以如何在一台服务器上实现的一个范例。在此范例中，BIOS 闪存并未被强有力地保护，因此 BIOS 代码的完整性在启动过程中被验证。更新机制 3 的系统框图范例展示了 BIOS 闪存 SPI 控制器可由宿主和 SP 访问。由于它拥有对于 BIOS 闪存存储器的写入访问权限，此范例中的 SP 环境必须是安全、受保护的环境，如第 5 章所述。

> 图 3：更新机制 3 系统框图范例

在此范例中，如需引发 BIOS 更新，宿主上的系统管理软件可以同 SP 交互以便将 BIOS 更新镜像发送到 SP。或者，BIOS 更新镜像可以经过 SP 以太网通过带外通讯的方式到达 SP。然后，作为 RTU 的一部分的 SP 认证此 BIOS 更新镜像。如果此镜像合法，即使在宿主操作系统启动以后对于系统闪存仍然拥有写入访问权限的 SP 可以通过同系统闪存的 SPI 控制器进行交互以执行闪存更新。

在此范例中，系统 BIOS 包含它自身的 RTU 验证组件，它用于在每次启动时认证系统 BIOS 的剩余部分。此验证组件驻留于系统闪存中，并且出于描述此更新机制的目的，它将被标记为 RTU-V。此 RTU-V 在系统重置时被赋予对于宿主侧的控制权。系统重置同时也会解锁全部 SPI 闪存部分。在系统闪存内部，RTU-V 是可以独立于系统 BIOS 的剩余部分而被锁定的。RTU-V 也可以按照如下所述被更新：类似于更新机制范例 2,RTU-V 更新发生于重启时，并且由 RTU-V 本身来更新。它同 SP 通讯以查询候选 RTU-V 更新镜像。如果存在，则它从 SP 读入到宿主内存中并且进行认证。如果此镜像通过认证，则由 RTU-V 通过同 SPI 闪存控制器的交互来进行 BIOS 闪存 ROM 的 RTU-V 部分的更新。当 RTU-V 更新结束时，RTU-V 强制系统重置并且重新启动以便从新的镜像执行。

如果 SP 指示候选 RTU-V 更新镜像不存在，或者候选 RTU-V 更新镜像验证失败，则 RTU-V 通过同 SPI 控制器进行交互将闪存的 RTU-V 区域锁定直到重置。当此锁定被设置时，对此 SPI 区域的锁定寄存器的访问变为只读，使得“锁定直到重置”的设置本身不能被修改。此区域的锁定先于退出 RTU-V（例如，在执行 BIOS 的剩余部分之前）完成。

由于系统闪存区域包含不可锁定的 BIOS 代码，并且会受到恶意代码的修改，因此由 RTU-V 认证系统 BIOS 的剩余部分。系统 BIOS 的剩余部分保存于系统闪存中的独立闪存区域中。如果认证通过，RTU-V 将控制权传递给系统 BIOS 的剩余部分。在此范例中，系统 BIOS 的剩余部分不会锁定包含系统 BIOS 剩余部分的闪存区域。不锁定此闪存区域的可能的原因之一是在运行时简化 BIOS RTU 对此区域的访问。另一种可能的原因是这些区域中的一部分需要在运行时可写入，而区域锁定的粒度不足以保证在锁定 BIOS 的同时不会同时锁定需要可写入的区域。

如果 BIOS 认证失败，它不会被执行。与之相反，RTU-V 同 SP 上的 BIOS RTU 进行通讯以告知认证失败。然后 SP 必须访问之前存储于 SP 环境中的一份合法 BIOS 镜像（可能来自先前的认证 BIOS 更新），认证它并且执行闪存更新。然后 SP 强制系统重置以重新启动 RTU-V，它将于其后认证并执行系统 BIOS 的剩余部分。

# 附录 E——用语

此出版物中使用的选定的词语定义如下：

* **基本输入/输出系统（BIOS）**：总体地用于指代基于传统 BIOS、可扩展固件接口（EFI）和统一可扩展固件接口（UEFI）的启动固件。
* **传统 BIOS**：用于众多 x86 兼容计算机系统的老旧启动固件，也称为遗产 BIOS。
* **可扩展固件接口（EFI）**：关于操作系统和平台固件之间的接口规范。1.10 版本是 EFI 规范的最终版本，由统一可扩展固件接口论坛制定的后续修订版本属于 UEFI 规范的一部分。
* **固件**：包含在只读存储器（ROM）中的软件。
* **Option ROM**：由系统 BIOS 调用的固件。Option ROM 包含扩展卡（例如显卡、硬盘控制器、网卡等）上的 BIOS 固件以及用于扩展系统 BIOS 功能的模块。
* **系统管理模式（SMM）**：见于 x86 兼容处理器的一种高权限操作模式，用于低级系统管理功能。系统管理模式仅可在系统生成系统管理中断时进入，并且仅可执行来自隔离的内存块中的代码。
* **系统闪存存储器**：系统 BIOS 所在的非易失性闪存，通常是主板上的电可擦除可编程只读控制器（EEPROM）闪存存储器。尽管系统闪存存储器是一个技术具体的词语，此文档中的指导意见本意是将系统闪存存储器应用于指代包含系统 BIOS 的任意非易失性存储介质。
* **可信平台模块（TPM）**：构建于某些计算机主板中的防破坏集成电路，它可以执行密码学操作（包括密钥生成）以及保护少量敏感信息，诸如口令和密码学密钥。
* **统一可扩展固件接口（UEFI）**：正在广泛部署到新的基于 x86 的计算机系统上的针对传统 BIOS 的可能的替代品。UEFI 规范继承自 EFI 规范。

# 附录 F——首字母缩略词和缩略语

此附录包含此指南中使用的一组选定的首字母缩略词和缩略语。

* ACPI：高级配置与电源接口
* BIOS：基本输入/输出系统
* CPU：中央处理器
* EEPROM：电可擦除可编程只读存储器
* EFI：可扩展固件接口
* FIPS：美国联邦信息处理标准
* FISMA：美国联邦信息安全管理法案
* GPIO：通用目的输入/输出
* I2C：集成电路总线
* IO：输入/输出
* IT：信息科技
* ITL：信息科技实验室
* LAN：局域网
* LPC：低针数总线
* NIST：美国国家标准技术研究所
* OEM：原始设备制造商
* OMB：美国行政管理和预算局
* OS：操作系统
* PC：个人计算机
* PCI：外设元件互联标准
* ROM：只读存储器
* RTU：更新可信根
* RTU-V：更新可信根的验证组件
* SMI：系统管理中断
* SMM：系统管理模式
* SP：服务处理器
* SP：特别出版
* TPM：可信平台模块
* UEFI：统一可扩展固件接口
* USB：通用串行总线

# 附录 G——参考文献

* \[DuGr09\] Loïc Duflot, Olivier Grumelard, Olivier Levillain and Benjamin Morin. “ACPI and SMI handlers: some limits to trusted computing.” _Journal in Computer Virology_. Volume 6, Number 4, 353-374.
* \[EFI\] _EFI 1.10 Specification_. Intel. 1 November 2003. [http://www.intel.com/technology/efi/](http://www.intel.com/technology/efi/)
* \[EmSp08\] Shawn Embleton, Sherri Sparks, and Cliff C. Zou. "SMM Rootkits: A New Breed of OS Independent Malware," _Proceedings of 4th International Conference on Security and Privacy in Communication Networks_ \(_SecureComm_\), Istanbul, Turkey, September 22-25, 2008.
* \[FIPS180-4\] FIPS 180-4, _Secure Hash Standard_. March 2012.
* \[FIPS186-4\] FIPS 186-4, _Digital Signature Standard_. July 2013.
* \[Graw09\] D. Grawrock. _Dynamics of a Trusted Platform: A Building Block Approach_. Hillsboro, OR: Intel Press, 2009.
* \[Heas07a\] J. Heasman. “Firmware Rootkits: A Threat to the Enterprise.” _Black Hat DC_. Washington, DC. 28 February 2007. [http://www.nccgroup.com/Libraries/Document_Downloads/02_07_Firmware_Rootkits_The_Threat_to_the_Enterprise_Black_Hat_Washington_2007_sflb.sflb.ashx](http://www.nccgroup.com/Libraries/Document_Downloads/02_07_Firmware_Rootkits_The_Threat_to_the_Enterprise_Black_Hat_Washington_2007_sflb.sflb.ashx)
* \[Heas07b\] J. Heasman. “Hacking the Extensible Firmware Interface.” _Black Hat USA_. Las Vegas, NV. 2 August 2007. [https://www.blackhat.com/presentations/bh-usa-07/Heasman/Presentation/bh-usa-07-heasman.pdf](https://www.blackhat.com/presentations/bh-usa-07/Heasman/Presentation/bh-usa-07-heasman.pdf)
* \[Intel03\] _Intel Platform Innovation Framework for EFI- Architecture Specification v0.9_. Intel. September 2003. [http://www.intel.com/technology/framework/](http://www.intel.com/technology/framework/)
* \[KGH09\] A. Kumar, G. Purushottam, and Y. Saint-Hilaire. _Active Platform Management Demystified_. Hillsboro, OR: Intel Press, 2009.
* \[Sal07\] Salihun, Darmawan. _BIOS Disassembly Ninjutsu Uncovered_. Wayne, PA: A-LIST, 2007.
* \[SaOr09\] A. Sacco, A. Ortéga. “Persistant BIOS Infection.” _Phrack_. Issue 66. 6 November 2009. [http://www.phrack.com/issues.html?issue=66&id=7](http://www.phrack.com/issues.html?issue=66&id=7)
* \[SP800-57\] NIST SP 800-57 Part 1, _Recommendation for Key Management – Part 1: General_ \(_Revision 3_\). July 2012.
* \[SP800-89\] NIST SP 800-89, _Recommendation for Obtaining Assurances for Digital Signature Applications_. November 2006.
* \[SP800-131A\] NIST SP 800-131A, _Transitions: Recommendation for Transitioning the Use of Cryptographic Algorithms and Key Lengths_. January 2011.
* \[Sym02\] _W95.CIH Technical Details_. Symantec. 25 April 2002. [http://www.symantec.com/security_response/writeup.jsp?docid=2000-122010-2655-99](http://www.symantec.com/security_response/writeup.jsp?docid=2000-122010-2655-99)
* \[TCG05\] _PC Client Work Group Specific Implementation Specification for Conventional Bios Specification, Version 1.2_. Trusted Computing Group. July 2005. [http://www.trustedcomputinggroup.org/resources/pc_client_work_group_specific_implementation_specification_for_conventional_bios_specification_version_12](http://www.trustedcomputinggroup.org/resources/pc_client_work_group_specific_implementation_specification_for_conventional_bios_specification_version_12)
* \[UEFI\] _UEFI Specification Version 2.3_. Unified EFI Forum. May 2009. [http://www.uefi.org/specs/](http://www.uefi.org/specs/)
* \[Wech09\] F. Wecherowski. “A Real SMM Rootkit: Reversing and Hooking BIOS SMI Handlers.” _Phrack_. Issue 66. 6 November 2009. [http://www.phrack.com/issues.html?issue=66&id=11](http://www.phrack.com/issues.html?issue=66&id=11)
* \[WoTe09\] R. Wojtczuk and A. Tereshkin. “Attacking Intel BIOS.” _Black Hat USA_. Las Vegas, NV. 30 July 2009. [http://www.blackhat.com/presentations/bh-usa-09/WOJTCZUK/BHUSA09-Wojtczuk-AtkIntelBios-SLIDES.pdf](http://www.blackhat.com/presentations/bh-usa-09/WOJTCZUK/BHUSA09-Wojtczuk-AtkIntelBios-SLIDES.pdf)

