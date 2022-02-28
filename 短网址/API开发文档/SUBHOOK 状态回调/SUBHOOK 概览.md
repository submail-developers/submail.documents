## SUBHOOK 概览

<br>


### **概览**

<br>

`SUBHOOK` 是 API 事件推送通知接口。`SUBHOOK` 类似于一个 API 端口，但不同的是，开发者不需要请求 `SUBHOOK API`，而是设置一个或多个回调 `URL`，来接收 `SUBHOOK` 推送的通知。


要使用 `SUBHOOK`，您需要创建一个 [SUBHOOK](https://www.mysubmail.com/chs/shorturl/subhook) ，根据你的 `SUBHOOK` 配置，SUBMAIL 将会对相应的事件加入到通知推送事务队列，在你的用户接受、打开、点击或其他事件时，`SUBHOOK` 将会对你指定的回调 `URL` 中推送一条包含详细跟踪数据的通知。

`SUBHOOK` 推送事件通知时，采用 `HTTP POST` 方式，请在脚本中接收 `POST` 数据。


---



<br>

### **短网址 SUBHOOK 事件**

<br>


| 事件            | `描述`             |
| --------------- | ------------------ |
| create          | 创建短网址事件     |
| update          | 更新短网址事件     |
| delete          | 删除短网址事件     |
| create_group    | 短网址群组创建事件 |
| update_group    | 更新短网址群组     |
| delete_group    | 删除短网址群组     |
| vist            | 访问事件           |
| shorturl_accept | 短网址审核通过     |
| shorturl_reject | 短网址审核未通过   |



------