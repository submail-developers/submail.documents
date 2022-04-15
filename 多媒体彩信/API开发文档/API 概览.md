# API 概览
<br>

### **概览**

<br>
本文档中列出的所有 API 基础调用 URL 是 `https://api-v4.mysubmail.com` （ 如 API：`mms/xsend` 实际请求 URL `https://api-v4.mysubmail.com/mms/xsend` ） 。SUBMAIL 支持 `json` (默认) 和 `xml` 格式，如果你想要 API 返回码的格式为 `xml`，请在 完整 URL 的末尾加上 `.xml`。

API URL 规则 ：

##### `https://api-v4.mysubmail.com/[model]/[function].[format]`  
<br>
SUBMAIL 还提供开发模式的 API，方便开发者调试和集成 SUBMAIL 应用

---
<br>
### **RESTful API**
<br>
SUBMAIL API 基于 RESTful API 风格，它具备完整的 HTTP 请求规范，多数的 SUBMAIL API 需采用 POST 方式发送请求，少量的服务类 API 使用 GET 方式获取数据。除 API 列举的请求方式外，其他方法都不被支持。

继承 RESTful API 风格，所有的 SUBMAIL API 都具有 HTTP 返回代码

*   `2XX` - 请求成功。
*   `4XX` - 请求失败。（具体出错原因，会在返回数据中标注错误代码和原因）
*   `5XX` - 服务器错误。

参阅 [HTTP 状态码](https://www.mysubmail.com/documents/WfSBz3)  | [API 错误代码](https://www.mysubmail.com/documents/fbaT14)

---
<br>
### **SUBMAIL WEB API**
<br>
*   [mms/xsend](https://www.mysubmail.com/documents/N6ktR) (  彩信单发API )
*   [mms/multixsend](https://www.mysubmail.com/documents/UPKTG2)( 彩信群发 API )
*   [mms/template](https://www.mysubmail.com/documents/seyAm1)(彩信模板API)



------
<br>
### **创建应用**

<br>

在使用 SUBMAIL API 之前，您需要[创建 APP ID](https://www.mysubmail.com/console/mms/apps) 。

点击了解 [创建/管理 APP ID 指南 ](https://www.mysubmail.com/documents/9tTVk)。



------
