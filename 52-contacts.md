Contacts Sample是一个高级示例，它说明了除基本应用程序安全性之外的域对象访问控制列表（ACL）的更强大功能。该应用程序提供了一个界面，用户可以使用该界面管理简单的联系人数据库（域对象）。

要部署，只需将WAR文件从Spring Security发行版复制到容器的webapps目录中。该WAR应该被称为spring-security-samples-contacts-3.1.x.war（附加的版本号将根据您使用的版本而有所不同）。

启动容器后，检查应用程序是否可以加载。访问http://localhost:8080/contacts\(或任何适合您的web容器和部署的WAR的URL\)。

接下来，单击“调试”。系统将提示您进行身份验证，并在该页面上建议一系列用户名和密码。只需使用其中任何一个进行身份验证即可查看生成的页面。 它应包含类似于以下内容的成功消息：

```
Security Debug Information

Authentication object is of type:
org.springframework.security.authentication.UsernamePasswordAuthenticationToken

Authentication object as a String:

org.springframework.security.authentication.UsernamePasswordAuthenticationToken@1f127853:
Principal: org.springframework.security.core.userdetails.User@b07ed00: Username: rod; \
Password: [PROTECTED]; Enabled: true; AccountNonExpired: true;
credentialsNonExpired: true; AccountNonLocked: true; \
Granted Authorities: ROLE_SUPERVISOR, ROLE_USER; \
Password: [PROTECTED]; Authenticated: true; \
Details: org.springframework.security.web.authentication.WebAuthenticationDetails@0: \
RemoteIpAddress: 127.0.0.1; SessionId: 8fkp8t83ohar; \
Granted Authorities: ROLE_SUPERVISOR, ROLE_USER

Authentication object holds the following granted authorities:

ROLE_SUPERVISOR (getAuthority(): ROLE_SUPERVISOR)
ROLE_USER (getAuthority(): ROLE_USER)

Success! Your web filters appear to be properly configured!
```

成功收到上述消息后，返回示例应用程序的主页并单击“管理”。然后，您可以试用该应用程序。请注意，仅显示当前登录用户可用的联系人，并且只有具有ROLE\_SUPERVISOR的用户才有权删除其联系人。在幕后，MethodSecurityInterceptor正在保护业务对象。

该应用程序允许您修改与不同联系人关联的访问控制列表。请务必通过查看应用程序上下文XML文件来尝试并了解其工作原理。



