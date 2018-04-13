# 过滤器设置

## 安全过滤器:securityFilter

[更新地址](http://www.weaver.com.cn/cs/securityDownload.asp)

## 修改过滤项

```txt
<url>/weaver/weaver.file.FileDownload</url>
```

需要用sysadmin登陆下oa，登陆成功后把后面的地址替换updateRules.jsp。
`http://e8.e-cology.com.cn/updateRules.jsp`
让刚修改的规则库文件即时生效。如果是集群环境，请在每个节点上都执行以下这个jsp。

造成sql执行不通过：注释掉**过滤器ConnFastFilter**。

下载失败的话，需要把登陆保护去掉：

登录保护是在这个页面
把/ecology/WEB-INF/weaver_security_config.xml中的<is-login-check>true</is-login-check>改成<is-login-check>false</is-login-check>，如果没有添加一项

 改完后用sysadmin登录系统，访问下: http://这里是oa地址/updateRules.jsp