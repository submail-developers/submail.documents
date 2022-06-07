# API 概览

<br>

### **概览**

<br>

本文档中列出的所有 API 基础调用 URL 是 `https://api-v4.mysubmail.com` （ 如 API：`internationalsms/xsend` 实际请求 URL `https://api-v4.mysubmail.com/internationalsms/xsend` ） 。SUBMAIL 支持 `json` (默认) 和 `xml` 格式，如果你想要 API 返回码的格式为 `xml`，请在 完整 URL 的末尾加上 `.xml`。

API URL 规则 ：

##### `https://api-v4.mysubmail.com/[model]/[function].[format]`  
<br>
SUBMAIL 还提供开发模式的 API，方便开发者调试和集成 SUBMAIL 应用。

---
<br>
### **RESTful API**
<br>
SUBMAIL API 基于 RESTful API 风格，它具备完整的 HTTP 请求规范，多数的 SUBMAIL API 需采用 POST 方式发送请求，少量的服务类 API 使用 GET 方式获取数据。除 API 列举的请求方式外，其他方法都不被支持。

继承 RESTful API 风格，所有的 SUBMAIL API 都具有 HTTP 返回代码

*   `2XX` - 请求成功。
*   `4XX` - 请求失败。（具体出错原因，会在返回数据中标注错误代码和原因）
*   `5XX` - 服务器错误。

参阅 [HTTP 状态码](https://www.mysubmail.com/documents/uPcMX3)  | [API 错误代码](https://www.mysubmail.com/documents/wBDvw1)

---
<br>
###  **SUBMAIL WEB API**
<br>

| 接口                                                         | 用途                                           |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [InternationalSMS/Send - 国际短信发送](https://www.mysubmail.com/documents/3UQA3) | 根据您提交的短信签名和内容，自动创建模板并发送 |
| [InternationalSMS/XSend - 国际短信模板发送](https://www.mysubmail.com/documents/87QTB2) | 提前创建短信模版，提交模板 ID 发送             |
| [InternationalSMS/MultiXSend - 国际短信模板一对多发送](https://www.mysubmail.com/documents/B70hy) | InternationalSMS/XSend 的一对多发送版本        |
| [InternationalSMS/BatchSend - 国际短信批量群发](https://www.mysubmail.com/documents/yD46O) | InternationalSMS/Send 的批量群发版本           |
| [InternationalSMS/Template - 国际短信模板管理](https://www.mysubmail.com/documents/DIPbL4) | 获取、创建、编辑或删除您的国际短信模板         |
| [Balance/InternationalSMS - 国际短信余额查询](https://www.mysubmail.com/documents/gjRXN2) | 实时查询账户的国际短信余额                     |
| [Service/Verifyphonenumber - 国际短信归属地国家查询](https://www.mysubmail.com/documents/OQCN) | 查询国际手机号码的归属地国家等信息             |
| [Service/Timestamp - UNIX 时间戳](https://www.mysubmail.com/documents/mmoHq) | 返回服务器 UNIX 时间戳                         |
| [Service/Status - 返回服务器状态](https://www.mysubmail.com/documents/c4Gqg2) | 返回服务器状态和响应时间                       |

  

---

<br>

### **创建应用**

<br>

在使用 SUBMAIL API 之前，您需要[创建 APP ID](https://www.mysubmail.com/console/intersms/apps) 。

点击了解 [创建/管理 APP ID 指南 ](https://www.mysubmail.com/documents/VRcCH1)。

---
