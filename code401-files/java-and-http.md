# Class Readings on Java and HTTP

## Resources

Dev.to on the [HTTP Request Lifecycle](https://dev.to/dangolant/things-i-brushed-up-on-this-week-the-http-request-lifecycle-)  

Baeldung reviews how to [Do a Simple HTTP Request](https://www.baeldung.com/java-http-request)  

## HTTP Request Lifecycle Notes

HTTP communications boil down to this template: `<protocol>://<host><:optional port>/<path/to/resource><?query>. An example is |http|://|www.example.com||:5000||/mainpage||?query=param&query2=param2|` *[Daniel Golent, Dev.to article, accessed 29-May-22]*  

TCP/IP connection features are invoked as part of HTTP request/responses.  

1. SYN: Open a connection?
2. SYN-ACK: Open a conenction OK.
3. ACK: Thanks!
4. Datagrams exchanged...
5. FIN: Close the connection?
6. FIN-ACK: Close the connection OK.
7. ACK: Thanks, closed!

Name Resolution Plays a Part!

- localhost cache
- local/network-local caching DNS services like an edge router
- DNS caching beyond your local network
- Top-level DNS service queries

An actual HTTP Request isn't sent until TCP/IP and DNS have completed their initial tasks.  

All setups, requests, and teardown also have to traverse the network of Routers.  
*Note*: Routes to/from might not always be the same.  

File/resource caching plays a part!

- Some portions of an HTTP request could be cached, such as areas on a web page.

HTTP is a higher-level ("Application Layer") protocol in the OSI stack, so it relies on other lower-level protocols to do their job, so that it can send requests and handle responses accordingly.  
Simple HTTP Req/Res protocol is "connectionless" and "stateless".  
There are other HTTP protocol actions that are different in later versions.  

## Simple HTTP Requests with Spring

Applies to Spring 5 and Spring Boot 2.  

### Perform HTTP Requests in Java

Baeldung has a link to a page that explores updates to Java's [HTTP API](https://www.baeldung.com/java-9-http-client)  

### HttpUrlConnection

Class that enables basic HTTP Requests.  
Single library needed: java.net  
Simple functionality only.  
For more advanced, use other libraries.  

### Creating a Request

This is step one and *only creates the request*.  
Can be used for the following: GET, POST, HEAD, OPTIONS, PUT, DELETE, and TRACE.  

```java
URL url = new URL("http://website.ext");
HttpURLConnection connection = (HttpURLConnecion) url.openConnection();
connection.setRequestMethod(String: verb);
```

### Adding Request Params

Request parameters are set by Boolean property doOutput.  
Use a String to create an appropriate key:value pair to add a request parameter.  

```java
Map<String, String> parameters = new HashMap<>();
parameters.put("param1", "val");
connection.setDoOutput(true);
DataOutputStream out = new DataOutputStream(connection.getOutputStream());
// parameterStringBuilder is a custom class see Baeldung.com for details
out.writeBytes(ParameterStringBuilder.getParamsString(parameters));
out.flush();
out.close();
```

### Setting Request Headers

Add headers to a request via method `setRequestProperty()`  
Read the value of a header from a connection via method `getHeaderField()`  

```java
connection.setRequestProperty("Content-Type", "application/json");
String contentType = connection.getHeaderField("Content-Type");
```

### Configuring Timeouts

Set connect and read Timeouts via HttpUrlConnection class using `setConnectTimeout()` and `setReadTimeout()` methods.  

```java
connection.setConnectTimeout(Integer: number);
connection.setReadTimeout(Integer: number);
```

### Handling Cookies

Work with cookies using CookieManager and HttpCookie.  

### Handling Redirects

### Reading the Response

### Reading the Response on Failed Requests

### Building the Full Response

## Footer

Return to [Parent Readme.md](../README.html)  
