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



[Back to index in readme](./README.md)
