# API设计思路

API设计思路

![](/assets/image2019-8-13_11-11-33.png)

基本思路，基于rest api面向资源的设计来作为api的基本规范，对于实际业务里经常碰到的指令或者动作，用补充动词的方式来灵活处理。

同时，建议后端开发在构建接口方法时，命名方式对应rest api的动词，基本建议如下：

| Standard Method | HTTP Mapping | HTTP Request Body | HTTP Response Body |
| :--- | :--- | :--- | :--- |
| [List](https://link.jianshu.com/?t=https%3A%2F%2Fcloud.google.com%2Fapis%2Fdesign%2Fstandard_methods%23list) | GET &lt;collection URL&gt; | Empty | Resource\* list |
| [Get](https://link.jianshu.com/?t=https%3A%2F%2Fcloud.google.com%2Fapis%2Fdesign%2Fstandard_methods%23get) | GET &lt;resource URL&gt; | Empty | Resource\* |
| [Create](https://link.jianshu.com/?t=https%3A%2F%2Fcloud.google.com%2Fapis%2Fdesign%2Fstandard_methods%23create) | POST &lt;collection URL&gt; | Resource | Resource\* |
| [Update](https://link.jianshu.com/?t=https%3A%2F%2Fcloud.google.com%2Fapis%2Fdesign%2Fstandard_methods%23update) | PUT or PATCH &lt;resource URL&gt; | Resource | Resource\* |
| [Delete](https://link.jianshu.com/?t=https%3A%2F%2Fcloud.google.com%2Fapis%2Fdesign%2Fstandard_methods%23delete) | DELETE &lt;resource URL&gt; | Empty | Empty\*\* |

### **•对外API规范** {#API接口规范-•对外API规范}

http\(s\):// \[端点\]/\[包名称\]@\[版本\]/\[资源\]

方案-实践建议：

1.使用HTTP动词表示增删改查资源， GET：查询，POST：新增，PUT：更新，DELETE：删除

2.组合命名统一用 \_下划线命名法\(UnderScoreCase\)的形式。

3.GET只操作幂等性的查询操作。  
4.引入CustomVerb来描述动作或指令  
5.避免多级 URL

常见的情况是，资源需要多级分类，因此很容易写出多级的 URL，比如获取某个产品的某一类设备。

GET /products/12/devices/塔机/

这种 URL 不利于扩展，语义也不明确，往往要想一会，才能明白含义。

更好的做法是，除了第一级，其他级别都用查询字符串表达。

GET /products/12?devices=塔机

如果两级的collection/souce的关系，比如

GET /products/12/devices/2，

建议device id为唯一命名，可以直接通过

GET /devices/2定位资源

下面是另一个例子，查询已发布的产品。你可能会设计成下面的 URL。

GET /products/published

查询字符串的写法明显更好。

GET /products?published=true

1. 返回结果必须使用JSON

返回体统一格式如下   {

```
    "code":"DEVICE.001",

    "data":null,

    "msg":"test"

   }
```

1. HTTP状态码，在REST中都有特定的意义：200, 400, 401, 403, 500。比如401表示用户身份认证失败，403表示你验证身份通过了，但这个资源你不能操作。

2. 如果出现错误，返回一个错误码。比如：

999： 未知错误

1：     通用错误

2：     产品类错误

3：     设备类错误

4：     协议类错误

5：     权限类错误

10000：  通用参数类错误

10001： 资源未找到

10002： 未授权

### **解决Web端API 与 后台接口调用的API混用问题：** {#API接口规范-解决Web端API与后台接口调用的API混用问题：}

| method | api端点 | 版本 | 资源描述\[/Collection\]\[/Resource\] | 补充动词 | 查询 |
| :--- | :--- | :--- | :--- | :--- | :--- |
|  |  |  |  |  |  |

基本思路，基于BBF的思路，在版本处定义多端：

如标准web调用： /v1/

移动端调用： /V1.mobi/

内部API调用：/V1. service/   /V1.local/

也可参考：cdn的版本方案  /{api端点}/{mobi\|service\|local}@{版本}/{资源描述}  引入@标记。

