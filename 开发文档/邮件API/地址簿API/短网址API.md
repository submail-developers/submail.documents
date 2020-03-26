## API: `ShortURL`

<br>

### **概览**

<br>

`Shorturl`是 SUBMAIL 的短网址 API。

使用 Shorturl API 可以获取、创建、编辑或删除您的短网址模板。

`shorturl API` 使用 `HTTP` 规范中的 `GET`, `POST`, `PUT`, `DELETE` 方法对模板进行操作，使用 `GET` 方法获取单个或全部模板、`POST` 方法创建新的短网址模板并提交至 SUBMAIL 人工审核、`PUT` 方法更新或编辑一个短网址模板，或使用 `DELETE` 方法删除一个模板。

短网址模板引擎支持 `SUBHOOK` 异步推送状态，短网址模板在后台人工审核后，会使用 `SUBHOOK` 进行主动推送状态。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/addressbook/message/subscribe`

##### `<备> https://api.submail.cn/addressbook/message/subscribe`

<br>

### **支持格式**

<br>

格式 | URL
---|---
`json` | `https://api.mysubmail.com/addressbook/message/subscribe.json`（默认） 
`xml` |`https://api.mysubmail.com/addressbook/message/subscribe.xml`

---

<br>

### **http 请求方式**

<br>

##### `POST`

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
appid |string|必需|无|在 SUBMAIL 应用集成中创建的短信应用ID
address|string|必需|无|联系人 11 位 手机号码 e.g.13xxxxxxxxx
target| string      |可选|subscribe|地址簿标识，将联系人添加到目标地址簿<br/>忽略此参数，SUBMAIL 默认将联系人添加到订阅地址簿。<br/>请参见 [获取项目或地址簿的开发者标识](https://www.mysubmail.com/chs/documents/developer/MmSw12)
timestamp| UNIX 时间戳 |必需|无|参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3) >  `Timestamp` UNIX 时间戳
sign_type|string|可选|normal|API 授权模式（ ` md5 or sha1 or normal `）<br/>参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3) >  授权和验证方式
signature|string|必需|无|应用密匙 *或* 数字签名<br/>参阅 [API 授权与验证机制](https://www.mysubmail.com/chs/documents/developer/gbibb3) >  授权和验证方式



---

### **代码示例**

#### 添加一个短信联系人到订阅地址簿

*   JSON

#### `POST `

```
https://api.mysubmail.com/addressbook/message/subscribe.json
```

#### `POST Data：`


```
appid=your_app_id
&address=138xxxxxxxx
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
https://api.mysubmail.com/addressbook/message/subscribe.xml
```

#### `POST Data：`


```
appid=your_app_id
&address=138xxxxxxxx
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

#### 添加一个短信联系人到目标地址簿


*   JSON

#### `POST `

```
https://api.mysubmail.com/addressbook/message/subscribe.json
```

#### `POST Data：`


```
appid=your_app_id
&address=138xxxxxxxx
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
https://api.mysubmail.com/addressbook/message/subscribe.xml
```

#### `POST Data：`


```
appid=your_app_id
&to=138xxxxxxxx
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

#### 使用 `CURL` 添加一个短信联系人到订阅地址簿


*   JSON

##### `发送 CURL`

```
curl -d 'appid=your_app_id&address=138xxxxxxxx&signature=your_app_key' https://api.mysubmail.com/addressbook/message/subscribe.json
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
curl -d 'appid=your_app_id&address=138xxxxxxxx&signature=your_app_key' https://api.mysubmail.com/addressbook/message/subscribe.xml
```


#### `返回：`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status> success </status>
</xml>
```

---



#### 使用 `CURL` 添加一个短信联系人到目标地址簿


*   JSON

##### `发送 CURL`

```
curl -d 'appid=your_app_id&address=138xxxxxxxx&target=ThJBE4&signature=your_app_key' https://api.mysubmail.com/addressbook/message/subscribe.json
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
curl -d 'appid=your_app_id&to=138xxxxxxxx&target=ThJBE4&signature=your_app_key' https://api.mysubmail.com/addressbook/message/subscribe.xml
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
      <status> error </status>
      <code> 1xx </code>
      <msg> error message </msg>
</xml>
```

---



<br>

### **错误代码**

<br>

> 参阅 [API 错误代码](/chs/documents/developer/c8ujr)