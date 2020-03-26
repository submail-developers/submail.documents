
## 配置 DNS 解析

<br>

### **概览**

<br>

配置域名的 DNS 解析，是校验发件人身份和反垃圾邮件的核心技术手段。通过配置适当的 DNS 解析，能让收件服务器确定发件人身份，极大地提高邮件送达率。在使用 SUBMAIL 邮件服务之前，你需要配置你的域名 DNS 解析。

完整的 DNS 解析包含3个部分，完成域名验证解析和 SPF 解析是必选解析，DKIM 公匙解析部分是可选的（配置 DKIM 签名公匙，将提高你的邮件送达率）。

在你完成域名验证解析和 SPF 解析之前，或在 SUBMAIL 验证你的解析生效前，你将不能使用此域发送邮件。视域名服务商的不同，你的域名生效时间可能会有所延迟，一般在 6 -24 小时内生效解析，有些域名服务商则更快。

---

<br>

### **添加域名**

<br>

在配置 DNS 之前，请前往[域名配置](https://www.mysubmail.com/chs/mail/domains)页面添加你的域名，在添加你的域名文本框内填写你的域名，并点击“添加发送域名”按钮。

![](https://www.mysubmail.com/libraries/zh_cn/images/eg/dns-2.png)

---

<br>

### **域名验证解析**

<br>

要开始配置域名验证解析，请按以下步骤进行：

1.  请前往[域名配置](https://www.mysubmail.com/chs/mail/domains)页面，查看配置域名验证项的验证框代码，并复制此代码。
2.  请前往你的域名服务商页面，增加一条主机名为 submail 的 TXT 记录，粘贴并保存以上验证框内的代码。

请注意：如果您使用的是二级域名，如：mail.yourdomain.com 请将主机名填写为 submail.mail

![](https://www.mysubmail.com/libraries/zh_cn/images/eg/dns-1.png)

---

<br>

### **配置 SPF**

<br>

SPF 值

```
v=spf1 include:spf.submail.cn ~all
```

请前往你的域名服务商页面，增加一条 TXT 记录,并将主机名与您配置的域名记录保持一致，粘贴并保存以上 SPF 值。

**请注意**：
```
如果您使用的是根域名，请在主机名处填写 "@"符号，如果您已经配置了一条 SPF 记录，如：v=spf1 include:spf.163.com ~all ，请将 include:spf.submail.cn 插入此SPF记录中，在 v=spf1 include:spf.163.com 和 ~all 之间插入，并前后保持1个空格，即 v=spf1 include:spf.163.com  include:spf.submail.cn ~all
```


> 例：例如您的发送域名是 example.com，请在你的域名服务页面上，增加一条与此域名一致的 TXT 记录,将以上文本框中的 SPF 值粘贴并保存，如果您的域名已包含一条 SPF 记录，请将此条 SPF 记录中插入 include:spf.submail.cn 。

---

<br>

### **配置 DKIM**

<br>

DKIM 公匙：


```
v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDkHxTUZYMpZbLa+uzS8FQlbftDomp+51efjTY6yoffZaq9Zxjwk4HvuuONdRqwe6MBtC4YYUSDrgUyquCeIGnhNl5ZCesoiZyCghPvaM5vQANjMyxnYlBBzQOuMWD0ociCpkmCQB/qQvHdr1HZGivb5auk2hH5fT39jt5rOY8QywIDAQAB;
```


请在你的域名服务商处增加一条主机名为 submail._domainkey 的 TXT 记录。

> 例：例如您的发送域名是 example.com，请在你的域名服务页面上，增加一条主机名为 submail.\_domainkey. 的 TXT 记录,并将以上文本框内的 DKIM 值粘贴并保存 （即 submail.\_domainkey.example.com 的 TXT 解析）。

某些域名服务商可能需要您对此记录中包含的“;”号进行转义，请使用下面的转义后的 DKIM 公匙

转义后的 DKIM 公匙：


```
v=DKIM1\\; k=rsa\\; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDkHxTUZYMpZbLa+uzS8FQlbftDomp+51efjTY6yoffZaq9Zxjwk4HvuuONdRqwe6MBtC4YYUSDrgUyquCeIGnhNl5ZCesoiZyCghPvaM5vQANjMyxnYlBBzQOuMWD0ociCpkmCQB/qQvHdr1HZGivb5auk2hH5fT39jt5rOY8QywIDAQAB\\;
```
---

<br>

### **测试 DNS 配置**

<br>

SUBMAIL 自动域名检查队列每5分钟检查你的域名 DNS 配置，你也可以手动测试你的 DNS 是否生效，请前往[域名配置](https://www.mysubmail.com/chs/account/settings#/mail/domainConfigs)页面，点击测试 DNS 配置按钮，进行测试。

![](https://www.mysubmail.com/libraries/zh_cn/images/eg/dns-3.png)