#DEMEO:InternationalSMS/Template

<br>

## 概览
- 支持.Net版本：2.0以上 
- 依赖三方库 Newtonsoft.Json.dll

<br>

## 代码示列

```csharp
using System;
using System.Text;
using System.Net;
using System.IO;
using System.Collections.Generic;
using System.Web;
using System.Security.Cryptography;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
namespace SUBMAILDEMO
{
	public class IntersmsTemplateDemo
	{
		private const string API_IntersmsTemplate = "https://api.mysubmail.com/internationalsms/template.json";
		private const string API_Timestamp = "https://api.mysubmail.com/service/timestamp.json";

		public void template()
		{
			string appid = "656xx";
			string appkey = "e1a1d0182xxxx8e3d84bb19730f1";
			string sign_type = "md5";

			//get
			//string template_id = "4zwjd4";
			//string result = GetTemplate(appid, appkey, template_id, sign_type);
			//Console.WriteLine(result);

			//post
			//string sms_title = "POST模板示列";
			//string sms_signature = "【SUBMAIL】";
			//string sms_content = "你好，SUBMAIL";
			//string result = PostTemplate(appid, appkey, sms_title, sms_signature, sms_content, sign_type);

			//put
			//string template_id = "iBmgS1";
			//string sms_title = "PUT模板示列";
			//string sms_signature = "【赛邮】";
			//string sms_content = "哈喽，赛邮";
			//string result = PutTemplate(appid, appkey, template_id,sms_title, sms_signature, sms_content, sign_type);


			//del
			string template_id = "iBmgS1";
			string result = DeleteTemplate(appid, appkey, template_id, sign_type);


			Console.WriteLine(result);

		}



		public string GetTemplate(string appid, string appkey, string template_id, string sign_type)
		{

			Dictionary<string, object> d = new Dictionary<string, object>();
			d.Add("appid", appid);
			d.Add("template_id", template_id);
			string target_url = API_IntersmsTemplate + "?appid=" + appid + "&amp;template_id=" + template_id + "&amp;sign_type=" + sign_type;
			//如果不使用加密方式或者signature传normal则signature参数传入appkey的值
			if (sign_type.Equals("md5") || sign_type.Equals("sha1"))
			{
				string timestamp = JObject.Parse(HttpGet(API_Timestamp))["timestamp"].ToString();
				d.Add("sign_type", sign_type);
				d.Add("timestamp", timestamp);
				if (sign_type.Equals("md5"))
				{
					target_url = target_url + "×tamp=" + timestamp + "&amp;signature=" + GetMD5Signature(FormatRequest(d), appid, appkey);
				}
				else
				{
					target_url = target_url + "×tamp=" + timestamp + "&amp;signature=" + GetSHA1Signature(FormatRequest(d), appid, appkey);
				}
			}
			else
			{
				target_url = target_url + "&amp;signature=" + appkey;
			}

			string response = HttpGet(target_url);
			return response;
		}

		public string PostTemplate(string appid, string appkey, string sms_title, string sms_signature, string sms_content, string sign_type)
		{
			Dictionary<string, object> d = new Dictionary<string, object>();
			d.Add("appid", appid);
			d.Add("sms_title", sms_title);
			d.Add("sms_signature", sms_signature);
			d.Add("sms_content", sms_content);
			//如果不使用加密方式或者signature传normal则signature参数传入appkey的值
			if (sign_type.Equals("md5") || sign_type.Equals("sha1"))
			{
				string timestamp = JObject.Parse(HttpGet(API_Timestamp))["timestamp"].ToString();
				d.Add("sign_type", sign_type);
				d.Add("timestamp", timestamp);
				if (sign_type.Equals("md5"))
				{
					d.Add("signature", GetMD5Signature(FormatRequest(d), appid, appkey));
				}
				else
				{
					d.Add("signature", GetSHA1Signature(FormatRequest(d), appid, appkey));
				}
			}
			else
			{
				d.Add("signature", appkey);
			}
			return HttpMethod(API_IntersmsTemplate, d, "POST");
		}


		public string PutTemplate(string appid, string appkey, string template_id, string sms_title, string sms_signature, string sms_content, string sign_type)
		{
			Dictionary<string, object> d = new Dictionary<string, object>();
			d.Add("appid", appid);
			d.Add("template_id", template_id);
			d.Add("sms_title", sms_title);
			d.Add("sms_signature", sms_signature);
			d.Add("sms_content", sms_content);
			//如果不使用加密方式或者signature传normal则signature参数传入appkey的值
			if (sign_type.Equals("md5") || sign_type.Equals("sha1"))
			{
				string timestamp = JObject.Parse(HttpGet(API_Timestamp))["timestamp"].ToString();
				d.Add("sign_type", sign_type);
				d.Add("timestamp", timestamp);

				if (sign_type.Equals("md5"))
				{
					d.Add("signature", GetMD5Signature(FormatRequest(d), appid, appkey));
				}
				else
				{
					d.Add("signature", GetSHA1Signature(FormatRequest(d), appid, appkey));
				}
			}
			else
			{
				d.Add("signature", appkey);
			}
			return HttpMethod(API_IntersmsTemplate, d, "PUT");
		}




		public string DeleteTemplate(string appid, string appkey, string template_id, string sign_type)
		{
			Dictionary<string, object> d = new Dictionary<string, object>();
			d.Add("appid", appid);
			d.Add("template_id", template_id);

			//如果不使用加密方式或者signature传normal则signature参数传入appkey的值
			if (sign_type.Equals("md5") || sign_type.Equals("sha1"))
			{
				string timestamp = JObject.Parse(HttpGet(API_Timestamp))["timestamp"].ToString();
				d.Add("sign_type", sign_type);
				d.Add("timestamp", timestamp);

				if (sign_type.Equals("md5"))
				{
					d.Add("signature", GetMD5Signature(FormatRequest(d), appid, appkey));
				}
				else
				{
					d.Add("signature", GetSHA1Signature(FormatRequest(d), appid, appkey));
				}
			}
			else
			{
				d.Add("signature", appkey);
			}
			return HttpMethod(API_IntersmsTemplate, d, "DELETE");
		}



		public string HttpMethod(string url, Dictionary<string, Object> parameters, string method)
		{
			HttpWebRequest request = WebRequest.Create(url) as HttpWebRequest;//创建请求对象
			request.Method = method;//请求方式
			request.ContentType = "application/x-www-form-urlencoded";//链接类型
																	  //构造查询字符串
			if (!(parameters == null || parameters.Count == 0))
			{
				StringBuilder buffer = new StringBuilder();
				bool first = true;
				foreach (string key in parameters.Keys)
				{

					if (!first)
					{
						buffer.AppendFormat("&amp;{0}={1}", HttpUtility.UrlEncode(key, Encoding.UTF8), HttpUtility.UrlEncode((string)parameters[key], Encoding.UTF8));
					}
					else
					{
						buffer.AppendFormat("{0}={1}", HttpUtility.UrlEncode(key, Encoding.UTF8), HttpUtility.UrlEncode((string)parameters[key], Encoding.UTF8));
						first = false;
					}
				}

				Console.WriteLine("requestParam：" + buffer.ToString());
				byte[] data = Encoding.UTF8.GetBytes(buffer.ToString());
				//写入请求流
				using (Stream stream = request.GetRequestStream())
				{
					stream.Write(data, 0, data.Length);
					stream.Close();
				}
			}
			HttpWebResponse hwp = request.GetResponse() as HttpWebResponse;
			string response = GetResponseString(hwp);
			hwp.Close();
			return response;
		}


		//get请求
		public string HttpGet(string url)
		{
			HttpWebRequest request = WebRequest.Create(url) as HttpWebRequest;//创建请求对象
			request.Method = "GET";//请求方式 
			request.ContentType = "application/x-www-form-urlencoded";
			HttpWebResponse hwp = request.GetResponse() as HttpWebResponse;
			string response = GetResponseString(hwp);
			hwp.Close();
			return response;
		}



		public string GetResponseString(HttpWebResponse webresponse)
		{
			using (Stream s = webresponse.GetResponseStream())
			{
				StreamReader reader = new StreamReader(s, Encoding.UTF8);
				return reader.ReadToEnd();
			}
		}


		//加密参数升序
		public string FormatRequest(Dictionary<string, object> data)
		{
			StringBuilder builder = new StringBuilder();
			if (data.Count > 0)
			{
				List<KeyValuePair<string, Object>> lst = new List<KeyValuePair<string, Object>>(data);
				lst.Sort(delegate (KeyValuePair<string, object> s1, KeyValuePair<string, object> s2)
								{
									return s1.Key.CompareTo(s2.Key);
								});
				foreach (KeyValuePair<string, object> kvp in lst)
				{
					if (kvp.Value != null)
					{
						builder.Append(string.Format("{0}={1}&amp;", kvp.Key, kvp.Value));

					}

				}

			}
			string formatData = builder.ToString();
			Console.WriteLine(formatData);
			if (formatData.Length > 0)
			{
				return formatData.Substring(0, formatData.Length - 1);
			}
			return null;
		}

		//获取md5加密后的签名字符串
		private string GetMD5Signature(string data, string appid, string appkey)
		{
			string signStr = string.Format("{0}{1}{2}{3}{4}", appid, appkey, data, appid, appkey);
			MD5 md5 = new MD5CryptoServiceProvider();
			byte[] fromData = Encoding.GetEncoding("utf-8").GetBytes(signStr);
			byte[] targetData = md5.ComputeHash(fromData);
			StringBuilder sBuilder = new StringBuilder();
			for (int i = 0; i < targetData.Length; i++)
			{

				sBuilder.Append(targetData[i].ToString("x2"));
			}
			return sBuilder.ToString();
		}

		//获取sha1加密后的签名字符串
		private string GetSHA1Signature(string data, string appid, string appkey)
		{
			string signStr = string.Format("{0}{1}{2}{3}{4}", appid, appkey, data, appid, appkey);
			SHA1 sha1 = new SHA1CryptoServiceProvider();
			byte[] fromData = Encoding.GetEncoding("utf-8").GetBytes(signStr);
			byte[] targetData = sha1.ComputeHash(fromData);
			StringBuilder sBuilder = new StringBuilder();
			for (int i = 0; i < targetData.Length; i++)
			{
				sBuilder.Append(targetData[i].ToString("x2"));
			}
			return sBuilder.ToString();
		}
	}
}
```