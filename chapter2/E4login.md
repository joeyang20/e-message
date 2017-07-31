# 客户端单点登录异常以及下载文件乱码

## 引起原因：

是由于**SocialIMFilter**过滤器没有生效导致的，所以需要确保**过滤器**生效。

## 解决步骤：

1.首先在**部署的服务器**上找到需要修改的文件，文件名是**ecology/WEB-INF/web.xml**，如下图：

![web.xml文件](/image/webxml文件.PNG "Title")

2.打开文件，并且用**Ctrl+F**快捷键搜索是否含有**SocialIMFilter**关键字，如果找打这个**过滤器相关的配置**，那就**把以前的配置删除掉**，

3.然后再把**下方的配置**拷贝进去，粘贴在**文件最上方**，**\<web-app>**节点的下方，

```xml
<filter>
<filter-name>SocialIMFilter</filter-name>
<filter-class>weaver.social.filter.SocialIMFilter</filter-class>
</filter>
<filter-mapping>
<filter-name>SocialIMFilter</filter-name>
<url-pattern>/social/im/*.jsp</url-pattern>
</filter-mapping>
<filter-mapping>
<filter-name>SocialIMFilter</filter-name>
<url-pattern>/weaver/weaver.file.FileDownload</url-pattern>
</filter-mapping>
```

4.如果客户服务器使用的是`weblogic`作为web容器，请忽略上方配置而拷贝下方的配置：

```xml
<filter>
<filter-name>SocialIMFilter</filter-name>
<filter-class>weaver.social.filter.SocialIMFilter</filter-class>
</filter>
<filter-mapping>
<filter-name>SocialIMFilter</filter-name>
<url-pattern>/social/im/*</url-pattern>
</filter-mapping>
<filter-mapping>
<filter-name>SocialIMFilter</filter-name>
<url-pattern>/weaver/weaver.file.FileDownload</url-pattern>
</filter-mapping>
```

5.修改之后如下图：

请务必把该**过滤器**放在下图说明的位置，如果有新的过滤器需要配置，例如**安全过滤器SecurityFilter**，请不要放在**SocialIMFilter**过滤器上方，否则会出现问题。
![web.xml修改展示](/image/过滤器修改.png "Title")

6.上述步骤完成后，请重启OA服务，这样才能让配置生效。

7.如果客户是集群环境，那么集群环境里面的所有的OA服务的文件都得修改，这样才能确保功能正常，而且建议最好是一台轮着一台修改并且测试，不要一下子全都改了。并且每一台都测试通过才行。
