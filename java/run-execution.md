# 執行 exe 檔案

```java
String s = null;
		
try {
 Process p = Runtime.getRuntime().exec("main.exe read");
 BufferedReader stdInput = new BufferedReader(new 
                 InputStreamReader(p.getInputStream()));
            
 while ((s = stdInput.readLine()) != null) {  
 	System.out.println(s);
 }
}
		
  catch (IOException e) {
    e.printStackTrace();
   }

// 等待程執行完成
try {
			Runtime.getRuntime().exec("main.exe upload").waitFor();
		} catch (InterruptedException | IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

```

