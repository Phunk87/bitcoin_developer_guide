### 锁定时间和序列号\|Locktime And Sequence Number

所有的签名类型都会签定交易的锁定时间\(Bitcoin Core 的源代码里称为 [nLockTime](https://bitcoin.org/en/glossary/locktime).\) locktime代表交易被允许被被打包的最早时间。

Locktime 允许签名者创建一个时间锁定交易。因为只会在将来生效，这给签名者一个的反悔的机会。

如果其中任何一个签名者反悔了，他可以创建一个没有locktime 的交易。因为新创建的交易可以花掉旧交易的那部分input，所以旧交易在lock time解锁后 找不到可以花掉的input，旧交易就失效了。

当心 locktime所 的快失效的情况，点对点网络允许locktime 失效的前两个小时，打包被锁定的交易，此外区块产生的时间间隔也是不确定的。所以如果想取消交易，一定要在锁定时间的几个小时之前进行。

Bitcoin Core 的早期版本提供了一个可以防止签名者使用上述方法取消locktime 交易的功能。 出于防止拒绝服务攻击的原因，这个功能被禁用了。该系统还留下了这样的设置，每个输入会分配一个四字节的序列号。序列号的目的旨在允许多个签名者同意更新交易。他们可以将自己的sequence number设置为四字节的的无符号最大值\(0xffffffff\),使得交易的locktime 仍然有效的情况下，打包交易进块。

即使今天，如果所有的input 的sequence number都是最大值，locktime锁就会失效。所以如果想使用locktime，至少一个input的sequence number要小于最大值。由于sequence number不用于其他目的，任何sequence number 为零的交易都会启动locktime 功能。

Locktime 本身是一个无符号的四字节整数，可以通过以下两种方式解析：

* 如果locktime 小于5亿，locktime 被认为是区块的高度。交易只能被大于等于此高度的区块打包。
* 如果locktime 大于等于5亿，locktime 为使用Unix 时间格式（从1970-01-01 00:00 UTC 经过的秒数，目前超过12.95亿）解析。交易可以添加到任何大于此时间的区块中。 



