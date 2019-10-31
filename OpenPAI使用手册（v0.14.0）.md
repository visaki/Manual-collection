## 先决条件
已查看OpenVPN使用手册，并已成功连接VPN
## 集群资源
* 2080ti服务器： 2张2080TI显卡，192逻辑CPU核，768G内存
* Titan V服务器： 8张TITAN V显卡，40逻辑CPU核，512G内存
# 警告
自管理员处获取账号密码后，在使用集群过程中不得滥用漏洞（OpenPAI自身问题）
## 浏览器访问
192.168.111.100:9286
## 镜像
镜像需安装cifs-utils，openssh-server，curl，才能启用挂载存储和SSH功能。推荐一个新手练习镜像：192.168.111.99:5000/zhaoj-pytorch-py36-cu90
## 提交任务详解
### 选择Cluster
* default是专用于项目的，原则上不允许非项目使用
* gpu_only是用于非项目的
### Command详解（需要哪个功能就用Ctrl+C复制命令，然后Ctrl+V复制到Command栏）
* SSH功能:  

启用SSH命令：
```
sed -i 's/[# ]*Port.*/Port '$PAI_CONTAINER_SSH_PORT'/' /etc/ssh/sshd_config && service ssh restart
```
禁用SSH命令：
```
service ssh stop
```
* 挂载公共数据集至/data:  
```
mkdir /data && mount -t cifs -o username=dataset,password=123456,dir_mode=0555,file_mode=0555,nounix  //169.252.198.3/dataset /data
```
* 挂载个人目录至/code：  

必须在Secrets里将自己的密码设置为secrets。例如密码为12345678，在Secrets栏添加key为pwd，value为12345678，在Command栏里<% $secrets.pwd %>就代表着12345678。请将以下示例命令中的'账号'替换为自己的账号名，确认<% $secrets.pwd %>已设置完成。
```
mkdir /code && mount -t cifs -o username=账号,password=<% $secrets.pwd %>,dir_mode=0775,file_mode=0775,nounix  //169.252.198.3/homes /code
```
### 选择镜像
不要使用默认的镜像，应使用集群镜像，例如： 192.168.111.99:5000/zhaoj-pytorch-py36-cu90
### 分布式任务
分布式任务需要多个Task role，例如两个，分别叫task1，task2，在Command栏内可以用ssh task1-0或ssh task2-0轻松的ssh到每一个容器里
## SSH至一个Running容器
* 第一步： 使用xshell（ssh工具）远程连接集群，IP地址：202.38.69.243，端口：11099，账号密码从管理员获取
* 第二步： 使用以下命令移动至/students/ssh文件夹（主目录无法ssh，因为存储的设定）
```
cd /students/ssh
```
* 第三步： 查看任务的ssh info信息，有三行命令（wget，chmod，ssh什么的），依次执行即可SSH进容器内
## 上传数据
* 上传个人数据： 使用xftp（传输文件工具，也可以用winscp）向集群中自己的主目录传输即可
* 公共数据集： 使用xftp向集群中/students/dataset目录传输即可
* 挂载数据参考Command详解


