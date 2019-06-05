

> 环境配置

- 关闭防火墙

  - 关闭防火墙：`systemctl stop firewalld.service`
  - 禁用防火墙：`systemctl disable firewalld.service`
  - 查看防火墙：`systemctl status firewalld.service`

- 关闭Selinux

  - `vi /etc/selinux/config`
  - 将`SELINUX=enforcing`改为`SELINUX=disabled`

- 修改IP

  - 查看网卡：`ifconfig`，查看网卡名和IP地址（如`eth0`、`192.168.2.111`）

  - `vi /etc/sysconfig/network-scripts/ifcfg-eth0`

    ```
    # 修改如下2个值
    BOOTPROTO=static
    ONBOOT=yes
    
    # 配置ip
    IPADDR=192.168.2.111
    GATEWAY=192.168.2.1
    NETMASK=255.255.255.0
    ```
    
  - 重启网卡：`service network restart`

- 修改主机名：`hostnamectl set-hostname bigdata111`

- IP与主机名关系映射

  - `vi /etc/hosts`

    ```
    # 追加
    192.168.2.111 bigdata111
    ```

  - Mac/Windows IP与主机关系映射

    - Mac：`vi /etc/hosts`

      ```
      # 追加
      192.168.2.111 bigdata111
      ```

    - Windows：C:\Windows\System32\drivers\etc\hosts

      ```
      # 追加
      192.168.2.111 bigdata111
      ```

- 安装 jdk & Hadoop：见[软件安装](01linux/02software.md)

> 集群配置

- 创建路径：`mkdir /opt/module/hadoop-2.8.4/data /opt/module/hadoop-2.8.4/logs`

- 配置文件：/opt/module/hadoop-2.8.4/etc/hadoop

  - core-site.xml（放在`configuration`标签之间）

    ```
    <!-- 指定HDFS中NameNode的地址，低版本端口号为8020-->
    <property>
    	<name>fs.defaultFS</name>
    	<value>hdfs://bigdata111:9000</value>
    </property>
    
    <!-- 指定hadoop运行时产生文件的存储目录-->
    <property>
    	<name>hadoop.tmp.dir</name>
    	<value>/opt/module/hadoop-2.8.4/data</value>
    </property>
    ```

  - hdfs-site.xml（放在`configuration`标签之间）

    ```
    <!--数据冗余数/备份数-->
    <property>
    	<name>dfs.replication</name>
    	<value>3</value>
    </property>
    
    <!--secondary NameNode的地址-->
    <property>
    	<name>dfs.namenode.secondary.http-address</name>
    	<value>bigdata111:50090</value>
    </property>
    
    <!--关闭权限校验-->
    <property>
    	<name>dfs.permissions</name>
    	<value>false</value>
    </property>
    ```

  - yarn-site.xml（放在`configuration`标签之间）

    ```
    <!-- reducer获取数据的方式-->
    <property>
    	<name>yarn.nodemanager.aux-services</name>
    	<value>mapreduce_shuffle</value>
    </property>
    
    <!-- 指定YARN的ResourceManager的地址-->
    <property>
    	<name>yarn.resourcemanager.hostname</name>
    	<value>bigdata111</value>
    </property>
    
    <!-- 日志聚集功能使能-->
    <property>
    	<name>yarn.log-aggregation-enable</name>
    	<value>true</value>
    </property>
    
    <!-- 日志保留时间设置7天(秒) -->
    <property>
    	<name>yarn.log-aggregation.retain-seconds</name>
    	<value>604800</value>
    </property>
    ```

  - mapred-site.xml

    - 改名（可选）：`mv mapred-site.xml.template mapred-site.xml`

    - 配置（放在`configuration`标签之间）

      ```
      <!-- 指定mr运行在yarn上-->
      <property>
      	<name>mapreduce.framework.name</name>
      	<value>yarn</value>
      </property>
      
      <!--历史服务器的地址-->
      <property>
      	<name>mapreduce.jobhistory.address</name>
      	<value>bigdata111:10020</value>
      </property>
      
      <!--历史服务器页面的地址-->
      <property>
      	<name>mapreduce.jobhistory.webapp.address</name>
      	<value>bigdata111:19888</value>
      </property>
      ```

  - hadoop-env.sh、yarn-env.sh、mapred-env.sh配置`JAVA_HOME`

    ```
    # 追加
    export JAVA_HOME=/opt/module/jdk1.8.0_144
    ```

  - salves（可选）：修改为`bigdata111`

- 格式化 Namenode：`hdfs namenode -format`

- 设置SSH免密登录（否则每次启动集群的时候都需要输入多次密码）

  - 生成公钥和私钥
    - `ssh-keygen -t rsa`
    - 直接敲回车（三次）
  - 拷贝公钥到要免密登录的机器
    - `ssh-copy-id hostname`

- 启动集群：`start-all.sh`

- 查看进程是否启动：`jps`，若RM、NM、DN、NN、SN(2NN)都启动，则说明成功

- 查看hadoop主页：见[基础知识笔记](04hadoop.md)