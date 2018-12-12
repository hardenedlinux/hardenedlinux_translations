# 附录 A——首字母缩略词

此论文中使用的选定的首字母缩略词和缩略语定义如下。

* BIOS：基本输入/输出系统
* CoT：信任链
* CPLD：复杂可编程逻辑器件
* CTD：检测信任链
* CTRec：恢复信任链
* CTU：更新信任链
* FPGA：现场可编程逻辑门阵列
* ROM：只读存储器
* RoT：可信根
* RTD：检测可信根
* RTRec：恢复可信根
* RTU：更新可信根
* UEFI：统一可扩展固件接口

# 附录 B——词汇表

* **活动关键数据**：用于初始化或者配置设备的那一份关键数据副本。_注释：活动关键数据并不包括关键数据的备份。_
* **扩展卡**：用于指代可以通过诸如 PCI 等连接总线插入到平台中或者从平台中移除的任何设备的通用术语。扩展卡通常被插入到平台的物理机箱内部，而非物理存在于平台外部。扩展卡拥有其自身的设备及其相关联的固件，并且可能拥有其自身的扩展 ROM 固件。
* **认证更新**：使用认证更新机制的更新。
* **认证更新机制**：一种更新机制，它保证更新固件镜像经过数字签名，并且该数字签名可以在更新该镜像之前利用更新可信根（RTU）的密钥存储器中的某个密钥进行验证。
* **授权更新**：使用授权更新机制的更新。
* **授权更新机制**：一种更新机制，它在安装更新之前检查是否得到了批准。批准可能包括检查是否拥有凭证、由物理存在的人员进行确认，或者类似的方式。
* **启动固件**：用于描述在平台上执行以启动（启动、初始化）设备的任何固件的通用术语。这可能包括但不限于初始化设备内存、初始化设备寄存器、初始化连接性接口、设备的健康度检查等。启动固件的一般目的是使得设备或者平台对于正常操作使用准备就绪。
* **信任链（CoT）**：信任链（CoT）是植根于可信根（RoT）中的一系列协作性的元素，该元素通过当它移交其控制权时将相同的信任属性传递给下一个元素来延伸当前元素的信任边界。其结果是两个元素都能同等程度地完成信任功能，如同它们是一个可信元素那样。这一过程可以被延续，以进一步延伸信任链。一旦控制权被移交给未经验证或者不能被验证的代码，则信任链终结。这也被称为将控制权移交至某个非协作性的元素。
* **代码**：由处理器或者类似设备（FPGA、CPLD 等）直接执行的指令。也包括由程序进行解读的指令。_源代码_ 是被翻译成代码并且随后执行的人类可读指令。
* **损坏**：损坏是指固件代码的完整性的丧失，或者关键数据中的错误或者意外的值，这可能是一系列不同原因中的任意一种的结果，包括但不限于：恶意活动（例如攻击者）、编写不良的代码（例如缓冲区溢出、算法错误）、意外事件（例如用户疏忽的行为）、未能安装某个安全补丁、非授权更改，或者由硬件引发的（例如信号完整性、阿尔法粒子、供电故障等）。
* **关键数据**：关键数据是在加电循环之间持续存在的可变数据，并且必须处于由平台管理员授权的某种有效状态，以使得平台的恢复和/或启动过程可以安全和正确地进行。
* **关键平台固件**：所有具有这些特征的平台固件的集合：(a) 执行任何平台固件的保护、检测、恢复和更新功能；(b) 维护关键数据的安全性；或者 (c) 实现了不可绕过的关键数据接口。
* **设备**：用于指代平台上的任何计算或者存储元素，或者计算或者存储元素的组合的通用术语。设备的范例包括中央处理器（CPU）、应用处理器（APU）、嵌入式控制器（EC）、基板管理控制器（BMC）、可信平台模块（TPM）、图形处理器（GPU）、网卡（NIC）、硬盘驱动器（HDD）、固态硬盘（SSD）、只读存储器（ROM）、闪存 ROM 等。
* **设备固件**：仅用于某个特定设备的非宿主处理器固件和扩展 ROM 固件的组合。此固件通常由设备制造商提供。
* **扩展 ROM 固件**：用于指代在宿主处理器上执行的、被扩展设备在启动过程中所使用的固件的外设元件互连标准（PCI）术语。这包括 Option ROM 固件、UEFI 应用程序和 UEFI 驱动程序。扩展 ROM 固件可以作为宿主处理器启动固件的一部分而捆绑，也可以是独立的（例如来自扩展卡）。在此文档中，我们在一般性地指代 Option ROM 固件或者 UEFI 驱动程序和应用程序时使用扩展 ROM 固件这一术语。
* **固件**：用于描述存储于芯片中的任何代码的通用术语，这些代码要么驻留于对应处理器的重置向量（或者等价物），要么作为其他固件的扩展而提供（诸如扩展 ROM 固件）。存储于芯片中的通用目的操作系统在此文档的范围中一般不被看作固件。
* **宿主设备**：辅助共生设备建立满足此文档中的保护、检测和/或恢复指导意见所必需的可信根和信任链的设备。宿主和共生设备之间的功能分配取决于实现。宿主设备自身必须独立满足对其固件的指导意见。注意，这不应该同宿主处理器相混淆。宿主处理器可以作为宿主设备，但是宿主设备不一定是宿主处理器。
* **宿主处理器**：宿主处理器是平台中的主要处理单元，在传统上称为中央处理器（CPU），现在有时也被称为应用处理器（APU）或者系统芯片（SoC）。这是主操作系统（和/或虚拟机监视器）以及用户应用程序所在其上运行的处理单元。这是负责加载并执行宿主处理器启动固件的处理器。
* **宿主处理器启动固件**：用于描述由宿主处理器加载并且执行、为平台提供基本启动能力的固件的通用术语。此类固件包括传统 BIOS、系统 BIOS 和 UEFI，以及其他实现。在传统 BIOS 和 UEFI 之间的区别并不重要的情况下，将会使用宿主处理器启动固件这一术语。在这种区别至关重要的情况下，将会根据实际情况进行指代。扩展 ROM 启动固件也可以被看作宿主处理器启动固件的一部分。扩展 ROM 固件可以被作为宿主处理器启动固件的一部分而嵌入，也可以是独立于宿主处理器启动固件的（例如从扩展卡加载）。宿主处理器启动固件包括可能在运行时可用的固件。
* **不可变的**：不可发生更改的。在此文档的上下文环境中，这仅仅指代不能在现场通过制造商本意中的机制和/或限定的接口进行更改。注意，平台或者设备制造商可能仍然能够通过直接连接到本地（物理）存在的平台或者设备的生产或者服务工具来作出更改。
* **传统 BIOS（基本输入/输出系统）**：用于使用传统 x86 BIOS 架构的 x86 平台的一种宿主处理器启动固件形式。这种形式的宿主处理器启动固件已经或者正在被 UEFI 取代。
* **可变的**：可发生更改的。在此文档的上下文环境中，这仅仅指代能够在现场通过制造商本意中的机制和/或限定的接口进行更改。这样的机制可能要求密码学机制或者无歧义的物理存在。
* **非关键数据**：非关键数据是在加电循环之间持续存在，但是对于设备的启动、运作或者恢复并不具有决定性的可变数据。
* **非宿主处理器**：非宿主处理器是用于描述平台上的任何不是宿主处理器的处理单元（例如微控制器、协处理器等）的通用术语。
* **非宿主处理器固件**：非宿主处理器固件是用于描述被平台上的任何不是宿主处理器的处理单元所使用的固件的通用术语。
* **Option ROM 固件**：用于通常在宿主处理器上执行、在启动过程中被设备使用的启动固件的传统术语。Option ROM 固件可以被包括在宿主处理器启动固件中，也可以由设备（例如扩展卡）独立提供。
* **外设（又称为外部设备）**：外设（又称为外部设备）是物理存在于平台外部并且通过有线或者无线的方式连接到平台的设备。外设由其自身设备构成，它们可能拥有其自身的固件。尽管此文档中的原则和知道意见在概念上也可以同等程度地适用于外设，它们不属于此文档的范围之中。
* **平台**：平台由被组装起来共同工作以带来某种特定计算功能的一个或者多个设备所组成，但是并不包含作为平台中的设备的一部分的固件以外的任何其他软件。平台的范例包括笔记本、台式机、服务器、网络交换机、刀片等。
* **平台管理员权限**：管理平台设备中的固件和关键数据所必需的权限。特别地，这种权限可能是授权固件更新、更改固件配置设置，以及固件恢复操作所需要的。
* **平台管理员**：拥有平台管理员权限的实体。
* **平台固件**：平台上的所有设备固件的组合。在此文档中，平台固件这一术语可以被用于指代平台上所有被设备所使用的固件的组合。
* **主固件镜像**：存储于设备上的可执行代码。主固件镜像的不同部分可以通过不同方式保护。
* **只读存储器（ROM）**：一旦经过初始设置，就不能通过任何机制重写的存储器设备，使得该存储器成为不可变（不可更改）的。
* **具有弹性的**：具有特定性质的系统在干扰发生之前、之中和之后吸收该干扰、恢复到某种可接受的性能级别，并且维持该级别达到一段可接受的时间的能力。
* **可信根（RoT）**：构成了提供一项或者多项安全特定功能，诸如测定、存储、报告、恢复、验证、更新等的基础的元素。RoT 被信任为总是以预期的方式运作，由于它的不当行为不能被检测到，以及它的恰当运作对于提供其安全特定功能至关重要。
* **运行时固件**：用于描述平台上的任何在运行时（在启动完成之后）活动/起作用或者可用的固件的通用术语。
* **软件**：软件由加载操作系统、操作系统和随后由操作系统处理的所有用户应用程序和用户数据所必需的元素构成。参见图 1 以获得图形描述。
* **共生设备**：共生设备是完全或者部分依赖另一个设备（宿主设备）以建立为符合此文档中的保护、检测和恢复指导意见所必需的可信根和信任链的设备。宿主设备和共生设备之间的功能分配取决于实现。例如，宿主设备验证更新并且备份关键数据，而共生设备负责满足所有其他指导意见。共生属性可以具有传递性：一个设备可以是一个宿主设备的共生设备，而这两个设备可以随后作为另一个共生设备的宿主设备，等等。
* **系统**：系统是计算实体的整体，包括 _平台_（硬件、固件）和 _软件_（操作系统、用户应用程序、用户数据）中的所有元素。系统可以被看作逻辑构造（例如软件栈）或者物理构造（例如笔记本、台式机、服务器、网络交换机等）。参见图 1 以获得图形描述。
* **UEFI（统一可扩展固件接口）**：使用统一可扩展固件接口（UEFI）架构（如同 UEFI 论坛所定义）的一种宿主处理器启动固件形式。
* **UEFI 驱动程序**：在启动过程中加载以处理特定硬件部分的独立二进制可执行文件。
* **无歧义的物理存在**：由不能被恶意软件伪造的本地人员指示授权。

# 附录 C——参考文献

* \[1\] D. Cooper, W. Polk, A. Regenscheid, and M. Souppaya, _BIOS Protection Guidelines_, NIST Special Publication (SP) 800-147, National Institute of Standards and Technology, Gaithersburg, Maryland, April 2011, 26pp. [https://doi.org/10.6028/NIST.SP.800-147](https://doi.org/10.6028/NIST.SP.800-147)
* \[2\] A. Regenscheid., _BIOS Protection Guidelines for Servers_, NIST Special Publication (SP) 800-147B, National Institute of Standards and Technology, Gaithersburg, Maryland, August 2014, 32pp. [https://doi.org/10.6028/NIST.SP.800-147B](https://doi.org/10.6028/NIST.SP.800-147B)
* \[3\] Specifications, Unified Extensible Firmware Interface Forum \[Web site\], [http://www.uefi.org/specifications](http://www.uefi.org/specifications) \[accessed 5/2/18\]
* \[4\] TPM Library Specification, Trusted Computing Group \[Web site\], [https://trustedcomputinggroup.org/tpm-library-specification/](https://trustedcomputinggroup.org/tpm-library-specification/) \[accessed 5/2/18\]
* \[5\] S. Bradner, _Key words for use in RFCs to Indicate Requirement Levels_, RFC 2119, Internet Engineering Task Force, March 1997, 2pp, [https://doi.org/10.17487/RFC2119](https://doi.org/10.17487/RFC2119)
* \[6\] U.S. Department of Commerce. _Secure Hash Standard_, Federal Information Processing Standards (FIPS) Publication 180-4, August 2015, 36pp. [https://doi.org/10.6028/NIST.FIPS.180-4](https://doi.org/10.6028/NIST.FIPS.180-4)
* \[7\] U.S. Department of Commerce. _Digital Signature Standard_, Federal Information Processing Standards (FIPS) Publication 186-4, July 2013, 130pp. [https://doi.org/10.6028/NIST.FIPS.186-4](https://doi.org/10.6028/NIST.FIPS.186-4)
* \[8\] E. Barker, _Recommendation for Key Management, Part 1: General_, NIST Special Publication (SP) 800-57 Part 1 Revision 4, National Institute of Standards and Technology, Gaithersburg, Maryland, January 2016, 160pp. [https://doi.org/10.6028/NIST.SP.800-57pt1r4](https://doi.org/10.6028/NIST.SP.800-57pt1r4)
* \[9\] E. Barker, _Recommendation for Obtaining Assurances for Digital Signature Applications_, NIST Special Publication (SP) 800-89, National Institute of Standards and Technology, Gaithersburg, Maryland, November 2006, 38pp. [https://doi.org/10.6028/NIST.SP.800-89](https://doi.org/10.6028/NIST.SP.800-89)
* \[10\] International Council for Systems Engineering, “Resilient Systems Working Group Charter,” November 2011.
* \[11\] R. Ross, R. Graubart, D. Bodeau, and R. McQuaid, _Systems Security Engineering: Cyber Resiliency Considerations for the Engineering of Trustworthy Secure Systems_, NIST Special Publication 800-160 Volume 2 (DRAFT), National Institute of Standards and Technology, Gaithersburg, Maryland, March 2018, 158pp. [https://csrc.nist.gov/CSRC/media/Publications/sp/800-160/vol-2/draft/documents/sp800-160-vol2-draft.pdf](https://csrc.nist.gov/CSRC/media/Publications/sp/800-160/vol-2/draft/documents/sp800-160-vol2-draft.pdf)

