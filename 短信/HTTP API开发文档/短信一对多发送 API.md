# API: SMS/MultiSend  - 短信一对多发送

<br>

### **概览**

<br>

`sms/multisend` 是 SUBMAIL `sms/send` API 一对多（即1条API请求发送多个号码，可以灵活控制每个联系人的文本变量,并且无需提前创建模板）和群发 API 。（建议：单线程提交数量控制在50个联系人， 可以开多个线程同时发送）

使用方法与 `sms/send` 极为相似，不同的是 `sms/multisend` 去除了 `to` 参数将其整合到 `multi` 参数中，并且 `content` 参数将支持使用 `@var(key)` 方式申明文本变量，`multi` 参数可以将联系人的手机号码，和不同的文本变量整合，实现一对多场景中灵活控制文本变量的功能。

<br>

开发者们可在提交 `sms/multisend` API 时，将 `to` 和 `vars` 参数编码为 `JSON` 字符串格式添加到 `multi` 参数中提交，`multi` 参数的数据模型请参考以下示例：


```
multi=[{
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
```

<br>

完整的 `sms/multisend`  POST 请求请参考以下示例：


```
appid=your_app_id
content=【SUBMAIL】您好，@var(name)，您的取货码为 @var(code)
multi=[{
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
signature=your_app_key
```

------


<br>

### **URL**
<br>

##### `https://api-v4.mysubmail.com/sms/multisend`

------
<br>

###  **支持格式**
<br>

| 格式   | URL                                                          |
| ------ | ------------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/sms/multisend.json `**（默认）** |
| `xml`  | `https://api-v4.mysubmail.com/sms/multisend.xml`             |
| `yaml` | `https://api-v4.mysubmail.com/sms/multisend.yaml`            |

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

### **请求参数**
<br>


| 参数           | 类型          | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`      | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的短信应用ID                        |
| `content`      | `string`      | `必需`    | 短信正文 | 短信正文。<br>(正文中必须提交有效的短信签名，且您的短信签名必须放在短信的最前端，e.g.【SUBMAIL】您的短信验证码：4438，请在10分钟内输入。<br>content 参数将会与您账户中的短信模板进行匹配，如无匹配 则会自动创建一个短信模板并提交到人工审核，审核通过后下次提交相似短信内容时（内容达到一定匹配度）则不会触发人工审核，直接进行下发，如果审核失败则第二次请求返回 420 错误，审核失败会触发SUBHOOK中模板template_reject事件,请将短信正文控制在 1000 个字符以内。 |
| `multi`        | `json string` | `必需`    | 无       | 收件人 to 联系人参数和 vars 文本变量的整合模式，请将 to 和 vars 整合成 json字符串格式提交（数据模型请参考本页概览处multi参数示例） |
| `tag`          | `string`      | 可选      | 无       | 自定义标签功能，该标签可用作SUBHOOK追踪<br>（32 个字符以内，添加了 tag 参数的 API 请求，会在所有的 SUBHOOK 事件中携带此参数。tag参数不参加加密计算） |
| `timestamp`    | UNIX 时间戳   | 可选      | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`      | 可选      | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |
| `sign_version` | `string`      | 可选      | 2        | signature加密计算方式(当sign_version传2时，multi，content参数不参与加密计算) |
| `signature`    | `string`      | 必需      | 无       | 应用密匙或数字签名<br>参阅 [API授权与验证机制](https://www.mysubmail.com/documents/VBcbe)  \>  授权和验证方式 |


<br>
##### 注意：


```
multi 参数要求严格的 JSON 格式，以下是将参数转换为 JSON 格式的注意事项

json 字符串必须以双引号包含
json 字符串必须是 utf8 编码
不能有多余的逗号 如：[1,2,]
 json 字符串首尾必须被大括号{}包含 
 
PS:大多数的语言都有专属的JSON解析器（ ENCODING 和 DECODEING 方法）。如 PHP，首先将需要的变量以数组形式(如 $var[‘key’]=value) 创建后，使用 json_encode($var)方法创建 JSON 字符串；
```

------



<br>

### **代码示例**

<br>

#### 发送一封测试短信

<br>

##### POST URL

```
https://api-v4.mysubmail.com/multisend
```

<br>

##### POST DATA

```
appid=your_app_id
&amp;content=【SUBMAIL】您好，@var(name)，您的取货码为 @var(code)
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
    }]
&amp;signature=your_app_key
```

<br>

---

<br>

#### 返回值

<br>


##### 请求成功


```
[
  {
    "status": "success",
    "send_id": ""c2f0e679ad8dc2bf6cb71bf2925665e0",
    "fee": 1
    },{
    "status": "success",
    "send_id": ""z5sd8679ad8dc2bf6cb71bf292595g23,
    "fee": 1
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
        "msg":"error sms"
    },{
        "status":"success",
        "to":"18*********",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738"
    }
]
```

注：`sms/multisend API` 中返回码将包含成功和失败的状态 ，API 在一条API中发起对多个号码的请求，所以返回状态也是按多条API计算的，例如：单次请求中包含3个联系人，其中2个联系人请求成功，1个联系人请求失败时，此时的API返回状态，将包含3条状态数组（即2条 `status:success` ，1条 `status:error `的状态）

------

<br>



### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

------
