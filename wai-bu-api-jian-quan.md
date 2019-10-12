**1.1 **接口鉴权规范

请求头Header参数

| appid | 应用的唯一标识 |
| :--- | :--- |
| ts | 时间戳，1970年1月1日0点0分0秒到当前时间的毫秒数，防止重放攻击,ts有效时间为10分钟 |
| sign | 签名信息，MD5（requestbody+appKey+ts） |
| apiver | api标准版本号 |



