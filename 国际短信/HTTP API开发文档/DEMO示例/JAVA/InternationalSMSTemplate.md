# DEMO:InternationalSMS/Template

<br>

- 支持JDK版本：1.5以上 
- 依赖的jar包：httpclient-4.5.3.jar、httpcore-4.4.14.jar、commons-logging1.1.1.jar、fastjson-1.2.75.jar


```java
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.3</version>
</dependency>
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpcore</artifactId>
    <version>4.4.14</version>
</dependency>
<dependency>
    <groupId>commons-logging</groupId>
    <artifactId>commons-logging</artifactId>
    <version>1.1.1</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.75</version>
</dependency>
```

## 代码示例
### IntersmsTemplateDemo
```java
package com.submail.demo.intersms;
import com.alibaba.fastjson.JSONObject;
import com.submail.demo.RequestEncoder;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.*;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;
import java.io.IOException;
import java.net.URI;
import java.util.Map;
import java.util.TreeMap;

public class IntersmsTemplate {
    public static final String TIMESTAMP = "https://api-v4.mysubmail.com/service/timestamp";
    private static final String URL = "https://api-v4.mysubmail.com/internationalsms/template.json";
    public static final String TYPE_MD5 = "md5";
    public static final String TYPE_SHA1 = "sha1";

    public static void main(String[] args) throws IllegalStateException, IOException {
        TreeMap<String, String> requestData = new TreeMap<String, String>();
        String method = "delete";       //  get | post | put | delete
        String appid = "";
        String appkey = "";
        String signtype = "md5";         // normal | md5 | sha1
        //get请求参数
        String template_id = "Wk3zx2";
        //post请求参数
        String sms_title = "TEMPLATE接口测试";
        String sms_content = "您的验证码是@var(code)，请在二十分钟之内输入，请勿告知别人";

        requestData.put("appid", appid);
        switch (method) {
            case "post":
                requestData.put("sms_title", sms_title);
                requestData.put("sms_content", sms_content);
                HttpPost httpPost = new HttpPost(URL);
                httpPost.addHeader("charset", "UTF-8");
                httpPost.setHeader("Accept", "application/json");
                httpPost.setHeader("Content-Type", "application/json");
                StringEntity postEntity = new StringEntity(JSONObject.toJSONString(buildSignature(appid, appkey, signtype, requestData)), "UTF-8");
                httpPost.setEntity(postEntity);
                httpRequest(httpPost);
                break;
            case "get":
                requestData.put("template_id", template_id);
                requestData = buildSignature(appid, appkey, signtype, requestData);
                System.out.println("requestData = " + requestData);
                String urlGet = URL + "?";
                for (Map.Entry<String, String> entry : requestData.entrySet()) {
                    String key = entry.getKey();
                    Object value = entry.getValue();
                    if (value instanceof String) {
                        urlGet += key + "=" + value + "&amp;";
                    }
                }
                urlGet = urlGet.substring(0, urlGet.length() - 1);
                System.out.println("urlGet = " + urlGet);
                HttpGet httpGet = new HttpGet(urlGet);
                httpRequest(httpGet);
                break;
            case "put":
                requestData.put("template_id", template_id);
                requestData.put("sms_title", sms_title);
                requestData.put("sms_content", sms_content);
                HttpPut httpput = new HttpPut(URL);
                httpput.addHeader("charset", "UTF-8");
                httpput.setHeader("Accept", "application/json");
                httpput.setHeader("Content-Type", "application/json");
                StringEntity entity = new StringEntity(JSONObject.toJSONString(buildSignature(appid, appkey, signtype, requestData)), "UTF-8");
                httpput.setEntity(entity);
                httpRequest(httpput);
                break;

            case "delete":
                requestData.put("template_id", template_id);
                requestData = buildSignature(appid, appkey, signtype, requestData);
                String entityStr = "";
                for (Map.Entry<String, String> entry : requestData.entrySet()) {
                    String key = entry.getKey();
                    String value = entry.getValue();
                    entityStr += key + "=" + String.valueOf(value) + "&amp;";
                }
                System.out.println(entityStr);
                HttpDeleteWithBody httpDelete = new HttpDeleteWithBody(URL);
                HttpEntity delEntity = new StringEntity(entityStr);
                httpDelete.setEntity(delEntity);
                httpRequest(httpDelete);
                break;
        }

    }

    /**
     * 获取时间戳
     *
     * @return
     */
    private static String getTimestamp() {
        CloseableHttpClient closeableHttpClient = HttpClientBuilder.create().build();
        HttpGet httpget = new HttpGet(TIMESTAMP);
        try {
            HttpResponse response = closeableHttpClient.execute(httpget);
            HttpEntity httpEntity = response.getEntity();
            String jsonStr = EntityUtils.toString(httpEntity, "UTF-8");
            if (jsonStr != null) {
                JSONObject json = JSONObject.parseObject(jsonStr);
                return json.getString("timestamp");
            }
            closeableHttpClient.close();
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }

        return null;
    }

    public static void httpRequest(HttpRequestBase httpRequestBase) {
        try {
            CloseableHttpClient closeableHttpClient = HttpClientBuilder.create().build();
            HttpResponse response = closeableHttpClient.execute(httpRequestBase);
            HttpEntity httpEntity = response.getEntity();
            if (httpEntity != null) {
                String jsonStr = EntityUtils.toString(httpEntity, "UTF-8");
                System.out.println(jsonStr);
            }
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static TreeMap<String, String> buildSignature(String appid, String appkey, String sign_type, TreeMap<String, String> requestData) {
        if (sign_type.equals(TYPE_MD5) || sign_type.equals(TYPE_SHA1)) {
            String timestamp = getTimestamp();
            requestData.put("timestamp", timestamp);
            requestData.put("sign_type", sign_type);
            String signStr = appid + appkey + RequestEncoder.formatRequest(requestData) + appid + appkey;
            System.out.println(signStr);
            requestData.put("signature", RequestEncoder.encode(sign_type, signStr));
        } else {
            requestData.put("signature", appkey);
        }
        return requestData;
    }
}

class HttpDeleteWithBody extends HttpEntityEnclosingRequestBase {
    public static final String METHOD_NAME = "DELETE";

    public String getMethod() {
        return METHOD_NAME;
    }

    public HttpDeleteWithBody(final String uri) {
        super();
        setURI(URI.create(uri));
    }

    public HttpDeleteWithBody(final URI uri) {
        super();
        setURI(uri);
    }

    public HttpDeleteWithBody() {
        super();
    }
}

```
---
### RequestEncoder

```java
package com.submail.demo;

/**
 * @author zhang
 * @date 2021/8/4 - 5:52 下午
 */

import java.security.MessageDigest;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;

public class RequestEncoder {
    private static final char[] HEX_DIGITS = {'0', '1', '2', '3', '4', '5',
            '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};

    public static String encode(String algorithm, String str) {
        if (str == null) {
            return null;
        }
        try {
            MessageDigest messageDigest = MessageDigest.getInstance(algorithm);
            messageDigest.update(str.getBytes("UTF-8"));
            return getFormattedText(messageDigest.digest());
        } catch (Exception e) {
            throw new RuntimeException(e);
        }

    }

    private static String getFormattedText(byte[] bytes) {
        int len = bytes.length;
        StringBuilder buf = new StringBuilder(len * 2);
        for (int j = 0; j < len; j++) {
            buf.append(HEX_DIGITS[(bytes[j] >> 4) &amp; 0x0f]);
            buf.append(HEX_DIGITS[bytes[j] &amp; 0x0f]);
        }
        return buf.toString();
    }

    public static String formatRequest(Map<String, String> data) {
        Set<String> keySet = data.keySet();
        Iterator<String> it = keySet.iterator();
        StringBuffer sb = new StringBuffer();
        while (it.hasNext()) {
            String key = it.next();
            Object value = data.get(key);
            if (value instanceof String) {
                sb.append(key + "=" + value + "&amp;");
            }
        }
        if (sb.length() != 0) {
            System.out.println("sb.substring(0, sb.length() - 1) = " + sb.substring(0, sb.length() - 1));
            return sb.substring(0, sb.length() - 1);
        }
        return null;
    }
}
```