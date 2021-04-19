# POST

## 安裝套件

```text
compile 'org.apache.httpcomponents:httpclient:4.5'
implementation 'org.json:json:20171018'
```

## POST

### POST JSON

讀到的會是 JSONObject

```java
String inputData = "{\"key\":\"jansonpro\"}";
String strUrl = "https://asia-east2-kinetic-dream-310007.cloudfunctions.net/get_emp_data_api";
StringBuffer sb = new StringBuffer();
HttpURLConnection conn = (HttpURLConnection) new URL(strUrl).openConnection();
conn.setDoOutput(true);
conn.setDoInput(true);
conn.setRequestMethod("POST");
conn.setRequestProperty("Accept", "application/json");                
conn.setRequestProperty("Content-Type", "application/json; charset=\"UTF-8\"");
OutputStream out = conn.getOutputStream(); // if remove OutputStream, it return 404 error
out.write(inputData.getBytes());
out.close();     
System.out.println(conn.getResponseCode());
InputStreamReader in = new InputStreamReader((InputStream)conn.getContent());
BufferedReader br = new BufferedReader(in);
String line;
while ((line = br.readLine()) != null)
    sb.append(line).append("\n");
JSONObject jsonObject = new JSONObject(sb.toString());
System.out.println(jsonObject);
```

### POST FILE

```java
public void saveEmpData(String empId, ArrayList<byte[]> FPArr, File photoImg,
							String empName, String empDepartment) throws IOException {		
//		convert byte[] to string
		String fp1Str = new String(Base64.getEncoder().encode(FPArr.get(0)));
		String fp2Str = new String(Base64.getEncoder().encode(FPArr.get(1)));
		String fp3Str = new String(Base64.getEncoder().encode(FPArr.get(2)));
		
		JSONObject apiJsonObj = new JSONObject();
		apiJsonObj.put("key", "jansonpro");
		apiJsonObj.put("mode", "server");
		apiJsonObj.put("emp-id", empId);
		apiJsonObj.put("honprec-id", empId);
		apiJsonObj.put("name", empName);
		apiJsonObj.put("department", empDepartment);
		apiJsonObj.put("line-token", "123");
		apiJsonObj.put("photo", "321");
		apiJsonObj.put("FP1", fp1Str);
		apiJsonObj.put("FP2", fp2Str);
		apiJsonObj.put("FP3", fp3Str);
		
		JSONObject responseJsonObj = requestAPI(apiJsonObj.toString(), "https://asia-east2-kinetic-dream-310007.cloudfunctions.net/upload_emp_data_api");

//		
//		savePngFile(String.format("%s\\%s", path, phtotFileName), photoImg);
	}

private JSONObject requestAPI(String inputData, String url) throws IOException {		
		StringBuffer sb = new StringBuffer();
		HttpURLConnection conn = (HttpURLConnection) new URL(url).openConnection();
		
		conn.setDoOutput(true);
		conn.setDoInput(true);
		conn.setRequestMethod("POST");
		conn.setRequestProperty("Accept", "application/json");                
		conn.setRequestProperty("Content-Type", "application/json; utf-8");
		
		OutputStream out = conn.getOutputStream(); // if remove OutputStream, it return 404 error
		out.write(inputData.getBytes("utf-8"));
		out.close();     
		
		InputStreamReader in = new InputStreamReader((InputStream)conn.getContent());
		BufferedReader br = new BufferedReader(in);
		
		String line;
		while ((line = br.readLine()) != null)
		    sb.append(line).append("\n");
		
		return new JSONObject(sb.toString());
	}


```

## 參考資料

1. [Making a JSON POST Request With HttpURLConnection \| Baeldung](https://www.baeldung.com/httpurlconnection-post)
2. [JAVA Http POST request in UTF-8 - Stack Overflow](https://stackoverflow.com/questions/18823357/java-http-post-request-in-utf-8)
3. [Java Base64 Encoding and Decoding \| Baeldung](https://www.baeldung.com/java-base64-encode-and-decode)
4. [java - how to send byte array in json post request? - Stack Overflow](https://stackoverflow.com/questions/24568735/how-to-send-byte-array-in-json-post-request)
5. [java byte \[\] 转 String 再转回 byte \[\] 不一致问题\_Runner1st 的博客 - CSDN 博客](https://blog.csdn.net/Runner1st/article/details/104363726?utm_medium=distribute.pc_relevant_bbs_down.none-task-blog-baidujs-1.nonecase&depth_1-utm_source=distribute.pc_relevant_bbs_down.none-task-blog-baidujs-1.nonecase)
6. [java - How to send post request with x-www-form-urlencoded body - Stack Overflow](https://stackoverflow.com/questions/40574892/how-to-send-post-request-with-x-www-form-urlencoded-body)
7. [Java 图片和文本同时提交到 form 表单 multipart/form-data\_one\_hwx 的博客 - CSDN 博客](https://blog.csdn.net/one_hwx/article/details/81287795)
8. [Android HttpURLConnection 上傳檔案 \(multipart/form-data\)](http://blog.kenyang.net/2011/12/27/android-httpurlconnection-multipartform)

