##  API: Message/template

<br>

### **概览**

<br>

`message/template` 是 SUBMAIL 的短信模板 API。

使用 `message/template` 可以获取、创建、编辑或删除您的短信模板。

`message/template` API 使用 `HTTP` 规范中的 `GET`, `POST`, `PUT`, `DELETE` 方法对模板进行操作，使用 `GET` 方法获取单个或全部模板、`POST` 方法创建新的短信模板并提交至 SUBMAIL 人工审核、`PUT` 方法更新或编辑一个短信模板，或使用 `DELETE` 方法删除一个模板。

短信模板引擎支持 `SUBHOOK` 异步推送状态，短信模板在后台人工审核后，会使用 `SUBHOOK` 进行主动推送状态。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/message/template`

##### `<备> https://api.submail.cn/message/template`

---

<br>

### **支持格式**

<br>

格式 | URL
---|---
json | https://api.mysubmail.com/message/template.json **（默认）**
xml |https://api.mysubmail.com/message/template.xml

---

<br>

### **http 请求方式**

<br>

- GET         获取全部模板列表，或获取指定的单个模板
- POST        创建一个新的短信模板，并提交至 SUBMAIL 进行人工审核
- PUT          编辑或更新一个短信模板，并提交至 SUBMAIL 进行人工审核
- DELETE        删除一个短信模板

---

<br>

### **是否需要授权**

<br>

##### **是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### **Message/template GET 方法（获取模板列表）请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的邮件应用ID
template_id |string|可选|无|模板ID（要获取单个模板，请将在此参数中提交该模板ID。为空则获取最新的1000个短信模板）
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制]( https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制]( https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制]( https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

----

<br>

### **Message/template POST 方法（创建模板）请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的邮件应用ID
sms_title |string|可选|无|模板标题（创建模板时可以在此参数中提交当前模板的标题，作为模板标记）
sms_signature |string|必需|无|短信模板签名(`请使用您的公司名或应用、APP、网站名作为您的短信签名，请将签名字数控制在2-10个字符以内，并使用全角大括号“【”和“】”包括，如:“【SUBMAIL】”`)
sms_content |string|必需|无|短信正文(`提交短信模板正文，请将模板正文字数控制在256个字符以内。可使用文本变量 参阅`[了解如何创建和使用文本变量](https://www.mysubmail.com/chs/documents/developer/index#/oKraS3))
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制]( https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制]( https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制]( https://api.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---

<br>

### **Message/template PUT 方法（更新模板）请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的邮件应用ID
template_id|string|必需|无|需要更新的模板 ID（在 SUBMAIL > Message >项目中查看你所创建的短信项目标记。请参见 [获取项目或地址薄的开发者标识](https://www.mysubmail.com/chs/documents/developer/MmSw12)）
sms_title |string|可选|无|模板标题（创建模板时可以在此参数中提交当前模板的标题，作为模板标记）
sms_signature |string|必需|无|短信模板签名(`请使用您的公司名或应用、APP、网站名作为您的短信签名，请将签名字数控制在2-10个字符以内，并使用全角大括号“【”和“】”包括，如:“【SUBMAIL】”`)
sms_content |string|必需|无|短信正文(`提交短信模板正文，请将模板正文字数控制在256个字符以内。可使用文本变量 参阅`[了解如何创建和使用文本变量](https://www.mysubmail.com/chs/documents/developer/index#/oKraS3))
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---
<br>

### **Message/template DELETE 方法（删除模板）请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的邮件应用ID
template_id |string|可选|无|需要删除的模板 ID(（在 SUBMAIL > Message >项目中查看你所创建的短信项目标记。请参见 [获取项目或地址薄的开发者标识](https://www.mysubmail.com/chs/documents/developer/MmSw12)）)
timestamp|UNIX 时间戳|可选|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（  `md5 or sha1 or normal` ）参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式
signature|string|必需|无|应用密匙或数字签名参阅 [API授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)  \>  授权和验证方式

---
#### 使用 `CURL` GET方法获取模板列表


*   JSON


#### `发送 CURL`


```
curl -s "https://api.mysubmail.com/message/template.json?appid=your_appid&signature=your_appkey"
```


#### `返回`


```
{
"status": "success",
"template": {
    "template_id": "FIJe14",
    "sms_title": "账户更改邮箱验证码",
    "sms_signature": "【SUBMAIL】",
    "sms_content": "您正在执行更改登录邮箱操作，验证码：@var(code) ，请在工单内提供此验证码",
    "add_date": "2016-01-08 21:28:04",
    "edit_date": "2016-01-08 21:28:04",
    "template_status": "2",
    "template_status_description": "通过审核"
    }
}
```
---
* XML

#### `发送 CURL`


```
curl -s "https://api.mysubmail.com/message/template.xml?appid=your_appid&signature=your_appkey"
```


#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status>success</status>
    <template>
        <template_id>FIJe14</template_id>
        <sms_title>账户更改邮箱验证码</sms_title>
        <sms_signature>【SUBMAIL】</sms_signature>
        <sms_content>您正在执行更改登录邮箱操作，验证码：@var(code) ，请在工单内提供此验证码</sms_content>
        <add_date>2016-01-08 21:28:04</add_date>
        <edit_date>2016-01-08 21:28:04</edit_date>
        <template_status>2</template_status>
        <template_status_description>通过审核</template_status_description>
    </template>
</xml>
```

---

#### 使用 `CURL` POST方法提交短信模板



*   JSON


#### `发送 CURL`


```
curl -d "appid=your_appid&signature=your_appkey&sms_title=POST方法测试&sms_signature=【SUBMAIL】&sms_content=您的验证码是：@var(code)，请在10分钟内输入。" http://api.mysubmail.com/message/template.json
```


#### `返回`


```
{
    "status": "success",
    "template_id": "FsoAF3"    // API 返回的模板ID，作为请求 API 的 PROJECT 参数
}
```
---
* XML
#### `发送 CURL`


```
curl -d "appid=your_appid&signature=your_appkey&sms_title=POST方法测试&sms_signature=【SUBMAIL】&sms_content=您的验证码是：@var(code)，请在10分钟内输入。" http://api.mysubmail.com/message/template.xml
```


##### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status>success</stats>
    <template_id>FsoAF3</template_id>     // API 返回的模板ID，作为请求 API 的 PROJECT 参数
</xml>
```

---

#### 使用 `CURL` PUT 方法修改短信模板



*   JSON


#### `发送 CURL`


```
curl --data "appid=your_appid&signature=your_appkey&template_id=FsoAF3&sms_title=PUT方法更新模板测试&sms_signature=【SUBMAIL】&sms_content=您的验证码是：@var(code)，请在30分钟内输入。" -X put http://api.mysubmail.com/message/template.xml
```


#### `返回`


```
{
    "status":"success"
}
```
---

*XML

#### `发送 CURL`

```
curl --data "appid=your_appid&signature=your_appkey&template_id=FsoAF3&sms_title=PUT方法更新模板测试&sms_signature=【SUBMAIL】&sms_content=您的验证码是：@var(code)，请在30分钟内输入。" -X put http://api.mysubmail.com/message/template.xml
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status> success </status>
</xml>
```

---


#### 使用 `CURL` DELETE 方法删除短信模板



*   JSON

### `发送 CURL`


```
curl --data "appid=your_appid&signature=your_appkey&template_id=FsoAF3" -X delete http://api.mysubmail.com/message/template.json
```


##### `返回`


```
{
    "status":"success"
}
```

* XML

#### `发送 CURL`

```
curl --data "appid=your_appid&signature=your_appkey&template_id=FsoAF3" -X delete http://api.mysubmail.com/message/template.json
```

#### `返回`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status> success </status>
</xml>
```

<br>

### **template_status 模板状态描述**

<br>



模板状态| 描述
---|---
template_status : 0| 未提交审核
template_status : 1| 正在审核
template_status : 2| 审核通过
template_status : 3| 未通过审核

---

<br>

### **返回码**

<br>

*   JSON

#### `请求成功`


```
{
    "status":"success"
}
```


#### `请求失败`


```
{
    "status":"error",
    "code":"1xx",
    "msg":"error message"
}
```

* XML

##### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status> success </status>
</xml>
```


#### `请求失败`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status> error </status>
    <code> 1xx </code>
    <msg> error message </msg>
</xml>
```

<br>

### **错误代码**

<br>

参阅 [API 错误代码](https://www.mysubmail.com/chs/documents/developer/c8ujr)