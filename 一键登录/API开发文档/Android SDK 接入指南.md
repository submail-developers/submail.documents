## Android SDK 接入指南

<br>

### 概览

<br>

   此文档为Andorid一键登陆SDK1.0.1版本开发文档。[点击下载SDK以及Demo](https://github.com/dev-submail/OneLogin_Android_SDK_AND_DEMO.git "点击下载SDK以及Demo")

------

<br>

### 名词解释

<br>

*   初始化：一次有效，通过getLoginAccessCode方法完成，会进⾏⽹络流量请求。预取号失败返回错误信息，业务方可跳转到其他登录方式；预取号成功后，在回调函数中返回已开启蜂窝流量的运营商类型，脱敏手机号（188****8888）和accessCode，可缩短拉起登录授权页面的时间。建议在判断当前⽤户处于未登录状态，且在执行拉起登录授权页前调用（1-3s），已登录状态⽤户请不要调⽤该⽅法。

*   Token:⽤来和后台置换完整⼿机号（18888888888）。⼀次有效。通过getLoginToken方法获取。必须在授权页（见授权页规范）中调用。Token是业务方实现登录的必备参数。

*   授权页：取token必须在授权页中调用，各运营商对授权页样式要求有所不同（见授权页规范）。

------

<br>

### 一键登录能力时序表

<br>

![](https://libraries.mysubmail.com/public/e6c6783fa0e6ca8ddd61385a5ad92ad6/images/72157b4853a73a5dbd06ead15f7c36f4.png)

<br>

### 准备工作

<br>

**前置条件:**

- 本SDK必须打开蜂窝数据流量并且手机操作系统给予应用蜂窝数据权限才能使用
- ⽀持中国移动3/4G、联通3/4G、电信4G的取号能⼒，在3G⽹络下时延会更⾼
- ⽀持单数据⽹络/数据⽹络与WiFi⽹络双开，不⽀持单WiFi⽹络
- 对于双卡⼿机，只对当前流量卡取号，双卡均未开数据流量SDK将会返回错误码
- SDK请求过程需要消耗用户少量数据流量（国外漫游时可能会产生额外的费用）
- 移动，联通，电信需要自定义授权界面，该界面的全路径activity类名需要提前提供给平台支撑方预先配置。请仔细阅读<授权页面规范>一节，提前做出配置
- Android端需要向平台支撑方提供5种配置：appid，appkey，应用包名，应用签名，电信的授权页面类全名。
- 一键免密登录登录接口必须在授权页面中调用
- 主线程中调用各接口。


---

<br>

### 接入流程

<br>
   前往([SUBMAIL控制台](https://www.mysubmail.com/chs/ocl/apps))申请appid和appkey，并按要求填写申请所需资料。

------

<br>

### 开发流程

<br>

#### 1.下载SDK以及demo代码

请在您账户[一键登录](https://www.mysubmail.com/chs/ocl)控制台下下载SDK包以及代码示列。


<br>

#### 2.搭建开发环境

- Android Studio版本需要使用3.0以上<br>
- 集成submail_sdk_1.0.1.aar, allnetloginsdk_2.3.5_release.aar，CMCCSSOSDK_5.7.1_release.aar，unicom_login_android_v4.1.0.aar，CTAccount_sdk_api_v3.7.0_all.aar到项目的libs目录下，并在gradle中做以下配置：


```
compileOptions { 
 sourceCompatibility = '1.8' 
 targetCompatibility = '1.8'
 }
													
repositories {
 flatDir { dirs 'libs' }
}

```

```
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation(name: 'submail_sdk_1.0.1', ext: 'aar')
    implementation(name: 'CMCCSSOSDK_5.7.1_release', ext: 'aar')
    implementation(name: 'allnetloginsdk_2.3.5_release', ext: 'aar')
    implementation(name: 'CTAccount_sdk_api_v3.7.0_all', ext: 'aar')
    implementation(name: 'unicom_login_android_v4.1.0', ext: 'aar')
    implementation 'com.alibaba:fastjson:1.2.58'
    implementation 'com.squareup.okhttp3:okhttp:3.6.0'
```

- 在gradle中配置signingConfig签名信息，并在编译apk时，使用该签名。
  将app包名和签名提供给SUBMAIL审核。
  平台需要校验app包名和签名，请务必提供准确信息。信息更改后，需要重新向SUBMAIL重新申请应用能力。
  可使用命令：keytool -v -list -keystore 你的应用签名文件.jks获取签名的MD5信息。

- 在AndroidManifest.xml配置必要的权限支持，并在代码中做动态权限申请。

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_SETTINGS" />
<uses-permission android:name="android.permission.GET_TASKS" />

```

- 配置Activity

```
    <activity
            android:name="com.submail.onelogin.sdk.ui.OneLoginPageActivity"
            android:configChanges="orientation|keyboardHidden|screenSize" />
        <activity
            android:name="com.submail.onelogin.sdk.ui.AgreeMentActivity"
            android:configChanges="orientation|keyboardHidden|screenSize" />

        <activity
            android:name="com.cmic.sso.sdk.activity.LoginAuthActivity"
            android:configChanges="orientation|keyboardHidden|screenSize" />
```

- 配置混淆策略

```
#ct
-keep class cn.com.chinatelecom.account.api.**{*;}
# cmcc中国移动一键免密登录
-dontwarn com.cmic.sso.sdk.**
-keep class com.cmic.sso.sdk.**{*;}
#cu 小沃科技免密登录sdk
-dontwarn com.unicom.xiaowo.account.shield.**
-keep class com.unicom.xiaowo.account.shield.**{*;}
# sdk
-dontwarn com.submail.onelogin.sdk.**
-keep class com.submail.onelogin.sdk.**{*;}
-dontwarn com.cmcc.allnetlogin.**
-keep class com.cmcc.allnetlogin.client.**{*;}
-keep class com.cmcc.allnetlogin.model.**{*;}
-keep class com.cmcc.allnetlogin.http.**{*;}
-keep class com.cmcc.allnetlogin.utils.**{*;}
-keep class org.apache.commons.codec1.**{*;}

```

<br>

------

<br>

### SDK方法及说明

<br>

####  初始化请求（init方法）

本方法用于初始化SDK，SDK完成网络请求并根据运营商类型自动选择配置信息。

<br>

##### 方法示列

```
public static void init(Context context, String appid, String appkey, SubCallback subCallback)
```

<br>

##### 参数说明

| 参数     | 是否必选 | 类型               | 说明                                                         |
| -------- | -------- | ------------------ | ------------------------------------------------------------ |
| context  | 是       | Context            | 上下文                                                       |
| appid    | 是       | String             | Submail一键登录应用id                                        |
| appkey   | 是       | String             | Submail一键登录应用秘钥                                      |
| callback | 是       | SubSDK.SubCallback | SubCallback为回调监听器，需要调用者自己实现；void onResult(boolean isSuccess, String result)是该接口中唯一的抽象方法 |

<br>

##### 响应参数

**SubCallback 响应参数：**

| 参数     | 类型    | 说明           |
| -------- | ------- | -------------- |
| isSucces | boolean | 是否初始化成功 |
| result   | String  | 初始化结果描述 |

<br>

##### 代码示列


```
 SubSDK.init(mCtx, appid, appkey, new SubCallback() {
                    @Override
                    public void onResult(boolean var1, final String var2) {
                        Logger.d("测试结果：", var1 + "，" + var2);
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                Toast.makeText(mCtx, var2, Toast.LENGTH_SHORT).show();
                            }
                        });
                    }
                });
```

<br>

#### 获取AccessCode（getLoginAccessCode方法）

<br>


##### 方法原型

```
public static void getLoginAccessCode(Context ctx, SubCallback callback) 

```

<br>

##### 参数说明

| 参数     | 是否必选 | 类型               | 说明                                                         |
| -------- | -------- | ------------------ | ------------------------------------------------------------ |
| context  | 是       | Context            | 上下文                                                       |
| callback | 是       | SubSDK.SubCallback | SubCallback为回调监听器，需要调用者自己实现；void onResult(boolean isSuccess, String result)是该接口中唯一的抽象方法 |

<br>

##### 响应参数

**SubCallback 响应参数：**

| 参数     | 类型    | 说明                   |
| -------- | ------- | ---------------------- |
| isSucces | boolean | 是否获取accesscode成功 |
| result   | String  | 获取accesscode结果描述 |

<br>

**callback成功时返回参数：**


```
   {
      "accessCode":"nmf12db627f7a44f268d56813bfdf89ee4",
      "expiredTime":"3600",
      "operator":3,
      "others":{"gwAuth":"1306","reqId":"24bd961b4f47380bb5cbd5cded57a041"},
      "phone":"199****5361"
   }
```

<br>

**Tips：**

```
       operator：可选值。0-未知运营商
                         1-移动
                         2-联通
                         3-电信  
        others ：字段存放各运营商特殊字段              
```

<br>

##### 代码示列

```
  SubSDK.getLoginAccessCode(mCtx, new SubCallback() {
                    @Override
                    public void onResult(boolean isSuccess, String result) {
                        if(isSuccess){
                            //获取AccessCode成功处理逻辑，需要客户自行实现
                        }
                       
                    }
                });
```

<br>

#### 获取Token（getLoginToken方法）

<br>


##### 方法原型

```
public static void getLoginToken(Context ctx, LoginPageConfig loginPageConfig， SubCallback callback) 

public static void getLoginToken(Context ctx, AuthThemeConfig authThemeConfig， SubCallback callback) 

```

<br>

##### 参数说明

| 参数            | 是否必选 | 类型               | 说明                                                         |
| --------------- | -------- | ------------------ | ------------------------------------------------------------ |
| context         | 是       | Context            | 上下文                                                       |
| authThemeConfig | 可选     | AuthThemeConfig    | 移动授权页配置参数                                           |
| loginPageConfig | 可选     | LoginPageConfig    | 联通/电信授权页配置参数                                      |
| callback        | 是       | SubSDK.SubCallback | SubCallback为回调监听器，需要调用者自己实现；void onResult(boolean isSuccess, String result)是该接口中唯一的抽象方法 |

<br>

##### 响应参数

**SubCallback 响应参数：**

| 参数     | 类型    | 说明              |
| -------- | ------- | ----------------- |
| isSucces | boolean | 是否获取token成功 |
| result   | String  | 获取token结果描述 |

<br>

**callback成功时返回参数：**


```
  {
      "operator":3,
      "others":{
                "phone":
                "199****5361",
                "gwAuth":"5079",
                "expiredTime":"3600",
                "reqId":"c8 bf5081e5ef3b6492a46c139e540937"
               },
      "token":"nm8eff132bb0414c63a08390cb976c2287"
      
  }
```

<br>

**Tips：**
    

```
       operator：可选值。0-未知运营商
                         1-移动
                         2-联通
                         3-电信
                         
        others ：字段存放各运营商特殊字段              
```

<br>

##### 代码示列

```
      public void getLoginToken(){
            SubSDK.getLoginToken(mCtx, loginPageConfig,new SubCallback() {
                        @Override
                        public void onResult(boolean isSuccess, String result) {
                            if(isSuccess){
                            //获取token成功处理逻辑，需要客户自行实现
                          }
                        }
                    });
        }
```

**Ps：由于依赖的移动内置授权页的原因，当前为移动网络运营商的时候，需要单独配置授权页。**

<br>

#### 获取手机号码

     为了提高安全性，不建议在app端直接获取手机号码明文，需要开发者自行实现。通过获取的token值对接获取手机号码API,即可以换取手机号码，具体请参考获取手机号码API文档。

<br>

------

<br>

### SDK其他方法说明

<br>

#### 1.获取运营商类型


##### 方法原型

```
 public static int getNetworkType(Context context)；
```

<br>

##### 参数说明

| 参数    | 是否必选 | 类型    | 说明   |
| ------- | -------- | ------- | ------ |
| context | 是       | Context | 上下文 |

<br>

##### 返回参数


| 参数 | 类型 | 说明                               |
| ---- | ---- | ---------------------------------- |
| type | int  | 0-未知网络，1-移动，2-联通，3-电信 |

<br>


#### 2.打印日志

##### 方法原型

```
  public static void isShowLog(boolean isShowLog)

```

<br>

##### 参数说明

| 参数      | 是否必选 | 类型    | 说明         |
| --------- | -------- | ------- | ------------ |
| isShowLog | 是       | boolean | 是否打印日志 |


<br>

---

<br>

### 授权页规范

<br>


#### 中国移动授权页规范

```
  为了确保用户在登录过程中将手机号码信息授权给开发者使用的知情权，一键登录需要开发者提供授权页登录页面 
供用户授权确认。开发者在调用授权登录方法前，必须弹出授权页，明确告知用户当前操作会将用户的本机号码信 
息传递给应用。 
  为了确保用户在登录过程中将手机号码信息授权给开发者使用的知情权，一键登录需要开发者提供授权页登录页面 
供用户授权确认。开发者在调用授权登录方法前，必须弹出授权页，明确告知用户当前操作会将用户的本机号码信 
息传递给应用。 

```

<br>

##### 授权页规范


![](https://libraries.mysubmail.com/public/e6c6783fa0e6ca8ddd61385a5ad92ad6/images/a6309c322b4feac29a59f1364d7cfeba.png)



<br>

**注意：**

```
1、开发者不得通过任何技术手段，破解授权页，或将授权页面的号码栏、隐私栏、品牌露出内容隐
藏、覆盖。
2、登录按钮文字描述必须包含“登录”或“注册”等文字，不得诱导用户授权。
3、对于接入移动认证SDK并上线的应用，我方会对上线的应用授权页面做审查，如果有出现未按要求
弹出或设计授权页面的，将关闭应用的认证取号服务。 

```

<br>

##### 配置授权页

开发者可以通过在调用getLoginToken方法shi传入AuthThemeConfig参数进行移动授权页的配置。

<br>

##### AuthThemeConfig配置参数说明


| 方法                    | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| setStatusBar            | 设置状态栏颜色（系统版本在5.0以上可设置）、字体颜色（系统版本6.0以上可以设置黑色、白色） |
| setNavTextColor         | 设置服务条款标题字体颜色                                     |
| setNavTextSize          | 设置服务条款标题字体大小                                     |
| setClauseLayoutResID    | 设置服务条款标题布局资源ID                                   |
| setAuthLayoutResID      | 设置授权页布局文件ID                                         |
| setNumberColor          | 设置手机号码字体颜色                                         |
| setNumberSize           | 设置号码栏字体大小                                           |
| setNumFieldOffsetY      | 设置号码栏相对于标题栏下边缘y偏移                            |
| setNumFieldOffsetY_B    | 设置号码栏相对于底部y偏移                                    |
| setNumFieldOffsetX      | 设置号码栏相对于默认位置的x轴偏移量                          |
| setLogBtnText           | 设置登录按钮文本内容、字体颜色，字体大小                     |
| setLogBtnImgPath        | 设置授权登录按钮图片                                         |
| setLogBtn               | 设置登录按钮的宽高                                           |
| setLogBtnMargin         | 设置登录按钮相对于屏幕左右边缘边距                           |
| setLogBtnOffsetY        | 设置按钮相当于标题栏下边缘y偏移                              |
| setLogBtnOffsetY_B      | 设置按钮相对于底部y偏移                                      |
| setLogBtnClickListener  | 设置登录按钮点击事件                                         |
| setPrivacyAlignment     | 设置隐私条款的协议文本，自定义条款，自定义条款链接           |
| setPrivacyText          | 设置隐私条款字体大小、文字颜色、是否居中                     |
| setCheckBoxImgPath      | 设置复选框图片                                               |
| setPrivacyOffsetY       | 设置隐私条款相对于标题栏下边缘y偏移                          |
| setPrivacyOffsetY_B     | 设置隐私条款相对于底部y偏移                                  |
| setPrivacyMargin        | 设置隐私条款距离手机左右边缘的边距                           |
| setAuthPageActIn        | 设置授权页进场动画                                           |
| setAuthPageActOut       | 设置授权页出场动画                                           |
| setAuthPageWindowMode   | 设置授权页宽高比例                                           |
| setAuthPageWindowOffset | 设置授权页窗口X轴Y轴偏移                                     |
| setWindowBottom         | 设置授权页是否居于底部，0=居中；1=底部，设置1时Y轴偏移失效   |
| setThemeId              | 设置授权页弹窗主题，也可以在Manifest中设置。                 |

<br>


##### finish授权页

```
  SDK完成回调后，不会立即关闭授权页面，需要开发者主动调用离开授权页面方法去完成页面的关闭,请调用 SubSDK.quitActivity(mCtx);

```

<br>

---

<br>

### 中国联通授权页规范

<br>

服务条款需文字标明 `联通统一认证服务条款`，协议内容链接如下： https://opencloud.wostore.cn/authz/resource/html/disclaimer.html?fromsdk=true



![](https://libraries.mysubmail.com/public/e6c6783fa0e6ca8ddd61385a5ad92ad6/images/7cfbaea2e26b4957d00c9ce11ce1c333.png)

------

<br>

### 中国电信授权页规范

<br>

为了确保用户在登录过程中将手机号码信息授权给接入方使用的知情权，天翼账号登录认证需要接入方满足如下要求：

（1）接入方在调用登录认证方法前，必须显示出授权页面，授权页面需明确告知用户操作会将用户本机号码信息授权给应用；（天翼账号服务与隐私协议url地址：https://e.189.cn/sdk/agreement/detail.do?hidetop=true）

（2）接入方需展示“天翼账号”品牌露出，不得通过任何技术手段，将授权页面的隐私栏、品牌露出内容隐藏、覆盖；

（3）接入方上线前需要将授权页面提交给我方进行审核，审核通过后才可正式开放登录功能调用使用量。若有出现未按要求设计授权页面的行为或有非正常调用行为，为了保护用户的隐私安全，我方有权将接入方应用的登录功能下线。

如下是天翼账号标准页面的设计规范，供合作方参考;


![](https://libraries.mysubmail.com/public/e6c6783fa0e6ca8ddd61385a5ad92ad6/images/2766991eebe0fde1c1bee2431130ee06.png)



  

------
