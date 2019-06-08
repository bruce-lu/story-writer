---
title: Spring-Cloud-每天10分钟-Eureka-server
tags: spring cloud,eureka,service registry
author: Bruce Lu
---

# Spring Cloud 每天10分钟 - Eureka server

## 文章历史记录

- 2019.6.7 创建

## 作者

- Bruce Lu

## 目标
10分钟内开发运行测试基本的Spring Cloud Eureka server

## 背景
- Eureka

	是Netflix开源给社区的一个服务发现（Service Discovery）组件。

- 餐馆点餐场景的例子

	菜单列出了餐馆的服务清单。 顾客按照菜单上的名字下单给服务生， 服务生会下单给厨师， 等厨师做好了顾客就可以享受美味佳肴了。 
Eureka就好比上面场景里面的菜单， 顾客是服务消费者， 服务生和厨师是服务提供者。

- 为什么需要服务发现

	在一个分布式系统里面当一个服务消费者（Service Consumer）调用另外一个或几个服务的时候需要知道服务提供者（Service Provider）的地址（比如IP和端口号）。  这个世界上唯一不变的就是变化本身，  花了几周时间写好的几十个微服务互相直接IP端口号调用，突然有一天需要迁移到新环境， IP都变了...  这种变化怎么说呢，先是脑海里各种神马疾驰而过尘土飞扬， 然后加班到太阳照常升起。
	
	按照Spring Cloud官网的说法，Netflix 的Eureka， 那是上过战场动过真刀真枪的角色， 绝非美颜谄媚ppt吹牛拍马屁之流可比的（后半句我加的）。 它的出现就是不让上面的各种神马出现。 本质上就是把服务的IP地址和端口用服务名（service name）屏蔽掉， 好比DNS里的域名任你IP三千，而我只有一个。 对服务调用者， 只需要知道服务名就可以调用了， 不用关心IP和端口。


- 世间本该如此美好。


## 开发工具和运行环境

- Spring Cloud Greenwich
- Spring Boot 2.1.5
- Java 1.8.0
- STS (Spring Tool Suite) 4.1.1
- MackBook Pro Mojave


## 打开 STS， 新建项目

- File -> New -> Spring Starter Project

Name: eureka-server

![新建项目 ](https://www.github.com/bruce-lu/story-writer/raw/master/story-img/1559922921380.png)

![选择Eureka Server依赖](https://www.github.com/bruce-lu/story-writer/raw/master/story-img/1559923021373.png)

Next, Finish

![等待下载依赖包](https://www.github.com/bruce-lu/story-writer/raw/master/story-img/1559923174660.png)


## EurekaServerApplication.java
- 添加 @EnableEurekaServer 用来开启Spring Cloud的服务注册和发现功能
- 完整代码如下

``` java
package com.blue.sc.eureka;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(EurekaServerApplication.class, args);
	}

}

```

## application.yml
- application.properties 改名为application.yml
- 完整代码如下
``` yaml
server:
  port: 8761

spring:
  application:
    name: eureka-server
    
eureka:
  instance:
    hostname: localhost
    
  client:
    fetch-registry: false
    register-with-eureka: false
    service-url:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka
```

## 验证
- 运行应用
右键 EurekaServerApplication -> Run As -> Spring Boot App

- 打开浏览器输入： http://localhost:8761/ 可以看到
![Eureka server Web 页面](https://www.github.com/bruce-lu/story-writer/raw/master/story-img/1559925981713.png)

这说明Eureka server应用成功启动。

## 源码

https://github.com/bruce-lu/spring-cloud-10-mins-a-day/tree/v0.1/eureka-server

