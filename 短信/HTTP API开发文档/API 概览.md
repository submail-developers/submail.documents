# API 概览

<br>

### **概览**

<br>
本文档中列出的所有 API 基础调用 URL 是 `https://api-v4.mysubmail.com` （ 如 API：`sms/xsend` 实际请求 URL `https://api-v4.mysubmail.com/sms/xsend` ） 。
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

| 接口                                                         | 用途                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [SMS/Send - 短信发送](https://www.mysubmail.com/documents/FppOR3) | 根据您提交的短信签名和内容，自动创建模板并发送               |
| [SMS/XSend - 短信模板发送](https://www.mysubmail.com/documents/OOVyh) | 提前创建短信模版，提交模板 ID 发送                           |
| [SMS/Multisend - 短信一对多发送](https://www.mysubmail.com/documents/KZjET3) | SMS/Send 的一对多发送版本                                    |
| [SMS/MultiXSend - 短信模板一对多发送](https://www.mysubmail.com/documents/eM4rY2) | SMS/XSend 的一对多发送版本                                   |
| [SMS/BatchSend - 短信批量群发](https://www.mysubmail.com/documents/AzD4Z4) | SMS/Send 的批量群发版本                                      |
| [SMS/BatchXSend - 短信批量模板群发](https://www.mysubmail.com/documents/G5KBR) | SMS/XSend 的批量群发版本                                     |
| [SMS/UnionSend - 国内短信与国际短信联合发送](https://www.mysubmail.com/documents/HSX9F4) | 结合了国内短信和国际短信的发送接口，在单一接口实现全球化短信发送功能 |
| [SMS/Template - 短信模板管理](https://www.mysubmail.com/documents/yp2in) | 获取、创建、编辑或删除您的短信模板                           |
| [SMS/Reports - 短信分析报告](https://www.mysubmail.com/documents/Hvmb02) | 实时查询短信分析报告                                         |
| [SMS/Balance - 短信余额查询](https://www.mysubmail.com/documents/AIcGd4) | 实时查询账户的短信余额                                       |
| [SMS/Log - 历史明细查询](https://www.mysubmail.com/documents/onhvw) | 实时查询已发送的短信历史明细数据                             |
| [SMS/MO - 短信上行查询](https://www.mysubmail.com/documents/YOx2m2) | 实时查询短信上行回复                                         |
| [AddressBook/SMS/Subscribe - 短信订阅](https://www.mysubmail.com/documents/2j0ej2) | 管理您的短信订阅用户                                         |
| [AddressBook/SMS/unsubscribe - 短信退订](https://www.mysubmail.com/documents/NLkEs1) | 管理您的短信退订用户                                         |
| [Service/Timestamp - UNIX 时间戳](https://www.mysubmail.com/documents/oTzAq1) | 返回服务器 UNIX 时间戳                                       |
| [Service/Status - 返回服务器状态](https://www.mysubmail.com/documents/8AV6z1) | 返回服务器状态和响应时间                                     |



------
<br>
### **创建应用**

<br>

在使用 SUBMAIL API 之前，您需要[创建 APP ID](https://www.mysubmail.com/console/sms/apps) 。

点击了解 [创建/管理 APP ID 指南 ](https://www.mysubmail.com/documents/pDGDf3)。



------

