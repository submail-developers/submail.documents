## API: Voice/multixsend

<br>

### **概览**

<br>

`voice/multixsend` 是 SUBMAIL 的语音通知一对多（即1条API请求发送多个号码，并可以灵活控制每个联系人的文本变量）和群发 API 。


与 `voice/xsend` API 一样，`voice/multixsend`  提供完整且强大的语音通知呼叫功能，`voice/multixsend` 解决开发者在应用场景中的一对多或群发的需求，极大的提高 API 并发效率。

 

使用方法与 `voice/xsend` 相似，不同的是 `voice/multixsend` 去除了 to 和 vars 参数将其整合到 `multi` 参数中，可以将联系人的手机号码，和不同的文本变量整合，实现一对多场景中灵活控制文本变量的功能。

 

开发者们可在提交 `voice/multixsend` API 时，将 `to` 和` vars` 参数编码为 `JSON` 字符串格式添加到 `multi` 参数中提交，`multi` 参数的数据模型请参考以下示例：


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


完整的 `voice/multixsend`  POST 请求请参考以下示例：


```
appid=your_app_id
project=EM9sd
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
---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/voice/multixsend`

##### `https://api.submail.cn/voice/multixsend`

---

<br>

###  **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/voice/multixsend.json **(默认)**
xml |https://api.mysubmail.com/voice/multixsend.xml

---

****

<br>

### **http 请求方式**

<br>



请求方式| content-type设置
---|---
http post  | multipart/form-data、x-www-form-urlencoded、application/json

---

<br>

### **是否需要授权**

<br>

##### **是**

参阅 [API 授权和验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### **请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的语音应用 ID
project|string|必需|无|项目标记,在 SUBMAIL > Voice >项目中查看你所创建的短信项目标记。请参见[获取项目或地址薄的开发者标识](https://www.mysubmail.com/chs/documents/developer/MmSw12)
multi |json string|必需|无|收件人 to 联系人参数和 vars 文本变量的整合模式，请将 to 和 vars 整合成 json字符串格式提交（数据模型请参考本页概览页面提交打multi参数示例）
tag|string|可选|无|自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
sign_version|string|可选|1|signature加密计算方式(当sign_version传2时，multi参数不参与加密计算)
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

**请注意：**


```
multi 参数要求严格的 JSON 格式，以下是将参数转换为 JSON 格式的注意事项

json 字符串必须以双引号包含
json 字符串必须是 utf8 编码
不能有多余的逗号 如：[1,2,]
 json 字符串首尾必须被大括号{}包含 
 

PS:大多数的语言都有专属的JSON解析器（ ENCODING 和 DECODEING 方法）。如 PHP，首先将需要的变量以数组形式(如 $var[‘key’]=value) 创建后，使用 json_encode($var)方法创建 JSON 字符串；
```

---

<br>

### **代码示例**

<br>

#### 发送一封测试短信

> * JSON
#### `POST URL`

https://api.mysubmail.com/voice/multixsend.json

#### `POST Data`

```
appid=your_app_id
&project=ThJBE4
&multi=[{
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
&signature=your_app_key
```

#### `返回：`


```
[
   {
        "status":"success",
        "to":"15*********",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
       "fee":1,
        "money_account":14197
    },{
        "status":"success",
        "to":"18*********",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
        "fee":1,
        "money_account":14196
    }
]
```
---
> * XML

#### `POST URL`

https://api.mysubmail.com/voice/multixsend.xml

#### `POST Data`


```
appid=your_app_id
&project=ThJBE4
&multi=[{
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
&signature=your_app_key
```


#### `返回`

```
<?xml version="1.0" encoding="utf-8"?>
<xml>
   <item>
       <status>success</status>
       <to>15*********</to>
       <send_id>61aed69029363042495078c756a1f836</send_id>
       <fee>1</fee>
       <sms_credits>14197</sms_credits>
   </item>
   <item>
       <status>success</status>
       <to>18*********</to>
       <send_id>61aed69029363042495078c756a1f836</send_id>
       <fee>1</fee>
       <money_account>14196</money_account>
   </item>
</xml>
```
---

---

<br>

### **返回码**

<br>

>*   JSON

#### `请求成功`


```
[
   {
        "status":"success",
        "to":"15*********",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
        "fee":1,
        "money_account":14197
    },{
        "status":"success",
        "to":"18*********",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
        "fee":1,
        "money_account":14196
    },
]
```


#### `请求失败`


```
[
   {
        "status":"error",
        "to":"15*********",
        "code":1xx,
        "msg":"error message",
    },{
        "status":"success",
        "to":"18*********",
        "send_id":"093c0a7df143c087d6cba9cdf0cf3738",
        "money_account":14196
    }
]
```


>* XML

#### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
   <item>
       <status>success</status>
       <to>15*********</to>
       <send_id>61aed69029363042495078c756a1f836</send_id>
       <fee>1</fee>
       <money_account>14197</money_account>
   </item>
   <item>
       <status>success</status>
       <to>18*********</to>
       <send_id>61aed69029363042495078c756a1f836</send_id>
       <fee>1</fee>
       <money_account>14196</money_account>
   </item>
</xml>
```


#### `请求失败`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
   <item>
       <status>error</status>
       <code>1xx</code>
       <msg>error message</msg>
   </item>
   <item>
       <status>success</status>
      <to>18*********</to>
      <send_id>61aed69029363042495078c756a1f836</send_id>
      <money_account>14196</money_account>
   </item>
</xml>
```
注：`voice/multixsend` API 中返回码将包含成功和失败的状态 ，与message/multixsend相同。

---

<br>

### **错误代码**

<br>

参阅 [API 错误代码](https://www.mysubmail.com/chs/documents/developer/c8ujr)