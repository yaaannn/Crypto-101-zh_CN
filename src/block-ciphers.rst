分组密码
-------------

   Few false ideas have more firmly gripped the minds of so many intelligent men
   than the one that, if they just tried, they could invent a cipher that no one
   could break.

      *David Kahn*

.. _description-1:

说明
~~~~~~~~~~~

分组密码（:term:`block cipher`）是一种允许我们对多个固定长度的块进行加密的算法。
它提供了一个加密函数 :math:`E`，通过一个密钥 :math:`k`，将明文块 :math:`P` 转换成密文块 :math:`C`。

.. math::

   C = E(k, P)

明文和密文块都是比特序列。
它们的大小都是相同的，这个大小是由分组密码固定的：它被称为分组密码的 *块大小* 。
所有可能的密钥的集合称为密钥空间（:term:`Keyspace`）。

一旦我们把所有明文块加密成密文块，之后就必须再次解密以恢复原来的明文块。
这是用一个解密函数 :math:`D` 来完成的，它将密文块 :math:`C` 和密钥 :math:`k` （与加密块所用的密钥相同）作为输入，并产生原始的明文块 :math:`P`。

.. math::

   P = D(k, C)

或者，以分组的形式直观表示：

.. figure:: Illustrations/BlockCipher/BlockCipher.svg
   :align: center

分组密码是对称密钥加密（:term:`symmetric-key encryption`）方案的一个例子，也称为私密密钥加密（:term:`secret-key encryption`）方案。
这意味着加密和解密都使用同一个秘钥。我们将在本书后面与公钥加密（:term:`public-key encryption`）算法进行对比，后者的加密和解密使用不同的密钥。

分组加密是一种 *加密置换*。它是一种 *置换*，因为分组加密将每一个可能的块映射到其他块上。
它也是一个 *加密的置换*，因为密钥确切地决定了块之间的映射。
它是一个置换这很重要，因为接受者也需要能够将每块映射回原来的块，只有当它是一对一的时候，你才能做到这一点。


我们将通过一个不切实际的，只有4比特块大小的分组密码来说明这一点， :math:`2^4 = 16` 种可能的区块。
由于每个区块都映射到一个十六进制数字，我们用这个数字来表示区块。
:numref:`fig-BlockCipherBlocks` 说明了密码操作的区块。


.. _fig-BlockCipherBlocks:

.. figure:: Illustrations/BlockCipher/AllNodes.svg
   :align: center

   由分组密码操作的所有16个节点，每个节点由一个十六进制数字指定。


一旦我们选择了一个秘密密钥，分组加密就会用它来确定任何给定块的加密内容。
我们将用一个箭头来说明这种关系：箭头开头的区块，在密钥 :math:`k` 下使用 :math:`E` 加密，被映射到箭头末端的区块。


.. _fig-BlockCipherEncryption:

.. figure:: Illustrations/BlockCipher/Encryption.svg
   :align: center

   分组加密在特定的密钥下产生的加密排列 :math:`k`。

在 :numref:`fig-BlockCipherEncryption` 中，注意到排列不仅仅是一个大环：一个由7个元素组成的大环，还有几个小环，分别是4、3和2个元素。
一个元素加密为它自己加密也是完全可能的。
这是在选择随机排列时可能出现的，这可能就是分组加密的做法，它并不是来展示分组加密的一个错误。

当你在解密而不是加密的时候，分组加密只是计算逆向置换。在 :numref:`fig-BlockCipherDecryption` 中，你可以看到我们得到了同样的说明，只是所有的箭头都是朝另一个方向。


.. _fig-BlockCipherDecryption:

.. figure:: Illustrations/BlockCipher/Decryption.svg
   :align: center

   分组加密在同一密钥下产生的解密置换 :math:`k`：是 加密置换反向，即所有的箭头都被反转了。

要知道哪个区块映射到哪个其他区块，唯一的方法就是知道密钥。
不同的密钥将导致一组完全不同的箭头，你可以在 :numref:`fig-BlockCipherEncryptionDifferentKey` 中看到。

.. _fig-BlockCipherEncryptionDifferentKey:

.. figure:: Illustrations/BlockCipher/Encryption2.svg
   :align: center

   分组加密在其他密钥下产生的一种加密置换方式。

在这个插图中，你甚至会注意到，有两个长度为1的排列组合：一个元素映射到自身。
这是在选择随机排列时可以预期的事情。

知道一个给定密钥的一堆（输入、输出）对，不应该从中得到任何关于该密钥 [#]_ 下的其他（输入、输出）对的信息。
只要我们谈论的是一个假设的完美的分组加密，除了“暴力破解”密钥之外，没有其他更简单的方法来解密一个组：即只有一个一个尝试，直到找到正确的那一个。

.. [#]
   细心的读者可能已经注意到了，这在极端情况下是有特例的：如果你知道所有的映射对，但有一个不知道，那么你就会通过排除法知道最后一个。

我们的玩具演示分组加密， 每组只有4位，也就是每组有 :math:`2^4 = 16` 种可能。
真正的、现代的分组加密有更大的区块大小，如128位，或 :math:`2^{128}` （比 :math:`10^{38.5}` 略多）可能的区块。
数学告诉我们，一个 :math:`n` 元素集有 :math:`n!` （读作 :math:`n` 阶乘）不同的排列组合。
它被定义为从1到并包括 :math:`n` 的所有数字的乘积。

.. math::

   n! = 1 \cdot 2 \cdot 3 \cdot \ldots \cdot (n - 1) \cdot n

阶乘的增长速度快得惊人。比如 :math:`5! = 120` ， :math:`10! = 3628800` ，而且速度还在继续增加。
组大小为128位的密码的组集的排列个数为 :math:`(2^{128})!`。
只是 :math:`2^{128}` 已经很大了（需要39位数字才能写下来），所以 :math:`(2^{128})!` 是一个令人匪夷所思的巨大数字，无法理解。
常见的密钥大小只在128到256位之间，所以一个密码能进行的排列组合只有 :math:`2^{128}` 和 :math:`2^{256}` 之间。
这只是所有可能的分组组合中的一小部分，但没关系：这一小部分还远远没有小到让攻击者可以尝试所有的组合。"

当然，只要不会牺牲上述任何一个特性前提下，分组加密应该尽可能地易于计算。

AES
~~~

目前最常用的分组加密是AES。

与它的前身DES（我们将在下一章中详细介绍）相反，AES是在公开征集提案后，通过公开的、经过同行评审的竞赛选出的。
这个竞选包括几轮，所有的参赛者都会被介绍，接受广泛的密码分析，并进行投票。
AES程序在密码学家中受到好评，类似的程序一般被认为是选择密码标准的首选方式。

在被选为高级加密标准之前，该算法被称为Rijndael，这个名字来源于设计该算法的比利时密码学家的两个姓氏。
Vincent Rijmen和Joan Daemen。
Rijndael算法定义了一个分组密码家族，其组大小和密钥大小可以是128位和256位之间的32位的任何倍数。
:cite:`daemen:aes` 当Rijndael通过FIPS标准化过程成为AES时，参数被限制在128位的组大小和128、192和256位的密钥大小。
:cite:`fips:aes`

目前还没有针对AES的实用攻击。
虽然在过去的几年里有一些发展，但大多数涉及到相关密钥攻击 :cite:`cryptoeprint:2009:317` ，其中一些只涉及到AES的简化版 :cite:`cryptoeprint:2009:374` 。
[#]_

.. [#]
   对称算法通常依靠一个轮函数来重复多次。通常每次调用都会涉及到一个从主密钥衍生出来的“轮密钥”。
   简化版本故意更容易被攻击。这些攻击可以深入了解全加密版本的抗性。

   相关的密钥攻击涉及到用一些特定的数学关系对AES在几种不同密钥下的表现进行一些预测。
   这些关系相当简单，比如用攻击者选择的常数进行XOR。
   如果允许攻击者用这些相关密钥加密和解密大量的区块，他们就可以尝试恢复原始密钥，其计算量比通常破解它所需的计算量要少得多。

   由于理论上理想的分组密码不会受到相关密钥攻击的影响，这些攻击并不被认为是实际问题。
   在实践中，密码密钥是通过一个密码学上安全的伪随机数生成器，或安全的 :term:`key agreement` 方案或密钥推导方案（我们将在后面看到更多关于这些的内容）生成的。
   因此，偶然选择两个这样的相关密钥的几率是不存在的。
   从学术的角度来看，这些攻击是很有趣的：它们可以帮助提供密码工作原理的见解，指导密码学家设计未来的密码和针对当前密码的攻击。

A closer look at Rijndael
^^^^^^^^^^^^^^^^^^^^^^^^^
.. canned_admonition::
   :from_template: advanced

AES consists of several independent steps. At a high level, AES is a
:term:`substitution-permutation network`.

Key schedule
''''''''''''

AES requires separate keys for each round in the next steps. The key
schedule is the process which AES uses to derive 128-bit keys for each
round from one master key.

First, the key is separated into 4 byte columns. The key is rotated and
then each byte is run through an S-box (substitution box) that maps it
to something else. Each column is then XORed with a round constant. The
last step is to XOR the result with the previous round key.

The other columns are then XORed with the previous round key to produce
the remaining columns.

SubBytes
''''''''

SubBytes is the step that applies the S-box (substitution box) in AES.
The S-box itself substitutes a byte with another byte, and this S-box is
applied to each byte in the AES state.

It works by taking the multiplicative inverse over the Galois field, and
then applying an affine transformation so that there are no values
:math:`x` so that :math:`x \xor S(x) = 0` or :math:`x \xor S(x)=\texttt{0xff}`.
To rephrase: there are no values of :math:`x` that the substitution box maps to
:math:`x` itself, or :math:`x` with all bits flipped. This makes the cipher
resistant to linear cryptanalysis, unlike the earlier DES algorithm,
whose fifth S-box caused serious security problems.  [#]_

.. figure:: Illustrations/AES/SubBytes.svg
   :align: center

.. [#]
   In its defense, linear attacks were not publicly known back when DES
   was designed.

ShiftRows
'''''''''

在将SubBytes步骤应用于该组的16个字节后，AES将 :math:`4 \times 4` 数组进行交换：

.. figure:: Illustrations/AES/ShiftRows.svg
   :align: center

MixColumns
''''''''''

MixColumns multiplies each column of the state with a fixed polynomial.

ShiftRows and MixColumns represent the diffusion properties of AES.

.. figure:: Illustrations/AES/MixColumns.svg
   :align: center

AddRoundKey
'''''''''''

As the name implies, the AddRoundKey step adds the bytes from the round
key produced by the key schedule to the state of the cipher.

.. figure:: Illustrations/AES/AddRoundKey.svg
   :align: center

DES and 3DES
~~~~~~~~~~~~

DES是被广泛使用的最古老的分组密码之一。
它于1977年作为FIPS官方标准发布。
它不再被认为是安全的，主要是因为它的密钥大小只有56位。（DES算法实际上需要一个64位的密钥输入，但剩下的8位只用于奇偶校验，并立即被丢弃）。
它不应该在新系统中使用。
在现代硬件上，DES可以在不到一天的时间里被暴力破解。 :cite:`sciengines:breakdes`

为了延长DES算法的寿命，使大部分已花费的硬件开发工作得以重用，人们想到了3DES：一种先对输入进行加密，然后解密，然后再次加密的方案：

.. math::

   C = E_{DES}(k_1, D_{DES}(k_2, E_{DES}(k_3, p)))

这个方案提供了两点改进：

-  通过应用三次算法，密文就很难直接通过密码分析进行攻击
-  通过可以选择使用分布在三个密钥上的更多总密钥，所有可能的密钥集变大很多，使暴力破解变得不切实际。

三个密钥都可以独立选择（产生168个密钥位），或者 :math:`k_3 = k_1` （产生112个密钥位），或者 :math:`k_1 = k_2 = k_3` ，当然，这只是普通的DES（有56个密钥位）。
在最后一个键位选项中，中间的解密会把第一次的加密反过来，所以你真正得到的只是最后一次加密的效果。
这是为现有DES系统提供的一种向后兼容模式。
如果3DES被定义为 :math:`E(k_1, E(k_2, E(k_3, p)))` ，那么对于需要与DES兼容的系统，就不可能使用3DES实现。
这对硬件实现尤其重要，因为在硬件实现中，并不总是能够在主要的3DES接口旁边提供一个次要的、常规的“单一DES”接口。

已知对3DES的某些攻击会降低其有效安全性。
虽然用第一种密钥选项破解3DES目前还不切实际，但对于任何现代密码系统来说，3DES都是一个糟糕的选择。
安全系数已经很小，而且随着密码攻击的改进和处理能力的增长，安全系数还在继续缩小。

有更好的替代品，如AES。它们不仅比3DES更安全，而且通常也快得多。在相同的硬件和相同的工作模式（ :term:`mode of operation` ）（我们将在下一章解释这意味着什么），AES-128每字节只需要12.6个周期，而3DES每字节需要134.5个周期。
:cite:`cryptopp:bench` 先不说从安全的角度来看更差，它确实慢了一个数量级。

虽然DES的更多迭代可能会增加安全系数，但并没有实际使用。
首先，这个过程从未被标准化超过三次迭代。
另外，随着增加更多的迭代，性能只会变得更差。
最后，增加密钥位的安全回报率越来越低，只是随着密钥位数的增加，所产生的算法的安全级别增加的幅度越来越小。
虽然带密钥选项1的3DES的密钥长度为168位，但有效安全级别估计只有112位。

尽管3DES在性能上明显差了很多，在安全性上也略差，但3DES仍然是金融行业的主力军。
由于已经有了大量的标准，而且新的标准还在不断地被创造出来，在这样一个技术极其保守的行业里，Fortran和Cobol仍然在大规模的大型机上称王称霸，它可能会在未来的很多年里继续被使用，除非有一些大的密码分析的突破，威胁到3DES的安全性。

.. _remaining-problems-1:

遗留问题
~~~~~~~~~~~~~~~~~~

即有了分组密码，仍然存在一些未解决的问题。

例如，我们只能发送长度非常有限的消息：分组加密的组长度。
显然，我们希望能够发送更长的消息，或者说，理想情况下，发送大小不确定的流。我们将用一个 :ref:`流加密 <stream-ciphers>`
来解决这个问题。

虽然我们已经大大减少了密钥的大小（从一次性密码本方案下发送的所有数据的总大小到大多数分组加密的几个字节），但我们仍然需要解决在不安全的信道上商定这几个密钥字节的问题。
我们将在后面的一章中用一个 :ref:`密钥交换协议 <key-exchange>`
来解决这个问题。