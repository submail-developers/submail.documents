# DEMEO:InternationalSMS/MultiXSend

###示例代码
<br>

####依赖
```
import (
	"bytes"
	"crypto/md5"
	"encoding/hex"
	"encoding/json"
	"fmt"
	"io"
	"io/ioutil"
	"mime/multipart"
	"net/http"
	"sort"
	"strconv"
	"strings"
)
```


####配置信息
```
const (
	API    = "https://api.mysubmail.com/internationalsms/multixsend"
	APPID  = "10***"
	APPKEY = "f8a5**********************778df"
)
```


####非加密代码示例
```
   //示例模版ID：zcMxF4，示例模版内容：Your verification code is @var(code), please enter it within @var(time)minutes。
	multi := make([]map[string]interface{}, 0, 32)
	//添加一个号码
	vars := make(map[string]string)
	vars["code"] = "123456"
	vars["time"] = "10分钟"
	multi = append(multi, map[string]interface{}{
		"to":   "+052********",//号码一
		"vars": vars,
	})
	//添加一个号码
	vars["code"] = "123456"
	vars["time"] = "10分钟"
	multi = append(multi, map[string]interface{}{
		"to":   "+053********",//号码二
		"vars": vars,
	})
	//添加一个号码
	vars["code"] = "123456"
	vars["time"] = "10分钟"
	multi = append(multi, map[string]interface{}{
		"to":   "+054********",//号码三
		"vars": vars,
	})
	m, _ := json.Marshal(multi)
	postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = APPKEY
	postdata["project"] = "zcMxF4"
	postdata["multi"] = string(m)

	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range postdata {
		_ = writer.WriteField(key, val)
	}
	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))

```



####加密代码示例
```
    //所需参数
	multi := make([]map[string]interface{}, 0, 32)
	//添加一个号码
	vars := make(map[string]string)
	vars["code"] = "123456"
	vars["time"] = "10分钟"
	multi = append(multi, map[string]interface{}{
		"to":   "+052********",//号码一
		"vars": vars,
	})
	//添加一个号码
	vars["code"] = "123456"
	vars["time"] = "10分钟"
	multi = append(multi, map[string]interface{}{
		"to":   "+053********",//号码二
		"vars": vars,
	})
	//添加一个号码
	vars["code"] = "123456"
	vars["time"] = "10分钟"
	multi = append(multi, map[string]interface{}{
		"to":   "+054********",//号码三
		"vars": vars,
	})
	m, _ := json.Marshal(multi)

	postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = ""
	postdata["project"] = "zcMxF4"
	postdata["multi"] = string(m)
	postdata["timestamp"] = ""
	postdata["sign_type"] = "md5"
	postdata["sign_version"] = "2"
	//获取服务器时间戳，该时间戳为 UNIX 时间戳，也可以自己生成
	q, _ := http.Get("https://api.mysubmail.com/service/timestamp")
	r, _ := ioutil.ReadAll(q.Body)
	t := make(map[string]float64)
	json.Unmarshal(r, &amp;t)
	postdata["timestamp"] = strconv.FormatFloat(t["timestamp"], 'f', -1, 64)
	//签名加密
	sign := make(map[string]string)
	sign["appid"] = postdata["appid"]
	sign["project"] = postdata["project"]
	sign["timestamp"] = postdata["timestamp"]
	sign["sign_type"] = postdata["sign_type"]
	sign["sign_version"] = postdata["sign_version"]
	keys := make([]string, 0, 32)
	for key, _ := range sign {
		keys = append(keys, key)
	}
	sort.Strings(keys)
	sign_list := make([]string, 0, 32)
	for _, key := range keys {
		sign_list = append(sign_list, key+"="+sign[key])
	}
	sign_str := APPID + APPKEY + strings.Join(sign_list, "&amp;") + APPID + APPKEY
	mymd5 := md5.New()
	io.WriteString(mymd5, sign_str)
	postdata["signature"] = hex.EncodeToString(mymd5.Sum(nil))

	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range postdata {
		_ = writer.WriteField(key, val)
	}
	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))
	
```