# API: SMS/Log - 历史明细查询

<br>

### **概览**

<br>

`sms/log` 是 SUBMAIL 的历史明细查询API。使用 `sms/log` 可以实时查询已发送的短信历史明细数据。



请注意：

- 该接口请求限制为每分钟1次，时间间隔内返回上一次查询的缓存数据。
- 请注意 start_date（开始日期）和 end_date（结束日期）参数，当有其他筛选条件时，该时间段内查询不到时会返回无记录

------

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/sms/log`

------


<br>

### **支持格式**

<br>


| 格式   | URL                                                 |
| ------ | --------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/sms/log.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/sms/log.xml`          |
| `yaml` | `https://api-v4.mysubmail.com/sms/log.yaml`         |

------

<br>

### **http 请求方式**

<br>

| 请求方式    | content-type设置                                             |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

------

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

------

<br>

### **sms/log   请求参数**

<br>


| 参数         | 类型          | 必需/可选 | 默认     | 描述                                                         |
| ------------ | ------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`      | `string`      | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `start_date` | `UNIX 时间戳` | `可选`    | 1天前    | 开始时间，unix时间戳，精确到秒 `eg:1640100000`               |
| `end_date`   | `UNIX 时间戳` | `可选`    | 当前时间 | 结束时间，unix时间戳，精确到秒 `eg:1640100000`               |
| `to`         | `string`      | `可选`    | 无       | 查询特定的手机号码                                           |
| `send_id`    | `string`      | `可选`    | 无       | 查询特定的 Send ID                                           |
| `sendlist`   | `string`      | `可选`    | 无       | 查询特定的发送任务，（`batchsend`,`batchxsend`和`timedtask`接口的`batchlist` 参数） |
| `status`     | `string`      | `可选`    | 无       | `delivered`或`dropped`，如需查询所有成功的明细请将该参数设置为：`delivered`，查询失败则传参 `dropped` |
| `rows`       | `int`         | `可选`    | `50`     | 返回的数据行数                                               |
| `offset`     | `int`         | `可选`    | `0`      | 数据偏移值（与sql翻页操作方法一致）                          |
| `timestamp`  | `UNIX 时间戳` | `可选`    | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`  | `string`      | `可选`    | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `signature`  | `string`      | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |

------

<br>

### **代码示例**

<br>

##### 发送 CURL请求


```json
curl -d "appid=your_appid&signature=your_appkey" https://api-v4.mysubmail.com/sms/log
```

<br>

##### 返回


```json
{
    "status": "success", //API请求状态
    "start_date": 1644152198, //日志查询开始日期
    "end_date": 1644238598,	//日志查询结束日期
    "total": 724,	// 记录数
    "offset": 0, // 数据偏移值
    "results": 50, //每页行数
    "data": [ //数据
        {
            "sendID": "f3a34daf58210d498917f31c7d26693f", //send ID
            "to": "xxx", // 手机号码
            "appid": "xxx",	// AppID
            "template_id": "xxx", //模板ID
            "sms_signature": "【xx】",	//短信签名
            "sms_content": "您本次登录的验证码：xxx",	//短信正文
            "status": "delivered", //发送状态 ，delivered = 成功 ， dropped = 失败 ， pending=未知（运营商未返回）
            "report_state": "DELIVRD", // 运营商返回的实际状态 DELIVRD = 成功，其他均为失败 pending=未知（运营商未返回）
            "location": "广东 广州",  //手机号归属地
            "mobile_type": "中国移动", // 手机运营商
            "ip_address": "xxx", // 发送IP
            "send_at": 1644209557, // 请求时间
            "sent_at": 1644209557, //平台发送时间
            "report_at": 1644209561 //运营商状态汇报时间（一般为用户的手机收到短信的时间）
        },
      	{
            "sendID": "c7770e74d84377a5cdad844131e46b96",
            "to": "xxx",
            "appid": "xxx",
            "template_id": "xxx",
            "sms_signature": "【xxx】",
            "sms_content": "您本次登录的验证码：xxx",
            "status": "dropped",
            "report_state": "mk:0012",
            "dropped_reason": "空号/停机", // 失败原因，该参数仅在该条数据失败时返回的原因分析
            "location": "上海 上海",
            "mobile_type": "中国移动",
            "ip_address": "xxx",
            "send_at": 1644210137,
            "sent_at": 1644210137,
            "report_at": 1644210139
        },
        {…………}
        ]
}
```

---

<br>

##### 请求失败


```json
{
"status":"error",
"code":"1xx",
"msg":"error message"
}
```

---

<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------

