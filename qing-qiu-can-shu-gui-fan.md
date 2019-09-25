# 请求参数规范

### 1.1 过滤信息：

请求信息应该为集合提供过滤、排序、选择和分页等功能

1）Filtering过滤:

使用唯一的查询参数进行过滤：

例如：查询已发布的产品。你可能会设计成下面的 URL。

GET /products/published

查询字符串的写法明显更好。

GET /products?published=true

2）Sorting排序:

允许针对多个字段排序

GET /products?sortby=-manufactorer,desc+model,asc

这是返回根据生产者降序和模型升序排列的products集合

3）Fieldselection

移动端能够显示其中一些字段，它们其实不需要一个资源的所有字段，给API消费者一个选择字段的能力，这会降低网络流量，提高API可用性。

GET /products?fields=manufacturer+model+id+color

**注：设计中"+"代表字段的合并，“,”连接字段的相关附件信息**

4）Paging分页

使用 limit 和offset.实现分页，缺省limit=20 和offset=0；

//GET /products?offset=10&limit=5

GET /products?pageNo=10&pageSize=20

--

过滤器通常用于过滤GET请求返回的资源集合，在GET请求中，可以通过URL传递过滤器信息。你可以放心把下面例子中列出的过滤器类型应用到自己的API中：

pageSize=20，//limit=10：限制返回给用户的结果集的数量（通常用于分页）；

pageNo=10 //offset=10：给用户返回一个结果集（通常用于分页）；\[逍遥子笔记：指定偏移量，从指定位置开始返回结果集，与limit结合使用就可以达到分页效果，第一次从开始获取指定数量的结果，后续都要从上次结果之后开始返回\]

product\_type\_id=1：返回符合条件的结果集（类似于数据库的WHERE查询条件：WHERE product\_type\_id=1）；

sortby=name,asc：将结果集按照指定属性和指定排序方式进行排序（类似于数据的ORDER BY name ASC）；

### 1.2.避免多级 URL

常见的情况是，资源需要多级分类，因此很容易写出多级的 URL，比如获取某个产品的某一类设备。

GET /products/12/devices/塔机/

这种 URL 不利于扩展，语义也不明确，往往要想一会，才能明白含义。

更好的做法是，除了第一级，其他级别都用查询字符串表达。

GET /products/12?devices=塔机

如果两级的collection/souce的关系，比如

GET /products/12/devices/2，

建议device id为唯一命名，可以直接通过

GET /devices/2定位资源

