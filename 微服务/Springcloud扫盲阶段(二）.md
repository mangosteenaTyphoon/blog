> 接着一之后这篇文章将从fegin开始记录，帮助自己一点点的扫盲springcloud.

## Feign远程调用

先来看我们以前利用RestTemplate发起远程调用的代码：

```java
String url ="http://userservice/user/"+order.getUserId();
User user=restTemplate.getForObject(url,User.class);
```

可以明显看出这样写的问题：

* 代码的可读性，编程体验不统一。
* 参数复杂URL难以维护。

> Feign是一个声明式的http客户端，客户地址：<https://github.com/OpenFeign/feign>  其作用就是帮助我们优雅的实现http请求的发送，解决上面遇到的问题。

![image-20221229165445786](https://shanzhu-edu.oss-cn-shanghai.aliyuncs.com/blog/202212291654993.png)

###  Feign代替ResTemplate

Feign的使用步骤如下：

####  引入依赖

我们在order-service服务的pom文件中引入feign的依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>

```

####  添加注解

在order-service的启动类添加注解开启Feign的功能：

![image-20221229170315470](https://shanzhu-edu.oss-cn-shanghai.aliyuncs.com/blog/202212291703561.png)

####  编写Feign客户端

在order-service中新建一个接口，内容如下：

```java
package cn.itcast.order.client;

import cn.itcast.order.pojo.User;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

@FeignClient("userservice")
public interface UserClient {
    @GetMapping("/user/{id}")
    User findById(@PathVariable("id") Long id);
}

```

这个客户端主要是基于SpringMVC的注解来声明远程调用的信息，比如：

* 服务名称：userservice
* 请求方式：Get
* 请求路径：/user/{id}
* 请求参数：Long id
* 返回值类型：User

这样，Feign就可以帮助我们发送http请求，无需自己使用RestTemplate来发送了。

####  测试

修改order-service中的OrderService类中的queryOrderById方法，使用Feign客户端代替RestTemplate

~~~java
    @Autowired
    private UserClient userClient;

    public Order queryOrderById(Long orderId) {
        // 1.查询订单
        Order order = orderMapper.findById(orderId);
        // 2.用Feign远程调用
        User user = userClient.findById(order.getUserId());
        // 3.封装user到Order
        order.setUser(user);
        // 4.返回
        return order;
    }
~~~

这样的话就优雅很多了。

#### 总结

使用Feign的步骤：

* 引入依赖
* 添加@EnableFeignClients注解
* 编写FeignClient接口
* 使用FeignClient中定义的方法代替RestTemplate

### 自定义配置

| **类型**            | **作用**         | **说明**                                               |
| ------------------- | ---------------- | ------------------------------------------------------ |
| feign.Logger.Level  | 修改日志级别     | 包含四种不同的级别：NONE、BASIC、HEADERS、FULL         |
| feign.codec.Decoder | 响应结果的解析器 | http远程调用的结果做解析，例如解析json字符串为java对象 |
| feign.codec.Encoder | 请求参数编码     | 将请求参数编码，便于通过http请求发送                   |
| feign. Contract     | 支持的注解格式   | 默认是SpringMVC的注解                                  |
| feign. Retryer      | 失败重试机制     | 请求失败的重试机制，默认是没有，不过会使用Ribbon的重试 |

一般情况下，默认值就能满足我们使用，如果要自定义时，只需要创建自定义的@Bean覆盖默认Bean即可。

下面以日志为例来演示如何自定义配置。

####  配置文件方式

基于配置文件修改feign的日志级别可以针对单个服务：

~~~ yaml
feign:  
  client:
    config: 
      userservice: # 针对某个微服务的配置
        loggerLevel: FULL #  日志级别 

~~~

也可以针对所有服务：

~~~yaml
feign:  
  client:
    config: 
      default: # 这里用default就是全局配置，如果是写服务名称，则是针对某个微服务的配置
        loggerLevel: FULL #  日志级别 

~~~

而日志的级别分为四种：

- NONE：不记录任何日志信息，这是默认值。
- BASIC：仅记录请求的方法，URL以及响应状态码和执行时间
- HEADERS：在BASIC的基础上，额外记录了请求和响应的头信息
- FULL：记录所有请求和响应的明细，包括头信息、请求体、元数据。