##  使用 `SMTP` 协议发送邮件

<br>

### **概览**

<br>

如果你将要整合 SUBMAIL 的服务到你现有的应用、网站或移动 APP，使用 `SMTP` 是最为简单和快捷。你只需修改你的用户名、密码和 `SMTP` 配置即可完成集成。

SUBMAIL 还提供强大的 `SMTP API` 帮助你更灵活的控制你的发送请求，如添加联系人、将地址簿添加至发送队列，或使用文本变量或超链接变量来灵活地控制邮件内容，甚至在 `SMTP API` 中使用模板。请参阅[SMTP API](https://www.mysubmail.com/chs/documents/developer/fsBPJ2)。

---
<br>

### **SMTP 配置**

<br>


服务器 |<主> cloud.mysubmail.com|<备> cloud.submail.cn
---|---|---
端口| 25 |
用户名|你的应用ID |  请参阅 [创建应用](https://www.mysubmail.com/chs/documents/developer/b1hC31)
密码 | 你的应用密匙 | 请参阅 [创建应用](https://www.mysubmail.com/chs/documents/developer/b1hC31)

---

<br>

### **内置变量**

<br>

变量 | 描述 |类型
---|---|---
[@subscribe()](https://www.mysubmail.com/chs/documents/developer/T9Naw) | 订阅变量 |超链接变量
[@subscribe(link)](https://www.mysubmail.com/chs/documents/developer/T9Naw) | 订阅变量 | 文本变量
[@unsubscribe()](https://www.mysubmail.com/chs/documents/developer/SlR5s2) | 退订变量 |超链接变量
[@unsubscribe(change)](https://www.mysubmail.com/chs/documents/developer/XhWnq2) | 变更电邮地址变量 | 超链接变量
[@recipient()](https://www.mysubmail.com/chs/documents/developer/asB7v) | 收件人变量 |文本变量
[@recipient(name)](https://www.mysubmail.com/chs/documents/developer/asB7v) | 收件人变量 |文本变量
[@webversion()](https://www.mysubmail.com/chs/documents/developer/pluMT3) | 网页版本变量 |超链接变量
[@webversion(link)](https://www.mysubmail.com/chs/documents/developer/pluMT3) | 网页版本变量 | 文本变量
[@date()](https://www.mysubmail.com/chs/documents/developer/Iqu011) | 日期与时间变量 |文本变请参阅[日期与时间](https://www.mysubmail.com/chs/documents/developer/Iqu011)

<br>

### **参考文档**

<br>

##### [[Ruby] Mail 类使用代码示例](https://www.mysubmail.com/chs/blog/view/10)

##### [[C#] SMTP 发送邮件指引​ (.net)](https://www.mysubmail.com/chs/blog/view/12)