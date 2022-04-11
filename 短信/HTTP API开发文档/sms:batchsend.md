## API: SMS/BatchSend

<br>

### **概览**

<br>

`sms/batchsend` 是 SUBMAIL 的批量短信发送接口。与 sms/send 接口相似，在请求中自由提交短信内容，to （联系人）参数可以批量提交联系人手机号码（单次请求最大支持 10000 个）大幅提高群发需求的发送效率。

------

<br>



### URL

<br>

#####  `https://api-v4.mysubmail.com/sms/batchsend`

------



<br>

###  **支持格式**

<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/sms/timedtask.json `**（默认）** |
| `xml`  | `https://api-v4.mysubmail.com/sms/timedtask.xml`             |
| `yaml` | `https://api-v4.mysubmail.com/sms/timedtask.yaml`            |

------

<br>

### **http 请求方式**

<br>

| 请求方式    | content-type 支持                                            |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data、x-www-form-urlencoded、application/json` |

------

<br>

### **是否需要授权**

<br>

##### 是

#####  参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/VBcbe)

------


<br>

### **sms/batchsend 方法请求参数**

<br>

| 参数           | 类型          | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`      | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `to`           | `string`      | `必需`    | 无       | 收件人手机号码，多个手机号请使用半角逗号“,”分隔，如“138****,139********”。单次请求最大上限可提交 10000 个手机号码 |
| `content`      | `string`      | `必需`    | 无       | 短信正文<br>（正文中必须提交有效的短信签名，且您的短信签名必须放在短信的最前端，e.g.【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。<br>`content `参数将会与您账户中的短信模板进行匹配，如无匹配 API会创建一个短信模板并提交到人工审核，审核通过后下次提交相似短信（内容达到一定匹配度）则不会触发人工审核直接进行下发，如审核失败则第二次请求返回 420 错误，审核失败会触发 SUBHOOK 中模板 `template_reject` 事件<br>请将短信正文控制在 1000 个字符以内。） |
| `tag`          | `string`      | 可选      | 无       | 自定义标签功能，该标签可用作 SUBHOOK 追踪<br>（32 个字符以内，添加了 `tag` 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。`tag` 参数不参加加密计算） |
| `timestamp`    | `UNIX 时间戳` | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`      | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `sign_version` | `string`      | 可选      | 无       | signature加密计算方式<br>(当sign_version传2时，content参数不参与加密计算) |
| `signature`    | `string`      | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式。当sign_type=normal时signature应传appkey的值。 |

#### 

------

<br>

### **代码示例**

<br>

##### 发送请求

```
request: curl -d "appid=***&signature=***&content=【签名】测试&to=138xxxx,139xxxx" https://api-v4.mysubmail.com/sms/batchsend
```

##### 响应

```json
{
    "status": "success", //请求状态
    "batchlist": "***", //任务ID
    "total_fee": 2, //总计费条数
    "responses": [
        {
            "status": "success", //单号状态
            "to": "138xxxxxx", //号码
            "send_id": "007cb85168d1450e7aca462462ef12b8", //单号 SEND ID
            "fee": 1 //单号计费条数
        },
        {
            "status": "success",
            "to": "139xxxxxx",
            "send_id": "de4e69f475d24aad62948ac601e1c0ac",
            "fee": 1
        }
    ]
}
```

<br>

##### 请求失败


```
{
      "status":"error",
      "code":"1xx",
      "msg":"error message"
}
```

------

<br>

### **错误代码**

<br>

参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------

