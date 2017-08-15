# springboot

### Spring、Spring MVC和Spring Boot的区别

Spring 是一个“引擎” 
Spring MVC 是基于 Spring 的一个 MVC 框架 
Spring Boot 是基于 Spring4 的条件注册的一套快速开发整合包 

Spring 最初利用“工厂模式”（ DI ）和“代理模式”（ AOP ）解耦应用组件。大家觉得挺好用，于是按照这种模式搞了一个 MVC 框架（一些用 Spring 解耦的组件），用开发 web 应用（ SpringMVC ）。然后有发现每次开发都要搞很多依赖，写很多样板代码很麻烦，于是搞了一些懒人整合包（ starter ），这套就是 Spring Boot 。 

数十年来， Spring 的努力就是为了减少复杂度，解耦，少些一些代码。虽然掌握 Spring 可以减少很多多余的工作，但是掌握 Spring 本身也变成很复杂的一件事。 Spring 的 XML，注解配置，EL 表达式这种 DSL ，把很多很简单的事情搞复杂了，当 Spring Boot 自动配置失灵时就带来了更多的麻烦。
