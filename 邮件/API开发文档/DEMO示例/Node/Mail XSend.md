# DEMO:Mail/XSend

    var request = require('request');
    var crypto = require('crypto');
    
    var appid = "input your appid";
    var appkey = "input your appkey";
    var api = "https://api-v4.mysubmail.com/mail/xsend";


​    
​    
​    //生成加密签名
​    
    function BuildSignature(params){
        var sorted = [];
        for(var key in params) {
            sorted[sorted.length] = key;
        }
        sorted.sort();
        var tempDict = {};
        for(var i = 0; i < sorted.length; i++) {
            tempDict[sorted[i]] = params[sorted[i]];
        }
        var signStr = "";
        for(var key in tempDict) {
            signStr += key + '=' + tempDict[key] + '&amp;'; 
        }
        signStr = signStr.substring(0, signStr.length-1);
        signStr = appid + appkey + signStr + appid + appkey; 
        var md5sum = crypto.createHash('md5');
        md5sum.update(signStr);
        return md5sum.digest('hex');
    }
    
    //无加密示例
    
    request.post({
        url: api, 
        formData: {
            appid:appid,
            signature:appkey,
            project : "HQrbw1",
            from : "submail@yilinglingyi.xyz",
            to : "514******@qq.com",
            vars : JSON.stringify({
                param1 : "文本内容一",
                param2 : "文本内容二"
            }),
            links : JSON.stringify({
                link1 : "https://www.mysubmail.com/voice",
                link2 : "https://www.qq.com"
            })
        }
    }, function optionalCallback(err, httpResponse, body) {
        if (err) {
            return console.error(err);
        }
        console.log(body);
    });
    
    //加密示例
    
    request({
        uri: "https://api-v4.mysubmail.com/service/timestamp",
        method: 'GET'
    }, function(error, response, body) {
        var result = JSON.parse(body);
        var requestParams = {}
        requestParams['timestamp'] = result["timestamp"];
        requestParams['sign_type'] = "md5";
        requestParams['appid'] = appid;
        requestParams['sign_version'] = "2";
        requestParams['from'] = "submail@yilinglingyi.xyz";
        requestParams['to'] = "514******@qq.com";
        requestParams['project'] = "HQrbw1";
        requestParams['signature'] = BuildSignature(requestParams);
        requestParams['vars'] = JSON.stringify({
            param1 : "文本内容一",
            param2 : "文本内容二"
        });
        requestParams['links'] = JSON.stringify({
            link1 : "https://www.mysubmail.com/voice",
            link2 : "https://www.qq.com"
        });


​        
​        request.post({
​            url: api, 
​            formData: requestParams
​        }, function optionalCallback(err, httpResponse, body) {
​            if (err) {
​                return console.error(err);
​            }
​            console.log(body);
​        });
​    });