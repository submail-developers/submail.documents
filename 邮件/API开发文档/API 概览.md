## API 概览
<br>

### **概览**

<br>
本文档中列出的所有 API 基础调用 URL 是 `https://api.mysubmail.com` （ 如 API：`mail/xsend` 实际请求 URL `https://api.mysubmail.com/mail/xsend` ） 。
SUBMAIL 支持 `json` (默认) 和 `xml` 格式，如果你想要 API 返回码的格式为 `xml`，请在 完整 URL 的末尾加上 `.xml`。

API URL 规则 ：
##### `<主> https://api.mysubmail.com/[model]/[function].[format]`  
##### `<备> https://api.submail.cn/[model]/[function].[format]`  



---

<br>

### **RESTful API**
<br>

SUBMAIL API 基于 RESTful API 风格，它具备完整的 HTTP 请求规范，多数的 SUBMAIL API 需采用 POST 方式发送请求，少量的服务类 API 使用 GET 方式获取数据。除 API 列举的请求方式外，其他方法都不被支持。

继承 RESTful API 风格，所有的 SUBMAIL API 都具有 HTTP 返回代码

*   `2XX` - 请求成功。
*   `4XX` - 请求失败。（具体出错原因，会在返回数据中标注错误代码和原因）
*   `5XX` - 服务器错误。

参阅 [HTTP 状态码](https://www.mysubmail.com/documents/MmTlW3)  | [API 错误代码](https://www.mysubmail.com/documents/i22PE4)

---
<br>

### **SUBMAIL WEB API**
<br>

*   [mail/send](https://www.mysubmail.com/documents/4MfRT2) ( 基础邮件发送 API )
*   [mail/xsend](https://www.mysubmail.com/documents/Vu8Qh3)( 增强的邮件发送 API )
*   [addressbook/mail/subscribe](https://www.mysubmail.com/documents/dyNlf) （ 邮件订阅 API ）
*   [addressbook/mail/unsubscribe](https://www.mysubmail.com/documents/E2YD33) （ 邮件退订 API ）
*   [service/timestamp](https://www.mysubmail.com/documents/wwBcQ4) ( 服务器 UNIX 时间戳 )
*   [service/status](https://www.mysubmail.com/documents/5Oyvq2) （服务器状态）

---

<br>

### **SMTP**

<br>

*   [SMTP](https://www.mysubmail.com/documents/J2pHa)
*   [SMTP API](https://www.mysubmail.com/documents/2cpYo2)

------
<br>
### **创建应用**

<br>

在使用 SUBMAIL API 之前，您需要[创建 AppID](https://www.mysubmail.com/console/mail/apps) 。

点击了解 [创建/管理 AppID 指南 ](https://www.mysubmail.com/documents/TmFfr2)。

------
