---
layout: post
title: redis简介
categories: JavaSE
tags: redis
author: fidemyuan
---

## 什么是redis

Redis 是一个使用 C 语言写成的，开源的 key-value 数据库。。和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list(链表)、set(集合)、zset(sorted set –有序集合)和hash（哈希类型）。这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。目前，Vmware在资助着redis项目的开发和维护。<br>

redis是一种基于内存的数据库，并且提供一定的持久化功能。<br>

Redis和MongoDB是当前使用最广泛的NoSQL<br>

## redis应用场景

主要是用于存储缓存用的数据；<br>

1.存储，日常对数据库的操作中，读操作的次数远超写操作，比例约 1:9 到 3:7。而使用SQL语句去数据库进行读写操作时，数据库就会去磁盘把对应的数据索引取回来，这是一个相对较慢的过程。把数据放入redis，也就是内存中查询速度回很快，限于成本的原因，一般我们只是使用 Redis 存储一些常用和主要的数据，比如用户登录的信息等。

2.高读/写场合。在涉及到大量数据请求时：比如网站首页、爆款商品抢购、秒杀.....访问量瞬间增加成千上万。数据库不能承受，极其容易造成数据库系统瘫痪，最终导致服务宕机的严重生产问题。<br>


3.排行榜，如果使用传统的关系型数据库来做，非常麻烦，而利用Redis的SortSet数据结构能够非常方便搞定；<br>

4.计算器/限速器，利用Redis中原子性的自增操作，我们可以统计类似用户点赞数、用户访问数等，这类操作如果用MySQL，频繁的读写会带来相当大的压力；限速器比较典型的使用场景是限制某个用户访问某个API的频率，常用的有抢购时，防止用户疯狂点击带来不必要的压力；<br>

5.好友关系，利用集合的一些命令，比如求交集、并集、差集等，可以方便搞定一些共同好友、共同爱好之类的功能；<br>

6.简单消息队列，除了Redis自身的发布/订阅模式，我们也可以利用List来实现一个队列机制，比如到货通知、邮件发送之类的需求，不需要高可靠，但是会带来非常大的DB压力，完全可以用List来完成异步解耦；<br>

7.Session共享，以PHP为例，默认Session是保存在服务器的文件中，如果是集群服务，同一个用户过来可能落在不同机器上，这就会导致用户频繁登陆；采用Redis保存Session后，无论用户落在那台机器上都能够获取到对应的Session信息。<br>

## redis优势

1.速度快，完全基于内存，使用C语言实现,支持每秒十几万此的读/写操作，其性能远超数据库，网络层使用epoll解决高并发问题，单线程模型避免了不必要的上下文切换及竞争条件；<br>

2.丰富的数据类型，Redis有8种数据类型，当然常用的主要是 String、Hash、List、Set、 SortSet 这5种类型，他们都是基于键值的方式组织数据。每一种数据类型提供了非常丰富的操作命令，可以满足绝大部分需求，如果有特殊需求还能自己通过 lua 脚本自己创建新的命令（具备原子性）；<br>

3.它还支持事务、持久化、支持集群、分布式、主从同步等配置<br>

4.还提供了像慢查询分析、性能测试、Pipeline、事务、Lua自定义命令、Bitmaps、HyperLogLog、发布/订阅、Geo等个性化功能。<br>
