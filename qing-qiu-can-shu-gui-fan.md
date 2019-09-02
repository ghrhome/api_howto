# 请求参数规范

### 1.1 过滤信息：

请求信息应该为集合提供过滤、排序、选择和分页等功能

1）Filtering过滤:

  


使用唯一的查询参数进行过滤：

  


GET /cars?color=red 返回红色的cars

  


2）Sorting排序:

  


允许针对多个字段排序

  


GET /cars?sort=-manufactorer,+model

  


这是返回根据生产者降序和模型升序排列的car集合

  


3）Fieldselection

  


移动端能够显示其中一些字段，它们其实不需要一个资源的所有字段，给API消费者一个选择字段的能力，这会降低网络流量，提高API可用性。

  


GET /cars?fields=manufacturer,model,id,color

  


4）Paging分页

  


使用 limit 和offset.实现分页，缺省limit=20 和offset=0；

  


GET /cars?offset=10

&

limit=5

  


为了将总数发给客户端，使用订制的HTTP头：X-Total-Count.

  


链接到下一页或上一页可以在HTTP头的link规定，遵循Link规定:

  


Link:

&lt;

[https://blog.mwaysolutions.com/sample/api/v1/cars?offset=15&limit=5](https://blog.mwaysolutions.com/sample/api/v1/cars?offset=15&limit=5)

&gt;

;rel=

"

next

"

,

&lt;

[https://blog.mwaysolutions.com/sample/api/v1/cars?offset=50&limit=3](https://blog.mwaysolutions.com/sample/api/v1/cars?offset=50&limit=3)

&gt;

;rel=

"

last

"

,

&lt;

[https://blog.mwaysolutions.com/sample/api/v1/cars?offset=0&limit=5](https://blog.mwaysolutions.com/sample/api/v1/cars?offset=0&limit=5)

&gt;

;rel=

"

first

"

,

&lt;

[https://blog.mwaysolutions.com/sample/api/v1/cars?offset=5&limit=5](https://blog.mwaysolutions.com/sample/api/v1/cars?offset=5&limit=5)

&gt;

;rel=

"

prev

"

,

--

过滤器通常用于过滤GET请求返回的资源集合，在GET请求中，可以通过URL传递过滤器信息。你可以放心把下面例子中列出的过滤器类型应用到自己的API中：

limit=10：限制返回给用户的结果集的数量（通常用于分页）；

offset=10：给用户返回一个结果集（通常用于分页）；\[逍遥子笔记：指定偏移量，从指定位置开始返回结果集，与limit结合使用就可以达到分页效果，第一次从开始获取指定数量的结果，后续都要从上次结果之后开始返回\]

animal\_type\_id=1：返回符合条件的结果集（类似于数据库的WHERE查询条件：WHERE animal\_type\_id=1）；

sortby=nameℴ=asc：将结果集按照指定属性和指定排序方式进行排序（类似于数据的ORDER BY name ASC）；

