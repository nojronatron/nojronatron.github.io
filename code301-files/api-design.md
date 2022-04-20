# Read08 API Design

## Index

## API Web Design Best Practices

Source: Designing REST API for HTTP [Microsoft Docs](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)  

## Q and A

What does REST stand for?

> REpresentational State Transfer.  

REST APIs are designed around *resources*.

What is an identifier of a resource? Give an example.

> The unique URI of the resources. `https://docs.microsoft.com`  

What are the most common HTTP verbs?

> GET, PUT, POST, PATCH, DELETE

What should the URIs be based on?

> Create separate URIs for individual resources.

Give an example of a good URI.

> URI is based on the NOUNS of what it is, and is simple not complex.  
> Example: To get a list of products in inventory a URI might be `https://this-co.com/inventory` and would only accept a GET verb.
> Use plural endpoint names for APIs that return collections of items i.e. `https://this-co.com/orders` returns a list of orders.

What does it mean to have a ‘chatty’ web API? Is this a good or a bad thing?

> APIs that expose a large number of small resources. This is a bad thing as it creates unnecessary load on the web server.  

What status code does a successful GET request return?

> HTTP 200 (OK)  

What status code does an unsuccessful GET request return?

> HTTP 404 (Not Found) or HTTP 204 (No Content).  

What status code does a successful POST request return?

> HTTP 201 (Created)

What status code does a successful DELETE request return?

> HTTP 204 (No Content)

## RegEx Readings To Review

Media-Temples [RexExr](https://regexr.com/)  
Medium.com [RegEx Cheatsheet](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285)  
[Regular Expressions 101](https://regex101.com/)  

## References

Antipatterns:

[Chatty IO](https://docs.microsoft.com/en-us/azure/architecture/antipatterns/chatty-io/)  
[Extreneous Fetching](https://docs.microsoft.com/en-us/azure/architecture/antipatterns/extraneous-fetching/)  
[MSFT REST API Guidelines](https://docs.microsoft.com/en-us/azure/architecture/antipatterns/extraneous-fetching/)  
[Web API Checklist](https://mathieu.fenniak.net/the-api-checklist)  
[Open API Initiative](https://www.openapis.org/)  

## Footer

Back to [readme.md](../README.html)  
