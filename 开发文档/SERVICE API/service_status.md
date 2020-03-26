
## API: service/status

<br>

### 概览

<br>

`service/status` API，返回 SUBMAIL 服务器状态和响应时间(单位：秒)。

---

<br>

### URL

<br>

##### `<主> https://api.mysubmail.com/service/status`

##### `<备> https://api.submail.cn/service/status`

---

<br>

### 支持格式

<br>

格式 | URL
---|---
json |https://api.mysubmail.com/service/status.json **（默认）**
xml |https://api.mysubmail.com/service/status.xml

<br>

### http 请求方式

<br>

##### **GET**

---

<br>

### 是否需要授权

<br>

##### **否**

---
<br>

### 请求参数

<br>

##### **无**

---

<br>

### 返回码

<br>

*   JSON


#### `请求成功`


```
{
      "status":"runing",
      "runtime":0.024
}
```
---

* XML

#### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <status>runing</status>
     <runtime>0.024</runtime>
</xml>
```

<br>

### 错误代码

<br>

##### **无**

---