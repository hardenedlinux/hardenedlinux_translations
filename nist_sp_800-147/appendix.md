# 附录 A 系统 BIOS 实现指导意见总结

此附录包含了可在 3.1 节找到的用于系统 BIOS 实现的安全 BIOS 更新指导意见的总结。这些指导意见本意是用于平台厂商设计、实现或者选择一种系统 BIOS 实现。读者应该查询此文档正文中的相关章节以获取那些深入描述此指导意见的目的和上下文的更多信息性的文字。

## 1. 许可的 BIOS 更新机制

* 1-A 所有系统 BIOS 更新应该使用 3.1.1 节描述的认证更新机制，或者符合 3.1.2 节所述指导意见的可选安全本地更新机制。

## 2. BIOS 更新认证

* 2-A 应该有一个更新可信根（RTU），它包含一种签名验证算法以及一个包含用于验证 BIOS 更新镜像的签名的公钥的密钥存储器。
* 2-B 密钥存储器和签名验证算法应该以一种受保护的方式存储于计算机系统上，并且仅可使用认证更新机制或者 3.1.2 节所述的安全本地更新机制来修改。
* 2-C RTU 中的密钥存储器应该包含用于验证 BIOS 更新镜像的签名的公钥或者用于验证包含公钥的 BIOS 更新镜像的公钥的散列值 \[FIPS180-3\]。在后一种情况下，更新机制应该保证由 BIOS 更新镜像提供的公钥的散列值出现在密钥存储器中，然后才能使用提供的公钥来验证 BIOS 更新镜像的签名。
* 2-D BIOS 更新镜像应该以符合 NIST SP 800-89，_Recommendation for Obtaining Assurances for Digital Signature Applications_（关于获得数字签名应用程序的担保的建议）\[SP800-89\] 的方式来签名，使用一种在 NIST FIPS 186-3，_Digital Signature Standard_（数字签名标准）\[FIPS186-3\] 中具体说明的经过许可的数字签名算法，它提供至少 112 位的安全强度，以符合 NIST SP 800-131A，_Transitions: Recommendation for Transitioning the Use of Cryptographic Algorithms and Key Lengths_（过渡：关于密码学算法和密钥长度的使用的过渡的建议）\[SP800-131A\] 的要求。
* 2-E 认证更新机制应该保证 BIOS 更新镜像经过数字签名，并且该数字签名可以在更新 BIOS 之前利用 RTU 中的密钥存储器中的密钥之一来验证。

## 3. 安全本地更新（可选）

BIOS 实现可以可选地包括一种安全本地更新机制，在此，由物理存在来认证 BIOS 更新镜像的安装，而无需使用认证更新机制。

* 3-A 安全本地更新机制应该通过要求物理存在来保证 BIOS 更新镜像的合法性和完整性。

## 4. 完整性保护

* 4-A RTU 和 BIOS（除了存储于非易失性存储器中的被 BIOS 使用的配置数据）应该被保护以防止无意或者恶意的修改，使用一种在认证 BIOS 更新机制以外不能被超越的机制。
* 4-B 保护机制应该被保护以防止非授权的修改。
* 4-C 认证 BIOS 更新机制应该被保护以防止无意或者恶意的修改，利用一种至少和保护 RTU 和系统 BIOS 的机制一样强的机制。
* 4-D 保护机制应该先于执行那些无需使用认证更新机制或者安全本地更新机制就能修改的固件和软件保护包含系统 BIOS 的系统闪存的相关区域。
* 4-E 保护应该由除了通过认证机制以外不可更改的硬件机制来强制执行。

## 5. 不可绕过性

这些不可绕过性的指导意见不适用于存储于非易失性存储器中的由系统 BIOS 所使用的配置数据。

* 5-A 认证 BIOS 更新机制应该是在没有贯穿于安全本地更新机制的物理介入的情况下更新系统 BIOS 的唯一机制。
* 5-B 系统及其附带的系统组件和固件的设计应该保证没有任何机制可以允许系统处理器或者任何其他系统组件绕过认证更新机制，除了安全本地更新机制以外。
* 5-C 尽管系统组件可能拥有对 BIOS 闪存的读取访问权限，它们不应该能够直接修改系统 BIOS，除了通过认证更新机制或者利用某种要求物理介入的认证机制以外。
    * 5-C.i 能够绕过主处理器的总线控制（例如，对于系统闪存的直接内存访问）不应该能够直接修改固件。

系统中的微控制器不应该能够直接修改固件，除非微控制器的硬件和固件组件使用和 RTU 相同的机制被保护。

# 附录 B 术语

此出版物中使用的部分选定的术语定义见下文。

* **基本输入/输出系统（BIOS）**：在此出版物中，总体地用于指代基于传统 BIOS、可扩展固件接口（EFI）和统一可扩展固件接口（UEFI）的启动固件。
* **传统 BIOS**：用于众多 x86 兼容计算机系统的老旧启动固件，也称为遗产 BIOS。
* **用于测定的核心可信根（CRTM）**：在启动过程中，主处理器上所执行的第一段 BIOS 代码。在一台具有可信平台模块的系统上，CRTM 被隐含地信任，以自举该计算机系统上所执行的其他固件和软件的后续认证的测定链的构建过程。
* **可扩展固件接口（EFI）**：关于操作系统和平台固件之间的接口规范。1.10 版本是 EFI 规范的最终版本，由统一可扩展固件接口论坛制定的后续修订版本属于 UEFI 规范的一部分。
* **固件**：包含在只读存储器（ROM）中的软件。
* **Option ROM**：由系统 BIOS 调用的固件。Option ROM 包含扩展卡（例如显卡、硬盘控制器、网卡等）上的 BIOS 固件以及用于扩展系统 BIOS 功能的模块。
* **保护模式**：见于 x86 兼容处理器的一种操作模式，具有内存保护、虚拟内存和多任务的硬件支持。
* **实模式**：见于 x86 兼容处理器的一种老旧的高权限操作模式。
* **系统管理模式（SMM）**：见于 x86 兼容处理器的一种高权限操作模式，用于低级系统管理功能。系统管理模式仅可在系统生成系统管理中断时进入，并且仅可执行来自隔离的内存块中的代码。
* **系统闪存存储器**：系统 BIOS 所在的非易失性闪存，通常是主板上的电可擦除可编程只读控制器（EEPROM）闪存存储器。尽管系统闪存存储器是一个技术具体的词语，此文档中的指导意见本意是将系统闪存存储器应用于指代包含系统 BIOS 的任意非易失性存储介质。
* **可信平台模块（TPM）**：构建于某些计算机主板中的防破坏集成电路，它可以执行密码学操作（包括密钥生成）以及保护少量敏感信息，诸如口令和密码学密钥。
* **统一可扩展固件接口（UEFI）**：正在广泛部署到新的基于 x86 的计算机系统上的针对传统 BIOS 的可能的替代品。UEFI 规范继承自 EFI 规范。

# 附录 C 首字母缩略词和缩略语

此附录包含此指南中用到的一组选定的首字母缩略词和缩略语。

* ACPI：高级配置与电源接口
* BDS：启动设备选择
* BIOS：基本输入/输出系统
* CPU：中央处理器
* CRTM：用于测定的核心可信根
* DXE：驱动程序执行环境
* EEPROM：电可擦除可编程只读存储器
* EFI：可扩展固件接口
* FIPS：美国联邦信息处理标准
* FISMA：美国联邦信息安全管理法案
* GPT：全局唯一标识分区表
* GUID：全局唯一标识
* HTTP：超文本传输协议
* IT：信息科技
* ITL：信息科技实验室
* MBR：主引导记录
* NIST：美国国家标准技术研究所
* OEM：原始设备制造商
* OMB：美国行政管理和预算局
* OS：操作系统
* PEI：前 EFI 初始化
* POST：加电自检
* PXE：预启动执行环境
* ROM：只读存储器
* RT：运行时
* RTU：更新可信根
* SMI：系统管理中断
* SMM：系统管理模式
* SP：特别出版
* TPM：可信平台模块
* UEFI：统一可扩展固件接口

# 附录 D 参考文献

以下列表提供了此出版物的参考文献。

* \[Duarte08\] G. Duarte. “How Computers Boot Up.” 5 June 2008. [http://www.duartes.org/gustavo/blog/post/how-computers-boot-up](http://www.duartes.org/gustavo/blog/post/how-computers-boot-up)
* \[EFI\] _EFI 1.10 Specification_. Intel. 1 November 2003. [http://www.intel.com/technology/efi/](http://www.intel.com/technology/efi/)
* \[EmSp08\] Shawn Embleton, Sherri Sparks, and Cliff C. Zou. "SMM Rootkits: A New Breed of OS Independent Malware," _Proceedings of 4th International Conference on Security and Privacy in Communication Networks_ \(_SecureComm_\), Istanbul, Turkey, September 22-25, 2008.
* \[FIPS180-3\] FIPS 180-3, _Secure Hash Standard_. October 2008.
* \[FIPS186-3\] FIPS 186-3, _Digital Signature Standard_. June 2009.
* \[DuGr09\] Loïc Duflot, Olivier Grumelard, Olivier Levillain and Benjamin Morin. “ACPI and SMI handlers: some limits to trusted computing.” _Journal in Computer Virology_. Volume 6, Number 4, 353-374.
* \[Graw09\] D. Grawrock. _Dynamics of a Trusted Platform: A Building Block Approach_. Hillsboro, OR: Intel Press, 2009.
* \[Heas07a\] J. Heasman. “Firmware Rootkits: A Threat to the Enterprise.” _Black Hat DC_. Washington, DC. 28 February 2007. [http://www.nccgroup.com/Libraries/Document_Downloads/02_07_Firmware_Rootkits_The_Threat_to_the_Enterprise_Black_Hat_Washington_2007_sflb.sflb.ashx](http://www.nccgroup.com/Libraries/Document_Downloads/02_07_Firmware_Rootkits_The_Threat_to_the_Enterprise_Black_Hat_Washington_2007_sflb.sflb.ashx)
* \[Heas07b\] J. Heasman. “Hacking the Extensible Firmware Interface.” _Black Hat USA_. Las Vegas, NV. 2 August 2007. [https://www.blackhat.com/presentations/bh-usa-07/Heasman/Presentation/bh-usa-07-heasman.pdf](https://www.blackhat.com/presentations/bh-usa-07/Heasman/Presentation/bh-usa-07-heasman.pdf)
* \[Intel03\] _Intel Platform Innovation Framework for EFI- Architecture Specification v0.9_. Intel. September 2003. [http://www.intel.com/technology/framework/](http://www.intel.com/technology/framework/)
* \[KGH09\] A. Kumar, G. Purushottam, and Y. Saint-Hilaire. _Active Platform Management Demystified_. Hillsboro, OR: Intel Press, 2009.
* \[Sal07\] Salihun, Darmawan. _BIOS Disassembly Ninjutsu Uncovered_. Wayne, PA: A-LIST, 2007.
* \[SaOr09\] A. Sacco, A. Ortéga. “Persistant BIOS Infection.” _Phrack_. Issue 66. 6 November 2009. [http://www.phrack.com/issues.html?issue=66&id=7](http://www.phrack.com/issues.html?issue=66&id=7)
* \[SP800-57\] NIST SP 800-57, _Recommendation for Key Management – Part 1: General_. March 2007.
* \[SP800-61\] NIST SP 800-61rev1, _Computer Security Incident Handling Guide_. March 2008.
* \[SP800-89\] NIST SP 800-89, _Recommendation for Obtaining Assurances for Digital Signature Applications_. November 2006.
* \[SP800-128\] Draft NIST SP 800-128, _Guide for Security Configuration Management of Information Systems_. March 2010.
* \[SP800-131A\] NIST SP 800-131A, _Transitions: Recommendation for Transitioning the Use of Cryptographic Algorithms and Key Lengths_. January 2011.
* \[Sym02\] _W95.CIH Technical Details_. Symantec. 25 April 2002. [http://www.symantec.com/security_response/writeup.jsp?docid=2000-122010-2655-99](http://www.symantec.com/security_response/writeup.jsp?docid=2000-122010-2655-99)
* \[TCG05\] _PC Client Work Group Specific Implementation Specification for Conventional Bios Specification, Version 1.2_. Trusted Computing Group. July 2005. [http://www.trustedcomputinggroup.org/resources/pc_client_work_group_specific_implementation_specification_for_conventional_bios_specification_version_12](http://www.trustedcomputinggroup.org/resources/pc_client_work_group_specific_implementation_specification_for_conventional_bios_specification_version_12)
* \[UEFI\] _UEFI Specification Version 2.3_. Unified EFI Forum. May 2009. [http://www.uefi.org/specs/](http://www.uefi.org/specs/)
* \[Wech09\] F. Wecherowski. “A Real SMM Rootkit: Reversing and Hooking BIOS SMI Handlers.” _Phrack_. Issue 66. 6 November 2009. [http://www.phrack.com/issues.html?issue=66&id=11](http://www.phrack.com/issues.html?issue=66&id=11)
* \[WoTe09\] R. Wojtczuk and A. Tereshkin. “Attacking Intel BIOS.” _Black Hat USA_. Las Vegas, NV. 30 July 2009. [http://www.blackhat.com/presentations/bh-usa-09/WOJTCZUK/BHUSA09-Wojtczuk-AtkIntelBios-SLIDES.pdf](http://www.blackhat.com/presentations/bh-usa-09/WOJTCZUK/BHUSA09-Wojtczuk-AtkIntelBios-SLIDES.pdf)

