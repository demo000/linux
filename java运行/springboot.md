运行jar
```$xslt
nohup java -jar xxx.jar >xxx &
xxx为启动日志要写入的文件
```
但是如果想要在外网ip上访问该ip:port上的web服务，则需要打开对应的端口号。
### 4、CentOS7系统打开服务所使用的端口号： 
CentOS7使用firewalld防火墙(7之前使用iptables)，需要使用到的命令如下： 
1) systemctl start firewalld：启动前可以先用systemctl status firewalld查看firewalld状态； 
2) firewall-cmd --zone=public --add-port=8761/tcp --permanent：打开8761端口，其中端口号(8761)根据实际需要使用的端口决定； 
3) firewall-cmd --reload：重启服务； 
4) firewall-cmd --zone=public --list-ports：可以用来查看已打开的端口号； 
5) firewall-cmd --zone= public --remove-port=8761/tcp --permanent：当不希望这个端口被打开时，则使用该命令删除
