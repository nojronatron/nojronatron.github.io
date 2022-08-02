# More CRUD Readings

## Status Codes Based On REST Methods

In your own words, describe what each group of status code represents:

100’s = Informational: Inform caller that Headers have been received.  
200’s = Success: Inform caller the command was accepted (but not necessarily *processed).  
300’s = Redirect: Tells client to call another URL to get what they are wanting.  
400’s = Bad Requests (Client-side): Tells client the request was not accepted/invalid.  
500’s = Error: Server-side error occured e.g. too busy, unreachable, or exceptions.  

What is a status code 202?  

> Asynchronous Processing. All validation requirements have been met and processing has succeeded.  

What is a status code 308?  

> Permanent Redirect.  
> Only applies to GET requests.  
> Suggested application is to use in nested endpoints to ease navigation for the client.  

What code would you use if an update didn’t return data to a client?  

> HTTP 204.  

What code would you use if a resource used to exist but no longer does?  

> HTTP 404.  

What is the ‘Forbidden’ status code?  

> HTTP 403. Permissions not granted to access resources on the endpoint.  

## Videos to Browse

Build A REST API With Node.js, Express, & MongoDB - Quick - First 20 minutes

Why do we need to pull our MongoDB database string out of our server and put it into our .env?  

> So the API Server knows how to contact the DB Server.  
> It is a connection string *to* the DB.  

What is middleware?

> They are like a translation layer that helps communications between distributed applications.  

What does app.use(express.json()) do?  

> Enables using ExpressJS functions and properties, so an API server can be built and configured.  

What does the /:id mean in a route?  

> The Client is sending either a POST or DELETE verb, and a URL with the unique ID of a record that it wants to retreive, update, or remove from the store.  

What is the difference between PUT and PATCH?  

> PUT: The client sends an entire JSON object with loaded properties to make an udpate to an *existing* entity on the API server.  
> PATCH: The client sends a *partial* JSON object with only the properties that are to be changed (and their values).  

How do you make a default value in a schema?  

> Apply the 'default:' keyword. See the following example, sourced from *[Mongoose API, accessed 28-Apr-22]*:

```js
new Schema({
  name: {type: String, default: 'foo'}  //  value
  timeStamp: {type: Date, default: Date.now}  //  function
})
```

[Mongoos API Page](https://mongoosejs.com/docs/2.7.x/docs/defaults.html)  

What does a 500 error status code mean?

> A server-side error has occurred, specifically 'Internal Server Puppy'.

[HTTP Status Dogs](https://httpstatusdogs.com/)  

What is the difference between a status 200 and a status 201?  

> 200 just says "Request received and accepted".  
> 201 adds "Your request was processed and a new resource now exists".  

## References

[Which HTTP Status Code to Use for Every CRUD App](https://www.moesif.com/blog/technical/api-design/Which-HTTP-Status-Code-To-Use-For-Every-CRUD-App/)  
Web Dev Simplified [Build REST API with Node Express and Mongo](https://www.youtube.com/channel/UCFbNIlppjAuEX4znoulh0Cw)  

## Footer

[Back to readme.md](../README.html)  
