# Reading Notes on Spring Authentication and Authorization

## Intro to Spring Security

https://spring.io/guides/topicals/spring-security-architecture/

### Implementation Notes

Use Filters and Method Annotations.

Spring Boot offers default behavior for application security.

Authentication: Proof of who you are.

### Authentication

Use AuthenticationManager.

AuthenticationManager's Authenticate method functionality:

- Return an Authentication (true/false) if it can verify a user/service principal.
- Throw an AuthenticationException when a principal is not authenticate-able.
- Return Null if the function "cannot decide".

#### Provider Manager

Common implementatino of AuthenticationManager.

Chains AuthenticationManager instances.

Adds a method that describes if a specific authentication type is supported, via a Boolean return type.

The Type must be recognizable to AuthenticationManager otherwise it will just be skipped.

AuthenticationManager instances can be dedicated to each protected resource, or groups of resources.

ProviderManager acts as a "Parent" to authentication Providers.

### Customization

AuthenticationManagerBuilder: For In-memory, JDBC, or LDAP user details.

AuthenticationManagerBuilder can also be used to create a custom UserDetailsService.

Configuring AuthenticationManager: Add `@AutoWired` to the method definition and add the 'builder' and 'dataSource' params in the params list, then use chaining:

```java
// snipped from spring.io guides: security and architecture
builder.jdbcAuthentication().dataSource(dataSource).withUser(string).password(secret).roles("ROLE");
```

A Global AuthenticationManager is available through Spring that can be used on its own or you can '@Override' it however that will change the scope to the local scope and will no longer be exposed at the global level.

### Authorization

Authorization: Dis/allowance for what a requestor can/not do.

### Access Controls, Authz

Manage Authz AFTER Authentication (Authn).

Leverage AccessDecisionManager for AC and Authz.

ConfigAttributes decorations needed for AccessDecisionVoter instances to make their decisions.

AccessDecisionVoters are scoped to an authentication and a secure object decorated with ConfigAttributes.

A 'vote' is an integer return based on AccessDecisionVoter's results comparing configAttributes and classes (clazzes?).

Generics are implemented in AccessDecisionManager and AccessDecisionVoter so that any resources can be tested for access control(s).

ConfigAttribute is an Interface type, with one Generic method that returns a String, representing access controls (set by the owner).

Access controls in the returned ConfigAttribute string are prefixed "ROLE_" and use symantic terminology like "ROLE_USER" or "ROLE_ADMIN".

#### SpEL

Spring Expression Language.

Example given *[spring.io/guides/topicals/spring-security-architecture]*:

```java
isFullyAuthenticated() && hasRole('user')
```

AccessDecisionVoters support SpEL.

SecurityExpressionRoot and/or SecurityExpressionHandler can be implemented to support a wider range of expessions.

### Web Security

Spring Security for Web Tier (UIs and HTTP back ends) is based on Filters servlet.

WRRC looks like this:

`[Client] <==> [Filter] <==>[FilterChainProxy] <==>[Filter] <==> [Servlet]`

Servlets handle requests synchronously.

Filters are chained so they are applied in-order on a per-request basis.

Each filter has VETO and MODIFICATION powers upon the request anywhere in the chain.

Use `@Order` on `@Beans<Filter>` to implement filters.

Alternatively implemented `Ordered` as part of a FilterRegistrationBean.

SessionRepositoryFilter (Spring Session) includes a 'DEFAULT_ORDER = Integer.MIN_VALUE + 50' so it is early in the chain.

Spring Security is of type FilterChainProxy and is a single Filter for chaining.

The Spring Security security filter is a Bean in the ApplicationContext and will apply to every request by default (installed by default too).

FilterChainProxy is a wrapper with specialized Filters within it.

DelegatingFilterProxy is usually installed in the container and does NOT have to be a Bean.

DelegatingFilterProxy proxies to FilterChainProxy which IS always a Bean.

FilterChainProxy contains all the security logic within chained filters.

Only one Filter Chain handles a single request.

Each set of resources has WebSecurityConfigurerAdapter that defines unique order and request matching rules.

Overlapped rules boil down to the earliest-ordered-filter-chain wins.

### Request Matching for Dispatch and Authorization

Determines whether to apply itself to an HTTP request.

Once it is applied to the filter chain, no others are applied.

Fine-grained controls can still be within the filter chain using the HttpSecurity configurer.

There is sample code that demonstrates this concept.

*Remember*: Matchers apply to different processes and only one is a request matcher for the entire filter chain, the other is for selecting which access rule to apply.

### Combining Application Security Rules with Actuator Rules

Spring Boot Actuator: Used for management endpoints.

Add filter chain ordered *prior to* the actuator one.

*Remember*: Request Matchers include the actuator endpoint (presumedly it will not be applied otherwise).

### Method Security

Spring Security applies to Java methods too.

Methods are a "protected resource".

First, enable method security at the top level config for the application.

Second, decorate the method directly with `@Secured("ROLE_string")`

Security constraints can be enforce with annotations `@PreAuthorize` and `@PostAuthorize`

Basically, ref method params and return values in an expression to (apply the security rules?).

### Threads and Spring Security

Spring Security must be able to make authenticated security available to downstream "consumers".

Therefore Spring Security is thread-bound.

SecurityContextHolder has static convenience methods for manipulating SecurityContext (contains an Authentication instance).

Use `@RequestMapping` to access currently authn principals in a web endpoint.

### Process Secure Methods Asynchronously

SecurityContext is thread-bound.

'@Async' can be used for background processing *so long as the context is propagated* too.

'Runnable' and 'Callable' were mentioned as possibly used keywords involved with asynchronous execution.

Use AsuncConfigurer and set the Executor to the proper type to propagate the Security Context.

## Spring Auth Reference Notes

Codefellows Spring Auth [Cheat Sheet](https://github.com/codefellows/seattle-java-401d2/blob/master/SpringAuthCheatSheet.md)

Use this cheatsheet (by GitHub user mnfmnfm) as a template for setting up Spring Authentication.

## Footer

Back to root [Readme](../README.html)
