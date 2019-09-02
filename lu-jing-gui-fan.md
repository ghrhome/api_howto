# 路径规范

### 1.1 API的根URL

API的根URL设计非常重要。当开发人员接手一个使用已有API所开发的旧项目，并且需要为它增加新特性的时候，他可能完全不了解现有的服务，或许他们知道的就是所调用的一系列URL。重要的是API的URL根应该尽可能简单。

如果应用程序很庞大，或者未来它可能变得很庞大，可以把API放在各自的子域内，这么做可以让你的程序在以后的发展中更灵活、更容易扩展。

如果程序不会变得这么大，或者目的是简化程序的使用（例如，想通过一个框架同时提供网站和API服务），就把API放在URL的根域（例如：/api/）之后。

建议将API部署在专有域名下，以此屏蔽消费者对服务提供方的部署细节（可借助于平台的反向代理+路由网关），在服务地图丰富起来之后可以考虑多级域名。

[https://api.example.com](https://api.example.com/)

[https://example.com/api/](https://example.org/api/)

ZValleyOS平台API的根URL设计基于微服务及模块，（注：目前平台微服务集中在单一域名端口下）

```
http://10.39.52.225:8101/
```

### 1.2  端点（endpoint）

路径又称端点（endpoint），表示API的具体网址。

在ZValleyOS平台的应用中，**端点指对应的 {微服务地址}+{模块/资源根节点}。与传统端点有所区别的是，在ZValley OS平台中，端点描述的是服务。**

例如：

```
http://10.39.52.225:8101/ea/
```

### 1.3 api版本控制（详情件版本控制规范）

应该将API的版本号放入URL。

```
https://api.example.com/{endpoint}/v{n}/
```

采用多版本并存，增量发布的方式

v{n} n代表版本号,分为整形和浮点型

整形的版本号: 大功能版本发布形式；具有当前版本状态下的所有API接口 ,例如：v1,v2

浮点型：为小版本号，只具备补充api的功能，其他api都默认调用对应大版本号的api 例如：v1.1 v2.2

### 1.4 资源（collection+resource）

在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"集合"（collection），所以API中的名词也应该使用复数。

ZValleyOS平台里采用{collection}+{resource}的形式来定位资源，

例：集合类资源

```
http://10.39.52.225:8101/ea/v1/products/
```

具体资源

```
http://10.39.52.225:8101/ea/v1/products/{pid}
```

### 1.5 补充动词（CustomVerb）

引入CustomVerb来描述动作或指令。

```
//启用组件 
POST   http://10.39.52.225:8101/ea/v1/components.start                 
       params: {id: Number, version: String}

//禁用组件 
POST  http://10.39.52.225:8101/ea/v1/components.disable              
      params: {id: Number, version: String}

//组件升级 
POST  http://10.39.52.225:8101/ea/v1/components.upgrade             
      params: {id: Number, version: String}
```

### 方案-实践建议：

1.使用HTTP动词表示增删改查资源， GET：查询，POST：新增，PUT：更新，DELETE：删除

2.**组合命名统一用 \_下划线命名法\(UnderScoreCase\)的形式。**

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

