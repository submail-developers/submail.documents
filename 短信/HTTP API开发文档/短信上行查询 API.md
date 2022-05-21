# API: SMS/mo - 短信上行查询

<br>

### **概览**

<br>

`sms/mo` 是 SUBMAIL 的短信上行查询API。使用 `sms/mo` 可以实时查询短信上行回复。



请注意：

- 该接口请求限制为每分钟1次，时间间隔内返回上一次查询的缓存数据。
- 请注意 start_date（开始日期）和 end_date（结束日期）参数，当有其他筛选条件时，该时间段内查询不到时会返回无记录

------

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/sms/mo`

------


<br>

### **支持格式**

<br>


| 格式   | URL                                                |
| ------ | -------------------------------------------------- |
| `json` | `https://api-v4.mysubmail.com/sms/mo.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/sms/mo.xml`          |
| `yaml` | `https://api-v4.mysubmail.com/sms/mo.yaml`         |

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
| `from`       | `string`      | `可选`    | 无       | 查询特定的手机号码                                           |
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
curl -d "appid=your_appid&signature=your_appkey" https://api-v4.mysubmail.com/sms/mo
```

<br>

##### 返回


```json
{
    "status": "success", // API 请求状态
    "start_date": 1652554968, //开始日期
    "end_date": 1653159768, //结束日期
    "total": 2,	//查询总数
    "offset": 0, //数据偏移值
    "results": 2, //返回结果数
    "mo": [
        {
            "appid": "3xxxx",  // appid
            "from": "158xxxxxxxx", // 回复手机号
            "content": "你好 xxxx", // 回复正文
            "reply_at": 1653026354 // 回复时间
        },
        {
            "appid": "3xxxx", // appid
            "from": "132xxxxxxxx", // 回复手机号
            "content": "td", // 回复正文
            "reply_at": 1652573228 // 回复时间
        }
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

