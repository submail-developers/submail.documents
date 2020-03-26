## API: `**`addressbook/mail/subscribe`**`

<br>

### **概览**

<br>

`addressbook/mail/subscribe` 是 SUBMAIL 的邮件订阅 API ，使用 `addressbook/mail/subscribe` API 管理你的邮件订阅用户。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/addressbook/mail/subscribe`

##### `<备>  https://api.submail.cn/addressbook/mail/subscribe`

<br>

### **支持格式**

<br>

格式 | URL
---|---
`json` | `https://api.mysubmail.com/addressbook/mail/subscribe.json`（默认） 
`xml` |`https://api.mysubmail.com/addressbook/mail/subscribe.xml`

---

<br>

### **http 请求方式**

<br>

##### `**POST**`

---

<br>

### **是否需要授权**

<br>

##### **是**

参阅 [API 授权和验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3)

---

<br>

### **请求参数**

<br>

参数| 类型|必需/可选|默认|描述
---|---|---|---|---
appid |string|必需|无|在 SUBMAIL 应用集成中创建的邮件应用ID
address|string|必需|无|联系人邮件地址   <br/>e.g.  `leo ` 或` `或 `leo@submail.cn`<br/>SUBMAIL 支持完整的 RFC 822 收件人标准，请确保您的邮件地址的有效性。<br/>请参见 [维基百科 EMAIL ADDRESS RFC822 文档](http://en.wikipedia.org/wiki/Email_address)
target| string      |可选|subscribe|地址簿标识，将联系人添加到目标地址簿<br/>忽略此参数，SUBMAIL 默认将联系人添加到订阅地址簿。<br/>请参见 [获取项目或地址簿的开发者标识](https://www.mysubmail.com/chs/documents/developer/MmSw12)
timestamp| UNIX 时间戳 |必需|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3) >  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（ ` md5 or sha1 or normal `）<br/>参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3) >  授权和验证方式
signature|string|必需|无|应用密匙 *或* 数字签名<br/>参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3) >  授权和验证方式



---

### **代码示例**

#### 添加一个邮件联系人到订阅地址簿

*   JSON

#### `POST `

```
https://api.mysubmail.com/addressbook/mail/subscribe.json
```

#### `POST Data：`


```
appid=your_app_id
&address=leo <leo@submail.cn>
&signature=your_app_key
```


#### `返回：`


```
{
    "status":"success"
}
```

---
* XML

#### `POST `

```
https://api.mysubmail.com/addressbook/mail/subscribe.xml
```

#### `POST Data：`


```
appid=your_app_id
&address=leo <leo@submail.cn>
&signature=your_app_key
```


#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
</xml>
```

---

#### 添加一个邮件联系人到目标地址簿


*   JSON

#### `POST `

```
https://api.mysubmail.com/addressbook/mail/subscribe.json
```

#### `POST Data：`


```
appid=your_app_id
&address=leo <leo@submail.cn>
&target=ThJBE4
&signature=your_app_key
```


#### `返回：`


```
{
    "status":"success"
}
```

---
* XML

#### `POST `

```
https://api.mysubmail.com/addressbook/mail/subscribe.xml
```

#### `POST Data：`


```
appid=your_app_id
&to=leo <leo@submail.cn>
&target=ThJBE4
&signature=your_app_key
```


##### `返回`


```
<?xml version="1.0" encoding="utf-8"?> 
<xml>     
    <status> success </status> 
</xml>
```

---

#### 使用 `CURL` 添加一个邮件联系人到订阅地址簿


*   JSON

##### `发送 CURL`

```
curl -d 'appid=your_app_id&address=leo <leo@submail.cn>&signature=your_app_key' https://api.mysubmail.com/addressbook/mail/subscribe.json
```

#### `返回：`


```
{
      "status":"success"
}
```
---
* XML

#### ``发送 CURL``

```
curl -d 'appid=your_app_id&address=leo <leo@submail.cn>&signature=your_app_key' https://api.mysubmail.com/addressbook/mail/subscribe.xml
```


#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
</xml>
```

---



#### 使用 `CURL` 添加一个邮件联系人到目标地址簿


*   JSON

##### `发送 CURL`

```
curl -d 'appid=your_app_id&address=leo <leo@submail.cn>&target=ThJBE4&signature=your_app_key' https://api.mysubmail.com/addressbook/mail/subscribe.json
```

#### `返回：`


```
{
      "status":"success"
}
```

---

* XML

#### ``发送 CURL``

```
curl -d 'appid=your_app_id&to=leo <leo@submail.cn>&target=ThJBE4&signature=your_app_key' https://api.mysubmail.com/addressbook/mail/subscribe.xml
```


#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
</xml>
```

---

#### 返回码


*   JSON

##### `请求成功`

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

---

* XML

#### ``请求成功``

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
     <status> success </status>
</xml>
```

---



<br>

### **错误代码**

<br>

> 参阅 [API 错误代码](/chs/documents/developer/c8ujr)