# API鉴权

# 术语

## AppKey

基础物联API认证密钥中user Auth.key。每个应用对应一个AppKey对应基础物联一个用户。应用数据权限为改用户所拥有的数据权限。



# 接口规则

## 总体规则

| 接口方式 | HTTP传输REST接口 |
| :--- | :--- |
| 提交方式 | POST方法提交 |
| 数据格式 | 提交和返回数据都为JSON格式 |
| 字符编码 | 统一采用UTF-8字符编码 |
| 签名算法 | MD5 |
| 签名要求 | 请求和接收数据均需要校验签名，详细方法请参考[安全规范-签名算法](https://pay.weixin.qq.com/wiki/doc/api/micropay.php?chapter=4_3) |

## 参数规则

请求参数包括权限验证参数及请求参数。权限验证参数为所有接口公共部分，请求参数放在data中。



| **参数名** | **参数类型** | **说明** |
| :--- | :--- | :--- |
| appId | String | 应用对应AppKey |
| version | String | 接口版本 |
| timeStamp | String | 请求时间：yyyy-MM-dd HH:mm:ss |
| nonce | String | 随机字符串 |
| sign | String | 签名字段 |
| data | object | 请求参数json体 |



参数示例：

```
{
"appId":"rIJXygBqTxQWcdBw",
"version":"v1",
"timeStamp":"2019-10-10 16:12:24",
"nonce":"edc4f9ee-bf01-4350-8e3c-18d2e3e8cb54",
"sign":"C6B94C68AE036650379B763339A18963",
"data":{
"iotId": null,
"uniqueNo": "100000000000000002",
"alarmTime": "2019-09-16 17:40:36",
"alarmTypeId": "alarm00",
"alarmName": null,
"alarmValue": "0",
"alarmResult": 102082,
"alarmGuid": "",
"province": "",
"city": "",
"area": "",
"road": null,
"longitude": 114.090582,
"latitude": 22.561305,
"encryptLong": 114.095711,
"encryptLat": 22.558624,
"accRunTimes": null,
"systemTime": "2019-09-16 17:39:36",
"inputTime": "2019-09-16 17:40:04"}
}
```



返回参数：



| **参数名** | **参数类型** | **说明** |
| :--- | :--- | :--- |
| code | String | 返回码 0000表示接口调用层返回成功 |
| data | object | 返回接口调用返回json体，又包含一层code和data。其中data才是最后返回的数据{“code”:”0000”,“data”:{}} |



```
{
"code": "0000",
"data": {
"data": {
"id": 373.0,
"code": "KaaBsDgt",
"name": "917演示传感器",
"description": "",
"tag": "",
"transportProtocol": "MQTT",
"transportProtocolDesc": "MQTT",
"nodeType": "0",
"nodeTypeDesc": "设备",
"isLinkGateway": "1",
"isLinkGatewayDesc": "是",
"status": "0",
"statusDesc": "未发布",
"catalogId": 1.0,
"catalogName": "自定义类型",
"createTime": "2019-09-03 11:46:19"
 },
"code": "0000"
 }
}
```

## 安全规范

签名算法

签名生成的通用步骤如下：

第一步，data内非空参数值的参数和timeStamp，nonce一起按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA。最后将appId拼接到最后stringA + “key”=appId得到stringB。

特别注意以下重要规则：

◆ 参数名ASCII码从小到大排序（字典序）；

◆ 如果参数的值为空不参与签名；

◆ 参数名区分大小写；

第二步，对stringB进行MD5运算，得到的值赋值给权限验证参数sign。

假设传送的参数如下：

```
{
"appId":"IyxNVtFiObOqcHUs",
"version":"v1",
"timeStamp":"2019-10-10 16:34:40",
"nonce":" e7dee728-c6a7-4fb0-ba7e-4cf146dd33c4",
"sign":"",
"data":{
"productCode":"KaaBsDgt"

}
}
```

第一步：对参数按照key=value的格式得到stringB：

nonce=e7dee728-c6a7-4fb0-ba7e-4cf146dd33c4&productCode=KaaBsDgt&timeStamp=2019-10-10 16:34:40&key=IyxNVtFiObOqcHUs

第二步：MD5计算签名的sign值：

9508C3DA8BF67392E2EFC17C59811372

最后发送参数为：

```
{
"appId":"IyxNVtFiObOqcHUs",
"version":"v1",
"timeStamp":"2019-10-10 16:34:40",
"nonce":" e7dee728-c6a7-4fb0-ba7e-4cf146dd33c4",
"sign":"C6B94C68AE036650379B763339A18963",
"data":{
"productCode":"KaaBsDgt"

}
}
```



# API列表

参数说明只有请求参数data Json体部分，权限验证参数这里不再列出。

