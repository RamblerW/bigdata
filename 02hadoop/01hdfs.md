> 概念

- 组成
  - NameNode：负责管理整个文件系统的元数据，以及每一个路径（文件）所对应的数据块信息
  - DataNode：负责管理用户的文件数据块，每一个数据块都可以在多个datanode上存储多个副本
  - Secondary NameNode：用来检测HDFS状态的辅助后台程序，每隔一段时间获取HDFS元数据的快照
- 文件块大小
  - HDFS中的文件在物理上市分块存储，块的大小通过参数`dfs.blocksize`配置
  - hadoop2.x中默认为128M，老版本为64M

> 常用命令

- 基本语法：`hadoop fs -` + linux命令
- 查看hadoop根目录：
- 查看目录内容：`hadoop fs -ls /`
- 创建目录：`hadoop fs -mkdir -p hdfsDir`
- 从本地剪切到hdfs：`hadoop fs -moveFromLocal localDir hdfsDir`
- 追加文件到另一个末尾：`hadoop fs -appendToFile localDir hdfsDir`
- 显示文件内容：`hadoop fs -cat hdfsDir`
- 监控文件：`hadoop fs -tail -f hdfsDir`
- 修改权限
  - `hadoop fs -chmod 777 hdfsDir`
  - `hadoop fs -chown someuser:somegrp hdfsDir`
- 拷贝文件：`hadoop fs -cp oldHdfsDir newHdfsDir`
- 移动/重命名：`hadoop fs -mv oldHdfsDir newHdfsDir`
- 下载文件到本地
  - `hadoop fs -copyToLocal hdfsDir localDir`
  - `hadoop fs -get hdfsDir localDir`
- 上传文件
  - `hadoop fs -copyFromLocal localDir hdfsDir`
  - `hadoop fs -put localDir hdfsDir`
- 合并文件：`hadoop fs -getmerge sourceDir resultDir`
- 删除：`hadoop fs -rm -r hdfsDir`
- 统计可用空间：`hadoop fs -df -h hdfsDir`
- 统计文件夹大小
  - `hadoop fs -du -s -h hdfsDir`
  - `hadoop fs -du -h hdfsDir`
- 统计文件节点数量：`hadoop fs -count hdfsDir`
- 设置hdfs中文件的副本数量：`hadoop fs -setrep repCount hdfsDir`