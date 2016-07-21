## LINUX学习笔记

2016-07-20:
    使用at执行计划任务时，如

    > at noon tomorrow
    
    使用CTRL+D来实现EOF,表示输入完成

    另一种执行计划任务的方式是crontab

    > crontab -e 打开cron表编辑
    > crontab -l 查看当前用户的crontab表
    > crontab -r 删除当前用户的cron进程
    > crontab -u 用户名 以某个用户的身份来控制cron表

cron的写法

    分钟 小时 日 月 周 [用户] 命令

*代表任意时间
,代表不连续的时间点，如2,3表示2和3都行
-表示连续的时间点，如2-4,表示2,3,4
*/n表示每隔单位时间，*/15表示每隔15分钟


2016-07-21：
  一,linux上网问题的解决：
        1. IP地址的设置一般在/etc/sysconfig/network-scripts/目录下的一堆ifup-xxx.cfg,ifdown-xx.cfg下面，修改其配置文件就可以把本机的ip设置成静态或者dhcp
        2. 改完之后需要修改域名解析，也就是/etc/resolv.conf文件，配置的nameserver会从上到下依次执行
        3. 配置路由表，使用route add default gw <路由器的ip地址>
        手工设置ip地址也可以使用ifconfig 接口 ip地址    
        
    网卡的安装一般需要下载对应的驱动，linux下是`.c`或者`.o`文件,下载下来make && make install就可以安装成功

  二,BASH的配置文件:
    SHELL分为Login Shell和nologin shell.在图形界面下登陆的shell都是非login shell。
    需要登陆系统才能使用的是login shell
   
   1. 只有login shell 才会读取系统设置文件/etc/profile。它是系统的整体的配置
   每个用户登陆后取得bash后一定会读取这个配置文件
   2. login shell读取完配置文件/etc/profile之后,接下来就会读取用户的个人配置文件，个人配置文件主要有3个隐藏文件：~/.bash_login,~/.bash_profile,~/.profile,如果bash_profile存在就不会理睬其他俩文件,如果没有bash_profile，就会读取bash_login,如果也不存在就读取~/.profile,读取bash_profile的时候还会读取~/.bashrc,所以个人配置最好放在bashrc下
   
   