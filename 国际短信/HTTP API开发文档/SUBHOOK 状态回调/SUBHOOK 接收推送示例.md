## SUBHOOK 接收推送示例

<br>

### **示例**

<br>

使用 PHP 脚本将 SUBHOOK 通知保存到文件

<br>

#### 代码示例

<br>


```php
<?php
    $subhook = fopen('/log/subhook.log', 'a+');
    if ($subhook){
    fwrite($subhook, date('Y-m-d H:i:s').print_r($_POST,true));
    fclose($subhook);
    }
```

<br>

#### 比对数字签名示例

<br>


```php
<?php
    $key='my_subhook_key';
    $token=$_POST['token'];
    $signature=md5($token.$key);
    if($signature == $_POST['signature']){
        $subhook = fopen('/log/subhook.log', 'a+');
        if ($subhook){
            fwrite($subhook, date('Y-m-d H:i:s').print_r($_POST,true));
            fclose($subhook);
        }
    }
```

------