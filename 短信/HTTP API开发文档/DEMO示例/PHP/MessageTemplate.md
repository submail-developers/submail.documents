# DEMO:Message/Template

<br>


## 代码示列


```
<?php
    /*****************
     * 非加密请求 示例代码
     ******************/
    //---------------------------------get  获取短信模板数据-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //模板ID   短信-创建/管理短信模板中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $project = "F***U";                                                             //短信模板ID

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'template_id'   => $project
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => "https://api.mysubmail.com/message/template?".http_build_query($post_data),
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);




    //---------------------------------post  创建短信模板-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //生成模板如下
    //  【短信模板签名】您的验证码是@var(code)，请在@var(time)内输入。
    $appid = '6***3';                                                                   //appid参数
    $appkey = '5d****************************58';                                       //appkey参数
    $title = '短信模板标题';                                                              //短信模板标题
    $signature = '短信模板签名';                                                          //短信模板签名
    $content = '您的验证码是@var(code)，请在@var(time)内输入。';                             //短信正文

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'sms_title'     => $title,
        'sms_signature' => $signature,
        'sms_content'   => $content
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/message/template',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 1,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------put  更新短信模板-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //模板ID   短信-创建/管理短信模板中获得
    //生成模板如下
    //  【短信模板签名】您的验证码是@var(code)，请在@var(time)内输入。
    $appid = '6***3';                                                                   //appid参数
    $appkey = '5d****************************58';                                       //appkey参数
    $title = '短信模板标题';                                                              //短信模板标题
    $signature = '短信模板签名';                                                          //短信模板签名
    $content = '您的验证码是@var(code)，请在@var(time)内输入。';                             //短信正文
    $template_id = 'F***U';                                                             //短信模板ID

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'sms_title'     => $title,
        'sms_signature' => $signature,
        'template_id'   => $template_id,
        'sms_content'   => $content
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/message/template',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'PUT',
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------delete 删除模板-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //模板ID   短信-创建/管理短信模板中获得
    $appid = '6***3';                                                                   //appid参数
    $appkey = '5d****************************58';                                       //appkey参数
    $template_id = 'F***U';                                                             //短信模板ID

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'template_id'   => $template_id,
    );

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL => 'https://api.mysubmail.com/message/template' ,
        CURLOPT_RETURNTRANSFER => 1,
        CURLOPT_CUSTOMREQUEST => 'DELETE',
        CURLOPT_POSTFIELDS => http_build_query($post_data),
        CURLOPT_HTTPHEADER => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    /*****************
     * 加密请求 示例代码
     ******************/
    //---------------------------------get  获取短信模板数据-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //模板ID   短信-创建/管理短信模板中获得
    $appid = '6***3';                                                               //appid参数
    $appkey = '5d****************************58';                                   //appkey参数
    $template_id = "F***U";                                                         //短信模板ID

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'template_id'   => $template_id,
        'sign_type'     => 'md5',
        'timestamp'     => $timestamp
    );

    $temp = $post_data;
    ksort($temp);
    reset($temp);
    unset($temp['signature']);
    $str = "";
    foreach ($temp as $key => $value) {
        $str.=$key."=".$value."&amp;";
    }
    $str = substr($str,0,-1);
    $post_data['signature'] = md5($appid.$appkey.$str.$appid.$appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => "https://api.mysubmail.com/message/template?".http_build_query($post_data),
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);


    //---------------------------------post  创建短信模板-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //生成模板如下
    //  【短信模板签名】您的验证码是@var(code)，请在@var(time)内输入。
    $appid = '6***3';                                                                   //appid参数
    $appkey = '5d****************************58';                                       //appkey参数
    $title = '短信模板标题';                                                              //短信模板标题
    $signature = '短信模板签名';                                                          //短信模板签名
    $content = '您的验证码是@var(code)，请在@var(time)内输入。';                             //短信正文

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/service/timestamp.json',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'sms_title'     => $title,
        'sms_signature' => $signature ,
        'sms_content'   => $content ,
        'sign_type'     => 'md5',
        'sign_version'  => 2,
        'timestamp'     => $timestamp,
    );

    $temp = $post_data;
    unset($temp['signature']);
    unset($temp['sms_title']);
    unset($temp['sms_signature']);
    unset($temp['sms_subject']);
    unset($temp['sms_content']);
    ksort($temp);
    reset($temp);
    $str = "";
    foreach ($temp as $key => $value) {
        $str.=$key."=".$value."&amp;";
    }
    $str = substr($str,0,-1);
    //生成签名
    $post_data['signature'] = md5($appid.$appkey.$str.$appid.$appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/message/template',
        CURLOPT_RETURNTRANSFER  => 1,
        CURLOPT_POST            => 1 ,
        CURLOPT_POSTFIELDS      => $post_data
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------put  更新短信模板-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //模板ID   短信-创建/管理短信模板中获得
    //生成模板如下
    //  【短信模板签名】您的验证码是@var(code)，请在@var(time)内输入。
    $appid = '6***3';                                                                   //appid参数
    $appkey = '5d****************************58';                                       //appkey参数
    $title = '短信模板标题';                                                              //短信模板标题
    $signature = '短信模板签名';                                                          //短信模板签名
    $content = '您的验证码是@var(code)，请在@var(time)内输入。';                             //短信正文
    $template_id = 'F***U';                                                             //短信模板ID

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/service/timestamp.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'sms_title'     => $title,
        'sms_signature' => $signature,
        'template_id'   => $template_id,
        'sms_content'   => $content,
        'sign_type'     => 'md5',
        'sign_version'  => 2,
        'timestamp'     => $timestamp
    );

    $temp = $post_data;
    unset($temp['signature']);
    unset($temp['sms_title']);
    unset($temp['sms_signature']);
    unset($temp['sms_subject']);
    unset($temp['sms_content']);
    ksort($temp);
    reset($temp);
    $str = "";
    foreach ($temp as $key => $value) {
        $str.=$key."=".$value."&amp;";
    }
    $str = substr($str,0,-1);
    //生成签名
    $post_data['signature'] = md5($appid.$appkey.$str.$appid.$appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/message/template',
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'PUT',
        CURLOPT_POSTFIELDS      => http_build_query($post_data),
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);



    //---------------------------------delete 删除模板-------------------------------------
    //appid参数 appkey参数在     短信-创建/管理AppID中获取
    //模板ID   短信-创建/管理短信模板中获得
    $appid = '6***3';                                                                   //appid参数
    $appkey = '5d****************************58';                                       //appkey参数
    $template_id = 'F***U';                                                             //短信模板ID

    //通过接口获取时间戳
    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/service/timestamp.json' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_POST            => 0 ,
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);
    $timestamp = $output['timestamp'];

    $post_data = array(
        'appid'         => $appid,
        'signature'     => $appkey,
        'template_id'   => $template_id,
        'sign_type'     => 'md5',
        'timestamp'     => $timestamp
    );

    $temp = $post_data;
    ksort($temp);
    reset($temp);
    unset($temp['signature']);
    $str = "";
    foreach ($temp as $key => $value) {
        $str.=$key."=".$value."&amp;";
    }
    $str = substr($str,0,-1);
    //生成签名
    $post_data['signature'] = md5($appid.$appkey.$str.$appid.$appkey);

    $ch = curl_init();
    curl_setopt_array($ch , array(
        CURLOPT_URL             => 'https://api.mysubmail.com/message/template' ,
        CURLOPT_RETURNTRANSFER  => 1 ,
        CURLOPT_CUSTOMREQUEST   => 'DELETE' ,
        CURLOPT_POSTFIELDS      => http_build_query($post_data) ,
        CURLOPT_HTTPHEADER      => array("Content-Type: application/x-www-form-urlencoded")
    ));
    $output = curl_exec($ch);
    curl_close($ch);
    $output = json_decode($output,true);

    print_r($output);


```