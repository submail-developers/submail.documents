# Factor/ocr_idcard_img - 身份证OCR识别(带抠图版本)
<br>
<?php

    /*****************
     * 示例代码
     ******************/
    //appid参数 appkey参数在     身份认证-创建/管理AppID中获取
    $appid      = '6***3';                                                                  //appid参数
    $appkey     = '5d****************************58';                                       //appkey参数
    $timestamp  = time();                                                                   //获取当前时间戳
    $file_type  = 'file';                                                                   //图片的格式(file | base64)，选择 file 那边 base64 参数就可为空，反之亦然
    $file       = curl_file_create('***/***/***.png');                              //图片文件  支持 png、jpeg、jpg
    $base64     = 'data:image/......';                                                      //图片的base64编码
    $ocr_type   = 1 ;                                                                       //身份证正反面  0正面 1反面
    
    $temp_data = array(
        'appkey'    => $appkey ,
        'timestamp' => $timestamp,
    );
    //生成签名
    ksort($temp_data);
    reset($temp_data);
    $signature = hash('sha256', http_build_query($temp_data));
    
    $post_data = array(
        'appid'     => $appid,
        'timestamp' => $timestamp,
        'signature' => $signature,
        'file_type' => $file_type,
        'file'      => $file,
        'base64'    => $base64,
        'ocr_type'  => $ocr_type,
    );
    
    $curl = curl_init();
    curl_setopt_array($curl, array(
        CURLOPT_URL             => "https://tpa.mysubmail.com/factor/ocr_idcard_img",
        CURLOPT_RETURNTRANSFER  => true,
        CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST   => "POST",
        CURLOPT_POSTFIELDS      => $post_data,
    ));
    $response = curl_exec($curl);
    $err = curl_error($curl);
    curl_close($curl);
    
    if ($err) {
        echo "cURL Error #:" . $err;
    } else {
        echo $response;
    }