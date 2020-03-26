## 语音 SUBHOOK 事件

<br>

### **请求 request**

<br>


events | request
---|---
address | 此联系人的手机号码
app | 应用 ID
send_id|该条短信的唯一发送标识，可在 API 请求时获取
timestamp|事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名）
token|32 位随机字符串
signature|数字签名

#### 推送示例


```
{
"events":"request",
"address":"138xxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```

---

<br>

### **语音发送成功delievered**

<br>


events | delivered
---|---
address | 此联系人的手机号码
app | 应用 ID
send_id|该条短信的唯一发送标识，可在 API 请求时获取
hold|通话持续时间（秒）
answer_time|接听时间（时间戳）
hangup_time|挂断时间（时间戳）
timestamp|事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名）
token|32 位随机字符串
signature|数字签名

#### 推送示例


```
{
"events":"delivered",
"address":"138xxxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"hold":20,
"answer_time":1415213855,
"answer_time":1415233725,
"timestamp":1415235639,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```
---

<br>

### **语音发送失败 dropped**

<br>


events | dropped
---|---
address | 此联系人的手机号码
app | 应用 ID
send_id|该条语音的唯一发送标识，可在 API 请求时获取
tag|自定义标签
timestamp|事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名）
token|32 位随机字符串
signature|数字签名

#### 推送示例


```
{
"events":"dropped",
"address":"138xxxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```
---
<br>

### **语音正在呼叫中sending**

<br>


events | sending
---|---
address | 此联系人的手机号码
app | 应用 ID
send_id|该条短信的唯一发送标识，可在 API 请求时获取
timestamp|事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名）
token|32 位随机字符串
signature|数字签名

#### 推送示例


```
{
"events":"sending",
"address":"138xxxxxxxx",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```
---

<br>

### **语音按键反馈 signal**

<br>


events | signal
---|---
address | 此联系人的手机号码
app | 应用 ID
signal|交互按键
send_id|该条短信的唯一发送标识，可在 API 请求时获取
timestamp|事件触发时间（此时间戳为此事件本身的触发时间，不参与计算签名）
token|32 位随机字符串
signature|数字签名

#### 推送示例


```
{
"events":"signal",
"address":"138xxxxxxxx",
"signal":"1",
"send_id":"093c0a7df143c087d6cba9cdf0cf3738",
"app":xxxxxx,
"timestamp":1415014855,
"token":"067ef7e2f286a9a56eabb07dc9657852",
"signature":"a70d09a9345adfdd353d34a505dac4ca"
}
```
---
