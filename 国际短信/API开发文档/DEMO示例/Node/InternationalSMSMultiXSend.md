#DEMEO:InternationalSMS/MultiXSend

	var request = require('request');
	var crypto = require('crypto');
	var appid = "input your appid";
	var appkey = "input your appkey";
	var api = "https://api.mysubmail.com/internationalsms/multixsend";


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
    
    //multi参数示例
    var multi = [{
            to :"+221********",
            vars : {
            code : "123456",
            time : "6月15日"
            }
        },{
            to :"+221********",
            vars : {
                code : "123456",
                time : "6月15日"
            }
        },{
            to :"+221********",
            vars : {
                code : "123456",
                time : "6月15日"
            }
        }]
    
    //无加密示例
    request.post({
        url: api, 
        formData: {
            appid:appid,
            signature:appkey,
            project : "9vFM31",
            multi : JSON.stringify(multi)
        }
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
        requestParams['sign_version'] = "2";
        requestParams['project'] = "9vFM31";
        requestParams['signature'] = BuildSignature(requestParams);
        requestParams['multi'] = JSON.stringify(multi);
        request.post({
            url: api, 
            formData: requestParams
        }, function optionalCallback(err, httpResponse, body) {
            if (err) {
                return console.error(err);
            }
            console.log(body);
        });
    });


​    