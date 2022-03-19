# DEMO:Message/template

###示例代码
<br>

####非加密代码示例
```python
import requests
import urllib.parse

appid = 'appid'             #SUBMAIL控制台创建appid
appkey = 'appkey'           #SUBMAIL控制台获取appkey
url = 'https://api.mysubmail.com/message/template.json'


# get
def gettemplate():
    param = {
        'appid': appid,
        'signature': appkey,
        # 'template_id': 'm8hxx', #根据模板id获取单个模板信息
        'offset': '0'
    }
    res = requests.get(url, param)
    return res.json()


# post
def posttemplate():
    param = {
        'appid': appid,
        'signature': appkey,
        'sms_signature': '【xxx公司】',   #短信内容 【xxx公司】为签名，需要更换为公司或者产品名称
        'sms_content': '这是一条post测试的短信模板'
    }
    res = requests.post(url, param)
    return res.json()


# put
def puttemplate():
    param = {
        'appid': appid,
        'signature': appkey,
        'sms_signature': '【xxx公司】',
        'sms_content': '这是一条put测试的短信模板', #短信内容 【xxx公司】为签名，需要更换为公司或者产品名称
        'template_id': 'm8hxx'
    }
    res = requests.put(url, param)
    return res.json()


# delete
def deletetemplate():
    param = {
        'appid': appid,
        'signature': appkey,
        'template_id': 'm8hxx'
    }
    paramstr = urllib.parse.urlencode(param)

    res = requests.delete(url, data=paramstr)
    return res.json()


print(gettemplate())
# print(posttemplate())
# print(puttemplate())
# print(deletetemplate())

```

####加密代码示例
```python
import hashlib
import requests
import urllib.parse

appid = 'appid'     #SUBMAIL控制台创建appid
appkey = 'appkey'    #SUBMAIL控制台获取appkey
url = 'https://api.mysubmail.com/message/template.json'
sign_type = 'md5'
sign_version = '2'

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


# get
def gettemplate():
    param = {
        'appid': appid,
        'sign_type': sign_type,
        'timestamp': gettimestamp(),
        # 'template_id': 'm8hxx'  #根据模板id获取单个模板信息
    }
    signarute = getmd5(param)
    param['signature'] = signarute
    param['offset'] = '0'
    res = requests.get(url, param)
    return res.json()


# post
def posttemplate():
    param = {
        'appid': appid,
        'sign_type': sign_type,
        'timestamp': gettimestamp(),
        'sign_version': sign_version
    }
    signarute = getmd5(param)
    param['sms_signature'] = '【xxx公司】'   #短信内容 【xxx公司】为签名，需要更换为公司或者产品名称
    param['sms_content'] = '这是一条post测试的短信模板'
    param['signature'] = signarute
    res = requests.post(url, param)
    return res.json()


# put
def puttemplate():
    param = {
        'appid': appid,
        'sign_type': sign_type,
        'timestamp': gettimestamp(),
        'sign_version': sign_version,
        'template_id': 'm8hxx'
    }
    signarute = getmd5(param)
    param['sms_signature'] = '【xxx公司】'  #短信内容 【xxx公司】为签名，需要更换为公司或者产品名称
    param['sms_content'] = '这是一条put测试的短信模板'
    param['signature'] = signarute
    res = requests.put(url, param)
    return res.json()


# delete
def deletetemplate():
    param = {
        'appid': appid,
        'sign_type': sign_type,
        'timestamp': gettimestamp(),
        'template_id': 'm8hxx'
    }
    signarute = getmd5(param)
    param['signature'] = signarute
    paramstr = urllib.parse.urlencode(param)
    res = requests.delete(url, data=paramstr)
    return res.json()


print(gettemplate())
# print(posttemplate())
# print(puttemplate())
# print(deletetemplate())

```