## 一、购买服务器
#### 1.搬瓦工简单介绍
搬瓦工是来自加拿大 IT7 旗下的便宜 VPS 商家，主要销售基于 KVM 架构的 VPS 方案，机房包括香港 CN2 GIA、洛杉矶 DC6 CN2 GIA-E、洛杉矶 DC9 CN2 GIA、日本软银 JPOS_1、荷兰联通 EUNL_9、洛杉矶 CN2、洛杉矶 MCOM、洛杉矶 Fremont 等十几个机房   
#### 2.搬瓦工常见方案  
|    配置/类型  |   CN2 (入门)      |   CN2 GIA-E (推荐)      |   HK CN2 GIA (高端)   |
| ---- | ---- | ---- | ---- |
|   CPU   |   1 核      |   2 核      |   2 核      |
|   内存   |   1024 MB     |   1024 MB     |   2048 MB     |
|   硬盘   |   20 GB SSD      |   20 GB SSD      |   40 GB SSD      |
|   流量   |   1000 GB / 月     |   1000 GB / 月     |   500 GB / 月     |
|   带宽   |   1 Gbps      |   2.5 Gbps      |   1 Gbps      |
|   机房   |   DC3 / DC8 机房      |   DC6 / DC9 / 软银机房      |   DC3 / DC8 机房      |
|   价格   |   $49.99/年      |   $49.99/季度，$169.99/年      |   $89.99/月，$899.99/年      |
|   备注   |   入门首选，速度够用    |   最推荐，三网直连，速度超快    |   土豪高端选择，绝对好用    |
|   购买   |   <a href="https://bwh81.net/aff.php?aff=67039&pid=57" >直达通道（CN2方案）</a>      |   <a href="https://bwh81.net/aff.php?aff=67039&pid=87" >直达通道（CN2 GIA-E方案）</a>      |   <a href="https://bwh81.net/aff.php?aff=67039&pid=95" >直达通道（香港 CN2 GIA方案）</a>      |

以上是购买人数最多也是最优的几种方案，更多可到<a href="https://bwh81.net/aff.php?aff=67039" >搬瓦工官网</a>查看
#### 3.购买流程
教程以CN2 GIA-E方案为例，点击上方链接打开购买页面。默认为49.99美元/季度，可选择半年付或年付，机房推荐选择日本软银，国内延迟相对较低  
![](https://github.com/ycyw/transfer/blob/main/static/1.png)  
> 添加到购物车后，使用优惠码`BWHNY2022`可减免12.22%，循环折扣，续费也是这个价格  

![](https://github.com/ycyw/transfer/blob/main/static/2.png)  
> 填写注册信息，其中邮箱、电话号码、密码、国家需要认真填写，其他信息随意  

![](https://github.com/ycyw/transfer/blob/main/static/3.png)  
> 提交订单后，邮箱会收到六位数字验证码，输入验证码点击确认  

![](https://github.com/ycyw/transfer/blob/main/static/4.png)  
> 点击支付按钮跳转至支付宝页面扫码支付，支付完成后，邮箱会收到服务器的IP、端口、密码等信息，到此服务器就购买成功了  

![](https://github.com/ycyw/transfer/blob/main/static/5.png)  

## 二、登录服务器配置端口转发
#### 1.下载服务器管理软件Xshell
<a href="https://pan.baidu.com/s/1ADwxcw7Dd9cwCxtFa3m8GQ?pwd=ncwr" >点击此处</a>跳转至百度网盘下载  

#### 2.登录服务器
下载安装后打开软件，点击**文件** -> **新建**打开新建会话属性，输入邮箱中收到的IP和port端口  
![](https://github.com/ycyw/transfer/blob/main/static/6.png)  
> 点击**用户身份认证**，继续输入用户名root，密码为邮箱中收到的password密码，点击**连接**  

![](https://github.com/ycyw/transfer/blob/main/static/7.png)  
> 点击**接受并保存**进入命令行  

![](https://github.com/ycyw/transfer/blob/main/static/8.png)  

#### 3.安装启动socat转发
> 依次执行以下两个安装socat转发、启动转发进程命令  

```
yum install -y socat
nohup socat TCP-LISTEN:6688,reuseaddr,fork TCP:eth.f2pool.com:6688 >> socat.log 2>&1 &
```
说明：
> TCP-LISTEN:6688 -> 监听访问本机的6688TCP端口，可改成自己矿机想访问的端口  
> fork TCP:eth.f2pool.com:6688 -> 转发到eth.f2pool.com的6688端口，根据需要自行修改为矿池的地址和端口  

执行后如下图，则搭建完成，将矿池地址修改为邮件中的服务器ip:6688即可开始挖矿，例如：1.2.3.4:6688
![](https://github.com/ycyw/transfer/blob/main/static/9.png)  

## 三、常见问题
#### 如何修改挖矿地址
* 内核直接去修改挖矿地址
* 轻松地址修改流程：矿池选择栏 -> 矿池管理 -> 右键矿池地址 -> 修改 -> 矿池地址
* 开源地址修改流程：主矿池选择栏 -> 管理 -> 双击矿池地址 -> 重写矿池地址

#### 查看当前共有多少矿机连接
执行如下命令查询所有连接到本机的矿机数量
```
num=$( ps -ef | grep socat | grep -v grep | wc -l) && if [ ${num} -gt 0 ]; then expr ${num} - 1; else echo ${num}; fi
```

#### 停止端口转发
执行如下命令停止全部端口转发
```
ps -ef | grep socat | grep -v grep | awk '{print $2}' | xargs kill -9
```

#### 启动端口转发
执行如下命令转发至鱼池eth，参数解释见上文。此外，服务器重启后需要使用该命令重新启动端口转发  
```
nohup socat TCP-LISTEN:6688,reuseaddr,fork TCP:eth.f2pool.com:6688 >> socat.log 2>&1 &
```

#### 如何卸载socat
执行如下命令即可  
注：卸载不能停止端口转发，若需要停止使用上面的停止命令
```
yum remove -y socat
```

#### 端口转发原理
端口转发是将矿机直连矿池，变成了矿机连服务器，服务器连矿池，服务器在中间作为一个代理桥梁的存在  
对矿池而言，你的服务器在香港，那么你就是香港用户，矿机的具体位置城市，矿池是无法查看到的  
再配合匿名挖矿，矿池即使想，也获取不到挖矿用户的具体信息  
