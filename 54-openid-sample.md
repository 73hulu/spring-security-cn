OpenID示例演示了如何使用命名空间配置OpenID以及如何为Google，Yahoo和MyOpenID身份提供程序设置属性交换配置（如果愿意，可以尝试添加其他配置）。它使用基于JQuery的openid-selector项目来提供用户友好的登录页面，允许用户轻松选择提供者，而不是键入完整的OpenID标识符。

该应用程序与普通身份验证方案的不同之处在于，它允许任何用户访问该站点（前提是他们的OpenID身份验证成功）。当你第一次登录时，你会收到一条“欢迎\(你的名字\)”的信息。如果您注销并重新登录（具有相同的OpenID标识），则应更改为“欢迎回来”。

这是通过使用自定义UserDetailsService来实现的，该自定义UserDetailsService为任何用户分配标准角色并在内部将身份存储在地图中。显然，真正的应用程序将使用数据库。请查看源表单中的更多信息。该类还考虑到可能从不同的提供者返回不同的属性，并构建相应的用户名。

