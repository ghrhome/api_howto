### **对外API规范** {#API接口规范-•对外API规范}

http\(s\):// \[端点\]/\[包名称\]@\[版本\]/\[资源\]

# 

# 

# 对外API接口规范

调用saas系统API接口的客户端可能来自浏览器，手机app等。 对于接口的设计主要是鉴权的场景不同，具体接口的业务逻辑是一致的

1.浏览器调用场景

浏览器保存token信息，调用SaaS接口时，在API接口请求header中携带token信息，如下

请求头Header参数

| authorization | token信息 |
| :--- | :--- |


如 authorization: {“token”:"84F9F72BBB97130DD8AA6D59A2C9C2F"}

1. 手机APP调用场景

假如手机APP中不保存token信息，调用接口使用用户名和密码

| userid | 用户唯一标识 |
| :--- | :--- |
| ts | 时间戳，1970年1月1日0点0分0秒到当前时间的毫秒数，防止重放攻击,ts有效时间为10分钟 |
| sign | 签名信息，MD5（requestbody+password+ts） |
| apiver | api标准版本号 |

1. URL命名规范

[http\(s\)://domain:port/saas/microservicename/version/endpoints](http://domainport/)

例如获取设备信息[http://apigw.zoomlion.cn:port/saas//device/v1/](http://domainport/)devices

4.返回信息格式

{  
"code":"0000",  
"msg":"",  
"data":{  
    }  
}

