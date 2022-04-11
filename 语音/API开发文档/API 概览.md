## API 概览

<br>

### **概览**
<br>

本文档中列出的所有 API 基础调用 URL 是 `https://api-v4.mysubmail.com` （ 如 API：`voice/xsend` 实际请求 URL `https://api-v4.mysubmail.com/voice/xsend` ） 。SUBMAIL 支持 `json` (默认) 和 `xml` 格式，如果你想要 API 返回码的格式为 `xml`，请在 完整 URL 的末尾加上 `.xml`。

API URL 规则 ：

##### `https://api-v4.mysubmail.com/[model]/[function].[format]`  
---
<br>

### **RESTful API**
<br>

SUBMAIL API 基于 RESTful API 风格，它具备完整的 HTTP 请求规范，多数的 SUBMAIL API 需采用 POST 方式发送请求，少量的服务类 API 使用 GET 方式获取数据。除 API 列举的请求方式外，其他方法都不被支持。

继承 RESTful API 风格，所有的 SUBMAIL API 都具有 HTTP 返回代码

*   `2XX` - 请求成功。
*   `4XX` - 请求失败。（具体出错原因，会在返回数据中标注错误代码和原因）
*   `5XX` - 服务器错误。

参阅 [HTTP 状态码](https://www.mysubmail.com/documents/eR0Je)  | [API 错误代码](https://www.mysubmail.com/documents/smwHw2)

---
<br>
### **SUBMAIL WEB API**
<br>

*   [voice/send](https://www.mysubmail.com/documents/meE3C1) ( 基础语音发送 API )
*   [voice/xsend](https://www.mysubmail.com/documents/KbG03)( 增强的语音发送 API )
*   [voice/multixsend](https://www.mysubmail.com/documents/FkgkM2)( 语音群发API)
*   [voice/verify](https://www.mysubmail.com/documents/yRhyQ4) (语音验证码API)
*   [balance/voice](https://www.mysubmail.com/documents/rH6iu2) （语音余额API ）

------

<br>
### **创建应用**

<br>

在使用 SUBMAIL API 之前，您需要[创建 APP ID](https://www.mysubmail.com/chs/voice/apps) 。

点击了解 [创建/管理 APP ID 指南 ](https://www.mysubmail.com/documents/u0I3M3)。



------
