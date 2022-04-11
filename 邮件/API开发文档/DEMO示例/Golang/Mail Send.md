# DEMO:Mail/Send

### 示例代码

<br>

#### 依赖

```
import (
	"bytes"
	"crypto/md5"
	"encoding/hex"
	"encoding/json"
	"fmt"
	"io"
	"io/ioutil"
	"net/http"
	"os"
	"path/filepath"
	"sort"
	"strconv"
	"strings"

	"mime/multipart"
)
```

#### 配置信息

```
const (
	API    = "https://api-v4.mysubmail.com/mail/send"
	APPID  = "10***"
	APPKEY = "f8a5**********************778df"
	FROM   = "submail@submail.cn"
)
```

#### 非加密代码示例

```
    postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["signature"] = APPKEY
	postdata["from"] = FROM
	postdata["from_name"] = "SUBMAIL"
	postdata["subject"] = "来自 SUBMAIL 的端午祝福"
	postdata["to"] = "514030829@qq.com"
	postdata["html"] = "<body><h1>您好，祝您阖家欢乐，万事如意</h1></body>"

	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range postdata {
		_ = writer.WriteField(key, val)
	}
	//附件1
	file1, _ := os.Open("/Users/duan/Desktop/12455.png")
	defer file1.Close()
	fromFile1, _ := writer.CreateFormFile("attachments[]", filepath.Base("/Users/duan/Desktop/12455.png"))
	io.Copy(fromFile1, file1)
	//附件2
	file2, _ := os.Open("/Users/duan/Desktop/12345.png")
	defer file2.Close()
	fromFile2, _ := writer.CreateFormFile("attachments[]", filepath.Base("/Users/duan/Desktop/12345.png"))
	io.Copy(fromFile2, file2)

	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))

```



#### 加密代码示例

```
    postdata := make(map[string]string)
	postdata["appid"] = APPID
	postdata["from"] = FROM
	postdata["from_name"] = "SUBMAIL"
	postdata["subject"] = "来自 SUBMAIL 的端午祝福"
	postdata["to"] = "514030829@qq.com"
	postdata["timestamp"] = ""
	postdata["sign_type"] = "md5"
	postdata["sign_version"] = "2"
	//获取服务器时间戳，该时间戳为 UNIX 时间戳，也可以自己生成
	q, _ := http.Get("https://api-v4.mysubmail.com/service/timestamp")
	r, _ := ioutil.ReadAll(q.Body)
	m := make(map[string]float64)
	json.Unmarshal(r, &amp;m)
	postdata["timestamp"] = strconv.FormatFloat(m["timestamp"], 'f', -1, 64)
	//签名加密
	sign := make(map[string]string)
	sign = postdata
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
	postdata["html"] = "<body><h1>您好，祝您阖家欢乐，万事如意</h1></body>"

	body := &amp;bytes.Buffer{}
	writer := multipart.NewWriter(body)
	for key, val := range postdata {
		_ = writer.WriteField(key, val)
	}
	//附件1
	file1, _ := os.Open("/Users/duan/Desktop/12455.png")
	defer file1.Close()
	fromFile1, _ := writer.CreateFormFile("attachments[]", filepath.Base("/Users/duan/Desktop/12455.png"))
	io.Copy(fromFile1, file1)
	//附件2
	file2, _ := os.Open("/Users/duan/Desktop/12345.png")
	defer file2.Close()
	fromFile2, _ := writer.CreateFormFile("attachments[]", filepath.Base("/Users/duan/Desktop/12345.png"))
	io.Copy(fromFile2, file2)

	contentType := writer.FormDataContentType()
	writer.Close()
	resp, _ := http.Post(API, contentType, body)
	result, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(result))
	
```