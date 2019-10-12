# 协议规范

为进一步确保数据交互安全。生产环境必须遵循HTTPS协议。

**每个微服务要有且仅有一个自己唯一的API端点（\[协议\]://\[域名\]:\[端口\]/\[微服务\]/）。在项目配置文件中要添加静态变量专门进行存储。**

**每个项目/应用要有且仅有一个自己唯一的域名+端口。**

### HTTP动词使用规范：

### 1.1 动词 + 宾语

RESTful 的核心思想就是，客户端发出的数据操作指令都是"动词 + 宾语"的结构。比如，`GET /products`这个命令，`GET`是动词，`/products`是宾语。

动词通常就是五种 HTTP 方法，对应 CRUD 操作。

> * GET：读取（Read）
> * POST：新建（Create）
> * PUT：更新（Update）
> * PATCH：更新（Update），通常是部分更新
> * DELETE：删除（Delete）

根据 HTTP 规范，动词一律大写。

### 1.2 动词的覆盖

有些客户端只能使用`GET`和`POST`这两种方法。服务器必须接受`POST`模拟其他三个方法（`PUT`、`PATCH`、`DELETE`）。

这时，客户端发出的 HTTP 请求，要加上`X-HTTP-Method-Override`属性，告诉服务器应该使用哪一个动词，覆盖`POST`方法。

> ```
> POST /api/products HTTP/1.1  
>
> X-HTTP-Method-Override:
>  PUT
> ```

上面代码中，`X-HTTP-Method-Override`指定本次请求的方法是`PUT`，而不是`POST`。





