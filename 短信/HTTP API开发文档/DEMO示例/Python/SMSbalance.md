# DEMO: Balance/SMS - 短信余额查询

### 示例代码

<br>

#### 非加密代码示例

```python

import requests
import json

appid = 'appid'     #SUBMAIL控制台创建appid
appkey = 'appkey'   #SUBMAIL控制台获取appkey

url = 'https://api-v4.mysubmail.com/balance/sms.json'

header = {"Content-type": "application/json"}
params = {
    'appid': appid,
    'signature': appkey,
}
res = requests.post(url, data=json.dumps(params), headers=header)
print(res.json())

```

#### 非加密代码示例

```python
import hashlib
import requests
import json

appid = 'appid'     #SUBMAIL控制台创建appid
appkey = 'appkey'   #SUBMAIL控制台获取appkey

sign_type = 'md5'
url = 'https://api-v4.mysubmail.com/balance/sms.json'

header = {"Content-type": "application/json"}

# 获取时间戳
def gettimestamp():
    res = requests.get('httpsapi-v4.mysubmail.comcom/service/timestamp').json()
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
    'timestamp': gettimestamp(),
    'sign_type': sign_type
}
signarute = getmd5(param)
param['signature'] = signarute
res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())

```