<?php
    /*****************
     * 示例代码
     ******************/
    //appid参数 appkey参数在     身份认证-创建/管理AppID中获取
    $appid      = '6***3';                                                                  //appid参数
    $appkey     = '5d****************************58';                                       //appkey参数
    $timestamp  = time();                                                                   //获取当前时间戳
    $mobile     = '152********';                                                            //待验证用户 电话号码

    $temp_data = array(
        'appkey'    => $appkey ,
        'timestamp' => $timestamp,
        'mobile'    => $mobile,
    );
    
    //生成签名
    ksort($temp_data);
    reset($temp_data);
    $signature = hash('sha256', http_build_query($temp_data));
    
    $post_data = array(
        'appid'     => $appid,
        'timestamp' => $timestamp,
        'signature' => $signature,
        'mobile'    => $mobile,
    );
    
    $curl = curl_init();
    curl_setopt_array($curl, array(
        CURLOPT_URL             => "https://tpa.mysubmail.com/factor/mobile_online",
        CURLOPT_RETURNTRANSFER  => true,
        CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST   => "POST",
        CURLOPT_POSTFIELDS      => http_build_query($post_data),
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded"),
    ));
    $response = curl_exec($curl);
    $err = curl_error($curl);
    curl_close($curl);
    
    if ($err) {
        echo "cURL Error #:" . $err;
    } else {
        echo $response;
    }