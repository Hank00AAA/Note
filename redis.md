# Redis

-  redis提供五种数据结构，各式各样的问题都会映射到这些结构体上（字符串、列表、集合、散列、有序集合）p6
- memcached只能存储普通字符串键值，且redis能够以两种不同的方式写入硬盘（rdb&aof？）
- redis主从复制
- mysql插入性能慢，一次插入会触发一次随机读，一次随机写
- 工具会极大地改变人们解决问题的方式
- 



## 列表

| command     | description |
| :---------- | ----------- |
| RPUSH/LPUSH |             |
| LRANGE      |             |
| LINDEX      |             |
| LPOP/RPOP   |             |



## 集合

| command             | descriotion |
| ------------------- | ----------- |
| SADD                |             |
| SMEMBERS            |             |
| SISMEMBER           |             |
| SREM                |             |
| SINTER/SUNION/SDIFF |             |



## 散列

| command | description |
| ------- | ----------- |
| HSET    |             |
| HGET    |             |
| HGETALL |             |
| HDEL    |             |



## 有序集合

| command       | description |
| ------------- | ----------- |
| ZADD          |             |
| ZRANGE        |             |
| ZRANGEBYSCORE |             |
| ZREM          |             |



## 发布与订阅

- 旧版redis如果一个订阅者消费速度不够快，不断积压的消息会影响redis服务稳定性。新版redis则会自动断开此类连接
- 数据传输可靠性有关。当redis客户端在执行订阅操作过程中断线，那么客户端对丢失在短线期间发送的所有消息



## redis事务

- redis会执行MULTI和EXEC之间的命令



## redis持久化

- aof & rdb



## redis可用性

- redis主从复制