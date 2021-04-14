# POST

## 安裝套件

```text
compile 'org.apache.httpcomponents:httpclient:4.5'
implementation 'org.json:json:20171018'
```

## POST

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

