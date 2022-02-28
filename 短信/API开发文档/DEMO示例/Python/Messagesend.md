# DEMO:Message/send

###示例代码
<br>

####非加密代码示例
```python
import requests
import json

appid = 'appid'                             #SUBMAIL控制台创建appid
appkey = 'appkey'                           #SUBMAIL控制台获取appkey
content = '【xxx公司】这是一条测试的短信'       #短信内容 【xxx公司】为签名，需要更换为公司或者产品名称
to = '186xxxxxxxx'                          #手机号码

url = 'https://api.mysubmail.com/message/send.json'

header = {"Content-type": "application/json"}
param = {
    'appid': appid,
    'signature': appkey,
    'content': content,
    'to': to
}
res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())

```

####加密代码示例
```python
import hashlib
import requests
import json

appid = 'appid'                             #SUBMAIL控制台创建appid
appkey = 'appkey'                           #SUBMAIL控制台获取appkey
content = '【xxx公司】这是一条测试的短信'       #短信内容 【xxx公司】为签名，需要更换为公司或者产品名称
to = '186xxxxxxxx'                          #手机号码

sign_version = '2'
sign_type = 'md5'

url = 'https://api.mysubmail.com/message/send.json'

header = {"Content-type": "application/json"}


# 获取时间戳
def gettimestamp():
    res = requests.get('https://api.mysubmail.com/service/timestamp').json()
    timestamp = str(res['timestamp'])
    return timestamp


# 参数md5计算
def getmd5(params):
    signStr = ''
    for key in sorted(params):
        signStr += key + '=' + params[key] + '&amp;'
    signStr = signStr[:-1]
    signStr = appid + appkey + signStr + appid + appkey
    print(signStr)

    m = hashlib.md5()
    b = signStr.encode(encoding='utf-8')
    m.update(b)
    return m.hexdigest()


param = {
    'appid': appid,
    'to': to,
    'sign_version': sign_version,
    'sign_type': sign_type,
    'timestamp': gettimestamp()
}
param["signature"] = getmd5(param)
param["content"] = content

res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())

```
