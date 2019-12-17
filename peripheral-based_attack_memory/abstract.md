# 检测针对宿主内存的基于外设的攻击

Patrick Stewin

# 摘要

对手可以通过在目标平台上部署 rootkit 技术以便以某种隐秘的方式持续攻击计算机系统。行业和政治间谍活动、对用户的监控，以及引导网络犯罪等行为要求对计算机系统进行隐秘攻击。利用某种 rootkit 技术意味着，所实现的攻击代码中的一部分负责隐藏此次攻击。被加载到诸如网卡或者特殊的微控制器等外设的攻击代码目前成为了 rootkit 进化的顶峰。本工作检视了宿主计算机上的此类基于外设的隐秘攻击。外设拥有一块专用处理器以及专用的运行时内存以处理其任务。这意味着这些外设实质上是一个独立的系统。攻击者得益于这种隔离。外设通常通过宿主的主内存同宿主进行通讯。攻击者利用了这一事实。宿主的所有运行时数据存在于主内存中，这包括密码学密钥、口令、已打开的文件以及其他敏感数据。攻击者只需定位这些数据。随后，攻击者可以利用外设的直接内存访问机制暗中读取和修改这些数据。这使得绕过诸如业界最先进的反病毒软件和加固的现代操作系统内核等安全软件成为可能。

检测这样的攻击是本工作的目标。基于独立微控制器的隐形恶意软件被实现为引导技术分析。此恶意软件的概念验证称为 DAGGER，它来自于 _Direct memory Access based keystroke code loGGER_（基于直接内存访问的击键码记录器）。对此恶意软件的开发和分析揭示了基于外设的恶意软件的重要属性。其检测程序称为 BARM——_Bus Agent Runtime Monitor_（总线代理运行时监视器）。此检测程序揭示了通过利用某些硬件属性对宿主的主内存进行的基于外设的隐秘攻击。一种永久的并且高效利用资源的测定策略保证了此检测程序同时还能检测瞬时攻击。如果所应用的测定策略只会在特定的时间点进行测定，则此类瞬时攻击将会成为可能。攻击者可以如此利用此种测定策略，通过在两次测定之间对系统进行攻击，并且在系统被测定之前销毁所有进攻痕迹。对于之前提出的预防性保护方式，即输入/输出内存管理单元，此检测程序代表了一种替代解决方案。由于实践方面的原因，之前提出的方法不一定是高效的。这一事实再加上由基于外设的恶意软件所带来的威胁共同要求本工作所呈现的替代检测方案。此检测程序不仅能够揭示攻击，同时能够终止该恶意设备。BARM 立即检测到并且阻止由 DAGGER 引导的攻击。其性能开销可以忽略。更进一步地，BARM 能够向外部平台报告宿主的主内存是否受到了外设的攻击。

# 与本论文相关的发表

本论文呈现的工作带来了下列通过同行评审的发表：

* _Understanding DMA Malware_, Patrick Stewin and Iurii Bystrov, DIMVA2012 Proceedings of the 9th Conference on Detection of Intrusions and Malware & Vulnerability Assessment, Heraklion, Crete, Greece, July 26-27th, 2012 (\[参见 123\] / 第 4 章)
* Extended Abstract – _Poster: Towards Detecting DMA Malware_, Patrick Stewin, Jean-Pierre Seifert, Collin Mulliner, CCS2011 Proceedings of the 18th ACM Conference on Computer and Communications Security, 2011 (\[参见 126\] / 第 4 章)
* _A Primitive for Revealing Stealthy Peripheral-based Attacks on the Computing Platform’s Main Memory_, Patrick Stewin, RAID2013 Proceedings of the 16th International Symposium on Research in Attacks, Intrusions and Defenses (RAID), St. Lucia, October 23-25, 2013 (\[参见 122\] / 第 5 章)

下列通过同行评审的发表根据第 6 章进行了更新，以考虑到基于 DMA 的恶意软件的场景，这也是本论文关注的焦点：

* _Beyond Secure Channels_, Yacine Gasmi, Ahmad-Reza Sadeghi, Patrick Stewin, Martin Unger, N. Asokan, STC2007 Proceedings of the 2007 ACM Workshop on Scalable Trusted Computing, 2007 (\[参见 52\])
* _An Efficient Implementation of Trusted Channels based on OpenSSL_, Frederik Armknecht, Yacine Gasmi, Ahmad-Reza Sadeghi, Patrick Stewin, Martin Unger, Gianluca Ramunno, Davide Vernizzi, STC2008 Proceedings of the 3rd ACM Workshop on Scalable Trusted Computing, 2008 (\[参见 10\])

