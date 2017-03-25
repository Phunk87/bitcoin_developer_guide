### 微支付通道 \| Micropayment Channel

Alice 为Bob 工作，兼职管理论坛。每当有人在Bob的论坛发帖，Alice会检查帖子是不是攻击性或者垃圾内容。但是Bob 经常忘记支付工资，所以Alice 要求每当她批准或者删除摸个帖子时立即支付工资。Bob 由于交易费拒绝了，因为数百笔小额付款会产生上万的交易费。所以Alice 建议使用微支付通道技术。

Bob向Alice 索要公钥，然后创建如下交易。

bond transaction： 通过P2PH支付100 聪到一个2 -of -2 的公钥脚本，需要Alice 和bob 的共同签名。 广播这个交易会使得 100 聪成为Alice 的“人质“，所以这时Bob 不会广播这个交易。

refund transaction： 第二个交易在锁定时间一天后，支付全部bond transaction的output（减去交易费）返还给Bob。Bob 不能自己签署退款交易，所以她要让Alice签名。如下图所示![](/assets/import.png)  


Alice 检查refund 交易是在24小时后，签署后交还给Bob交易副本。然后Alice 向Bob 索要Bond transaction 查看refund 是否能花掉Bond transaction 的钱。现在Alice 可以向网络广播这个交易，确保Bob 的100聪仔交易锁定到期之前不会被花到其他地方。对于Bob，除了一部分交易费，没有花掉任何比特币，他能够在锁定时间之后（24小时）广播refund交易来获得全额退款。

现在Alice完成了价值1 聪的工作，Alice 要求Bob 重写并签名一份新的refund 交易。版本2交易 分配1聪给Alice。99 聪给Bob。这个交易没有锁定时间，所以Alice 可以在任何时间签名后广播到网络中（但是Alice 没有立即这样做。）

Alice 和Bob 重复进行 ”工作-支付“ 的步骤。直到这一天结束或者锁定时间快失效时，Alice 签署并且广播最后一个版本的refund，Alice 和Bob 分配到了最后一份refund 分配的比特币。第二天，Alice 开始新的工作，他们创建了一个新的 微支付通道合约。



如果Alice 

爱的色放





























































