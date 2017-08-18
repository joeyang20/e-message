# 程序相关代码：

oa文件路径记录：

```txt
客户端相关函数：ecology\social\im\js\im_pc_wev8.js
appkey文件：/ecology/WEB-INF/prop/EMobileRong.properties
过滤器：ecology\WEB-INF\web.xml
组织架构：HrmOrgTree
脚本：ecology\social\im\SocialIMUtil.jsp
群设置文件：SocialDiscussSetting.jsp
图片轮播页面：ecology\social\im\imageReview.jsp
开启emessage功能：ecology\WEB-INF\prop\Messager2.properties
```

相关方法：

```txt
显示表情，插入表情：drawExpressionWrap
```

vs-code调试：

```json
{
    "version": "0.2.0",
    "configurations": [{
        "name": "调试主进程",
        "type": "node",
        "request": "launch",
        "cwd": "C:/Users/joe/Desktop/electron_test/",
        "runtimeExecutable": "C:/Users/joe/Desktop/electron_test/electron.exe",
        "program": "C:/Users/joe/Desktop/electron_test/resources/app/main.js"
    }]
}
```

```java
jsp添加日志：
方法一：
<%@page import="weaver.general.BaseBean"%>
BaseBean log = new BaseBean();
log.writeLog("addOrDelGroupBook===========resourceids="+resourceids);

方法二：
<jsp:useBean id="log" class="weaver.general.BaseBean" scope="page" />
log.writeLog("addOrDelGroupBook===========resourceids="+resourceids);


java打日志：
new BaseBean().writeLog("querySql============"+querySql);
```

程序调试总结：

```log

```