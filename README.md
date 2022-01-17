## 自建中转服务教程

腾讯阿里云教程<a href="https://github.com/ycyw/transfer/blob/main/tenxunyun.md" target="_blank">点击此处</a>

恒创云教程<a href="https://github.com/ycyw/transfer/blob/main/hengchuangyun.md" target="_blank">点击此处</a>  
恒创云总部位于香港，主要为香港/海外用户提供服务，不需要实名认证，简体中文操作界面  

关于延迟情况，国内有三大运营商，且地域广阔，实际延迟根据不同地域、运营商线路等会上下浮动。实测广州/深圳地区电信10ms+

## 中转服务节点  
不想或不会自建服务器，可直接使用下面的地址，服务器费用0.5%  
|    矿池/币种  |   ETH（TCP协议）      |   ETH（SSL加密）      |
| ---- | ---- | ---- |
|   鱼池（f2pool.com）   |   f2pool.555pool.com:6688      |   f2pool.555pool.com:6689      |
|   e池（ethermine.org）   |   ethermine.555pool.com:14444      |   ethermine.555pool.com:5555      |
|   币印（poolin.me）   |   poolin.555pool.com:1883      |   poolin.555pool.com:1884      |
|   Hive OS（hiveon.net）   |   hiveon.555pool.com:24442      |   hiveon.555pool.com:24443      |
|   凤池（flexpool.io）   |   flexpool.555pool.com:3344      |   flexpool.555pool.com:4455      |
|   蚂蚁（antpool.com）   |   antpool.555pool.com:8008      |   antpool.555pool.com:8009      |
  
* TCP地址可直接使用
* SSL地址各个内核的格式并不全都统一，且部分内核不支持SSL，若SSL地址连接报错，可尝试在地址前添加`stratum+ssl://`，或查看内核配置文档ssl所需的参数，以下内核已测试：   
  * gminer需要添加配置参数`--SSL 1`  
  * nbminer需要在地址前添加`stratum+ssl://`  
* 部分矿池可能会连接失败，此时等待一分钟左右，让内核程序自动重连即可
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
#### 4.联系方式  
<a href="https://t.me/+jKRf0T6YgPhlNTA1" target="_blank">TG交流群</a>  
微信号w_onea  
