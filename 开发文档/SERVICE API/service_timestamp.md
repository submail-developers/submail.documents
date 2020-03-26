
## API: service/timestamp

<br>

### **概览**

<br>

UNIX 时间戳在 SUBMAIL API 中有着非常重要的作用，它是大多数提交 API 请求时 (几乎所有的 POST 请求) 必要的签名参数。

`timestamp` API 请求时使用 `http GET` 方法，返回一个服务器 UNIX 时间戳。

---

<br>

### **URL**

<br>

##### `<主> https://api.mysubmail.com/service/timestamp`

##### `<备> https://api.submail.cn/service/timestamp`

---

<br>

### **支持格式**

<br>

格式 | URL
---|---
json |https://api.mysubmail.com/service/timestamp.json（默认）
xml |https://api.mysubmail.com/service/timestamp.xml

<br>

### **http 请求方式**

<br>

##### **GET**

---

<br>

### **是否需要授权**

<br>

##### **否**

参阅 [API 授权和验证机制](https://api.mysubmail.com/chs/documents/developer/gbibb3)

---
<br>

### **http请求方法**

<br>

##### **无**

---

  <br>

### **返回码**

<br>

*   JSON


#### `请求成功`


```
{
      "timestamp":1414253462
}
```
---

* XML

#### `请求成功`


```
<?xml version="1.0" encoding="utf-8"?>
<xml>
     <timestamp>1414253508</timestamp>
</xml>
```

<br>

### **错误代码**

<br>

##### **无**

---