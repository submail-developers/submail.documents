# DEMO:Mail/Balance

## 代码示例

    /*****************
     * 非加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     邮件-创建/管理AppID中获取
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    
    $post_data = array(
        "appid"     => $appid,
        "signature" => $appkey,
    );
    
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/balance/mail.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 1,
        CURLOPT_POSTFIELDS     => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    
    echo json_encode($output);



    /*****************
     * 加密请求 示例代码
     ******************/
    //appid参数 appkey参数在     邮件-创建/管理AppID中获取
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    
    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output, true);
    $timestamp = $output['timestamp'];
    
    $post_data = array(
        "appid"     => $appid,
        "timestamp" =>$timestamp,
        "sign_type" =>'md5',
    );
    //整理生成签名所需参数
    $temp = $post_data;
    unset($temp['content']);
    ksort($temp);
    reset($temp);
    $tempStr = "";
    foreach ($temp as $key => $value) {
        $tempStr .= $key . "=" . $value . "&amp;";
    }
    $tempStr = substr($tempStr, 0, -1);
    //生成签名
    $post_data['signature'] = md5($appid . $appkey . $tempStr . $appid . $appkey);
    
    $ch = curl_init();
    curl_setopt_array($ch, array(
        CURLOPT_URL            => 'https://api.mysubmail.com/balance/mail.json',
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_POST           => 1,
        CURLOPT_POSTFIELDS     => $post_data,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    
    echo json_encode($output);