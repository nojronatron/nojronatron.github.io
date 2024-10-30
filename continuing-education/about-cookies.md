# Notes About Web Cookies

Other areas of this repository have notes about cookies, and they are referenced below. This page will be dedicated to specific considerations and technical details around cookies.

## Table of Contents

- [Cookies Having Independent Partitioned State (CHIPS)](#cookies-having-independent-partitioned-state-chips)
- [Third Party Cookies](#third-party-cookies)
- [References](#references)
- [Footer](#footer)

## Cookies Having Independent Partitioned State (CHIPS)

AKA "Partitioned Cookies"

- Opt-in a cookie to partitioned storage.
- A separate cookie-jar is used.
- Are _double-keyed_ by the origin that sets them and the origin of the top-level page.

Protections and Benefits:

- Third-party cookies could track users across _unrelated top-level sites_.
- Can only be read by the top-level site that sets them _and_ the origin of the top-level page.
- Blocks cross-site tracking.
- Allows legitimate uses of third party cookies (e.g. persisting state of embedded objects or widgest across domains, or persisting CDN config or headles CMS provider information).
- Binding a Partitioned Cookie to a domain ensures the cookie won't be shared between subdomains.

What about CHIPS?

- Allows 3rd-party content embeds across different subdomains of a site to access cookies set by that content.
- Essentially, the partition key match occurs around the domain name and TLD, so sub-domains like `new.same-domain.tld` will actually match `same-domain.tld`.

Technical Details:

- Cookies were historically set using the host or domain name of the site that set them. This is known as the _host key_.
- When setting `partitioned` and `secure` flags, if the `__Host` prefix is also set, this binds the cookie to the current Domain (or subdomain).
- Paritioned cookies require being set with the `secure` flag.
- Third-party Cookies are set using _two keys_: `Host`, and `partition`. This means a single object containing _both keys_ is used as the cookie Key in memory. Another 3rd party sub-domain would _not match_ the one that is part of the object that is now the partitioned cookie key, so it is not accessible to that sub-domain to read, and a different cookies would have to be set.

Example HTTP Set-Cookie statement:

```text
Set-Cookie: __Host-{domain}={value}; SameSite=None; Secure; Path=/; Partitioned;
```

Compatible Browsers:

- Chrome
- Edge
- Firefox
- Opera
- Chrome Android
- Firefox for Android
- Opera Andoid
- Samsung Internet

Incompatible Browsers:

- Safari
- Safari on iOS
- WebView Android
- WebView on iOS

## Third Party Cookies

These are (slowly) being phased out but still very much in use.

## References

- Using [Cookies With Expressjs](./express-cookies-review.html)
- MDN [Cookies Having INdependent Partitioned State (CHIPS)](https://developer.mozilla.org/en-US/docs/Web/Privacy/Privacy_sandbox/Partitioned_cookies)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
