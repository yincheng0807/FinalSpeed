# FinalSpeed
服务器TCP双边加速软件可达到90%的物理带宽利用率

[FinalSpeed官方停止维护更新](http://www.ip4a.com/t/944.html)


## 开放端口

`service iptables start`

`iptables -A INPUT -p tcp --dport 你的vps端口号 -j ACCEPT`

`iptables -A OUTPUT -p tcp --sport 你的vps端口号 -j ACCEPT`

`service iptables save`

## 安装命令:

`rm -f install_fs.sh`

`wget https://raw.githubusercontent.com/yincheng0807/FinalSpeed/master/install_fs.sh`

`chmod +x install_fs.sh`

`./install_fs.sh 2>&1 | tee install.log`

## 常用命令使用说明

更新：执行一键安装会自动完成更新。

卸载： `sh /fs/stop.sh ; rm -rf /fs`

启动： `sh /fs/start.sh`

停止： `sh /fs/stop.sh`

重新启动： `sh /fs/restart.sh`

运行日志： `tail -f /fs/server.log`

## 设置服务端口：
默认udp 150和tcp 150 ,修改端口后服务端会自动修改防火墙

linux版: 
```
mkdir -p /fs/cnf/ ;
echo 端口号 > /fs/cnf/listen_port;
sh /fs/restart.sh
```

windows 版: 在cnf目录下新建文件listen_port,文件内容为端口号.

注意:由于finalspeed的工作原理,不要开放finalspeed所使用的tcp端口.