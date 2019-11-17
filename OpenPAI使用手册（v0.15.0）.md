## 先决条件
已查看OpenVPN使用手册，并已成功连接VPN
## 集群资源
* 2080ti服务器： 2张2080TI显卡，192逻辑CPU核，768G内存
* Titan V服务器： 8张TITAN V显卡，40逻辑CPU核，512G内存
* 剩余资源详细情况：http://192.168.111.100:8088/cluster/nodes
# 警告
自管理员处获取账号密码后，在使用集群过程中不得滥用漏洞（OpenPAI自身问题）
## 浏览器访问
192.168.111.100:9286
## 制作具有SSH功能镜像（可选）
如果需要SSH功能，镜像需安装openssh-server和curl，。推荐一个新手练习镜像：192.168.111.99:5000/zhaoj-pytorch-py36-cu90
## 提交任务详解
### 选择Cluster
* default是专用于项目的，原则上不允许非项目使用
* gpu_only是用于非项目的
### Command详解（Ctrl+C和Ctrl+V可轻松复制粘粘）
* 安全SSH命令（默认是不安全的，不要使用，后果自负）：
```
cat /userhome/.ssh/id_rsa.pub > ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
```
* 禁用SSH功能（默认是启动的）:  
```
service ssh stop
```
* 公共数据集文件夹被自动挂载至容器中/dataset目录下，使用示例（容器内进入公共数据集文件夹）:  
```
cd /dataset
```
* 个人家目录被自动挂载至容器中/userhome目录下，使用示例（容器内进入个人家目录）：  
```
cd /userhome
```
### 选择镜像
不要使用默认的镜像，应使用集群镜像（前缀都是192.168.111.99:5000），例如： 192.168.111.99:5000/zhaoj-pytorch-py36-cu90
### 分布式任务
分布式任务需要多个Task role，例如两个，分别叫task1，task2，在Command栏（或ssh至容器内后）可以用ssh task1-0或ssh task2-0轻松的ssh到每一个容器里
## 安全SSH至一个Running容器
* 第一步： 提交任务时在Command栏添加安全SSH命令：
```
cat /userhome/.ssh/id_rsa.pub > ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
```
* 第二步： 使用xshell（ssh工具）远程连接集群，连接成功如下所示.  确保IP地址为202.38.69.243，端口为11099，账号，密码.这四项输入无误
```
zhangsan@depoly:~$
```
* 第三步： 查看任务的ssh info信息中的最后一行命令（安全SSH方法下其它行没用），修改最后一行命令中的 -i 秘钥名 为 -i ~/.ssh/id_rsa , 例如最后一行为ssh -i zhangsan_1573621908725_776cbb77 -p 20841 root@192.168.111.110，则修改为：
```
zhangsan@depoly:~$ ssh -i ~/.ssh/id_rsa -p 20841 root@192.168.111.110
```
## 上传数据
* 上传个人数据： 使用xftp（传输文件工具，也可以用winscp）向集群中自己的主目录传输即可.  确保IP地址为202.38.69.243，端口为11099，账号，密码.这四项输入无误
* 公共数据集： 使用xftp向集群中/game/dataset目录传输即可


