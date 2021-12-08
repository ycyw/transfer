## 前言
目前各大矿池国内DNS基本被污染无法请求  
可搭建香港服务器转发数据解决该问题
## 购买香港服务器
#### 1.选配服务器
国内推荐腾讯云和阿里云的香港服务器，点击下方链接打开网页  
[【腾讯云】云服务器全球购](https://cloud.tencent.com/act/cps/redirect?redirect=1068&cps_key=5c54c86b3f4415abe2b9de54f11937db&from=console)  
[【阿里云】云服务器 精选特惠](https://www.aliyun.com/daily-act/ecs/activity_selection?userCode=xrpv28iz)  
**腾讯云**选择**中国香港**地域，操作系统选择**Ubuntu**系统，其他默认即可，点击购买  
若已售罄可**切换配置**或选择**新加坡**地域或选择**轻量应用服务器**  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111508863-1065655365.png)  
**阿里云**选择**中国香港与海外服务器**，立即购买  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111515135-1164723545.png)  
选择**系统镜像**栏下的**ubuntu**系统，其他默认即可，点击购买  
若已售罄可**切换配置**或选择**新加坡**地域或回到上一页选择**ECS服务器** 
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111521855-44752120.png)  
付款后进入云服务器控制台，稍等一会儿，等待服务器初始化完成状态为运行中  
注：购买一次后，就成老用户了，老用户价格会比较贵，所以买之前想清楚，推荐购买一年的最低配  
下方教程以腾讯云为例，阿里云的流程也基本一样  
#### 2.点击更多 -> 密码/秘钥 -> 重置密码  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111526432-558635387.png)  
重置密码界面输入新密码 -> 下一步 -> 同意强制关机 -> 重置密码  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111529226-241161976.png)  
#### 3.打开云服务器登录页  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111531437-2085908523.png)  
输入刚才重置的密码登录  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111534013-1017324382.png)  
登录成功后进入命令行界面  
## 安装启动端口转发服务  
#### 1.下方两行命令依次复制粘贴至命令行回车执行  
```
sudo apt-get update -y
sudo apt-get install redir -y
```
执行后如下图则已完成转发服务安装  

![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130113825315-1626231946.png)  

#### 2.启动转发端口服务  
```
sudo redir :6666 asia2.ethermine.org:4444
```
执行后没有任何输出，表示执行成功  
说明：  
6666：监听访问本服务器的6666端口，可改成自己矿机想访问服务器的端口  
asia2.ethermine.org:4444：转发到asia2.ethermine.org的4444端口，可根据需要自行修改为矿池的地址和端口  
到此就搭建完成了！  
使用服务器公网ip:6666即可。例如：1.2.3.4:6666  
内核直接去修改挖矿地址  
轻松地址修改流程：矿池选择栏 -> 矿池管理 -> 右键矿池地址 -> 修改 -> 矿池地址  
开源地址修改流程：主矿池选择栏 -> 管理 -> 双击矿池地址 -> 重写矿池地址  
注：若购买的是轻量服务器，需要去防火墙/安全组将端口放开，教程使用的是6666端口，可以改成自己想用的端口，1024-49151任选一个端口号即可  
# 补充：修改端口转发地址  
#### 1.查看当前监听端口的id  
```
sudo netstat -anp |grep 6666
```
执行后如下图，看到该监听端口id为1907  
![](https://img2020.cnblogs.com/blog/1862911/202111/1862911-20211130111538901-836598323.png)  
#### 2.停止当前转发服务  
```
sudo kill 1907
```
此处的1907为我查询到的id，需要替换成你实际看到的id，不要直接复制该命令执行  
#### 3.启动转发端口服务  
```
sudo redir :6666 asia2.ethermine.org:4444
```
执行后没有任何输出，则修改成功！  
此外，若云服务器重启，转发服务也需要重新启动，执行此处的启动命令即可  
有问题可以加微信w_onea  
[tg交流群](https://t.me/+CetxQfaj0aBlM2I1)  
# 附：自建免费中转服务  
该中转服务器为腾讯云香港地域  
不想自建中转服务可直接使用该地址，无抽水  
也可用来测试矿机延迟情况，按照上方教程自建服务后，延迟与该服务器基本一致  
|    币种/矿池  |   鱼池（f2pool.com）      |
| ---- | ---- |
|   ETH   |   f2pool.555pool.com:6688      |
|   ETC   |   f2pool.555pool.com:8118     |
|   LTC   |   f2pool.555pool.com:8888      |
