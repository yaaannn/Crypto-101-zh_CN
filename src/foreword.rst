前言
========

关于本书
---------------

   许多从事密码学工作的人对实际的应用问题并没有深入的关注。他们只是想找到一些足够深度的东西以便来撰写论文。

      *惠特菲尔德·迪菲*

本书旨在为任何水平的程序员介绍密码学。 这是作者在PyCon 2013大会上同名演讲的延续。

本书的结构非常相似：它从非常简单的原语开始，逐步介绍新的，并说明为什么它们是必要的。
最终，所有这些一起组合成完整的、实用的密码系统，如TLS、GPG和 :term:`OTR`。

本书的目标不是让所有人都成为密码学家或安全研究人员。
本书的目标是以鸟瞰似地理解完整的密码系统是如何工作的，以及如何在实际软件中应用它。

本书所附的练习侧重于通过破解低安全等级的系统来教授密码学。这样一来，你就不仅仅是“知道”某些特定的东西被破解了；
你将确切地知道它是如何被破解的，而你自己，只需要一些空闲时间和你最喜欢的编程语言，就可以破解它们。
通过知道这些表面上安全的系统实际上是如何被完全破解的，你将理解 **为什么** 所有这些原语和构造对于完整的密码系统是必要的。
希望这些练习也会让你以后对各种形式的DIY加密方法有充分的不信任感。

长期以来，密码学一直被认为是专家的专属领域。从多年来我们看到的许多大公司和小公司的内部泄密事件来看，这种做法显然是弊大于利。
我们不能再把这两个世界严格分开了。我们必须将它们联合成一个世界，让所有的程序员都接受信息安全的基础教育，这样他们就可以和信息安全专业人员一起为大家生产更安全的软件系统。
这并不会使渗透测试人员和安全研究人员等人变得过时或降低价值，事实上恰恰相反。
通过提高所有程序员对安全问题的意识，专业安全审计的需求将变得更多，而不是减少。


本书希望成为一座桥梁：让任何领域或专业的日常程序员，学到足够的密码学知识来完成他们的工作，或者也许只是满足他们的好奇心。


高级部分
-----------------

这本书的目的是为程序员提供一个密码学实用指南。
为了实现这一目标，有些章节进超出本需深度。
无论如何，它们都在书中，以防你好奇；但我通常建议跳过这些部分。
它们会被这样标记：


.. declare_admonition::
   :name: advanced
   :type: attention

   .. figure:: ./Illustrations/Propeller/Propeller.svg
      :width: 80
      :align: left

   This is an optional, in-depth section. It almost certainly won't help you write better software,
   so feel free to skip it. It is only here to satisfy your inner geek's curiosity.

.. canned_admonition::
   :from_template: advanced

创作
-----------

整个Crypto 101项目都在GitHub上以 ``crypto101`` 组织的名义公开创作，包括 `这本书
<https://www.github.com/crypto101/book/>`_。

这是本书的一个早期预发布版。我们非常感谢您的所有问题、意见和bug报告。
如果您看完本书后有什么不明白的地方，或者觉得某句话用词特别笨拙， *这是一个bug* ，我非常希望能够修复它!
当然，如果我从没有听到你的问题，那对我来说很难处理......

您正在阅读的本书的副本是基于哈希值为 |version| 的git commit，也称为 |release| 。

鸣谢
---------------

如果没有许多人的支持和贡献，本书的第一次公开发行都不可能完成。
有人审阅了文本，有人贡献了技术检查，还有人为最初的演讲提供了帮助。
排名不分先后：

-  My wife, Ewa
-  Brian Warner
-  Oskar Żabik
-  Ian Cordasco
-  Zooko Wilcox-O'Hearn
-  Nathan Nguyen (@nathanhere)

公开发布后，又有许多人提出了修改意见。我要特别鸣谢以下人员（同样排名不分先后）：

-  coh2, for work on illustrations
-  TinnedTuna, for review work on the XOR section (and others)
-  dfc, for work on typography and alternative formats
-  jvasile, for work on typefaces and automated builds
-  hmmueller, for many, many notes and suggestions
-  postboy (Ivan Zuboff), for many reported issues
-  EdOverflow, for many contributions
-  gliptak (Gábor Lipták) for work on automating builds,

以及众多人员为拼写，语法和内容改进做出贡献的。谢谢你们！
