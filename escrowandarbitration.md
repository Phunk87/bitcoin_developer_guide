### 托管和仲裁 \|Escrow And Arbitration

顾客Charlie 想要从老板Bob买商品，但是他们之间相互猜疑。所以他们使用合约来保证Charlie 能拿到商品，Bob 能拿到钱。

一个简单的合约可以这样设定，Charlie支付比特币到一个多重签名地址，只有Bob 和Charlie 都签名时output 才可以被花费。也就是说，除非Charile拿到商品后Bob 才会被支付，还可能是Charlie没有拿到商品，但是支付的钱也拿不回来了。

这个简单的合约没有解决问题，所以他们找到了Alice作为仲裁者来创建托管交易。Charlie 支付比特币到一个2-of-3 d 多重签名脚本，（只有两个及以上签名时，output才可以花费）。如果没有问题，Charlie 可以签名支付给Bob，商品有问题时，Bob 退回Charlie 的钱。如果有分歧，Alice 可以决定谁得到支付的比特币。为了创造一个多重签名地址（output），三个交出他们的公钥，Bob 创建如下的P2SH的赎回脚本：

```
OP_2 [A's pubkey] [B's pubkey] [C's pubkey] OP_3 OP_CHECKMULTISIG
```

（把公钥的推入验证栈的操作码（Opcode）没有展示）

`OP_2`和`OP_3`把真实的数字2 和3 放入栈内。`OP_2`确定了需要两个签名，`OP_3`表明需要提供三个公钥（未经过哈希运算的）。这就是2 -of - 3 的多重签名脚本，更一般的叫法是 m-of -n 公钥脚本（m是需要的最小匹配的签名数量，n是提供的公钥数量）

Bob 把这个赎回脚本给Charlie，确保他的公钥和Alice 的公钥包含在脚本内。之后，Charlie hash运算这个赎回脚本，创建了P2SH 交易的赎回脚本，然后为这笔交易支付比特币。Bob 看到P2SH交易被区块链打包确认后，交付商品。

不幸的是，运送过程中商品有了轻微的损耗，Charlie 希望要全部退款，Bob 认为退还10% 才是合理的。于是他们找到Alice 仲裁这笔交易。Alice 向Charlie 所要之前由Bob 生成并由Charlie 检查确认过的赎回脚本和商品损耗的证据。

Alice 经过查看证据，认为40%是一个合理的数值。所以 Alice创建并签名了一个有两个output 的交易，支付60%的比特币到Bob 的公钥地址，支付剩余部分到 Charlie 的公钥地址。

在签名脚本中，Alice 写入她自己的签名和Bob之前创建的未哈希的序列化的赎回脚本的副本，Alice 把这个不完整交易的副本分别给Charlie 和Bob。Charlie 和Bob中的任意一个人都可以通过自己签名的方式，创建下面的签名脚本:

```
OP_0 [A's signature] [B's or C's signature] [serialized redeem script]
```

\(把签名和赎回脚本压入验证栈的操作码没有展示\)

