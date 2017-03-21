# 比特币开发者指南 \| Bitcoin Developer Guide

## 当前版本 \| Current Version

| Name | Value |
| :--- | :--- |
| source | [https://github.com/bitcoin-dot-org/bitcoin.org](https://github.com/bitcoin-dot-org/bitcoin.org) |
| commit | [000887a2f4b67c2345ea1c91578cee44c0f90088](https://github.com/bitcoin-dot-org/bitcoin.org/commit/000887a2f4b67c2345ea1c91578cee44c0f90088) |

## 关于译本 \| About Translation

该译本的所有内容被托管在 [GitHub](https://github.com/0dayZh/bitcoin_developer_guide) 上，你可以通过 [GitBook](https://www.gitbook.com/book/0dayzh/bitcoin_developer_guide) 进行在线阅读或下载 PDF、EPUB、MOBI 的格式。

如果你发现有任何的翻译出入或者文字书写错误，欢迎 fork 提 pull request，也可以提 [issues](https://github.com/0dayZh/bitcoin_developer_guide/issues) 提出对译本的建议及意见。

## 捐献 \| Donation

如果你觉得该译本对你有所帮助并希望为我做些事情作为回馈，除了提出修改意见外，还可以捐赠比特币或者购买亚马逊心愿清单中的物品。

* [Bitcoin: 1EdMCu32fzGo5iNCyQuMZhHboSe2gzqQPg](bitcoin:1EdMCu32fzGo5iNCyQuMZhHboSe2gzqQPg)
* [Amazon 心愿单](http://www.amazon.cn/registry/wishlist/QBFPXWCWVD4N)

## 进度 \| Progress \(1 / 8\)

* [x] 区块链
  * [x] 区块链总览
  * [x] 工作量证明
  * [x] 区块高度及分叉
  * [x] 交易数据
  * [x] 一致性规则变更
  * [x] 发现分叉
* [x] 交易
  * [x] P2PKH 脚本验证
  * [x] P2SH 脚本
  * [x] 标准交易
  * [x] 非标准交易
  * [x] 签名哈希的类型
  * [x] Locktime And Sequence Number
  * [x] 交易手续费及变更
  * [x] 避免 公钥和私钥重用
  * [x] 交易的可锻性
* [ ] 合约
  * [ ] 托管和仲裁
  * [ ] 微支付频道
  * [ ] CoinJoin
* [ ] 钱包
  * [x] 钱包程序
  * [x] 完整服务的钱包
  * [x] 只用于签名的钱包
  * [x] 离线钱包
  * [x] 硬件钱包
  * [x] 只用于发布的钱包
  * [ ] 钱包文件
  * [ ] 私钥格式
  * [ ] 钱包导入格式
  * [ ] Mini 私钥格式
  * [ ] 公钥格式
  * [ ] 分级确定性密钥生成
  * [ ] Hardened Keys
  * [ ] 存储根种子
  * [ ] Loose-Key 钱包
* [ ] 支付流程
* [ ] 运作模式
* [ ] 点对点网络
* [ ] 挖矿

## 简介 \| Introduction

此开发者指南旨在提供给你理解比特币的信息，让你能够开始构建以比特币为基础的应用，并不是一本[规范手册](https://bitcoin.org/en/developer-reference#not-a-specification)。为了尽可能的理解该文档，你可能需要安装最新版本的 Bitcoin Core，你可以通过[源码](https://github.com/bitcoin/bitcoin)或者[预先编译好的可执行文件](https://bitcoin.org/en/download)来获取到。

关于比特币开发的问题最好在[比特币社区](https://bitcoin.org/en/development#devcommunities)中提出。对于在 Bitcoin.org 上的文档相关的错误或者意见可以通过[提交 issue](https://github.com/bitcoin-dot-org/bitcoin.org/issues) 或者发送邮件到[比特币文档邮件列表](https://groups.google.com/forum/#!forum/bitcoin-documentation)进行。

