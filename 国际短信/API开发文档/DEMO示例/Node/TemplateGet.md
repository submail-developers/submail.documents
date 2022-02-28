#DEMO:Template/Get

	var request = require('request');
	var crypto = require('crypto');
	
	var appid = "input your appid";
	var appkey = "input your appkey";
	var api = "https://api.mysubmail.com/internationalsms/template";


​    
​    
    //生成加密签名
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
    request({
        url: api+"?appid="+appid+"&amp;signature="+appkey+"&amp;template_id=jHYY33", 
        method: 'GET'
    }, function optionalCallback(err, httpResponse, body) {
        if (err) {
            return console.error(err);
        }
        console.log(body);
    });
    
    //加密示例
    
    request({
        uri: "https://api.mysubmail.com/service/timestamp",
        method: 'GET'
    }, function(error, response, body) {
        var result = JSON.parse(body);
        var requestParams = {}
        requestParams['timestamp'] = result["timestamp"];
        requestParams['sign_type'] = "md5";
        requestParams['appid'] = appid;
        requestParams['template_id'] = "toCnd3";
        requestParams['signature'] = BuildSignature(requestParams);
        var paramsEncode = "";
        for(key in requestParams){
            paramsEncode += key+"="+requestParams[key]+"&amp;"
        }
        paramsEncode = paramsEncode.substring(0, paramsEncode.length-1);
        request({
            url: api+"?"+paramsEncode, 
            method: 'GET'
        }, function optionalCallback(err, httpResponse, body) {
            if (err) {
                return console.error(err);
            }
            console.log(body);
        });
    });


​    