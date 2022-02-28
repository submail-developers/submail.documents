## 配置 DNS 解析

<br>

### **概览**

<br>

配置域名的 DNS 解析，是校验发件人身份和反垃圾邮件的核心技术手段。通过配置适当的 DNS 解析，能让收件服务器确定发件人身份，极大地提高邮件送达率。

在使用 SUBMAIL 邮件服务之前，您需要配置您的域名 DNS 解析。

在您完成域名验证解析和 SPF 解析之前，或在 SUBMAIL 验证你的解析生效前，您将不能使用此域发送邮件。

视域名服务商的不同，您的域名生效时间可能会有所延迟，一般在 6 -24 小时内生效解析，有些域名服务商则更快。

---
 <br>
### 新增域名
 <br>
进入[配置发信域名](https://www.mysubmail.com/console/mail/domain "配置发信域名")页面，点击 ![](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/08ec8a95e42fd4a4f3c8c2c5616c54fb.png) -》输入您的域名-》验证并保存。

如图所示：

![](https://z3.ax1x.com/2021/06/09/2yPmQO.gif)
<br>
在域名管理平台（本文档以阿里云为例）将域名验证、SPF 解析、MX 解析绑定到您的发信域名：点击解析设置-》添加记录-》选择记录类型-》复制粘贴主机名和记录值-》点击确认。

如图所示：

**域名验证**

![](https://z3.ax1x.com/2021/06/09/2yFsMT.gif)
<br>
**SPF 解析**

![](https://z3.ax1x.com/2021/06/09/2yFvWt.gif)

如果您的域名已包含一条 SPF 记录，请在 SPF 记录中插入 include:spf.submail.cn 。
<br>
**MX 解析**

![](https://z3.ax1x.com/2021/06/09/2yk9OS.gif)

------
<br>
### 验证 DNS 解析
 <br>
操作完成后，点击 ![“验证 DNS 解析”](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/975a82004caaadd9949ee74eed45be2d.png "“验证 DNS 解析”")，全部显示 ![](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/aa29f1321b363b760e71de3226ad395c.png) 即成功配置发信域名。

如图所示：

![](https://libraries.mysubmail.com/public/99040a5a4bb73c0f8ab0495dae84a27f/images/b45b68f82a4f0f431c175cefeff758c7.gif)

------
