下一步是向war注册`springSecurityFilterChain`。这可以在Java Configuration中完成，在Servlet 3.0+环境中使用Spring的WebApplicationInitializer支持[Spring’s WebApplicationInitializer support](https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/mvc.html#mvc-container-config)。不出所料，Spring Security提供了一个基类AbstractSecurityWebApplicationInitializer，它将确保为您注册springSecurityFilterChain。我们使用AbstractSecurityWebApplicationInitializer的方式不同，这取决于我们是否已经在使用Spring，或者Spring Security是否是应用程序中惟一的Spring组件。

* [Section 6.1.2, “AbstractSecurityWebApplicationInitializer without Existing Spring”](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#abstractsecuritywebapplicationinitializer-without-existing-spring)-如果您尚未使用Spring，请使用这些说明

* [Section 6.1.3, “AbstractSecurityWebApplicationInitializer with Spring MVC”](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#abstractsecuritywebapplicationinitializer-with-spring-mvc)-如果您已经在使用Spring，请使用这些说明



