#### 分布式锁

setnx获取锁 --> setExpire给锁加过期时间

### Keys

Keys获取特定模式的所有key，阻塞

### Scan

Keys获取特定模式的所有key，非阻塞，有一定重复概率，需要去重。

#### zrangebyscore

获取前N个数据轮询处理

#### bgsave

全量持久化

#### aof

增量持久化

#### restore data

use bgsave to reconstruct memory, and use aof to re-perform recent cmds to restore memory completely.

#### bgsave

fork the child thread to operate bgsave, with copy and write technology.

#### 同步机制

Redis可以使用主从同步，从从同步。第一次同步时，主节点做一次bgsave，并同时将后续修改操作记录到内存buffer，待完成后将rdb文件全量同步到复制节点，复制节点接受完成后将rdb镜像加载到内存。加载完成后，再通知主节点将期间修改的操作记录同步到复制节点进行重放就完成了同步过程。

#### Redis集群

Redis Sentinal着眼于高可用，在master宕机时会自动将slave提升为master，继续提供服务。

Redis Cluster着眼于扩展性，在单个redis内存不足时，使用Cluster进行分片存储。