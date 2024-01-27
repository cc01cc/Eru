---
title: 获取并生成 Aliyun STS 签名 URL 访问 OSS
copyright: BY-NC-ND
date: 2023-04-02 19:30:59
tags:
    - blog-build
categories:
    - blog-build
---

> 此文章是在搭建 cn 站 v2 的过程中的一个小弯路
>
> 如果使用服务器连接 OSS，不需要 STS 授权，直接 IP 授权即可。
>
> 此方法适用于给用户临时授权，

## 使用 Spring Boot 搭建授权服务

为了方便后续拆分，以及调整，此处将 博客页面和图片 的授权分别放置于不同的模块中。

### 关于授权的相关概念

- 什么是STS: <https://help.aliyun.com/document_detail/28756.html>
- 基本概念: <https://help.aliyun.com/document_detail/28628.html>
- OSS访问域名使用规则: <https://help.aliyun.com/document_detail/31834.htm>
- 在URL中包含签名: <https://help.aliyun.com/document_detail/100670.htm>

### 获取临时访问安全令牌 STS

1. 前往 RAM 访问控制 - 用户: <https://ram.console.aliyun.com/users>
2. 创建用户 `ZEO-OSS-USER` 授权 STS 服务，OSS 管理权限
3. 创建用户后，分别进入用户详情页，创建 AccessKey，**记录 ID 和 key**
4. 前往 RAM 访问控制 - 角色：<https://ram.console.aliyun.com/roles>
5. 创建角色 `ZEO-OSS-Role`  授权 STS 服务
6. 进入角色详情页，记录**角色名称**和**ARN**
7. 前往 AssumeRole_安全令牌_API调试-阿里云OpenAPI开发者门户: <https://next.api.aliyun.com/api/Sts/2015-04-01/AssumeRole>
8. 填入必要参数，并复制生成的代码以及SDK依赖
9. 改编获取到的代码示例，我这儿将它改编成了一个工具类

```java
package com.cc01cc.blog.Utils;

import com.aliyun.sts20150401.models.AssumeRoleResponse;
import com.aliyun.tea.TeaException;

/**
 * @author cc01cc
 * 
 * 代码改编自 阿里云 OpenAI <https://next.api.aliyun.com/api/Sts/2015-04-01/AssumeRole>
 */
public class AliyunStsUtils {
    /**
     * 使用AK&SK初始化账号Client
     * 
     * @param accessKeyId
     * @param accessKeySecret
     * @return Client
     * @throws Exception
     */
    public static com.aliyun.sts20150401.Client createClient(String accessKeyId, String accessKeySecret)
            throws Exception {
        com.aliyun.teaopenapi.models.Config config = new com.aliyun.teaopenapi.models.Config()
                // 必填，您的 AccessKey ID
                .setAccessKeyId(accessKeyId)
                // 必填，您的 AccessKey Secret
                .setAccessKeySecret(accessKeySecret);
        // 访问的域名
        config.endpoint = "sts.cn-hangzhou.aliyuncs.com";
        return new com.aliyun.sts20150401.Client(config);
    }

    public static AssumeRoleResponse getSts(String accessKeyId, String accessKeySecret, String roleSessionName,
            String roleArn, Long durationSeconds) throws Exception {
        // 工程代码泄露可能会导致AccessKey泄露，并威胁账号下所有资源的安全性。以下代码示例仅供参考，建议使用更安全的 STS
        // 方式，更多鉴权访问方式请参见：https://help.aliyun.com/document_detail/378657.html
        com.aliyun.sts20150401.Client client = createClient(accessKeyId, accessKeySecret);
        com.aliyun.sts20150401.models.AssumeRoleRequest assumeRoleRequest = new com.aliyun.sts20150401.models.AssumeRoleRequest()
                .setRoleSessionName(roleSessionName)
                .setRoleArn(roleArn)
                .setDurationSeconds(durationSeconds);
        com.aliyun.teautil.models.RuntimeOptions runtime = new com.aliyun.teautil.models.RuntimeOptions();
        try {
            // 复制代码运行请自行打印 API 的返回值
            return client.assumeRoleWithOptions(assumeRoleRequest, runtime);
        } catch (TeaException error) {
            // 如有需要，请打印 error
            com.aliyun.teautil.Common.assertAsString(error.message);
        } catch (Exception _error) {
            TeaException error = new TeaException(_error.getMessage(), _error);
            // 如有需要，请打印 error
            com.aliyun.teautil.Common.assertAsString(error.message);
        }
        return null;
    }
}
```

> 参考 Credentials 设置: <https://help.aliyun.com/document_detail/378657.html>

### 使用 STS 生成 签名 URL

Java授权访问: <https://help.aliyun.com/document_detail/32016.htm#p-f2i-r4x-6lz>

```java
/**
 * 代码改编自 Java授权访问:
 * https://help.aliyun.com/document_detail/32016.htm#p-f2i-r4x-6lz
 * 
 * @param endpoint
 * @param accessKeyId     STS 所返回的 accessKeyId，不是 ram 的 accessKeyId 下同
 * @param accessKeySecret
 * @param securityToken
 * @param bucketName
 * @param objectName
 * @param durationSeconds
 * @return
 */
public static URL getPresignedUrl(String endpoint, String accessKeyId, String accessKeySecret, String securityToken,
        String bucketName, String objectName, Long durationSeconds) {
    // 从STS服务获取临时访问凭证后，您可以通过临时访问密钥和安全令牌生成OSSClient。
    // 创建OSSClient实例。
    OSS ossClient = new OSSClientBuilder().build(endpoint, accessKeyId, accessKeySecret, securityToken);

    try {
        // 设置签名URL过期时间，单位为毫秒。
        Date expiration = new Date(new Date().getTime() + durationSeconds * 1000);
        // 生成以GET方法访问的签名URL，访客可以直接通过浏览器访问相关内容。
        URL url = ossClient.generatePresignedUrl(bucketName, objectName, expiration);
        System.out.println(url);
        return url;
    } catch (OSSException oe) {
        System.out.println("Caught an OSSException, which means your request made it to OSS, "
                + "but was rejected with an error response for some reason.");
        System.out.println("Error Message:" + oe.getErrorMessage());
        System.out.println("Error Code:" + oe.getErrorCode());
        System.out.println("Request ID:" + oe.getRequestId());
        System.out.println("Host ID:" + oe.getHostId());
    } catch (ClientException ce) {
        System.out.println("Caught an ClientException, which means the client encountered "
                + "a serious internal problem while trying to communicate with OSS, "
                + "such as not being able to access the network.");
        System.out.println("Error Message:" + ce.getMessage());
    } finally {
        if (ossClient != null) {
            ossClient.shutdown();
        }
    }
    return null;
}
```

### 将以上的方法合并获取签名 url

```java
/**
 * 直接通过 ram 获取 签名 url
 * 
 * @param accessKeyId
 * @param accessKeySecret
 * @param roleSessionName
 * @param roleArn
 * @param durationSeconds
 * @param endpoint
 * @param bucketName
 * @param objectName
 * @return
 */
public static URL getPresignedUrl(String accessKeyId, String accessKeySecret, String roleSessionName,
        String roleArn, Long durationSeconds, String endpoint, String bucketName, String objectName) {
    AssumeRoleResponse sts;
    try {
        sts = getSts(accessKeyId, accessKeySecret, roleSessionName,
                roleArn, durationSeconds);
        AssumeRoleResponseBodyCredentials credentials = sts.getBody().getCredentials();
        return getPresignedUrl(endpoint, credentials.accessKeyId, credentials.accessKeySecret,
                credentials.securityToken, bucketName, objectName, durationSeconds);
    } catch (Exception e) {
        e.printStackTrace();
    }
    return null;
}
```

<!--
Copyright © 2023-2024 [cc01cc](https://github.com/cc01cc)

本页面采用 [知识共享署名-非商业性使用 4.0 国际许可协议](http://creativecommons.org/licenses/by-nc/4.0/) 进行许可。

转载请注明原始地址：<https://cc01cc.com/>
-->