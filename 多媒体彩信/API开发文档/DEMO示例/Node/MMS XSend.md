# DEMO:MMS/XSend

    var request = require('request');
    var crypto = require('crypto');
    var appid = "input your appid";
    var appkey = "input your appkey";
    var api = "https://api-v4.mysubmail.com/message/xsend";


​    
​    
​    //生成加密签名
​    function BuildSignature(params){
​        var sorted = [];
​        for(var key in params) {
​            sorted[sorted.length] = key;
​        }
​        sorted.sort();
​        var tempDict = {};
​        for(var i = 0; i < sorted.length; i++) {
​            tempDict[sorted[i]] = params[sorted[i]];
​        }
​        var signStr = "";
​        for(var key in tempDict) {
​            signStr += key + '=' + tempDict[key] + '&amp;'; 
​        }
​        signStr = signStr.substring(0, signStr.length-1);
​        signStr = appid + appkey + signStr + appid + appkey; 
​        var md5sum = crypto.createHash('md5');
​        md5sum.update(signStr);
​        return md5sum.digest('hex');
​    }
​    
    //无加密示例
    request.post({
        url: api, 
        formData: {
            appid:appid,
            signature:appkey,
            project : "4r8Rv2",
            to : "15511111111",
            vars : JSON.stringify({
                code : "123456",
                time : "6月15日"
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
        requestParams['to'] = "155********";
        requestParams['project'] = "4r8Rv2";
        requestParams['signature'] = BuildSignature(requestParams);
        requestParams['vars'] = JSON.stringify({
                        code : "123456",
                        time : "6月15日"
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