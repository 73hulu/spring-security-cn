JAAS示例是如何在Spring Security中使用JAAS LoginModule的非常简单的示例。如果用户名等于密码，则提供的LoginModule将成功验证用户，否则抛出LoginException。本示例中使用的AuthorityGranter始终授予角色ROLE\_USER。示例应用程序还演示了如何通过将jaas-api-provision设置为“true”来作为LoginModule返回的JAAS主题运行。
