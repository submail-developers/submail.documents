## API: Mail/XSend

<br>

### **概览**

<br>

`mail/xsend` 是邮件 API 的升级版本。与 `mail/send` API 一样，`mail/xsend` 提供强大的邮件发送功能，区别于 `mail/send` API，`mail/xsend` 无需提交 html 源码或邮件文本内容，甚至无需提交邮件标题或发件人，仅需提交你在 SUBMAIL MAIL 中创建的邮件项目模板ID，并可以使用变量动态的控制每封邮件的内容。 
<br>
项目模版ID：

![](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/4afe538cb023890cfc2555bb0cbf6ebc.png)

了解如何使用[文本变量](https://www.mysubmail.com/documents/TOYJC1)和[超链接变量](https://www.mysubmail.com/documents/uDRmO1)。
<br>
使用 `mail/xsend` API 你将可以使用 SUBMAIL 编辑器 高效、可视化地创建你的触发邮件，无需管理邮件中的一切静态资源或编码（如图片，html 代码兼容等问题），甚至移动设备兼容问题，SUBMAIL 编辑器 已为你做好了一切。

---

<br>

### **URL**

<br>

##### `https://api-v4.mysubmail.com/mail/xsend`

---
<br>

### **支持格式**

<br>

| 格式   | URL                                                    |
| ------ | ------------------------------------------------------ |
| `json` | `https://api-v4.mysubmail.com/mail/xsend.json`（默认） |
| `xml`  | `https://api-v4.mysubmail.com/mail/xsend.xml`          |

---

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

##### 参阅 [API 授权和验证机制](https://www.mysubmail.com/documents/Xi096)

---

<br>

### **请求参数**

<br>

| 参数           | 类型          | 必需/可选 | 默认     | 描述                                                         |
| -------------- | ------------- | --------- | -------- | ------------------------------------------------------------ |
| `appid`        | `string`      | `必需`    | 无       | 在 SUBMAIL 应用集成中创建的邮件应用ID                        |
| `to`           | `string`      | `必需`    | 无       | 收件人地址 (多个联系人用半角“,”隔开：e.g. `"leo <leo@submail.cn>, <info@mysubmail.com>, service@submail.cn"`,<br>SUBMAIL 支持完整的 RFC 822 收件人标准，请确保您的邮件地址的有效性。请参见 维基百科 [EMAIL ADDRESS RFC822 文档](https://en.wikipedia.org/wiki/Email_address)) |
| `from`         | `e-mail`      | `可选`    | 无       | 发件人地址 ，标准的发件人地址 e.g. leo@submail.cn            |
| `from_name`    | `string`      | `可选`    | 无       | 发件人称呼，显示名称 e.g. Submail （20个字符以内）           |
| `reply`        | `e-mail`      | `可选`    | 无       | 回复地址，标准的回复邮件地址 e.g. leo@submail.cn             |
| `cc`           | `string`      | `可选`    | 无       | 抄送地址 <br>*(多个抄送地址请用 “ , ”半角逗号区分，请将抄送联系人控制在 5 个以内)。* |
| `bcc`          | `string`      | `可选`    | 无       | 密送地址<br>*(多个密送地址请用 “ ,”半角逗号或区分，请将密送联系人控制在 5 个以内)。* |
| `subject`      | `string`      | `可选`    | 无       | 邮件标题（100个字符以内,`不提交邮件标题，此标题将读取项目标题`) |
| `project`      | `string`      | `必须`    | 无       | 项目标记(ID)在SUBMAIL>MAIL>项目中，（如果您的账户已开通应用集成，提交并验证了的开发者身份后）你将可以查看你所创建的邮件项目标记。<br>此参数将根据你提交的标记来确定该发送的项目。 |
| `vars`         | `json string` | `可选`    | 无       | 使用文本变量动态控制邮件中的文本，<br>参阅 [了解如何创建和使用文本变量](https://www.mysubmail.com/documents/TOYJC1) |
| `links`        | `json string` | `可选`    | 无       | 使用超链接变量动态控制邮件中的超链接，<br>参阅 [了解如何创建和使用超链接变量](https://www.mysubmail.com/documents/uDRmO1) |
| `headers`      | `json string` | `可选`    | 无       | 自定义 EMAIL 头文件指令，headers 是一个标准的 JSON 字符串，headers 参数可以让开发者在 EMAIL 的标头部分插入自定义指令（500个字符以内）。<br>如：` {"X-Accept-Language": "zh-cn", "X-Priority":"3","X-Mailer": "My Application"}` |
| `asynchronous` | `string`      | `可选`    | `false`  | 异步选项，该值设为 true 时启用异步发送模式                   |
| `tag`          | `string`      | `可选`    | 无       | 自定义标签功能，该标签可用作SUBHOOK追踪（32 个字符以内）     |
| `timestamp`    | `UNIX 时间戳` | `可选`    | 无       | 参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/Xi096)  \>  `Timestamp` UNIX 时间戳 |
| `sign_type`    | `string`      | `可选`    | `normal` | API 授权模式（  `md5 or sha1 or normal` ）<br>参阅 [API 授权与验证机制](https://www.mysubmail.com/documents/Xi096)  \>  授权和验证方式 |
| `sign_version` | `string`      | `可选`    | 无       | signature加密计算方式(当sign_version传2时，vars，links参数不参与加密计算) |
| `signature`    | `string`      | `必需`    | 无       | 应用密匙 *或* 数字签名                                       |

<br>
注意：


```
Submail 保留 x-submail-smtp-api 指令，请务必不要在邮件标头中使用此指令

自定义的 EMAIL headers 指令通常以字母 X- 开头，请将此规范应用到你的指令

vars,  links 和 headers 参数要求严格的 JSON 格式，以下是将参数转换为 JSON 格式的注意事项

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

#### 发送一封测试邮件
<br>

##### POST URL

```
https://api-v4.mysubmail.com/mail/xsend.json
```

<br>
##### POST Data


```
appid=your_app_id
&amp;to=leo <leo>
&amp;project=ThJBE4
&amp;signature=your_app_key
```


<br>
##### 返回


```
{
    "status":"success",
    "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---



<br>

#### 发送一封测试邮件，多收件人


<br>

##### POST URL

```
https://api-v4.mysubmail.com/mail/xsend.json
```

<br>

##### POST DATA


```
appid=your_app_id
&amp;to=leo <leo>,retro@submail.cn
&amp;project=ThJBE4
&amp;signature=your_app_key
```

<br>
##### 返回


```
{
    "status":"success",
    "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---



<br>
#### 使用地址簿发送一封测试邮件

<br>

##### POST URL

```
https://api-v4.mysubmail.com/mail/xsend.json
```


<br>
##### POST DATA


```
appid=your_app_id
&amp;addressbook=subscribe
&amp;project=ThJBE4
&amp;signature=your_app_key
```

<br>
##### 返回


```
{
    "status":"success",
    "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---



<br>
#### 使用 `CURL` 发送一封测试邮件


<br>

##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;to=leo<leo> &amp;project=ThJBE4&amp;signature=your_app_key' https://api-v4.mysubmail.com/mail/xsend.json
```

<br>
##### 返回


```
{
      "status":"success",
      "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---


<br>

#### 使用 `CURL` 发送一封测试邮件,多收件人

<br>
##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;to=leo<leo> ,retro@submail.cn&amp;&amp;project=ThJBE4&amp;signature=your_app_key' https://api-v4.mysubmail.com/mail/xsend.json
```

<br>
##### 返回


```
{
      "status":"success",
      "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---


<br>
#### 使用 `CURL` 发送一封测试邮件,使用地址簿中的收件人


<br>
##### 发送 CURL

```
curl -d 'appid=your_app_id&amp;addressbook=subscribe&amp;&amp;project=ThJBE4&amp;signature=your_app_key' https://api-v4.mysubmail.com/mail/xsend.json
```

<br>
##### 返回


```
{
      "status":"success",
      "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
       }
     ]
}
```

---


<br>
#### 返回值

<br>


##### 请求成功


```
{
      "status":"success",
      "return": [
       {
         "send_id": "HstDN4",
         "to": "eg@eg.com"
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

---



<br>

### **错误代码**

<br>

##### 参阅 [API 错误代码](https://www.mysubmail.com/documents/i22PE4)

------
