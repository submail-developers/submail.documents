## API 概览

<br>

### **概览**

<br>
本文档中列出的所有 API 基础调用 URL 是 `https://api.mysubmail.com` （ 如 API：`message/xsend` 实际请求 URL `https://api.mysubmail.com/message/xsend` ） 。
SUBMAIL 支持 `json` (默认) 和 `xml` 格式，如果你想要 API 返回码的格式为 `xml`，请在 完整 URL 的末尾加上 `.xml`。

---

<br>

### **RESTful API**

<br>

SUBMAIL API 基于 RESTful API 风格，它具备完整的 HTTP 请求规范，多数的 SUBMAIL API 需采用 POST 方式发送请求，少量的服务类 API 使用 GET 方式获取数据。除 API 列举的请求方式外，其他方法都不被支持。

继承 RESTful API 风格，所有的 SUBMAIL API 都具有 HTTP 返回代码

*   `2XX` - 请求成功。
*   `4XX` - 请求失败。（具体出错原因，会在返回数据中标注错误代码和原因）
*   `5XX` - 服务器错误。

<br>
参阅 [HTTP 状态码](https://www.mysubmail.com/documents/mKviw)  | [API 错误代码](https://www.mysubmail.com/documents/rK2yh3)

---

<br>

### **SUBMAIL WEB API**

<br>

*   [message/send](https://www.mysubmail.com/documents/FppOR3)( 基础短信发送 API)
*   [message/xsend](https://www.mysubmail.com/documents/OOVyh) ( 增强的短信发送 API)
*   [message/multisend](https://www.mysubmail.com/documents/KZjET3) (免创建模板短信群发发送 API)
*   [message/multixsend](https://www.mysubmail.com/documents/eM4rY2) ( 短信群发发送 API)
*   [message/template](https://www.mysubmail.com/documents/yp2in)(短信模板操作API)
*   [message/balance](https://www.mysubmail.com/documents/AIcGd4)(短信余额查询API)
*   [addressbook/message/subscribe](https://www.mysubmail.com/documents/2j0ej2)（ 短信订阅 API ）
*   [addressbook/message/unsubscribe](https://www.mysubmail.com/documents/NLkEs1)（ 短信退订 API ）
*   [service/timestamp](https://www.mysubmail.com/documents/oTzAq1) ( 服务器 UNIX 时间戳 )
*   [service/status](https://www.mysubmail.com/documents/8AV6z1) （服务器状态）

------
<br>
### **创建应用**

<br>

在使用 SUBMAIL API 之前，您需要[创建 APP ID](https://www.mysubmail.com/console/sms/apps) 。

点击了解 [创建/管理 APP ID 指南 ](https://www.mysubmail.com/documents/pDGDf3)。



