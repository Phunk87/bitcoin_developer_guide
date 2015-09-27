## 区块链 | Block Chain

区块链是所有交易保持有序及时序的一个记录，它为比特币提供了公开的账本。这套系统被用于防止双花和对之前交易的修改。

在比特币网络中的每个完全节点存储着一个区块链，只包含被该节点验证过的区块。当多个节点在其区块链中都有了同样的区块时，他们被认为是[一致的](TOADD)(consensus)。这些节点用来维持一致性的验证规则被称作[一致性规则](TOADD)(consensus rules)。本节会涉及很多关于一致性规则的描述，而其被 Bitcoin Core 所使用。

### 区块链总览 | Block Chain Overview

![简化的比特币区块链](./en-blockchain-overview.svg)

上图展现了一个简化版的区块链。一个或多个新的交易被收集到一起成为了一个[区块](TOADD)(block)的交易数据部分。每个交易的副本都会被哈希，然后这些哈希被配对，被哈希，再配对，再哈希，直到只有一个哈希值，这就是 merkle �树的 merkle 根节点。



### 工作量证明 | Proof Of Work

### 区块高度及分叉 | Block Height And Forking

### 交易数据 | Transaction Data

### 一致性规则变更 | Consensus Rule Changes

### 发现分叉 | Detecting Forks