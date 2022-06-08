# Spring Tutorial on OAuth

Read the tutorial and optionally walk through the tutorial in code (not required).

## Reference

Spring [Tutorial on OAuth](https://spring.io/guides/tutorials/spring-boot-oauth2/)

## Spring Boot and OAuth2

Requirements: OAuth 2.0 (native in) Spring Boot

SSO providers like Google and GitHub can be integrated into your authentication flow.

OAuth with Spring Boot can be applied to simple websites - the demo code is just a couple web pages including a static home/index page.

## SSO with GitHub

1. Add Spring Security as a dependency.
1. Include Spring OAuth 2.0 Client Starter.
1. Create a home/splash page and add the JS canned code suggested in the reference article.
1. Add a new GitHub app => New OAuth App => (enter app homepage e.g. localhost:8080) => add callback URL e.g. 'http://localhost:8080/login/oauth2/code/github' => Register App
1. Config 'application.yml' (see demo code at source webiste).
1. github-client-id and github-client-secret are placeholders, so replace them with the OAuth 2.0 creds created with GitHub, above.
1. SSO enables sign-on through browser sessions close/openings, etc.
1. Clear your browser cache => local credentials: This clears the SSO cache that was set via 'Set-Cookie' and 'JSESSIONID'.
1. Add a Welcome! page by marking some HTML elements with "container unauthenticated", "/oaugh2/authoriation/github", "container authenticated", and 'user'.
1. The '/user' endpoint is server-side and returns the currently-logged-in user. SocialApplication.java code is included in the reference article.
1. *Note* Annotations '@RestController', '@GetMapping', 'OAuth2User' are injects to the handler above.
1. Enable a public homepage by extending WebSecurityConfigurerAdapter in SocialApplication.java. See the code in the reference site.
1. The '@SpringBootAnnotation' annotation attaches security filter chain configuration for the OAuth 2.0 processor.
1. Allow '/', '/error', '/webjars/**' for general operation of the website.
1. Configure AJAX endpoints to respond with 401 (instead of defaulting to redirect to login page) => Configure 'authenticationEntryPoint' to do this.
1. Add a Logout button client-side (via JS) that will ask the server to cancel the OAuth cookie. Review the code at the referenced website.
1. Add a logout endpoint '/logout' (clears session and invalidates cookie) via the WebSecurityConfigureAdapter.java.configure() method. Keep in mind the logout is a *POST* call. See the reference page code block.
1. Add a filter to create a cookie that emulates the XSRF-TOKEN type cookie, within the WebSecurityConfigurerAdapter.java.config() method. See the code.
1. Add js-cookie library to enable adding CSRF Token (via the backend), then reference it in the index.html file using some ajax. See code on the site.

## SSO with Google API


## Footer

Back to [Root Readme](../README.md)
