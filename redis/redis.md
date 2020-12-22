brew services start redis
redis-cli

redis (nosql:非关系型数据库) 数据在内存
mysql (sql:关系型数据库)  数据存在磁盘中

### Redis 数据类型
    Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。
## String（字符串）
    string 是 redis 最基本的类型，你可以理解成与 Memcached 一模一样的类型，一个 key 对应一个 value。
    string 类型是二进制安全的。意思是 redis 的 string 可以包含任何数据。比如jpg图片或者序列化的对象。
    string 类型是 Redis 最基本的数据类型，string 类型的值最大能存储 512MB。
## Hash（哈希）
    Redis hash 是一个键值(key=>value)对集合。
    Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于存储对象。
## List（列表）
    Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边）。
## Set（集合）
    Redis 的 Set 是 string 类型的无序集合。
    集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。
## zset(sorted set：有序集合)
    Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
    不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
    zset的成员是唯一的,但分数(score)却可以重复。

### 常用命令
## string
    set key value	    设置 key 的值
    get key	            获取 key 的值
    del key	            删除 key 的值
    exists key	        查看此 key 是否存在
## hash 不保证顺序
    hset key field value    // hset myhash username zhangsan        // 存储
    hget key field          // hget myhash username                 // 获取指定的field对应的值
    hgetall key             // hgetall myhash                       // 获取所有的field和value
    hdel key field          // hdel myhash username                 // 删除指定的field对应的值
## 列表类型list 可以添加一个元素到列表的头部（左边）或者尾部（右边）
    lpush key value         // 将元素添加到列表左边
    rpush key value         // 将元素添加到列表右边
    lrange key start end    // 范围获取   lrange key 0 -1  // 获取多有
    lpop key                // 删除列表最左边的元素，并返回该元素
    rpop key                // 删除列表最右边的元素，并返回该元素
## 集合类型 set ： 不允许重复 不保证顺序
    sadd key value    sadd key a       sadd key b c d
    smembers key
    srem key value
## 有序集合类型 sortedset ： 不允许重复元素，且会根据score从小到大排序
    zadd key score value
    zrange key start end
    zrange key start end withscores
    zrem key value
## 通用命令
    keys *	            查看所有的 key
    type key            获取键对应的value的类型
    del key             删除指定的key value
    flushall	        消除所有的 key


### 持久化
1、redis是一个内存数据库，当redis服务器重启之后，或者电脑重启，数据会丢失，可以将redis内存中的数据持久化保存到硬盘的文件中。
2、redis持久化机制：
    1、RDB：默认方式，不需要进行配置，默认就使用这种机制；
        在一定的间隔时间中，检测key的变化情况，然后持久化数据
        1、编辑conf文件
            save 900 1
            save 300 10
            save 60 10000
        2、重新启动redis服务器，并指定配置文件名称
    2、AOF：日志记录的方式，可以记录每一条命令操作。可以每一次命令操作后，持久化数据
        1、编辑conf文件
            appendonly no (关闭aof) -> appendonly yes (开启aof)

            # appendfsync always ： 每一次操作都进行持久化
            appendfsync everysec ： 每隔一秒进行一次持久化
            # appendfsync no     ： 不进行持久化
        2、重新启动redis服务器，并指定配置文件名称      

redis-cli

## 在远程服务上执行命令
redis-cli -h host -p port -a password
redis-cli -h 127.0.0.1 -p 6379 -a "mypass"