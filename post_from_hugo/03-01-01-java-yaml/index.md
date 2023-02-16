---
title: java 读取 yaml
description: 这是一切开始的地方
date: 2022-06-04
slug: java-yaml
categories:
    - Java
---

## 1. pom.xml

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.dataformat/jackson-dataformat-yaml -->
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-yaml</artifactId>
    <version>2.13.3</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.13.3</version>
</dependency>
```

## 2. 文件结构

```txt
.
├──  Main.java
└──  pojo
        ├── Config.java
        ├── Qq.java
        ├── Feishu.java
        └── Dingtalk.java

config.yml
```

## 3. config.yml

yaml 中的层级关系，转化到 Java 中，类似于类的包裹

```yml
qq:
  account:
  key:

feishu:
  account:
  key:

dingtalk:
  account:
  key:
```

## 4. Main.java

```java
public static void main(String[] args) throws Exception{
    File f = new File("path_to_config.yml");
    ObjectMapper objectMapper = new ObjectMapper(new YAMLFactory());
    Config config = objectMapper.readValue(f, Config.class);
}
```

## 5. Config.java

```java
import lombok.Getter;
import lombok.Setter;

@Setter
@Getter
public class Config {
    // 确保变量名的大小写和 yaml 文件参数一致
    private Qq qq;
    private Feishu feishu;
    private DingTalk dingtalk;
}

```

## 6. Qq/Feishu/Dingtalk.java

以 Qq.java 为例

```java
import lombok.Getter;
import lombok.Setter;

import java.util.Arrays;

@Setter
@Getter
public class Qq {
    private Long account;
    private String key;
}
```

## 7. 注意点

1. yaml 中 `@` 等字符，可以使用单双引号包裹
2. yaml 区分大小写

## 8. 参考

1. YAML file read/parse and write in java| Latest tutorials: <https://www.w3schools.io/file/yaml-java-read-write/>

---

- 文章系个人学习总结，希望可以给大家带来些许启发，欢迎提出建议或给予指正。
- 本作品采用[知识共享署名-相同方式共享 4.0 国际许可协议](https://creativecommons.org/licenses/by-sa/4.0/legalcode.zh-Hans)进行许可。
- 欢迎大家转载分享，转载请标明源地址，谢谢