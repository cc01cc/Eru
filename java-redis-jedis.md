---
title: jedis
date: 2022-11-19
tags:
    - java
    - redis
    - jedis
excerpt: Java Redis Jedis
---

> redis/jedis: Redis Java client designed for performance and ease of use. <https://github.com/redis/jedis>

## 文件树

```txt
src/
├───main/java/com/cc01cc/jedis/util/
│   │
│   └───JedisConnectionFactory.java
│
└───test/java/com/cc01cc/test/
    │
    ├───TestJedis.java
    │
    └───TestJedisPool.java
```

## 引入依赖

```xml
<!-- pom.xml -->
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>4.3.0</version>
</dependency>
```

## 建立连接

```java
// TestJedis.java
@BeforeEach
void setUp() {
    // 1. 建立连接
    jedis = new Jedis("192.168.0.104", 6379);
    // 2. 设置密码
    jedis.auth("abc123");
    // 3. 选择库
    jedis.select(0);
}
```

## 操作

```java
// TestJedis.java
@Test
void testString() {
    // 存入数据
    String result = jedis.set("name", "testName");
    System.out.println("result = " + result);

    // 获取数据
    String name = jedis.get("name");
    System.out.println("name = " + name);
}
@Test
void testHash() {
    // 插入 hash 数据
    jedis.hset("user:1", "name", "Jack");
    jedis.hset("user:1", "age", "21");

    // 获取
    Map<String, String> map = jedis.hgetAll("user:1");
    System.out.println(map);
}
```

## 释放资源

```java
// TestJedis.java
@AfterEach
void tearDown() {
    if (jedis != null) {
        jedis.close();
    }
}
```

## Jedis 连接池

```java
// JedisConnectionFactory.java
public class JedisConnectionFactory {
    private static final JedisPool jedisPool;

    static {
        // 配置连接池
        JedisPoolConfig poolConfig = new JedisPoolConfig();
        poolConfig.setMaxTotal(8);
        poolConfig.setMaxIdle(8);
        poolConfig.setMinIdle(0);
        poolConfig.setMaxWait(Duration.ofMillis(1000));

        // 创建连接池对象
        jedisPool = new JedisPool(poolConfig,
                "192.168.0.104", 6379, 1000, "abc123");
    }

    public static Jedis getJedis() {
        return jedisPool.getResource();
    }
}

// TestJedisPool.java
@BeforeEach
void setUp() {
    // 建立连接
    jedis = JedisConnectionFactory.getJedis();
}
```

---

- 代码：<https://github.com/cc01cc/Initial/tree/master/09-01-redis/jedis-initial>

<!--
Copyright © 2022-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://github.com/cc01cc/cc01cc>
-->