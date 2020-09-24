```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
            .antMatchers("/design", "/orders")
                .hasRole("ROLE_USER")
            .antMatchers(“/”, "/**").permitAll();
}
```

authorizeRequests() 的调用返回一个对象（ExpressionInterceptUrlRegistry），可以在该对象上指定 URL 路径和模式以及这些路径的安全需求。在这种情况下，指定两个安全规则：

- 对于 /design 和 /orders 的请求应该是授予 ROLE_USER 权限的用户的请求。
- 所有的请求都应该被允许给所有的用户。

这些规则的顺序很重要。首先声明的安全规则优先于较低级别声明的安全规则。如果交换这两个安全规则的顺序，所有请求都将应用 permitAll()，那么关于 /design 和 /orders 请求的规则将不起作用。

| 方法                       | 做了什么                                         |
| -------------------------- | ------------------------------------------------ |
| anonymous()                | 默认用户允许访问                                 |
| authenticated()            | 认证用户允许访问                                 |
| access(String)             | 如果 SpEL 表达式的值为 true，则允许访问          |
| denyAll()                  | 无条件拒绝所有访问                               |
| fullyAuthenticated()       | 如果用户是完全授权的（不是记住用户），则允许访问 |
| hasAnyAuthority(String...) | 如果用户有任意给定的权限，则允许访问             |
| hasAnyRole(String...)      | 如果用户有任意给定的角色，则允许访问             |
| hasAuthority(String)       | 如果用户有给定的权限，则允许访问                 |
| hasIpAddress(String)       | 来自给定 IP 地址的请求允许访问                   |
| hasRole(String)            | 如果用户有给定的角色，则允许访问                 |
| not()                      | 拒绝任何其他访问方法                             |
| permitAll()                | 无条件允许访问                                   |
| rememberMe()               | 允许认证了的同时标记了记住我的用户访问           |



