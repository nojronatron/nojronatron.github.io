# Notes on an External Article at diveinto.html5doctor.com  

[HTML5 Dr. on Local Storage For Web Applications](http://diveinto.html5doctor.com/storage.html)  

## Overview

Desktop Apps have had advantage over web apps, where there are plenty of storage possibilities and if the right one does not already exist, a desktop app developer can invent one.

WebApps have been stuck with cookies:

- Plain-text
- Limited to 4K Bytes
- Can slow a website down

WebApps want more storage space, that persists between browser refresh, and is not transmitted to the server.

## Hacks Before HTML5

MSFT introduced DHTML userData in Internet Explorer which held up to 640K.
Flash Cookies (Local Shared Objects) came next.  
Brad Neuburg created AMASS (AJAX Mass Store System) to initeroperate with LSO, and later updated it to work with javascript (DOJO).  
Google added a browser plug-in "Gears", an API for an embeded SQLite instance.  
DOJO was updated to be a super-API for all these, called DOJOX.  

LocalStorage nowadays is either:

1. Tied to a specific browser, or
2. Provided only through a 3rd party plug-in

## Introducing HTML5 Storage

HTML5 Storage == Web Storage == LocalStorage == DOM Storage

*but not all necessarily equal*, rather, similar.  

HTML5: KVP storage in the browser, similar to cookies. Survives refresh and browser or tab closure. Never transmitted across the wire. *Available in all modern browsers*.  

### Detecting HTML5 Storage

Options:  

- Run a function in JS to detect it (see the article for a sample).  
- Utilize *Modernizr.localstorage* to test if window.localstorage is available.  

### Using HTML5 Storage

KVP Keys are strings.  
KVP Values can by any JS Object type, but is stored as a string (in the end).  
Calling 'set' to an existing Key will overwrite whatever value is already stored there.  

### Tracking Changes to HTML5 Storage Area

A DOM 'storage' event could be fired if any of the following actually make a change:

`setItem()`
`removeItem()`
`clear()`

The storageEvent object can report:

- The named key that was added/removed/modified.
- The previous value of a KVP (or null on first add).
- The latest new value KVP (null if removed).
- URL (or URI) of page thta called the storage change.

All are *non-cancellable*.

### HTML5 Storage Limitations in Current Browsers

- 5 Megabytes: Storage allocated to each 'origin'. Recall these are all stored as String type.
- QUOTA_EXCEEDED_ERR: The error thrown when 5MB is exceeded.
- no: You cannot increase the QUOTA.

## HTML5 Storage in Action

There are some rules to remember and good things to do when interacting with HTML5 Local Storage:

- Remember that items are stored *as Strings*.  
- When retreiving items, the value should be *coerced* into the datatype you expect.  
- Test Local Storage for existing KVP's to simulate 'resume game' type behavior.  

## Beyond Named KVPs

Google Gears inspired Web SQL Database spec, or "WebDB".  
Enables simple js access to a local SQLite DB layer:  

`openDatabase();`

`obj.executeSql("sql_statement");`

Yes, that's right, Select, Update, Insert, and Delete statements are supported.  

### Web SQL DB Support

- IE: ?
- Firefox: ?
- Safari: 4.0+  
- Chrome: 4.0+  
- Opera: 10.5+  
- IPhone: 3.0+  
- Android: 2.0+  

### WebSimpleDB

AKA 'Indexed Database API' AKA 'IndexedDB'.  

- IS A: Object store.
- Similar to SQL databse e.g. records and tables etc.  
- Transactions, cursors, fields, etc.

*However* it is *not* structured:

- No support for `select * from users where ...`
- Methods are provided to open the DB, enumerate the records, and compare values.

IndexedDB does not enjoy support across all browsers.  

## References

The article itself has a vast number of references to HTML5 Storage, WebSQL, IndexedDB, and the history of persistent storage in browsers.  
A side comparison of [IndexedDB and Web SQL Database](http://hacks.mozilla.org/2010/06/comparing-indexeddb-and-webdatabase/)  

[Back to index in readme](./README.md)
