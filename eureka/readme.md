> 作者：gitveio
> 链接：https://www.jianshu.com/p/2e6e53635f8a
> 来源：简书

# 说明

基于spring cloud体系架构，eureka作为注册中心负责服务注册和服务发现，使用中发现服务运行启动后需要一段时间才能被正常调用，这里记录一下里面配置细节。

# 整体逻辑

eureka使用了缓存和异步数据处理技术，来提高性能和可用性。

> 比如有服务：A服务，B服务，C服务(eureka server)，依赖关系是A->B，都依赖C的服务发现，完整处理逻辑可能是：

> 1 A定时从C拉取最新的服务列表 -> serverlist

> 2 A服务收到请求后，在调用B服务前由loadbalance选择一个B服务的实例进行请求，该loadbalance有维护服务列表的缓存

> 3 B服务在启动完成后调用接口将自己注册到eureka server上面去

> 4 eureka server在收到拉取最新服务列表的请求时，从缓存中获取服务列表信息返回给调用方

> spring cloud对于第3步来说是立即注册的没有延迟，其他每一步都可能会有延迟，也有对应的配置可以做微调

# 配置

```xml
eureka server:
// 清除失效服务间隔时间
eureka.server.EvictionIntervalTimerInMs=3000
// 响应数据缓存有效期
eureka.server.responseCacheUpdateIntervalMs=3000
eureka client:
// 拉取服务列表间隔时间
eureka.client.registryFetchIntervalSeconds=5
// 负载均衡器服务列表缓存
ribbon.ServerListRefreshInterval=5000
// 指定时间内没有数据上报可能会被清理掉
eureka.instance.LeaseExpirationDurationInSeconds=15
// 服务状态上报间隔
eureka.instance.LeaseRenewalIntervalInSeconds=5
```
