## 自建中转服务教程
腾讯阿里云教程<a href="https://github.com/ycyw/transfer/blob/main/tenxunyun.md" target="_blank">点击此处</a>  
根据目前情况虽然腾讯云给部分中转用户发了自查通知，但实际并未进行封禁操作，后续也不太可能直接关停，首选还是推荐腾讯云，网络延迟相对低一些  

恒创云教程<a href="https://github.com/ycyw/transfer/blob/main/hengchuangyun.md" target="_blank">点击此处</a>  
恒创云总部位于香港，主要为香港/海外用户提供服务，不需要实名认证，担心清退可选择该服务商  

此外，也可使用uc云，该服务商价格相对较优惠，先<a href="https://www.ucloud.cn/site/active/kuaijiesale.html?invitation_code=C1x6272BF38EE97" target="_blank">注册账号</a>，再<a href="https://www.ucloud.cn/site/active/kuaijiesale.html?invitation_code=C1x6272BF38EE97" target="_blank">点击此处</a>打开链接注册购买香港服务器年付最低仅84元  

关于延迟情况，国内有三大运营商，且地域广阔，实际延迟根据不同地域、运营商线路等会上下浮动。实测广州/深圳地区腾讯云10ms，恒创云、uc云10+ms，比腾讯云略高


## 中转服务节点  
不想或不会自建服务器，可直接使用下面的地址，服务器费用0.5%  
|    币种/矿池  |   鱼池（f2pool.com）      |   e池（ethermine.org）      |
| ---- | ---- | ---- |
|   ETH（TCP协议）   |   f2pool.555pool.com:6688      |   ethermine.555pool.com:14444      |
|   ETH（SSL加密）   |   f2pool.555pool.com:6689      |   ethermine.555pool.com:5555      |
  
注：TCP地址可直接使用。SSL地址各个内核的格式并不全都统一，且部分内核不支持SSL，若SSL地址连接报错，可尝试在地址前添加“stratum+ssl://”，或查看内核配置文档ssl所需的参数  
已测试内核：  
gminer需要添加配置参数“--SSL 1”  
nbminer需要在地址前添加“stratum+ssl://”  
## 常见问题  
#### 1.端口转发原理  
端口转发是将矿机直连矿池，变成了矿机连服务器，服务器连矿池，服务器在中间作为一个代理桥梁的存在  
对矿池而言，你的服务器在香港，那么你就是香港用户，矿机的具体位置城市，矿池是无法查看到的  
再配合匿名挖矿，矿池即使想，也获取不到挖矿用户的具体信息  
#### 2.云服务器重启后无法连接  
云服务器重启后需要重新启动端口转发服务，执行如下命令即可  
```
sudo redir :6666 eth.f2pool.com:6688
```
#### 3.可以添加多个端口转发吗  
```
sudo redir :本地监听端口 转发到的地址和端口
```
该启动端口转发命令执行多次即可，注意本地监听端口不可重复  
#### 4.如何联系  
有问题可以添加微信w_onea  
