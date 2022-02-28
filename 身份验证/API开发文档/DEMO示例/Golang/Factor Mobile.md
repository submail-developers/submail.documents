# DEMO:Factor/Mobile
<br>

####依赖
```
import (
	"bytes"
	"crypto/sha256"
	"fmt"
	"io/ioutil"
	"mime/multipart"
	"net/http"
	"net/url"
	"strconv"
	"time"
)
```


####配置信息
```
const (
	API    = "https://tpa.mysubmail.com/factor/mobile"
	APPID  = "10***"
	APPKEY = "f8a5**********************778df"
)
```


####代码示例
```
    //所需参数
	data := make(map[string]string)
	data["appid"] = APPID
	data["timestamp"] = strconv.FormatInt(time.Now().Unix(), 10)
	data["name"] = "张三"
	data["mobile"] = "152********"

	//生成签名
	sign := url.Values{}
	sign.Set("appkey", APPKEY)
	sign.Set("mobile", data["mobile"])
	sign.Set("name", data["name"])
	sign.Set("timestamp", data["timestamp"])
	h := sha256.New()
	h.Write([]byte(sign.Encode()))
	data["signature"] = fmt.Sprintf("%x", h.Sum(nil))

	//请求
	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range data {
		_ = writer.WriteField(key, val)
	}
	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))

```