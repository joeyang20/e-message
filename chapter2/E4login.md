# 客户端单点登录异常以及下载文件乱码

### 引起原因：

* 是由于`SocialIMFilter`过滤器没有生效导致的，所以需要确保`过滤器`生效。

### 解决步骤：

* 1.首先在`部署的服务器`上找到需要修改的文件，文件名是**ecology/WEB-INF/web.xml**，如下图：
<br/>
![web.xml文件](/image/webxml文件.PNG "Title")

* 2.打开文件，并且用`Ctrl+F`快捷键搜索是否含有`SocialIMFilter`关键字，如果找打这个`过滤器相关的配置`，那就`把以前的配置删除掉`，

* 3.然后再把`下方的配置`拷贝进去，粘贴在`文件最上方`，<web-app>节点的下方，

> \<filter><br/>
\<filter-name>SocialIMFilter\</filter-name><br/>
\<filter-class>weaver.social.filter.SocialIMFilter\</filter-class><br/>
\</filter><br/>
\<filter-mapping><br/>
\<filter-name>SocialIMFilter\</filter-name><br/>
\<url-pattern>/social/im/*.jsp\</url-pattern><br/>
\</filter-mapping><br/>
\<filter-mapping><br/>
\<filter-name>SocialIMFilter\</filter-name><br/>
\<url-pattern>/weaver/weaver.file.FileDownload\</url-pattern><br/>
\</filter-mapping><br/>

* 4.如果客户服务器使用的是`weblogic`作为web容器，请忽略上方配置而拷贝下方的配置：

> \<filter><br/>
\<filter-name>SocialIMFilter\</filter-name><br/>
\<filter-class>weaver.social.filter.SocialIMFilter\</filter-class><br/>
\</filter><br/>
\<filter-mapping><br/>
\<filter-name>SocialIMFilter\</filter-name><br/>
\<url-pattern>/social/im/*\</url-pattern><br/>
\</filter-mapping><br/>
\<filter-mapping><br/>
\<filter-name>SocialIMFilter\</filter-name><br/>
\<url-pattern>/weaver/weaver.file.FileDownload\</url-pattern><br/>
\</filter-mapping><br/>


* 5.修改之后如下图：
请务必把该**过滤器**放在下图说明的位置，如果有新的过滤器需要配置，例如**安全过滤器SecurityFilter**，请不要放在**SocialIMFilter**过滤器上方，否则会出现问题
![web.xml修改展示](/image/过滤器修改.png "Title")
