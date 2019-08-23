# 设备列表管理

## 创建单个设备 {#创建单个设备}

| 方法 | API | 说明 |
| :--- | :--- | :--- |
| POST | /v3/iot/management/device | 创建单个设备 |

**请求参数**

| 参数名称 | 参数类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| deviceName | string | 必选 | 设备名称 |
| description | string | 必选 | 描述 |
| schemaId | string | 必选 | 物模型 |

**返回参数**

一个[DeviceAccessDetailResponse](https://cloud.baidu.com/doc/IOT/s/Mjwvy7nqs#deviceaccessdetailresponse%E5%8F%82%E6%95%B0%E5%88%97%E8%A1%A8)对象

**请求示例**

```
POST /v3/iot/management/device HTTP/1.1
Host: iotdm.gz.baidubce.com
Authorization: {authorization}
Content-Type: application/json; charset=utf-8
{
       "deviceName": "mydevice",
       "description": "device_description",
       "schemaId":"uuid"
}  
```

**返回示例**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
x-bce-request-id: 993ff7e9-018b-4246-a7ba-5dddac970054
{
       "tcpEndpoint": "tcp://test.baidu.iot.com",
       "sslEndpoint": "ssl://test.baidu.iot.com",
       "username": "endpointName/device_1",
       "key":"bWwCxGwaw3boV48NqsuG+XVaHpxfKdMPvmdJzNObvbY="
} 
```

## 删除设备 {#删除设备}

| 方法 | API | 说明 |
| :--- | :--- | :--- |
| PUT | /v3/iot/management/device?remove | 删除设备 |

**请求参数**

一个[DeviceListRequest](https://cloud.baidu.com/doc/IOT/s/Mjwvy7nqs#devicelistrequest%E5%8F%82%E6%95%B0%E5%88%97%E8%A1%A8)对象

**返回参数**

一个[DeviceListResponse](https://cloud.baidu.com/doc/IOT/s/Mjwvy7nqs#devicelistresponse%E5%8F%82%E6%95%B0%E5%88%97%E8%A1%A8)对象

**请求示例**

```
PUT /v3/iot/management/device?remove HTTP/1.1
Host: iotdm.gz.baidubce.com
Authorization: {authorization}
Content-Type: application/json; charset=utf-8
{
    "devices": [
        "device-1",
        "device-2"
    ]
}
```

**返回示例**

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
x-bce-request-id: 993ff7e9-018b-4246-a7ba-5dddac970054
{
    "devices": [
        "device-1",
        "device-2"
    ]
}
```



