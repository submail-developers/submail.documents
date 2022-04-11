# DEMEO:InternationalSMS/Verifyphonenumber 

    var request = require('request');
    var crypto = require('crypto');
    var api = "https://api-v4.mysubmail.com/service/verifyphonenumber";


​    
​    //示例
​    request.post({
​        url: api, 
​        formData: {
​            to : "+998********"
​        }
​    }, function optionalCallback(err, httpResponse, body) {
​        if (err) {
​            return console.error(err);
​        }
​        console.log(body);
​    });