# FinalSpeed
服务器TCP双边加速软件可达到90%的物理带宽利用率，直观讲就是油管上看4K视频无压力！
[FinalSpeed官方停止维护更新](http://www.ip4a.com/t/944.html)


## 开放端口,一般的话该步骤不需要，除非你需要指定其他端口，默认是150端口。
`service iptables start`

`iptables -A INPUT -p tcp --dport 你的vps端口号 -j ACCEPT`

`iptables -A OUTPUT -p tcp --sport 你的vps端口号 -j ACCEPT`

`service iptables save`

## 安装命令:

`rm -f install_fs.sh`

`wget https://raw.githubusercontent.com/yincheng0807/FinalSpeed/master/install_fs.sh`

`chmod +x install_fs.sh`

`./install_fs.sh 2>&1 | tee install.log`
debian，ubuntu下如果执行脚本出错，需要切换到 dash：
`sudo dpkg-reconfigure dash`

## 常用命令使用说明

更新：执行一键安装会自动完成更新。

卸载： `sh /fs/stop.sh ; rm -rf /fs`

启动： `sh /fs/start.sh`

停止： `sh /fs/stop.sh`

重新启动： `sh /fs/restart.sh`

运行日志： `tail -f /fs/server.log`
如果以上步骤报错：`ohup: failed to run command 'java': No such file or directory`
请安装JAVA，ubuntu可能不带java，[官方教程>>](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html)
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
## 设置开机启动和定时任务：
```
chmod +x /etc/rc.local
vi /etc/rc.local
```
在`exit 0`前面添加：
`	sh /fs/start.sh`  
设置每天凌晨三点重启服务,更多参数请查询Crontab表达式：
`crontab -e`
`0 3 * * * sh /fs/restart.sh`
## 设置服务端口：
默认udp 150和tcp 150 ,修改端口后服务端会自动修改防火墙

linux版: 
```
mkdir -p /fs/cnf/ ;
echo 端口号 > /fs/cnf/listen_port;
sh /fs/restart.sh
```

windows 版: 在cnf目录下新建文件listen_port,文件内容为端口号.

注意:由于finalspeed的工作原理,不要开放finalspeed所使用的tcp端口.即安全组中编辑入站规则添加开放FS端口的UDP协议入站
