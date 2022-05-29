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

## Footer

Return to [Parent Readme.md](../README.html)  
