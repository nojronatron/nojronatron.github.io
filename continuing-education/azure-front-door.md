# Azure Front Door

Azure Front Door is a secure, modern content delivery network service in Azure with performance and security features for cloud-based web applications.

## Features

- Simple Pricing: Monthly charge per Policy and custom Rule Set charges are built-in.
- CDN: High-bandwidth content through globally-zoned caching to Azure WebApps, Cloud Services, or Storage, or any publicly accessibel web server.
- Application Firewall: Protects web application from common exploits, vulnerabilities.
- High Availability Service: Global Edge Network deployments.
- Performance: Low-latency web pages optimized via geographically strategic locations.
- Custom Domain Support: Bring an existing domain with user content.

## Lifecycle

- 15-Aug-2025: Azure CDN (classic) no longer supports new domain onboarding. Use Azure Front Door Standard or Premium instead.
- 15-Aug-2025: Azure CDN (classic) no longer supports Managed Certificates. Switch to BYOC or Azure Front Door Standard or Premium.
- 30-Sept-2027: Azure CDN Standard will be retired. Migrate to Azure Frond Door Standard or Premium.
- 15-Jan-2025: Azure CdN from EdgeIO was retired.

## Tiers and SKUs

### Tiers

Classic: Entry level. Bolsters Azure CDN and Azure WebApp Firewall services.

Standard: Adds seamless content delivery.

Premium: Improves security over other tiers.

### Standard

- CDN optimization
- Static and Dynamic content acceleration
- Global Load Balancing
- SSL Offloading
- Domain and Certificate Management
- Enhanced Traffic Analysis
- Basic security features

### Premium

- Azure Front Door Standard features
- Extensive security across WebApp Firewall
- Private Link support
- Integration with MS Threat Intelligence and security analytics

## Content Delivery Optimizations

- Anycast Protocol
- TCP Layer 7 optimization
- Smart HTTP/S client request routing using multiple methods

### Routing Optimizations

Routing Configuration Options:

- Latency: Send requests to lowest-latency backend, with sensitivity range setting.
- Priority: Set a primary backend service.
- Weighted: Assigned to backends to distribute load.
- Session Affinity to frontend hosts or domains maintains user session to same 'backend'.

### CDN Features

- Dynamic Site Accelleration
- CDN Caching Rules
- HTTPS Custom Domain Support
- Azure Diagnostic Logging
- File Compression
- Geo-filtering

### Content Security

- WebApp Firewall
- Located at network edge (at network ingress points)
- Managed Rule Sets
- Custom Rules

Rules are Conditions, configured with Priority, an Action, and a mode of either _Detection_ (event logging only) or _Prevention_ (performs an action)

## When To Use Azure Front Door

Need a CDN with Web Application firewall? Use Azure Front Door Standard which includes:

- CDN optimizations.
- Static and dynamic content acceleration.
- GLobal load balancing.
- SSL Offload.
- Domain and certificate management.
- Enhanced traffic analytcs.
- Basic security capabilities.

Your solution requires more than what these services provide:

- Azure Traffic Manager: DNS-based global routing (which lacks TLS termination, SSL offloading, and App-layer processing).
- Azure Application Gateway: Load-balance servers (in single Region) at Application layer.
- Affordable and simplified Azure TM and Azure App Gateway deployments with some cost effeciencies.

Need dynamic and static content delivery service:

- Scalability: Use Azure Front Door to simplify scale out-in operations.
- Pricing: Monthly charge or hourly billing? Ok for added charges for custom Rules?
- Content Delivery: Simple optimization without extra security? Front Door Standard.
- Security: Enhanced security required? Front Door Premium.

Scalability a requirement? Define, manage, and monitor web traffic global routing, with global failover.

Pricing constraints? Use Front Door Standard/Premium billing based on:

- Fixed hourly charges.
- Egress and Ingress data.
- Requests per (timeframe?) to Azure Front Door edge locations.

A high level of CDN security is required? Select Azure Front Door Premium which includes:

- Web App Firewall enhaced security (over Standard).
- BOT protection.
- Private Link support.
- Integration with Threat Intelligence and security analytics.

## Azure CDN Notes

Azure CDN Operates at the Application Layer:

- Dynamic site acceleration.
- Content delivery network caching rules.
- HTTPS custom domain support.
- Azure Diagnostic logs.
- File compression.
- Geo-filtering.

Creating an Azure CDN requires:

- An Azure Subscription.
- CDN Network Profile with list of endpoint profiles.

Azure CDN Limitations:

- Number of CDN Profiles.
- Number of endpoints in a CDN Profile.
- Number of custom domains mapped to an endpoint.
- Lack of Dynamic Site Delivery.
- Only CNAM based certificate validation.
- Lacks server variables and regex in rules engine.
- Does not support custom WebApp Firewall Rules.
- No support for Private Link Connections to Origin.
- Lacks integration with Azure Analytics.
- Does not integrate with Azure Policy.
- Lacks support for Managed Identities and Azure Key Vault.

Use Azure Front Door Standard or Premium since AFD Classic and Azure CDN Classic will be retired.

## References

- [Azure CDN Overview](https://learn.microsoft.com/en-us/azure/cdn/cdn-overview)
- [Compare Azure CDN and AFD](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-cdn-comparison#feature-comparison?azure-portal=true)
- [What is Azure WEbApp Firewall on Azure App Gateway?](https://learn.microsoft.com/en-us/azure/web-application-firewall/ag/ag-overview)
- [What is AFD?](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)
- [AFD Best Practices](https://learn.microsoft.com/en-us/azure/frontdoor/best-practices?source=recommendations)

## Footer

Return to [ContEd Index](./conted-index.md)

Return to [Root README](../README.md)
