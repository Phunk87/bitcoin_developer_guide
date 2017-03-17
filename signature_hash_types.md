### 签名哈希类型 \| Signature Hash Types

[`OP_CHECKSIG`](https://bitcoin.org/en/developer-reference#term-op-checksig)从每个计算的签名中提取一个非堆栈参数，这使得签名者可以选择签署交易任意部分。这种设置使得被签名的部分不会被篡改，同时，签名者可以有选择的让其他人修改他们的交易。

各种的签名选项称为哈希前面类型，目前有三种可用：

* [`SIGHASH_ALL`](https://bitcoin.org/en/glossary/sighash-all),是默认设置，该签名类型保护了输入和输出，只有签名脚本是可以更改的。

* [`SIGHASH_NONE`](https://bitcoin.org/en/glossary/sighash-none)签名所有输入，不签名输出，除非其他签名使用其他签名哈希flag保护输出，允许任何人改比特币的去向。

* [`SIGHASH_SINGLE`](https://bitcoin.org/en/glossary/sighash-single)  只签署一个和input 对应的输出（输出有和i输入有相同的输出索引（output index））确保没人可以改变签名人所属的交易部分， 交易的其余部分都是可以更改的。对应的签名输出必须存在或者值为1来绕过比特币的安全策略。使用这种方法签名的input 和其他input 都包括在签名中，但其他input 的序列号不包括在签名中，可以更新。

以上三种基础签名哈希类型可以结合 [`SIGHASH_ANYONECANPAY`](https://bitcoin.org/en/glossary/sighash-anyonecanpay) flag 创造三种新的类型：

* [`SIGHASH_ALL|SIGHASH_ANYONECANPAY`](https://bitcoin.org/en/glossary/sighash-anyonecanpay) 签名所有output 和一个input，并且允许任何人添加和删除其他输入和输出。所以每个人可以贡献自己比特币放入到交易中，但是不能改变已经签名的部分的交易 的流向的数量。

* [`SIGHASH_NONE|SIGHASH_ANYONECANPAY`](https://bitcoin.org/en/glossary/sighash-anyonecanpay) 只签名自己

fsdaafdssdffadsdasfsadadsf

