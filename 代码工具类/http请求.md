http请求服务
```java
private static final String path = "http://121.43.39.49:8095/blade-test/customerRecords/getToken";  // 要请求的接口路径
  
public String getTokenInfo() throws Exception {  
  
    HttpUtil.createPost(path);  
    HttpRequest post = HttpRequest.post(path);  
    HttpResponse response = post.execute();  
    response.body();
    URL url = new URL(path);  
    HttpURLConnection connection = (HttpURLConnection) url.openConnection(); 
    connection.setRequestMethod("POST"); // 设置请求方式 GET、POST 等  
    connection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");  
    connection.setRequestProperty("Connection", "Keep-Alive");  
    connection.setConnectTimeout(2000); // 设置连接超时时间，单位：ms 。  
    connection.setReadTimeout(2000); // 设置读取超时时间，单位：ms 。  
    connection.setDoInput(true); // 设置打开输入流 ： default = true    connection.setDoOutput(true); // 设置打开输出流：default = false  
    connection.setUseCaches(false); // 设置是否启用用户缓存： default = false    OutputStream outputStream = connection.getOutputStream(); // 获取输出流对象，准备往服务器写数据  
    outputStream.flush();  
    outputStream.close();  
  
    // 获取服务器返回的响应状态  
    if (connection.getResponseCode() != HttpURLConnection.HTTP_OK) {  
        System.out.println(" request fail ...");  
        return connection.getResponseMessage();  
    }  
  
    // 读取服务器返回的数据  
    BufferedReader reader = new BufferedReader(new  
            InputStreamReader(connection.getInputStream(), StandardCharsets.UTF_8));  
    String line;  
    StringBuffer sb = new StringBuffer();  
    while ((line = reader.readLine()) != null) {  
        sb.append(line);  
    }  
    reader.close();  
    String result = sb.toString();  
    log.info("获取到最新的token信息:{}", result);  
    return result;  
}
```