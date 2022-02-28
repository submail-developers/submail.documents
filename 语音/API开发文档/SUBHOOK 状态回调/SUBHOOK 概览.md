## SUBHOOK 概览


<br>

### **概览**

<br>

`SUBHOOK` 是 API 事件推送通知接口。`SUBHOOK` 类似于一个 API 端口，但不同的是，开发者不需要请求 `SUBHOOK API`，而是设置一个或多个回调 `URL`，来接收 `SUBHOOK` 推送的通知。


要使用 `SUBHOOK`，您需要创建一个 [SUBHOOK](https://www.mysubmail.com/console/voice/subhook) ，根据你的 `SUBHOOK` 配置，SUBMAIL 将会对相应的事件加入到通知推送事务队列，在你的用户接受、打开、点击或其他事件时，`SUBHOOK` 将会对你指定的回调 `URL` 中推送一条包含详细跟踪数据的通知。

`SUBHOOK` 推送事件通知时，采用 `HTTP POST` 方式，请在脚本中接收 `POST` 数据。

参阅：[SUBHOOK 状态推送](https://www.mysubmail.com/documents/VfWMU2)

---

<br>

### **语音 SUBHOOK 事件**

<br>

| 事件        | 描述           |
| ----------- | -------------- |
| `request`   | 发送请求被接收 |
| `delivered` | 发送成功       |
| `dropped`   | 发送失败       |
| `sending`   | 正在发送       |
| `signal`    | 按键反馈       |

---