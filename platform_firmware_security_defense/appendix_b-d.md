# 附录 B 企业平台固件安全指南总结检查列表

此部分为关于本书文本和参考资料，特别是对于适用的 NIST 标准的检查列表总结。当您拾起此列表时，您将会在某种程度上贯穿您当前的所有硬件的_硬件生命周期_。我们建议您简单地开始从头实现（策略和程序），并且将此整个列表应用到您的下一批自然发生的硬件采购中来。然后，如果时间允许，为旧硬件贯穿实施此过程，从最为敏感的位置的硬件开始，例如：

* 官员、财务和法务部门的笔记本
* 符合 _PCI_、_HIPAA_ 等标准的服务器

这可能会由于安全性的原因触发某些计划外的采购，然而旧硬件可以在不那么敏感的应用中重复使用。

---

## 元问题：策略和程序

* 复查并更新现存的公司安全策略以使其包括固件安全
* 复查并更新现存的公司安全程序以使其包括固件安全

## 采购前调研阶段

将硬件和固件包含到威胁模型中来。宽泛地考虑固件。一台计算机包含多种固件镜像：微码、多种平台固件镜像（UEFI 或 BIOS、ACPI 等）、每一块适配器板卡上的固件、每一件外设及其适配器线缆中的固件。除了裸机固件以外，虚拟化技术还拥有同样可以受到攻击的虚拟固件驱动程序。虚拟固件存在其自身的一套攻击方式，有些同裸机固件相同，有些是 VMM 实现所特有的，还有些与传统的应用程序层级的攻击相同。除了存储于闪存和 NVRAM 中的固件 blob 以外，UEFI 将固件作为文件存储在基于 FAT 的磁盘分区上，即 EFI 系统分区（ESP），这在不带 ACL 的 FAT 卷上可以潜在地被攻击者编辑。

计划采购安全的和可以防护的系统，并且在所有层级上防护整个系统：硬件、固件和软件。阅读整篇指南文档并计划实施。

教育技术员工有关固件威胁的内容。为非技术用户防护系统，并且训练他们关于邪恶女仆攻击的内容——特别是对于拥有移动计算设备的用户。

将固件添加到硬件生命周期：系统管理员应该整合 NIST 147，它提供了安全固件生命周期，以增强现存的企业硬件生命周期。数字取证与事故响应（DFIR）团队应该扩展他们的检查列表以包括联系固件厂商、OEM 和 IBV。NIST 147 是一个起始点。

确保厂商特定固件工具的可获得性，测试并且学习使用它们，包括黄金镜像散列值，以及经过签名的更新。

更新对于固件的新闻和培训资源，包括普通的 bug 修复，以及重要安全更新。保证这种覆盖度，以及更新适合于目的。

请求来自厂商的安全数据。自行搜索这些数据，例如，获得一台新型号的样机并且确认它通过了 CHIPSEC 安全测试。

设置公司策略：

* 关于所购买的新系统必须拥有的安全特性，例如，安全启动、验证启动、TPMv2、CHIPSEC 测试等
* 拒绝购自灰色市场的硬件
* 关于新系统所必须配置的安全特性

考虑当前已部署的系统。它们能否满足目的？是应该加速新硬件的采购呢，还是将旧系统部署到不那么敏感的应用中呢？

---

## 供货阶段

基于公司的安全策略配置固件安全设置，例如，启用或禁用 VT/TPM/TXT、唤醒特性、固件/BIOS 口令、固件的网络能力、安全启动等。

确保所有厂商固件为最新，带有最新的密钥用于任何经过签名的代码。

在系统清单中注册终端机身份和 BIOS 完整性信息。

在最初的系统采购过程中，制作您自己的平台固件初始黄金镜像，保存该文件作为初始基线以用于将来的比对。如果厂商提供了它们自己的黄金镜像，将您的镜像或者散列值同它们的进行比对。

使用内建的硬件/固件安全特性：使用现存的厂商固件安全特性、TPM、UEFI 安全启动、验证启动、测定启动、可信启动、Heads 等。

使用经过签名的固件镜像：对于 UEFI，除了安全启动以外，仅使用经过适当签名的固件。理解代码签名过程以及哪里可能存在空当——例如，某些证书被赋予闭源的二进制文件并且不允许源代码审计。

---

## 操作和维护阶段

保持固件为最新：除了操作系统和应用程序外，也进行固件更新，理想情况是通过经过签名的、自动化的机制，例如 Windows Update、Linux _fwupd_（_LVFS_）等。

应用来自 [uefi.org](https://uefi.org/) 或者 [microsoft.com](https://www.microsoft.com) 的最新安全启动黑名单密钥数据库。

利用散列值验证固件更新。

执行周期性的固件安全扫描。下载固件 blob 并且利用散列值检查意外的更改。

将 IT 人员同最终用户设备之间的“亲手操作”互动视为运行自动化的固件层级安全测试的机会。

监视固件传出/传入的所有网络流量。

审计那些建议固件更新的操作系统层级代码。如果正在加固操作系统/应用程序，考虑将执行固件更新的工具限制为只有认证帐户才能访问。

在安全事故中，使用传统恶意软件分析技术以查找固件层级的恶意软件，并且添加固件专用工具，诸如 UEFITool、ACPItool 等。

在安全事故中，响应措施应当包括重新获取固件镜像以及重新运行固件安全测试（CHIPSEC 等），以便同之前的镜像/结果进行比对。

查询供应链中的所有厂商的厂商安全咨询站点以获得关于安全性的建议，以及可供使用的新的检测工具，包括主 CPU、TPM 厂商、操作系统厂商、OEM 以及所有 IHV 等。

---

### 恢复（事故响应）阶段

使用取证工具比较当前的 ROM 镜像和之前的扫描结果以查找更改。

重新运行安全测试，同最后一次已知正确的结果进行比对，以查找攻击者留下的记号。例如，SPI 保护曾经被禁用，但是现在被启用了。

如果系统被操作系统/应用程序层级的恶意软件攻击，它可能已经更新了固件。验证整个系统，进行固件和操作系统层级的测试。利用固件和操作系统的黄金镜像恢复系统。

安全事故之后，事故响应（IR）团队将会需要额外的时间以清除一台系统中的固件层级的恶意软件。在某些情况下，系统可能会变砖并且不能恢复。

安全事故之后，IR 团队的事后分析报告应该包含哪些厂商未能提供足够的工具/镜像以用于固件恢复，并且丢弃那些系统，或者将其重新部署到相对次要的应用中。

---

## 废弃处理阶段

废弃处理之前，将固件恢复至出厂状态。废弃处理一台系统之前，除了清除磁盘介质外，将固件重设至一种已知正确的状态，使用厂商的黄金镜像。

废弃处理之前，清除固件中的任何 PII。废弃处理一台系统之前，确保存储于固件中的任何 PII、用户认证数据、TPM 机密等都被重置。询问厂商如何恢复任何由固件存储的 PII。

# 附录 C 作者传记

## Paul English

Paul English 是 PreOS Security Inc. 的首席执行官。Paul 于 1998 年获得伍斯特理工学院的计算机科学学士学位。自 1996 年起，Paul 成为了一名 UNIX 和 Linux 系统管理员并且戴过很多其他 IT 帽子。其后他管理过少数人，而同时仍然偶尔管理服务器。在 2014～2017 年，Paul 曾经是专业系统管理员联盟（[https://lopsa.org](https://lopsa.org)）的一名委员会成员，该组织是一个非盈利性的专业协会，以推动系统管理实践的进步。

LinkedIn：[https://www.linkedin.com/in/englishpaul/](https://www.linkedin.com/in/englishpaul/)

Twitter：@[penglish_PreOS](https://twitter.com/penglish_PreOS)

## Lee Fisher

Lee 是 PreOS Security Inc. 的首席技术官。他的 IT 职业生涯始于担任一名 VAX/VMS 和 AT&T Unix 系统管理员，彻夜工作以支持其完成大学学业。Lee 曾在微软的多个系统产品团队度过了多年，包括发布“Debugging Tools for Windows”（新的 Windbg）、“Windows NT HAL Kit”以及“Windows NT IFS Kit”。Lee 和他人共同运营了微软移植实验室（Microsoft Porting Lab），他在此帮助了大多数 OEM 和 IHV 将其驱动程序移植到 Windows NT。Lee 将众多开源项目——诸如 NCSA Mosaic——带到微软总部以帮助它们将其代码移植到 Windows。Lee 在 IT 行业中曾经以多种角色工作，但是更加倾向于使用 C 语言编写安全/系统工具。在创办 PreOS 之前，他正在为少数朋友的公司咨询少数特别的内核驱动程序。

Lee 曾在几十场会议中做报告，包括 Security BSides Portland '16、LinuxFest NorthWest、ToorCon Seattle 和微软 WinHEC 等。

Lee 的个人博客可以在这里找到：[https://FirmwareSecurity.com/](https://FirmwareSecurity.com/)

LinkedIn：[https://www.linkedin.com/in/lee-fisher-b80b14143/](https://www.linkedin.com/in/lee-fisher-b80b14143/)

Twitter：@[leefisher_PreOS](https://twitter.com/leefisher_PreOS)

# 附录 D 勘误

## 勘误

## 改进

* 更多插图和示意图
* 带有指向所有攻击向量的名称/箭头的主板
* 硬件生命周期流程图
* 增加直接连接 PCI、USB、JTAG 的攻击向量范例
