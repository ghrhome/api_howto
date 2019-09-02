# 术语及含义

本文档中所使用的术语及其含义如下：

**Resource（资源）：**单个实例对象，例如equipment（一个设备）【Roy ThomasFielding（REST风格的提出者）如此解释资源的含义：一个资源可以是一份文档、一张图片、一个与时间相关的服务（例如：洛杉矶今天的天气）等等，资源是实体的概念性映射，而不是实体本身】

**Collection（集合）：**集合是一组同类的实例对象，例如products（产品集合）。

**HTTP/HTTPS：**在网络上传输的通信协议；

**Consumer（使用方、用户）：**能够发送http请求的客户端程序；\[这里Consumer实际是指API的调用方\]

**Third Party Developer（第三方开发人员）**：不是你项目项目团队的成员，但希望使用你的服务的那些开发人员；

**Server（服务器）：**能够被Consumer通过网络访问的HTTP服务器/程序；

**Endpoint（端点）：**服务器提供的一个URL，它标识了一个资源（Resource）或者集合（Collection）；【在ValleyOS平台的应用中，**端点指对应的 {微服务地址}+{模块/资源根节点}**】

**Idempotent（幂等）：**多次重复操作得到的结果一样；

**URL Segment（URL片段）：**从某个URL中取出的一小部分片段；

