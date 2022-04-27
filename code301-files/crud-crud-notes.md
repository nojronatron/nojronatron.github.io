# More CRUD Readings

## Q and A

Which HTTP method would you use to update a record through an API?  

> PUT is used to update an existing record.  

Which REST methods require an ID parameter?  

> DELETE requires an :id.  

What’s the relationship between REST and CRUD?  

```text
REST        CRUD      Meaning
----        ----      -------
POST    =>  Create    Add an item to the server
GET     =>  Read      Read one or more item values from the server
PUT     =>  Update    Update an existing item at the server
DELETE  =>  Delete    Remove an existing item from the server
```

If you had to describe the process of creating a RESTful API in 5 steps, what would they be?

1. Deploy a database or data store of some sort.  
1. Deploy an API server with connectivity to the data store.  
1. Add required middleware like CORS or other wingdings as your API design requires.  
1. Create routes for each REST operation, translating to CRUD operation(s).  
1. Implement validation and error handling mechanisms.  

## References

[CRUD Basics](https://medium.com/geekculture/crud-operations-explained-2a44096e9c88)  
[Speed Coding: Build a CRUD API](https://www.youtube.com/watch?v=EzNcBhSv1Wo)  

## Footer

[Back to readme.md](../README.html)  
