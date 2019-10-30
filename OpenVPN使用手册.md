## 先决条件
希望使用GPU集群
## 申请账号
发送邮件至827008326@qq.com，邮件中须写清楚以下三条信息：账号，密码，操作系统（支持windows，ubuntu16，ubuntu18），示例邮件:
```
你好，我想申请的账号名是zhangsan，密码是1234，操作系统是ubuntu18
```
## Windows下如何使用OpenVPN
* 第一步： 确认已申请的账号密码
* 第二步： 获取安装包openvpn2.3.10和配置文件压缩包config-game
* 第三步： 安装openvpn2.3.10，安装时要选上两个未选上的选项
* 第四步： 将解压后的config-game文件夹放在openvpn安装目录的config文件夹下
* 第五步： 点击openvpn，选择connect，输入账号密码即可（也可能是选择client->connect）
## Ubuntu下如何使用OpenVPN
* 第一步： 确认已申请的账号密码
* 第二步： 获取配置文件压缩包config-game-ubuntu
* 第三步（16.04）： 使用以下命令安装openvpn
```
apt-get update -y && apt-get install -y openvpn
```
* 第三步（18.04）： 获取openvpn_2.3.10-1ubuntu2_amd64.deb，然后使用以下命令安装
```
dpkg -i openvpn_2.3.10-1ubuntu2_amd64.deb
```
* 第四步： 将解压后的config-game-ubuntu文件夹放在/etc/openvpn/下
* 第五步： 使用如下命令启动openvpn，然后输入账号密码即可
```
sudo openvpn /etc/openvpn/config-game-ubuntu/client.ovpn
```
