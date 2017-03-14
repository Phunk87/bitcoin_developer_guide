### P2PKH 脚本验证 \| P2PKH Script Validation

Developer Guide - Bitcoin

验证过程需要计算签名脚本和公钥脚本，对于一个P2PKH的交易，支出地址的公钥脚本是如下格式

```
OP_DUP OP_HASH160 <PubkeyHash> OP_EQUALVERIFY OP_CHECKSIG
```

交易的花费者的签名脚本会被验证，并作为脚本开头的前缀。 对于一个P2PKH 交易，签名脚本包括一个secp256k1加密算法的签名和完整的公钥，拼接成以下格式：

```
<Sig> <PubKey> OP_DUP OP_HASH160 <PubkeyHash> OP_EQUALVERIFY OP_CHECKSIG
```

脚本语言是一种类 Forth 栈语言。被设计拥有成无状态和非图灵完备的性质。无状态性保证了一旦一个交易被区块打包，这个交易就是可用的。图灵非完备性（具体来说，缺少循环和goto 语句）使得比特币的脚本语言更加不灵活和更可预测，从而大大简化了安全模型。为了检测交易是不是有效的，从Bob的签名脚本一直到Alice 的公钥脚本依次执行。下面的图示展示了计算一个标准P2PKH 的公钥脚本。

![](/en-p2pkh-stack.png)

签名（来自Bob 的签名脚本）被压入空栈，以为签名只是数据，不需要做任何计算，只是把签名入栈。之后公钥（同样来着签名脚本）被压入堆栈。

* 从Alice 的公钥脚本，开始执行OP\_DUP，OP\_DUP 被压入堆栈，拷贝一份堆栈顶的数据，在这个例子中，指的是拷贝Bob提供 的公钥。

* 接下来执行的运算是 OP\_ HASH160, 把堆栈头的数据进行HASH 运算，在这个例子中，对Bob 提供的公钥进行了HASH运算。

* 接下来Alice 的公钥脚本把Bob在第一笔交易中给他的公钥Hash 压入栈。这时候，已经有了两份Bob 的公钥Hash放置在堆栈的头部。
* 有趣的部分：Alice 的公钥脚本执行 OP\_EQUALVERIFY. OP\_EQUALVERIFY 等价于执行OP\_VERIFY\(未展示\) 后执行 OP\_EQUAL.

OP\_EQUAL \(未展示\)计算堆栈头部的前两个值，在这个例子中，检测了 从Bob 提供的全 公钥生成的公钥Hash 是否和Alice提供的在第一次交易中生成的公钥hash一致。OP\_EQUAL 出栈头部的两个值，压入计算结果：0 （否）和 1（真）。

OP\_VERIFY\(未展示\) 检查了堆栈头的值，如果堆栈头为FALSE， 立刻终止全部计算，交易验证失败。否则，以TRUE 值出栈。

* 最后，Alice’s  的公钥脚本执行 OP\_CHECKSIG, 该操作检测Bob 提供的签名是不是授权了Bob提供的现在认证的公钥。如果签名和公钥匹配，并且使用所有需要签名的数据生成，则OP\_CHECKSIG将值true推送到堆栈的顶部。

如果经过公钥脚本计算，在堆栈顶部不是False 值，那么验证脚本为有效的（证明交易没有其他问题）。

