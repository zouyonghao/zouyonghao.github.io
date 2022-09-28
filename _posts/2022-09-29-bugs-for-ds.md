---
title: Bugs found for distributed systems
layout: post
---

Here I list some of bugs found by my fuzzing tools for distributed systems and databases.

* Braft/brpc
    * [memory leak](https://github.com/baidu/braft/issues/268)
    * [Fail to rename](https://github.com/baidu/braft/issues/272)
    * [No exception handling after error?](https://github.com/baidu/braft/issues/273)
    * [Check failed: meta.term == header.term](https://github.com/baidu/braft/issues/279)
    * [data loss after restart?](https://github.com/baidu/braft/issues/280)
    * [memory leak if binding failed](https://github.com/apache/incubator-brpc/issues/1390)
    * [Node cannot response after one node stepped down](https://github.com/baidu/braft/issues/338)
    * [TaskControl may interrupt non-exist threads](https://github.com/apache/incubator-brpc/issues/1624)

* C-Raft
    * [ASan reported heap-buffer-overflow](https://github.com/canonical/raft/issues/236)
    * [ASan report bad-free](https://github.com/canonical/raft/issues/219)
    * [ASan reported SEGV](https://github.com/canonical/raft/issues/202)
    * [example/server failed to start after killing](https://github.com/canonical/raft/issues/199)
    * [Fix memory leak when crc check failed.](https://github.com/canonical/raft/pull/249)

* NuRaft
    * [Got FATL logs when test with the calc example](https://github.com/eBay/NuRaft/issues/271)
    * [Exit if ctrl-d received](https://github.com/eBay/NuRaft/pull/211)

* RedisRaft
    * [Fix heap buffer overflow](https://github.com/RedisLabs/redisraft/pull/165)
    * [Assertion `cache->start_idx + cache->len == idx' failed](https://github.com/RedisLabs/redisraft/issues/189)
    * [Radis raft panic](https://github.com/RedisLabs/redisraft/issues/107)
    * [Assertion `(c->flags & REDIS_SUBSCRIBED || c->flags & REDIS_MONITORING)' failed.](https://github.com/RedisLabs/redisraft/issues/104)

* RethinkDB
    * [Memory bugs reported by ASan](https://github.com/rethinkdb/rethinkdb/issues/6956)
    * [Guarantee failed: [iterator_and_is_new.second] value to be inserted already exists.](https://github.com/rethinkdb/rethinkdb/issues/6962)

* Aerospike
    * [stack-buffer-underflow](https://github.com/aerospike/aerospike-server/issues/33)
    * [error creating fabric published endpoint list](https://github.com/aerospike/aerospike-server/issues/27)
    * [dirty read if the connection is not stable?](https://github.com/aerospike/aerospike-server/issues/30)

* ClickHouse
    * [Distributed table cannot be used after rename column](https://github.com/ClickHouse/ClickHouse/issues/37899)
    * [Distributed table cannot find column with "greater" query](https://github.com/ClickHouse/ClickHouse/issues/37557)
    * [Not found column in substr](https://github.com/ClickHouse/ClickHouse/issues/37523)
    * [Constraint check throws Missing columns exception](https://github.com/ClickHouse/ClickHouse/issues/37509)
    * [Does distributed table support select with order?](https://github.com/ClickHouse/ClickHouse/issues/37475)
    * [Always use default database when creating distributed table](https://github.com/ClickHouse/ClickHouse/issues/37318)
    * [Cannot drop table after a wrong create distributed table statement executed](https://github.com/ClickHouse/ClickHouse/issues/37316)
    * [Cannot create table after drop](https://github.com/ClickHouse/ClickHouse/issues/37314)
    * [Create Distributed table can succeed if the database not exists](https://github.com/ClickHouse/ClickHouse/issues/37076)
    * [Fatal error when createDatabase](https://github.com/ClickHouse/ClickHouse/issues/29255)
    * [Got weird fatal log: floating point inexact result](https://github.com/ClickHouse/ClickHouse/issues/26300)
    * [Logical error: 'It's new replica, but database is not empty'](https://github.com/ClickHouse/ClickHouse/issues/26015)

* etcd
    * [runtime error: slice bounds out of range](https://github.com/etcd-io/etcd/issues/13493)

* ZooKeeper
    * [Committing zxid 0x100000003 but next pending txn 0x100000002](https://issues.apache.org/jira/browse/ZOOKEEPER-4418)
    * [NullPointerException in SendAckRequestProcessor](https://issues.apache.org/jira/browse/ZOOKEEPER-4409)
    * [Zookeeper crashes after commit fail](https://issues.apache.org/jira/browse/ZOOKEEPER-4408)
