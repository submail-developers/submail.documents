 # API: InternationalSMS/MultiXSend - 国际短信模板一对多发送

<br>

### **概览**

<br>

`internationalsms/multixsend` 是 SUBMAIL 的国际短信一对多（即1条API请求发送多个号码，并可以灵活控制每个联系人的文本变量）和群发 API 。

 

`internationalsms/multixsend ` 能够提供完整且强大的短信发送功能，`internationalsms/multixsend` 解决开发者在应用场景中的一对多或群发的需求，极大的提高 API 并发效率。

 


 <br>

开发者们可在提交 `internationalsms/multixsend` API 时，将 `to` 和 `vars` 参数编码为 `JSON` 字符串格式添加到 `multi` 参数中提交，multi 参数的数据模型请参考以下示例：




```
multi=[{
        "to":"+177888*********",
        "vars":{
            "name":"kevin",
            "code":123456
        }
    },{
        "to":"+8529*********",
        "vars":{
            "name":"jacky",
            "code":236554
        }
    },{
        "to":"+45489*********",
        "vars":{
            "name":"tom",
            "code":236554
        }]
```

<br>
完整的 `internationalsms/multixsend`  POST 请求请参考以下示例：


```
appid=your_app_id
&amp;project=EM9sd
&amp;multi=[{
    "to":"15*********",
    "vars":{
        "name":"kevin",
        "code":123456
    }
},{
    "to":"18*********",
    "vars":{
        "name":"jacky",
        "code":236554
    }
},{
    "to":"13*********",
    "vars":{
        "name":"tom",
        "code":236554
    }]
&amp;signature=your_app_key
```
---

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/internationalsms/multixsend`

---

<br>

###  **支持格式**

<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/internationalsms/multixsend.json `**（默认）** |
| `xml`  | `https://api-v4.mysubmail.com/internationalsms/multixsend.xml` |
| `yaml` | `https://api-v4.mysubmail.com/internationalsms/multixsend.yaml` |

------

<br>

### **http 请求方式**

<br>

| 请求方式    | content-type设置                                             |
| ----------- | ------------------------------------------------------------ |
| `http post` | `multipart/form-data`、`x-www-form-urlencoded`、`application/json` |

---

<br>

### **是否需要授权**

<br>

##### 是

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/pdxzv1)

---

<br>

### **请求参数**

<br>

| 参数           | 类型          | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`      | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的国际短信应用 ID                   |
| `project`      | `string`      | `必需`    | 无       | 项目标记，在 SUBMAIL >国际 短信>项目列表中查看你所创建的短信项目（模板ID）标记。请参见 [获取项目 ID](https://www.mysubmail.com/documents/US56a) |
| `multi`        | `json string` | `必需`    | 无       | 收件人 to 联系人参数和 vars 文本变量的整合模式，请将 to 和 vars 整合成 json字符串格式提交（数据模型请参考本页概览页面提交打multi参数示例） |
| `timestamp`    | UNIX 时间戳   | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/pdxzv1)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`      | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/pdxzv1)  \>  授权和验证方式 |
| `sign_version` | `string`      | 可选      | 无       | signature加密计算方式(当sign_version传2时，multi参数不参与加密计算) |
| `signature`    | `string`      | `必需`    | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/pdxzv1)  \>  授权和验证方式 |

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信
<br>

##### POST URL

```
https://api-v4.mysubmail.com/internationalsms/multixsend.json
```

<br>

##### POST DATA

```
appid=your_app_id
&amp;project=ThJBE4
&amp;multi=[{
    "to":"+17788xxxxxxxx",
    "vars":{
        "name":"kevin",
        "code":123456
        }
    },{
    "to":"+17788xxxxxxxx",
    "vars":{
        "name":"jacky",
        "code":236554
        }
    }]
&amp;signature=your_app_key
```

<br>

---



<br>

#### **返回值**

<br>



##### 请求成功


```
[
   {
        "status":"success",
        "to":"+17788xxxxxxxx",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
        "fee":0.05,
        "account_balance":14197.087
    },{
        "status":"success",
        "to":"+17788xxxxxxxx",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
        "fee":0.05,
        "account_balance":14197.037
    }
]
```

<br>
##### 请求失败


```
[
   {
        "status":"error",
        "code":1xx,
        "msg":"error message"
    },{
        "status":"success",
        "to":"+17788xxxxxxxx",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
		"fee":0.05,
        "account_balance":14197.087
    }
]
```
<br>
注：`internationalsms/multixsend API` 中返回码将包含成功和失败的状态 ，API 在一条API中发起对多个号码的请求，所以返回状态也是按多条API计算的，例如：单次请求中包含3个联系人，其中2个联系人请求成功，1个联系人请求失败时，此时的API返回状态，将包含3条状态数组（即2条 `status:success` ，1条 `status:error `的状态）

---

<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/wBDvw1)

------

