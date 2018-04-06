ONMP
===

适用于安装了Entware固件的onmp一键安装命令

目前已经在Padavan、LEDE、梅林上测试成功

`php-fpm` 和 `mysqld` 启动失败的可以开启swap

```
$ onmp open 
# 选择7
```

## 说明

ONMP: Opkg + Nginx + MySQL + PHP

这是一个用Linux Shell编写的脚本，可以为使用opkg包管理的路由器快速搭建Nginx/MySQL/PHP环境，并且内置了一些好用的网站程序一键免配置快速安装

```
ONMP内置了以下程序的一键安装：
(1) phpMyAdmin（数据库管理工具）
(2) WordPress（使用最广泛的CMS）
(3) Owncloud（经典的私有云）
(4) Nextcloud（Owncloud团队的新作，美观强大的个人云盘）
(5) h5ai（优秀的文件目录）
(6) Lychee（一个很好看，易于使用的Web相册）
(7) Kodexplorer（可道云aka芒果云在线文档管理器）
(8) Netdata（详细得惊人的服务器监控面板）
(9) Typecho (流畅的轻量级开源博客程序)
(10) Z-Blog (体积小，速度快的PHP博客程序)
```

所有的软件包均通过opkg安装，一切配置均在脚本中可见，请放心使用

## 使用说明

[如何格式化U盘](https://github.com/xzhih/ONMP/blob/master/format-partition.md)

本脚本使用教程发布在恩山无线论坛
传送门：[Padavan固件一键安装onmp](http://www.right.com.cn/forum/thread-244810-1-1.html)

## 安装教程

### 1. 安装 Entware

Entware-ng是一个适用于嵌入式系统的软件包库，使用opkg包管理系统进行管理，现在在官方的源上已经有超过2000个软件包了，可以说是非常的丰富

不同的固件，安装方式都不一样，请认准安装方式（自己是什么固件总该懂得吧😂）

[在LEDE上使用Entware](https://github.com/xzhih/ONMP/blob/master/LEDE-entware.md)

[在梅林上使用Entware](https://github.com/xzhih/ONMP/blob/master/Merlin-entware.md)

### 2. 安装onmp

一键命令，复制->粘贴->回车

```
 $ sh -c "$(curl -kfsSl https://raw.githubusercontent.com/xzhih/ONMP/master/oneclick.sh)"
```

一长串的复制如果出错，可以按照以下给出的命令，一步步进行安装

```
 cd /opt && opkg install wget unzip # 进入 entware 挂载目录
# 下载软件包
wget --no-check-certificate -O /opt/onmp.zip https://github.com/xzhih/ONMP/archive/master.zip 
unzip /opt/onmp.zip # 解压
cd /opt/ONMP-master 
chmod +x ./onmp.sh 
./onmp.sh # 运行
```

要是正常运行到脚本，会出现下面的情景，选1安装即可

![安装](https://i.loli.net/2018/03/03/5a99ac096c6a1.png)

正常安装中要是出现错误，会有错误信息，根据提示操作，目前得到的大多数反馈都是网络问题，因为 entware 的源在国外，而且他们的管理者说之前受到了来自亚洲的DDOS，所以对这边限流了，速度较慢。遇到这种情况，可以去看看剧，没准回来的时候就好了😄

安装成功得到的结果是这样的

![安装成功](https://i.loli.net/2018/03/03/5a99aeda756ac.png)

如果你也是和上图一样，那么恭喜你，成功的安装上了 ONMP，你可以尽情的玩耍了

## ONMP 详细使用教程

**基本命令：**

```
管理：onmp open
启动、停止、重启：onmp start|stop|restart
查看网站列表：onmp list 
```

**设置数据库密码：**

输入 `onmp open` 后选择3，会提示 `Enter password:` ，这个时候要输入当前数据库的密码，比如我初始设置的数据库密码是123456，回车后要是密码正确，会提示输入你要设置的新密码，回车后会提示再次输入确认。也就是，一次旧密码，两次新密码。

这个位置很简单，但是很多人都说改不了密码，其实是没看提示，没输入旧密码，所以我写清楚一些。
