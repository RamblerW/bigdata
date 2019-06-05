

- 查看系统版本：`cat /etc/redhat-release`

- 查看进程：`jps`

- 清屏：`clear`或`ctrl + L`

- 历史命令：`history`

- 上传下载文件工具 lrzsz

  - 上传：`rz`
  - 下载：`sz fileName`

- 服务器间文件传输：`scp -r fileName username@hostname:targetPath`

- 防火墙

  - 查看状态：`systemctl status firewalld.service`
  - 关闭：`systemctl stop firewalld.service`
  - 禁用：`systemctl disable firewalld.service`

- yum

  - 配置阿里yum源
    - 下载aliyun yum源repo文件：`wget -O /etc/yum.repos.d/CentOS-Base.repo  http://mirrors.aliyun.com/repo/Centos-7.repo`
    - 清除缓存：`yum clean all`
    - 把yum源缓存到本地，加快软件的搜索和安装速度：`yum makecache`

  - 查找安装包：`yum search softwareName`
  - 安装：`yum -y install packageName`
  - 查看已安装：`yum list installed`

- 文件目录类

  - 返回上一个操作的目录：`cd -`
  - 当前绝对路径：`pwd`
  - 创建文件：`touch fileName`
  - 创建目录：`mkdir directoryName`
    - 递归创建：`mkdir -p directoryName`
  - 复制文件或目录：`cp oldDir newDir`
    - 递归复制：`cp -r oldDir newDir`
  - 删除：`rm dirName`
    - 递归删除：`rm -rf dirName`
  - 移动：`mv oldDir newDir`
  - 重命名：`mv oldName newName`
  - 查看文件：`cat fileName`
  - 监控文件：`tail -f fileName`或`tailf fileName`
  - 追加：`echo addStr >> fileName`
  - 覆盖：`echo coverStr > fileName`
  - 连接：
    - 软连接（只生成一个镜像）：`ln -s oldFile newFile`
    - 硬连接（生成相同的文件）：`ln oldFile newFile`

- Vim
  - 进入：`vim filename`
  - 一般模式
    - 复制一行：`yy`
    - 复制 N 行：`yNy`
    - 粘贴：`p`
    - 撤销：`u`
    - 删除一行：`dd`
    - 删除 N 行：`dNd`
    - 移动到行头：`shift + ^`
    - 移动到行尾：`shift + $`
    - 跳到最后一行：`shift + g`
    - 跳到第 N 行：`N + shift + g`或`N + g + g`
    - 显示行号：`:set nu`
    - 搜索：`\`
    - 搜索下一个：`n`
  - 编辑模式
    - 进入编辑：`i`
    - 下一行编辑：`o`
    - 退出编辑：`Esc`
  - 指令模式
    - 保存：`w`
    - 退出：`q`
    - 强制：`!`
  
- 时间日期类
  - 当前时间：`date`
  - 设置时间：`date -s 'yyyy-MM-dd HH:mm:ss'`
  - 查看日历：`cal [option]`
  
- 用户管理类
  - 新增用户：`useradd userName`
  - 删除用户：`userdel userName`
  - 判断用户是否存在：`id userName`
  - 设置密码：`passwd userName`
  - 切换用户：`su userName`
  - 查看在线用户：`w`
  
- 磁盘分区类
  - 查看分区：`fdisk -l`
  - 查看硬盘：`df`
  
- 搜索查找类
  - find \[搜索范围\]\[匹配条件\]
    - 按文件名：`find /opt -name *.jar`
    - 按拥有者：`find /opt -user root`
    - 按文件大小：`find /opt -size +1024`(大于1M的文件）
  - grep管道
  
- 进程线程类
  - 查看进程：`ps -aux`
  - 查看系统状态：`top`
  - 杀死进程：`kill`
  
- 压缩和解压
  - 解压tar到指定目录：`tar -zxvf fileName -C resultDir`
  - 压缩文件：`gzip fileName`，注：不能压缩目录
  - 解压缩：`gunzip fileName`
  - 压缩文件：`zip zipName fileName`
  - 解压缩：`unzip fileName`
  
- 定时任务 Crontab
  - 编辑定时任务：`crontab -e`
  - 查询定时任务：`crontab -l`
  - 删除定时任务：`crontab -r`
  - cron 表达式（\* \* \* \* \*）：分 时 天 月 周
  
- 配置网卡：`vi /etc/sysconfig/network-srcipts/ifcfg-eth0`