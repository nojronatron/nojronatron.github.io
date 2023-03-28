# Monitoring Azure Resources

Collection of notes about monitoring Azure services.

## Overview

Monitor Azure Resources to provide feedback should something go wrong.

## Reactor Content

### Monitoring Tools

- Azure Advisor
- Service Health
- Monitor: Log Analytics
- Monitor: Alerts
- Insights ($$)

### Why Monitor?

Reliability: Ensure improved continuity.

Security: Detect threats and vulnerabilities.

Performance: Improve speed based on current performance inputs.

Operational Excellence: Improve process and workflow efficiency.

Cost: Reduce overall Azure spending through optimizations.

### Azure Advisor

Regularly recommends workload improvements.

Advises on reliability, security, performance, OpExcellence, and Costs.

Provides an overal Score, Impacted Resources count, and Security Alerts count.

Provides links to quick fixes if they are available (e.g. Security Alerts quick fix).

Recommended to _start_ with Azure Advisor to get ramped up quickly with monitoring and improvements.

### Service Health

Portal includes view on:

- Service Issues
- Planned Maintenance
- Health Advisories
- Security Advisories

Also has a health history view, insight into resource health, and provides health alerts.

### Azure Monitor

Global service takes information from workloads, ifrastrucutre, azure platofrm, and custom reesources.

Generates logs based on the inputs.

Use to monitor specific thresholds to stay on top of performance, security, and costs.

Allows creation of dashboards and the ability to query the data, and design custom telemetry.

Application Insights is tied-in to Azure Monitor.

Workbooks: Create custom performance analysis charts and views/layouts with selected metrics.

Allows publishing to Azure Dashboards.

Integrates with the following for a variety of visualization sources:

- PowerBI
- Grafana
- Azure Workbooks
- Azure Dashboards

Metric Explorer: Create a visualization based on specified metrics, suitable for an Azure Dashboard view.

#### Azure Monitor Alerts

Create Alert Rules with static or dynamic thresholds.

Uses logical operators to determine thesholds and alert conditions.

Multiple sets (cascading?) of conditions can be configured within an alert.

Notification Action Group is used to configure _who_ will receive notifications from the alert.

Supports Email, SMS, _voice messaging_, and Mobile App notifications.

Action Groups are used to execute something based on the Alert:

- Automation Runbook i.e. PowerShell, AzCLI
- Azure Function i.e. Python script function
- Event Hub
- ITSM i.e. ticket management system e.g. ServiceNow etc
- Logic App i.e. Code-free, graphical UI implementation e.g. Jira, SAP, etc
- Webhooks (including secure)

### Log Analytics

Uses a SQL-like language.

Provides results that can be:

- Pinned to Azure Dashboard, which will render as a chart.
- Examined in tabular format.

### Application Map

Displays a map of how the AppService and Azure services and resources are connected and interact.

### Application Insights Usage Section

Users, Sessions, Events, Funnels, User Flows, and more.

User Flows: How are users are using the app, displayed in a graphical form. Funnels should be used in conjunction with User Flows.

### Live Metrics

As events happen, they are displayed in a log view as well as graphical representations.

### Application Insights

Has a cost.

Monitors applications, VMs, Storage Accounts, Containers, Networks, Databases, Key Vaults, and more.

### Azure Dashboards

Create custom Azure Dashboards and include Resources _and Service Health, Monitor, and Application Insights_ widgets.

## Resources

Johan Myburgh - MSFT Technical Trainer (MSFT UK) and Cloud Solution Architect: @sayedimac; LinkedIn: aka.ms/johan

aka.ms/AZ900LM

aka.ms/AZ900EP10LM

Azure Support `@AzureSupport`

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
