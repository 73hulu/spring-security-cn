重定向URI是应用程序中的路径，最终用户的用户代理在使用Google进行身份验证并在“同意”页面上授予了对OAuth客户端（在上一步中创建）的访问权限后重定向回的路径。

在“设置重定向URI”子部分中，确保将“授权重定向URI”字段设置为[http://localhost:8080/login/oauth2/code/google](http://localhost:8080/login/oauth2/code/google)

> 默认重定向URI模板是{baseUrl}/login/oauth2/code/{registrationId}。registrationId是ClientRegistration的唯一标识符。



