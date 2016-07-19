
1. 数据节点

- 不是机器的意思
- ZK树形结构中的数据节点，用于存储数据
- 持久节点(Persistent) 一旦创建，除非主动调用删除操作，否则一直存储在ZK上
- 临时节点(Ephemeral):与客户端的会话绑定，一旦客户端会话失效，这个客户端创建的所有临时节点都会被移除
- 持久顺序节点(Persistent_Sequential):创建子节点的时候，如果设置树形为Sequential,则会自动在节点名后面追击啊一个整形数字，上线是整形的最大值。

临时节点的创建使用命令: 

> create -e /路径/节点名 数据 

当客户端(zkCli.sh|java)关闭(退出，close)之后，该节点直接消失

临时节点一般用来实现分布式锁

顺序节点的创建使用命令: 

> create -s /路径/节点名 数据

问题：集群中有多个及其，当某个通用的配置发生变化之后，怎么让所有服务器的配置都统一生效?
当集群某个节点宕机，其他节点怎么知道？

> ZK中引入了**watcher**机制来实现发布订阅功能，能够让多个订阅者同时监听一个主题对象，当这个主题对象自身状态发生变化时，会通知所有的订阅者

watcher组成:

1. 客户端
2. 客户端watchManager
3. ZK服务器

watcher机制

- 客户端向ZK服务器注册watcher的同时，会将watcher对象存储在客户端的watchManager
- ZK服务器触发watcher事件后，会向客户端发送通知，客户端线程从watchManager中调起watcher执行

wathcer接口:

- public class Zlock implements Watcher

- public void process(WatchedEvent event)

watcher事件:

- 通知状态:org.apache.zookeeper.WatcherEvent.KeeperState
- 事件类型:org.apache.zookeeper.WatcherEvent.EventType




