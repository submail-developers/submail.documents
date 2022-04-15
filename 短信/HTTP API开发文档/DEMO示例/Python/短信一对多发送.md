# DEMO: SMS/MultiSend - 短信一对多发送

### 示例代码

<br>

#### 非加密代码示例

```python
import requests
import json

appid = 'appid'     # SUBMAIL控制台创建appid
appkey = 'appkey'   # SUBMAIL控制台获取appkey

# 模板不带变量
# content = '【XXX公司】这是一个测试的模板'       #短信内容 【xxx公司】为短信签名，需要更换为公司或者产品名称
# multi = [{'to': '186xxxxxxxx'}, {'to': '153xxxxxxxx'}]

# 模板带有变量
content = '【XXX公司】这是一个来自 @var(name)的测试模板 时间@var(time)'   #短信内容 【xxx公司】为短信签名，需要更换为公司或者产品名称
multi = [{'to': '186xxxxxxxx', 'vars': {'name': 'test1', 'time': '2021-1-1'}},
         {'to': '153xxxxxxxx', 'vars': {'name': 'test2', 'time': '2021-1-1'}}]

url = 'https://api-v4.mysubmail.com/sms/multisend.json'

header = {"Content-type": "application/json"}
param = {
    'appid': appid,
    'signature': appkey,
    'content': content,
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

appid = 'appid'     # SUBMAIL控制台创建appid
appkey = 'appkey'   # SUBMAIL控制台获取appkey

sign_version = '2'
sign_type = 'md5'

# 模板不带变量
# content = '【xxx公司】这是一个测试的模板'                    #短信内容 【xxx公司】为短信签名，需要更换为公司或者产品名称
# multi = [{'to': '186xxxxxxxx'}, {'to': '153xxxxxxxx'}]

# 模板带有变量
content = '【xxx公司】这是一个来自 @var(name)的测试模板 时间@var(time)'   #短信内容 【xxx公司】为短信签名，需要更换为公司或者产品名称
multi = [{'to': '186xxxxxxxx', 'vars': {'name': 'test1', 'time': '2020-1-1'}},
         {'to': '153xxxxxxxx', 'vars': {'name': 'test2', 'time': '2020-1-1'}}]

url = 'https://api-v4.mysubmail.com/sms/multisend.json'


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
    'sign_version': sign_version,
    'sign_type': sign_type,
    'timestamp': gettimestamp()
}

param["signature"] = getmd5(param)
param["multi"] = json.dumps(multi)
param["content"] = content
res = requests.post(url, data=json.dumps(param), headers=header)
print(res.json())


```