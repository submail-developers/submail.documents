# DEMO:Factor/Mobile

     /*代码块一*/
    var request = require('request');
    var crypto = require('crypto');
    var appid = "input your appid";
    var appkey = "input your appkey";
    var api = "https://tpa.mysubmail.com/factor/mobile";
    
    /*代码块二*/
    //示例代码
    request({
        uri: "https://api.mysubmail.com/service/timestamp",
        method: 'GET'
    }, function(error, response, body) {
        var result = JSON.parse(body);
        var requestParams = {}
        requestParams['timestamp'] = result["timestamp"];
        requestParams['appid'] = appid;
        requestParams['mobile'] = "152********";
        requestParams['name'] = "张三";
    
        //生成签名
        var sign_str = "appkey="+appkey+"&amp;mobile="+requestParams['mobile']+"&amp;name="+requestParams['name']+"×tamp="+requestParams['timestamp'];
        requestParams['signature'] = crypto.createHash('sha256').update(encodeURI(sign_str)).digest("hex");
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