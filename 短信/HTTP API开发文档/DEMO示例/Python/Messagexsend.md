# DEMO:Message/xsend

###示例代码
<br>

####非加密代码示例
```python

import requests
import json

appid = 'appid'  # SUBMAIL控制台创建appid
appkey = 'appkey'  # SUBMAIL控制台获取appkey
project = '模板id'  # SUBMAIL控制台创建模板 获取模板id
to = '186xxxxxxxx'  # 手机号码

url = 'https://api.mysubmail.com/message/xsend.json'

header = {"Content-type": "application/json"}
vars = {
    'code': '123456',    #code为参数名 和模板中参数名一致
    'time': '20min'      #time为参数名 和模板中参数名一致
}
param = {
    'appid': appid,
    'signature': appkey,
    'project': project,
    'to': to,
    'vars': json.dumps(vars)
}
res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())

```


####加密代码示例
```python

import hashlib
import requests
import json

appid = 'appid'  # SUBMAIL控制台创建appid
appkey = 'appkey'  # SUBMAIL控制台获取appkey
project = '模板id'  # SUBMAIL控制台创建模板 获取模板id
to = '186xxxxxxxx'  # 手机号码
sign_version = '2'
sign_type = 'md5'

url = 'https://api.mysubmail.com/message/xsend.json'
vars = {
    'code': '123456',    #code为参数名 和模板中参数名一致
    'time': '20分钟'      #time为参数名 和模板中参数名一致
}

header = {"Content-type": "application/json"}

# 获取时间戳
def gettimestamp():
    res = requests.get('https://api.mysubmail.com/service/timestamp').json()
    timestamp = str(res['timestamp'])
    return timestamp

# 参数md5计算
def getmd5(param):
    signStr = ''
    for key in sorted(param):
        signStr += key + '=' + param[key] + '&amp;'
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
    'project': project,
    'sign_version': sign_version,
    'sign_type': sign_type,
    'timestamp': gettimestamp()

}

param["signature"] = getmd5(param)
param["vars"] = json.dumps(vars)

res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())


```