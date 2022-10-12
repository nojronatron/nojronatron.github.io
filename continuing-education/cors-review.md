# Cross Origin Resource Sharing

CORS is a safety feature that restricts certain types of traffic between web apps and servers.

In past projects I have run into CORS-related issues and it has taken lots of time to resolve these.

This reference documentation is meant to be a high-level review of how and why CORS works, with links to references to more detail.

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

## Preflight Requests with Credentials

Wildcard *not* allowed in 'Access-Control-Allow-Origin' response header.

Response header must have explicit allow origin list.

Wildcard *not* allowed in 'Access-Control-Allow-Headers' response header.

Response header must have explicit allow headers list.

Wildcard *not* allowed in 'Acces-Control-Allow-Methods' response header.

Response header must have explicit allow methods list.

## Third Party Cookies

Subject to cookie policies.

## HTTP Response Headers

- access-control-allow-origin
- access-control-expose-headers
- access-control-max-age
- access-control-allow-credentials (this means browser will automatically add credentials, unlike implementing credentials in code)
- access-control-allow-methods
- access-control-allow-headers

## HTTP Request Headers

- origin
- access-control-request-method
- access-control-request-headers

## Key Takeaways: Jake Achibald

See [Resources](#resources) for the blog post where I took these key takeaways:

- `Content-type`: Tells the server what content to except from the caller.
- `X-Content-Type-Options: nosniff`: Header tells server to not parse content unless content-type is set. This covers lots of 'other origin' requests too, and led to protection called CORB.
- `SameSite` cookie attribute: The 2nd site opts-in to cookies sent with the request (e.g. login state).
- Frames presented a cross-site origin problem that led to the `same-origin` policy.
- An origin is the web address *from the protocol through the domain including the port*, and is the 'referer' aka origin of the page that made the request.
- `XMLHttpRequest` grew out of `new ActiveXObject('Microsoft.XMLHTTP')` and requires same-origin.
- A 'site' is the domain name of an equivalent 'origin'.
- There is something called a 'public suffix list' that all browsers use that helps distinguish between same-site and same-origin addresses.
- Flash went with a resource opt-in model based on cross-domain XLM files that became difficult to manage (of course) and required multiple requests from callers.
- If both sides had an opt-in, they can declare happy origins using `postMessage` -- this worked for frame-to-frame traffic.
- Opt-in via HTTP Header `Access-Control-Allow-Origin: *` (used today).
- Troubleshoot CORS issues: Open Network DevTools and look for `Sec-Fetch-Mode` header, which shows 'cors' or 'no-cors' (Chrome, Firefox).
- To force non-cors to a cors request, implement `crossorigin` attribute e.g. `<link crossorigin rel="" href="" />`
- CORS requests are by default made *without* credentials. Same-origin requests include cookies, or client certs, or Authorization header, or Set-Cookie.
- Not all websites accept `origin` for all requests (e.g. WebSocket, POST, GET, etc) as it triggers a 'cors' flag so does not work.
- All headers are case-insensitive keys, but *case sensitive* values.
- Headers can be exposed (except protected ones like `Set-Cookie`). `Access-Control-Expose-Headers:` can be used with wildcard or certain header types.
- Browser Caches have partitions for caching credentialed requests, although implementations are different.
- There are additional implications with long-term caching. In short, change the URL/Name in `Access-Control-Allow-Origin` so the client gets a new header, rather than using the cached one.
- When CDNs or browser cache reuses a response with private data, that data should be considered exposed: Non-cors fetch -> Response goes into cache -> cors fetch for same -> Cache returns original reponse. Include `Vary: Cookie` so that 'only cached version of this state of Cookie header match to original request can be served'. `Vary: Origin` can be used as a flag to indicate a cors request (but is not a guarantee). `Vary: Origin, Cookie` allows checking for *both* which can help work around this issue.
- No private data? Use `Access-Control-Allow-Origin: *`.
- Sometimes contains private data (per cookies)? Use both `Access-Control-Allow-Origin:*` and `Vary: Cookie`. This fixes browser and CDN Cache handling of cors requests with private data.
- Avoid using `Access-Control-Allow-Origin: *` if serving secured data, else it *will* leak elsewhere as a caller can send it anywhere.

### Adding Credentials

Add credentials back in to CORS requests:

Using "fetch": `const response = await fetch(url, { credentials: 'include', });`
Using HTML: `<img crossorigin="use-credentials" src="" />`. Response must contain access control allow credentials and origin headers as well as 'Vary: Cookie Origin`!

### Preflight

Requests that browser API's *don't generally make*, it is an 'unusual request' from the perspective of cors.

Request type determines 'usual': `GET`, `HEAD`, or `POST`.

Request headers that are 'unusual': Headers not on a 'safelist'.

Headers `Access-Control-Request-Method: ...` and `Access-Control-Request-Headers: item, item2, ...` with a method of `Options` are sent to the destination URL. No credentials are sent in preflight request.

Preflight server response could be happy or not:

happy:

```text
Access-Control-Max-Age: seconds-in-effect
Access-Control-Allow-Methods: unusual-methods-to-allow
Access-Control-Allow-Headers: unusual-headers-to-allow
```

FORBIDDEN LIST: Browser-controlled list of headers that are always stripped from cors requests.

Preflight response must pass CORS check so status code must be in 200's and response headers must include:

```text
Access-Control-Allow-Origin
Access-Control-Allow-Credentials: true
```

*Remember*: Access-Control-Allow-Credentials means *the browser* is *automatically* adding credentials to the request, *not* implemented custom headers!

After Preflight response is received *then* the actual request can be sent.

The post-preflight request *must also pass cors tests* or it will be forbidden or ignored.

Note: HTTP Method names *might be case sensitive*, meaning the browser might require `Access-Control-Allow-Methods` names to be UPPER-CASED, else they will not pass the check. It is okay to duplicate the method name in Pascal-Case and UPPER-CASE in the same header.

## General Notes

Cookie Header can be considered a Credential!

## Resources

Cross Origin Resource Sharing [on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

[Web Dev Simplified: CORS in 6 minutes](https://www.youtube.com/watch?v=PNtFSVU-YTI)

[Jake Archibald's blog page](https://jakearchibald.com/2021/cors/)

## Footer

Return to [root README](../README.html)
