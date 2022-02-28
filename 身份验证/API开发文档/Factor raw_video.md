# 活体检测     
### API: Factor/raw_video
### 概览
`Factor/raw_video`是submail的活体检测API，检查用户拍摄的视频是否为活体。
***
### URL
```
<主> http://tpa.mysubmail.com/factor/raw_video  
<备> https://tpa.mysubmail.com/factor/raw_video
```
***
### http请求方式
| 请求方式  | content-type设置                                             |
| --------- | ------------------------------------------------------------ |
| http post | multipart/form-data、x-www-form-urlencoded、application/json |
***
### 返回参数格式
`jsonString`
***
### 请求参数说明
| 参数       | 是否必填 | 类型   | 类型                                                         |
| ---------- | -------- | ------ | ------------------------------------------------------------ |
| appid      | 是       | string | 在 SUBMAIL 身份认证服务中创建并且认证通过的应用 ID           |
| timestamp  | 是       | string | UNIX 时间戳                                                  |
| signature  | 是       | string | 签名，详细规则看下方介绍                                     |
| motions    | 是       | string | 用户动作序列，BLINK 眨眼;MOUTH 张嘴; NOD 点头; YAW 摇头      |
| complexity | 是       | string | 活体检测通过的难易程度，默认为 0， 0:简单模式;1: 正常模式;2:困难模式;3:地狱模式 |
| image_flag | 是       | string | 是否需要返回照片，Y/N                                        |
| video      | 是       | file   | 视频文件                                                     |
***
### signature创建规则
1. 请将以下参数按照字段升序（A-Z）排列    appkey 、timestamp
2. 创建签名字符串 ：以"key=value" + "&amp;"（连接符）+ "key=value" 的方式连接所有参数
3. 创建签名：拼接签名字符串示例string = "appkey=xxxx×tamp=xxxxxxxxxx"，然后使用sha256(string)创建签名  
   注：中文需要使用urlencode处理后再参与创建签名
***
### 响应消息
```
API请求失败
{
    'status'  : 'error' ,                                          // 状态描述
    'send_id' : 'ee05d1635db847a2bf3c8317434539d6',                // API流水号
    'code'    : 1201 ,                                             // API返回的状态码    详情查看 API错误代码与描述  文档
    'msg'     : 'Incorrect APP ID.' ,                              // API返回的描述、  
}
```
```
API请求成功
{
    'status'  : 'success' ,                                       // 状态描述
    'send_id' : 'ee05d1635db847a2bf3c8317434539d6',               // API流水号
    'result' : {
         'pass' => true                                           //验证是否通过 true/false        
         'featureImage' => ...                                    //image_flag为N返回空，为Y返回图片的base64编码
    };
}
```