### 标准交易 \| Standard Transactions

在早期的几个比特币版本中发现几个严重的漏洞后，加入了一个检测的操作。只有当他们的公钥脚本和签名脚本与一组被认为是安全的模板匹配时，并且其余交易没有违反执行良好网络行为 的另一组规则，才接受来自网络的交易。这个操作名为 isSantard（）测试，通过该测试的交易称为标准交易。

那些没有通过测试的，被称为非标准交易，他们 可能被未使用比特币 core 开发组的默认设置的比特币节点所接受，如果他们包含在区块内，这些交易应该避免进行IsStandard 检测和被处理。

除了增加了通过免费广播有害交易来攻击比特币的困难度，标准交易检测可以防止用户创造阻碍将来增加新的交易特性的交易。比如说，每个交易包括版本号 - 如果用户开始任意改变版本号，则它将作为用于引入向后不兼容特征的工具变得无用。

#### 支付到公钥哈希\(P2PKH\)\|Pay To Public Key Hash \(P2PKH\)

P2PKH 是最常见的公钥脚本形式，用来发起向多个或者一个地址的支付。

```
Pubkey script: OP_DUP OP_HASH160 <PubKeyHash> OP_EQUALVERIFY OP_CHECKSIG
Signature script: <sig> <pubkey>
```

#### 支付到脚本公钥\|Pay To Script Hash \(P2SH\)

P2SH用来向一个脚本hash 发起交易。每一个标准公钥脚本可以视为以一个P2SH 兑换脚本，但是，在实践中，直到更多的交易类型被认为是标准类型，只有多重签名公钥脚本是合理的。

```
Pubkey script: OP_HASH160 <Hash160(redeemScript)> OP_EQUAL
Signature script: <sig> [sig] [sig...] <redeemScript>
```

#### 多重签名脚本\|Multisig

尽管P2SH 多重签名脚本一般用于多重签名的交易，但是这个基础性的脚本也可以用于这种场景：当一个UTXO被使用之前，需要多重签名验证。

多重签名公钥脚本可以一般称为 m-of-n，至少需要m 个匹配公钥，n提供的公钥总数。m 和n 都应当根据需要的数量进行从`OP_1`到`OP_16`运算。

原始的比特币实现中存在一个错位错误，因此，出于兼容性原因，[`OP_CHECKMULTISIG`](https://bitcoin.org/en/developer-reference#term-op-checkmultisig)实际上在堆栈中消耗了m+1个值，因此签名脚本中的secp256k1签名列表必须以额外的值开头（`OP_0`），它将被消耗但不被使用。

这个签名脚本必须对应的公钥脚本中出现的公钥顺序，详细细节参见[`OP_CHECKMULTISIG`](https://bitcoin.org/en/developer-reference#term-op-checkmultisig)。

```
Pubkey script: <m> <A pubkey> [B pubkey] [C pubkey...] <n> OP_CHECKMULTISIG
Signature script: OP_0 <A sig> [B sig] [C sig...]
```

尽管这不是一个单独的交易类型，但是他使用了P2SH 实现了2-of-3 的多重签名：

```
Pubkey script: OP_HASH160 <Hash160(redeemScript)> OP_EQUAL
Redeem script: <OP_2> <A pubkey> <B pubkey> <C pubkey> <OP_3> OP_CHECKMULTISIG
Signature script: OP_0 <A sig> <C sig> <redeemScript>
```

#### 公钥\|Pubkey

公钥输出是一个[P2PKH 公钥脚本](https://bitcoin.org/en/glossary/p2pkh-address)的简化形式，但是安全性不及P2PKH，大部分新交易已经再不适用这种方式了。

```
Pubkey script: <pubkey> OP_CHECKSIG
Signature script: <sig>
```

#### Null数据\|Null Data

在Bitcion Core 0.9.0 和之后版本，可以把任意数据增加到可验证的不可支出公钥。因此当使用该版本的默认设置来传播和挖掘 的Null数据交易类型，不会被全节点存储在UTXO集上。因为Null数据交易类型在TUXO集中不能被自动修剪，这种交易类型适用于UTXO数据库膨胀的场景。然而，如果可以，更好的选择是把数据储存在交易信息之外。

如果null 数据交易符合一致性共识的其他部分，比如没有大于520 Bytes 的提交 数据，一致性共识允许null data的公钥脚本的大小最多10000bytes.

Bitcoin Core 0.9.x 到0.10.0 版本将会默认设置中转和打包null data 交易类型，支持单次提交数据多达40bytes和一个收入为0聪的交易结果。

```
Pubkey Script: OP_RETURN <0 to 40 bytes of data>
(Null data scripts cannot be spent, so there's no signature script.)
```

Bitcoin Core 0.11.x将默认值增加到80字节，其他规则保持不变。

只要不超过总字节限制，Bitcoin Core 0.12.0 默认支持最多83个字节，任意数量的数据推送的null 数据交易。必须仍然只有一个空数据输出和0聪的交易。

Bitcion Core 的 `-datacarriersize`配置选项允许设置最大体积来限制Null数据交易的广播和打包。

