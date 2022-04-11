# DEMO: SMS/multixsend

### 示例代码

<br>

#### 非加密代码示例

```python
import requests
import json

appid = 'appid'      #SUBMAIL控制台创建appid
appkey = 'appkey'    #SUBMAIL控制台获取appkey
project = '模板id'
url = 'https://api-v4.mysubmail.com/sms/multixsend.json'

# 模板带有变量
multi = [{'to': '186xxxxxxxx', 'vars': {'name': '123456', 'time': '20min'}},
         {'to': '153xxxxxxxx', 'vars': {'name': '888888', 'time': '20min'}}]

# 模板不带变量
# multi = [{'to': '186xxxxxxxx'}, {'to': '153xxxxxxxx'}]
header = {"Content-type": "application/json"}
param = {
    'appid': appid,
    'signature': appkey,
    'project': project,
    'multi': json.dumps(multi)
}
res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())

```



#### 加密代码示例

```python
import hashlib
import requests
import json

appid = 'appid'     #SUBMAIL控制台创建appid
appkey = 'appkey'   #SUBMAIL控制台获取appkey
project = '模板id'

sign_version = '2'
sign_type = 'md5'

url = 'https://api-v4.mysubmail.com/sms/multixsend.json'

# 模板带有变量
multi = [{'to': '186xxxxxxxx', 'vars': {'name': 'test', 'time': '2021-1-1'}},
         {'to': '153xxxxxxxx', 'vars': {'name': 'test2', 'time': '2021-1-2'}}]
# 模板不带变量
# multi = [{'to': '186xxxxxxxx'}, {'to': '153xxxxxxxx'}]
header = {"Content-type": "application/json"}

# 获取时间戳
def gettimestamp():
    res = requests.get('https://api-v4.mysubmail.com/service/timestamp').json()
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
    'sign_version': sign_version,
    'sign_type': sign_type,
    'project': project,
    'timestamp': gettimestamp()
}

param["signature"] = getmd5(param)
param["multi"] = json.dumps(multi)
res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())

```