# 参数说明

> 作者 张磊
iplatform-boot 0.0.7+

## Java参数

```sh
# 启动HTTPS（默认是true）
-Dssl=false
# JVM 内存参数
JAVA_OPTIONS=-Xmx1g -Xms1g -XX:OnOutOfMemoryError="kill -9 %p"
```

## 命令参数

### 最小启动参数

```sh
# 注册服务地址（必填）
discovery.server.address=https://127.0.0.1:8761/eureka/

# 实例ID（非必填）,默认生成一个唯一ID，格式为ip:服务名:port
server.instanceId='xxx'

# 服务IP（必填）
server.host=127.0.0.1
```

## 第二端口(非SSL)

当想保留原有https的端口，又想对外提供一个非ssl端口访问时配置

```sh
# 第二端口开关,默认false
server.second.enabled=false
# 第二端口号
server.second.port=xxx
```

## 集中配置参数

当使用集中配置时的参数

```sh
# 集中配置开关,默认flase
spring.cloud.config.enabled=false
# 服务环境（开启集中配置后必填）
spring.cloud.config.profile='XX业务系统'
```

## 服务隔离

当希望在一个注册中心的服务需要进行分组隔离时使用

```sh
# 服务所属租户，当需要做到服务隔离的时候使用（非必填）
eureka.instance.metadataMap.tenant=beijing
```

## Flume参数

如果要使用框架内置的flume时使用

```sh
# flume框架开关,默认false
flume.enabled=false
```

## JDBC数据源

```sh
# 数据源类型
spring.datasource.platform=mysql
# 数据源驱动
spring.datasource.dataSourceClassName=com.mysql.jdbc.Driver
# JDBC URL
spring.datasource.url='jdbc:mysql://127.0.0.1:3306/gulfdataflowdb?useUnicode=true&characterEncoding=utf-8&autoReconnect=true'
# 数据库用户名
spring.datasource.username=root
# 数据库密码
spring.datasource.password=root
# 启动时是否执行初始化脚本
spring.datasource.initialize=true
# 开启定期检查空闲连接
spring.datasource.test-while-idle=true
# 每5分钟检查一次空闲连接
spring.datasource.time-between-eviction-runs-millis=300000
# 空闲链接30秒后被清除
spring.datasource.min-evictable-idle-time-millis=30000
spring.datasource.validation-query="SELECT 1"
# 最大并发连接数
spring.datasource.max-active=100
# 最大空闲连接数
spring.datasource.max-idle=5
# 最小空闲连接数                
spring.datasource.min-idle=2
# sql最大等待30秒返回
spring.datasource.max-wait=30000
```

## Redis

### Redis哨兵模式

```sh
spring.redis.database=0
spring.redis.port=6379
spring.redis.password=xxx
spring.redis.sentinel.master=mymaster
spring.redis.sentinel.nodes=10.22.1.205:26379,10.22.1.204:26379
```

### Redis单例模式

```sh
spring.redis.database=0
spring.redis.password=xxx
spring.redis.host=127.0.0.1
spring.redis.port=6379
```

### Redis集群模式

```sh
spring.redis.password=xxx
spring.redis.cluster.enabled=true
spring.redis.cluster.nodes=172.18.254.109:8000,172.18.254.109:8001,172.18.254.109:8002
spring.redis.cluster.timeout=30
spring.redis.cluster.max-redirects=12
```

## MongoDB

```sh
spring.data.mongodb2.uri=mongodb://{username}:{password}@127.0.0.1/datashare
```

## Tomcat

```sh
server.tomcat.max-threads=2000
server.tomcat.max-http-header-size=65536
```

## Cache

```sh
spring.cache.type=guava
```

## 分布式锁

```sh
# 是否开启分布式锁，默认不开启
iplatform.scheduled.lock.enabled=false
# 分布式锁实现类型 jdbc,redis,mongo,zookeeper
iplatform.scheduled.lock.type=jdbc
```

## 安全

### XSS

```sh
iplatform.xss.enabled=true
iplatform.xss.words[0]="alert\\s*\\("
iplatform.xss.words[1]="eval\\s*\\("
iplatform.xss.words[2]="javascript:"
iplatform.xss.words[3]="<script>"
iplatform.xss.regex=
iplatform.xss.policy=break
```

### CSRF

```sh
# header attack 防篡改开关,默认false
iplatform.tamperproofing.headerhost.enabled=false
# header host 白名单
iplatform.tamperproofing.headerhost.whitelist=www.bomc.com:8761,www.bomc.org:8761
```

### HTTP方法

```sh
# 设置tomcat允许的方法列表
server.tomcat.port-header=HEAD,PUT,DELETE,OPTIONS,TRACE,COPY,SEARCH,PROPFIND  
```

### SSL

```sh
server.ssl.ciphers=TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384,TLS_ECDHE_RSA_WITH_AES_128_SHA256,TLS_ECDHE_ECDSA_WITH_AES_128_SHA256,TLS_ECDHE_RSA_WITH_AES_128_SHA,TLS_ECDHE_ECDSA_WITH_AES_128_SHA,TLS_ECDHE_RSA_WITH_AES_256_SHA384,TLS_ECDHE_ECDSA_WITH_AES_256_SHA384,TLS_ECDHE_RSA_WITH_AES_256_SHA,TLS_ECDHE_ECDSA_WITH_AES_256_SHA
server.ssl.protocol=TLS
server.ssl.enabled-protocols=TLSv1.2
```

## Ribbon

```sh
# Fegin自动重试次数
ribbon.MaxAutoRetries=3
```

## 消息开关

```sh
# 发生Http调用异常时通过消息总线发送异常事件
iplatform.messagebus.exception.httpclient = true
```

## 熔断

```sh
# 默认20，滚动时间窗口内，失败请求数超过此数则断路器开启
hystrix.command.default.circuitBreaker.requestVolumeThreshold=20
# 断路器开启后，超过此时间后才自动会关闭
hystrix.command.default.circuitBreaker.sleepWindowInMilliseconds=5000
# 设置失败百分比，失败率超过这个值，则断路器进入fallback
hystrix.command.default.circuitBreaker.errorThresholdPercentage=50
# 设置滚动时间窗口, 默认10000毫秒
hystrix.command.default.metrics.rollingStats.timeInMilliseconds=10000

```

## 隔离模式

```sh
# 隔离策略，SEMAPHORE=信号量，THREAD=线程池，默认SEMAPHORE
hystrix.command.default.execution.isolation.strategy=SEMAPHORE
# 允许请求的最大并发数，超过次数量后续请求将被拒绝
hystrix.command.default.execution.isolation.semaphore.maxConcurrentRequests=5000
# 设置调用者等待命令执行的超时限制，超过此时间则超时返回，默认180000毫秒
hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds=180000
# 回退最大并发请求量，超过此值将调用fallback,如果没有fallback则抛出异常
hystrix.command.default.fallback.isolation.semaphore.maxConcurrentRequests=5000
```

## 注册中心

```sh
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
eureka.client.serviceUrl.defaultZone
# 服务续约间隔时间
eureka.instance.lease-renewal-interval-in-seconds=5
# 服务续约到期时间 
eureka.instance.lease-expiration-duration-in-seconds=10
# 关闭自我保护模式
eureka.server.enable-self-preservation=false
# 扫描失效节点间隔
eureka.server.eviction-interval-timer-in-ms=5000
# 设置每5秒刷新注册服务的缓存   
eureka.server.response-cache-update-interval-ms=5000
```

## 跟踪服务

```sh
# 服务跟踪总开关，默认关闭
spring.sleuth.enabled=false

# jdbc服务跟踪开关，默认开启
spring.sleuth.mybatis.enabled=true

# 跟踪服务采样率
eureka.instance.metadataMap.trackSampling=0.1
# 跟踪消息发送方式，messagebus：消息总线，http：跟踪服务restfulapi（默认）
spring.zipkin.type=messagebus 
```

## 流控

```sh
# 服务流控权重
eureka.instance.metadataMap.weight=1
```

## 路由标签

```sh
# 或标签
eureka.instance.metadataMap.labelOr=beijing,shanghai

# 与标签
eureka.instance.metadataMap.labelAnd=beijing,shanghai
```

## 集中日志

```sh
# 集中日志开关,默认false
logger.kafka.enabled=false
# 集中日志分区数,默认20
logger.kafka.partitions=20
# 集中日志副本数,默认1
logger.kafka.replication=1
# 集中日志kafka地址
logger.kafka.bootstrapServers=localhost:9092
# 集中日志zk地址
logger.kafka.zookeeper=localhost:2181
```

## 控制命令

```sh
# 允许远程访问的ip白名单
endpoints.shutdown.allowip=192.168.1.100,192.168.1.101
```