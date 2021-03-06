# Spring Boot

### Spring、Spring MVC和Spring Boot的区别

Spring 是一个“引擎” 
Spring MVC 是基于 Spring 的一个 MVC 框架 
Spring Boot 是基于 Spring4 的条件注册的一套快速开发整合包 

Spring 最初利用“工厂模式”（ DI ）和“代理模式”（ AOP ）解耦应用组件。大家觉得挺好用，于是按照这种模式搞了一个 MVC 框架（一些用 Spring 解耦的组件），用开发 web 应用（ SpringMVC ）。然后有发现每次开发都要搞很多依赖，写很多样板代码很麻烦，于是搞了一些懒人整合包（ starter ），这套就是 Spring Boot 。 

数十年来， Spring 的努力就是为了减少复杂度，解耦，少些一些代码。虽然掌握 Spring 可以减少很多多余的工作，但是掌握 Spring 本身也变成很复杂的一件事。 Spring 的 XML，注解配置，EL 表达式这种 DSL ，把很多很简单的事情搞复杂了，当 Spring Boot 自动配置失灵时就带来了更多的麻烦。

### 微服务的拆分粒度

【粗粒度：一个服务层】

最粗犷的玩法，所有基础数据的访问，都通过一个service访问，在业务不是特别复杂的时候还好，一旦业务变复杂了，这个service层会变得非常重，成为耦合点之一，
，假设有一个通用的服务层来访问基础数据，这个服务层可能是这样的：有一个统一的service层，用户信息，好友信息，群组信息，消息信息都通过这个service层来走。


【一个子业务一个service】

如果所有的信息存储都在一个service里，那么一个地方出bug，就将影响整个业务，所以更合理的做法是在服务层进行垂直拆分，将子业务一个个拆出来
用户相关的子业务有user-service
好友相关的子业务有friend-service
群组相关的子业务有group-service
息相关的子业务有msg-service

这样的话，一个service出问题也不会影响其他service，同时数据层也按照业务垂直拆分开了。


【一个数据库对应一个】
数据访问service最初是从DAOORM的数据访问需求过来的，所以有些公司也有一个数据表一个service的玩法。
服务层，整个群业务是一个service
存储层，实际可能对应了群信息、群成员、群消息等多个数据表

群信息表，群成员表，群消息表等各个数据表之间也解耦开了，不会相互影响了。

【一个接口对应一个】
多个服务操纵同一个数据表，使用同一片缓存，每个接口出问题，都不会影响其他接口。

### Swagger Tools

https://github.com/swagger-api/swagger-codegen

### Spring Boot with Mybatis

git clone git@github.com:JeffLi1993/springboot-learning-example.git
