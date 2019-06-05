> **Q1**：Parallels Desktop克隆centos虚拟机后，设置静态ip不生效，重启网卡时报错

- 问题原因：新的虚拟机的mac地址发生了变化，需要修改网卡配置文件中的mac地址
- 解决方案：执行`ifconfig`查看mac地址（***ether项的值***），然后修改网卡配置文件***ifcfg-eth0***中***HWADDR***的值
- 参考链接：https://segmentfault.com/a/1190000005932091

> **Q2**：centos7重启网卡报错<font color=red>Restarting network (via systemctl):  Job for network.service failed. See 'systemctl status network.service' and 'journalctl -xn' for detail</font>，然后执行`systemctl status network.service`后显示<font color=red>Failed to start LSB: Bring up/down networking</font>

- 问题原因：同[Q1](FAQ.md)
- 参考链接：https://www.cnblogs.com/zyw-205520/p/5328887.html

> **Q3**：centos7执行`ifconfig`命令提示<font color=red>Command not found</font>

- 问题原因：centos7最小化安装时未安装一些工具
- 解决方案：执行命令`sudo yum install net-tools`安装
- 参考链接：https://blog.51cto.com/renxi/2338405