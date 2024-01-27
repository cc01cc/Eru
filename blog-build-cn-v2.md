---
title: 博客 cn 站搭建 v2.1
copyright: BY-NC-ND
date: 2023-04-01 12:34:48
tags:
    - blog-build
categories:
    - blog-build
---

- [1. 结构设计](#1-结构设计)
- [2. 准备](#2-准备)
- [3. 配置 OSS 对象存储](#3-配置-oss-对象存储)
- [4. 校验 OSS 配置](#4-校验-oss-配置)
- [5. OSS 域名配置并开启 HTTPS](#5-oss-域名配置并开启-https)
- [6. 编写 spring boot 程序](#6-编写-spring-boot-程序)
  - [6.1. 示例代码如下](#61-示例代码如下)
  - [6.2. 打包测试](#62-打包测试)
  - [6.3. 添加部署脚本](#63-添加部署脚本)
  - [6.4. 搭建自动部署流水线](#64-搭建自动部署流水线)
  - [6.5. 验证部署](#65-验证部署)
  - [6.6. 添加钉钉机器人通知](#66-添加钉钉机器人通知)
- [7. ECS 域名配置](#7-ecs-域名配置)
- [8. 配置 NGINX](#8-配置-nginx)
  - [8.1. no "ssl\_certificate" 问题](#81-no-ssl_certificate-问题)
    - [8.1.1. 【方法一】](#811-方法一)
    - [8.1.2. 【方法二】手动取消注释](#812-方法二手动取消注释)
  - [8.2. 检查 nginx 配置](#82-检查-nginx-配置)
    - [8.2.1. nginx 配置排查](#821-nginx-配置排查)
- [9. 添加 DCDN](#9-添加-dcdn)
  - [9.1. 添加 WAF 边缘防护](#91-添加-waf-边缘防护)
- [10. 搭建 cn 站自动部署流水线](#10-搭建-cn-站自动部署流水线)
  - [10.1. 添加钉钉机器人通知](#101-添加钉钉机器人通知)
- [11. 添加云监控](#11-添加云监控)
  - [11.1. 自动拨测](#111-自动拨测)
- [12. 可以优化的地方](#12-可以优化的地方)
- [13. 图库 v2 测试](#13-图库-v2-测试)
- [14. 记录](#14-记录)

## 1. 结构设计

![blog-build-v2.1](https://v01.static.cc01cc.cn/blog-build-v2-1.jpg)

## 2. 准备

1. ECS 服务器 * 1
2. OSS 对象存储 * 1
3. 域名 * 1（若服务器在境内，域名需备案）
4. 已安装的 picGo 软件（用于图片上传，可自行选择其他方式）
5. 记事本（随时复制粘贴一些配置以及重要信息）

## 3. 配置 OSS 对象存储

1. 前往对象存储 Bucket 列表 <https://oss.console.aliyun.com/bucket> 进入需要操作的 Bucket
2. 在文件列表中新建两个目录 `hexo_zeo`, `image_zeo`，分别用于存放博客页面以及图片
3. 前往 RAM 访问控制 - 用户: <https://ram.console.aliyun.com/users>
4. 创建二个用户（不需要授权，后续在 Bucket 中授权，可以自行判断是否添加用户组）：
   1. 允许读写 博客页面 的用户（供 hexo deploy 使用）
   2. 允许读写 图片 的用户（供 picGo 使用）
5. 创建用户后，分别进入用户详情页，创建 AccessKey，**记录 ID 和 key**
6. 配置 Bucket 授权策略（都要求 https 访问）：
   1. 分别指定资源将 读写 `hexo_zeo/*`, `image_zeo/*` 授权给子账号
   2. 指定资源将 只读(不包含ListObject) `hexo_zeo/*`, `image_zeo/*` 授权给 ecs 公网 ip
      1. OSS 资源预览必须使用 自定义域名，所以只能使用公网 ip
      2. 参考：(如何配置访问OSS文件时是预览行为？: <https://help.aliyun.com/document_detail/600802.html?spm=a2c4g.107034.0.i3#section-4e5-f7l-jpp>)
   3. 关于更多 阿里云 OSS 鉴权的流程和说明可以查看 OSS鉴权详解 <https://help.aliyun.com/document_detail/212436.html>

## 4. 校验 OSS 配置

1. 打开 picGo，配置阿里云 OSS，输入 `image_zeo` 对应读写子账号的 ID 和 key，测试图片是否可以上传。
2. 开启 ECS 服务器控制台，使用 `wget` 获取 OSS 中的资源，验证 ECS ip 授权是否正确
3. 进入本地 hexo 目录，执行 `npm install hexo-deployer-ali-oss --save` 安装部署插件
4. 配置 hexo

    ```yml
    deploy:
        type: ali-oss
        region: <您的oss 区域代码，例 oss-cn-hangzhou>
        accessKeyId: <您的oss  accessKeyId>
        accessKeySecret: <您的oss accessKeySecret>
        bucket: <您的bucket name>
        remotePath: <您要部署的目录>
    ```

5. 运行 `hexo deploy` 查看是否部署成功
6. 前往 OSS 文件列表，核验文件是否上传成功

## 5. OSS 域名配置并开启 HTTPS

1. 前往数字证书管理服务管理控制台<https://yundun.console.aliyun.com/>
2. 添加免费证书（每年可以领20份免费证书）域名之后需要绑定到 bucket
3. 前往对象存储 Bucket 列表 <https://oss.console.aliyun.com/bucket> 进入需要操作的 Bucket
4. Bucket 配置 > 域名管理，绑定域名，记录自己填写的域名
5. 点击绑定的域名，继续绑定证书
6. 进入 Bucket 文件列表，使用刚刚绑定的域名采用 HTTPS 模式复制并访问文件临时 url，验证操作是否成功

之后 ECS 将通过这个域名访问 OSS。

## 6. 编写 spring boot 程序

> 开发工具 VSCode + Java Extension Pack + Spring Boot Extension Pack

### 6.1. 示例代码如下

> 以 博客文件 hexo server 为例

pom 文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
 <modelVersion>4.0.0</modelVersion>
 <parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>3.0.5</version>
  <relativePath /> <!-- lookup parent from repository -->
 </parent>
 <groupId>com.cc01cc</groupId>
 <artifactId>blog-zeo</artifactId>
 <version>0.0.1-SNAPSHOT</version>
 <name>blog-zeo</name>
 <description>cc01cc's blog</description>
 <properties>
  <java.version>17</java.version>
 </properties>
 <dependencies>
  <!-- https://mvnrepository.com/artifact/org.apache.maven.plugins/maven-resources-plugin -->
  <dependency>
   <groupId>org.apache.maven.plugins</groupId>
   <artifactId>maven-resources-plugin</artifactId>
   <version>3.3.1</version>
  </dependency>
  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-devtools</artifactId>
   <scope>runtime</scope>
   <optional>true</optional>
  </dependency>
  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-configuration-processor</artifactId>
   <optional>true</optional>
  </dependency>
  <dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
   <optional>true</optional>
  </dependency>
  <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
   <scope>test</scope>
  </dependency>
  <dependency>
   <groupId>com.aliyun.oss</groupId>
   <artifactId>aliyun-sdk-oss</artifactId>
   <version>3.10.2</version>
  </dependency>
  <dependency>
   <groupId>com.aliyun</groupId>
   <artifactId>sts20150401</artifactId>
   <version>1.1.3</version>
  </dependency>
 </dependencies>

 <build>
  <finalName>blog-zeo</finalName>
  <resources>
   <resource>
    <directory>src/main/resources</directory>
    <!-- 需要将 maven 的 property 写入 src/main/resources
				下所有的配置文件中（只要该配置文件中使用了propetry对应的占位符，如上面 application.yml 配置的那样 -->
    <filtering>true</filtering>
   </resource>
  </resources>
  <plugins>
   <plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
   </plugin>
   <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-jar-plugin</artifactId>
    <version>2.4</version>
   </plugin>
  </plugins>
 </build>
 <!-- 参考：Maven 之 profile 与Spring boot 的 profile - 夏之夜 - 博客园:
	https://www.cnblogs.com/sandyflower/p/11600058.html -->
 <profiles>
  <profile>
   <id>local</id>
   <activation>
    <activeByDefault>true</activeByDefault>   <!-- 运行时未指明 profile,则使用默认的，该配置表示 dev为默认配置 -->
   </activation>
   <properties>
    <package.env>local</package.env>
   </properties>
  </profile>
  <profile>
   <id>ecs</id>
   <properties>
    <package.env>ecs</package.env>
   </properties>
  </profile>
 </profiles>
</project>
```

Controller 层代码如下

```java
@RestController
public class BlogController {

    private static final Logger logger = LoggerFactory.getLogger(BlogController.class);
    @Resource
    private BlogService blogService;

    @Value("${oss.url}")
    private String targetUrlPrefix;
    @Value("${oss.objectDir}")
    private String objectDir;

    @RequestMapping("/{*objectName}")
    public ResponseEntity<byte[]> getFile(@PathVariable String objectName, HttpServletRequest request) {
        // URL url = blogService.getHexoServerUrl(objectName);
        logger.info("objectName: " + objectName);
        // 日志记录 request 参数
        logger.info("request: " + request);
        // 以目录结尾的请求自动添加 index.html
        if (objectName.endsWith("/")) {
            objectName = objectName + "index.html";
        }
        URL url;
        try {
            url = new URL(targetUrlPrefix + objectDir + objectName);
            logger.info("url: " + url);
            return blogService.sendHttpRequest(url, request);
        } catch (MalformedURLException e) {
            logger.error("url error: " + e.getMessage());
            e.printStackTrace();
        }
        return null;
    }
}
```

service 层代码如下

```java
    public ResponseEntity<byte[]> sendHttpRequest(URL url, HttpServletRequest request) {

        logger.info("url: " + url);
        HttpHeaders headers = new HttpHeaders();
        Enumeration<String> headerNames = request.getHeaderNames();
        while (headerNames.hasMoreElements()) {
        String headerName = headerNames.nextElement();
        headers.set(headerName, request.getHeader(headerName));
        }

        HttpEntity<String> entity = new HttpEntity<>(headers);
        logger.info("entity: " + entity);
        ResponseEntity<byte[]> response;
        try {
            // RestTemplate 在字符串转义的时候有个大坑，所以这儿直接转换成了 URI
            response = restTemplate.exchange(url.toURI(), HttpMethod.GET, entity, byte[].class);
            logger.info("response: " + response.getStatusCode());
            return response;
        } catch (RestClientException e) {
            logger.error("RestClientException: " + e.getMessage());
            e.printStackTrace();
        } catch (URISyntaxException e) {
            logger.error("URISyntaxException: " + e.getMessage());
            e.printStackTrace();
        }
        return null;
    }
```

Application 层代码如下

```java
@SpringBootApplication
public class BlogApplication {

    public static void main(String[] args) {
        SpringApplication.run(BlogApplication.class, args);
    }

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

配置文件如下

```yml
# application.yml
spring:
  application:
    name: springboot-zeo-blog
  mvc:
    pathmatch:
      matching-strategy: PATH_PATTERN_PARSER
  autoconfigure:
    exclude: org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
  # 默认 local 环境
  profiles:
    active: @package.env@
```

```yml
# application-local.yml
server:
  port: 12050
logging: 
  file:
    path: ./logs
oss:
  url: http://127.0.0.1:4000 # 此处填写博客文件的根目录，如果再 OSS 上就填写 OSS 的外网地址
```

### 6.2. 打包测试

1. 使用 `maven package` 打包 spring 应用
2. 将 `target/***.jar` 上传到服务器
3. 在服务器运行 `java -jar ***.jar` 等待启动成功
4. 使用 `wget http://127.0.0.1:12050/hexo/index.html` 测试是否可以正常获取资源

### 6.3. 添加部署脚本

添加部署脚背，为后续自动部署做准备

在项目的根目录（不是仓库的根目录）添加 `deploy.sh`

```bash
# 改编自 https://atomgit.com/flow-example/spring-boot/blob/master/deploy.sh
#!/bin/bash

# 修改APP_NAME为云效上的应用名，需和 jar 包名一致
APP_NAME=blog-zeo

PROG_NAME=$0
ACTION=$1
APP_START_TIMEOUT=20                          # 等待应用启动的时间
APP_PORT=12050                                 # 应用端口
HEALTH_CHECK_URL=http://127.0.0.1:${APP_PORT}/hexo/index.html # 应用健康检查URL
APP_HOME=/home/admin/${APP_NAME}              # 从package.tgz中解压出来的jar包放到这个目录下
JAR_NAME=${APP_HOME}/target/${APP_NAME}.jar   # jar包的名字
JAVA_OUT=${APP_HOME}/logs/start.log           #应用的启动日志

# 创建出相关目录
mkdir -p ${APP_HOME}
mkdir -p ${APP_HOME}/logs
usage() {
    echo "Usage: $PROG_NAME {start|stop|restart}"
    exit 2
}

health_check() {
    exptime=0
    echo "checking ${HEALTH_CHECK_URL}"
    while true; do
        status_code=$(/usr/bin/curl -L -o /dev/null --connect-timeout 5 -s -w %{http_code} ${HEALTH_CHECK_URL})
        if [ "$?" != "0" ]; then
            echo -n -e "\rapplication not started"
        else
            echo "code is $status_code"
            if [ "$status_code" == "200" ]; then
                break
            fi
        fi
        sleep 1
        ((exptime++))

        echo -e "\rWait app to pass health check: $exptime..."

        if [ $exptime -gt ${APP_START_TIMEOUT} ]; then
            echo 'app start failed'
            exit 1
        fi
    done
    echo "check ${HEALTH_CHECK_URL} success"
}
start_application() {
    echo "starting java process"
    nohup java -jar ${JAR_NAME} >${JAVA_OUT} 2>&1 &
    echo "started java process"
}

stop_application() {
    checkjavapid=$(ps -ef | grep java | grep ${APP_NAME} | grep -v grep | grep -v 'deploy.sh' | awk '{print$2}')

    if [[ ! $checkjavapid ]]; then
        echo -e "\rno java process"
        return
    fi

    echo "stop java process"
    times=60
    for e in $(seq 60); do
        sleep 1
        COSTTIME=$(($times - $e))
        checkjavapid=$(ps -ef | grep java | grep ${APP_NAME} | grep -v grep | grep -v 'deploy.sh' | awk '{print$2}')
        if [[ $checkjavapid ]]; then
            kill -9 $checkjavapid
            echo -e "\r        -- stopping java lasts $(expr $COSTTIME) seconds."
        else
            echo -e "\rjava process has exited"
            break
        fi
    done
    echo ""
}
start() {
    start_application
    health_check
}
stop() {
    stop_application
}
case "$ACTION" in
start)
    start
    ;;
stop)
    stop
    ;;
restart)
    stop
    start
    ;;
*)
    usage
    ;;
esac
```

### 6.4. 搭建自动部署流水线

部署配置: <https://help.aliyun.com/document_detail/153848.htm#section-ol3-f7c-7ho>

Java 构建上传 > Java 构建命令

```bash
# 因为我的项目放在仓库的子目录所以需要先进入子目录
cd blog
mvn -B clean package -Dmaven.test.skip=true -Dautoconfig.skip
```

Java 构建上传 > 构建物上传 > 打包路径

```txt
blog/target/blog-zeo.jar
blog/deploy.sh
```

主机部署 > 部署脚本

```bash
rm -rf /home/admin/blog-zeo/target
rm -rf /home/admin/blog-zeo/deploy.sh
mkdir -p /home/admin/blog-zeo
tar zxvf /home/admin/app/package_blog-zeo.tgz -C /home/admin/blog-zeo/
mv /home/admin/blog-zeo/blog/* /home/admin/blog-zeo
sh /home/admin/blog-zeo/deploy.sh restart
```

其他参考：Web应用构建配置: <https://help.aliyun.com/document_detail/59293.html>（我在仓库的根目录尝试配置了 release 文件，但似乎没有生效）

### 6.5. 验证部署

运行流水线，如无误则，部署成功（deploy.sh 会自动进行检测）

### 6.6. 添加钉钉机器人通知

## 7. ECS 域名配置

> 此处域名配置为临时配置，便于后续验证，验证无误后域名将指向 DCDN

1. 我之前已经配置了一个指向 ECS 的域名 `cc01cc.cn`
2. 在此基础上，我再配置一个 `v01.static.cc01cc.cn` 子域名，当前专门用于图片的访问
3. 前往域名解析 <https://dns.console.aliyun.com/>
4. 给子域名添加 `A` `AAAA` 记录
5. 前往数字证书管理服务管理控制台<https://yundun.console.aliyun.com/>
6. 添加免费证书，并点击部署
7. 填写并记录证书存储路径等参数

不推荐使用 Let's Encrypt 证书，尤其是在开启 CDN 等配置的情况下 certbot 更新相对麻烦。

![https-20230628210913](https://v01.static.cc01cc.cn/https-20230628210913.png)

## 8. 配置 NGINX

我使用工具生成 NGINX 配置：NGINXConfig | DigitalOcean: <https://www.digitalocean.com/community/tools/nginx?global.app.lang=zhCN>

开源地址：digitalocean/nginxconfig.io: ⚙️ NGINX config generator on steroids 💉: <https://github.com/digitalocean/nginxconfig.io>

1. 进入 ECS 控制台复制已有的 NGINX 配置
2. 参考已有配置，在 NGINX 配置中调整或添加新的配置

### 8.1. no "ssl_certificate" 问题

中间遇到了个小坑，启动 nginx 服务的时候报错

```txt
nginx: [emerg] no "ssl_certificate" is defined for the "listen ... ssl" directive in /etc/nginx/sites-enabled/cc01cc.cn.conf:1
```

不要运行注释 SSL 相关指令即可，如果已经运行了可以

#### 8.1.1. 【方法一】

```bash
# 批量取消注释
sed -i -r -z 's/#?; ?#//g; s/(server \{)\n    ssl off;/\1/g' /etc/nginx/sites-available/***.conf
```

#### 8.1.2. 【方法二】手动取消注释

把 `/etc/nginx/sites-enabled/***.conf`，

```conf
#;#ssl_certificate /etc/letsencrypt/live/***/fullchain.pem;
```

以及其他类似注释手动取消

```conf
ssl_certificate /etc/letsencrypt/live/***/fullchain.pem;
```

### 8.2. 检查 nginx 配置

配置完成后，访问指定域名，查看是否返回目标页面，同时检查 HTTPS 是否正常

#### 8.2.1. nginx 配置排查

检查 nginx log, spring log

关于权限问题，可以使用以下命令，查看运行 nginx 的用户

```bash
ps aux | grep nginx
```

## 9. 添加 DCDN

全站加速 - aliyun 文档: <https://help.aliyun.com/product/64812.html>

### 9.1. 添加 WAF 边缘防护

边缘WAF概述（新版） - aliyun 文档: <https://help.aliyun.com/document_detail/404760.html>

## 10. 搭建 cn 站自动部署流水线

```bash
cnpm install
# cnpm run build
cnpm install -g hexo-cli

hexo clean

hexo deploy
```

### 10.1. 添加钉钉机器人通知

## 11. 添加云监控

云监控 - aliyun 文档: <https://help.aliyun.com/product/28572.html>

对 CDN, ECS, OSS 进行监控，包括可访问性，流量，带宽，请求次数等

### 11.1. 自动拨测

使用自动拨测工具，检测网站可访问性，以及信息完整性

## 12. 可以优化的地方

1. OSS 默认域名，强制下载现在使用的是自定义域名解决，之后将尝试修改 `Content-Type` 或 `Content-Disposition` 的方式
2. 暂时没有使用 DCDN，因为图片和其他资源使用了不同的域名，需要重新进行设计。

## 13. 图库 v2 测试

![Yeah](https://v01.static.cc01cc.cn/FmKsvhSakAEIzEg.jpg?x-oss-process=image/resize,w_100/quality,q_40)

## 14. 记录

总计部署了 31 次

![20230406004055](https://v01.static.cc01cc.cn/20230406004055.png)

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->