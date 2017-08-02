# 程序相关代码：

oa文件路径记录：

```txt
客户端相关函数：ecology\social\im\js\im_pc_wev8.js
appkey文件：/ecology/WEB-INF/prop/EMobileRong.properties
过滤器：ecology\WEB-INF\web.xml
组织架构：HrmOrgTree
脚本：ecology\social\im\SocialIMUtil.jsp
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