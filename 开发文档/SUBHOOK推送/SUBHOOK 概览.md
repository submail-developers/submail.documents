# SUBHOOK 概览

<br>

### **概览**

<br>

`SUBHOOK` 是邮件和短信 API 事件推送通知接口。`SUBHOOK` 类似于一个 API 端口，但不同的是，开发者不需要请求 `SUBHOOK API`，而是设置一个或多个回调 `URL`，来接收 `SUBHOOK` 推送的通知。


要使用 `SUBHOOK`，你需要在 [DEVELOPER](https://www.mysubmail.com/chs/developer) -\> [设置](https://www.mysubmail.com/chs/account/settings#/developer) -\> [SUBHOOK](https://www.mysubmail.com/chs/account/settings#/developer/subhooks) 页面创建一个 SUBHOOK，根据你的 `SUBHOOK` 配置，SUBMAIL 将会对相应的事件加入到通知推送事务队列，在你的用户接受、打开、点击或其他事件时，`SUBHOOK` 将会对你指定的回调 `URL` 中推送一条包含详细跟踪数据的通知。

`SUBHOOK` 推送事件通知时，采用 `HTTP POST` 方式，请在脚本中接收 `POST` 数据。

---

<br>

### **邮件 SUBHOOK 事件**

<br>


事件 | 描述
---|---
resquest | 发送请求被接收
dropped |邮件丢失或发送失败，当推送邮件 dropped 事件时， SUBHOOK 将会同时推送 dropped 原因  
delivered| 发送成功 
bounced|邮件被弹回
opened|邮件被阅读 
clicked|邮件中的超链接被点击
subscribe|订阅事件
unsubscribed|邮件退订事件
change_subscribe|用户电邮电子更改事件
marked_as_spam|邮件被标记为垃圾邮件
report_as_spam|邮件被举报为垃圾邮件
rejected|邮件被拒收

---

<br>

### **短信 SUBHOOK 事件**

<br>

事件| 描述
---|---
resquest|发送请求被接收
delivered|发送成功
dropped|发送失败
sending|正在发送
mo|短信上行（指用户回复和上行）
unkown|未知状态（指无法从网关获取短信回执状态）
template_accept|短信模板审核通过
template_reject|短信模板审核未通过

---

<br>

### **语音 SUBHOOK 事件**

<br>

事件| 描述
---|---
resquest|发送请求被接收
delivered|发送成功
dropped|发送失败
sending|正在发送
signal|按键反馈

---

<br>

### **国际短信 SUBHOOK 事件**

<br>

事件| 描述
---|---
resquest|发送请求被接收
delivered|发送成功
dropped|发送失败
sending|正在发送

---



<br>

### **彩信 SUBHOOK 事件**

<br>

事件| 描述
---|---
resquest|发送请求被接收
delivered|发送成功
dropped|发送失败
sending|正在发送
mo|短信上行（指用户回复和上行）
unkown|未知状态（指无法从网关获取短信回执状态）
template_accept|短信模板审核通过
template_reject|短信模板审核未通过
