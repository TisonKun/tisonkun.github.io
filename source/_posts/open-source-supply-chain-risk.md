---
title: 开源软件有断供的风险吗？
date: 2024-11-17
tags:
    - 开源
categories:
    - 夜天之书
---

近期，Linux 上游因为受美国出口管制条例的影响，将移除部分开发者的 MAINTAINER 权限，引起了新一轮对开源依赖的重新评估。

关于其中开源精神和社群治理的讨论，卫 Sir 的两篇文章已经讨论得比较清楚（见尾注）。本文主要从软件供应链的角度出发，回应对“开源软件的断供风险”的担忧。

简言之，**开源协议只是向用户授权自由使用特定版本源代码**。除此以外，大部分开源协议都**明确声明不提供维保，更不承诺有一个长期迭代的上游分支**。

<!-- more -->

## 开源协议提供了什么样的开源软件？

大部分人对开源协议的了解是不准确的。人们往往望文生义的认为开源软件只意味着源代码公开，至于软件的用途和使用限制，都是可以商议的。

严格意义上的[开源定义](https://opensource.org/osd)由开源促进会（OSI）提供，它定义了开源软件的分发条款必须符合的若干个标准，此外才是可以商议的部分。我们常见的 MIT License 为例，先读一遍协议原文，看看 MIT License 到底以什么形式分发软件。

我们采用开放原子开源基金会[“源译识”](https://www.openatom.org/journalism/detail/O9pwWd2ZeYlD)项目的中英对照翻译成果：

> Copyright [YEAR] [COPYRIGHT HOLDER]
>
> 版权所有 [年份] [版权持有人]
>
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> 特此向获得本软件及相关文档（合称“本软件”）副本的任何人免费授予不受限制地利用本软件的许可，包括而不限于：使用、复制、修改、合并、发布、分发、分许可和/或销售本软件副本，并允许本软件的接收者也获得前述许可，但须遵守以下条件：
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> 以上版权声明及本许可声明应包含在本软件的所有副本或主要部分中。
>
> THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
>
> 本软件系“按原样”提供，不包含任何形式的明示或默示保证，包括但不限于适销性、特定目的适用性及不侵权的保证。在任何情况下，无论是在合同、侵权或其他案件中，作者或版权持有人均不对因本软件、或因本软件的使用或其他利用而引起的、引发的或与之相关的任何权利主张、损害赔偿或其他责任承担责任。

MIT License 的条款包含了所有常见开源协议都具备的两大特征。第一个是授予获得以本协议许可的软件的任何人几项基本权利，主要是任意使用、任意修改和任意分发。第二个是强调该软件“按原样”（AS IS）提供，没有任何维护保障服务，也不承担任何用户使用软件带来的责任。

这两个条款所基于的开源精神，是软件作者已经无偿将代码公开发布并允许你自由使用、修改和重新分发了，那么用户也不应该再强求软件作者承担额外的责任，包括持续维护软件，或必须处理用户使用软件产生的问题。

此外，不同于朴素理解下，“一个软件是 MIT License 许可的开源软件”，意味着它将会以 MIT License 持续发布新版本，实际上，软件作者有权以任何协议发布其代码，而开源软件协议也只绑定在软件的特定发布版本上。

因此，我们可以看到，开源协议本质上只是绑定在特定版本软件上的一系列分发条款，或者说，开源协议本身就是对一个代码快照进行许可。在这种情况下，被“提供”的软件就是这个快照本身，而开源协议授予的一系列基本权利是不可撤销的。在这个维度下，**“开源断供”从未发生过**。以多次变更协议的 Redis 为例，今天全球用户仍然能自由使用其最后一个以 3-Clause BSD License 许可的版本（7.2.5）。

## 如何自己维护开源依赖？

既然从开源协议授予用户的权利，以及开源协议中大多包含的免责协议角度看，“开源断供”从未发生，那么甚嚣尘上的对于“开源软件的断供风险”的担忧到底指的是什么呢？应该说，这种担忧主要是对开源软件过度期待带来的误解。

今天，任何现实世界的应用软件都不可能脱离开源软件实现。换句话说，任何你实际使用的软件，都或多或少的依赖了开源软件。例如，只要你的应用涉及 TLS 网络通信，最常用的 OpenSSL 软件库就是一个开源软件；任何 Java 应用只要有输出日志的需求，很大概率就会依赖 Apache 软件基金会的开源软件 Log4j 等。

从软件供应链的角度来看，开源软件充满了终端应用的整个供应网络。上面提到的两个开源软件，分别出过 [Heartbleed 安全漏洞](https://heartbleed.com/)和 [Log4Shell 安全漏洞](https://en.wikipedia.org/wiki/Log4Shell)，影响了数以千万计的在线应用。

好在开发这两个软件的开源社群对安全漏洞都能做到快速响应，第一时间就提供了修复补丁。所有用户企业得以在第一时间自检是否收到漏洞影响并打上补丁修复。

现在，我们考虑到这些修复补丁是以新版本发布来提供的，按照上面的讨论，这一新版本其实有可能并不以开源协议来提供。举一个实际的例子，如果一个企业用 Akka 开发了核心业务系统，今年 Akka 归属的商业公司 Lightbend 变更了 Akka 的协议，后续 Akka 的安全漏洞补丁许多就只以新的专有协议发布。

这里就出现了“开源断供”的风险，即用户使用了开源软件，一旦该软件出现问题，上游有能力修复的情况下，出于商业考量或法律约束，不向特定用户提供修复版本。换句话说，**开源软件的用户不能想当然地认为开源软件必定有人维护，且该软件的后续版本一定会以开源协议提供**。

因此，企业开发和使用软件时，必须厘清软件的开源依赖，判断哪些核心依赖需要维护保障，进而采取相应措施。

鉴于开源软件供应链无处不在的影响，市场上出现了一系列分析软件依赖的工具和标准：

* [CycloneDX](https://github.com/CycloneDX)
* [FOSSA](https://fossa.com/)
* [SCANOSS](https://www.scanoss.com/)
* [SPDX®](https://spdx.dev/)
* [清源 SCA](https://www.sectrend.com.cn/)

这些工具大多提供为应用软件生成软件物料清单（Software Bill of Materials, SBOM），即罗列出软件所有依赖项的名字、协议属性和代码数字签名等等。这应当会成为未来软件供应链一个必然的趋势，欧盟今年出台的《网络弹性法案》就有此要求，从制造业的发展来看，物料清单也是产业发展成熟的一个最佳实践。

![SBOM 示例片段](sbom-example.png)

## 如何获得有维保的开源软件？

能够分析清楚自己开发和使用应用软件所依赖的开源软件之后，下一步就是如何获得关键依赖的维护保障。

前文已经说明，常见的开源协议都是不提供维护保障的，甚至这些协议都会有专门的免责声明和责任限制条款。因此，单纯祈祷开源软件的开发者持续保持热情，响应问题发布版本，是不可靠的。

另一方面，今天任何人都不可能完全不依赖开源软件开发一个新应用，甚至任何新应用当中绝大部分依赖都是开源依赖。因此，为了避免所谓“开源断供”的风险而选择由公司承担所有依赖代码的编写工作，是绝无可能的。没有任何一家公司能够负担得起这样的研发成本。

因此，使用开源软件，并确保核心依赖得到某种形式的维护保障，就是企业用户必须考虑的问题。我们可以把开源依赖分成四类：

1. 稳定的依赖。依赖库本身并不复杂或完成度极高，在可预见的未来没有任何迭代需求。例如 Hash 算法的实现或特定数据结构的软件库等。这类依赖只需下游用户固定住一个版本即可高枕无忧。甚至可以说最担心的就是上游没事找事胡乱迭代，下游激进跟进版本以后出现故障。例如各种 npm 生态种的迷你库曾经引发的互联网风暴。
2. 可靠的依赖。例如前文提到的 OpenSSL 和 Log4Shell 等，虽然它们都出现过严重的安全漏洞，但是软件开发总是要有漏洞的，这两个社群能够即时发布开源的补丁以供下游使用，这样的依赖就是可靠的。基石性的开源软件往往需要十分可靠才能得到大范围应用，例如 Linux 和 Kubernetes 等等。当然，依赖是否可靠也是动态变化的，例如维护人员的变动或者去世，还有维护组织经营状况和所属环境的改变等等。
3. 可替换的依赖。如果一个开源依赖既不稳定，也就是需要不断迭代以适应需求或使漏洞尽量收敛，又不可靠，也就是不存在一个可持续的上游社群维护，那么企业可以放心使用这一依赖的唯一出路，就是确保该依赖是可以替换的。换句话说，一旦这个开源依赖出现问题，可以替换成另一个没有问题的开源软件，或者由公司员工制作一个替代软件，或者向供应商采购替代软件。
4. 风险。除了以上三类依赖，其余的软件都是有风险的。它们既不稳定，也不可靠，一旦出现问题，公司也没有任何替换的预案。

这样分类过后，我们可以清楚的看到，公司要想获得有维保的开源软件，主观能动的解决方案，就是确保雇佣的员工能够兜底核心依赖，或者从供应商采购维保服务或替代软件。无论哪种方式，都需要企业支付对应的成本。

因此，企业要想安心使用开源软件，首先需要建立起来的认识就是，**开源依赖总是存在于软件供应链上，保障开源依赖的供应链安全是有成本的**。

在此基础上，根据自身应用的实际形态和复杂度，衡量成本，相应地选择（1）雇佣软件工程师维护（2）采购供应商的服务或软件；或者，也可以（3）直接跟开源软件的作者签订协议或提供赞助，确保或促进上游的可靠性、可持续性。

## Linux 基金会近期事件中的“开源断供”风险

其实，前段时间 Linux 基金会移除 Linux 项目中特定开发者的 MAINTAINERS 权限，跟上面分析的“开源断供”风险还有一些不同。

首先，根据目前的信息，Linux 基金会实际做的操作是根据一份美国政府的制裁名单，确保被制裁的个人或为被制裁企业提供服务的个人不出现在 MAINTAINER 列表上。这在规则上，并不影响 Linux 项目接收这些人提交的代码补丁。此外，被制裁的个人和企业实际上仍然可以自由地使用 Linux 软件。从供应链角度上看，没有直接的“断供”风险。

但是，这样的行为对特定下游用户的使用仍然是有实际影响的。例如，移除特定 MAINTAINERS 可能会导致 Linux 的某些模块现在事实上处于无人维护的状态，因此，原本将这些模块视为可靠依赖的下游，将不得不重新评估如何处理对相关模块的依赖。此外，企业由于受到制裁，而无法将任何员工培养成关键开源项目的维护者，可能会严重影响企业采用该开源项目的成本评估。这些就是更加复杂而大部分企业暂时遇不到的情况了，本文不做展开讨论。

## 尾注

卫 Sir 关于 Linux 基金会移除 MAINATINER 事件的相关评论文章如下：

* [Linux 移除部分俄罗斯维护者，违反开源和自由软件精神吗？](https://mp.weixin.qq.com/s/w1MDj-2A-EKZjSv-I-zIpQ)
* [Linus 到底违反了什么？](https://mp.weixin.qq.com/s/RpRNbLHQvzVEFxWZR3w93Q)

此外，大部分人对于开源理解的种种问题，实际上都可以通过阅读开源协议、开源定义来解决。我在日常交流中发现，绝大部分开发者和软件使用者根本没读过开源协议的原始文本，全靠各种二手信息、一图流懒人包，甚至一句话、一个词概括来了解某个开源协议的内涵。这不仅会导致“开源断供”式的误解，也可能导致近期另一个热点事件上出现的关于开源与营利，开源的产权保护方面的一系列误解。

建议各位读者在讨论开源问题时都先尝试阅读理解相关材料的原文。卫 Sir 出品的一系列人话解读开源协议文章就是一个很好的起点。
