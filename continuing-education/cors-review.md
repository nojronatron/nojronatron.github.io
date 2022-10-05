# Cross Origin Resource Sharing

CORS is a safety feature that restricts certain types of traffic between web apps and servers.

## Overview

CORS: Cross Origin Resource Sharing [on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

- By default, a Browser should *not* share sensitive data with another website.
- Outside of the browser, your environment won't have access to Browser-stored sensitive data.
- Sensitive data includes: Some cookies; in-browser cache; Java Web Tokens (JWTs); Local Storage.
- You don't have to change any CORS settings if you are not in the browser environment.
- Scripts might have access to a local file system and are blocked or restricted by default.
- APIs like XMLHttpRequest and Fetch mitigate risks of cross-origin HTTP requests and follow 'same-origin' policy to limit requests from same origin the application was loaded from.
- Additional CORS Headers are required to allow a request from another origin (from where the application was loaded from).

## Requests That Use CORS

- Web Fonts and CSS '@font-face'.
- WebGL textures.
- Images/Video frames: drawImage() => canvas.
- CSS Shapes from images.

## Simple Requests

These do *not* trigger CORS Preflight checks.

Simple Requests meet the following conditions:

- GET or HEAD or POST
- Headers that are auto-set by user agent
- Manually set Headers: Accept; Accept-Language; Content-Language; Content-Type; Range (with limits)
- Media Types: application/x-ww-form-urlencoded; multipart/form-data; text/plain
- Requests made using XMLHttpRequest *and* do not include Event Listeners (e.g. upload progress monitor)
- No 'ReadableStream' object in request

Note: Webkit and Safari have som additional limitations.

## Simple Request Example Overview

An XHR might cause browser to send a simple request that will include 'Origin: https://mysite.foo'.

Server might respond 'HTTP/1.1 200 OK' and include 'Access-Control-Allow-Origin: *' which means resource can be accessed by any origin.

If the server wanted to restrict to specific origins it would instead send: 'Access-Control-Allow-Origin: https://mysite.foo'.

*Note*: Credentialed requests *must* include a non-wildcard 'Access-Control-Allow-Origin' header response.

## Preflighted Requests

See full explanation of [access control scenarios at MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#examples_of_access_control_scenarios).

Browser sends an HTTP Req using 'OPTIONS'. This asks the server if request is safe to send.

A request might include a custom XHR Header and a 'Content-Type: text/xml' => Both of these make this a Preflighted Request and *not* a Simple Request.

The server replies with CORS origin URL, allowed methods, the allowed Headers (including allowed custom headers), and an age (expiration).

The client can then be sent to the server, and the Server will send the appropriate response.

*Note*: 'Access-Control-Request-*' headers are only needed for the OPTIONS request.

## Preflight Requests and Redirects

There is lingering behavior in browsers that completely disallows redirects in a Preflight Request type.

To work around this:

- Change server to avoid preflight or allow redirect.
- Change client request to a Simple Request (avoiding Preflight).

If those options are not possible:

- Use a Simple Request (Response.url or XMLHTttpRequest.responseURL) to get preflighted URL info.
- Make 2nd request using URL from above response.

*Note*: Authorization Headers in the request will always trigger Preflight Requests. This means that server-side changes must be made to work around the issue.

## Requests with Credentials

Credentials are not sent by default in XHR (request) or Fetch invokations.

XRH must include 'WithCredentials' flag (see code example) to allow cookie-setting by separate URL.

This gets a little complicated. Check out the [example on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#requests_with_credentials) that details what is going on and why.

## Preflight Requets with Credentials

Wildcard *not* allowed in 'Access-Control-Allow-Origin' response header.

Response header must have explicit allow origin list.

Wildcard *not* allowed in 'Access-Control-Allow-Headers' response header.

Response header must have explicit allow headers list.

Wildcard *not* allowed in 'Acces-Control-Allow-Methods' response header.

Response header must have explicit allow methods list.



## General Notes

Cookie Header can be considered a Credential!

## Footer

Return to [root README](../README.html)
