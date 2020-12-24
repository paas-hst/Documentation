# 快速开始
## 获取开发者ID和秘钥
首先从PaaS管理平台的面板页面获取开发者ID和秘钥，例如：
开发者ID：`a92b622559266609176621caf44f5857`
开发者秘钥：`6577543f6604bbaf`

## 生成Token
然后通过FspToken工具类生成token，以Java代码为例：
```java
String devId = "a92b622559266609176621caf44f5857"; //开发者ID
String devSecret = "6577543f6604bbaf"; //开发者秘钥
FspToken fspToken = new FspToken();
fspToken.setAppId(devId);
fspToken.setSecretKey(devSecret);
String token = fspToken.build();
System.out.println(token);
```
## 获取Access Token
在上述代码基础上，通过HTTP客户端调用接口获取Access Token：
```java
String authorization = devId + "." + token;
String url = "http://192.168.7.201:28000/access/token";
HttpGet getMethod = new HttpGet(url);
getMethod.setHeader("Authorization", authorization);
try (CloseableHttpClient httpclient = HttpClients.createDefault()) {
    CloseableHttpResponse rsp = httpclient.execute(getMethod);
    int status = rsp.getStatusLine().getStatusCode();
    System.out.println("http status:" + status);
    if (status == 200) {
        HttpEntity entity = rsp.getEntity();
        System.out.println(EntityUtils.toString(entity));
    }
} catch (IOException ex) {
    ex.printStackTrace();
}
```
获取到Access Token后，保存在缓存中，作为调用其他接口的凭证。
## Access Token的使用
以创建应用的接口为例演示如何使用Access Token：
```java
String url = "http://192.168.7.201:28000/v1/app";
HttpPost postMethod = new HttpPost(url);

// 将Access Token设置到请求头，用于接口鉴权
// getAccessTokenFromCache()代表从缓存获取Access Token，具体实现这里不提供
postMethod.setHeader("Authorization", getAccessTokenFromCache());
postMethod.setHeader("Content-Type", "application/json;charset=UTF-8");
        
// 封装创建应用的参数
JSONObject rootNode = new JSONObject();
rootNode.put("app_name", "test123");
rootNode.put("status", "online");
JSONArray arr = new JSONArray();
for (int i = 3; i < 9; i++) {
    JSONObject obj = new JSONObject();
    obj.put("service_id", i);
    arr.add(obj);
}
rootNode.put("service", arr);
String body = rootNode.toJSONString();
System.out.println(body);
        
postMethod.setEntity(new StringEntity(body));
try (CloseableHttpClient httpclient = HttpClients.createDefault()) {
    CloseableHttpResponse rsp = httpclient.execute(postMethod);
    int status = rsp.getStatusLine().getStatusCode();
    System.out.println("http status:" + status);
    if (status == 200) {
        HttpEntity entity = rsp.getEntity();
        System.out.println(EntityUtils.toString(entity));
    }
} catch (IOException ex) {
    ex.printStackTrace();
}
```