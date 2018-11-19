# 附录 A——安全性指导意见总结

此附录包含用于系统 BIOS 完整性测定实现的安全性指导意见的总结。

## 3.1.4 RoT 安全性指导意见

1. 终端机厂商**将要**为实现可信的 RTM、RTS 和 RTR 提供必需的硬件支持，并且利用该支持来实现 BIM 中的对应 RoT
2. 终端机厂商**将要**合并 RTM、RTS 和 RTR 的机制以形成用于 BIM 的集成式的，可靠的基础
3. 终端机厂商**应该**为受到完整性保护的，不可绕过的认证或者安全 BIOS 更新提供机制，作为满足 \[NIST-SP800-147\] 之必需
4. 终端机厂商**可以**为实现某种用于后启动时测定的可信的动态 RTM 提供硬件支持。终端机厂商和操作系统厂商**可以**使用该支持以实现用于 BIM 的这样的 RoT

## 3.2.1.2 RoT 属性的安全性指导意见

1. 终端机厂商**将要**提供定义于 3.2.1.1 节的属性
2. 终端机厂商**将要**在其提供更新和维护所用的最低级别的粒度上为可执行 BIOS 代码提供参考测定数据，并且该参考测定数据可以被用于验证返回自 RTR 的测定数据
3. 终端机厂商**将要**提供机制以测定和报告用于 BIOS 配置数据的测定数据基线
4. 终端机厂商**应该**部署那些并不排除扩展至系统 BIOS 外部的 Option ROM 的 BIOS 测定和报告机制
5. 终端机厂商**应该**以标准化的格式提供属性
6. 终端机厂商**可以**提供关于符合 \[NIST-SP800-147\] 的指示器

## 3.2.2.4 BIOS 完整性测定数据的生成和存储的安全性指导意见

1. 被测定的组件
    1. 终端机**将要**测定所有 BIOS 可执行组件
    2. 终端机**将要**测定所有 BIOS 配置数据组件，除了隐私敏感数据以外
    3. 终端机**应该**独立于其他 BIOS 数据组件来测定隐私敏感数据
2. BIOS 测定数据的生成和存储
    1. 终端机**将要**支持启动时测定
    2. 终端机**将要**使用 RTM 或者植根于 RTM 中的信任链中的某个组件来生成 BIOS 完整性测定数据
    3. 终端机**将要**使用批准的标准密码学技术以生成 BIOS 完整性测定数据
    4. 终端机**将要**使用标准的 BIOS 完整性测定数据格式
    5. BIM 数据——黄金测定数据和终端机测定数据——的格式和报告**将要**使用开放的标准或者规范，诸如 \[TCG-Manifest\] 或者 \[TCG-Integrity\]
    6. 终端机厂商**应该**使用可扩展的系统以允许添加对于测定 Option ROM 等的支持
    7. 终端机**将要**将 BIM 数据存储于 RTS 中
    8. 终端机厂商**应该**使得原始 BIOS 配置数据可用于报告，并且**应该**拥有方法以解读该可用的数据
3. 测定数据日志
    1. BIOS 功能**将要**把 SML 测定数据和事件扩展记录进 CIMR 和 DIMR 中
    2. BIOS 功能**应该**把 SML 测定数据和事件扩展记录进 PIMR 中
    3. 在将 BIM 数据和其他 BIOS 相关事件记录进 SML 中时，BIOS 功能**将要**使用一种标准化的格式，诸如 \[TCG-ConvBiosSpec\]
    4. BIOS **将要**保证恰当地将 SML 移交给后启动环境
4. 测定支持
    1. 操作系统厂商**将要**支持某种标准 API 以用于采集测定数据
    2. 终端机、操作系统和应用程序厂商**将要**支持用于采集和报告 BIM 数据的 RTR

## 3.3.2 报告协议的安全性指导意见

1. 在下列任何情况下，BIOS 报告机制**可以**准备并且向某个合法 MAA 签发 BIOS 完整性报告：
    1. 如果 BIOS 配置发生更改
    2. 如果 BIOS 软件发生更改
    3. 如果某个本地端口被用于访问 BIOS 或其配置
    4. 如果某个 BIOS 错误条件被生成
    5. 当连接至由某个合法 MAA 控制的网络时
2. BIOS 报告机制**可以**支持配置特定事件以引发 BIOS 完整性测定数据报告的能力
3. 报告请求**可以**由报告的报告方或者接收方引发。下列要求适用于由任何一方引发的请求：
    1. 机制**将要**能够提供可证明地新鲜的 BIOS 报告以发送至 MAA
    2. 此报告**应该**包含一段关于此报告所用的格式化标准/纲要的引用
    3. 此报告格式**应该**包含一个版本字段，它可以在报告格式发生扩展或者其他变化时随着时间被更新
    4. 来自非法实体的所有签发或者提供报告的请求**应该**被忽略
    5. 提供或者签发报告的请求**可以**包含优先级以指示该请求的紧急性
    6. 与请求相关的响应时间框架**可以**由授权用户根据优先级进行配置

## 3.4.2 测定数据采集和传输的安全性指导意见

传输代理**将要**安全地将 BIOS 完整性测定数据从终端机传输至 MAA，如下所述：

1. 所有报告会话**将要**：
    1. 拥有提供机密性保护的能力
    2. 提供完整性保护和新鲜度
    3. 认证 MAA
    4. 提供终端机身份认证
2. 传输代理：
    1. **将要**允许测定数据在从 RTR 到验证组件的全程受到完整性保护
    2. **应该**支持一系列不同的服务，诸如不间断监测、网络访问控制和应用程序层级的完整性监测等
    3. **应该**保证所得到的系统是廉价、非强迫性、高性能和安全的（尽管更高级的安全性可能要求更高级的开销）
3. 终端机上的采集代理传输代理**应该**支持开放格式以允许在众多不同类型的终端机和 MAA 之间以及在众多不同形式的通讯媒体之间实现可互操作性，直到能够存在这样的可用标准的程度

## 3.5.2 MAA 安全性指导意见

1. MAA **将要**能够存储期望值（黄金测定数据）
2. MAA **将要**能够将所报告的值同期望值和/或之前报告的（最后已知的）测定数据进行比较
3. MAA **将要**能够存储被报告的值
4. MAA **将要**支持开放格式以允许在众多不同类型的终端机和 MAA 之间以及在众多不同形式的通讯媒体之间实现可互操作性，直到能够存在这样的可用标准的程度
5. MAA **可以**能够提供关于某个意外、异常的测定数据是由比特衰减造成的可能性的评估机制，如果它被提供给产生此异常测定数据的 BIOS 内容以及存在黄金测定数据的 BIOS 内容

# 附录 B——用语和缩略语

此部分附录定义了此文档中所使用的术语。

* **属性**：评估者用于决定其可信度的 RoT 性质
* **BIOS 代码完整性测定数据寄存器（CIMR）**：包含终端机上的所有静态 BIOS 代码的密码学散列值或者构成了 BIOS 代码空间的所有 BIOS 组件的组合散列值的寄存器
* **BIOS 数据完整性测定数据寄存器（DIMR）**：包含终端机上的所有动态 BIOS 配置数据的密码学散列值或者构成了 BIOS 配置数据空间的所有 BIOS 组件的组合散列值的寄存器
* **BIOS 隐私完整性测定数据寄存器（PIMR）**：包含所有 BIOS 隐私敏感数据的组合散列值的寄存器
* **BIOS 完整性测定数据的生成**：创建 BIOS 组件的散列值并且用这些散列值填充静态和动态 BIOS 配置寄存器的行为
* **比特衰减**：由于随机物理过程造成的 BIOS 存储变化
* **采集**：测定终端机 BIOS 完整性的行为，以及收集所得到的测定数据以使得它们可以从终端机被传输的过程
* **动态 BIOS 组件**：BIOS 中可由用户更改而无需 BIOS 厂商或者系统厂商辅助的部分，这通常指代 BIOS 配置数据
* **终端机**：其 BIOS 完整性正在被测定的系统。终端机可以是台式机、服务器、虚拟化环境以及服务等
* **黄金测定数据**：关于 BIOS 及其配置数据的一组可信的完整性测定数据。这些测定数据通常由可信的相关方提供，诸如终端机的 OEM，它们也可以由系统管理员在一台设备的初始供货过程中采集。由 OEM 签名的 BIOS 的 SHA-2 散列值是黄金 BIOS 测定数据的一个范例。黄金 BIOS 测定数据并不提供关于恶意属性存在与否的信息。但是它确实能够帮助对某个对象进行快速、可靠以及不可抵赖的识别
* **完整性测定数据**：对于二进制代码和/或数据的紧凑表示形式。在 BIOS 完整性测定的上下文环境中，它通常表示为二进制代码和数据的密码学散列值，通常以密码学的方式签名以保持合法性和不可抵赖性
* **已知良好状态**：如果 BIOS 已经被验证为处于某种可接受的状态。此状态的一个范例是如果已加载的 BIOS 的数字签名被验证为与制造商的当前版本匹配
* **测定数据评估权威机构（MAA）**：一个代表 IT 管理部门运行的代理。它从客户端接收测定数据、检查这些测定数据的签名、通过将其同黄金测定数据进行比较来评估测定数据的质量，它可以进一步分析测定数据（以确定 BIOS 完整性测定数据发生了哪些更改，如果此测定数据与黄金测定数据不匹配），然后要么将此结果显示给 IT 管理部门，要么作为 IT 管理部门的代理以采取预设的行动，如果测定数据并非期望值
* **管理控制器**：在服务器环境中，通常有监督性的处理器或者控制器以“管理”运行应用程序的主处理器。此管理控制器独立于主处理器，并且能够为其或者以其身份执行若干操作
* **主处理器**：系统上可用于运行应用程序的可能的若干处理器（核心）之一
* **恢复**：修正计算系统的问题的过程
* **可信根（RoT）**：构成了一组被无条件信任的功能的组件（软件、硬件或者混合）和计算引擎。RoT 必须总是以某种预期的方式运作，由于它的不当行为不能被检测到
* **测定可信根（RTM）**：能够进行内在地可靠的完整性测定的计算引擎。RTM 是后续测定代理的传递性信任链的根基
* **报告可信根（RTR）**：能够可靠地报告由 RTM 及其测定代理提供的或者由 RTS 保存的信息的计算引擎
* **存储可信根（RTS）**：能够维持一段使得破坏显而易见的，关于完整性测定值及其测定序列的总结的计算引擎
* **静态 BIOS 组件**：BIOS 中可由用户修改的部分，通常需要来自 BIOS 厂商或者系统厂商的辅助。这通常被称为 BIOS 代码。在历史上，此代码几乎不包含任何对更改的保护机制。\[NIST-SP800-147\] 概述了厂商能够部署的 BIOS 保护机制

以下列表包含了此文档中所使用的首字母缩略词和其他缩略语。

* ACPI：高级配置与电源接口
* API：应用程序接口
* ARF：财产报告格式
* BBM：基于 BIOS 的管理
* BIM：BIOS 完整性测定
* BIOS：基本输入/输出系统
* CIM：通用信息模型
* CIMR：代码完整性测定数据寄存器
* CPU：中央处理器
* DIMR：数据完整性测定数据寄存器
* DMI：桌面管理接口
* DMTF：分布式管理任务小组
* EFI：可扩展固件接口
* FIPS：美国联邦信息处理标准
* HMAC：基于散列的消息认证码
* IMR：完整性测定数据寄存器
* ISV：独立软件厂商
* IT：信息科技
* ITL：信息科技实验室
* MAA：测定数据评估权威机构
* NFC：近场通讯
* NIST：美国国家标准技术研究所
* NISTIR：美国国家标准技术研究所跨部门报告
* OEM：原始设备制造商
* OS：操作系统
* PCR：终端机配置寄存器
* PIMR：隐私完整性测定数据寄存器
* POST：加电自检
* PXE：预启动执行环境
* RAM：随机存取存储器
* RFC：请求意见稿
* ROM：只读存储器
* RoT：可信根
* RTM：测定可信根
* RTR：报告可信根
* RTS：存储可信根
* SCAP：安全内容自动化协议
* SMBIOS：系统管理 BIOS
* SML：存储的测定数据日志
* SMRAM：系统管理内存
* SP：特别出版
* TCG：可信计算小组
* TLS：传输层安全性协议
* TLV：类型长度值
* TNC：可信网络连接
* TPM：可信平台模块
* UEFI：统一可扩展固件接口
* URI：统一资源标志符
* USB：通用串行总线
* VAR：增值分销商
* VM：虚拟机
* XML：可扩展标记语言

# 附录 C——参考文献

附录 C 标识出了相关参考文献。

* \[DMTF-SMBIOS\] DSP0134, “System Management BIOS (SMBIOS) Reference Specification”, Version 2.7.1, DMTF, February 2011, [http://www.dmtf.org/standards/smbios](http://www.dmtf.org/standards/smbios).

* \[IETF-RFC-2119\] Bradner, S., RFC 2119, “Key words for use in RFCs to Indicate Requirement Levels”, IETF, March 1997, [http://www.ietf.org/rfc/rfc2119.txt](http://www.ietf.org/rfc/rfc2119.txt).

* \[IETF-RFC-3576\] Chiba, M., Dommety, G., Eklund, M., Mitton, D., and Aboba, B., RFC 3576, “Dynamic Authorization Extensions to Remote Authentication Dial In User Service (RADIUS)”, IETF, July 2003, [http://www.ietf.org/rfc/rfc3576.txt](http://www.ietf.org/rfc/rfc3576.txt).

* \[IETF-RFC-5792\] Sangster, P. and Narayan, K., RFC 5792, “PA-TNC: A Posture Attribute (PA) Protocol Compatible with Trusted Network Connect (TNC)”, IETF, March 2010, [http://www.ietf.org/rfc/rfc5792.txt](http://www.ietf.org/rfc/rfc5792.txt).

* \[IETF-RFC-5793\] Sahita, R., Hanna, S., Hurst, R., and Narayan, K., RFC 5793, “PB-TNC: A Posture Broker (PB) Protocol Compatible with Trusted Network Connect (TNC)”, IETF, March 2010, [http://www.ietf.org/rfc/rfc5793.txt](http://www.ietf.org/rfc/rfc5793.txt).

* \[NIST-FIPS180-3\] FIPS PUB 180-3, “Secure Hash Standard (SHS)”, NIST, October 2008, [http://csrc.nist.gov/publications/fips/fips180-3/fips180-3_final.pdf](http://csrc.nist.gov/publications/fips/fips180-3/fips180-3_final.pdf).

* \[NIST-IR-7670\] Waltermire, D., Johnson, C., Kerr, M., Wojcik, M., and Wunder, J., IR 7670 (Draft), “Proposed Open Specifications for an Enterprise Remediation Automation Framework”, NIST, February 2011, [http://csrc.nist.gov/publications/drafts/nistir-7670/Draft-NISTIR-7670_Feb2011.pdf](http://csrc.nist.gov/publications/drafts/nistir-7670/Draft-NISTIR-7670_Feb2011.pdf).

* \[NIST-IR-7694\] Halbardier, A., Waltermire, D., and Johnson, M., IR 7694, “Specification for the Asset Reporting Format 1.1 (ARF)”, NIST, June 2011, [http://csrc.nist.gov/publications/PubsNISTIRs.html#NIST-IR-7694](http://csrc.nist.gov/publications/PubsNISTIRs.html#NIST-IR-7694).

* \[NIST-IR-7802\] Booth, H. and Halbardier, A., IR 7802, “Trust Model for Security Automation Data 1.0 (TMSAD)”, NIST, September 2011, [http://csrc.nist.gov/publications/PubsNISTIRs.html#NIST-IR-7802](http://csrc.nist.gov/publications/PubsNISTIRs.html#NIST-IR-7802).

* \[NIST-SP800-106\] Dang, Q., SP 800-106, “Randomized Hashing for Digital Signatures”, NIST, February 2009, [http://csrc.nist.gov/publications/PubsSPs.html#800-106](http://csrc.nist.gov/publications/PubsSPs.html#800-106).

* \[NIST-SP800-126\] Waltermire, D., Quinn, S., Scarfone, K., and Halbardier, A., SP 800-126 Revision 2, “The Technical Specification for Security Content Automation Protocol (SCAP): SCAP Version 1.2”, NIST, September 2011, [http://csrc.nist.gov/publications/PubsSPs.html#800-126](http://csrc.nist.gov/publications/PubsSPs.html#800-126).

* \[NIST-SP800-147\] Cooper, D., Polk, W., Regenscheid, A., and Souppaya, M., “NIST Special Publication 800-147: BIOS Protection Guidelines”, NIST, April 2011, [http://csrc.nist.gov/publications/PubsSPs.html#800-147](http://csrc.nist.gov/publications/PubsSPs.html#800-147).

* \[TCG-ARCH-INTER\] “TCG Trusted Network Connect TNC Architecture for Interoperability”, Version 1.4, Revision 4, Trusted Computing Group, May 2009, [http://www.trustedcomputinggroup.org/resources/tnc_architecture_for_interoperability_specification](http://www.trustedcomputinggroup.org/resources/tnc_architecture_for_interoperability_specification).

* \[TCG-Att-PTS\] “TCG Attestation PTS Protocol: Binding to TNC IF-M”, Version 1.0, Revision 28, Trusted Computing Group, August 2011, [http://www.trustedcomputinggroup.org/resources/tcg_attestation_pts_protocol_binding_to_tnc_ifm](http://www.trustedcomputinggroup.org/resources/tcg_attestation_pts_protocol_binding_to_tnc_ifm).

* \[TCG-ConvBiosSpec\] “TCG PC Client Specific Implementation Specification for Conventional BIOS”, Version 1.20, Trusted Computing Group, July 2005, [http://www.trustedcomputinggroup.org/resources/pc_client_work_group_specific_implementation_specification_for_conventional_bios_specification_version_12](http://www.trustedcomputinggroup.org/resources/pc_client_work_group_specific_implementation_specification_for_conventional_bios_specification_version_12).

* \[TCG-EFI\] “TCG EFI Platform Specification”, Version 1.20, Revision 1.0, June 2006, [http://www.trustedcomputinggroup.org/resources/tcg_efi_platform_specification_version_120_revision_10](http://www.trustedcomputinggroup.org/resources/tcg_efi_platform_specification_version_120_revision_10).

* \[TCG-IF-M\] “TCG Trusted Network Connect TNC IF-M: TLV Binding”, Version 1.0, Revision 37, Trusted Computing Group, March 2010, [http://www.trustedcomputinggroup.org/resources/tnc_ifm_tlv_binding_specification](http://www.trustedcomputinggroup.org/resources/tnc_ifm_tlv_binding_specification).

* \[TCG-IF-PEP\] “TCG Trusted Network Connect TNC IF-PEP: Protocol Bindings for RADIUS”, Version 1.1, Revision 0.7, Trusted Computing Group, February 2007, [http://www.trustedcomputinggroup.org/resources/tnc_ifpep_protocol_bindings_for_radius_specification](http://www.trustedcomputinggroup.org/resources/tnc_ifpep_protocol_bindings_for_radius_specification).

* \[TCG-IF-PTS\] “TCG Infrastructure Working Group Platform Trust Services Interface Specification (IF-PTS)”, Version 1.0, Revision 1.0, November 2006, [http://www.trustedcomputinggroup.org/resources/infrastructure_work_group_platform_trust_services_interface_specification_version_10](http://www.trustedcomputinggroup.org/resources/infrastructure_work_group_platform_trust_services_interface_specification_version_10).

* \[TCG-IF-T-EAP\] “TCG Trusted Network Connect TNC IF-T: Protocol Bindings for Tunneled EAP Methods”, Version 1.1, Revision 10, Trusted Computing Group, May 2007, [http://www.trustedcomputinggroup.org/resources/tnc_ift_protocol_bindings_for_tunneled_eap_methods_specification](http://www.trustedcomputinggroup.org/resources/tnc_ift_protocol_bindings_for_tunneled_eap_methods_specification).

* \[TCG-IF-T-TLS\] “TCG Trusted Network Connect TNC IF-T: Binding to TLS”, Version 1.0, Revision 16, Trusted Computing Group, May 2009, [http://www.trustedcomputinggroup.org/resources/tnc_ift_binding_to_tls_version_10_revision_16](http://www.trustedcomputinggroup.org/resources/tnc_ift_binding_to_tls_version_10_revision_16).

* \[TCG-Integrity\] “TCG Infrastructure Working Group Integrity Report Schema Specification”, Version 1.0, Trusted Computing Group, November 2006, [http://www.trustedcomputinggroup.org/resources/infrastructure_work_group_integrity_report_schema_specification_version_10/](http://www.trustedcomputinggroup.org/resources/infrastructure_work_group_integrity_report_schema_specification_version_10/).

* \[TCG-Manifest\] “TCG Infrastructure Working Group Reference Manifest (RM) Schema Specification”, Version 1.0, Trusted Computing Group, November 2006, [http://www.trustedcomputinggroup.org/resources/infrastructure_work_group_reference_manifest_rm_schema_specification_version_10/](http://www.trustedcomputinggroup.org/resources/infrastructure_work_group_reference_manifest_rm_schema_specification_version_10/).

# 附录 D——实现可信根的选项

BIOS 完整性保障的基础是 RoT，它们基于一种或者多种硬件机制属性构建。某些 RoT 本身假设 \[NIST-SP800-147\] 中的要求和建议已被满足。某些和 RoT 最为相关的硬件机制列于下方。（此列表并不完整。）

## D.1 CPU 和芯片组的启动逻辑

BIOS 完整性取决于 CPU 在启动时的良好定义的行为，特别是取决于芯片组正确地映射 BIOS 存储设备，以及 CPU 在重置之后如同期望中地执行正确的初始 BIOS 指令。此硬件机制是启动时 RTM 的基础，但是对于基于“延迟启动”机制的 RTM 或者 CPU 在运行时的重新初始化可能不那么相关。

## D.2 UEFI 加电 SEC 安全阶段

统一可扩展固件接口（UEFI）对于早先完全由 BIOS 处理的功能提供了补充和部分替换。UEFI 加电 SEC 安全阶段可以提供一种 RoT，它可能能够以这样一种方式可靠地调用 UEFI 中的软件管理代理，以使得它可以被用于实现用于 BIOS 完整性的 RTM。这可能要求符合 \[NIST-SP800-147\]。

## D.3 BIOS 存储设备的访问控制区域

BIOS 和 BIOS 测定数据的完整性基于对于 BIOS 存储设备本身的硬件访问控制机制。这样的访问控制可以通过能够阻止读取或者写入 BIOS 存储设备的“设置直到重启”的触发器来强制执行。这样的触发器被持续设置，直到下一次硬件重置，并且可以在启动的早期阶段被诸如 BIOS 本身等锁定。这些触发器可以通过诸如在 BIOS 存储设备本身或者 CPU 芯片组内部的硬件机制来实现。这些机制可以被用于形成符合 \[NIST-SP800-147\] 的基础。

被符合 \[NIST-SP800-147\] 的架构所支持的 BIOS 存储设备访问控制区域也可作为 RTS 和 RTR 的基础。例如，BIOS 可以在初始化过程中测定其自身，并且将测定结果置于一块可读但是“写保护直到硬件重置”的 BIOS 存储区域。BIOS 也可以在将控制权移交给操作系统或者引导程序之前利用密码学密钥创建报告，此密钥存储于一块将会在随后被设置为“不可访问直到下次硬件重置”的 BIOS 存储区域中。为了保证新鲜度，报告可以使用于上次操作系统执行过程中存储于 BIOS 的易失性区域中的临时随机数。

### D.3.1 静态的不可变 BIOS 启动块

一块静态的不可变 BIOS 启动块（或者初始 BIOS 代码区域）可以作为 BIOS 完整性 RTM 的基础，例如通过测定相关 BIOS 存储设备的内容以及设置其访问控制触发器。由于其构建于一块不可变的 BIOS 启动块的基础之上，这样的 RTM 可能提供定义于 3.1 节的可变状态容错性，甚至无需满足 \[NIST-SP800-147\]。

## D.4 隔离的 CPU 执行模式和访问控制内存

若干种 CPU 执行模式和内存访问控制特性可以构成 BIOS 完整性和 BIOS 测定数据的可信根。就其本质而言，这些实现不能提供如 3.1 节所定义的内存泄露容错性。

对于某种符合 \[NIST-SP800-147\] 的架构，CPU 的 SMM 执行模式能够成为某种隔离的、状态性的机制的基础的潜在 RoT，该机制在启动时由 BIOS 控制和初始化，但是在该设备的整个执行过程中可用，直到下一次重置。在某些情况下，SMM 代码可能对于 BIOS 存储设备拥有比操作系统内核更大的访问权限。SMM 模式就其自身而言不是一种 RTM 的基础。然而，SMM 模式可以构建于某种基于 BIOS 的 RTM 的基础之上，并且用于 (a) 执行对于 BIOS 存储设备的内容及其相关的访问控制触发器设置的运行时测定，(b) 通过将测定结果置于 SMRAM 中来实现一种 RTS，或者 (c) 实现一种 RTR，例如通过使得 BIOS 利用某个密码学私钥来初始化 SMRAM，此密钥被用于签名测定报告，并且在 BIOS 初始化之后除了通过 SMM 模式以外无处可以访问。

如同在 TCG 规范中概述的那样，某些 CPU 提供了所谓的动态 RoT 支持，在此，CPU 被重新初始化为某种已知良好状态。同 TPM 相配合，这样的“延迟启动” CPU 执行模式可以成为所有必需的 RoT 的基础。然而值的注意的是，这样的动态测定可能不能建立过去或者将来的硬件重置时的 BIOS 或者 BIOS 设置的完整性；为了建立这样的启动时保障，BIOS 完整性**必须**利用诸如 \[NIST-SP800-147\] 中概述的机制来保护。

## D.5 监督 CPU 执行模式和仅可由监督程序访问的内存

虚拟机监视器或者操作系统中的高权限、内核模式代码的一项传统任务是保护系统设备，诸如 BIOS。虚拟机监视器或者操作系统内核几乎总是通过由硬件支持的内存机制保护的，并且内核运行于一种监督执行模式，具有其自身的私有内存。在原理上，这些硬件机制可以成为用于实施 BIOS 完整性的 RTM、RTS 和 RTR 的 RoT，其中，虚拟机监视器或者操作系统保护其自身、BIOS，以及被报告的测定数据的完整性，特别是在假设架构符合 \[NIST-SP800-147\] 的情况下。由于它们的大小和复杂性，这样的由虚拟机监视器或者操作系统支持的 RoT 可能只能提供极少的保障和最小化的担保，至少是对于标准的虚拟机监视器或者操作系统而言。

## D.6 可信平台模块

TPM 可以作为 RTS 和 RTR 的基础。当它与静态的不可变 BIOS 启动块（由 TCG 规范控制，如 D.3 节所述）相结合时，TPM 可以提供可变状态容错性和内存泄露容错性，如 3.1 节所定义。

## D.7 私有 RoT

BIOS 完整性保护和测定机制可以由 CPU、CPU 芯片组和/或 BIOS 存储设备中的自定义逻辑来实现。这样的自定义逻辑可以被用于实现任意 RoT，尽管极少（如果有的话）这样的实现现在可用于客户端硬件平台商品。

这样的 RoT 的范例可能包括这样的 BIOS 存储设备，它们要么同某个嵌入式的独立微控制器打包在一起，要么与其紧密通讯，该微控制器被提供给了私钥和私有存储。如果被适当地实现，这样的 RoT 可以被用于实现那些能够提供如 3.1 节定义的可变状态容错性和内存泄露容错性的机制。

# 附录 E——范例实现的可能性

附录 E 列举了利用普遍可用的机制来实现 BIOS 完整性测定的一些可能性。在此处没有被考虑的一些机制的范例包括管理控制器（例如嵌入于 Intel Sandy Bridge 及其后续芯片组中的管理引擎）以及嵌入于 BIOS 存储设备中的微控制器。

## E.1 范例 1——利用高担保性的内核或者虚拟机监视器的可能实现

在此范例实现中，一段可信的监督程序（诸如一款可信的虚拟机监视器或者高担保性的隔离内核）被用于创建 BIOS 完整性测定所必需的 RoT，基于 CPU 启动逻辑（E.1 节）和监督执行模式（E.4 节条目 3）的硬件 RoT。此监督程序负责引导性地保护 RoT 以及在操作过程中和更新之间保证 BIOS 及其设置的完整性。

1. 在设备重置时，CPU 开始执行 BIOS 存储设备（例如闪存芯片）外的首段 BIOS 指令
2. BIOS 完成初始化并且将控制权直接移交给一段可信的监督程序，或者移交给一段可信的引导程序，后者查找并加载可信的监督程序
3. 此可信的监督程序负责实施 \[NIST-SP800-147\] 指导意见，以及完整调度和控制对于设备配置的访问权限，包括 CPU 启动逻辑和 BIOS 内容和设置的配置，以及包含引导程序的启动存储设备和监督程序本身的代码和配置的配置
4. 此可信监督程序还构成了 BIOS 完整性测定的 RTM、RTS 和 RTR，并且必须保护存储的测定结果（例如，作为启动存储设备上的受保护状态的一部分）并且允许这些结果被可证明地新鲜地报告（例如，以使得它们不能被伪造或者重放）。基于此目的，此监督程序可以使用私密的私钥，例如存储于 BIOS 或者启动存储设备中的私钥
5. 不论是按需、启动时还是每当 BIOS 升级时，此监督程序都可以准备 BIM 报告，通过测定诸如 (a) 所有 BIOS 代码，(b) 诸如不可写的配置设置等关键 BIOS 数据，以及 (c) NVRAM 配置数据等
6. 保证此监督程序（并且只有此监督程序）将会在下次硬件重置时被再次启动是 BIOS 和监督程序的责任。BIOS 必须保护其自身以及任何存储的 RTR 密码学密钥（例如，通过销毁这些密钥），除非 BIOS 能够保证当其完成初始化之后，控制权将被移交给一份通过验证的可信监督程序的副本

上述实现既不能提供 3.1 节所述的可变状态容错性，也不能提供 3.1 节所述的内存泄露容错性。

## E.2 范例 2——利用基于触发器的机制的可能实现

此范例实现假设一种符合 \[NIST-SP800-147\] 的架构，其中，由 BIOS 在启动时安装的 BIOS 启动代码和 SMM 代码的组合被用于创建 BIOS 完整性测定所必需的 RoT，基于 CPU 启动逻辑（D.1 节）、SMM 执行模式（D.4 节）和 BIOS 存储设备访问控制（D.3 节）的硬件 RoT。BIOS 本身及其 SMM 代码负责引导性地保护 RoT 以及在操作过程中和更新之间保证 BIOS 及其设置的完整性。

1. 在设备重置时，CPU 开始执行 BIOS 存储设备（例如闪存芯片）外的首段 BIOS 指令
2. 为了实施 \[NIST-SP800-147\] 的指导意见，BIOS 首先检查可访问的存储设备（例如磁盘、BIOS 闪存芯片中的剩余空间，或者插入的 USB 设备）中是否有可用的有效的、经过签名的 BIOS 升级。如果发现无需升级，BIOS 可以检查其自身的完整性；此步骤应该只需防止比特衰减，由于 BIOS 的完整性通过运行时写保护而被引导性地保持
3. BIOS 随后设置 SMM 模式并且将一份 BIOS 特定地私钥复制到 SMRAM。此 BIOS 也会复制一份完整的 BIOS/NVRAM 配置数据到 SMRAM 中。SMM 代码负责运行时 BIOS 测定以及 BIM 结果的密钥签名
4. BIOS 随后对“锁定直到设备重置”的触发器进行编程以 (a) 使得所有 BIOS 代码和所有关键数据，例如不可写的配置设置成为不可写，以及 (b) 使得包含 BIOS 特定的私钥的 BIOS 闪存区域成为不可访问，即既不可读也不可写
5. BIOS 将控制权移交给引导程序，后者查找并加载操作系统
6. 在运行时提供一个临时随机数以创建关于一项 BIM 属性的报告，例如 (a) BIOS 闪存芯片中的 BIOS 代码字节，(b) 当前或者启动时的 NVRAM 配置，(c) “锁定直到设备重置”的触发器的状态以及相关设备控制区域等
7. SMM 代码通过一个或者更多 SMI 调用，并且 SMM 代码测定所请求的属性，诸如……(c)……通过查询 BIOS 闪存芯片本身以及芯片组（例如南桥）中的控制寄存器
8. SMM 代码将其测定数据和临时随机数合并为一条消息摘要，并且利用 BIOS 特定的私钥对此消息摘要进行签名

上述实现既不能提供 3.1 节所述的可变状态容错性，也不能提供 3.1 节所述的内存泄露容错性。

## E.3 范例 3——利用基于 TPM 的机制的可能实现

此范例普遍存在于当今的企业客户端中，其中，BIOS 启动代码和由 TCG 详细说明的 TPM 的组合被用于创建 BIOS 完整性测定所必需的 RoT，基于 CPU 启动逻辑（D.1 节）、TPM（D.5 节）以及 BIOS 存储设备访问控制（D.3 节）的硬件 RoT。由 BIOS 本身负责引导性地保护软件测定代理，并且在操作过程中以及更新之间保证 BIOS 及其设置的完整性。

1. 在设备重置时，CPU 开始执行 BIOS 存储设备外的不可变的 BIOS 启动块的首段指令，并且 TPM 寄存器被设置为已知值
2. 不可变的 BIOS 启动块测定 (a) 所有 BIOS 代码，(b) 所有关键 BIOS 数据，诸如不可写的配置设置，以及 (c) NVRAM 配置数据，并且将这些测定数据扩展至 TPM 中的独立 PCR 中。TPM 负责存储测定数据以及报告 BIM 结果，并且 TPM 密钥被用于签名 BIM 结果
3. BIOS 启动块将控制权移交给驻留于 BIOS 存储设备中的已测定、可变的部分中的代码该代码随之将控制权移交给引导程序以查找并加载操作系统。注意，此实现不符合 \[NIST-SP800-147\]，由于它并未尝试建立 BIOS 代码完整性，例如，通过写保护 BIOS 存储设备中的代码区域
4. 在运行时提供一个临时随机数以创建关于一项 BIM 属性的报告，例如 (a) BIOS 代码散列值，(b) 启动时 NVRAM 配置，(c) “锁定直到设备重启”的触发器的状态及其相关设备控制区域等
5. TPM 中的 PCR 寄存器与临时随机数合并，并且由驻留 TPM 的密钥签名，以创建关于诸如 BIOS 代码以及存在于启动时的配置的报告

## E.4 范例 4——利用基于 CPU 延迟启动的机制的可能实现

在此范例实现中，BIOS 启动代码和符合 TCG 规范的 CPU 延迟启动的组合被用于创建 BIOS 完整性测定所必需的 RoT，基于 CPU 启动逻辑（D.1 节）、TPM（D.5 节）以及运行时重新初始化的 CPU 执行模式（D.4 节）的硬件 RoT。硬件本身负责引导性地保护 RoT，而 BIOS 及其设置在操作过程中以及更新之间的完整性可以通过不同的软件方式保护——或者甚至完全不受保护。

1. 在设备重置时，CPU 开始执行 BIOS 存储设备外的首段 BIOS 指令
2. \[NIST-SP800-147\] 的指导意见中的实现中的某个瑕疵可能使得 BIOS 损坏，然而，延迟启动的功能允许 BIOS 完整性被以这样一种方式测定，它将发现此种损坏，并且潜在地揭示一次攻击
3. BIOS 将控制权移交给引导程序，后者查找并加载操作系统
4. 在运行时提供一个临时随机数以创建关于一项 BIM 属性的报告，诸如 (a) BIOS 代码散列值，(b) NVRAM 配置，(c) “锁定直到设备重置”的触发器的状态及其相关设备控制区域等
5. CPU 通过延迟启动功能进入一种洁净、良好定义的环境，其在某些 TPM 寄存器中具有已知、良好定义的值
6. 此延迟启动环境测定下列内容，诸如 (a) 所有 BIOS 代码，(b) 所有关键 BIOS 数据，诸如不可写的配置设置，以及 (c) NVRAM 配置数据，并且将其写入 TPM 上的良好定义的独立 PCR 中。TPM 负责存储测定数据以及报告 BIM 结果，并且 TPM 密钥被用于签名 BIM 结果
7. TPM 中的 PCR 寄存器同临时随机数合并，并且由驻留 TPM 的密钥签名，以创建关于例如存在于启动时的 BIOS 代码的报告

