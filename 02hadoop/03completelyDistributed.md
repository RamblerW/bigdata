

集群部署规划（以3台为例）

|      | 服务器1                                                 | 服务器2     | 服务器3     |
| ---- | ------------------------------------------------------- | ----------- | ----------- |
| HDFS | NameNode<br />DataNode                                  | DataNode    | DataNode    |
| YARN | ResourceManager<br />SecondaryNameNode<br />NodeManager | NodeManager | NodeManager |

- 配置slaves：将所有的节点服务器的IP分别添加到每台服务器的`/opt/module/hadoop-2.8.4/etc/hadoop/slaves`中
- 清空数据：`rm -rf /opt/module/hadoop-2.8.4/data/* /opt/module/hadoop-2.8.4/logs/*`
- 配置SSH免密登录
  - 同[伪分布式（一台机器）搭建](02hadoop/02pseudoDistributed.md)中的***设置SSH免密登录***
  - 把公钥向集群内的所有节点服务器均复制一遍
  - 所有节点服务器重复一遍以上操作
- 格式化 Namenode：在主节点服务器执行`hdfs namenode -format`
- hadoop主页中Live Nodes  = 节点服务器数
- <!--注：每台节点服务器的core-site.xml、hdfs-site.xml、yarn-site.xml、mapred-site.xml配置文件中的ip地址都用主节点的-->